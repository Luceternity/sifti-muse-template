Sifti — Portable Build Template v0.4.3

> **Recipient installation instruction:** Build a new Sifti application from this specification inside my Muse environment. Use only my account, my Muse Feed, my sources, my schedules, my generated content, and destinations that I explicitly connect. Do not import, infer, or reuse another user’s data. Ask for my approval before connecting external services or publishing audio.

────────

1. Instructions for the Recipient’s Muse

You are building Sifti, a personal audio-first content digest application, from this specification inside the recipient’s own Muse environment.

Hard rules for this build:

1. Read this entire file before writing any code.
2. Create a new, empty Sifti application named “Sifti.” Do not copy any existing installation.
3. The application must be scoped only to the recipient’s own Muse account: their Muse Feed, their sources, their summaries, their audio, their transcripts, their schedules, their podcast destination, and their links.
4. Start with zero external sources. Do not seed any source, channel, creator, URL, or example content from any other installation.
5. Create the built-in “Muse Daily” section bound only to the recipient’s own Muse Feed content. If their Muse Feed cannot be detected automatically, ask them to confirm or select it. Never substitute another user’s feed.
6. Never hardcode a podcast feed URL from this template (this template contains none). If the recipient asks for a podcast feed and approves, create a fresh one for them following §16.1 and store its URL as a per-installation setting.
7. Ask the recipient for approval before connecting any external service or publishing any audio.
8. All stored data, generated links, schedules, and identifiers must be unique to this installation. Nothing may be shared with any other installation.

────────

2. Product Overview

Sifti is a personal listening companion: a mobile-first web application that collects content the user follows (a built-in Muse Daily digest plus user-added external sources such as video channels, creators, newsletters, or podcasts), turns each edition into a concise summary with an English narrated audio version and transcripts, and presents everything as a listening queue.

Core loop:

1. User adds sources they follow (or relies on the built-in Muse Daily).
2. On each source’s schedule, a new edition (digest) is generated: summary text, English audio narration, English transcript, optional secondary-language transcript.
3. Editions appear in the listening queue on the home screen, newest first, with unread indicators.
4. The user plays audio in the edition view; progress is saved and resumable.
5. Editions are marked finished automatically when playback ends, or manually.

Product character: an editorial magazine crossed with driving mode — warm, calm, premium, and minimal. The interface is quiet; gold is used sparingly as a precise status signal (new/unread/continue), never as decoration.

────────

3. Product Principles

1. Account isolation is the foundation. Every installation belongs to exactly one person. No data, link, schedule, or identifier is ever shared between installations.
2. Empty before full. A new installation starts empty. The user earns every source, edition, and setting by adding it themselves.
3. Audio first. The listening queue is the home screen. Text is the companion, not the destination.
4. One language on screen. The interface shows exactly one language at a time (English or Simplified Chinese). A second language appears only inside the transcript area of an edition.
5. Future-only settings. Changing voice, transcript language, frequency, or schedule affects future editions only. Existing editions are never rewritten.
6. Clearly AI-generated. Every summary is labeled as AI-generated, and the interface recommends the original source when it matters.
7. Permission before publishing. Nothing is published to any podcast destination without the recipient’s explicit connection and approval.

────────

4. Non-Negotiable Privacy and Account-Isolation Rules

These rules override everything else in this document. If any instruction below appears to conflict with them, these win.

1. This template contains zero personal data. It ships with no source names, no creator selections, no channel URLs, no feed URLs, no summaries, no transcripts, no audio, no podcast destinations, no listening history, no dates, no account identifiers, and no credentials.
2. A fresh installation must create its own records for everything: sources, editions, transcripts, audio blobs, schedules, settings, podcast links.
3. Never reuse a URL, feed, schedule, source configuration, or identifier from any other Sifti installation.
4. The built-in Muse Daily source must be bound to the recipient’s own Muse Feed. Never copy another user’s Muse Daily editions.
5. Generated audio must be stored in the recipient’s own storage and served only to them.
6. Publishing audio to a podcast destination requires the recipient’s own connection and their explicit approval, per edition or per standing permission they grant.
7. No credentials, tokens, cookies, API keys, or authentication material may be stored in the template or carried between installations.
8. Two installations built from this template must be completely unable to see or access each other’s information.

────────

5. First-Run Experience

1. The application opens on the home screen showing:
  • The “You’re all caught up” empty state (see §19).
  • The built-in Muse Daily card in an awaiting-first-edition state (“Your latest edition will appear here”).
  • The Sources section showing “No external sources have been added” with a prominent Add Source action.
