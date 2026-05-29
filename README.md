# 番剧推荐 Skill

[English README](./README.en.md)

一个面向 Codex、Claude Code、OpenClaw/Claw 类 Agent 的番剧推荐 skill。

它不是让 AI 生硬地问你“看过哪些番”，而是先和你聊口味：最近想看的感觉、喜欢的类型、雷点、看番场景、曾经合口味或不合口味的作品。然后再结合可靠的番剧数据源，给出更像“懂你”的推荐。

## 适用场景

- 想找下一部番，但不想自己翻榜单。
- 想基于以前看过/喜欢/弃掉的动画做推荐。
- 想找“像某部作品的氛围”，但不只是同题材替代品。
- 想补经典、新番、本季番、短篇、已完结作品。
- 想提前避雷后宫、卖肉、党争、血腥、烂尾、未完结、长篇等。

## 特点

- 自然入口：先聊口味，不强迫用户立刻列片名。
- 个性化画像：综合情绪、题材、角色关系、节奏、雷点和观看成本。
- 可靠数据源：优先使用 Bangumi、AniList、Jikan/MyAnimeList、ids.moe 等成熟 API/数据库做信息核验和补充。
- 中文友好：中文用户优先参考 Bangumi 的中文标题、评分、收藏和社区语境。
- 防剧透输出：推荐理由讲清楚，但默认不展开关键剧情。
- 多 Agent 可用：Codex、Claude Code、OpenClaw/Claw 类工具都可以把它作为本地 skill 使用。

## 安装

把 `anime-recommender` 文件夹复制到你的本地 skills 目录。

Codex 示例：

```bash
cp -R anime-recommender ~/.codex/skills/
```

其他 Claw/OpenClaw 类 Agent 或 Claude Code 环境中，请复制到对应的 skills 目录；只要支持 `SKILL.md` 风格的 skill 发现机制即可使用。

## 使用方式

推荐用自然语言启动：

```text
用 $anime-recommender 帮我找点新番看，你先和我聊聊我的动画口味。
```

也可以直接给偏好：

```text
用 $anime-recommender。最近想看轻松但有点情绪后劲的动画，不想看后宫和卖肉。
```

或者给观看历史：

```text
用 $anime-recommender。喜欢《葬送的芙莉莲》《孤独摇滚》《钢之炼金术师FA》，不太喜欢套路后宫，想看已完结、集数别太长的作品。
```

## 数据源策略

这个 skill 会指导 Agent 在需要实时信息时优先核验：

- Bangumi：中文标题、中文社区评分、收藏、放送信息。
- AniList：题材标签、关联作品、状态、季度和年份。
- Jikan/MyAnimeList：MAL 评分、人气、排行、季度番信息。
- ids.moe：跨 Bangumi、AniList、MAL、Kitsu、Simkl 等平台做 ID 对齐。

评分只作为辅助依据，不会简单按分数排序。推荐会优先考虑你的口味匹配度、雷点、观看成本和作品状态。

## 许可证

MIT-0。可以自由使用、修改和再分发，无需署名。
