# Media API Candidates

These notes were extracted from the PRD, not newly researched. Availability,
authentication, pricing, and capabilities below are inherited, unverified claims;
check official provider documentation before implementation. No provider comparison
or feasibility validation has been completed by this extraction.

## Existing candidates

| Category | API                             | Notes                                                       |
| -------- | ------------------------------- | ----------------------------------------------------------- |
| Games    | IGDB (via Twitch)               | Cover art, platform info                                    |
| Books    | Google Books API                | Free, no key required for basic queries                     |
| Movies   | TMDB                            | Free tier, cover art + year                                 |
| Music    | MusicBrainz + Cover Art Archive | Free, no auth. Or consider Spotify API for better cover art |

IGDB is the existing choice for the games-first design. All other candidates are
preserved context for the broader product vision, not initial-release work.

## Questions to verify

- IGDB/Twitch authentication, browser access, credential handling, and rate limits.
- Provider terms for cover art, attribution, and caching/offline use.
- Current access requirements and capabilities of the other candidates if those categories enter scope.

## Links

- [Product requirements](../PRD.md)
- [Games-first design](../design/games-first.md)
