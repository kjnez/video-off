# Contributing

Thanks for considering a contribution.

This project is intentionally small. Changes should keep the extension narrow, transparent, privacy-preserving, and easy to audit.

## Rule Changes

When changing `extension/rules.json`:

- Keep rule IDs unique and stable.
- Use focused `urlFilter` patterns.
- Prefer generic media delivery patterns over site-specific rules.
- Add site-specific rules only when they materially improve blocking and are easy to explain.
- Do not add tracking, analytics, ads, affiliate links, telemetry, or remote code.

After editing JSON, run:

```sh
python3 -m json.tool extension/manifest.json >/dev/null
python3 -m json.tool extension/rules.json >/dev/null
```

## Testing

Manual testing is currently the main validation path:

1. Open `chrome://extensions`.
2. Enable **Developer mode**.
3. Click **Load unpacked** and select the repository's `extension/` folder.
4. Visit representative pages with embedded or streaming video.
5. Confirm video playback is blocked while ordinary navigation still works.
6. Check the extension details page for manifest, ruleset, or permission errors.
