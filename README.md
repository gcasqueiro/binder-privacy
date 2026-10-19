# Binder privacy policy

Last updated: 19 October 2026 (Binder 1.0.0)

Published at https://gcasqueiro.github.io/binder-privacy/

This document lists what data the Binder Chrome extension handles, where it is sent and where it is stored. Binder has no server of its own and no analytics.

## When Binder reads a page

Binder runs on a page only after you press the shortcut (Alt+S by default), click its toolbar button, or choose **Bind highlight** from the right-click menu. It then reads, from that tab only:

- the URL, title, meta tags (description, author, published date, site name, `og:image`) and JSON-LD;
- the readable text of the page (via Mozilla Readability);
- in Full reader view, the article structure (headings, paragraphs, lists, quotes, code, images and links);
- on X (x.com / twitter.com), the posts of the thread shown on the page, or the X Article shown on the page (its title, cover, author and text; in Summary mode the article text is used only to write the summary and is not saved);
- on YouTube (watch, Shorts and live pages), the video's title, channel, publish date, duration, thumbnail and description, and its transcript: the caption track is requested from youtube.com itself, from the YouTube tab (same origin, with the same access the page has), or, if that returns nothing, read from the page's own transcript panel. The transcript is used only to write the summary, and is saved only when you choose Full reader view;
- the text you selected, if any, which is saved as a highlight.

Nothing is read or sent until you confirm the save in the overlay (on YouTube, the video data and transcript are read when you confirm). When the overlay opens for a Notion database, Binder asks Notion whether that page's URL is already in the database, so it can show "Already bound" (and add a highlight to the earlier Bind instead of creating a new one).

## Bind this link (right-click menu)

When you choose **Bind this link** on a link, Binder downloads that one linked page and reads it the same way (title, meta tags, readable text, and in Full reader view the article structure). The page is fetched without your cookies, and its HTML is parsed inside the extension; scripts in it are never run. To fetch it, Binder needs access to that site: a small Binder window asks you, and the access is removed again right after the Bind. Links to X posts use the X endpoint described below and need no extra access. The result is shown on Binder's toolbar icon; Binder does not use notifications.

## Weekly digest (optional, off by default)

If you turn on the weekly digest in Options, Binder wakes up once a week at the day and time you pick (Chrome alarms) and:

- in Notion, lists the pages created in your Binds database (or under your Binds page) during the past 7 days — their titles, links, categories and types — and creates one "Weekly digest" page there;
- if you chose **A separate page** for digests, it also reads the TL;DR and highlights Binder wrote on those pages (and highlights added this week to older Binds), creates the week's page as a subpage of the page you picked (or of a "Binds Digests" page Binder creates there when you ask), and adds a link to it on that page;
- in Obsidian (vault folder), reads the frontmatter (title, type, saved date, category) of the notes in your chosen folder and also reads the TL;DR and highlights in those notes, and writes `Weekly digest YYYY-MM-DD.md` into your digest folder (`Digests` by default);
- if "AI overview" is on, sends only the titles and categories of that week's Binds to your AI provider to write a short summary of themes.

Nothing else is read, and nothing runs if the digest is off. "Generate now" in Options does the same once, on demand.

## Data sent to Notion (api.notion.com)

When the destination is Notion, Binder sends with your integration token:

- the page properties: title, URL, author, published date, save date, type, tags, category and your personal note, as far as your database has matching properties;
- the AI summary (TL;DR, key points, quotes, takeaways) as blocks;
- in Full reader view, the article content or the X thread;
- the cover image: Binder downloads the page's `og:image` and uploads it to Notion through Notion's file upload API;
- in Full reader view, the article's images: Binder downloads them from the site that hosts them (for example pbs.twimg.com for X) and uploads them to Notion; if a download is not allowed, the image is linked instead;
- for a YouTube video: the video link (shown as a video block), its thumbnail as the cover, and in Full reader view the transcript with links to each time;
- for every Bind, a small "View on …" link to the original page;
- a highlight (the selected text and a link back to it) appended to an earlier Bind of the same page, or placed on top of a new Bind;
- for the duplicate check: a query of your Binds database for the page's URL;
- for the weekly digest (if enabled): a query of that week's pages in your Binds database and one new "Weekly digest" page with links to them;
- during setup and in Options: searches for the pages and databases shared with the integration, reads their titles, parent pages and properties, and creates a database or page if you ask it to. This happens only while Options is open.

