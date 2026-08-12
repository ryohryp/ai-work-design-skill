# Skill検証

`ai-work-design` は、次の2種類のEvalで検証します。

## 1. クロスプラットフォーム手動Eval

[eval-cases.md](eval-cases.md) のE01〜E06を、新しい会話でCodexとClaude Codeの両方へ入力します。

- Codex: `<INVOKE>` を `$ai-work-design` に置き換える
- Claude Code: `<INVOKE>` を `/ai-work-design` に置き換える
- E03はSkill名を付けず、暗黙起動しないことを確認する

結果は [results-template.md](results-template.md) に記録します。

この比較で重視するのは文章表現の一致ではなく、次の判断原則です。

- Gateを無視しない
- 検証容易性と失敗影響度を分ける
- AIへ具体的な役割を与えつつ、必要な決定権を人間に残す
- AIの自己チェックだけを独立検証としない
- 自律化しない結論も認める
- 未確認事項を推測で埋めない
- 曖昧な依頼では、実装へ飛ばず目的を確認する

## 2. Agent Skills自動Eval

Skill本体には [`skills/ai-work-design/evals/evals.json`](../skills/ai-work-design/evals/evals.json) を収録しています。

これはAgent SkillsのEval形式で、出力品質を反復検証するためのケースです。対話全体を一度に採点しにくいケースについては、必要な前提をプロンプトに含め、1回の実行で判断原則を観測しやすくしています。

現在の自動Evalは次を対象にします。

1. 通常業務でのタスク分解・意味のある委譲・独立検証
2. 未承認環境・機密情報でのGate停止と未確認事項の保持
3. 人事評価でのL4過剰委譲の抑制
4. 請求書でのAI自己チェック拒否と独立検証
5. 「AI化」が目的になっている場合の目的の置き直しと適切な質問

単なる製品比較でSkillが誤起動しないこと（手動Eval E03）は、Skillを強制ロードする出力Evalでは測れないため、手動のトリガー検証として残しています。

### Claude Codeでの実行

Claude Codeの `skill-creator` を利用できる環境では、このSkillを評価するよう依頼し、`evals/evals.json` を使って分離実行・採点・ベンチマークを行えます。

例:

```text
skill-creator を使って ~/.claude/skills/ai-work-design を評価してください。
既存の evals/evals.json を使い、with-skill の各ケースを実行・採点してください。
可能なら without-skill も実行し、Skillによる改善を比較してください。
```

実際の配置場所に合わせてSkillパスは変更してください。

## ベンチマーク履歴

- [2026-08-12 Claude.ai 初回ベンチマーク](results/2026-08-12-claude-ai/benchmark.md)
  - with-skill: 100%
  - without-skill: 8%
  - 同一エージェントが実行と採点を担当したため、独立した性能証明ではなく回帰テスト用の初期基準として扱う
  - この実行で見つかったEvalの穴を受け、通常ケースの意味のある委譲、Gate停止時の推測禁止、曖昧依頼で質問ゼロを許さない条件を追加した

今後の結果は `tests/results/YYYY-MM-DD-<environment>/` に残し、同じSkill版・同じEval版で比較できるようにします。

## 判定の考え方

モデルや環境で質問順、言い回し、L1/L2の境界が多少異なることは許容します。

一方、次の差はSkill側の修正候補です。

- 片方だけGateを通過してしまう
- 高影響な最終判断を片方だけL4へ上げる
- 片方だけAI自己チェックを検証として認める
- 既知情報を何度も聞き直す
- 一度に巨大なフォームを提示する
- 質問すべき曖昧さがあるのに質問ゼロで実装へ進む
- 最終シートに判断理由や未確認事項が残らない

環境差をモデルの個性として片付ける前に、`SKILL.md` の判断原則をより明確にできないか検討します。
