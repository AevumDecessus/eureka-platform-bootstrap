ARG VAULT_VERSION=1.13.3
ARG PUID=1234
ARG PGID=1234

FROM hashicorp/vault:$VAULT_VERSION

RUN apk update && apk add --no-cache curl jq coreutils

RUN deluser vault
RUN addgroup -g ${PGID} vault
RUN adduser -S -u ${PUID} -G vault vault

RUN cat /etc/passwd
COPY ./config /usr/local/bin/ebsco/config
COPY ./scripts /usr/local/bin/ebsco/scripts

RUN chown -R vault /vault
RUN chmod 500 /usr/local/bin/ebsco/scripts/*
RUN chmod 400 /usr/local/bin/ebsco/config/*
RUN chown -R vault /usr/local/bin/ebsco

ENTRYPOINT [ "/usr/local/bin/ebsco/scripts/start.sh" ]
