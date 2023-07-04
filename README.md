# es-perf-github-status

Custom GitHub Action for Elasticsearch Performance team used to send notifications about GitHub Action job status.

## v1

The initial version sends notification using Slack. It is based on legacy Slack Incoming Webhooks.

Required inputs:
* `slack_webhook_url` - Slack Incoming Webhook URL
* `slack_channel` - Slack channel name or ID
* `status` - Slack job status description

Example use:

```
env:
  DEFAULT_BRANCH: master

jobs:
  <job-id>:
    steps:
     [..]
      - uses: elastic/es-perf-github-status@v1
        if: ${{ failure() && ( github.event_name == 'schedule' || ( github.event_name == 'push' && github.ref_name == env.DEFAULT_BRANCH ) ) }}
        with:
          slack_webhook_url: ${{ secrets.SLACK_WEBHOOK_URL }}
          slack_channel: ${{ secrets.SLACK_CHANNEL }}
          status: FAILED
```

## v2

This version uses [Slack app](https://github.com/slackapi/slack-github-action#technique-2-slack-app) method.

Required inputs:
* `slack_bot_token` - Slack Bot token
* `slack_channel` - Slack channel ID
* `status` - Slack job status description

Example use:

```
env:
  DEFAULT_BRANCH: master

jobs:
  <job-id>:
    steps:
     [..]
      - uses: elastic/es-perf-github-status@v2
        if: ${{ failure() && ( github.event_name == 'schedule' || ( github.event_name == 'push' && github.ref_name == env.DEFAULT_BRANCH ) ) }}
        with:
          slack_bot_token: ${{ secrets.SLACK_BOT_TOKEN }}
          slack_channel: ${{ secrets.SLACK_CHANNEL }}
          status: FAILED
```
