
# Webhooks 🕷🥞🕸⚓

Use incoming webhooks to get real-time updates
Listen for events on your NFT order / job so your integration can automatically trigger reactions .

Completed | Progress | Failed | Unrecoverable Fatal Error

- <b>🔸 completed</b>
  This is triggered when the NFT is successfully minted.

- <b>🔸 progress</b>
  This is triggered when job update the status of the order/job

- <b>🔸 failed</b>
  This is triggered when a task fails. Please keep in mind that the job is retrying 10 times until the order's status is declared as unrecoverable. Fatal Error

- <b>🔸 unrecoverableFatalError</b>
This is triggered when a job fails many times and will not be retried; the job is then removed from the queue stack.


## Implementing a Webhook

This events are triggered by the job queue when a job is completed, failed or in progress...
POST a webhook to your slack channel to get notified when a job is completed, failed or in progress.

We send a payload using POST, 3 times if response is not 2xx ->> OK
This will change in futures updates and Auth system will be add it.
```

