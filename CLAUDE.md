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
