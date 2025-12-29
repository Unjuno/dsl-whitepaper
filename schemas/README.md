# JSON Schema Definitions

このディレクトリには、DSLプロトコルで使用されるデータ形式のJSON Schema定義が含まれています。

## ファイル一覧

### model_manifest.schema.json

Model Manifest（特化モデルのメタデータ）のスキーマ定義です。

**使用例**:
```python
import json
import jsonschema

with open('schemas/model_manifest.schema.json') as f:
    schema = json.load(f)

with open('examples/basic_manifest.yaml') as f:
    # YAMLをJSONに変換してから検証
    manifest = yaml.safe_load(f)
    jsonschema.validate(manifest, schema)
```

### run_log.schema.json

Run Log（推論実行ログ）のスキーマ定義です。JSONL形式の各行を検証する際に使用します。

**使用例**:
```python
import json
import jsonschema

with open('schemas/run_log.schema.json') as f:
    schema = json.load(f)

with open('examples/run_log_sample.jsonl') as f:
    for line in f:
        log_entry = json.loads(line)
        jsonschema.validate(log_entry, schema)
```

### audit_set.schema.json

Audit Set（監査セット）のスキーマ定義です。

**使用例**:
```python
import json
import jsonschema

with open('schemas/audit_set.schema.json') as f:
    schema = json.load(f)

with open('audit/audit_set_v1.json') as f:
    audit_set = json.load(f)
    jsonschema.validate(audit_set, schema)
```

## バリデーションツール

実装時は、これらのスキーマを使用してデータの妥当性を検証してください。

推奨ツール:
- Python: `jsonschema` ライブラリ
- Node.js: `ajv` ライブラリ
- コマンドライン: `ajv-cli`

## スキーマの拡張

実装の進捗に応じて、スキーマを拡張する場合は、バージョン管理を行ってください。

例: `model_manifest.schema.v2.json` など
