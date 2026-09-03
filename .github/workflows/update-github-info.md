---
name: update-github-info
on:
  schedule: daily
  workflow_dispatch:
permissions:
  contents: read
  pull-requests: read
engine: copilot
tools:
  edit:
  web-fetch:
  github:
    toolsets: [repos]
network:
  allowed:
    - github.blog
    - github.com
safe-outputs:
  create-pull-request:
    base-branch: main
    draft: true
    max: 1
---

# Update GitHub Info

Keep Mona's GitHub Info content current while preserving her practical, review-first editorial style.

1. Read `notes/mona-notes.md` before drafting anything.
2. Use the GitHub repository API tools to read repository guidance and reference files, including `README.md`, `site/content/github-info.md`, and any relevant files under `.github/`. Do not use terminal, the GitHub CLI, or sandboxed shell commands for these repository reads.
3. Use the web-fetch tool to fetch:
   - https://github.blog/latest/
   - https://github.blog/changelog/
4. Identify a small set of recent, useful GitHub Blog or Changelog updates that fit Mona's editorial angle. Prefer information that helps developers learn GitHub faster.
5. Update only `site/content/github-info.md` with concise summaries, clear source labels, and links to the official GitHub Blog or Changelog pages. Preserve useful existing content unless it is stale or contradicted by the fetched sources.
6. Review the resulting content for accuracy, concise wording, working source links, and consistency with the repository guidance.
7. Open a draft pull request for Mona to review using the `create-pull-request` `safe-outputs`. Target `main`, explain what changed and cite the source pages. Do not write directly to `main` and do not modify files outside `site/content/github-info.md`.

If there are no substantive updates worth publishing, leave the file unchanged and do not open a pull request.
