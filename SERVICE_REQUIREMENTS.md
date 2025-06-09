# Service Requirements

This document summarizes the functional and technical requirements gathered so far for the unified content collaboration platform.

## Functional Requirements

1. **Content Transformation**
   - The service automatically converts posts, chats, and call transcripts into multiple formats (e.g., blog, email, forum thread) so users can view content in their preferred style.

2. **User Management**
   - Accounts are bound to the local server instance by default.
   - Users should be able to export their account data and easily migrate to another instance with minimal downtime.

3. **Self-Hosting**
   - Installation should be as simple as running a single Go binary with a local SQLite database.
   - Optional container images may be provided for convenience, but they are not required.

4. **Decentralization**
   - Instances can share or federate public content with others. The specifics of the protocol (ActivityPub or a lightweight custom API) remain open for discussion.

5. **Privacy and Security**
   - All private data must be end-to-end encrypted using established libraries (e.g., libsodium or OpenPGP).
   - Public content may be stored in plain text, but transfers between instances should still use HTTPS/TLS.

## Technical Requirements

- **Backend**: Go 1.20+
- **Database**: SQLite (optionally encrypted)
- **Frontend**: HTML5 with minimal JavaScript components, no heavy framework
- **APIs**: REST or gRPC endpoints for posting, retrieving, and transforming content
- **Scalability**: SQLite is sufficient for single-user or small-team setups; the architecture should allow future upgrade paths if larger storage is needed.

These requirements are subject to change as design and implementation progress. Feedback is welcome.
