FROM golang:1.19-alpine@sha256:bb72ffd13e9c75ccb65487e89845ecc572d749a07635c9b7fb4df2047c1bef68

ENV DOWNLOAD_MANAGER_REF="main"

WORKDIR {GOPATH:-/go}/src/temporalite
RUN apk add --no-cache git && \
    git clone https://github.com/temporalio/temporalite.git && \
    cd temporalite && \
    go build -o ${GOPATH:-/go}/bin/ ./cmd/temporalite

FROM alpine:3.16@sha256:cbe5d5973103a2d03408d1689a6efde4ea4920bde9f4b51fe7872e60ce2d8e56
WORKDIR /

COPY --from=0 ${GOPATH:-/go}/bin/temporalite /

EXPOSE 7233
EXPOSE 8233

ENTRYPOINT ["/temporalite", "start"]