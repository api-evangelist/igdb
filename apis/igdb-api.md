# IGDB API

The IGDB (Internet Game Database) API provides programmatic access to one of the largest open video game databases on the web, covering games, platforms, companies, genres, releases, covers, screenshots, and more.

## Overview

- **Provider:** IGDB / Twitch
- **Base URL:** `https://api.igdb.com/v4`
- **API style:** REST, POST-only query endpoints with Apicalypse query language
- **Format:** JSON (also supports protobuf)
- **Authentication:** Twitch OAuth Client Credentials (Client-ID + Bearer token)

## Authentication

1. Register an application on the [Twitch Developer Console](https://dev.twitch.tv/console).
2. Capture the resulting **Client-ID** and **Client-Secret**.
3. Exchange the client credentials for an access token:

```bash
curl -X POST "https://id.twitch.tv/oauth2/token" \
  -d "client_id=$CLIENT_ID" \
  -d "client_secret=$CLIENT_SECRET" \
  -d "grant_type=client_credentials"
```

4. Send the access token as `Authorization: Bearer <token>` and the `Client-ID` header on every IGDB request.

## Apicalypse Query Language

IGDB endpoints accept an Apicalypse query string in the request body. Example:

```
fields name,summary,cover.url,first_release_date;
where rating > 80;
sort rating desc;
limit 10;
```

## Core Endpoints

| Endpoint | Description |
| --- | --- |
| `POST /games` | Query video game records and metadata |
| `POST /platforms` | Query gaming platforms and hardware |
| `POST /companies` | Query developer/publisher companies |
| `POST /involved_companies` | Query company involvement on games |
| `POST /genres` | Query genres |
| `POST /themes` | Query themes |
| `POST /game_modes` | Query game modes |
| `POST /covers` | Query game cover artwork |
| `POST /screenshots` | Query screenshots |
| `POST /artworks` | Query promotional artworks |
| `POST /release_dates` | Query release date records |
| `POST /collections` | Query collections |
| `POST /franchises` | Query franchises |
| `POST /keywords` | Query keywords |
| `POST /age_ratings` | Query age ratings |
| `POST /websites` | Query game websites |
| `POST /search` | Cross-entity free-text search |

## Rate Limits

- 4 requests per second per Client-ID.
- Maximum 500 records per request via `limit`; paginate with `offset`.

## Example Request

```bash
curl -X POST "https://api.igdb.com/v4/games" \
  -H "Client-ID: $CLIENT_ID" \
  -H "Authorization: Bearer $TOKEN" \
  -d 'fields name,summary,rating; where rating > 90; sort rating desc; limit 5;'
```

## References

- [API Documentation](https://api-docs.igdb.com/)
- [Getting Started](https://api-docs.igdb.com/#getting-started)
- [Authentication](https://api-docs.igdb.com/#authentication)
- [Apicalypse Query Language](https://apicalypse.io/)
