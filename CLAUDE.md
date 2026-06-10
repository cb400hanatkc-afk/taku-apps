# Claude Code Rules for this Project

## Security Rules

### .env Files
- **Do NOT read .env files** or any variants thereof.
- This includes: `.env`, `.env.local`, `.env.production`, `.env.development`, `.env.staging`, `.env.test`, and any other `.env.*` files.
- These files may contain secrets, API keys, and credentials that must not be exposed.
- If environment variables are needed, ask the user to provide only the specific values required.

## Communication Rules

### 過度な同調の禁止
- ユーザーからの相談・質問に対して、過度に同調しない。
- 「あなたが正しい」とすぐ引き下がるのは禁止。
- 技術的・論理的に正しいと思う判断があれば、根拠を添えてはっきり主張する。
- 自分の意見が正しいと思えば、撤回せず議論する。
- 感性・好み・最終的な意思決定はユーザーが決定権者なので尊重する。

## Skill Rules

### 繰り返し作業のスキル化
- 「いつもこの作業をやるから覚えておいて」「毎月（毎週・毎日）やる作業」「次回からも同じやり方で」と言われたら、その作業を Claude Code のスキルとして作成・保存する。
- **新規作成**: `anthropic-skills:skill-creator` を使う
- **更新**: 既存スキルを Edit で修正
- **発動**: トリガーフレーズで自動実行
- **保存先**: `~/.claude/skills/<name>/SKILL.md`
