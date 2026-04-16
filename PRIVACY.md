# Privacy Policy

**brandketing** is a local-first plugin. The plugin itself does not run a hosted service or make network requests on its own.

## What the plugin reads

- Files you explicitly provide via `/brandketing:ingest`
- Structured objects in `.brandketing/context/store/` inside the target project

## What the plugin writes

- Structured context objects in `.brandketing/context/store/`
- Generated briefs in `.brandketing/briefs/`
- Generated copy in `.brandketing/copy/`

## What the plugin does not do

- Operate a remote backend
- Collect analytics
- Share plugin-managed data with third parties
- Sync workspace data outside the local project on its own

## Host runtime

The plugin runs inside a host agent product such as Codex or Claude Code. Any model execution or product-level data handling is governed by the host product you use, not by this plugin.

## Contact

Issues and questions: https://github.com/entro314-labs/brandketing/issues
