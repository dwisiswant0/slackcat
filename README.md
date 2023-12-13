# slackcat

A simple way of sending messages from the CLI output to your Slack with webhook.

> See [discat](https://github.com/dwisiswant0/discat) for Discord version.

## Installation

- Download a prebuilt binary from [releases page](https://github.com/dwisiswant0/slackcat/releases/latest), unpack and run! or
- If you have go1.13+ compiler installed: `go get github.com/dwisiswant0/slackcat`
  - for go1.18+: `go install github.com/dwisiswant0/slackcat@latest`

## Configuration

**Step 1:** Get yours Slack incoming webhook URL [here](https://slack.com/intl/en-id/help/articles/115005265063-Incoming-webhooks-for-Slack).

**Step 2** _(optional)_**:** Set `SLACK_WEBHOOK_URL` environment variable.
```bash
export SLACK_WEBHOOK_URL="https://hooks.slack.com/services/xxx/xxx/xxx"
```

## Usage

It's very simple!

```bash
▶ echo -e "Hello,\nworld!" | slackcat
```

### Flags

```
Usage of slackcat:
  -1    Send message line-by-line
  -u string
        Slack Webhook URL
  -v    Verbose mode
```

### Workaround

The goal is to get automated alerts for interesting stuff!

```bash
▶ assetfinder dw1.io | anew | slackcat -u https://hooks.slack.com/services/xxx/xxx/xxx
```

The `-u` flag is optional if you've defined `SLACK_WEBHOOK_URL` environment variable.

Slackcat also strips the ANSI colors from stdin to send messages, so you'll receive a clean message on your Slack!

```bash
▶ nuclei -l urls.txt -t cves/ | slackcat
```

![Proof](https://user-images.githubusercontent.com/25837540/90967983-4d29a100-e511-11ea-9138-28b6901856dc.png)

### Line-by-line

Instead of have to wait for previously executed program to finish, use the `-1` flag if you want to send messages on a line by line _(default: false)_.

```bash
▶ amass track -d domain.tld | slackcat -1
```

## Thanks

- Inspired by [rez0](https://twitter.com/rez0__) [article](https://rez0.blog/hacking/2020/02/07/bugbounty-alert-automation-tips.html), that's why this tool was made!
- [acarl005](https://github.com/acarl005) for his awesome stripansi.
