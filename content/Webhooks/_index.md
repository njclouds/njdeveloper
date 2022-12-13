---
title: "Webhooks"
date: 2022-12-13T10:39:14+05:30
draft: false
weight: 30
---

A Webhook is a way to deliver events like open, click, bounce, etc. over the HTTP Protocol which helps to integrate with various applications.

## Webhook Events

| Events | Description |
---------|--------------
| MessageSent | An e-mail has been successfully delivered to its endpoint (either SMTP or HTTP). |
| MessageDelayed | An e-mail has been delayed due to an issue with the receiving endpoint. It will be retried automatically. |
| MessageDeliveryFailed | An e-mail cannot be delivered to its endpoint. This is a permanent failure so it will no be retried. |
| MessageHeld | An e-mail has been held in Postal. This will be because a limit has been reached or your server is in development mode. |
| MessageBounced | We received a bounce message in response to an email which had previously been successfully sent. |
| MessageLinkClicked | A link in one of your outbound messages has been clicked. |
| MessageLoaded | A message you have sent has been loaded. |
| DomainDNSError | This will be triggered when we detect an issue with the DNS configuration for any domain for this server. |

## Webhook Sample Response

### Sent

```json
{
  "event": "MessageSent",
  "timestamp": 1670907960.484763,
  "payload": {
    "message": {
      "id": 28,
      "token": "MWGhl8YadqgK",
      "direction": "outgoing",
      "message_id": "20221211224752.067922@hostname.com",
      "to": "to@example.com",
      "from": "from@fromdomain.com",
      "subject": "This is the test subject.",
      "timestamp": 1670779075.962122,
      "spam_status": "NotChecked",
      "tag": null
    },
    "status": "Sent",
    "details": "Message for to@example.com accepted by example.com (x.x.x.x)",
    "output": "250 OK : queued as gh8lPitJTJxlLpUdwuBZzXVHpMwQ\n",
    "sent_with_ssl": true,
    "timestamp": 1670907960.308573,
    "time": 0.83
  },
  "uuid": "31832909-22db-4b7d-8f09-93fd6853736b"
}
```

### Bounce

```json
{
  "event": "MessageDeliveryFailed",
  "timestamp": 1670911506.9640582,
  "payload": {
    "message": {
      "id": 29,
      "token": "mQ2SFRlihhdG",
      "direction": "outgoing",
      "message_id": "53f3957a-e072-427a-843c-f2444b81ee52@hostname.com",
      "to": "to@example.com",
      "from": "from@fromdomain.com",
      "subject": "This is the test subject.",
      "timestamp": 1670911462.998097,
      "spam_status": "NotChecked",
      "tag": null
    },
    "status": "HardFail",
    "details": "Permanent SMTP delivery error when sending to example.com (x.x.x.x)",
    "output": "550 \n",
    "sent_with_ssl": true,
    "timestamp": 1670911506.920094,
    "time": 20.55
  },
  "uuid": "7e44eb7d-f30b-403c-92ec-0bd2884a5efa"
}
```
