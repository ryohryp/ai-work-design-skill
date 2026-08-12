# AI仕事設計 Skill

書籍『AI仕事設計』公式コンパニオンです。

本書で説明する「AI仕事設計の八つの問い」を、AIとの対話を通じて自分の仕事へ適用し、保存・レビューできる「AI仕事設計シート」にまとめます。

> 書籍ページ: 公開後に追加予定（`BOOK_URL_TODO`）

このリポジトリは、本の内容を要約したり代替したりするものではありません。本でフレームワークを理解した読者が、実際の業務を設計するための実践ツールです。

`SKILL.md` を中心とした Agent Skills 形式で作っているため、CodexとClaude Codeで同じSkill本体を利用できます。環境ごとに別のフレームワークを保守する必要はありません。

## 何ができるか

- 対象業務の「本当の目的」を整理する
- AIを利用してよい条件を最初に確認する
- 業務を実際のタスクへ分ける
- タスクごとに、確かめやすさと失敗時の影響を見極める
- 人間とAIの役割分担をL0〜L4で決める
- 製品名ではなく、必要な文脈・権限・能力から道具を選ぶ
- AIの間違いを発見する具体的な検証方法を決める
- 自律化する場合の境界と安全策を設計する
- Before / Afterと見直し条件を残す

一度に巨大なフォームを埋める必要はありません。AIが会話から分かっていることを再質問せず、曖昧な点だけを順に確認します。

## 八つの問い

1. **利用条件を確認する** — その環境・情報・権限でAIを使ってよいか。
2. **分ける** — 業務は、どの実タスクに分かれるか。
3. **見極める** — 正しさを確かめやすいか。失敗時の影響は大きいか。
4. **任せる** — どこまでAIへ任せ、どの判断を人間に残すか。
5. **道具を選ぶ** — 必要な文脈・権限・実行能力・利用環境は何か。
6. **確かめる** — 間違いをどう発見し、何と照合するか。
7. **自律化する** — L4候補の境界、観測、復旧、上限をどう設計するか。
8. **残す** — 導入前後をどう比べ、いつ見直すか。

## 使い方

### Codex

#### 1. Skillをインストールする

**Skillインストーラーを使う場合**

Codexへ次のように依頼します。

```text
$skill-installer で https://github.com/ryohryp/ai-work-design-skill の skills/ai-work-design をインストールしてください
```

**手動で配置する場合**

このリポジトリをダウンロードまたはcloneし、`skills/ai-work-design` フォルダを個人用Skillフォルダへコピーします。

- macOS / Linux: `$HOME/.agents/skills/ai-work-design`
- Windows: `%USERPROFILE%\.agents\skills\ai-work-design`

CodexがSkillを認識しない場合は、Codexを再起動してください。Skillの公式仕様と配置場所は、[OpenAI公式ドキュメント](https://developers.openai.com/codex/skills)でも確認できます。

#### 2. 対話を始める

Codex CLIまたはIDE拡張では、`$` でSkillを明示できます。

```text
$ai-work-design を使って、毎週の売上報告作成を見直したいです。
```

ChatGPTデスクトップアプリでもStandalone Skillを利用でき、Skillが利用可能な状態なら `@` で明示して呼び出せます。利用方法や対応環境は、[OpenAI公式ドキュメント](https://developers.openai.com/codex/skills)で最新情報を確認してください。

### Claude Code

#### 1. Skillをインストールする

このリポジトリの `skills/ai-work-design` を、Claude CodeのPersonal Skillフォルダへコピーします。

- macOS / Linux: `$HOME/.claude/skills/ai-work-design`
- Windows: `%USERPROFILE%\.claude\skills\ai-work-design`

特定のプロジェクトだけで使いたい場合は、そのリポジトリ内の `.claude/skills/ai-work-design` に配置できます。

Claude CodeのSkill仕様と配置場所は、[Anthropic公式ドキュメント](https://code.claude.com/docs/en/skills)で確認できます。

#### 2. 対話を始める

Claude Codeでは、`/` でSkillを明示して呼び出せます。

```text
/ai-work-design 毎週の売上報告作成を見直したいです。
```

依頼内容がSkillの `description` と一致する場合は、Claudeが自動的にSkillを選ぶこともできます。

### 共通の流れ

最初に確認されるのは、対象業務と目的です。その後、利用条件のGateを通過できた場合だけ、八つの問いを順に進めます。

対話の最後に、次の内容を含むMarkdown形式の「AI仕事設計シート」が生成されます。

- 利用条件のGate判定
- タスク分解と評価
- 現在・目標の委譲レベル
- 人間に残す判断
- 道具の要件
- 独立した根拠を使う検証方法
- 自律化の可否と安全設計
- Before / After、効果測定、見直し条件
- 未確認事項と意思決定の理由

そのまま `.md` ファイルへ保存し、上司、同僚、情報管理・法務担当者など、必要な人とレビューできます。

## 大切にしていること

- AI利用が禁止・不適切なら、設計を先へ進めません。
- すべてをAIへ任せることを成功とは考えません。
- L4の候補がなければ「自律化しない」を正しい結論として認めます。
- 「人間が確認する」だけで済ませず、照合先と判定方法を具体化します。
- AI自身の出力だけを、AI出力の正しさの根拠にはしません。
- 特定のAI製品へ依存しない設計を優先します。

## 例

[会議後処理の簡単な例](examples/simple-example.md)を収録しています。特定企業の情報や、書籍で扱う出版プロジェクトの完全なケーススタディは含めていません。

## 検証

Skillの変更で挙動が崩れていないか確認するため、[手動Evalケース](tests/eval-cases.md)を用意しています。

通常ケースだけでなく、未承認環境でのGate停止、L4の過剰委譲、AIの自己チェックだけを検証とみなすケース、単なる製品比較でSkillが誤起動しないことなどを確認します。

同じEvalケースをCodexとClaude Codeの両方で実行すると、モデルや実行環境による挙動差も比較できます。

## ファイル構成

```text
README.md
LICENSE
skills/
  ai-work-design/
    SKILL.md
    agents/
      openai.yaml
    references/
      worksheet.md
examples/
  simple-example.md
tests/
  eval-cases.md
```

`SKILL.md` と `references/worksheet.md` が共通のSkill本体です。`agents/openai.yaml` はOpenAI側のSkill一覧表示などに使う任意メタデータで、Claude Code向けに別のSkill本文を持つ必要はありません。

Webアプリ、MCP、バックエンド、認証、データベース、外部依存関係はありません。

## ライセンス

[MIT License](LICENSE)で公開します。
