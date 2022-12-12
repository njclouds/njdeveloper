---
title: "Send message"
date: 2022-12-12T17:46:26+05:30
draft: false
---

This endpoint is solely responsible for sending emails over Ninjaemail's API.

## Request

### Endpoint

`POST <endpoint>/api/v1/send/message`

### Authentication

#### Headers


| Fields | Value |
|--------------|----------------|
| X-Auth-Token | <secret_token> |


### Request Body


| Parameters | Type | Details |
|------------|-------|--------|
| to | Array | The e-mail addresses of the recipients (max 50) |
| cc | Array | The e-mail addresses of the CC contacts (max 50) |
| bcc | Array | The e-mail addresses of the BCC contacts (max 50) |
| from | String | The e-mail address for the From header |
| subject | String | The subject of the email |
| tag | String | The tag of the email |
| html_body | String | The HTML body of the e-mail |
| attachments | Array | You need to provide [Array of Objects](#attachments-object) with more details. |
| headers | Hash | A hash of additional headers |

#### Attachments Object

| Parameters | Type | Details |
|------------|-------|--------|
| name | String | Filename  |
| content_type | String | File mime type like `text/csv`, `image/jpeg` etc  |
| data | String | Base64 encoded file content  |


### Sample curl call

```sh
curl -i -X POST \
   -H "Content-Type:application/json" \
   -H "X-Server-API-Key:secret_token" \
   -d \
'{
  "from":"from@domain.com",
  "to":[
      "dre_to_1@example.com",
      "dre_to_2@example.com"
  ],
  "cc":[
       "dre_cc1@example.com",
       "dre_cc2@example.com"
   ],
  "bcc":[
       "dre_bcc@example.com"
   ],
  "subject":"Testing from API",
  "plain_body":"This is plain body",
  "html_body":"<b>This is plain body</b>",
  "tag":"campaign_1",
  "headers":{
    "header1":"test_header_1",
    "header2":"test_header_2"
  },
  "attachments":[
    {
      "name":"test.csv",
      "content_type":"text/csv",
      "data":"cmVjb3JkMUBleGFtcGxlLmNvbQ0KcmVjb3JkMkBleGFtcGxlLmNvbQ0K"
    }
  ]
}' \
 'https://api.endpoint.com/api/v1/send/message'
```

## Response

### Headers

`200 OK`

### Body

#### Success

```json
{
    "status": "success",
    "time": 0.25,
    "flags": {},
    "data": {
        "message_id": "bdaf4be2-c29a-4c57-8be9-21d3546430c6@rp.postal.ninjaemail.cloud",
        "messages": {
            "dre_to_1@example.com": {
                "id": 400147,
                "token": "B8jbY7GcteCf"
            },
            "dre_to_2@example.com": {
                "id": 400148,
                "token": "RfPQWWl074OR"
            },
            "dre_cc1@example.com": {
                "id": 400149,
                "token": "ji1rpo3Ataub"
            },
            "dre_cc2@example.com": {
                "id": 400150,
                "token": "vhUjIUTfdwkt"
            },
            "dre_cc3@example.com": {
                "id": 400151,
                "token": "exSEBMlJaOcK"
            }
        }
    }
}
```

#### Error

```json
{
    "status": "error",
    "data": {
        "code": "InvalidServerAPIKey",
        "message": "The API token provided in X-Server-API-Key was not valid.",
        "token": "vYjATVF1jh3AxkaqmXFAggfDd"
    }
}
```
