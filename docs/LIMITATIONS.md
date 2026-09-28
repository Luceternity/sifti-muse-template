# Known Limitations

Sifti v0.4.3 is a portable Muse build specification for a functional prototype. It is not a universal source-code export or a guaranteed one-click deployment package.

## 1. Content Generation Pipeline

The template specifies the product interface, data model, scheduling behavior, permission gates, and `upsertDigest` ingestion contract. It does not include a universal implementation for:

- Detecting new content from every supported platform
- Extracting video, image, audio, newsletter, or webpage content
- Generating summaries
- Translating secondary transcripts
- Synthesizing narrated audio
- Running scheduled jobs continuously

The recipient's Muse environment must implement these capabilities or connect to an external pipeline.

## 2. Platform Access

Content availability depends on the source platform. Login walls, private accounts, anti-automation controls, deleted content, region restrictions, API limits, and unsupported formats may prevent ingestion.

Adding a source URL does not guarantee that Muse can access or process it.

## 3. Muse Daily Connection

The specification requires each installation to use only the recipient's own Muse Feed. Automatic feed detection depends on Muse account capabilities and permissions. If the feed cannot be detected, the recipient must select or confirm it.

## 4. Podcast Publishing

Sifti does not bundle a universal podcast host. Automatic feed creation requires native podcast-publishing capability in the recipient's Muse environment. Muse checks this capability inside the provisioning flow; the absence of an existing feed alone does not establish that provisioning is unsupported.

If native capability is unavailable, Sifti can provide in-app listening or use a supported, recipient-authorized podcast-host integration when one exists. A bare RSS URL normally provides subscription access, not write access, and cannot be used as proof that Sifti may publish to that destination. Feed stability, privacy, storage limits, and distribution behavior depend on the selected provider.

Some providers require an initial published item before producing a valid RSS feed. Sifti may publish a short **Welcome to Sifti** trailer under the disclosed feed-creation approval. This trailer must use the recipient's current Muse agent identity and must not publish, modify, or change the listening status of existing digests.

“Unlisted” does not mean secret. Anyone with the RSS URL may be able to access the feed.

External podcast apps do not reliably report playback completion back to Sifti. After listening externally, the recipient must manually select **Mark as finished** in Sifti to keep the unfinished queue accurate.

## 5. Audio Generation

Natural narrated audio depends on an available TTS service and supported voice options. Voice names, quality, duration limits, quotas, and availability may differ by environment.

The template does not provide a system-voice fallback by default.

## 6. Language Support

The interface currently supports English and Simplified Chinese.

Secondary transcripts support Simplified Chinese, Spanish, and French. Translation quality may vary with subject matter, source quality, terminology, and the model available in the recipient's environment. Important information should be checked against the original source.

## 7. AI Accuracy

AI-generated summaries and transcripts may omit context, misinterpret claims, miss updates, or introduce factual errors. Sifti links back to original material and may recommend viewing or reading it in full.

Sifti should not be used as the sole source for medical, legal, financial, safety-critical, or other high-stakes decisions.

## 8. Copyright and Source Rights

Recipients are responsible for using public or properly authorized sources. The template does not grant rights to republish third-party material.

Public sharing should:

- Link to original content
- Label summaries as AI-generated
- Avoid reproducing substantial copyrighted material
- Avoid cloned voices or protected media without permission
- Respect platform terms and creator rights

## 9. Privacy and Security

The portable specification contains no original-user content or credentials. Actual privacy still depends on how each recipient's Muse environment and connected providers store data.

The template has not undergone an independent security audit. Recipients should review permissions, storage, authentication, logs, and public links before using sensitive sources.

## 10. Product Scope

- In-app Q&A is currently a placeholder.
- Sifti is designed as a single-recipient installation, not a shared multi-user SaaS deployment.
- Existing editions are not automatically regenerated when settings change.
- One edition per source per period is the intended default.
- Migration between template versions is not guaranteed to be automatic.

## 11. No Service Guarantee

Sifti is an evolving prototype and portfolio project. Availability, scheduled execution, third-party integrations, and generated output are not guaranteed.
