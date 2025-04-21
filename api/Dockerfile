FROM ruby:3.2.2-slim AS base

# 作業ディレクトリを設定
WORKDIR /rails

# 必要なパッケージをインストール（MySQL -> MariaDB へ変更）
RUN apt-get update -qq && \
    apt-get install --no-install-recommends -y \
    curl \
    libjemalloc2 \
    libvips \
    mariadb-client \
    build-essential \
    git \
    libmariadb-dev \
    pkg-config && \
    rm -rf /var/lib/apt/lists /var/cache/apt/archives

# 環境変数を設定
ENV BUNDLE_PATH="/usr/local/bundle"

# Gemfile をコピーして bundle install
COPY Gemfile Gemfile.lock ./
RUN bundle install

# アプリケーションコードをコピー
COPY . .

# 開発用の設定（root ユーザーで動作）
RUN mkdir -p tmp/pids && chmod -R 777 tmp

# ポートを公開
EXPOSE 3000

# コンテナ起動時のデフォルトコマンド
CMD ["bundle", "exec", "rails", "server", "-b", "0.0.0.0"]