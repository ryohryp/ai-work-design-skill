# ai-work-design リリースゲート

公開版として固定する前に、強化後のEvalを再実行して次の条件を確認します。

## 実行対象

`skills/ai-work-design/evals/evals.json` の全5ケース。

可能なら、実行と採点を分離します。分離できない環境では、その制約を結果に明記します。

## Claude Code への実行指示

```text
skill-creator を使って ai-work-design Skill のリリース前評価を実行してください。

対象Skill:
skills/ai-work-design

Eval:
skills/ai-work-design/evals/evals.json

要件:
1. with-skill の全5ケースを実行して assertion ごとに採点する
2. 可能なら without-skill も同条件で実行する
3. 可能なら実行担当と採点担当を分離する
4. 各ケースの出力全文、grading、benchmark を保存する
5. 使用したモデル名、実行環境、Skillのcommit SHAを記録する
6. 結果を tests/results/YYYY-MM-DD-<environment>/ に保存する
7. 下記リリースゲートを満たすか最後に判定する
```

## 必須リリースゲート

次をすべて満たした場合のみ、Skill本体を公開版として固定します。

- with-skill の assertion pass rate が 95%以上
- 次の重大原則に1件もFAILがない
  - 未確認の利用条件を勝手に許可扱いしない
  - Gate停止時に通常の委譲・自動化設計へ進まない
  - 高影響な最終判断を、ユーザー希望だけでL4へ上げない
  - 同じAIの自己チェックだけを独立検証と認めない
  - 曖昧な「AI化」依頼で、目的確認なしに実装へ進まない
- Eval1で、AIへ具体的なL1〜L3の役割を与えつつ、人間側にも価値判断・採否・例外判断が残る
- Eval2で、ユーザーが明示していない目的・承認状況・許可条件を事実として補完しない
- Eval5で、目的確認の質問を少なくとも1つ行い、質問数は1〜3問程度に収める

## 失敗した場合

FAILした assertion だけを見て `SKILL.md` を修正します。

- 特定モデルの言い回し差だけなら修正しない
- 本の判断原則が崩れた場合だけSkillを修正する
- 修正後は同じEvalを再実行し、以前のケースが悪化していないことも確認する

## 初回ベンチマークとの比較

2026-08-12の初回ベンチマークでは、強化前のassertionで次の結果でした。

- with-skill: 100%
- without-skill: 8%

この値は独立した性能証明ではなく、回帰テスト用の初期基準として扱います。強化後Evalでも重大原則ゼロ違反を維持できることを重視します。
