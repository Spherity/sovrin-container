FROM docker.io/library/ubuntu:bionic

COPY generate-keys.sh /usr/local/bin/generate-keys

RUN apt-get update && \
    apt-get install -y gpg software-properties-common curl pwgen && \
    apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys CE7709D068DB5E88 && \
    add-apt-repository "deb https://repo.sovrin.org/sdk/deb bionic stable" && \
    apt-get update && \
    apt-get install -y indy-cli && \
    rm -rf /var/lib/apt/lists* && \
    curl -OSsL https://raw.githubusercontent.com/sovrin-foundation/sovrin/master/sovrin/pool_transactions_builder_genesis && \
    curl -OSsL https://raw.githubusercontent.com/sovrin-foundation/sovrin/stable/sovrin/pool_transactions_sandbox_genesis && \
    curl -OSsL https://raw.githubusercontent.com/sovrin-foundation/sovrin/stable/sovrin/pool_transactions_live_genesis && \
    curl -SsL -o ssi4de_pool_transactions_genesis https://raw.githubusercontent.com/Echsecutor/docker-indy-node/master/lib_indy/ssi4de/pool_transactions_genesis  && \
    mkdir -p /etc/indy-cli && \
    chmod +x /usr/local/bin/generate-keys

COPY cliconfig.json /etc/indy-cli/cliconfig.json

CMD ["indy-cli", "--config", "/etc/indy-cli/cliconfig.json"]
