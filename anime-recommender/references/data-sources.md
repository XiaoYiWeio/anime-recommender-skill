# Anime Data Sources

Use this reference when recommendations need live metadata, source selection, or cross-source merging.

## Source Selection

### Bangumi

Best for Chinese-language anime discovery and Chinese-community context.

- Docs: `https://bangumi.github.io/api/`
- Useful endpoints include `/calendar`, `/v0/search/subjects`, and `/v0/subjects/{subject_id}`.
- Use for Chinese titles, subject summaries, air dates, ratings, rank, collection counts, relations, and daily calendar.
- Prefer this source when the user writes in Chinese or asks about 番剧/新番/补番.

### AniList

Best for flexible candidate search and rich tags.

- Docs: `https://anilist.gitbook.io/anilist-apiv2-docs`
- GraphQL endpoint: `https://graphql.anilist.co`
- Use for tags, genres, format, status, season/year, relations, staff, studios, and recommendation-style searches.
- Prefer when filtering by multiple structured conditions such as completed TV anime from a year range with specific tags.

### Jikan

Best for unauthenticated MyAnimeList-derived metadata.

- Docs: `https://docs.api.jikan.moe/`
- REST base: `https://api.jikan.moe/v4`
- Useful routes include `/anime`, `/seasons/{year}/{season}`, `/top/anime`, and `/recommendations/anime`.
- Respect conservative limits; docs historically list about 3 requests/second and 60 requests/minute.
- Treat as a MAL metadata proxy, not an official source.

### MyAnimeList Official API

Best when the user wants recommendations based on their authenticated MAL list.

- Docs entry point: `https://myanimelist.net/apiconfig/references/api/v2`
- Requires API credentials/OAuth or client ID depending on endpoint.
- Do not make this a first-version dependency unless the user has credentials configured.

### ids.moe

Best for mapping IDs across databases.

- Site/API: `https://ids.moe/`
- Use when merging Bangumi, AniList, MyAnimeList, Kitsu, Simkl, or other records.
- If ID mapping is unavailable, deduplicate by normalized title, year, and relations, then disclose uncertainty.

### Kitsu

Useful fallback for JSON:API anime metadata and streaming links.

- Docs: `https://hummingbird-me.github.io/api-docs/`
- Use only when it adds information not already available from Bangumi/AniList/Jikan.

### Simkl

Useful if the user tracks anime together with TV and movies.

- Docs: `https://docs.simkl.org/how-to-use-simkl`
- Consider for cross-media watchlists or tracking workflows, not as a first-pass recommendation source.

## Practical Merge Rules

- Normalize titles by removing punctuation, comparing original/romaji/English/Chinese aliases, and checking year plus format.
- Treat sequels, remakes, recap films, specials, and spin-offs as separate watch items unless the user asks for franchise-level advice.
- Prefer higher-confidence source fields:
  - Chinese title/community context: Bangumi
  - Tags/status/relations: AniList
  - MAL score/member count/rank: Jikan or official MAL
  - Cross-source identity: ids.moe
- When sources disagree, report the conflict only if it affects the recommendation, watch order, status, or availability.

## Score Use

Do not rank by score alone. Consider:

- score value
- rating/member count
- popularity and recency
- whether the audience niche matches the user
- whether the show is still airing and therefore unstable

Avoid recommending obscure high-score items unless there are enough users or the taste match is particularly strong.
