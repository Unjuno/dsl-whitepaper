# Contributing to DSL

DSLプロジェクトへの貢献を歓迎します！

## 参加方法

1. **Issueで実装したい機能を宣言**
   - 既存のIssueを確認
   - 新規の場合は [Issue テンプレート](.github/ISSUE_TEMPLATE/) を使用
   - 「Help Wanted」ラベルのIssueから始めることを推奨

2. **実装前に設計を共有**
   - Discussionで設計案を共有（推奨）
   - 小規模な変更の場合は直接PRでも可

3. **PR提出時は以下を含める**
   - 実装の説明
   - テスト結果
   - プロトコル準拠の確認
   - ドキュメント更新（必要に応じて）

## 実装の優先順位

### Phase 1: MVP（最小実装）

**目標**: 基本的な動作を確認できる状態

- [ ] **MVP runner**
  - 1つの特化モデル + verifier
  - 基本的な勝者決定ロジック
  - run_log.jsonl形式でのログ出力

- [ ] **基本的なVerifier実装**
  - JSON Schema検証（推奨：最も安い）
  - または Unit Test検証

- [ ] **Model Manifest検証**
  - YAML形式の読み込み
  - 必須フィールドの検証

### Phase 2: プロトコル完成

**目標**: プロトコル仕様を完全に実装

- [ ] **Metric Registry実装**
  - metric_v1の実装
  - 報酬関数の実装
  - ログへのmetric_version記録

- [ ] **Audit Set実行**
  - 監査セットの読み込み
  - 自動検証実行

- [ ] **Selector実装**
  - 基本的なルーティング
  - 学習データの収集（勝者ログから）

### Phase 3: 分散化

**目標**: 分散参加が可能な状態

- [ ] **モデルレジストリ**
  - モデル一覧の管理
  - バージョン管理

- [ ] **供給網検証**
  - hash検証
  - manifest検証
  - 署名検証（将来）

- [ ] **Selector学習**
  - 勝者ログからの学習
  - 推論時のルーティング最適化

## コーディング規約

### プロトコル準拠を最優先

- 既存のスキーマ定義（[schemas/](schemas/)）に従う
- Model Manifest形式に準拠
- Run Log形式に準拠

### テストは必須

- Verifierを含むテストを実装
- プロトコル準拠のテスト
- サンプルデータでの動作確認

### ドキュメント

- 実装した機能のドキュメント更新
- サンプルコードの提供（可能な場合）

## 質問・議論

- **技術的な質問**: Issueで「Question」ラベルを使用
- **設計の議論**: Discussionを使用
- **バグ報告**: Issueで「Bug」ラベルを使用

## 実装例

実装の参考になるサンプル：

- [examples/basic_manifest.yaml](examples/basic_manifest.yaml) - Model Manifest例
- [examples/run_log_sample.jsonl](examples/run_log_sample.jsonl) - Run Log例
- [schemas/](schemas/) - JSON Schema定義

## コミットメッセージ

以下の形式を推奨：

```
[IMP] 実装内容の簡潔な説明

- 変更点1
- 変更点2
```

例：
```
[IMP] MVP runner実装

- 基本的な勝者決定ロジック実装
- run_log.jsonl形式でのログ出力
- Model Manifest読み込み機能
```

## レビュープロセス

1. PR提出後、自動チェック（CI）が実行されます
2. メンテナーがレビューします
3. フィードバックに基づいて修正
4. 承認後、マージされます

## 行動規範

- 建設的なフィードバックを心がける
- プロトコル仕様に従う
- コミュニティを尊重する

## ライセンス

貢献するコードは、プロジェクトのライセンス（Apache-2.0）に従うものとします。
