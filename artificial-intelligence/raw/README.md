# Raw Sources

This directory contains your source documents — articles, papers, transcripts, notes.

## Rules

- **Immutable**: the LLM agent reads from here but NEVER modifies, creates, or deletes files in this directory.
- **You own this layer**: you decide what goes here. Drop files in and tell the agent to ingest them.
- **Preferred format**: Markdown (`.md`). PDFs and plain text also work.
- **Images**: download to `raw/assets/` using Obsidian's "Download attachments" feature.

## Recommended Sources to Start

- Blog posts clipped via Obsidian Web Clipper
- arXiv paper markdown exports
- Transcript notes from talks / podcasts
- Your own handwritten notes or highlights

## Folder Structure

```
raw/
├── README.md         ← This file
├── assets/           ← Downloaded images and attachments
└── <your files>      ← Flat or organized however you like
```

When you're ready to ingest a file, say:  
**"ingest raw/<filename>"**
