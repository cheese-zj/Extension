# Chrome Web Store Submission Notes

## Store Description (copy/paste)

ChatGPT Branch Tree turns your ChatGPT conversations into an interactive, navigable tree so you never lose track of branches. It:

- Automatically tracks “Branch in new chat” events and shows parent/child threads as a clear tree, including nested branches.
- Lets you click any node to scroll to the exact message or open the branched conversation in a new tab.
- Shows message previews and full-text tooltips on hover; branch nodes use distinct colors and labels so you can see where you’re viewing.
- Auto-refreshes as you chat and keeps a floating toggle to open/close the panel without leaving the page.
- Offers light/dark/system themes, compact mode, timestamp format, and preview length controls; you can clear all stored data anytime.

Privacy-first: all branch metadata and settings stay in `chrome.storage` on your device; no external servers or tracking. Only needs access to ChatGPT domains plus basic `tabs`/`scripting`/`storage` to fetch conversation data and render the panel.

## Permission Justifications

- **tabs**: Needed to detect the active ChatGPT tab, open/focus specific conversations when you click a branch, and send messages to the correct tab for scrolling to messages.
- **storage**: Needed to save branch metadata, titles, settings (theme/compact/timestamps), and cache flags locally so the tree persists between sessions. Data never leaves the device.
- **scripting**: Used to inject the content script into the ChatGPT tab (when the action button is clicked) so the panel can toggle and send/receive tree updates.
- **Host permissions (`https://chatgpt.com/*`, `https://chat.openai.com/*`)**: Required to read the current conversation, track “Branch in new chat”, and render the tree UI on ChatGPT pages. No other hosts are accessed.

## Remote Code

- **Are you using remote code?** No. All JavaScript/HTML/CSS is packaged with the extension; there are no remote scripts, evals, or external module URLs.
