# kube-app

Kubernetesアプリケーションのデプロイメント設定リポジトリです。

## アーキテクチャ

このアプリケーションは以下のコンポーネントで構成されています：

### コンポーネント

1. **vproapp** - Webアプリケーション
   - イメージ: `yoshijyk/vprofileapp`
   - ポート: 8080
   - 依存関係: MySQL、Memcached

2. **vprodb** - MySQLデータベース
   - イメージ: `yoshijyk/vprofiledb`
   - ポート: 3306
   - ストレージ: AWS EBS Volume
   - ノード配置: ap-northeast-1a

3. **vpromq01** - RabbitMQメッセージキュー
   - イメージ: `rabbitmq`
   - ポート: 15672

4. **vpromc** - Memcachedキャッシュ
   - イメージ: `memcached`
   - ポート: 11211

## デプロイメントファイル

- `vproappdep.yaml` - Webアプリケーションのデプロイメント
- `vprodbdeploy.yaml` - データベースのデプロイメント
- `rmq-dep.yaml` - RabbitMQのデプロイメント
- `memorycachedeploy.yaml` - Memcachedのデプロイメント
- `vproapp-service.yaml` - Webアプリケーションのサービス
- `db-cip.yaml` - データベースのClusterIPサービス
- `rmq-cip.yaml` - RabbitMQのClusterIPサービス
- `mc-cip.yaml` - MemcachedのClusterIPサービス
- `app-secret.yaml` - アプリケーションのシークレット

## デプロイ方法

```bash
# シークレットの作成
kubectl apply -f app-secret.yaml

# データベースのデプロイ
kubectl apply -f vprodbdeploy.yaml
kubectl apply -f db-cip.yaml

# RabbitMQのデプロイ
kubectl apply -f rmq-dep.yaml
kubectl apply -f rmq-cip.yaml

# Memcachedのデプロイ
kubectl apply -f memorycachedeploy.yaml
kubectl apply -f mc-cip.yaml

# Webアプリケーションのデプロイ
kubectl apply -f vproappdep.yaml
kubectl apply -f vproapp-service.yaml
```

## GitHub Copilot Agentsについて

このリポジトリでGitHub Copilot Agentsを活用する方法については、以下のドキュメントをご覧ください：

- **[クイックスタートガイド](./QUICKSTART.md)** - すぐに始められる基本的な使い方
- **[詳細ガイド](./AGENTS.md)** - Agentsの全機能と実践的なユースケース
- **[サンプル集](./examples/)** - 実用的な設定例とテンプレート

## 注意事項

- データベースはAWS EBSボリュームを使用しています
- ボリュームID (`vol-07710b87864ceb449`) は環境に応じて変更してください
- シークレットはBase64エンコードされています
