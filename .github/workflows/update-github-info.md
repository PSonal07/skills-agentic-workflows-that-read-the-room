---
name: update-github-info
description: Draft website updates for Mona's GitHub Info site from official GitHub sources.
intent: Keep GitHub Info practical and current with useful developer guidance from official GitHub Blog and Changelog updates.
on:
  schedule:
    - cron: "0 9 * * *"
  workflow_dispatch:
  skip-if-match: 'is:pr is:open in:title "[GitHub Info]"'
permissions:
  contents: read
  pull-requests: read
  copilot-requests: write
strict: true
engine:
  id: copilot
  copilot-sdk: true
network:
  allowed:
    - github.blog
    - github.com
tools:
  edit: 
  web-fetch: 
  github:
    mode: gh-proxy
    toolsets: [default]
safe-outputs:
  create-pull-request:
    title-prefix: "[mona] "
    draft: true
    fallback-as-issue: false
    allowed-files:
      - site/content/github-info.md
---

# Update GitHub Info

Read `notes/mona-notes.md` and `site/content/github-info.md` first. Fetch:

- https://github.blog/latest/
- https://github.blog/changelog/

Review current official posts for recent, accurate information that helps
developers learn GitHub faster. Add only genuinely useful updates that are not
already covered; keep the page concise and preserve its existing structure and
editorial angle. Attribute each addition to its specific GitHub Blog or
Changelog source with a direct link and publication date. Do not invent details
or change unrelated content.

If there is no practical, non-duplicate update, make no file changes and call
`noop` with a brief reason. Otherwise, edit only
`site/content/github-info.md` and open one pull request for Mona to review. Give
the PR a concise summary and mention the source links. Use the configured
`create-pull-request` safe output; never push changes or write directly to the
default branch.
