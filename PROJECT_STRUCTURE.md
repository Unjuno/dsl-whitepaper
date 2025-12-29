# プロジェクト構成とドキュメント構造

## このドキュメントについて

このドキュメントは、DSLプロジェクトの理想的な構成を説明しています。
現在のプロジェクト状態は [README.md](README.md) を参照してください。

## Cursorで整理するときのゴール

**"読んだ開発者が、そのまま実装を始められる"**状態にする。

## 1. ファイル構成（最低限）

```
/README.md                      # 1ページ概要（思想＋使い方）
/WHITEPAPER_JP.md               # 今回の理論本文（v1.3 Full）
/DSL_PROTOCOL_V0_1.md           # プロトコル要約：実装者向け
/CONTRIBUTING.md                 # PR/issueのルール
/LICENSE                         # ライセンス

/SPEC/
  protocol.md                   # ログ/イベント/通信仕様
  metric_registry.md            # metric_vN と切替手順
  model_manifest_schema.yaml    # model.yaml のスキーマ
  verifier_catalog.md           # verifier種類とPASS条件例

/GOVERNANCE/
  contribution.md               # 追加・淘汰・審査ルール
  security.md                   # hash/署名/汚染対策

/MODELS/
  registry.json                 # 登録モデル一覧（id,version,tags）

/schemas/                       # JSON Schema
/examples/                      # inputs.jsonl、expectedの例
/manifests/                     # サンプルmanifest
/metrics/                       # metric_v1定義
/audit/                         # audit_set_v1
```

これだけあれば「誰かが作る」が起きやすいです。

## 2. READMEの冒頭テンプレ（これが一番効く）

1. **1行**：DSLとは何か
2. **3行**：なぜ speed-only はダメか（拒否テンプレ問題）
3. **図**：route→infer→verify→log→learn(router)（MermaidでOK）
4. **MVP**：JSON only（最初の成功条件）
5. **Help wanted**：issueへのリンク（3つ）

## 3. "プロトコル要約"は1枚に潰す

DSL_PROTOCOL_V0_1.md にこれだけ書けばOK：

- manifest.json 必須フィールド
- run_log.jsonl 必須フィールド
- metric_v1（q0/q1/cの定義）
- audit_set_v1（形式だけでも）
- stable昇格条件（PASS率など）

## 4. Issueを切る（最小3つ）

1. **MVP runner**
2. **q1 metrics**
3. **audit set**

**DoD（完了条件）**を箇条書きで入れる。

## 5. プロトコル仕様（最低限のI/O契約）

実装者が動けるように、ログ形式とイベントを決める。

### イベントタイプ

- `INFER_REQUEST`
- `INFER_RESULT(model_id, time_ms, tokens, output_hash, verifier_score)`
- `SELECT_TRAIN_EXAMPLE(prompt_hash, winner_model_id)`
- `MODEL_ADD_REQUEST(reason, stats_snapshot)`
- `EVAL_METRIC_CHANGE(old_metric, new_metric, epoch)`

ここがホワイトペーパーの価値を決めます。

## 6. 指標の"置換"手順（ガバナンス）

プロジェクトの強みである「指標を固定しない」を、手順に落とす。

- 切替条件（劣化検知）
- 移行期間（混在ウィンドウ）
- 過去ログとの互換性
- 再現性の担保（バージョン付け）

これが無いと「途中で変えたらおじゃん」論に負けます。

## 7. 初期モデル集合の設計指針

- 最小カバレッジ（領域数の下限）
- 重複許容（重なりを許す/許さない）
- "未知"の扱い（拒否モデル or ベースモデル）
- 初期バイアスの吸収方針（後段で指標切替）

## 8. 選択モデル（Selector）の仕様

- **入力**：プロンプト特徴（テキスト／埋め込み）
- **出力**：モデルIDの分布
- **学習データ**：(prompt, winner_model)
- **失敗時フォールバック**：上位k本を試す、など

## 9. 実験を"他人にやらせる"具体ルート

### 9.1 研究者ルート

- arXiv に conceptual paper
- タイトルに distributed / proxy / specialization を入れる
- 「We invite falsification」系の書き方
- → 壊しに来る人が現れる

### 9.2 OSS / Hacker ルート

- GitHub repo（コード空）
- Issues に実験案、想定FAIL、比較手法
- → 誰かが勝手にPoCを書く

### 9.3 反AI中央集権勢ルート（かなり強い）

- 「巨大GPU前提にNOを突きつける構造」
- ローカル実行、セキュリティ
- これは思想的支持者がつく。

## 10. 自分で実験しないための最低条件

### 条件A：反証可能であること

「うまくいくはず」ではダメ。どこで失敗するかが明記されていること。

プロジェクトの構想はすでに：
- 初期モデル依存
- proxy破綻
- 雑即答優位

と失敗条件が明確 → これは強み。

### 条件B：実験が"安い"こと

- GPU必須 ❌
- 大規模データ ❌
- ✔ 小モデル
- ✔ 機械検証可能タスク
- ✔ 数日で終わる

→ 第三者が試せる

### 条件C：実験したくなる"報酬"があること

報酬は金でなくていい。
- 論文化しやすい
- ブログネタになる
- 批判しやすい（←重要）

人は「壊せそうな理論」を試す。

## 11. ホワイトペーパーを「実験仕様書」に寄せる

今の内容を：
- 思想 30%
- 検証プロトコル 70%

に振り切る。

必須項目：
- 仮説 H
- 最小実験 T
- PASS / FAIL 条件
- 想定される破れ方

これ、もうほぼ書けてます。

## 12. 「PoC不要宣言」を明示する（逆に重要）

READMEにこう書く：

```
This proposal intentionally provides no reference implementation.
The goal is to enable independent verification and falsification.
```

これは逃げではなく、分散研究を誘発する宣言。
