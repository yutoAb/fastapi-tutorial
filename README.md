# FastAPI Tutorial

FastAPIを使ったタスク管理APIアプリケーションのチュートリアルプロジェクトです。

## 概要

このプロジェクトは、FastAPIとSQLAlchemyを使用したRESTful APIアプリケーションの実装例です。タスクの作成、取得、更新、完了機能を持つシンプルなタスク管理システムを構築しています。

## 技術スタック

- **Web フレームワーク**: FastAPI 0.119.x
- **サーバー**: Uvicorn
- **ORM**: SQLAlchemy 2.0.x
- **データベース**: MySQL 8.0
- **データベース接続**: aiomysql
- **コンテナ**: Docker & Docker Compose
- **パッケージ管理**: Poetry

## プロジェクト構造

```
fastapi-tutorial/
├── api/
│   ├── cruds/          # データベース操作
│   │   ├── task.py
│   │   └── done.py
│   ├── models/         # SQLAlchemyモデル
│   │   └── task.py
│   ├── routers/        # APIエンドポイント
│   │   ├── task.py
│   │   └── done.py
│   ├── schemas/        # Pydanticスキーマ
│   │   ├── task.py
│   │   └── done.py
│   ├── db.py           # データベース設定
│   ├── main.py         # アプリケーションエントリーポイント
│   └── migrate_db.py   # データベースマイグレーション
├── docker-compose.yaml
├── Dockerfile
├── pyproject.toml
└── README.md
```

## 機能

- ✅ タスクの作成
- ✅ タスク一覧の取得
- ✅ タスクの更新
- ✅ タスクの完了管理
- ✅ MySQL データベース連携
- ✅ Docker によるコンテナ化

## セットアップ

### 前提条件

- Docker
- Docker Compose

### インストールと起動

1. リポジトリをクローン
```bash
git clone <repository-url>
cd fastapi-tutorial
```

2. Docker Composeでアプリケーションを起動
```bash
docker-compose up -d
```

3. データベースマイグレーションを実行
```bash
docker-compose exec demo-app poetry run python -m api.migrate_db
```

4. アプリケーションにアクセス
   - API: http://localhost:8000
   - API ドキュメント（Swagger UI): http://localhost:8000/docs
   - ReDoc: http://localhost:8000/redoc

### データベース接続情報

- **ホスト**: localhost
- **ポート**: 33306
- **データベース名**: demo
- **ユーザー**: root
- **パスワード**: (なし)

## API エンドポイント

### タスク関連

| メソッド | エンドポイント | 説明 |
|---------|---------------|------|
| GET | `/tasks` | タスク一覧の取得 |
| POST | `/tasks` | 新しいタスクの作成 |
| PUT | `/tasks/{task_id}` | タスクの更新 |
| DELETE | `/tasks/{task_id}` | タスクの削除 |

### 完了状態関連

| メソッド | エンドポイント | 説明 |
|---------|---------------|------|
| PUT | `/tasks/{task_id}/done` | タスクを完了にマーク |
| DELETE | `/tasks/{task_id}/done` | タスクの完了状態を解除 |

## 開発

### ローカル開発環境

```bash
# 依存関係のインストール
poetry install

# アプリケーションの起動
poetry run uvicorn api.main:app --reload

# データベースマイグレーション
poetry run python -m api.migrate_db
```

### コンテナの停止

```bash
docker-compose down
```

### データベースデータの削除

```bash
docker-compose down -v
```

## ライセンス

このプロジェクトはチュートリアル目的で作成されています。

https://zenn.dev/sh0nk/books/537bb028709ab9/viewer/f1b6fc
こちらの記事を参考にして，実装しました.(2025/10/19)