2. If the recipient’s Muse Feed can be detected, bind the built-in Muse Daily source to it silently. If it cannot, show a setup prompt asking them to confirm or select their own Muse Feed. Never proceed with another user’s feed.
3. Do not generate any edition until (a) the Muse Daily feed is bound, or (b) the user adds their first external source and its first scheduled window completes.
4. The podcast section in Settings shows a disconnected state: no feed URL exists yet. It must explain that a destination is created only when the user connects one, and publishing requires their approval.

────────

6. Information Architecture

Sifti is a single-page application with internal view state (no URL router). Four views:

Home (listening queue)
├── Source detail (per source)
│   └── Edition detail (per edition)
└── Settings

• Home → tap a source row → Source detail → tap an edition → Edition detail. Back buttons return up the hierarchy.
• Home → gear icon → Settings. Back returns to Home.
• Scroll position resets to top on every view change.
• Any in-progress speech/audio playback is stopped when navigating between views.

────────

7. Screen-by-Screen UI Specification

7.1 Home screen (listening queue)

• Header: small kicker text “LISTENING QUEUE”, large H1 showing the unread queue count (e.g., “3 to listen”), settings gear icon at top-right.
  • When the queue is empty, the H1 reads “You’re all caught up”.
• Hero card (latest unread edition): dark charcoal rounded card with:
  • A pulsing gold dot (new/unread signal).
  • “Continue listening” label.
  • Source name + localized period label.
  • Large edition title.
  • Play call-to-action that opens the edition detail and starts audio.
  • When nothing is unread: an “All clear” empty variant.
• Muse Daily card: gold-accented card with an “M” mark, “Latest edition” label, and an unread pulse badge when the latest Muse Daily edition is unread. Tapping opens the latest Muse Daily edition.
• Sources section: header row with an Add button. Each source row shows:
  • Monogram tile (platform initials, e.g., “YT”).
  • Source name.
  • Gold unread-count badge (hidden when zero).
  • Frequency label + latest period label.
  • Chevron.
  • Tapping opens the source-detail screen.
  • When zero sources: empty-state call-to-action (“No external sources have been added” + Add Source button).
• Footnote: one quiet line at the bottom (e.g., app tagline or version note).

7.2 Source-detail screen

• Back button to Home.
• Platform kicker (uppercase, e.g., “YOUTUBE”).
• Large source title.
• Meta row: frequency label (“Updates daily” / “Updates twice a week” / etc.), edition count, gold “unfinished” count.
• Vertical timeline of editions, newest first:
  • Gold rail dot for unread editions.
  • Edition title, 2-line clamped preview, duration label (e.g., “Reading time ~6 min”).
  • Tapping opens the edition detail.
• Empty state when the source has no editions yet: “Your first digest is on the way.”
• Settings button (hidden for the built-in Muse Daily source) opens the source-settings modal: frequency list + delete-source button.

7.3 Edition-detail screen

• Back button (returns to the source) + read-state pill: gold “unfinished” or neutral “finished”.
• Kicker: period label + duration label.
• Large edition title.
• Original source title line (when available).
• Audio section: native audio player labeled “Narrated by {narrator_name}”; “listening position is saved” note; load-failure state with retry; missing-audio state distinguishing “still preparing” (auto-retries) from “unavailable”.
• “Mark as finished” button. Playback ending inside Sifti auto-marks the edition finished and clears saved progress; manual marking does the same. Explain that listeners who finish an edition in an external podcast app should return here and mark it finished because external playback-completion state may not sync back to Sifti.
• Transcript section: language tabs — English (default, always present), secondary language (only if generated for this edition). If a tab’s transcript is missing, the tab is not rendered.
• Feed-items list (Muse Daily editions): each item shows kicker · category / title / summary.
• Recommendation block: gold-bordered callout (when present).
• “Open original” external link to the source material.
• “Also worth a look” extra links list (when present).
• Q&A block (placeholder): a textarea plus a button to copy the question into chat. API-backed answering is reserved for a future version; any API-key field is disabled.

7.4 Settings screen

Five sections:

