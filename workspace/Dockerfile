

FROM ghcr.io/graalvm/graalvm-ce:java11-21.0.0.2 as builder 
RUN gu install native-image && \
    mkdir /app

WORKDIR /app

ENTRYPOINT ["bash"]
