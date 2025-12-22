ARG VAULT_VERSION=1.13.3
ARG PUID=1234
ARG PGID=1234

FROM hashicorp/vault:$VAULT_VERSION

RUN apk update && apk add --no-cache curl jq coreutils shadow

RUN usermod -u ${PUID} vault
COPY ./config /usr/local/bin/ebsco/config
COPY ./scripts /usr/local/bin/ebsco/scripts

RUN chown -R vault:${PGID} /vault
RUN chmod 500 /usr/local/bin/ebsco/scripts/*
RUN chmod 400 /usr/local/bin/ebsco/config/*
RUN chown -R vault:${PGID} /usr/local/bin/ebsco

ENTRYPOINT [ "/usr/local/bin/ebsco/scripts/start.sh" ]
