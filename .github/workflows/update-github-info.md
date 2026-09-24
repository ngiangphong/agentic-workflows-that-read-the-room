---
name: update-github-info
description: Keep the GitHub Info page current with official GitHub updates.
on:
  schedule: daily
  workflow_dispatch:
permissions: read-all
engine:
  id: copilot
  model: gpt-5-mini
tools:
  github:
    toolsets: [repos]
  edit:
  web-fetch:
network:
  allowed:
    - defaults
    - github.blog
    - github.com
    - awesome-copilot.github.com
safe-outputs:
  create-pull-request:
    title-prefix: "[github-info] "
    draft: true
    if-no-changes: ignore
    allowed-files:
      - site/content/github-info.md
---

# Update GitHub Info

Refresh the website content for Mona's review.

## Source and repository guidance

1. Read `notes/mona-notes.md` before making any changes.
2. Use the `web-fetch` tool to fetch and read:
   - https://github.blog/latest/
   - https://github.blog/changelog/
   - https://awesome-copilot.github.com/workflows/
3. Use the GitHub repository API tools to read relevant repository guidance and reference files, including the current `site/content/github-info.md`. Do not use terminal commands, the GitHub CLI, or sandboxed shell commands for repository guidance or file lookups.

## Update

Use the official GitHub Blog, Changelog, and Awesome Copilot workflows sources to identify concise, practical updates that fit Mona's editorial angle. Preserve useful existing content, mention the source for each new item, and keep the page focused on helping developers learn GitHub faster.

Edit only `site/content/github-info.md`. If there is no worthwhile, source-backed update, leave the file unchanged. When there are changes, use the `create-pull-request` safe output to open a draft pull request with a clear summary and ask Mona to review it. Never write directly to the default branch.