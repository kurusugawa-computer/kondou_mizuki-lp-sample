# ベースイメージを指定
FROM ruby:3.3.6-bullseye

# ロケールとタイムゾーンの設定
ENV LANG=ja_JP.UTF-8
ENV LANGUAGE=ja_JP:ja
ENV LC_ALL=ja_JP.UTF-8
RUN set -eux \
    && export DEBIAN_FRONTEND=noninteractive \
    && apt-get update \
    && apt-get install -y --no-install-recommends \
        # ロケール用データ
        locales \
        # タイムゾーンデータ
        tzdata \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* \
    # 日本語ロケールを生成
    && sed -i '/ja_JP.UTF-8/s/^# //' /etc/locale.gen \
    && locale-gen \
    # タイムゾーンを東京に設定
    && ln -sf /usr/share/zoneinfo/Asia/Tokyo /etc/localtime \
    # タイムゾーン情報をファイルに書き込む
    && echo "Asia/Tokyo" > /etc/timezone

# ユーザー・グループ追加
RUN useradd --create-home --shell /bin/bash vscode

# ユーザーを変更
USER vscode

# JekyllとBundlerをインストール
RUN gem install bundler jekyll
