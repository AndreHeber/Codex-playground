# Unified Content Collaboration Platform

This project is an experiment in consolidating multiple communication formats—blogs, chats, forums, and call transcripts—into a single, self-hosted service. Creators can publish in their preferred formats while collaborators can read or interact using whichever interface they like. Content is stored once and automatically transformed for different views.

## Key Goals

- **Creator freedom, consumer choice**: A blog post, chat message, or call transcript can be viewed as email, forum thread, or chat depending on user preference.
- **Easy self-hosting**: Runs as a single Go binary backed by SQLite.
- **Decentralized sharing**: Instances may federate with each other for public content.
- **Privacy first**: Uses established end-to-end encryption libraries for private data.

## Technology Overview

- **Backend**: Go
- **Storage**: SQLite (with optional encrypted mode)
- **Frontend**: Basic HTML5 components with light JavaScript
- **Content model**: Markdown with metadata for easy transformation

## Repository Structure

- `SERVICE_REQUIREMENTS.md` – functional and technical requirements for the service
- `README.md` – this file

## Getting Started

1. Install Go (version 1.20 or newer recommended).
2. Clone this repository.
3. Run `go build` to compile the binary.
4. Start the service with `./<binary>` (details will be added as implementation evolves).

The project is in an early design phase. See `SERVICE_REQUIREMENTS.md` for more detail on planned features.
