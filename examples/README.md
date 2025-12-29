# Examples

このディレクトリには、DSLプロトコルを実装する際の参考となるサンプルファイルが含まれています。

## ファイル一覧

### basic_manifest.yaml

Model Manifestのサンプルです。JSON変換タスクに特化したモデルの例を示しています。

**使用例**:
```bash
# バリデーション（実装時）
validator --schema schemas/model_manifest.schema.json --data examples/basic_manifest.yaml
```

### run_log_sample.jsonl

Run Logのサンプルです。JSONL形式（各行がJSON）で記録されます。

**使用例**:
```bash
# ログの読み込み（実装時）
cat examples/run_log_sample.jsonl | jq '.'
```

## 実装時の参考

これらのサンプルファイルは、実装時の参考として使用してください。

1. **Model Manifest**: モデル登録時のメタデータ形式
2. **Run Log**: 推論実行ログの形式
3. **JSON Schema**: [schemas/](../schemas/) ディレクトリを参照

## カスタマイズ

実際の実装では、これらのサンプルをベースに、自分のタスク領域に合わせてカスタマイズしてください。
