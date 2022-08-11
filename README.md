## Snippet Slack API in Gitlab CI/CD

This is a small snippet explaining how to create a Slack bot that can be integrated in the Gitlab CI/CD.  
This will send a customized message in a selected channel in a toolchain.


## Creating a Slack Bot and generate token

- Go to https://api.slack.com/

- Click 'Your apps' at the top-right > Create New App > From Scratch

- Choose an App name and select your workspace > Create app

- In 'Add features and functionality', select Bots > Review Scopes to add

- In Scopes section, click 'Add an OAuth Scope' and select 'chat:write'

- Scroll back up and click 'Install to Workspace' > click 'Allow'

- Copy your newly created 'Bot User OAuth Token' starting by 'xoxb-' and paste it in SLACK_AUTH_TOKEN variable

- Update SLACK_CHANNEL variable (On Slack, select the channel on the left panel, click on the channel's name in the middle panel, scroll down, copy the channel ID on the bottom)


## Testing the API call to send a message

- You can test that everything is good until now here: https://api.slack.com/methods/chat.postMessage/test

- In the Arguments section, paste the Bot Token in 'Token', the 'Channel' you want the bot to send messages to, and a message in 'Text'

- Click the 'Test the method' for the bot to send a message to the selected channel

- If you got 'not_in_channel' error when testing, it means you need to integrate your application to the channel.  
To do that, go to Slack, select the channel, click on the icon with the number of members in the channel at the top-right, select Integrations > Applications > click 'Add an application' > click 'Add' next to your newly added application

## Integrate in your .gitlab-ci.yaml

Add the slack_message step in one of your stage by extending it
For example, you can add this after deploying a new webapp, it will notify the channel of the update.

Example in the stage release in the yaml:
```bash
release:
  extends:
    - .slack_message
```

## Warning

For the free version of a Slack workspace, only 10 applications can be added
