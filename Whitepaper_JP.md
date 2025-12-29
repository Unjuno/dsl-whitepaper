# Distributed Specialist Learning (DSL) Whitepaper v1.3
**副題**: 分散「特化差分集合 + ルーティング + 検証 + 淘汰」で、巨大GPUなしでも“集合として強い”応答をローカルに届ける  
**版**: v1.3（運用可能仕様 / MVP値を含む）  
**日付**: 2025-12-29（Asia/Tokyo）  

---

## 0. 要旨（Abstract）
DSLは、基礎モデル \(M_0\) と特化差分 \(\Delta_k\) の集合を維持し、入力ごとに selector が候補を絞ってローカルで **少数（1〜2）だけ実行**する。  
“最速だけ強化”は速い拒否/テンプレ（速いゴミ）を強化して破綻するため、DSLは **verifier足切り + 合成報酬（速度はコスト）** をMUSTとする。

- verifier足切り（PASSのみ勝者候補）
- 速度は報酬ではなくコスト：\(R=q_0+\beta q_1-\lambda c-\pi\cdot\text{RefusalPenalty}\)
- quota + top-k 探索（単一支配を防ぐ）
- spawn/prune（増殖と淘汰）
- Metric Registry（指標置換）
- manifest/監査ログ/スキーマ/ガバナンス（分散運用の契約）

---

## 1. 分散学習の3モード（定義）
- DL-1 分散評価：多数モデル比較→勝者ログ生成  
- DL-2 分散更新：勝者ログで特化差分更新→提出（LoRA等）  
- DL-3 分散供給：検証・署名・監査ログで受け入れ配布し淘汰  

MVPは DL-1 + DL-2（非集約）を採用。

---

## 2. 二層品質（q₀/q₁）と合成報酬（必須）
qを曖昧にすると破綻するため二層化する。
- q₀：verifier PASS（0/1）
- q₁：タスク固有スコア（正規化[0,1]）
- c ：コストproxy（TTFT/TPS/total/tokens/memory等）

---

## 3. selector学習（スケールの関門）
- 特徴：入力埋め込み + メタ特徴
- 教師：勝者one-hotではなく soft label（候補R分布）
- 新規モデル冷遇対策：quota（n_min）で最低試行保証
- 推論時：k_infer=1〜2固定（ローカルコスト一定化）

---

## 4. MVP固定値（推奨レンジ）
|parameter|推奨初期値|
|---|---:|
|k_infer|1〜2|
|k_train|4|
|n_min|50|
|tau|0.15|
|rho|0.08|
|lambda|0.3|
|pi|1.0|
|beta|1.0|
|tau_s|0.25|

計測は load_ms と gen_ms を分離し、各入力3回測定の中央値を採用（warm/coldも記録）。

---

## 5. 参考文献（抜粋）
Switch Transformers arXiv:2101.03961 / LoRA arXiv:2106.09685 / QLoRA arXiv:2305.14314 / FedAvg arXiv:1602.05629
