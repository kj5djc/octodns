# Copilot Instructions

## Conventional Commits

All commit messages must follow the [Conventional Commits](https://www.conventionalcommits.org/) specification:

```
<type>(<scope>): <short summary>
```

### Types

- `feat` — a new DNS record or zone is added
- `fix` — correcting an existing record (wrong IP, wrong value, wrong TTL, etc.)
- `chore` — maintenance changes (dependency updates, config changes, workflow tweaks)
- `ci` — changes to GitHub Actions workflows
- `docs` — updates to README or other documentation
- `refactor` — restructuring YAML without changing DNS outcomes (e.g. ordering, formatting)
- `remove` — deleting a record or zone

### Scope

Use the domain name as the scope (without the trailing dot):

```
feat(kj5djc.com): add localdev A record
fix(kj5djc.com): correct MX preferences for iCloud Business
remove(kj5djc.com): drop legacy SES DKIM CNAME records
```

If the change spans multiple zones, omit the scope:

```
chore: update octodns and provider dependencies
```

### DNS-Specific Examples

| Scenario | Commit message |
|---|---|
| Add a new A record | `feat(kj5djc.com): add orange A record pointing to 192.168.1.69` |
| Change an A record's IP | `fix(kj5djc.com): update mail A record to new server IP` |
| Add DKIM CNAME for a new provider | `feat(kj5djc.com): add iCloud DKIM sig1._domainkey CNAME` |
| Remove records from an old mail provider | `remove(kj5djc.com): drop SES DKIM CNAMEs and old SPF` |
| Switch MX provider | `feat(kj5djc.com): migrate MX from Google to iCloud Business` |
| Enable Cloudflare proxying on a record | `fix(kj5djc.com): enable Cloudflare proxy on netlog CNAME` |
| Add a new zone file | `feat(example.com): initial zone configuration` |
| Update SPF record | `fix(kj5djc.com): update SPF to include businessmail.apple` |
| Workflow change | `ci: add dry-run step before applying DNS changes` |

### Rules

- Summary line is lowercase, imperative mood, no trailing period
- Keep the summary under 72 characters
- Add a body if the change needs context (e.g. why a record was removed, what service a new record supports)
- Do not commit SOA or NS record changes — those are managed by Cloudflare directly
