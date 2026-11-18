---
name: update-github-info
description: Propose practical updates to the GitHub Info page from official GitHub Blog sources.
intent: Keep Mona's GitHub Info page current with concise, practical developer guidance grounded in official GitHub Blog sources.
on:
  schedule: daily
  workflow_dispatch:
permissions:
  contents: read
  copilot-requests: write
tools:
  edit: true
  web-fetch
network:
  allowed:
    - github.blog
    - github.com
engine:
  id: copilot
  copilot-sdk: true
safe-outputs:
  create-pull-request:
    allowed-files:
      - site/content/github-info.md
    base-branch: main
    draft: true
    max: 1
---

# Update GitHub Info

Read `notes/mona-notes.md` and `site/content/github-info.md` before making any changes.

Fetch both https://github.blog/latest/ and https://github.blog/changelog/. Find recent, verified updates that are useful to developers and fit Mona's practical editorial angle. Use only claims supported by those sources, and link each update to its specific source article or changelog entry.

If there is a relevant, non-duplicate update, edit only `site/content/github-info.md`. Keep the page concise, practical, and consistent with its existing format. Do not edit any other file.

When you make a meaningful change, use the configured `create-pull-request` safe output to open a draft PR targeting `main` for Mona to review. Summarize the updates and include the source links in the PR description. Do not merge the PR or write directly to `main`.

If neither source contains a useful update, or the evidence is insufficient, make no edits and call `noop` with a brief reason.
