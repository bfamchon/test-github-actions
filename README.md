# How to GitHub Actions

## Setup project

`npx create-next-app --ts`

## Declare your wanted workflow

We're gonna build a workflow that notify when a new PR is opened
### Setup slack webhook

### Setup GitHub Secrets

### Write workflow

```yaml
on: pull_request
name: Slack Notification Demo
jobs:
  notify-slack:
    name: Send a notification to Slack channel
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2
    - name: Notify
      uses: rtCamp/action-slack-notify@v2
      env:
        SLACK_WEBHOOK: ${{ secrets.SLACK_WEBHOOK }}
        SLACK_USERNAME: PR_BOT
        SLACK_ICON_EMOJI: ":robot:"
        SLACK_COLOR: ${{ job.status }}
        SLACK_FOOTER: "Good job ! :rocket:"
```

## Profit