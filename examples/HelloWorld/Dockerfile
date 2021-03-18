FROM ghcr.io/graalvm/graalvm-ce:java11-21.0.0.2 as builder 
RUN gu install native-image && \
    mkdir /app

WORKDIR /app

FROM builder as compiler
COPY . /app
RUN javac -d out HelloWorld.java && \ 
    native-image --static -cp out HelloWorld out/helloworld && \
    #  This line is only for demo purpose. Not required for application
    time java -XX:-UseJVMCICompiler -cp out HelloWorld && \
    # This is only for demo purpose. Not required for application
    time out/helloworld 

FROM scratch
COPY --from=compiler /app/out/helloworld /opt/docker/helloworld
ENTRYPOINT ["/opt/docker/helloworld"]

