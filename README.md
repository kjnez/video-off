# Video Off

Video Off is a small Manifest V3 Chrome extension that blocks common online video playback requests.

It uses Chrome's `declarativeNetRequest` API with a static ruleset. There is no background service worker, no content script, no analytics, and no remote code.

## Repository Layout

- `extension/`: the Chrome extension package. Load this folder in Chrome.
- `extension/manifest.json`: extension metadata, permissions, icons, and ruleset registration.
- `extension/rules.json`: static `declarativeNetRequest` blocking rules.
- `extension/icons/`: packaged extension icons.
- `assets/`: source assets that are useful for the repository but not required in the unpacked extension.

## What it blocks

The current rules block common video delivery URLs and media patterns, including:

- `googlevideo.com` requests
- HLS manifests ending in `.m3u8`
- DASH manifests ending in `.mpd`
- media files ending in `.mp4`
- media files ending in `.webm`

The goal is to reduce or stop common web video playback while keeping the implementation easy to inspect.

## Limitations

This is not a universal video blocker. Some sites may use delivery patterns that are not covered by the current static rules, and future site changes can require new rules.

The extension currently uses `host_permissions: ["<all_urls>"]` because declarative network request rules need to match video requests across the sites where you browse. The extension does not read page contents or collect browsing data.

## Privacy

Video Off does not collect, store, transmit, sell, or share user data.

All blocking happens locally in Chrome through the extension's static `declarativeNetRequest` ruleset. See [PRIVACY.md](PRIVACY.md) for the full privacy note.

## Install Locally

1. Open `chrome://extensions`.
2. Enable **Developer mode**.
3. Click **Load unpacked**.
4. Select the `extension/` folder in this repository.
5. Visit a page with embedded or streaming video and confirm playback is blocked.

If Chrome reports a manifest or ruleset error, open the extension details page and check the error output.

## Development

Validate the extension JSON after editing:

```sh
python3 -m json.tool extension/manifest.json >/dev/null
python3 -m json.tool extension/rules.json >/dev/null
```

When adding blocking coverage, keep rule IDs unique and prefer focused, explainable `urlFilter` patterns. Avoid adding broad site-specific rules unless they materially improve blocking and are easy to justify.

## Contributing

Rule contributions are welcome when they are narrow, readable, and improve real video blocking behavior. Please include the site or media pattern that motivated the change and note any expected tradeoffs.

## License

MIT. See [LICENSE](LICENSE).
