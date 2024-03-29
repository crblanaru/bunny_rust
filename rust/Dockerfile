# Rust as the base image
FROM rust:1.51 as build

# Create a new empty shell project
RUN USER=root cargo new --bin holodeck
WORKDIR /holodeck

# Copy our manifests
COPY ./Cargo.toml ./Cargo.toml

# Build only the dependencies to cache them
RUN cargo build --release
RUN rm src/*.rs

# Copy the source code
COPY ./src ./src

# Build for release.
RUN rm ./target/release/deps/holodeck*
RUN cargo build --release

# The final base image
FROM debian:buster-slim

# Copy from the previous build
COPY --from=build /holodeck/target/release/holodeck /usr/src/holodeck
# COPY --from=build /holodeck/target/release/holodeck/target/x86_64-unknown-linux-musl/release/holodeck .

# Run the binary
CMD ["/usr/src/holodeck"]
