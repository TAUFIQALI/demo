# Notes for Claude

This repo is the Haukao Shopify theme (UK store, GBP, Shopify Basic plan).

- Read `docs/storefront-redesign-brief.md` before any design or theme work. It is the source of truth for colours, type, layout and rules.
- Theme files (`assets/`, `config/`, `layout/`, `locales/`, `sections/`, `snippets/`, `templates/`) live at the repo root once added.
- Never invent reviews, stock urgency, delivery times, discounts or trust claims.
- Don't change product/collection handles, checkout, payment or policy settings.
- Don't edit `config/settings_data.json` by hand unless asked: the theme editor writes it and conflicts are common.
- Run `shopify theme check` after Liquid changes when the CLI is available.
- No secrets or customer data in commits.