## Data sent to the AI provider

Binder sends one request per Bind to the provider you chose (none when a highlight is only added to an earlier Bind) (xAI, OpenAI, Anthropic, Google Gemini, OpenRouter or a custom OpenAI-compatible endpoint), using your API key. The request contains the page title, URL, author, site name, description, up to about 24,000 characters of the readable text (or the thread text, the X Article text, or a YouTube video's description and transcript), and the names of your existing Notion categories. The weekly digest, if enabled with its AI overview, sends one request per week with only the titles and categories of that week's Binds. The provider's own terms apply to that data. No AI request is made for the "Send a test Bind" button. The **Test key** button in Options sends one request to the provider's model list or key endpoint (for example `api.x.ai/v1/models`) with your key; if the key may not list models, it sends a one-token "ping" generation instead. No page content is sent.

## Data sent to X (cdn.syndication.twimg.com, pbs.twimg.com)

For X posts Binder asks X's public embed endpoint for the post and the posts it replies to (one request per post, at most 30), using the post id. The answer can include the X Article the post links to (its title, preview text and cover). No X account, cookie or API key is used. Images from X posts and the cover of an X Article are downloaded from pbs.twimg.com so they can be uploaded to Notion or saved in your vault.

## YouTube (youtube.com, i.ytimg.com)

When you save a YouTube video, Binder's script in that YouTube tab reads the video's details from the page and asks youtube.com, from the same tab, for the video page data and its caption track (the request goes from the YouTube page to YouTube itself, like the page's own requests; Binder adds no host permission for it). If no transcript comes back, Binder opens the page's own transcript panel, reads it and closes it again. Binder downloads the video's thumbnail from i.ytimg.com to use as the cover. The video id, title, channel, description and transcript are sent only to your AI provider (for the summary) and to your Notion workspace or vault (the video link, thumbnail and summary; the transcript only in Full reader view). No YouTube account data or API key is used or stored.

## Obsidian

When the destination is Obsidian, the note is written as a Markdown file into the folder you chose on your computer, or handed to the Obsidian app through an `obsidian://` link (with the clipboard for long notes). The note itself is not sent over the network for Obsidian (images saved into the vault are downloaded from the sites that host them, see Images).

## Images

For X posts, Binder draws a picture of the post on your computer from the public post data it already fetches, and uploads that picture to your Notion workspace. When you save to an Obsidian vault folder, Binder downloads the page's cover image and the images in the post or article from the sites that host them, and saves them in an `attachments` folder in your vault. Nothing is sent anywhere else.

## Stored on your device

- In the extension's IndexedDB: your Notion integration token and one AI API key per provider, and the handle of the Obsidian folder you chose.
- In `chrome.storage.local`: your settings (destination, chosen Notion database or page and its property mapping, provider, model, endpoint URL, Save mode, Obsidian folder and file name template, weekly digest on/off, day, time and AI overview) and the time the API key was last changed; for the weekly digest, the titles and links of the last 20 digests Binder created (so a week is never created twice); for the Obsidian app route, the file names Binder created and the URL each was saved from (last 500), so a highlight can be added to the same note.
- In `chrome.storage.session` (cleared when the browser closes): the list of Notion database names shown in the setup picker, so reopening Options is quick.

This data stays in your browser profile until you disconnect, change it or remove the extension. Binder does not sync it.

## What Binder does not do

Binder does not read pages you do not save, does not keep a history of browsing, and does not send data anywhere other than the services listed above. It has no analytics, no advertising and no server of its own. Data is not sold or transferred to third parties other than the Notion workspace and AI provider you configure, is not used for purposes unrelated to saving Binds, and is not used to determine creditworthiness or for lending.

## Limited Use

The use of information received from Chrome APIs adheres to the Chrome Web Store User Data Policy, including the Limited Use requirements.

## Trademarks

Notion, X, Obsidian, YouTube and the AI provider names are trademarks of their respective owners. Binder is an independent project and is not affiliated with or endorsed by them.

## Contact

Questions: email [contact@gcasqueiro.com](mailto:contact@gcasqueiro.com).
