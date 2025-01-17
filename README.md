# zenn_ai_hackathon_2501_ws

AI Agent Hackathon with Google Cloud のワークスペース

## 概要

このリポジトリは、Flutter モバイルアプリケーション（フロントエンド）と Go バックエンドを含む統合開発環境を提供します。マイクロサービスアーキテクチャを採用し、効率的なモバイルアプリケーション開発を実現します。

### アーキテクチャ概要

- **フロントエンド**: Flutter モバイルアプリケーション（iOS/Android対応）
- **バックエンド**: Go言語による RESTful API サーバー
- **インフラ**: Docker によるコンテナ化、Google Cloud Platform での展開

## 必要条件

### 共通

- Git 2.0以上
- Docker 20.10以上
- Docker Compose 2.0以上

### フロントエンド開発環境

- Flutter SDK 3.0以上
- Dart SDK 3.0以上
- Android Studio または Xcode
- iOS開発の場合: macOS
- Android開発の場合: Android SDK

### バックエンド開発環境

- Go 1.21以上
- Make

## セットアップ

```bash
# 1. ワークスペースのclone
git clone --recurse-submodules https://github.com/zenn-ai-hackathon-2501/zenn_ai_hackathon_2501_ws.git
cd zenn_ai_hackathon_2501_ws

# 2. submodule の初期化と更新（既に含まれている場合はこのステップを省略）
# このように、git cloneの際に--recurse-submodulesオプションを使用することで、サブモジュールも同時にクローンされるようにしています
git submodule update --init --recursive

# 3. 環境変数の設定
cp .env.example .env
# .env ファイルを編集して必要な環境変数を設定してください
```

!注意!

以降は AI がが生成した出鱈目な手順です。
今はコピペしても動きませんが、今後の開発で目指すべきところでもあるので参考に残します。

## 開発環境の起動

### バックエンド（Go）

```bash
# Docker Composeでバックエンドサービスを起動（http://localhost:8080）
cd zenn_ai_hackathon_2501_backend
docker-compose up -d

# ローカルでの開発時
go mod download
go run cmd/main.go
```

### フロントエンド（Flutter）

```bash
# 依存関係のインストール
cd zenn_ai_hackathon_2501_frontend
flutter pub get

# 開発用デバイスの確認
flutter devices

# iOSシミュレータでの起動
flutter run -d ios

# Androidエミュレータでの起動
flutter run -d android

# 物理デバイスでの起動（デバイスを接続している場合）
flutter run
```

## アプリケーション構成

### バックエンド構成

```text
zenn_ai_hackathon_2501_backend/
├── cmd/            # エントリーポイント
├── internal/       # 内部パッケージ
├── pkg/            # 外部から利用可能なパッケージ
├── api/            # API定義
└── docker/         # Dockerファイル
```

### フロントエンド構成

```text
zenn_ai_hackathon_2501_frontend/
├── lib/
│   ├── app/       # アプリケーション設定
│   ├── features/  # 機能モジュール
│   ├── core/      # コアロジック
│   └── shared/    # 共有コンポーネント
└── test/          # テストファイル
```

## 開発ワークフロー

1. **ブランチ戦略**
   - `main`: プロダクション環境用
   - `develop`: 開発用メインブランチ
   - `feature/*`: 機能開発用
   - `hotfix/*`: 緊急バグ修正用

2. **コミットメッセージ規約**

   ```text
   feat: 新機能
   fix: バグ修正
   docs: ドキュメントのみの変更
   style: コードの意味に影響を与えない変更
   refactor: リファクタリング
   test: テストコード
   chore: ビルドプロセスやツールの変更
   ```

3. **プルリクエストフロー**
   - レビュー必須 (セルフレビューや、AIにレビューさせてください)
   - CI/CDパイプラインのパス必須
   - コンフリクト解消必須

## テスト

### バックエンド

```bash
cd zenn_ai_hackathon_2501_backend
# ユニットテスト
go test ./...

# カバレッジレポート
go test -cover ./...
```

### フロントエンド

```bash
cd zenn_ai_hackathon_2501_frontend
# ユニットテスト
flutter test

# 統合テスト
flutter test integration_test
```

## デプロイ

```bash
# プロダクションビルド
docker-compose -f docker-compose.prod.yml up -d

# Flutterアプリのビルド
cd zenn_ai_hackathon_2501_frontend
# iOS用
flutter build ios
# Android用
flutter build apk
```

## トラブルシューティング

よくある問題と解決方法については、各サブモジュールのREADMEを参照してください。

### よくある問題

1. **Flutter ビルドエラー**
   - `flutter clean` を実行してから再度ビルド
   - Flutter/Dart の依存関係を更新

2. **バックエンドの起動エラー**
   - Docker のログを確認
   - 環境変数の設定を確認

## コントリビューション

1. このリポジトリをフォーク
2. 機能ブランチを作成 (`git checkout -b feature/amazing-feature`)
3. 変更をコミット (`git commit -m 'feat: Add amazing feature'`)
4. ブランチをプッシュ (`git push origin feature/amazing-feature`)
5. プルリクエストを作成

## ライセンス

このプロジェクトは no license です。非公開です。

## 行動規範

### コミュニケーション

- 参加者同士は互いを尊重し、建設的な対話を心がけてください
- ハラスメントや差別的な言動は禁止します
- 技術的な議論は歓迎します
- 困ったことがあれば、遠慮なくチームメンバーに相談してください

### 知的財産・リポジトリ管理

- 他者の知的財産権を尊重してください
- コードの共有は参加者全員の合意を得てください
- リポジトリの削除は以下のいずれかを満たす場合に限り可能です:
  - 参加者全員の合意を得た場合
  - 相当の連絡努力の後、3ヶ月以上経過した場合
