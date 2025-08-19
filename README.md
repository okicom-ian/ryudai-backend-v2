
# Ryudai Backend （日本語版）

これは **琉大ロボットプロジェクト** のバックエンドサービススタックです。
Docker によりコンテナ化されており、簡単にセットアップでき、ローカル開発環境を再現可能に構築できます。

## ✨ 含まれるサービス

- Node-RED（フローと統合）
- Mosquitto（MQTT ブローカー、WebSockets はポート 9001）
- InfluxDB 2.7（時系列データベース）
- Grafana 10（ダッシュボード、プロビジョニング対応）
- MySQL 8（メインの SQL データベース）
- phpMyAdmin（MySQL 用の Web UI）
- Docker 化による一貫性と移植性

---

## 🧰 前提条件

- [Docker](https://www.docker.com/)
- [Docker Compose](https://docs.docker.com/compose/)
- WSL（Ubuntu 推奨）
- Git
- VS Code（任意、*Remote – WSL* 拡張機能を使用）

---

## 🛠️ セットアップ手順

💡 **注意:** このセットアップは WSL 環境で実行してください。

- 以下のコマンドはすべて WSL (Ubuntu など) 内で実行します。
- VS Code を使用する場合は、WSL 内で `code .` を実行してください (*Remote – WSL* 拡張が必要です)。

---

### 1. リポジトリをクローン

```bash
git clone <Github Personal Token>@github.com/okicom-ian/ryudai-backend-v2.git
cd ryudai-backend
```

### 2. 環境ファイルを作成

- サンプルファイルをコピーして、自分用に設定します:
```bash
cp .env.example .env
```


### 3. VS Code で .env ファイルを編集

**`.env` を開き、MS Teams チャンネル 「okicom社内調整 ＞ Githubリポジトリ構成ｖ２」 に記載されている値を設定し、パスワードやトークンを変更してください。**

### 4. Mosquitto パスワードファイルを初期化

ワンタイムの init サービスを実行して `/mosquitto/data/passwd` を作成します:

```bash
docker compose -f docker-compose.yml -f docker-compose.init.yml run --rm mosquitto-init
```

この作業が必要なのは以下の場合のみです:

- 新しくクローンした直後
- `.env` 内の `MQTT_USER` / `MQTT_PASS` を変更したとき

### 5. 全サービスを起動
```bash
docker compose up -d
```

### 🌐 サービスにアクセス

- **Node-RED** → http://localhost:1880
- **Grafana** → http://localhost:3000
  - ログイン: `.env` の `GF_SECURITY_ADMIN_USER` / `GF_SECURITY_ADMIN_PASSWORD`
- **InfluxDB** → http://localhost:8086
  - Org: `.env` の `DOCKER_INFLUXDB_INIT_ORG`
  - Bucket: `.env` の `DOCKER_INFLUXDB_INIT_BUCKET`
  - Token: `.env` の `DOCKER_INFLUXDB_INIT_ADMIN_TOKEN`
- **MySQL** → ポート 3306
- **phpMyAdmin** → http://localhost:8080
  - サーバー: `mysql`
  - ユーザー / パスワード: `.env` の `MYSQL_USER` / `MYSQL_PASSWORD`



---




# Ryudai Backend 　（英語版）

This is the backend service stack for the **Ryudai Robot Project**, containerized with Docker for easy setup and repeatable local development.

## ✨ What’s included

- Node‑RED (flows & integrations)
- Mosquitto (MQTT broker, WebSockets on 9001)
- InfluxDB 2.7 (time‑series DB)
- Grafana 10 (dashboards; provisionable)
- MySQL 8 (primary SQL DB)
- phpMyAdmin (web UI for MySQL)
- Dockerized for consistency & portability

---

## 🧰 Prerequisites

-   [Docker](https://www.docker.com/)
-   [Docker Compose](https://docs.docker.com/compose/)
-   WSL (Ubuntu recommended)
-   Git
-   VS Code (optional, with Remote – WSL extension)

---

## 🛠️ Getting Started

💡 Note: This setup should be run in a WSL environment

-   All commands below are intended to be executed inside WSL (e.g., Ubuntu).
-   If you are using VS Code, make sure to run code . from within WSL (the WSL extension is required).

---

### 1. Clone the Repository

```bash
git clone <Github Personal Token>@github.com/okicom-ian/ryudai-backend-v2.git
cd ryudai-backend
```



### 2. Create environment file

- Copy the example and set your own secrets:
```bash
cp .env.example .env
```

### 3. Open VS Code and edit .env file

**Edit .env with the values indicated in the MS Teams channel okicom社内調整＞Githubリポジトリ構成ｖ２ and change passwords/tokens to the indicated values.**

### 4. Initialize Mosquitto password file

Run the one-off init service to create /mosquitto/data/passwd:
```bash
docker compose -f docker-compose.yml -f docker-compose.init.yml run --rm mosquitto-init
```

This only needs to be done:

After a fresh clone, or

If you change MQTT_USER / MQTT_PASS in .env.

### 5. Start all services
```bash
docker compose up -d
```

### 🌐 Access the services

- Node-RED → http://localhost:1880

- Grafana → http://localhost:3000

  - Login: GF_SECURITY_ADMIN_USER / GF_SECURITY_ADMIN_PASSWORD from .env

- InfluxDB → http://localhost:8086

  - Org: DOCKER_INFLUXDB_INIT_ORG

  - Bucket: DOCKER_INFLUXDB_INIT_BUCKET

  - Token: DOCKER_INFLUXDB_INIT_ADMIN_TOKEN

- MySQL → port 3306

- phpMyAdmin → http://localhost:8080

  - Server: mysql

  - User/pass from .env (MYSQL_USER / MYSQL_PASSWORD)