1. Interface language — segmented picker: English / Simplified Chinese. Changes UI copy only; never changes audio or transcripts.
2. Transcript languages — English fixed row; secondary-language selector (Simplified Chinese / Spanish / French). Note: “Applies to future editions only.”
3. Schedule — one row per source: frequency select (Daily / Twice a week · Wed & Sun / Weekly · Saturday / Monthly · 1st), digest-time input (recipient’s local time, DST-aware). Dirty-aware Save button. Delete-source button (hidden for the built-in Muse Daily source). Note: changes affect future editions; scheduling is reconciled daily.
4. Narrator and voice — use the recipient’s own Muse agent name when it is available; otherwise ask the recipient to choose a narrator display name. Provide 4 voice options (e.g., warm / smooth / vanessa / ronan, with gender labels). Name and voice changes apply to future English audio only.
5. Podcast feed — connection state panel:
  • Disconnected: explains the feed is link-only/unlisted (invisible to search, accessible to anyone with the link). Includes a clear action (e.g., “Create my podcast feed”). Before the action, disclose that some providers require a short “Welcome to Sifti” trailer to initialize the RSS feed and that tapping the button authorizes this trailer when required. Tapping this button IS the recipient’s explicit request and approval — no separate chat request is needed — and it triggers the feed-creation flow in §16.1.
  • Unsupported: show this state only after the recipient’s Muse has explicitly checked for native podcast-provisioning capability and found none. Explain that this Muse environment cannot provision or publish a feed by itself. Offer Connect a podcast host only when a supported provider authorization/API integration is available; otherwise offer Continue with in-app listening only. Do not ask the recipient to paste a bare RSS URL as though it were a writable publishing destination.
  • Connected: shows the recipient’s own RSS URL in a copy panel with copied/failed feedback and two clear actions:
    1. Copy RSS link — copies the recipient-specific RSS URL for use in any compatible podcast client.
    2. Copy for Apple Podcasts — copies the same RSS URL, then displays platform-specific instructions: on iPhone/iPad, open Apple Podcasts → Library → More (…) → Follow/Add a Show by URL → paste → Follow; on Mac, choose File → Follow a Show by URL → paste → Follow.
  • Make clear that these actions do not create two different feeds. Apple Podcasts accepts the RSS URL itself; Sifti does not generate or promise a public podcasts.apple.com catalog page. Do not promise universal client compatibility. State that new published episodes can appear through the client’s normal feed updates while playback completion may not sync back to Sifti.

7.5 Add Source flow (modal)

Fields:

