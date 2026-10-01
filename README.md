```
# Plugin Submissions

This repo is the intake point for submitting plugins to the **Dioxamine Plugin
Registry** — the catalog the [Dioxamine](https://github.com/rhythmcache/Dioxamine)
app fetches from to list installable plugins under Browse.

> This repo does not host plugin code itself. It's only for submission
> requests. Approved plugins are mirrored into their own repo under this
> organization.

Before submitting, read the official plugin documentation:
**[Plugin Overview & Architecture](https://rhythmcache.github.io/Dioxamine/book/plugins/overview.html)**

## How to submit a plugin

1. Make sure your plugin repo has, at its root:
   - `plugin.json` — your plugin manifest, following the
     [manifest specification](https://rhythmcache.github.io/Dioxamine/book/plugins/overview.html),
     with a valid `updateJson` field pointing to your `update.json`
   - `update.json` — version/download pointer, kept up to date on every release
   - An icon file (matching the `icon` field in `plugin.json`)
   - A GitHub Release containing your plugin's `.zip` build

2. Open a **[new submission issue](../../issues/new?template=submit-plugin.yml)**
   with your repo URL, plugin ID, and the required consent checkboxes filled in.

3. A maintainer reviews your `plugin.json`/`update.json`, checks the
   permissions declared are reasonable for what the plugin does, and checks
   the code for anything malicious.

4. If approved:
   - Your repo is cloned (full history) into a new repo under this org
   - You're invited as a **collaborator with write access** to the mirrored repo
   - You keep pushing updates directly to it going forward — nothing changes
     about how you develop
   - The registry index picks it up automatically within 24 hours (or sooner,
     on request)

## What we check before approving

- `plugin.json` is valid and matches the
  [manifest spec](https://rhythmcache.github.io/Dioxamine/book/plugins/overview.html)
- `plugin.json`'s `updateJson` field points to a reachable, valid `update.json`
- Declared `permissions` accurately reflect what the plugin actually does —
  no excessive or unused permission requests
- No malicious, obfuscated, or intentionally hidden code
- `update.json`'s `download` field resolves to a real `.zip` release asset
- The plugin ID/name doesn't already exist in the registry under a different repo

## plugin.json

See the [manifest specification](https://rhythmcache.github.io/Dioxamine/book/plugins/overview.html)
for the full schema and all supported fields (permissions, entry point,
fullscreen mode, button interception, etc).

Minimum required for registry inclusion:

{
  "schemaVersion": 1,
  "id": "io.github.username.yourplugin",
  "name": "Your Plugin Name",
  "description": "Short description of what it does",
  "version": "1.0.0",
  "versionCode": 1,
  "author": "your-username",
  "entry": "index.html",
  "icon": "icon.png",
  "minAppVersionCode": 1,
  "permissions": {},
  "homepage": "https://github.com/username/yourplugin",
  "updateJson": "https://raw.githubusercontent.com/<org>/<your-plugin-repo>/main/update.json"
}

## update.json

Kept at your repo root, updated on every release:

{
  "id": "io.github.username.yourplugin",
  "version": "1.0.1",
  "versionCode": 2,
  "download": "Download Link",
  "changelog": "Changelog Link"
}

- `versionCode` **must** increase with every release — the app compares this
  integer to decide if an update is available, not the `version` string.
- `changelog` is a URL to a plain text/markdown file, not inline text.
- Both `download` and `changelog` must be `http://` or `https://` URLs.

## After you're mirrored in

- You retain push access to your plugin's repo under this org — update
  `plugin.json`'s `version`/`versionCode` and `update.json` together on every
  release, and attach the new `.zip` to a GitHub Release.
- The registry index refreshes automatically every 24 hours, or on-demand
  when a maintainer triggers it.
- You keep authorship credit — the `author` field in your manifest and your
  commit history are untouched by the mirror.

## Questions

Open an issue here, or see the full [Dioxamine documentation](https://rhythmcache.github.io/Dioxamine/)
for plugin development guides, the JavaScript bridge API reference, and more.

## License

This registry and its submission process are provided under the same
[Apache-2.0](https://github.com/rhythmcache/Dioxamine/blob/main/LICENSE)
license as Dioxamine itself. Submitted plugins retain whatever license their
original author has chosen.
```
