# DSOC Setup Validation

Use this guide to verify that a contributor can set up VoiceyBill and prove the setup with clear evidence.

Program link: https://www.devweekends.com/dsoc/

## What Counts As Validation

The program requires proof, not just a claim that something works.

- If a setup step shows visible UI, include a screenshot.
- If a setup step includes navigation, login, onboarding, or any interactive flow, include a short video or screen recording.
- If a step is command-line only, paste the exact output in the issue or pull request.
- If a step is both visible and command-line driven, include both the output and the media.

## Preflight Checks

Run these checks before setup:

```bash
node --version
npm --version
git --version
docker --version
docker compose version
```

Use the versions required by the repository you are working in. If a check fails, fix the environment before continuing.

## Setup Verification Flow

1. Clone the relevant repository.
2. Install dependencies.
3. Configure the environment file.
4. Start any required local services.
5. Run the app, API, or dashboard.
6. Confirm the expected output appears.
7. Capture screenshots or a video if the setup produces a visible result.

## Evidence To Capture

| Step type | What to capture |
| --- | --- |
| Backend startup | Server logs, health check output, and any MongoDB or API connection message |
| Web setup | Build output, local URL, and a browser screenshot if the page loads |
| Mobile setup | Metro Bundler output and a device or simulator screenshot |
| UI flow | Screenshot plus screen recording if the flow is interactive |
| Failure case | The exact error output and any relevant screenshot or recording |

## Submission Rules

- Include the setup steps you followed.
- Include the exact commands you ran.
- Include the output that proves success.
- Include screenshots or video links whenever the setup has a visible result.
- Mention any machine-specific notes such as OS, simulator, device, or Docker configuration.

## Ready To Share

Before you open an issue or pull request, make sure you can answer yes to all of these:

- The setup path is reproducible.
- The validation output is included.
- Screenshots or video are attached when the setup is visible.
- The instructions are clear enough for another contributor to follow.