• Source name (free text, e.g., “Example Creator”).
• Platform select: YouTube / Xiaohongshu / Podcast / Newsletter / Other.
• Public source URL or channel identifier (placeholder: https://example.com/source). Never accept or store another installation’s private feed URL.
• Frequency segmented control (default: Daily).
• Content types chips: video / image / text / audio (default: video).
• Digest time defaults to 08:00 recipient-local at creation; editable later in Settings.

On submit: create the source record. Re-adding the same identifier reactivates the existing record instead of duplicating it.

7.6 Delete source (two-step confirm)

• Available for external sources only; the built-in Muse Daily source cannot be deleted (blocked in both client and server).
• Confirm dialog warns that all of the source’s editions and listening progress will be permanently removed.
• Deletion cascades to the source’s editions and saved progress.

────────

8. Visual Design System

Preserve this direction as closely as possible.

• Themes: adaptive via prefers-color-scheme.
  • Light “paper” theme: background #f7f5ef, surface #fffdfa, ink #171714.
  • Dark editorial theme: background #171714, surface #22221e, ivory text #f3efe5.
• Accents:
  • Warm gold #b88917 (light) / #d4aa3c (dark) — status signal only: pulse dots, unread badges, “new” labels. Gold-soft tinted backgrounds for emphasis blocks.
  • Red #b6452c — destructive actions and platform kickers.
  • Deep green #425049 — primary action surfaces.
• Typography: system body stack with CJK support (PingFang SC, Noto Sans CJK SC, system-ui fallback). Georgia serif for dates, period labels, and numbers — the editorial signature. Large editorial headings throughout.
• Shape: asymmetric editorial radii — hero and audio cards use 3px 3px 30px 3px; modals are 24px top sheets.
• Layout: 760px max-width, mobile-first, generous whitespace, 44px+ touch targets, safe-area insets.
• Motion: restrained. The gold pulse dot is the primary motion element; view transitions are simple.

────────

9. Data Model

Three tables, per-installation isolated storage (e.g., SQLite via Drizzle or equivalent).

sources

|Column                     |Type       |Notes                                                                 |
|---------------------------|-----------|----------------------------------------------------------------------|
|`id`                       |integer PK |                                                                      |
|`name`                     |text       |User-provided, e.g., “Example Creator”                                |
|`platform`                 |text       |YouTube / Xiaohongshu / Podcast / Newsletter / Other / Muse (built-in)|
|`source_identifier`        |text UNIQUE|Stable external ID or URL for the source                              |
|`frequency`                |enum       |`daily` / `twice_weekly` / `weekly` / `monthly`                       |
|`digest_time`              |text HH:MM |Default `08:00`, recipient-local (DST-aware)                          |
|`content_types`            |JSON       |e.g., `["video","image","text","audio"]`                              |
|`active`                   |boolean    |Soft-delete flag                                                      |
|`created_at` / `updated_at`|timestamps |                                                                      |

summaries (editions)

|Column                                                                    |Type                        |Notes                                                                         |
|--------------------------------------------------------------------------|----------------------------|------------------------------------------------------------------------------|
|`id`                                                                      |integer PK                  |                                                                              |
|`source_id`                                                               |FK → sources, cascade delete|                                                                              |
|`period_key`                                                              |text                        |e.g., `2026-09-25`; UNIQUE(`source_id`, `period_key`) — one edition per period|
|`period_label`                                                            |text                        |Localized display label, e.g., “Sep 25” / “9月25日”                             |
|`title`                                                                   |text                        |Edition title                                                                 |
|`body`                                                                    |text (Markdown)             |Full summary                                                                  |
|`source_url` / `source_title`                                             |text                        |Original source reference                                                     |
|`published_at`                                                            |timestamp                   |                                                                              |
|`duration_label`                                                          |text                        |e.g., “Reading time ~6 min”                                                   |
|`audio_url`                                                               |text                        |Legacy audio slot (preserved, never overwritten)                              |
|`audio_url_en`                                                            |text                        |English audio (remote HTTPS MP3 at ingest)                                    |
|`audio_blob_key` / `audio_blob_key_en`                                    |text                        |Owned-storage keys, e.g., `digest-audio/{id}/{track}.mp3`                     |
|`audio_import_status`                                                     |enum                        |`not_needed` / `pending` / `ready` / `failed`                                 |
|`audio_import_attempts` / `audio_import_error` / `audio_import_updated_at`|                            |Import bookkeeping                                                            |
|`transcript_en`                                                           |text                        |Matches the English audio                                                     |
|`transcript_secondary` / `transcript_secondary_language`                  |text                        |`zh` / `es` / `fr`                                                            |
|`recommendation`                                                          |text                        |Optional callout                                                              |
|`extra_links`                                                             |JSON                        |“Also worth a look” links                                                     |
|`feed_items`                                                              |JSON                        |Muse Daily structured items: `[{kicker, category, title, summary}]`           |
|`is_read`                                                                 |boolean                     |                                                                              |
|`created_at` / `updated_at`                                               |timestamps                  |                                                                              |

user_settings (singleton, id = 1)

|Column                          |Notes                                                                                                             |
|--------------------------------|------------------------------------------------------------------------------------------------------------------|
|`language`                      |Interface language: `en` / `zh`                                                                                   |
|`narrator_name`                 |Recipient-specific narrator display name; defaults to the recipient’s Muse agent name when detectable             |
|`voice`                         |Narration voice option                                                                                            |
|`secondary_transcript_language` |`zh` / `es` / `fr`                                                                                                |
|`podcast_provider`              |Connected hosting provider identifier; `null` until a supported provider is authorized                            |
|`podcast_provider_connection_id`|Reference to the recipient-scoped provider authorization held in a secure connection store; never a raw credential|
|`podcast_feed_url`              |Recipient-specific RSS URL; `null` until a feed is created or connected                                           |
|`podcast_connection_status`     |`disconnected` / `connecting` / `connected` / `unsupported` / `error`                                             |
|`podcast_publish_permission`    |`none` / `per_episode` / `standing`; defaults to `none` and must reflect the recipient’s explicit approval        |

Published actions (server API surface)

Implement these actions; do not implement any bootstrap/seed action that hardcodes a specific channel, edition, or URL:

• getDashboard → per-source counts, total_unread, latest_unread
• getSource(source_id) → source + its editions
• getSummary(summary_id) → edition detail; triggers audio import at read time
• createSource(...) → upsert on source_identifier (re-adding reactivates)
• updateSource(...) → frequency / digest_time / name
• deleteSource(source_id) → cascades editions + progress; refused for the built-in Muse Daily source
• markSummaryRead(summary_id)
• upsertDigest(...) → ingestion API; requires source_identifier + period_key; auto-creates the built-in Muse Daily source record on first use; on update, never replaces the legacy audio slot and never implicitly replaces audio_url_en
• repairMissingAudio() → retries all editions with remote audio
• getsettings / updatesettings

────────

10. Muse Daily Workflow

1. The built-in source has the reserved identifier muse-feed, name/platform “Muse”, default frequency daily at 06:00, content types text+audio.
2. It is auto-created on the first upsertDigest call with source_identifier = "muse-feed" — bound to the recipient’s own Muse Feed content.
3. It renders as a dedicated gold card on Home (not in the regular source list) and its deletion is prohibited client- and server-side.
4. Its editions are titled <localized> · <period label> and carry structured feed_items.
5. If the recipient’s Muse Feed cannot be detected, ask them to confirm or select it before generating anything. Never fall back to another user’s feed.

────────

11. External Source Workflow

1. User adds a source via the Add Source modal (§7.5). A recipient-scoped source record is created.
2. On each scheduled window, the pipeline:
  • Detects new content since the previous completed edition.
  • If there is no new content, writes nothing (no empty editions).
  • Generates the edition (summary, transcripts, audio) and writes it via upsertDigest.
3. The edition appears in the listening queue and on the source timeline with an unread indicator.
4. Frequency/time changes in Settings apply to future editions only.
5. Deleting a source removes its editions and progress permanently (two-step confirm).

────────

12. Scheduling Logic

• Supported frequencies: Daily, Twice a week (Wednesday & Sunday), Weekly (Saturday), Monthly (1st).
• Each source stores its own digest_time (recipient-local wall clock, DST-aware).
• A daily reconciliation pass aligns all source schedules with the recipient’s settings.
• Schedule edits take effect for future editions; in-flight or past editions are untouched.
• If a scheduled run finds no new content, it ends silently — no empty edition, no notification.

────────

13. Summary Generation Rules

1. Generate a concise but meaningful summary; preserve important context, claims, names, and takeaways.
2. Structure with headings; keep it scannable.
3. Include the original source link whenever available.
4. Every summary is labeled as AI-generated in the UI.
5. When the original is worth experiencing directly, say so explicitly (“worth watching/reading in full”).
6. One edition per source per period — enforced by UNIQUE(source_id, period_key).
7. Never write placeholder or empty content. If generation fails, the edition is not created.
8. Summaries follow the interface language for titles/body structure; the second language appears only in the transcript area (see §18 / Localization).

────────

14. Transcript Generation Rules

1. Every new edition ships with an English transcript that matches its English audio.
2. One optional secondary-language transcript per edition: Simplified Chinese, Spanish, or French — chosen in Settings.
3. The secondary-language choice applies to future editions only.
4. In the edition view, language tabs render only for transcripts that exist for that edition (English default; missing secondary tab is hidden, not disabled).

────────

15. Audio Generation Rules

1. New editions generate English audio only, narrated using the recipient-specific narrator_name and selected voice. Default the name to the recipient’s own Muse agent when detectable; otherwise ask the recipient. Never inherit another installation’s narrator identity.
2. At ingest, the remote HTTPS MP3 is imported into the recipient’s own blob storage (digest-audio/{edition_id}/{track}.mp3), up to 3 attempts, with status tracked (pending → ready / failed) and errors recorded.
3. Playback is served via short-expiring signed URLs (e.g., 6-hour expiry).
4. The player is a native audio element labeled “Narrated by {narrator_name}” with a “listening position is saved” note.
5. Playback progress persists locally (e.g., localStorage key digest-audio-progress:{edition_id}:{track}); resume only when more than ~10 seconds was played and more than ~10 seconds remain.
6. When playback ends, the edition is auto-marked finished and saved progress is cleared.
7. Load failures show a retry state; genuinely missing audio distinguishes “still preparing” (auto-retries in the background) from “unavailable.”
8. External podcast clients do not reliably return playback-completion state to Sifti. Keep the manual Mark as finished action available so a recipient who listened externally can remove the edition from the unfinished queue without replaying it inside Sifti.

────────

16. Podcast Publishing Rules

1. The podcast destination is per-recipient and opt-in. A fresh installation has no podcast feed URL.
2. Configure the feed as link-only/unlisted when the selected provider supports it: not submitted to public directories, but accessible to anyone with the URL. If the provider cannot guarantee this behavior, disclose that limitation before connection and do not describe the feed as private or unlisted.
3. Creating a destination and publishing any episode requires the recipient’s explicit connection and approval. Feed-creation approval covers publishing a provider-required initialization trailer (see §16.1), but it does not authorize publication of any existing digest. Per-episode approval is the default; a standing permission is acceptable only if the recipient grants it clearly.
4. Publish only the recipient’s own editions, to the recipient’s own destination. Never publish to any other account, feed, or destination.
5. The app stores the feed URL as a per-installation setting (not hardcoded) and offers copy-to-clipboard with copied/failed feedback.
6. Publishing success/failure is surfaced per episode in the UI.
7. Explain that the copied RSS URL can be added to compatible podcast clients that support manual RSS subscription. Provide both Copy RSS link and Copy for Apple Podcasts actions; both copy the same recipient-specific RSS URL, while the Apple action additionally displays the Apple Podcasts paste instructions. Apple Podcasts on iPhone, iPad, and Mac and Pocket Casts are examples, but compatibility and update behavior are client- and provider-dependent; do not promise support in every podcast app.
8. Listening progress and completion state in external podcast clients are not assumed to sync back to Sifti. After listening externally, the recipient uses Mark as finished in Sifti to update the listening queue.
9. A bare RSS URL is a subscription/read address, not proof of write permission. Do not treat pasted RSS text as a publishing connection. Automatic publishing requires either the Muse environment’s own podcast-publishing capability or a recipient-authorized podcast host integration.

16.1 Creating the podcast feed (recipient’s Muse follows these steps)

The template ships with no pre-created feed and no hardcoded feed URL. The “Create my podcast feed” action starts a recipient-specific provisioning flow; the recipient’s Muse must provision the feed or report that the required capability is unavailable. Do not skip these steps or assume a feed already exists:

1. The trigger is the recipient tapping “Create my podcast feed” in the app’s Settings panel (or an equivalent explicit yes in chat). The Settings panel must first disclose that a provider-required “Welcome to Sifti” trailer may be published to initialize the feed. After that disclosure, the tap IS the explicit request and approval required by §18 for feed creation and, when required, the initialization trailer — do not ask again. If the recipient has not tapped it (or otherwise said yes after the same disclosure), do not create a feed.
2. The recipient’s Muse explicitly checks the current environment for native podcast-publishing/provisioning capability (this check runs inside the provisioning flow, not as a separate app UI state). Do not infer “unsupported” merely because no feed exists yet, because a new recipient is expected to begin without one. The app shows the unsupported state only after this capability check actually fails.
3. When native capability is available, use it (not any feed, URL, or account from this template — there are none) to create a brand-new podcast feed owned by the recipient. Suggested feed title: “Sifti” (the recipient may rename it). Configure it as link-only/unlisted if the provider supports that mode; otherwise explain the provider’s actual discoverability before proceeding.
4. Some providers require one published item before they return a valid RSS feed. If so, the feed-creation approval from step 1 covers publishing a short initialization trailer titled “Welcome to Sifti” — no separate approval is required. Generate a brief neutral introduction using the current installation’s narrator_name and selected voice. The spoken host name must match the recipient’s current Muse agent identity when detectable; never use “Momo” or any other inherited name unless that is actually the recipient’s chosen narrator. Publish only this initialization trailer. Do not publish, modify, or mark any existing digest as heard during feed initialization.
5. Take the newly created feed’s RSS URL and store it as a per-installation setting in the app (e.g., in user_settings or an equivalent app setting). Never hardcode it in code.
6. Verify the Settings podcast panel now shows the connected state with the new RSS URL in the copy panel.
7. Each subsequent digest publication follows the approval gate in §18; feed creation and trailer initialization do not grant permission to publish earlier or future digests automatically.

If the explicit native capability check confirms that your environment has no podcast-publishing capability, tell the recipient plainly that the feed cannot be created automatically. If a supported podcast-host integration is available, offer a secure Connect a podcast host authorization flow and let that provider create or return the recipient’s feed. Never request or store raw provider credentials in the template. If no supported integration is available, offer Continue with in-app listening only.

Do not ask the recipient to find and paste an arbitrary RSS URL. An existing RSS URL may be copied into a podcast client for listening, but Sifti cannot publish new episodes to it unless the corresponding host has separately granted write access through a supported connection.

────────

17. Localization Rules

• Interface languages: English and Simplified Chinese. A segmented picker switches UI copy; it never changes stored source data, audio, or transcripts.
• Default bilingual configuration: English + Simplified Chinese transcripts.
• Secondary transcript options: Simplified Chinese, Spanish, French — all supported as transcript options.
• Do not claim the interface supports Spanish or French — those are transcript options only.
• One-language-on-screen rule: the interface shows exactly one language at a time. The second language appears only inside an edition’s transcript area.
• Dates and period labels use the editorial serif treatment and follow the interface language.

────────

18. User Permissions and Approval Gates

|Action                                            |Gate                                                                                             |
|--------------------------------------------------|-------------------------------------------------------------------------------------------------|
|Bind Muse Daily to the recipient’s Muse Feed      |Automatic if detectable; otherwise ask the recipient to confirm/select                           |
|Add an external source                            |User action in the Add Source modal                                                              |
|Connect an external service (channel API, etc.)   |Explicit recipient approval                                                                      |
|Create a podcast destination                      |Explicit recipient approval — tapping “Create my podcast feed” in Settings counts as the approval|
|Publish an episode to the podcast destination     |Explicit recipient approval (per episode, or a clearly granted standing permission)              |
|Delete a source                                   |Two-step confirm; built-in Muse Daily source is never deletable                                  |
|Change voice / transcript language / schedule     |Allowed anytime; applies to future editions only                                                 |

────────

19. Empty, Loading, and Error States

• Global loading: three gold dots.
• Load error (all views): “Couldn’t load — try again” with a retry button.
• “You’re all caught up”: home hero when the queue is empty.
• No external sources: “No external sources have been added” + Add Source CTA.
• Awaiting first edition: source timeline shows “Your first digest is on the way”; Muse Daily card shows “Your latest edition will appear here.”
• No new content: scheduled run ends silently; no edition is created.
• Audio loading / failed: retry control; missing-audio states distinguish preparing vs. unavailable.
• Schedule saving: inline saving → saved / error states on the Settings rows.
• Feed copy: copied / failed feedback in the podcast panel.
• Delete confirm: explicit two-step dialog with permanent-removal warning.
• Read states: gold “unfinished” pill vs. neutral “finished” pill.
• Podcast disconnected: explanatory empty state (see §7.4.5).
• Podcast unsupported: shown only after the recipient’s Muse has explicitly checked for native podcast-provisioning capability and found none. Explains that this Muse environment cannot provision or publish a feed automatically. Offer a supported Connect a podcast host authorization flow when available; otherwise offer Continue with in-app listening only. Never present a bare RSS URL field as a writable connection.
• Podcast publish result: per-episode success / failure notice.

────────

20. Acceptance Tests

A correct build from this template must pass all of these:

1. A new recipient sees their own Muse Daily content — never another user’s editions.
2. A new recipient starts with zero external sources and a visible Add Source action.
3. No other installation’s source names or URLs appear anywhere in the app.
4. No other installation’s summaries, transcripts, or audio appear anywhere.
5. Adding a source creates a recipient-scoped record and recipient-scoped links.
6. Scheduled digests follow the recipient’s selected frequency and digest time.
7. Switching the interface between English and Simplified Chinese works and changes only UI copy.
8. English + Simplified Chinese transcript generation works for new editions.
9. Spanish and French are selectable as secondary transcripts.
10. Generated audio belongs to the correct recipient and plays from their own storage.
11. Podcast publishing is impossible without the recipient’s own connection and approval.
12. The template file itself contains no credentials, tokens, or identifiers.
13. Two separate installations cannot see or access each other’s data in any way.
14. When the recipient requests a podcast feed, Muse explicitly checks native podcast-publishing capability before deciding which flow to show. If capability is available, Muse provisions a brand-new recipient-owned feed (§16.1) and the Settings panel shows it as connected. Only after that check fails may the app offer a supported recipient-authorized podcast-host connection or in-app listening only.
15. The narrator display name is scoped to the recipient and never inherited from another installation.
16. Completing playback inside Sifti marks an edition finished automatically; manually marking an externally heard edition removes it from the unfinished queue.
17. In the connected podcast state, Copy RSS link and Copy for Apple Podcasts both copy the recipient’s own RSS URL; the Apple action also displays correct manual-subscription steps and never claims to create a public Apple Podcasts catalog link.
18. Pasting a bare RSS URL never grants publishing permission. The app reaches connected only after native provisioning or a supported provider authorization confirms write access and returns the recipient’s feed URL.
19. If the provider requires a first published item to initialize the feed, the feed-creation approval covers publishing the “Welcome to Sifti” trailer; no existing digest is published, modified, or marked as heard during initialization.
20. The initialization trailer uses the recipient’s current narrator_name and voice, and feed initialization neither publishes existing digests nor changes their listening status.

────────

21. Known Limitations

1. Content generation pipeline is external. The application is the display/playback/account-scoping layer. Detecting new content, writing summaries, translating transcripts, and synthesizing audio are performed by an external pipeline (scheduled jobs + agent) that writes editions through the upsertDigest ingestion API. The template specifies the contract; the pipeline implementation is the recipient’s responsibility.
2. Podcast feed hosting is external. The app displays, copies, and manages the recipient’s feed link; actual RSS hosting and distribution live outside the app. The recipient’s Muse provisions the feed via §16.1 using its own podcast-publishing capability — the template prescribes the steps, not a specific hosting service.
3. External playback state is not synchronized. Sifti cannot assume that a podcast client reports listening progress or completion back to the Muse application. Recipients manually mark externally heard editions as finished.
4. In-app Q&A is a placeholder. The edition view includes a question box that copies the question to chat; live API-backed answering is reserved for a future version.
5. Dark-mode visuals are defined via adaptive CSS (prefers-color-scheme); verify both themes during the build.
6. No system-voice fallback player. Only natural narrated audio is supported; do not implement a synthetic speech fallback unless the recipient requests it.
7. One edition per source per period. Backfills for the same period update rather than duplicate.

────────

22. Version Metadata

|Field                    |Value                                                                                                                                                                                                                                                                                           |
|-------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|Template name            |Sifti_Muse_Build_Template                                                                                                                                                                                                                                                                       |
|Version                  |v0.4.3                                                                                                                                                                                                                                                                                          |
|Created                  |2026-09-25                                                                                                                                                                                                                                                                                      |
|Updated                  |2026-09-27                                                                                                                                                                                                                                                                                      |
|v0.2 changes             |Spanish/French secondary transcripts confirmed working; experimental labels removed (§7.4/§14/§17/§20); podcast feed creation procedure added (§16.1); tapping “Create my podcast feed” counts as explicit approval; feed URL is stable so the recipient subscribes once.                       |
|v0.3 changes             |Clarified that the template contains no pre-created feed; added podcast connection and permission fields to `user_settings`; made podcast provisioning acceptance tests capability-dependent; added an explicit unsupported state; qualified link-only/unlisted behavior by provider capability.|
|v0.4 changes             |Made narrator identity recipient-specific; added provider-aware RSS client instructions; clarified that external podcast playback does not automatically update Sifti and requires manual “Mark as finished.”                                                                                   |
|v0.4.1 changes           |Added a dedicated “Copy for Apple Podcasts” helper; corrected the unsupported flow so a bare RSS URL is never treated as a writable destination; added supported podcast-host authorization or in-app-only alternatives.                                                                        |
|v0.4.2 changes           |Required an explicit native podcast-capability check before showing unsupported; added separately approved feed-initialization trailer behavior; bound the trailer narrator to the recipient’s current Muse agent identity; preserved existing digests during initialization.                    |
|v0.4.3 changes           |Corrected to match the shipped design: removed the “checking capability” app progress state (the capability check runs inside Muse’s provisioning flow, not as app UI); after an upfront disclosure, feed-creation approval covers the provider-required “Welcome to Sifti” trailer with no separate approval gate (§7.4/§16.1/§18/§19/§20); unsupported state follows Muse’s explicit capability check. Trailer narrator rule and digest-preservation guarantees unchanged. |
|Source application       |Sifti (dark editorial, mobile-first listening companion)                                                                                                                                                                                                                                        |
|Interface languages      |English, Simplified Chinese                                                                                                                                                                                                                                                                     |
|Secondary transcripts    |Simplified Chinese, Spanish, French                                                                                                                                                                                                                                                             |
|Narrator                 |Recipient-specific Muse agent identity (name and voice configurable for future editions)                                                                                                                                                                                                        |
|Data isolation           |Per-installation; no shared records, links, schedules, or identifiers                                                                                                                                                                                                                           |
|Personal data in template|None — verified by final privacy audit (§23)                                                                                                                                                                                                                                                    |

────────

23. Final Privacy Audit

Before this file was delivered, it was scanned for:

☑ Source names, creator/blogger selections, YouTube channels — none present (only “Example Creator” and https://example.com/source placeholders)
☑ Source URLs, feed URLs, podcast destinations — none present
☑ Summaries, transcripts, audio references — none present
☑ Dates or scheduling history — none present (only structural examples like 2026-09-25 as a format illustration and 08:00 as a default)
☑ Account identifiers, credentials, tokens, API keys — none present
☑ Hidden identifiers from the source installation — none present
☑ Screenshots or cached content — none present

Result: the file contains only reusable product structure, behavior specifications, design tokens, neutral placeholders, and supported-language information. Another user’s Muse can build a clean Sifti installation from it without gaining access to any part of the original installation.
