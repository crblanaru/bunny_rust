# Rust as the base image
FROM rust:1.51

# 1. Create a new empty shell project
RUN addgroup \
    --gid 1000 \
    docker

RUN adduser \
    --disabled-password \
    --gecos "" \
    --home "$(pwd)" \
    --ingroup docker \
    --no-create-home \
    --uid 1000 \
    docker

RUN USER=root cargo new --bin holodeck
WORKDIR /holodeck

# 2. Copy our manifests
#COPY ./Cargo.lock ./Cargo.lock
COPY ./Cargo.toml ./Cargo.toml

# 3. Build only the dependencies to cache them
RUN cargo build --release
RUN rm src/*.rs

# 4. Now that the dependency is built, copy your source code
COPY ./src ./src

# 5. Build for release.
RUN rm ./target/release/deps/holodeck*
RUN cargo install --path .

RUN chown -R 1000:0 /holodeck

CMD ["holodeck"]
