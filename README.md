# Anime Recommender Skill

A Codex/OpenClaw skill for anime recommendations based on natural taste interviews, watch history, preferences, and live metadata sources.

## What It Does

- Starts with a conversational intake instead of forcing users to list anime titles.
- Builds a taste profile from mood, genres, favorite traits, watched shows, dislikes, and content limits.
- Recommends anime with spoiler-safe reasons, caveats, completion status, and confidence.
- Uses live metadata when current season, status, ratings, popularity, watch order, or streaming availability matter.
- Prioritizes Bangumi for Chinese context, AniList for structured tags, Jikan/MAL for score and popularity signals, and ids.moe for ID mapping.

## Install

Copy the `anime-recommender` folder into your local skills directory:

```bash
cp -R anime-recommender ~/.codex/skills/
```

Then invoke it with:

```text
Use $anime-recommender to chat with me about my anime taste and recommend what to watch next.
```

## License

MIT-0. ClawHub-published skills are expected to be freely usable, modifiable, and redistributable under MIT-0.
