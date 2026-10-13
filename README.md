# Binder privacy policy

Last updated: 14 October 2026

This document lists what data the Binder Chrome extension handles, where it is sent and where it is stored. Binder has no server of its own and no analytics.

## When Binder reads a page

Binder runs on a page only after you press the shortcut (Alt+S by default) or click its toolbar button. It then reads, from that tab only:

- the URL, title, meta tags (description, author, published date, site name, `og:image`) and JSON-LD;
- the readable text of the page (via Mozilla Readability);
- in Full reader view, the article structure (headings, paragraphs, lists, quotes, code, images and links);
- on X (x.com / twitter.com), the posts of the thread shown on the page.

Nothing is read or sent until you confirm the save in the overlay.

## Data sent to Notion (api.notion.com)

When the destination is Notion, Binder sends with your integration token:

- the page properties: title, URL, author, published date, save date, type, tags, category and your personal note, as far as your database has matching properties;
- the AI summary (TL;DR, key points, quotes, takeaways) as blocks;
- in Full reader view, the article content or the X thread;
- the cover image: Binder downloads the page's `og:image` and uploads it to Notion through Notion's file upload API;
- in Full reader view, the article's images: Binder downloads them from the site that hosts them (for example pbs.twimg.com for X) and uploads them to Notion; if a download is not allowed, the image is linked instead;
- during setup and in Options: searches for the pages and databases shared with the integration, reads their titles, parent pages and properties, and creates a database or page if you ask it to. This happens only while Options is open.

## Data sent to the AI provider

Binder sends one request per Bind to the provider you chose (xAI, OpenAI, Anthropic, Google Gemini, OpenRouter or a custom OpenAI-compatible endpoint), using your API key. The request contains the page title, URL, author, site name, description, up to about 24,000 characters of the readable text (or the thread text), and the names of your existing Notion categories. The provider's own terms apply to that data. No AI request is made for the "Send a test Bind" button. The **Test key** button in Options sends one request to the provider's model list or key endpoint (for example `api.x.ai/v1/models`) with your key; if the key may not list models, it sends a one-token "ping" generation instead. No page content is sent.

## Data sent to X (cdn.syndication.twimg.com, pbs.twimg.com)

For X posts Binder asks X's public embed endpoint for the post and the posts it replies to (one request per post, at most 30), using the post id. No X account, cookie or API key is used. Images from X posts are downloaded from pbs.twimg.com so they can be uploaded to Notion.

## Obsidian

When the destination is Obsidian, the note is written as a Markdown file into the folder you chose on your computer, or handed to the Obsidian app through an `obsidian://` link (with the clipboard for long notes). Nothing is sent over the network for Obsidian.

## Stored on your device

- In the extension's IndexedDB: your Notion integration token and one AI API key per provider, and the handle of the Obsidian folder you chose.
- In `chrome.storage.local`: your settings (destination, chosen Notion database or page and its property mapping, provider, model, endpoint URL, Save mode, Obsidian folder and file name template) and the time the API key was last changed.
- In `chrome.storage.session` (cleared when the browser closes): the list of Notion database names shown in the setup picker, so reopening Options is quick.

This data stays in your browser profile until you disconnect, change it or remove the extension. Binder does not sync it.

## What Binder does not do

Binder does not read pages you do not save, does not keep a history of Binds, and does not send data anywhere other than the services listed above. It has no analytics, no advertising and no server of its own. Data is not sold or transferred to third parties other than the Notion workspace and AI provider you configure, is not used for purposes unrelated to saving Binds, and is not used to determine creditworthiness or for lending.

## Limited Use

The use of information received from Chrome APIs adheres to the Chrome Web Store User Data Policy, including the Limited Use requirements.

## Trademarks

Notion, X, Obsidian and the AI provider names are trademarks of their respective owners. Binder is an independent project and is not affiliated with or endorsed by them.

## Contact

Questions: email [contact@gcasqueiro.com](mailto:contact@gcasqueiro.com).
