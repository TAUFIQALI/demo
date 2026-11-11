# Haukao Shopify theme

Theme source and planning docs for the Haukao storefront (https://www.haukao.com).

## Status

The theme code **has not been added yet**. This repo currently holds:

- `docs/storefront-redesign-brief.md`: the design and implementation brief, including the handoff for Shopify Sidekick.
- `docs/design/haukao-tokens.css`: reference colour tokens and a small custom CSS layer.
- Tooling config for Shopify theme development (`.shopifyignore`, `.theme-check.yml`, a CI workflow).

## Getting the theme into this repo

Choose one route.

### Option A: Shopify GitHub integration (no local tools needed)

1. In Shopify admin: **Online Store → Themes → Add theme → Connect from GitHub**.
2. Select this repository and a branch, for example `theme-redesign`. **Do not use `main` for the live theme until the redesign is approved.**
3. Shopify syncs the theme files both ways: edits in the theme editor commit to the branch, and pushes to the branch update the theme.

Docs: https://shopify.dev/docs/storefronts/themes/tools/github

> To check: Shopify expects theme folders (`assets/`, `config/`, `layout/`, `locales/`, `sections/`, `snippets/`, `templates/`) at the repo root. Confirm that the extra `docs/` and `.github/` folders are ignored by the sync before connecting.

### Option B: Shopify CLI (local development)

```bash
npm install -g @shopify/cli
shopify theme pull --store your-store.myshopify.com   # pick the theme to copy
shopify theme dev                                     # local preview with hot reload
shopify theme check                                   # lint
shopify theme push --unpublished                      # upload as a NEW unpublished theme
```

Docs: https://shopify.dev/docs/storefronts/themes/tools/cli

## Working rules

- **Never push straight to the live theme.** Work on an unpublished theme and publish only after the merchant approves.
- Don't commit secrets, access tokens, or customer data. `.env` files are git-ignored.
- Keep custom CSS small and documented. Prefer theme settings.
- Follow the acceptance checks in the brief before publishing.
