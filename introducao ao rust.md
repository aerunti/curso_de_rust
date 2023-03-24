
# Introdução ao Rust

Rust é uma linguagem de programação que visa oferecer desempenho, confiabilidade e produtividade aos desenvolvedores. Rust é extremamente rápido e gerencia memória eficientemente: sem runtime ou garbage collector, podendo potencializar a performance de serviços críticos, rodar em sistemas embarcados, e facilmente integrar-se a outras linguagens. Rust também possui um rico sistema de tipos e um modelo de ownership que garantem segurança de memória e segurança de concorrência — e permitem que você elimine muitas categorias de erros durante a compilação. Além disso, Rust possui uma ótima documentação, um compilador amigável com mensagens de erros úteis, e ferramental de primeira qualidade — uma ferramenta integrada de compilação e gerenciamento de pacotes, suporte inteligente para múltiplos editores com autocompleção e inspeções de tipos, um formatador automático, e muito mais.

Rust pode ser usada para construir aplicações web, serviços de rede, ferramentas de linha de comando, sistemas embarcados, WebAssembly e muito mais . Rust possui uma comunidade ativa e diversa que contribui para o desenvolvimento da linguagem e do ecossistema. Rust também é usada por centenas de empresas ao redor do mundo em produção para criar soluções multiplataforma rápidas e eficientes. Software que você conhece e ama, como Firefox , Dropbox , e Cloudflare , usam Rust.



## Porque programar em Rust

Olá, leitores! Hoje eu vou falar sobre um assunto que me deixa muito animado: porque programar em Rust? Rust é uma linguagem de programação moderna, rápida e segura, que oferece muitas vantagens para quem quer desenvolver software de alta qualidade. Vamos ver alguns motivos para escolher Rust como sua próxima linguagem favorita!

- Rust é rápida: Rust é compilada para código nativo, o que significa que ela roda diretamente no processador, sem precisar de uma máquina virtual ou um interpretador. Isso garante um desempenho excelente, comparável ao de linguagens como C ou C++.
- Rust é segura: Rust tem um sistema de tipos e de gerenciamento de memória que previne erros comuns como estouro de buffer, vazamento de memória ou uso indevido de ponteiros. Rust também evita condições de corrida e outros problemas relacionados à concorrência, graças ao seu modelo de propriedade e empréstimo.
- Rust é expressiva: Rust tem uma sintaxe clara e concisa, que facilita a leitura e a escrita do código. Rust também tem recursos poderosos como macros, traits, enums e closures, que permitem abstrair conceitos complexos e criar soluções elegantes e reutilizáveis.

