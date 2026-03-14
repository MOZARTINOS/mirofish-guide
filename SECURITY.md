# Security Notes

This repository is documentation and skill material, but it still needs strict data hygiene.

## What Must Not Be Committed

- `.env` files and secret-bearing config files
- API keys, tokens, session cookies, or auth headers
- private datasets or user-submitted source material
- raw simulation uploads or report outputs that contain personal or internal data
- internal-only URLs, hostnames, or infrastructure details

## Safe Contribution Rules

1. Replace secrets with placeholders.
2. Redact names, emails, IDs, and private links from logs and examples.
3. Summarize sensitive artifacts instead of pasting them verbatim.
4. Keep examples synthetic or clearly public.
5. If a file was generated locally and is not clearly intended for version control, do not commit it.

## Scope Of This Repository

This repository should document how to use MiroFish safely and effectively.
It should not become a storage location for production data, private prompts, or organization-specific context.

## Reporting

If you notice a sensitive file or secret in a commit or pull request, open a private report to the repository owner instead of discussing the secret in public.
