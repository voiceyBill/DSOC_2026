# Contributing to VoiceyBill - DSOC 2026

Thanks for participating in DSOC. This guide covers what you need to contribute to any VoiceyBill repository during the program.

Program link: https://www.devweekends.com/dsoc/


## Repositories

| Repo | What it covers |
|---|---|
| [voiceyBill-server](https://github.com/voiceyBill/voiceyBill-server) | Express API, MongoDB, auth, AI pipeline |
| [voiceyBill-web](https://github.com/voiceyBill/voiceyBill-web) | React 19 web client |
| [voiceyBill-App](https://github.com/voiceyBill/voiceyBill-App) | React Native / Expo mobile app |

Each repository has its own issue templates, PR template, and contributing guide. Always work inside the correct repo for the area you are changing.


## Issues

Issues of all kinds are welcome across all repositories. You do not need permission or an invitation to open one. Bug reports, feature ideas, questions, suggestions, discussions, and anything else are all fair game.

When your issue matches one of the templates below, use it. GitHub shows the picker automatically when you click New Issue:

- **Bug report** - a reproducible defect with steps, expected result, and actual result
- **Feature request** - a new feature or improvement with a clear problem statement
- **Question** - usage, setup, or clarification help

If your issue does not fit any of those templates, open a blank issue and describe it clearly. You are not limited to those three categories. The templates exist to make triage easier, not to restrict what you can raise.

**Rules:**
- Do not leave required template fields empty
- Keep one issue focused on one topic
- Include a screenshot, GIF, or short recording for anything visual or hard to explain in text
- Link a related issue when the report is a follow-up
- Review [ideas.md](ideas.md) before proposing new features to avoid duplicates


## Pull requests

Every pull request must use the PR template from the repository you are contributing to. GitHub loads it automatically when you open a PR.

A complete PR includes:

- **Summary** - what changed and why, not just which files were touched
- **Related issues** - link using `Closes #N` or `Related to #N`
- **Type of change** - check the correct box
- **How to test** - steps a reviewer can follow to verify the change locally
- **Validation output** - paste the actual output of lint, build, or type-check commands
- **Screenshots or recordings** - required for any UI change, setup change, or visible behavior
- **Breaking changes** - note any migration steps if applicable
- **Checklist** - all boxes checked before requesting review

PRs with incomplete sections or missing validation output will be sent back for updates.


## AI policy

AI tools including Claude, GitHub Copilot, and ChatGPT are permitted and encouraged during DSOC. The following rules apply.

**What is allowed:**
- Using AI to write, debug, or refactor code
- Using AI to draft issue descriptions, PR summaries, or documentation
- Using AI to understand the codebase or generate test cases

**What is required:**
- Disclose AI assistance in every PR that contains AI-generated content. Add a co-author line to your commit or note it in the PR summary:

```
Co-Authored-By: Claude Sonnet 4.6 <noreply@anthropic.com>
```

- Review everything AI produces. You are responsible for the correctness and quality of every line you submit, regardless of how it was written.
- Be able to explain any section of your PR if a reviewer asks. If you cannot explain it, do not submit it.

**What is not allowed:**
- Submitting AI-generated code you have not read or understood
- Using AI to fabricate validation output, test results, or screenshots
- Claiming sole authorship of work that is substantially AI-generated


## Branch and commit conventions

- Target the `dev` branch. Never push directly to `main`.
- Follow [Conventional Commits](https://www.conventionalcommits.org/):
  - `feat(web): add budget progress bar`
  - `fix(api): correct recurring transaction query`
  - `docs(dsoc): update AI policy`


## Contributor checklist

- [ ] Correct issue template used, or blank issue with clear description
- [ ] Issue is focused on one topic
- [ ] PR template fully completed with no sections left empty
- [ ] AI assistance disclosed if applicable
- [ ] Validation output included
- [ ] Screenshot, GIF, or recording attached for visual changes
- [ ] Related issue linked
- [ ] Feature idea checked against [ideas.md](ideas.md) when applicable
