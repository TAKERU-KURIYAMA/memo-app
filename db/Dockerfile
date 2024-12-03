# ベースイメージとして公式 SQL Server イメージを使用
FROM mcr.microsoft.com/mssql/server:2019-latest

# 必要なツールをインストールする前にroot権限に切り替える
USER root

# 必要なツールをインストール
RUN apt-get update && apt-get install -y curl apt-transport-https gnupg2 && \
    curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add - && \
    curl https://packages.microsoft.com/config/ubuntu/20.04/prod.list > /etc/apt/sources.list.d/mssql-release.list && \
    apt-get update && \
    ACCEPT_EULA=Y apt-get install -y mssql-tools unixodbc-dev && \
    echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> /etc/profile && \
    echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

# デフォルトの非rootユーザーに戻す
USER mssql

# デフォルトコマンドを維持
CMD ["/opt/mssql/bin/sqlservr"]
