<!--
SPDX-FileCopyrightText: 2021 Andre 'Staltz' Medeiros

SPDX-License-Identifier: CC-BY-4.0
-->

# Security considerations

## Malicious web visitor

A web visitor, either human or bot, could attempt brute force visiting all possible invite URLs, in order to force themselves to become an [internal user](../Stakeholders/Internal%20user.md). However, this could easily be mitigated by rate limiting requests by the same IP address.