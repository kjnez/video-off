# Privacy

Block Video does not collect, store, transmit, sell, or share user data.

The extension has no analytics, no telemetry, no ads, no affiliate links, no background service worker, no content script, and no remote code. It uses Chrome's `declarativeNetRequest` API to block matching network requests locally in the browser.

The extension declares `host_permissions: ["<all_urls>"]` so the static blocking rules can apply to video requests across the web. This permission does not mean the extension reads page content, captures browsing history, or sends browsing activity anywhere.

