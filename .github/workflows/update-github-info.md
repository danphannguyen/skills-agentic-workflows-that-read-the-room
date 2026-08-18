---
name: update-github-info
description: Refreshes GitHub news content daily or on demand and proposes updates via pull request for Mona review
on:
  schedule: daily
  workflow_dispatch:
permissions:
  contents: read
  pull-requests: read
  issues: read
engine: copilot
tools:
  edit:
  web-fetch:
  github:
    toolsets: [repos, pull_requests]
network:
  allowed:
    - defaults
    - github.com
    - github.blog
safe-outputs:
  create-pull-request:
    title-prefix: "[github-info] "
    labels: [automation, content]
    draft: true
---

# Mission

Update the GitHub information page and open a pull request for Mona to review.

## Required Inputs and Sources

1. Read notes/mona-notes.md first.
2. Use web-fetch to read https://github.blog/latest/.
3. Use web-fetch to read https://github.blog/changelog/.
4. Read repository guidance and reference files with GitHub repository API tools (not terminal, CLI, or sandboxed shell commands).

## Update Task

1. Update site/content/github-info.md with concise, accurate, and current highlights based on the fetched sources and notes.
2. Keep edits focused, factual, and easy to scan.
3. If uncertain, prefer fewer statements over speculative content.

## Output and PR Rules

1. Do not write directly to main.
2. Use the safe output create-pull-request to propose the change.
3. In the PR title or body, clearly indicate it is for Mona to review.
4. Include a short summary of what changed and source URLs used.
