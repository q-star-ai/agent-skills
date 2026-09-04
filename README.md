# agent-skills

Portable **agent skills** — self-contained capability modules that drop into an
AI agent runtime and give it a new, well-defined job.

Maintained by [Guangzhou Qigu Technology Co., Ltd.](https://www.q-star.ink/) as part of
our work on AI agents, video generation and digital humans.

## What is a skill?

A skill is one directory containing a `SKILL.md`: YAML front matter that declares
the skill's name, version and trigger conditions, followed by Markdown instructions
the agent follows when those conditions match. No build step, no runtime dependency —
the agent reads the file and acquires the behaviour.

This format is compatible with [Claude Code](https://claude.com/claude-code) skills and
with OpenClaw-style agent runtimes.

## Available skills

| Skill | Purpose |
| --- | --- |
| [`qstar-video-ecom`](./qstar-video-ecom) | Generate AI product videos with Chinese TTS voiceover for Chinese e-commerce and social platforms — Taobao, Douyin, Xiaohongshu, Pinduoduo, JD.com and WeChat Channels. Selects aspect ratio and duration per platform, and accepts product images for personalised output. |

## Usage

Copy the skill directory into wherever your agent runtime discovers skills — for
Claude Code that is `~/.claude/skills/` (user-wide) or `.claude/skills/` (per project):

```bash
git clone https://github.com/hubtiger123/agent-skills.git
cp -r agent-skills/qstar-video-ecom ~/.claude/skills/
```

The agent picks the skill up on its next session and invokes it when a request
matches the trigger conditions declared in `SKILL.md`.

## Who this is for

Developers and operators running AI agents for Chinese e-commerce and short-video
marketing, who want reusable, reviewable capability modules rather than prompts
pasted between projects.

## Contributing

Issues and pull requests are welcome. A new skill should be a single directory
with a `SKILL.md` carrying complete front matter (`name`, `version`, `description`,
`tags`) and instructions specific enough to run without further context.

## License

[MIT](./LICENSE) © 2026 Guangzhou Qigu Technology Co., Ltd.
