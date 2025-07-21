# Daily Standard Ebooks JSON

This repository automatically fetches one new public-domain ebook per day from Standard Ebooks’ OPDS feed and publishes a minimal JSON snapshot (`today.json`) with the following fields:

- **date**: UTC date of selection (`YYYY-MM-DD`)  
- **title**: Book title  
- **author**: Author name  
- **summary**: Plain-text summary  
- **coverUrl**: Full-resolution cover image URL  
- **entryUrl**: Canonical ebook page URL (ideal for QR codes)  
- **subjects**: Array of Standard Ebooks subject terms  

Every night at 00:05 UTC (or on demand via workflow dispatch), GitHub Actions:

1. Downloads the full OPDS feed (Atom XML).  
2. Counts `<entry>` elements.  
3. Computes a “random” index from today’s date.  
4. Extracts that single `<entry>`.  
5. Pulls out only the desired fields via `xmlstarlet` + `jq`.  
6. Emits `today.json`, and commits & pushes if it changed.

---

## Usage

1. **Clone** this repo.  
2. **Add** a [`OPDS_KEY`](https://standardebooks.org/developer) secret in Settings → Secrets.  
3. **Watch** the repo so you get daily updates in your feed.  
4. Use the raw `today.json` URL in your web app, site, or QR-code generator.
