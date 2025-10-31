# GitHub Copilot Agentsの実践例

このディレクトリには、GitHub Copilot Agentsが生成できる実用的な例が含まれています。

## 含まれる例

### 1. CI/CDワークフロー
- `github-actions-validate.yml` - Kubernetesマニフェストの検証ワークフロー
- `github-actions-security.yml` - セキュリティスキャンワークフロー

### 2. 拡張されたデプロイメント設定
- `vproapp-production.yaml` - 本番環境用の拡張設定（リソース制限、ヘルスチェック、HPA付き）
- `vprodb-ha.yaml` - High Availability構成のデータベース設定

### 3. Kustomize設定
- `kustomization/` - 環境別の設定管理例

### 4. モニタリング設定
- `monitoring/` - PrometheusとGrafanaの設定例

## Agentsに依頼する例

### 例1: CI/CDワークフローの作成依頼

```
「.github/workflows/validate.ymlを作成してください。
以下を含めてください：
- Kubernetesマニフェストの構文チェック
- kubevalによるバリデーション
- セキュリティスキャン（Trivy使用）」
```

### 例2: 本番環境設定の作成依頼

```
「examples/vproapp-production.yamlを作成してください。
以下の本番環境要件を満たすこと：
- レプリカ数: 3
- リソース制限: CPU 1core、メモリ 2Gi
- ヘルスチェック付き
- HPA設定（CPU 70%でスケール、最大10レプリカ）
- PodDisruptionBudget付き」
```

### 例3: Kustomize設定の作成依頼

```
「examples/kustomization/ディレクトリ配下に、
開発環境と本番環境用のKustomize設定を作成してください。
base/にベース設定、overlays/dev/と overlays/prod/に
環境固有の設定を配置してください」
```

## これらの例を使用する方法

1. `examples/`ディレクトリ内のファイルを参照
2. 必要に応じて自分の環境に合わせて修正
3. Agentsに依頼して、類似の設定を生成してもらう

## 注意事項

- これらの例は参考用です
- 実際の環境に合わせて適切に修正してください
- セキュリティ設定は特に慎重に確認してください
