# AI仕事設計 Skill

書籍『AI仕事設計』の公式コンパニオンです。

**「この仕事、AIにどこまで任せればいい？」を、AIとの対話で整理するためのツール**です。

難しい設定はなるべく必要ありません。Codex または Claude Code を使っている方なら、下の文章をそのままコピーして導入できます。

> 書籍ページ: 公開後に追加予定（`BOOK_URL_TODO`）

## まずはこれだけ

必要なのは **Codex または Claude Code のどちらか**です。

### Codexを使う場合

最初の1回だけ、Codexに次の文章を送ってください。

```text
$skill-installer を使って、
https://github.com/ryohryp/ai-work-design-skill の
skills/ai-work-design を個人用Skillとしてインストールしてください。

インストール後、ai-work-design が使える状態か確認してください。
```

導入できたら、あとは仕事について相談するだけです。

```text
$ai-work-design を使って、毎週の売上報告作成を見直したいです。
```

### Claude Codeを使う場合

最初の1回だけ、Claude Codeに次の文章を送ってください。

```text
https://github.com/ryohryp/ai-work-design-skill の
skills/ai-work-design を、私の個人用Claude Code Skillとしてインストールしてください。

OSに合った個人用Skillフォルダを使ってください。
すでにインストール済みなら最新版へ更新してください。
インストール後、/ai-work-design が使える状態か確認してください。
```

導入できたら、次のように始めます。

```text
/ai-work-design 毎週の売上報告作成を見直したいです。
```

## 使うとどうなる？

AIが最初から長い質問票を出すことはありません。

たとえば、

```text
会議議事録をAI化したいです。
```

と相談すると、いきなり自動化方法を決めるのではなく、まず「会議のあとに何を実現したいのか」を一緒に整理します。

その後、仕事を小さく分けながら、

- そもそもAIを使ってよい仕事か
- AIに任せやすい部分はどこか
- 人間が判断した方がよい部分はどこか
- AIの間違いをどう発見するか
- 自動化するなら、どこまで許可するか

を順番に考えます。

最後に、話した内容を **「AI仕事設計シート」** としてまとめます。

## このSkillが大切にしていること

このSkillは、何でもAIに任せるためのものではありません。

AIを使ってはいけない条件なら、そこで止まります。人間が判断した方がよい仕事は、人間に残します。AIが作った答えを、同じAIにもう一度確認させただけで「検証できた」とは扱いません。

**AIをたくさん使うことではなく、人間とAIの役割分担を理由を持って決めること**が目的です。

## 八つの問い

書籍『AI仕事設計』では、仕事を次の八つの問いで見直します。

1. 利用条件を確認する
2. 分ける
3. 見極める
4. 任せる
5. 道具を選ぶ
6. 確かめる
7. 自律化する
8. 残す

Skillは、この八つを一度に聞くのではなく、会話しながら必要な順番で進めます。

## うまく動かないとき

まず、次のようにSkill名を明示して呼び出してください。

- Codex: `$ai-work-design`
- Claude Code: `/ai-work-design`

それでも認識されない場合は、CodexまたはClaude Codeを一度再起動してみてください。

詳しい導入方法は、それぞれの公式ドキュメントでも確認できます。

- [OpenAI: Skills](https://developers.openai.com/codex/skills)
- [Anthropic: Claude Code Skills](https://code.claude.com/docs/ja/skills)

<details>
<summary>手動でインストールしたい方・技術的な詳細を見る</summary>

### Skill本体

共通のSkill本体は次のフォルダです。

```text
skills/ai-work-design/
```

Codexの個人用Skillは通常、次の場所に置きます。

```text
$HOME/.agents/skills/ai-work-design
```

Claude Codeの個人用Skillは通常、次の場所に置きます。

```text
$HOME/.claude/skills/ai-work-design
```

Claude Codeでは、特定プロジェクトだけで使う場合 `.claude/skills/ai-work-design` に配置することもできます。

`SKILL.md` と `references/worksheet.md` が共通のSkill本体です。CodexとClaude Codeで別々の内容を保守する必要はありません。

</details>

## 例

[会議後処理の簡単な例](examples/simple-example.md)を収録しています。

書籍で扱う出版プロジェクトの完全なケーススタディは、このリポジトリには収録していません。本では「なぜその役割分担にしたのか」という判断の過程まで説明します。

## 検証について

このSkillが意図した判断を続けられるか、複数のテストケースで確認しています。

2026-08-12のリリースゲートでは、強化後29項目に対して **29/29 PASS** でした。未承認環境で停止できるか、高影響な判断を安易に自動化しないか、AI自身の自己チェックだけを検証としないか、といったケースを含みます。

[検証結果を見る](tests/results/2026-08-12-claude-ai-release-gate/release-gate-verdict.md)

この結果は独立した性能保証ではなく、Skillの変更で重要な判断原則が崩れていないかを見るための回帰テストとして利用しています。

## ライセンス

[MIT License](LICENSE)で公開しています。
