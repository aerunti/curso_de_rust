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

 você encontrará um 'hello word' semelhante a esse para substituir no arquivo src/main.rs: 


*    use actix_web::{get, post, web, App, HttpResponse, HttpServer, Responder};

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


