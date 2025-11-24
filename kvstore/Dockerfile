FROM rust:bullseye as builder

WORKDIR /app

COPY Cargo.toml Cargo.lock ./
RUN mkdir src && echo "fn main() {}" > src/main.rs
RUN cargo build --release
RUN rm -rf src

COPY . .
RUN cargo build --release

FROM debian:bullseye-slim

WORKDIR ./app
COPY --from=builder /app/target/release/kvstore ./kvstore

CMD ["./kvstore"]
