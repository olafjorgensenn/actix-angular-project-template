FROM rust:1.75.0 AS runtime
MAINTAINER Stavros Grigoriou <unix121@protonmail.com>

WORKDIR /app

RUN apt-get update -y \
      && apt install -y --no-install-recommends openssl ca-certificates \
      && apt-get autoremove -y \
      && apt-get clean -y \
      && rm -rf /var/lib/apt/lists/*

COPY . .

# Update the configuration to production
RUN mv configuration-prod.yaml configuration.yaml
RUN mv .env.docker .env

# Build the application
ENV SQLX_OFFLINE true

RUN cargo build --release

EXPOSE 8000

ENTRYPOINT ["./target/release/api"]
