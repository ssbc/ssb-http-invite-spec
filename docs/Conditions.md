<!--
SPDX-FileCopyrightText: 2021 Andre 'Staltz' Medeiros

SPDX-License-Identifier: CC-BY-4.0
-->

# Conditions

This specification makes clear assumptions about the setup involved peers authenticating.

**Server:** an SSB peer, known as the "server", **MUST** have an internet-public host address, **MUST** be accessible for secret-handshake connections under a multiserver address, and **MUST** support HTTPS requests as well as it **MUST NOT** support plain HTTP.

**Client:** another SSB peer, known as the "client", **SHOULD** be able to open a secret-handshake and muxrpc connection with the server. The user controlling this SSB peer also **MUST** control a web browser used to make requests to the server. The client's browser and operating system **SHOULD** support hyperlinks to [SSB URIs](https://github.com/ssb-ngi-pointer/ssb-uri-spec), redirecting them to SSB applications that recognize and parse SSB URIs. The client's SSB application employed during SSB HTTP Authentication **MUST** be able to recognize and parse SSB URIs.
