# SSB HTTP Invites

**Revision:** `$REVISION`

**Author:** Andre Medeiros <contact@staltz.com>

**License:** This work is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).

## Abstract

As part of the process of onboarding to SSB, new users often need to connect to a "pub server" or "room server" where content can be retrieved from. These servers
often employ an access control system based on invite tokens, to prevent access to undesired actors from the public internet. The invite system deployed by these servers has been a convoluted algorithm repurposing secret-handshake to create an ephemeral muxrpc connection only for the initial remote procedure call to claim the invite token. In this document, we describe a simpler HTTP-based invite-token system for pubs and rooms that applies before any secret-handshake connection is built.

## Terminology

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in [RFC 2119](https://tools.ietf.org/html/rfc2119).

## Table of contents
