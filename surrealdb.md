## install

    curl -sSf https://install.surrealdb.com | sh

## run multi-node scalable cluster with tikv

install tiup

    curl -sSf https://tiup-mirrors.pingcap.com/install.sh | sh


run a cluster with one node

    tiup playground --tag surrealdb --mode tikv-slim --pd 1 --kv 1

start a surrealdb instance

    surreal start --log trace --user root --pass root tikv://127.0.0.1:2379

