# Bem vindo ao Curso de Rust para Web


A elaboração desse curso tem por objetivo suprir uma lacuna do mercado: o material a respeito de desenvolvimento para web é geralmente limitado e superficial.

O potencial da Linguagem Rust para o desenvolvimento web pode ser demonstrado pelos Benchmarks da [TechEmpower](https://www.techempower.com/benchmarks/#section=data-r21): no round 21, 5 dos 10 frameworks mais rápidos são desenvolvidos em Rust. 

No entanto, a maior parte é experimental e não tem nenhuma ou pouca documentação disponível

## Stack

- actix-web
- sqlx
- postgresql

A escolha do actix é porque é documentado, assíncrono e tem bons resultados nos benchmarkings. 

Sqlx porque não é um ORM, e permite usar sql diretamente, o que permite usar a própria documentação do banco de daddos

Postgreql porque é o banco de dados relacional opensource mais avançado, com excelente desempenho, documentação e comunidade de desenvolvimento


# Objetivo do Curso

O objetivo do curso é construir um blog, apresentando funcionalidades que são comuns a qualquer aplicação web:

-autenticação: cadastro, login e perfis de usuários
-sessões: permanencia de dados durante a navegação do usuário
-cache: minimizar a computação de solicitações repetidas
-acesso e registro de dados: o cadastro e acesso a informações do banco de dados é essencial em qualquer aplicação web
-api: muitas aplicações exigem disponibilizar dados via api
-frontend: como utilizar um frontend para interação do usuário final
-deployment: como colocar a aplicação em produção. 

A partir dessas funcionalidades básicas, o aprendiz será capaz de implementar novas funcionalidades, adaptando dos exemplos apresentados. 

## Observações gerais

É importante observar que um curso busca desenvolver as habilidades básicas para que o aluno possa iniciar o desenvolvimento de atividades, mas não é exaustivo. 
Cabe a cada aluno entender que para o seu trabalho do dia a dia, ele deve ser capaz de buscar respostas para os novos desafios. 

Em programação, isso significa que deverá consultar a documentação da linguagem, dos frameworks e bibliotecas utilizados, e buscar soluções para os problemas de implementação que encontrar. 

Sendo assim, esse curso busca não apenas dar a resposta, mas demonstrar o processo que levou à resposta: a pergunta, a busca, o processo de escolha da melhor solução. É essa habilidade que irá permanecer no dia a dia do programador. 


# Como instalar o Rust

O [site do rust](https://www.rust-lang.org/pt-BR) tem orientações sobre como instalar o rust. 

o caminho curto, se você usa linux é 

    curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh

Se usa windows, consulte o site a respeito dos procedimentos específicos


# Começando com o Actix-web

É essencial que você consulte o [site do Actix web](), que mais cedo ou mais tarde você terá que consultar para uma explicação detalhada das funcionalidades

Para um caminho mais rápido, abra o seu terminal na sua pasta de projetos e execute o comando abaixo para criar um projeto para iniciar nossa jornada


    cargo new actix-hello-word

o comando irá gerar a seguinte estrutura:

    actix-hello-word/
    ├── Cargo.toml
    └── src
        └── main.rs

Como é o 'hello world' do actix? 

em [Getting Started](https://actix.rs/docs/getting-started), há um exemplo básico

Adicione ao arquivo Cargo.toml

    [dependencies]
    actix-web = "4"

opcionalmente, você pode utilizar ´´´cargo add actix-web´´´ para adicionar a versão mais recente do actix-web



 você encontrará um 'hello word' semelhante a esse para substituir no arquivo src/main.rs: 


    use actix_web::{get, post, web, App, HttpResponse, HttpServer, Responder};

    #[get("/")]
    async fn hello() -> impl Responder {
        HttpResponse::Ok().body("Hello world!")
    }

    #[post("/echo")]
    async fn echo(req_body: String) -> impl Responder {
        HttpResponse::Ok().body(req_body)
    }

    async fn manual_hello() -> impl Responder {
        HttpResponse::Ok().body("Hey there!")
    }
    #[actix_web::main]
    async fn main() -> std::io::Result<()> {
        HttpServer::new(|| {
            App::new()
                .service(hello)
                .service(echo)
                .route("/hey", web::get().to(manual_hello))
        })
        .bind(("127.0.0.1", 8080))?
        .run()
        .await
    }


Agora execute 

    cargo run

E acesse [http://localhost:8080/](http://localhost:8080/) no seu navegador

# usando templates

O actix-web não oferece uma template engine padrão. Há [várias opções em rust](https://crates.io/categories/template-engine), mas escolhemos [tera](https://tera.netlify.app/) após avaliar as opções e [benchmark](https://github.com/rosetta-rs/template-benchmarks-rs). 

Encontrei um exemplo [https://nivethan.dev/devlog/a-web-app-in-rust.html][https://nivethan.dev/devlog/a-web-app-in-rust.html] em que basicamente orienta:

a) adicione a engine ao Cargo.toml

    cargo add tera

b) crie um diretório templates

    mkdir templates

c)  crie um arquivo templates/index.html com o conteúdo:

    <!DOCTYPE html>
    <html lang="en">
        <head>
            <meta charset="utf-8">
            <title>{{title}}</title>
        </head>
        <body>
            Hello, {{name}}!
        </body>
    </html>

d) substitua o conteúdo de src/main.rs por 

    use actix_web::{HttpServer, App, web, HttpResponse, Responder};
    use tera::{Tera, Context};

    async fn index(tera: web::Data<Tera>) -> impl Responder {
        let mut data = Context::new();
        data.insert("title", "Hacker Clone");
        data.insert("name","Nivethan");

        let rendered = tera.render("index.html", &data).unwrap();
        HttpResponse::Ok().body(rendered)
    }

    #[actix_web::main]
    async fn main() -> std::io::Result<()> {
        HttpServer::new(|| {
            let tera = Tera::new("templates/**/*").unwrap();
            App::new()
                .data(tera)
                .route("/", web::get().to(index))
        })
        .bind("127.0.0.1:8000")?
        .run()
        .await
    }


Infelizmente, esse exemplo está desatualizado e não funciona com actix 4. 

No entanto encontrei um [exemplo de utilização do tera no repositório de exemplos do actix 4](https://github.com/actix/examples/tree/master/templating/tera)

Basicamente, com algumas alterações para funcionar fora do repositório, ficou assim o src/main.rs: 

    use std::collections::HashMap;

    use actix_web::{
        body::BoxBody,
        dev::ServiceResponse,
        http::{header::ContentType, StatusCode},
        middleware::{self, ErrorHandlerResponse, ErrorHandlers},
        web, App,HttpResponse, HttpServer, Responder, Result,
    };
    // use actix_web::respond::Html;
    use tera::Tera;

    // store tera template in application state
    async fn index(
        tera: web::Data<Tera>,
        query: web::Query<HashMap<String, String>>,
    ) -> impl Responder {
        let mut data = tera::Context::new();
        if let Some(name) = query.get("name") {
            data.insert("title", &name);
        } else{
            data.insert("title", "Hacker Clone");
        };
        
        data.insert("name","Nivethan");
        let rendered = tera.render("index.html", &data).unwrap();

        HttpResponse::Ok().body(rendered)
    }

    #[actix_web::main]
    async fn main() -> std::io::Result<()> {
        std::env::set_var("RUST_LOG", "actix_web=info");
        env_logger::init();

        println!("Listening on: 127.0.0.1:8080, open browser and visit have a try!");
        HttpServer::new(|| {
            let tera = Tera::new(concat!(env!("CARGO_MANIFEST_DIR"), "/templates/**/*")).unwrap();

            App::new()
                .app_data(web::Data::new(tera))
                .wrap(middleware::Logger::default()) // enable logger
                .service(web::resource("/").route(web::get().to(index)))
                .service(web::scope("").wrap(error_handlers()))
        })
        .bind(("127.0.0.1", 8080))?
        .run()
        .await
    }

    // Custom error handlers, to return HTML responses when an error occurs.
    fn error_handlers() -> ErrorHandlers<BoxBody> {
        ErrorHandlers::new().handler(StatusCode::NOT_FOUND, not_found)
    }

    // Error handler for a 404 Page not found error.
    fn not_found<B>(res: ServiceResponse<B>) -> Result<ErrorHandlerResponse<BoxBody>> {
        let response = get_error_response(&res, "Page not found");
        Ok(ErrorHandlerResponse::Response(ServiceResponse::new(
            res.into_parts().0,
            response.map_into_left_body(),
        )))
    }

    // Generic error handler.
    fn get_error_response<B>(res: &ServiceResponse<B>, error: &str) -> HttpResponse {
        let request = res.request();

        // Provide a fallback to a simple plain text response in case an error occurs during the
        // rendering of the error page.
        let fallback = |e: &str| {
            HttpResponse::build(res.status())
                .content_type(ContentType::plaintext())
                .body(e.to_string())
        };

        let tera = request.app_data::<web::Data<Tera>>().map(|t| t.get_ref());
        match tera {
            Some(tera) => {
                let mut context = tera::Context::new();
                context.insert("error", error);
                context.insert("status_code", res.status().as_str());
                let body = tera.render("error.html", &context);

                match body {
                    Ok(body) => HttpResponse::build(res.status())
                        .content_type(ContentType::html())
                        .body(body),
                    Err(_) => fallback(error),
                }
            }
            None => fallback(error),
        }
    }

Não esqueça de adicionar o env_logger no Cargo.toml

    cargo add env_logger


