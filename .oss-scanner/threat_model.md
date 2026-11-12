# Threat model

## What this project does and where untrusted input enters
A monitoring/dashboard platform (Go backend + TypeScript frontend). Untrusted input: query
requests from data sources, plugin/panel data, uploaded images/dashboards, and the HTTP API.
Backend deserialization of dashboard JSON and the plugin sandbox are key surfaces.

## Components that matter most / least
- most: the HTTP API/dashboard JSON handling and the plugin execution/sandboxing.
- less: the frontend bundle, docs.

## How to exercise it
Load crafted dashboard JSON; exercise the API with malformed queries; test plugin boundaries.

## How you rate severity
- RCE (e.g., via a plugin or expression) or auth bypass: critical.
- Sandbox escape from a plugin: high. Stored XSS: medium-high. DoS: medium.

## Anything to leave alone
- The built frontend bundle is a build artifact; focus on the Go backend.
