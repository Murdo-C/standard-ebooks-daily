# Daily Standard Ebooks JSON

Each day, this repo publishes a curated public-domain ebook—randomly selected from [Standard Ebooks](https://standardebooks.org)—in a minimal JSON format for use in TRMNL or other projects.

## About

This API powers the *Timeless Texts* plugin for [TRMNL](https://usetrmnl.com), a minimal e-ink platform. It was originally built for a TRMNL hackathon during my parental leave. Standard Ebooks’ craft and consistency made them the perfect foundation to build on.

The goal was to deliver a timeless book discovery experience—free, beautifully formatted, and genre-personalized. To achieve this without exposing the full OPDS feed, the plugin uses a lightweight API hosted here, which runs daily via GitHub Actions.

## Features

- **20 daily picks**: One randomly selected book from the entire Standard Ebooks catalog, plus one from each of the 19 subject genres.
- **Minimal JSON output**: Optimized for front-end rendering with only the most relevant fields.
- **Genre personalization**: Books can be filtered by subject using simple front-end logic.
- **Open source & extendable**: Use this API as-is, fork it, or build on it for your own reading tools.

## today.json schema

Each day at 00:05 UTC, a GitHub Action fetches one random book from the full catalog and one from each genre. The result is a JSON file with this structure:

```json
{
  "date": "YYYY-MM-DD",
  "title": "Book Title",
  "author": "Author Name",
  "summary": "Plain-text summary of the book.",
  "coverUrl": "Full-resolution cover image",
  "entryUrl": "Canonical ebook page (ideal for QR codes)",
  "subjects": ["Subject 1", "Subject 2"]
}
```

## How it works

Every night, GitHub Actions:

1. Downloads the full OPDS feed (Atom XML) from Standard Ebooks.  
2. Extracts all `<entry>` elements.  
3. Randomly selects:  
   3.1. One book from the full catalog  
   3.2. One book from each of the 19 genre categories  
4. Parses key fields via `xmlstarlet` and `jq`  
5. Outputs a clean `books.json` (and `today.json` for single-book views)  
6. Commits and pushes if changes are detected  

Built with:
- Languages: Bash, XMLStarlet, jq, Liquid, JavaScript, Tailwind-style CSS
- Deployment: GitHub Actions
- Feeds: Standard Ebooks OPDS

## Credits

Built by Murdo Connochie. Special thanks to the TRMNL team and Standard Ebooks for making great tools and great books.

Fork it. Use the API. And if you build something cool, I’d love to see it.

---

Let me know if you want a version tailored specifically for `books.json` vs `today.json` or if you'd like to embed the GitHub Actions YAML logic inline.