Esses são apenas alguns dos motivos pelos quais eu adoro programar em Rust. Se você ficou curioso e quer saber mais sobre essa linguagem incrível, eu recomendo que você visite o site oficial (https://www.rust-lang.org/) e comece a aprender hoje mesmo. Você não vai se arrepender!

## instalação 

Olá! Neste post, eu vou te ensinar como instalar o Rust, uma linguagem de programação poderosa e segura que pode ser usada para criar aplicações incríveis. Rust é uma linguagem que se preocupa com a performance, a confiabilidade e a expressividade. Ela tem um sistema de tipos que previne erros comuns em outras linguagens, como acesso inválido à memória, data races e null pointers. Ela também tem um gerenciador de pacotes integrado chamado Cargo, que facilita a criação e o gerenciamento de projetos em Rust.

Para instalar o Rust, você vai precisar de uma ferramenta chamada rustup, que é um instalador e um gerenciador de versões do Rust. Com o rustup, você pode escolher qual versão do Rust você quer usar (estável, beta ou nightly), quais componentes você quer instalar (como ferramentas para cross-compilação) e quais canais você quer acompanhar (como atualizações ou anúncios).

Se você estiver usando Windows, você pode baixar o instalador do rustup no site oficial do Rust: https://www.rust-lang.org/pt-BR/tools/install. Você pode precisar instalar o Visual Studio C++ Build tools se solicitado durante o processo de instalação. Se você estiver usando Linux ou macOS, você pode instalar o rustup pelo terminal com o seguinte comando:

    curl https://sh.rustup.rs -sSf | sh

Esse comando vai baixar e executar um script que vai verificar as dependências necessárias e instalar o rustup no seu sistema. Você vai precisar aceitar os termos de licença e escolher uma configuração padrão ou personalizada. O script também vai tentar configurar a variável de ambiente PATH para incluir o diretório onde as ferramentas do Rust são instaladas (~/.cargo/bin). Você pode verificar se a instalação foi bem sucedida rodando o seguinte comando:

    rustc --version

Esse comando vai mostrar a versão do compilador do Rust que você acabou de instalar. Se tudo der certo, você deve ver algo assim:

    rustc 1.57.0 (f1edd0429 2021-11-29)

Parabéns! Você acabou de instalar o Rust no seu computador! Agora você está pronto para começar a escrever seus próprios programas em Rust. Para isso, você pode usar o Cargo para criar e gerenciar seus projetos. O Cargo é uma ferramenta que cuida de várias tarefas para você, como compilar seu código, executar seus testes, gerar sua documentação e publicar sua biblioteca em crates.io (o repositório oficial de pacotes do Rust).

Para criar um novo projeto em Rust com o Cargo, basta rodar o seguinte comando:

    cargo new hello-rust

Esse comando vai criar um novo diretório chamado hello-rust com os seguintes arquivos:

    hello-rust
    |- Cargo.toml
    |- src
    |- main.rs

O arquivo Cargo.toml é o manifesto do seu projeto. Nele você encontra todos os metadados do seu projeto, como nome, versão, autores e dependências. O arquivo src/main.rs é onde você vai escrever seu código fonte em Rust. O Cargo já gera um programa "Hello, world!" para você! Você pode executar esse programa entrando no diretório recém criado e rodando o seguinte comando:

    cargo run

Esse comando vai compilar seu código e executá-lo em seguida. Você deve ver a seguinte saída no terminal:

    cargo run
    Compiling hello-rust v0.1.0 (/Users/aerun/rust/hello-rust)
        Finished dev [unoptimized + debuginfo] target(s) in 1.34s
        Running `target/debug/hello-rust`
    Hello, world!

Muito bem! Você acabou de escrever e executar seu primeiro programa em Rust! Agora você pode modificar seu código como quiser e explorar as possibilidades da linguagem.


## O que são crates do rust

Uma das grandes vantagens de Rust é o seu sistema de crates, que são pacotes de código reutilizável que podem ser facilmente integrados ao seu projeto.

As crates são unidades de compilação e distribuição do Rust. Elas podem ser executáveis ou bibliotecas. Uma crate é um conjunto de módulos, tipos, funções e outras definições que podem ser usados por outros programas ou crates.

As crates facilitam a organização do código, a reutilização de funcionalidades e a integração com outras bibliotecas. Além disso, elas permitem o gerenciamento de dependências através do Cargo, o gerenciador de pacotes do Rust.

Para criar uma crate executável, basta usar o comando `cargo new --bin nome_da_crate`. Para criar uma crate biblioteca, use `cargo new --lib nome_da_crate`. Depois, você pode editar o arquivo `Cargo.toml` para adicionar as informações da sua crate e as dependências que ela precisa.

Para usar uma crate externa no seu código, você precisa declará-la no arquivo `Cargo.toml` na seção `[dependencies]` e importá-la com a palavra-chave `use` no seu código. Por exemplo:

    ...
    [dependencies]
    rand = "0.8.4"

Isso indica ao Cargo que você quer usar a versão 0.8.4 da biblioteca rand, que é o último lançamento no momento em que escrevo este post. Você pode encontrar outras bibliotecas e suas versões no site crates.io, que é o repositório oficial de pacotes do Rust.

Depois de adicionar a linha da dependência ao seu arquivo Cargo.toml, você pode executar o comando cargo build para baixar e compilar a biblioteca e suas dependências. O Cargo irá criar um diretório chamado target, onde ele armazena os arquivos binários do seu projeto e das bibliotecas que ele usa.

Agora você pode usar a biblioteca rand no seu código fonte, importando-a com a palavra-chave use:

    use rand::Rng;

Isso permite que você use o trait Rng da biblioteca rand, que fornece métodos para gerar números aleatórios. Por exemplo, você pode gerar um número inteiro entre 1 e 10 com este código:

    let n = rand::thread_rng().gen_range(1..=10);

Pronto! Você acabou de adicionar uma dependência ao seu projeto Rust e usá-la no seu código. 

## Adicionando dependencias usando cargo add

Agora vou mostrar como adicionar dependências com features a um projeto Rust usando o cargo add. O cargo add é um comando que permite adicionar facilmente uma dependência ao seu arquivo Cargo.toml sem precisar editá-lo manualmente. Por exemplo, se você quiser adicionar a biblioteca serde com as features json e derive, basta digitar:

    cargo add serde --features json derive

Isso vai atualizar o seu Cargo.toml com algo assim:

    [dependencies]
    serde = { version = \"1.0\", features = [\"json\", \"derive\"] }

Pronto! Agora você pode usar a serde no seu código Rust com as features que você escolheu. Mas e se você quiser adicionar uma dependência que é usada por outra dependência do seu projeto, e você quer especificar as features dessa sub-dependência? Por exemplo, se você usa a biblioteca self_update, que depende da reqwest, e você quer usar a feature rustls-tls da reqwest para evitar o openssl? Infelizmente, o cargo add não suporta isso diretamente. Você teria que editar o seu Cargo.toml manualmente e adicionar algo assim:

    [dependencies]
    self_update = \"0.27\"
    reqwest = { version = \"0.11\", default-features = false, features = [\"rustls-tls\"] }

Isso vai fazer com que o cargo use a versão 0.11 da reqwest com a feature rustls-tls tanto para o seu projeto quanto para o self_update. Mas isso pode ser um pouco inconveniente, pois você tem que saber qual versão da reqwest o self_update usa e manter isso sincronizado.

Uma alternativa é usar o comando cargo edit para editar o seu Cargo.toml interativamente. Você pode instalar o cargo edit com:

    cargo install cargo-edit

Depois de instalado, você pode usar o comando cargo edit --manifest-path Cargo.toml para abrir o seu Cargo.toml em um editor de texto. Lá você pode adicionar ou modificar as dependências e as features que você quiser.

## Ver documentação de uma crate

Uma das grandes vantagens de Rust é o seu sistema de crates, que são pacotes de código reutilizável que podem ser facilmente integrados ao seu projeto.

Mas como saber o que cada crate faz e como usá-lo? A resposta é simples: consulte a documentação! A documentação de uma crate é um conjunto de páginas web que explicam o seu propósito, os seus módulos, as suas funções, as suas estruturas de dados e os seus exemplos de uso. A documentação é gerada automaticamente pelo compilador de Rust a partir dos comentários no código fonte da crate.

Para ver a documentação de uma crate do Rust, você tem duas opções: online ou offline. A opção online é acessar o site https://docs.rs/, que hospeda a documentação de todas as crates publicadas no https://crates.io/, o repositório oficial de crates do Rust. Lá você pode pesquisar pelo nome da crate que você quer consultar e navegar pelas suas páginas.

A opção offline é usar o comando `cargo doc` na linha de comando do seu computador. Esse comando vai gerar a documentação localmente para todas as crates que fazem parte do seu projeto atual. Você pode abrir o arquivo `target/doc/index.html` no seu navegador e ver a documentação das suas dependências. Você também pode usar o comando `cargo doc --open` para abrir o navegador automaticamente.

E pronto! Agora você já sabe como ver a documentação de uma crate do Rust e aproveitar todo o potencial dessa linguagem incrível. Espero que tenham gostado deste post e até a próxima!

