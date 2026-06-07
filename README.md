# Agent Island — distribution

Public distribution channel for **Agent Island**, the native macOS companion for
AI coding agents — https://island.dimsky.cn

This repo carries only what end users' machines need to receive updates:

- **`appcast.xml`** — the Sparkle update feed.
- **Release assets** — signed `AgentIsland.dmg` / `AgentIsland.zip` per version,
  attached to this repo's GitHub Releases.

The application source lives in a separate repository; its CI builds, signs,
notarizes, and publishes here.

Update feed: <https://raw.githubusercontent.com/dimsky/agent-island-dist/main/appcast.xml>
