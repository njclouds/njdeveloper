---
title: "Swaks"
date: 2022-12-12T15:07:33+05:30
draft: false
---


Swaks (Swiss Army Knife SMTP) is a command-line tool written in Perl for testing SMTP setups; it supports STARTTLS and SMTP AUTH (PLAIN, LOGIN, CRAM-MD5, SPA, and DIGEST-MD5). 

## example

```sh
swaks --server smtp.endpoint.com:2525 \
      --auth-user smtpuser \
      --auth-password smtppass \
      --to to@example.com \
      --from from@exmple.com \
      --header "Subject: SMTP from swaks" \
      --add-header "Content-Type: text/html" \
      --body 'This is a test body. <a href="https://google.com">go to google</a>'
```

