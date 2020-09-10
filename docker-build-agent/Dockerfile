FROM jenkins/inbound-agent:alpine

# Switch to root so we can extend the image
USER root

# Install docker and curl
RUN set -eux \
  && apk add --no-cache docker curl

# Install dgoss
RUN curl -L https://raw.githubusercontent.com/aelsabbahy/goss/master/extras/dgoss/dgoss -o /usr/local/bin/dgoss \
   && chmod +rx /usr/local/bin/dgoss

# Install goss
RUN LATEST=$(curl https://api.github.com/repos/aelsabbahy/goss/releases | grep "tag_name" | sed -E 's/.*"([^"]+)".*/\1/' | head -1) \
    && curl -L https://github.com/aelsabbahy/goss/releases/download/$LATEST/goss-linux-amd64 -o /goss-linux-amd64

# Set the goss path so we can execute goss commands
ENV GOSS_PATH /goss-linux-amd64

# Dgoss by default will try and mount the goss executable into the temp directory which Linux does not allow
ENV GOSS_FILES_STRATEGY cp


# Switch back to the Jenkins user
USER jenkins
