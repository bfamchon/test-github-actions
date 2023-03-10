# How to GitHub Actions

## Setup project

`npx create-next-app --ts`

## Declare your wanted workflow

We're gonna build a workflow that notify when a new PR is opened
### Setup slack webhook

Create a new app `https://api.slack.com/apps/` and activate `Features/Incoming Webhooks`, linking on the channel you want to post.

### Setup GitHub Secrets

Go to your project's settings under `Secrets and variables` and declare a new `Repository Secret`, ours is `SLACK_WEBHOOK`.
### Write workflow

Get back to your code directory and make a `.github/workflows/slack-notify.yml` file were we will declare our workflow.

```yaml
on:
  pull_request:
    # types: [opened, reopened]
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
        SLACK_WEBHOOK: ${{ secrets.SLACK_WEBHOOK_TRIBE }}
        SLACK_USERNAME: PR_BOT
        SLACK_ICON_EMOJI: ":building_construction:"
        SLACK_MESSAGE: A pull-request named `${{ github.event.pull_request.title }}` (${{ github.event.pull_request.html_url }}) has been opened and waiting your review
        SLACK_COLOR: ${{ job.status }}
        SLACK_FOOTER: "Good job ! :rocket:"
        MSG_MINIMAL: true
```