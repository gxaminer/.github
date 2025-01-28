# GXaminer

GXaminer is a Chrome extension for remote webpage content inspection and scraping using a client-server architecture.

## Overview

GXaminer enables users to remotely scrape webpage content from Chrome browsers running the GXaminer extension. The system consists of three key components:
- **Chrome Extension**: Scrapes content from the active tab.
- **GXaminer Server**: Handles communication between clients and extensions.
- **Client**: Makes HTTP requests to inspect webpages.

## How It Works

1. **Extension-WebSocket Connection**: The extension maintains a persistent WebSocket connection with the GXaminer server.
2. **Client Request**: Clients send HTTP requests to the server for specific page content.
3. **Content Scraping**: The extension scrapes the active webpage's DOM content.
4. **Return Content**: The server sends the scraped content back to the client.

## System Architecture

```mermaid
sequenceDiagram
    participant Client
    participant Server as GXaminer Server
    participant Extension as Chrome Extension
    participant Webpage

    Note over Extension,Webpage: Extension running in Chrome
    Note over Server: WebSocket connection established

    Client->>Server: HTTP Request to examine URL
    Server->>Extension: WebSocket message requesting page content
    Extension->>Webpage: Access active tab
    Extension->>Webpage: Scrape DOM content
    Webpage-->>Extension: Return page content
    Extension-->>Server: Send scraped content via WebSocket
    Server-->>Client: HTTP Response with page content
