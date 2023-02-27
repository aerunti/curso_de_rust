
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

