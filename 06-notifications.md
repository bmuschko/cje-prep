# Key CI/CD/Jenkins Concepts and their Usage

## Notifying the Team Upon a Broken Build

1. Change the list of Gradle tasks to `doesnotexist` to emulate a failure. The build will fail as the task doesn't exist in the build script.
2. Install the Google Chat plugin.
3. Create a new chat room in Google Chat named `jenkins-test` at [https://chat.google.com/](https://chat.google.com/).
4. For the chat room configure the webhook.
5. Configure the job to send a notification whenever the job fails. Use the webhook generated on Google Chat.
6. Execute the build. The build should fail and send a notification to the chat room.

<details><summary>Show Solution</summary>
<p>

Change the list of Gradle tasks first.

![Gradle Tasks](./images/06-notifications/change-gradle-tasks.png)

Find the plugin and install it.

![Google Chat Plugin](./images/06-notifications/google-chat-plugin.png)

Add a new chat room.

![Chat Room](./images/06-notifications/create-room.png)

For the chat room, click the little cog icon and create a new webhook.

![Add Webhook](./images/06-notifications/add-webhook.png)

Enter an appropriate name for the webhook.

![Webhook Naming](./images/06-notifications/webhook-naming.png)

Copy the generate webhook URL to the clipboard.

![Webhook URL](./images/06-notifications/webhook-url.png)

In the Jenkins job, create a new Google Chat notification. Add the webhook URL and provide a name.

![Notification Configuration](./images/06-notifications/notification-config.png)

Run a build. It should fail and send a new message to the chat room.

![Chat Room Message](./images/06-notifications/chat-room-message.png)

</p>
</details>