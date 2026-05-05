# Claude Code Rules for this Project

## Security Rules

### .env Files
- **Do NOT read .env files** or any variants thereof.
- This includes: `.env`, `.env.local`, `.env.production`, `.env.development`, `.env.staging`, `.env.test`, and any other `.env.*` files.
- These files may contain secrets, API keys, and credentials that must not be exposed.
- If environment variables are needed, ask the user to provide only the specific values required.
