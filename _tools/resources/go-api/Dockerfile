# ベースとなるDockerイメージ指定
FROM golang:1.19 as server-build
ENV TZ Asia/Tokyo
ARG APT_GET_PACKAGE="sudo vim iputils-ping net-tools git curl zip unzip telnetd inetutils-inetd telnet cron man jq"

RUN \
    # インストール apt package
    apt-get -y update \
    && apt-get install -y $APT_GET_PACKAGE \
    # インストール aws cli(curl/unzipに依存)
    && mkdir ~/aws_cli \
    && cd ~/aws_cli \
    && curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip" \
    && unzip awscliv2.zip \
    &&  ./aws/install \
    # apt-getをお掃除
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# コンテナ内の作業ディレクトリを作成し、そこを指定
WORKDIR  /go/src/go-todo-api
# apiディレクトリをコンテナの作業ディレクトリにコピー
# contextはdocker-compose.ymlと同一ディレクトリ
COPY ./go-api/api .
