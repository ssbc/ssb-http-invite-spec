# Specification

1. Suppose an SSB user (known as "the client") has the SSB ID `userId` and has an SSB app supporting parsing SSB URIs
1. Suppose the server is hosted at domain `serverHost` and has generated an invite `inviteCode`
1. The invite link corresponding to `inviteCode` **SHOULD** be a URL in the format `https://${serverHost}/join?invite=${inviteCode}`
1. When the client visits that URL in a browser, the server **MUST** respond with HTML such that:
    1. If the `inviteCode` is already claimed or otherwise no longer valid, an error page **SHOULD** be rendered as response, and no further steps in this specification apply
    1. Otherwise, the `inviteCode` is *unclaimed*, and the following SSB URI **MUST** be rendered on the response page: `ssb:experimental?action=claim-http-invite&invite=${inviteCode}&postTo=${submissionUrl}` where `${submissionUrl}` is another URL on the server
1. The client's SSB app **SHOULD** parse the SSB URI and subsequently **SHOULD** send an HTTPS POST request to the endpoint `submissionUrl` with the header `Content-Type` equal `application/json` and the following body: `{"id":"${userId}","invite":"${inviteCode}"}`
1. The server receives the POST request and:
    1. If the `inviteCode` is already claimed, the response **SHOULD** be an error, and no further steps in this specification apply
    1. Otherwise, the `inviteCode` is now considered *claimed* for `userId`, which means:
        1. The server **SHOULD** store the client's `userId` and allow the client to access resources on the server, effectively making the client a recognized member
        1. The server **MUST** respond with header `Content-Type` equal `application/json` and body `{"multiserverAddress":"${serverMsAddr}"}` where `${serverMsAddr}` consititutes the server's multiserver address
1. The client receives the `submissionUrl` response, parses `${serverMsAddr}` from the response body, and **MAY** use that multiserver address to create a muxrpc connection with the server
1. If the server receives a muxrpc connection from the client, it **MUST** authorize it and grant them a [tunnel address](Tunnel%20addresses.md)
1. The client is now an Internal User

The JSON schemas for which the response from the `submissionUrl` **MUST** conform to is shown below.

**Successful responses**

```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "$id": "https://github.com/ssb-ngi-pointer/ssb-http-invite#claimed-json-endpoint-success",
  "type": "object",
  "properties": {
    "status": {
      "title": "Response status tag",
      "description": "Indicates the completion status of this response",
      "type": "string",
      "pattern": "^(successful)$"
    },
    "multiserverAddress": {
      "title": "Multiserver address of the server",
      "description": "Should conform to https://github.com/ssbc/multiserver-address",
      "type": "string"
    }
  },
  "required": [
    "status",
    "multiserverAddress"
  ]
}
```

**Failed responses**

```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "$id": "https://github.com/ssb-ngi-pointer/ssb-http-invite#claimed-json-endpoint-error",
  "type": "object",
  "properties": {
    "status": {
      "title": "Response status tag",
      "description": "Indicates the completion status of this response",
      "type": "string"
    },
    "error": {
      "title": "Response error",
      "description": "Describes the specific error that occurred",
      "type": "string"
    }
  },
  "required": [
    "status",
    "error"
  ]
}
```

## Programmatic invite façade

As an additional endpoint for programmatic purposes, if the query parameter `encoding=json` is added to the invite link (for illustration: `https://${serverHost}/join?invite=${inviteCode}&encoding=json`), then the server **SHOULD** return a JSON response. The JSON body **MUST** conform to the following schemas:

**Successful responses**

```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "$id": "https://github.com/ssb-ngi-pointer/ssb-http-invite#invite-json-endpoint-success",
  "type": "object",
  "properties": {
    "status": {
      "title": "Response status tag",
      "description": "Indicates the completion status of this response",
      "type": "string",
      "pattern": "^(successful)$"
    },
    "invite": {
      "title": "Invite code",
      "description": "Sequence of bytes that acts as a token to accept the invite",
      "type": "string"
    },
    "postTo": {
      "title": "Submission URL",
      "description": "URL where clients should submit POST requests with a JSON body",
      "type": "string"
    }
  },
  "required": [
    "status",
    "invite",
    "postTo"
  ]
}
```

**Failed responses**

```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "$id": "https://github.com/ssb-ngi-pointer/ssb-http-invite#invite-json-endpoint-error",
  "type": "object",
  "properties": {
    "status": {
      "title": "Response status tag",
      "description": "Indicates the completion status of this response",
      "type": "string"
    },
    "error": {
      "title": "Response error",
      "description": "Describes the specific error that occurred",
      "type": "string"
    }
  },
  "required": [
    "status",
    "error"
  ]
}
```
