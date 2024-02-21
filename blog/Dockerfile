# Créer un Dockerfile pour cette application en mode production
FROM rustlang/rust:nightly

WORKDIR /usr/src/app
COPY . .

RUN cargo install --path .
RUN cp /usr/local/cargo/bin/blog ./blog
RUN cargo install diesel_cli --no-default-features --features postgres
RUN apt update && apt install curl -y \
        && rm -rf /var/lib/apt/lists/* \

CMD ["diesel","migration","run"]
CMD ["./blog"]