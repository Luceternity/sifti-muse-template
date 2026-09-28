# Using the Sifti Muse Build Template

This guide explains how to create a fresh Sifti installation in your own Muse environment using the portable build specification.

## What You Need

- Access to a Muse environment that can build applications from an attached specification
- Your own Muse account and Muse Feed
- Public or authorized content sources you want to follow
- Optional access to audio-generation or podcast-publishing capabilities

Capability availability may differ between Muse accounts and environments. The template instructs Muse to report unsupported features rather than fabricate a connection or reuse another installation's data.

## Installation

1. Download the Markdown file from the repository:

   ```text
   template/Sifti_Muse_Build_Template_v0.4.3.md
   ```

2. Open a new build conversation in your own Muse environment.

3. Attach the Markdown file. Do not paste another person's source list, feed URL, generated summaries, or podcast destination into the conversation.

4. Send this instruction:

   > Build a new Sifti application from this specification inside my Muse environment. Use only my account, my Muse Feed, my sources, my schedules, my generated content, and destinations that I explicitly connect. Read the entire specification before building, and ask for approval before connecting an external service or publishing audio.

5. Review Muse's proposed implementation before allowing external connections.

6. When the build finishes, complete the validation checklist below.

## First-Run Validation

Confirm all of the following before adding real sources:

- The application is named **Sifti**.
- The external Sources section is empty.
- No unfamiliar creator, channel, URL, edition, transcript, audio, or podcast link appears.
- Muse Daily is connected only to your own Muse Feed, or Muse asks you to select it.
- Podcast publishing begins in a disconnected state.
- No external service is connected without your approval.
- English and Simplified Chinese interface switching works.
- The narrator name defaults to your own Muse agent identity rather than an example identity from another installation.

If any data from another person or installation appears, stop the build and remove the installation. Do not continue using it.

## Add Your First Source

1. Select **Add Source**.
2. Enter a source name and choose its platform.
3. Add a public or authorized source URL.
4. Choose a digest frequency:
   - Daily
   - Twice a week
   - Weekly
   - Monthly
5. Select the content types and digest time.
6. Save the source.

For the first test, use a low-risk public source and verify the resulting summary against the original material.

## Configure Languages

- Interface language: English or Simplified Chinese
- Primary transcript and narration: English
- Optional secondary transcript: Simplified Chinese, Spanish, or French

Language changes apply to future editions unless Muse explicitly supports regeneration. Existing editions should not be silently rewritten.

## Audio and Listening Progress

New editions may include English narrated audio when audio generation is available. The narrator identity should use your own Muse agent's name and selected voice. Playback progress should be saved and resumable. Finishing playback inside Sifti—or selecting **Mark as finished**—removes the edition from the unfinished queue.

If you listen in an external podcast app, its playback-completion state may not sync back to Sifti. Return to the edition in Sifti and select **Mark as finished** so it leaves the unfinished queue; you do not need to replay it inside Muse.

If audio generation is unavailable, Sifti should show an honest unavailable or unsupported state rather than a broken player.

## Podcast Setup

Podcast publishing is optional.

1. Open **Settings**.
2. Read the feed-creation notice, including the provider's privacy and discoverability behavior.
3. Select **Create my podcast feed** only if you want a recipient-owned RSS destination. Some providers require a short **Welcome to Sifti** trailer before they return a valid RSS feed; the notice must disclose that selecting the button also authorizes this initialization trailer when required.
4. Muse checks for native podcast-publishing capability inside the provisioning flow. The absence of an existing feed is not evidence that the capability is unsupported.
5. If a trailer is required, confirm that it uses your current Muse agent name and voice. It must not publish, modify, or mark any existing digest as finished.
6. Approve each later digest before publication unless you intentionally grant a standing permission.

Once connected, copy the recipient-specific RSS URL and add it to a compatible podcast app using its **Add by URL** or **Follow a Show by URL** function. Apple Podcasts on Mac and Pocket Casts are examples; support and update behavior can vary by client and provider.

If Muse cannot provision a feed, Sifti should offer either:

- A supported authorization flow for a podcast host you own, when available, or
- In-app listening without podcast publishing

Do not paste a bare RSS subscription URL into Sifti as though it grants publishing access. An RSS URL normally allows reading or subscribing; publishing requires Muse's native capability or a supported host authorization with write access.

An unlisted feed is still accessible to anyone who has its URL. Do not treat an RSS URL as a secret-storage mechanism. Listening progress and completion status in an external podcast app may remain separate from Sifti.

## Updating the Template

Installing a newer specification does not guarantee automatic migration of an existing Sifti application. Before applying a later version:

1. Review its changelog.
2. Ask Muse to describe the proposed changes without modifying the current application.
3. Back up or record any settings you need.
4. Approve the update only after confirming that existing sources and generated content will not be replaced unexpectedly.

## Troubleshooting

### Muse Daily cannot be detected

Ask Muse to show the available feed choices and select only your own Muse Feed. Never substitute a sample or another user's feed.

### A source produces no edition

Check whether new eligible content exists, whether the source is publicly accessible, and whether the content-generation pipeline is available.

### Podcast creation is unsupported

First confirm that Muse actually ran its native podcast-provisioning check; a new account having no existing feed does not mean provisioning is unsupported. If the check fails, continue with in-app listening or use a supported authorization flow for a podcast host you own. Do not reuse a URL supplied by another installation, and do not treat a pasted RSS subscription URL as publishing permission.

### The build has no RSS link

If Sifti was created but the Podcast section still has no RSS URL, ask Muse to run the recipient-specific provisioning flow explicitly. You can send:

> Check whether this Muse environment has native podcast-provisioning capability. If it does, create a new Sifti podcast feed owned by my account and store and display its real RSS URL in this installation. If the provider requires a short “Welcome to Sifti” trailer to initialize the feed, explain that before publishing it and use my current Muse agent identity as the narrator. Do not reuse, invent, or copy a feed from another account.

This request should create a real recipient-owned feed only when the current environment supports it. Muse must not fabricate a URL or fall back to another installation's feed.

### The initialization trailer uses the wrong agent name

Stop before publishing additional episodes. Ask Muse to set `narrator_name` to your current Muse agent identity and regenerate only the initialization trailer if needed. Do not allow the correction to republish or change existing digests.

### The interface builds but no summaries appear

The application layer may be working while the external ingestion and generation pipeline is missing. See [Known Limitations](LIMITATIONS.md).
