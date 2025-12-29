# Distributed Specialist Learning (DSL)

**English**: [README_EN.md](README_EN.md) | **日本語**: This document

**DSLは「単一の強力モデル」ではなく「強力な応答を提供する分散システム」**です。

分散学習により、参加者が巨大GPUを持たなくても「強力な応答」をローカル（PC/ブラウザ）で使える状態を作ることを目指します。

## なぜ speed-only はダメか？

速度だけを最適化すると「速いゴミ」（短文テンプレ、拒否、無意味出力）が勝ってしまいます。
DSLは **Verifier（品質ゲート）+ 合成報酬関数** でこれを防ぎます。

## アーキテクチャ

DSLは三層構造を採用する：

- **探索層（分散）**: 多モデル競争で勝者ログを作り、特化を育てる
- **実行層（ローカル）**: selectorが少数モデルだけ呼び出して高速応答
- **ガバナンス層（制度）**: proxy置換、特化モデル増殖/淘汰、供給網安全

詳細なアーキテクチャ図とデータフローは [WHITEPAPER_JP.md](WHITEPAPER_JP.md) を参照。

## MVP: JSON変換タスク

最初の成功条件：JSON変換に特化したモデルが、verifier（schema検証）を通過し、品質と速度のバランスで勝者になる。

**推奨**: verifierが最も安い領域（JSON変換、コード生成など）から始める

## このプロジェクトについて

**This proposal intentionally provides no reference implementation.**
**The goal is to enable independent verification and falsification.**

実装はコミュニティに委ね、仕様とプロトコルを明確に定義することで、分散検証を促進します。

詳細は [WHITEPAPER.md](WHITEPAPER.md) (English) または [WHITEPAPER_JP.md](WHITEPAPER_JP.md) (Japanese) を参照してください。

## クイックスタート（実装者向け）

**5分で始める**: [QUICK_START.md](QUICK_START.md) を参照してください。

1. [DSL_PROTOCOL_V0_1.md](DSL_PROTOCOL_V0_1.md) を読む（5分）
2. [examples/](examples/) のサンプルを確認
3. 実装したい機能を [Issue](https://github.com/Unjuno/dsl-whitepaper/issues) で宣言

## Help Wanted

実装が必要な主要コンポーネント：

- [ ] **MVP runner** - 基本的な実行環境（1つの特化モデル + verifier）
- [ ] **q1 metrics** - 品質proxy実装
- [ ] **audit set** - 監査セット作成と実行

詳細は [CONTRIBUTING.md](CONTRIBUTING.md) を参照してください。

## ドキュメント

### 実装者向け（最初に読む）

- [QUICK_START.md](QUICK_START.md) - 5分クイックスタートガイド
- [DSL_PROTOCOL_V0_1.md](DSL_PROTOCOL_V0_1.md) - プロトコル要約（実装者向け）
- [CONTRIBUTING.md](CONTRIBUTING.md) - 参加方法とガイドライン

### 理論・仕様

- [WHITEPAPER.md](WHITEPAPER.md) - 完全版理論・仕様（v1.3、English）
- [WHITEPAPER_JP.md](WHITEPAPER_JP.md) - 完全版理論・仕様（v1.3、Japanese）**← 主要ドキュメント**
- [SPECIALIST_MODEL_DEFINITION.md](SPECIALIST_MODEL_DEFINITION.md) - 特化モデルの定義（補足）
- [METRICS_AND_AUDIT.md](METRICS_AND_AUDIT.md) - メトリクスとAudit仕様（補足）
- [MODEL_RESPONSE_SPEED.md](MODEL_RESPONSE_SPEED.md) - モデル応答速度の技術的説明（補足）

### プロジェクト情報

- [PROJECT_STRUCTURE.md](PROJECT_STRUCTURE.md) - プロジェクト構成ガイド
- [LICENSE_INFO.md](LICENSE_INFO.md) - ライセンス情報

### サンプル・スキーマ

- [examples/](examples/) - サンプルファイル
- [schemas/](schemas/) - JSON Schema定義

## プロジェクトの目標

**「みんながローカルで強力なモデルを使える」**

- ✅ 推論がローカルで成立（一般的PC/ブラウザでも動作）
- ✅ 学習が分散で回る（参加者は自分の得意領域の特化差分を作って投稿できる）
- ✅ 制度として壊れない（速いゴミ、単一支配、供給網汚染、モデル氾濫を抑制）

## License

Apache-2.0

詳細は [LICENSE_INFO.md](LICENSE_INFO.md) を参照してください。