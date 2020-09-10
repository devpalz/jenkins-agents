FROM alpine:latest

RUN apk add --update --no-cache curl \
  && curl http://192.168.1.88:8081/jnlpJars/agent.jar --output agent.jar

