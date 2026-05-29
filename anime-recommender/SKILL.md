---
name: anime-recommender
description: Recommend anime, anime series, seasonal anime, movies, or watchlists from a user's past viewing history, ratings, favorites, disliked works, mood, genre, platform, length, content limits, or "what should I watch next" requests. Use for Chinese or English anime recommendation requests, especially when the user wants recommendations based on previously watched anime, similar works, current/seasonal shows, Bangumi/MyAnimeList/AniList/Kitsu data, ratings, completion status, airing status, or spoiler-safe watch guidance.
---

# Anime Recommender

## Goal

Recommend anime from the user's actual taste profile, not from generic popularity. Use structured preference gathering, live data when needed, and concise reasoning that explains why each title fits.

## Default Workflow

1. Start with a conversational entry when the user's taste profile is not yet clear.
2. Build a taste profile from the user's described moods, genres, favorite traits, watched list, favorites, dropped shows, ratings, and stated preferences.
3. Identify constraints: mood, genre, era, length, completion status, language/title preference, platform, tolerance for content, and whether ongoing shows are acceptable.
4. Search or verify current metadata when recommendations depend on seasonal status, ratings, popularity, streaming availability, release dates, or uncertain facts.
5. Deduplicate candidates across sources and avoid recommending titles the user has already watched unless explicitly asked for rewatch/order advice.
6. Rank candidates by taste fit first, then confidence, viewing cost, popularity/score reliability, and novelty.
7. Present recommendations with reasons, caveats, and the next step for collecting better preferences.

## Conversation Entry

When the user wants recommendations but has not provided enough context, do not open with "list the anime you watched." Start like a friendly taste interview and let the user choose how to answer.

Use a short entry like:

```text
可以，我们先不用急着报片名。你可以从这几个角度随便说一点：

1. 最近想看的感觉：轻松、热血、治愈、悬疑、恋爱、科幻、胃痛、爽片、慢节奏都行。
2. 喜欢的类型或元素：校园、奇幻、群像、音乐、运动、智斗、日常、成长、强剧情等。
3. 看过之后觉得很合口味/不合口味的作品，如果想不起来片名，说“像那种...”也可以。
4. 雷点：后宫、卖肉、党争、血腥、烂尾、未完结、太长等。
```

Then continue based on the user's answer:

- If they describe mood/type only, infer a provisional taste profile and ask for one optional calibration signal: "有没有一两部你觉得接近这种感觉的？想不起来也没关系。"
- If they name works, ask what they liked or disliked about them instead of treating titles as enough.
- If they provide a long watched list, classify it into likely taste dimensions and confirm the top 2-4 signals before recommending.
- If they hesitate, offer sample choices rather than requiring recall.

## Intake Strategy

If the user gives enough context, do not ask follow-up questions first; recommend directly and state assumptions.

Ask at most 3 short questions only when the request is too broad. Prefer questions that can be answered without remembering exact titles:

- "这次想看什么状态：轻松下饭、剧情强、恋爱、科幻、治愈、悬疑、补经典、本季新番？"
- "你更在意什么：角色关系、剧情反转、世界观、氛围、作画、音乐、爽感、情绪后劲？"
- "有没有明确不想看的雷点，比如后宫、党争、胃痛、血腥、未完结、长篇？"
- "如果想得起来，有没有 1-3 部你很喜欢或很不喜欢的？想不起来也可以先不填。"

When the user wants recommendations from past viewing history, encourage structured input only after the conversational entry. Accept messy text, partial memories, genres, vibes, character types, and "像某某但不要某某" descriptions. Useful optional formats:

```text
喜欢/高分：葬送的芙莉莲 9，孤独摇滚 9，钢之炼金术师FA 10
一般：鬼灭之刃 7，咒术回战 7
不喜欢/弃番：租借女友，盾勇
雷点：后宫、无意义卖肉、烂尾
想要：近 5 年，已完结，12-28 集
```

Never make exact titles mandatory unless the task specifically depends on deduplicating the user's watched list. If title recall is weak, recommend a small exploratory set and explain that future feedback will tune the profile.

## Data Sources

Read `references/data-sources.md` when current metadata, API behavior, ID mapping, or source selection matters.

Default source order:

1. Bangumi for Chinese titles, Chinese-community score/context, calendar, subject details, and Chinese user expectations.
2. AniList for rich tags, relations, format/status/season/year metadata, and flexible GraphQL candidate searches.
3. Jikan for MyAnimeList score, member count, rankings, season lists, and quick unauthenticated MAL-derived checks.
4. ids.moe for cross-source ID alignment when merging Bangumi, AniList, MAL, Kitsu, or Simkl results.
5. Kitsu or Simkl as optional fallback sources for relations, streaming links, or watch tracking contexts.

Use live lookup for:

- current/latest/this-season/new-season recommendations
- airing, completion, sequel, or movie release status
- scores, rankings, member counts, popularity, and streaming availability
- claims where hallucinating a title, season, or watch order would be costly

If browsing or API access is unavailable, state that metadata was not verified live and avoid pretending certainty.

## Ranking Heuristics

Prefer candidates that match multiple taste signals:

- Similar themes, emotional texture, pacing, narrative structure, and character dynamics to the user's favorites.
- Avoid traits present in dropped/disliked shows.
- Enough score/member data to reduce one-off rating noise.
- Complete or short enough when the user implies low commitment.
- Related works by the same studio, director, writer, composer, or source genre only when the match is substantive.

Do not overfit to surface genre. For example, "喜欢《葬送的芙莉莲》" may imply quiet pacing, after-journey melancholy, strong atmosphere, and character growth rather than simply "fantasy".

## Output Format

Use Chinese by default when the user writes in Chinese. Keep spoilers out unless requested.

For normal recommendations, provide 5-8 titles:

```markdown
**最推荐**
1. 《标题》 - 年份，集数/状态
   推荐理由：...
   可能雷点：...
   适合现在看的原因：...

**备选**
...

**我需要你补充的信息**
...
```

For each title include:

- title, year, format/episode count if known
- one concrete taste-match reason
- one caveat or "可能雷点"
- confidence when the fit is uncertain

When using live sources, mention source names briefly, especially if data differs across sources. Do not drown the user in scores; use scores as supporting evidence, not the recommendation itself.

## Special Cases

For watch-order questions, verify relations and release chronology before answering.

For "像 X 的动画", ask what aspect of X they liked only if ambiguous; otherwise give a split such as "氛围像 / 题材像 / 角色关系像".

For adult, violent, depressing, or controversial content, label caveats plainly and avoid graphic detail.

For platform-specific recommendations, verify availability live because streaming catalogs change often.
