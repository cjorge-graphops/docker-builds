FROM golang:1.19-alpine@sha256:bb72ffd13e9c75ccb65487e89845ecc572d749a07635c9b7fb4df2047c1bef68

ENV DOWNLOAD_MANAGER_REF="main"

WORKDIR /go/src/gnosischain/download-manager
RUN apk add --no-cache git && \
    git clone https://github.com/gnosischain/download-manager --depth=1 --branch=${DOWNLOAD_MANAGER_REF} . && \
    go get github.com/vbauerster/getparty && \
    CGO_ENABLED=0 GOOS=linux go build -ldflags="-s -w" -a -installsuffix cgo -o download-manager .

FROM alpine:3.16@sha256:cbe5d5973103a2d03408d1689a6efde4ea4920bde9f4b51fe7872e60ce2d8e56
WORKDIR /
RUN apk add --no-cache curl aria2
COPY --from=0 /go/src/gnosischain/download-manager/download-manager /download-manager
