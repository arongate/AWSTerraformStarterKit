ARG BASH_VERSION
FROM "docker.io/bash:${BASH_VERSION}"

# Runtime dependencies
RUN apk add --no-cache --purge \
    curl \
    awscli \
    python3 py3-pip \
    git \
    wget \
    openssh-client \
    ;

RUN apk --update --no-cache --allow-untrusted --repository http://dl-cdn.alpinelinux.org/alpine/edge/community add \
    corkscrew \
    && rm -rf /var/cache/apk/* \
          /tmp/* \
          /var/tmp/*

ARG TFENV_VERSION

RUN wget -O /tmp/tfenv.tar.gz "https://github.com/tfutils/tfenv/archive/refs/tags/v${TFENV_VERSION}.tar.gz" \
    && tar -C /tmp -xf /tmp/tfenv.tar.gz \
    && mv "/tmp/tfenv-${TFENV_VERSION}/bin"/* /usr/local/bin/ \
    && mkdir -p /usr/local/lib/tfenv \
    && mv "/tmp/tfenv-${TFENV_VERSION}/lib" /usr/local/lib/tfenv/ \
    && mv "/tmp/tfenv-${TFENV_VERSION}/libexec" /usr/local/lib/tfenv/ \
    && mkdir -p /usr/local/share/licenses \
    && mv "/tmp/tfenv-${TFENV_VERSION}/LICENSE" /usr/local/share/licenses/tfenv \
    && rm -rf /tmp/tfenv* \
    && mkdir /var/tfenv \
    && touch /var/tfenv/version \
    && echo "latest" > /var/tfenv/version \
    && chmod 777 -R /var/tfenv \
    ;
ENV TFENV_ROOT /usr/local/lib/tfenv

ENV TFENV_CONFIG_DIR /var/tfenv

ENV TFENV_TERRAFORM_VERSION ""

VOLUME /var/tfenv

ENTRYPOINT ["/usr/local/bin/terraform"]

