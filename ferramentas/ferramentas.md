
# usando rust para otimizar sua vida

Obs: Baseado no video https://www.youtube.com/watch?v=dFkGNe4oaKk  e mais outras que encontrei relevantes


1) cargo install sccache

Para otimizar os tempos de compilação na instalação e build

https://github.com/mozilla/sccache

como usar

    RUSTC_WRAPPER=sccache cargo install <yourpackage>

ou edite o arquivo '''$HOME/.cargo/config.toml'''

    [build]
    rustc-wrapper = "/home/x/.cargo/bin/sccache"

2) Nushell 

https://www.nushell.sh/


3) Coreutils/uutils 

https://uutils.github.io/user/


4) Starship 

https://starship.rs/

basicamente use 

    curl -sS https://starship.rs/install.sh | sh 
 
e siga as instruções

5) du-dust

Substitui o comando du 

    cargo install du-dust

6) zellij 

https://zellij.dev/about/  é uma alternativa ao tmux

    cargo install zellij


7) mprocs 

é um visualizador dos processos rodando em paralelo, é uma alternativa ao tmux e zellij
https://github.com/pvolok/mprocs



    cargo install mprocs


8) Ripgrep 

https://github.com/BurntSushi/ripgrep/blob/master/GUIDE.md 

    cargo install ripgrep

9) gitui

https://github.com/extrawurst/gitui

    cargo install gitui



10) rtx-cli

https://crates.io/crates/rtx-cli

Gerenciador de instalação de runtimes (alternativa ao asdf)

    cargo install rtx-cli

11) cargo binstall

    cargo install binstall

instala pacotes binários, evitando a compilação

