# Protocols

This document outlines the protocols considered for the Unified Content Collaboration Platform. The choice of protocols is critical for achieving the project's goals of decentralization, interoperability, and privacy.

## Core Requirements Addressed by Protocols

-   **Federation**: Allowing different instances of the service to communicate with each other for public content.
-   **Content Formatting**: Handling different types of content like blog posts, chat messages, and forum threads.
-   **Real-time Communication**: For chat and potential voice/video calls.
-   **Encryption**: Ensuring privacy of user data, especially with End-to-End Encryption (E2EE).

## Federation and Content Protocols

This section covers protocols for sharing content like blog posts, forum discussions, and public chat messages between federated instances.

### ActivityPub

-   **Description**: A W3C standard for decentralized social networking. It powers the Fediverse, including platforms like Mastodon, Lemmy, and PeerTube.
-   **Pros**:
    -   **Wide Adoption**: Connects the platform to a large, existing network of federated services.
    -   **Flexible Content**: Well-suited for blog posts (`Article`), microblogging (`Note`), and threaded conversations, which maps well to the project's goals.
    -   **Mature Standard**: As a W3C Recommendation, it's stable and well-documented.
-   **Cons**:
    -   **Real-time Chat**: Not primarily designed for real-time, synchronous chat. While possible, other protocols are better suited.
    -   **E2EE**: End-to-end encryption is not a part of the core protocol and requires custom extensions.

### Matrix

-   **Description**: An open standard for interoperable, decentralized, real-time communication.
-   **Pros**:
    -   **Excellent for Chat**: Designed for real-time chat with features like typing indicators, read receipts, and more.
    -   **Strong E2EE**: Built-in, audited End-to-End Encryption (Olm/Megolm) is a core feature.
    -   **Versatile**: Can handle blog-style content and forums using room topics and custom message types. It can also bridge to other networks (IRC, XMPP, etc.).
-   **Cons**:
    -   **Complexity**: A full Matrix homeserver is complex and resource-intensive, which could conflict with the "Easy self-hosting" goal.
    -   **Federation Model**: The federation model is designed to replicate room history, which can be heavyweight for sharing simple, public blog posts compared to ActivityPub.

### Nostr (Notes and Other Stuff Transmitted by Relays)

-   **Description**: A simple, modern protocol for decentralized social networking that relies on clients signing events and sending them to simple, replaceable relays.
-   **Pros**:
    -   **Simplicity**: The protocol is extremely simple, and relays are lightweight and easy to run, aligning perfectly with the "Easy self-hosting" goal.
    -   **Resilience**: Its architecture is highly censorship-resistant.
-   **Cons**:
    -   **Immaturity**: The protocol is young and still evolving rapidly.
    -   **Discovery**: Finding users and content can be challenging compared to more established protocols.
    -   **E2EE**: Like ActivityPub, private messaging requires building E2EE on top of the protocol primitives.

## Real-time Communication (Voice and Video)

This section covers protocols for real-time voice and video calls. This functionality depends on a signaling protocol to set up the call and WebRTC to carry the media streams directly between browsers.

### SIP (Session Initiation Protocol)

-   **Description**: A mature, widely-used IETF standard for signaling and controlling multimedia sessions, including voice and video over IP.
-   **Pros**:
    -   **Interoperability**: Connects with a vast ecosystem of existing VoIP systems, hardware phones, and mobile apps.
    -   **Mature and Stable**: A robust and well-understood protocol.
-   **Cons**:
    -   **Complexity**: Implementing or managing a SIP server (like Kamailio or Asterisk) can be complex.
    -   **Web Integration**: Not inherently designed for modern web-first identity systems and can be difficult to run securely in a browser.
    -   **NAT Traversal**: Dealing with firewalls and NAT (requiring STUN/TURN servers) is notoriously complex with SIP.

### Matrix (using WebRTC)

-   **Description**: Matrix uses WebRTC for its voice and video calling, with signaling handled seamlessly through the same Matrix protocol used for chat.
-   **Pros**:
    -   **Unified Protocol**: Reduces complexity by using a single protocol for identity, chat, and call signaling.
    -   **Web Native**: Designed for the web, handling NAT traversal effectively.
    -   **Encrypted**: Leverages the existing identity and encryption framework from the chat protocol.
-   **Cons**:
    -   **Limited Interoperability**: Does not easily connect to the traditional telephony/VoIP world without a dedicated bridge.

## Summary and Final Recommendation

The project's goals require balancing broad federation for public content with secure, private, real-time communication. No single protocol excels at everything.

-   For **public content and federation (blogs, forums)**, **ActivityPub** is the strongest choice. It provides access to the broad Fediverse and is designed for the types of content mentioned.
-   For **real-time communication and E2EE (private chat, calls)**, **Matrix** is the most comprehensive and modern solution. It offers a unified, secure experience for all real-time features.
-   Your suggestion of **SIP** is the industry standard for VoIP but presents integration challenges for a web-first platform compared to the tightly integrated calling in Matrix.

### Recommended Approach

A hybrid approach would best serve the project's vision:

1.  **Use ActivityPub for the Public Federation Layer**: The service would act as an ActivityPub server to publish and federate public content like blogs and forum threads. This maximizes reach and interoperability.
2.  **Use Matrix for Real-time and Private Communication**: The service would include or act as a Matrix homeserver to handle all private chats, group chats, and voice/video calls. This guarantees state-of-the-art E2EE and a seamless user experience.

This hybrid model leverages the strengths of the two leading protocols in the decentralized space. For initial development, focusing on one protocol first would be pragmatic. Given the README's emphasis on varied content formats, starting with **ActivityPub** seems like a logical first step, with Matrix integration to follow. 