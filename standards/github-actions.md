## Reporting results to Slack

We use the [action-slack-notify](https://github.com/rtCamp/action-slack-notify) Github Action to post the results of GitHub actions to Slack. Here's an example configuration from the [circulation-patron-web](https://github.com/NYPL-Simplified/circulation-patron-web/) project, which posts a link to a report from an integration test suite:

```
      - name: Slack Notification
        uses: rtCamp/action-slack-notify@v2
        env: 
          SLACK_CHANNEL: test_reports
          SLACK_MESSAGE: ${{ steps.cypress.outputs.dashboardUrl }}
          SLACK_TITLE: Circulation Patron Web End-to-End Cypress Test Results
          SLACK_WEBHOOK: ${{ secrets.SLACK_WEBHOOK }}
          SLACK_USERNAME: nyplorgBot
```

In this case, the `SLACK_WEBHOOK` secret is set to the [test report WebHook URL](ci.md).

