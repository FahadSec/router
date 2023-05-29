FROM fuzzers/cargo-fuzz:0.11.0 as builder
RUN rustup toolchain install nightly

ADD . /router
WORKDIR /router

RUN cd fuzz/ && cargo +nightly fuzz build

FROM ubuntu:22.04
COPY --from=builder /router/target/x86_64-unknown-linux-gnu/release/router /
COPY --from=builder /router/target/x86_64-unknown-linux-gnu/release/federation /
COPY --from=builder /router/target/x86_64-unknown-linux-gnu/release/router_errors /
