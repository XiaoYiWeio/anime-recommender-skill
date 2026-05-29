# Anime Recommender Skill

[中文说明](./README.md)

An anime recommendation skill for Codex, Claude Code, and OpenClaw/Claw-style agents.

Instead of forcing users to list anime titles immediately, it starts with a natural taste interview: mood, genres, favorite traits, watch context, content limits, and examples of shows the user liked or disliked. It then combines that profile with reliable anime metadata sources.

## Highlights

- Conversational intake before asking for exact titles.
- Taste profiling from mood, genre, pacing, character dynamics, watched history, dislikes, and caveats.
- Live metadata guidance using Bangumi, AniList, Jikan/MyAnimeList, and ids.moe.
- Chinese-friendly recommendations with Bangumi as the preferred Chinese-context source.
- Spoiler-safe recommendation output.
- Compatible with Codex, Claude Code, and OpenClaw/Claw-style skill systems that support `SKILL.md`.

## Install

Copy the `anime-recommender` folder into your local skills directory.

For Codex:

```bash
cp -R anime-recommender ~/.codex/skills/
```

Then invoke it with:

```text
Use $anime-recommender to chat with me about my anime taste and recommend what to watch next.
```

## License

MIT-0. Free to use, modify, and redistribute without attribution.
