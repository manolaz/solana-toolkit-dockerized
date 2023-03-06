FROM --platform=$BUILDPLATFORM ubuntu:latest 

RUN apt-get install build-essential
# RUN apt-get update 
# RUN apt-get upgrade
# RUN apt-get install rustc
RUN curl --proto '=https' --tlsv1.3 https://sh.rustup.rs -sSf | sh
# RUN curl https://sh.rustup.rs -sSf | sh
RUN rustup component add rustfmt

WORKDIR /app
ARG TARGETARCH

RUN dpkg --add-architecture ${TARGETARCH}


# RUN apt-get install libssl-dev libudev-dev 
# RUN apt-get install pkg-config zlib1g-dev
# RUN apt-get install llvm clang
# RUN apt-get install cmake make
# RUN apt-get install libprotobuf-dev protobuf-compiler

ARG SOLANA_VERSION=1.15.2
# RUN git clone git@github.com:solana-labs/solana.git
# WORKDIR /app/solana
# RUN git checkout tags/v${SOLANA_VERSION} -b v${SOLANA_VERSION}
# RUN ./cargo build
# RUN ./cargo test

RUN sh -c "$(curl -sSfL https://release.solana.com/v$SOLANA_VERSION/install)"
WORKDIR /app/solana

# RUN mkdir solana-raw
# WORKDIR /solana-raw

# RPC json
EXPOSE 8899/tcp
# RPC pubsub
EXPOSE 8900/tcp
# entrypoint
EXPOSE 8001/tcp
# (future) bank service
EXPOSE 8901/tcp
# bank service
EXPOSE 8902/tcp
# faucet
EXPOSE 9900/tcp
# tvu
EXPOSE 8000/udp
# gossip
EXPOSE 8001/udp
# tvu_forwards
EXPOSE 8002/udp
# tpu
EXPOSE 8003/udp
# tpu_forwards
EXPOSE 8004/udp
# retransmit
EXPOSE 8005/udp
# repair
EXPOSE 8006/udp
# serve_repair
EXPOSE 8007/udp
# broadcast
EXPOSE 8008/udp
# tpu_vote
EXPOSE 8009/udp

WORKDIR /solana

RUN apt-get update
RUN apt-get install  -y bzip2

COPY --from=binaries /app/solana/bin ./bin

ENV PATH="/solana"/bin:"$PATH"

CMD ["solana-test-validator", "--reset"]