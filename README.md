# feiyun_architect

**[English](#english) | [中文](#中文)**

A Claude Code / Codex skill that auto-selects the right "automation architecture" (plain task / `/goal` / `/loop` / `/schedule` / workflow), asks what it needs to know, and hands you a plain-language plan with copy-pasteable commands — you approve before anything runs.

一个 Claude Code / Codex 通用 skill：自动判断该用哪种"自动化架构"，问清楚必要信息，给出大白话的执行计划和可复制粘贴的命令，确认后再执行。

---

## English

Inspired by the Loop Engineering concept from Claude Code's official article *"Getting started with loops"*: turning "an agent repeating cycles of work until a stop condition is met" into a reusable skill you can trigger with one sentence.

### What problem this solves

Most people using AI coding/office tools are still stuck prompting one step at a time — watching, re-asking, repeating themselves every turn. This skill hands the "how should this automation be organized" decision to the AI:

- You say "set up a loop that does XXX"
- It figures out which architecture fits, and asks follow-up questions if it's not sure yet (keeps asking until it's confident)
- It gives you a clear plan plus a ready-to-paste command
- **Then it stops and waits for your go-ahead** — nothing runs until you confirm

### Prerequisites

You need [Claude Code](https://claude.com/claude-code) (or Codex) already installed, with an active subscription/login. This repo is just a "skill" — an instruction file — not a standalone app. If you've never used Claude Code before, install and open it first, then come back here.

### Installation

**If you're comfortable with a terminal:**

```bash
git clone https://github.com/FeiYun-Novel/feiyun_architect.git
cp -r feiyun_architect/feiyun_architect ~/.claude/skills/   # Claude Code
cp -r feiyun_architect/feiyun_architect ~/.codex/skills/    # Codex (optional, only if you use Codex too)
```

(Windows/PowerShell: replace `cp -r` with `Copy-Item -Recurse`, and `~/.claude/skills/` with `$env:USERPROFILE\.claude\skills\`.)

**If you're not — no terminal needed:**

1. On this GitHub page, click the green **Code** button → **Download ZIP**, and unzip it
2. Open your file manager (Finder on Mac / Explorer on Windows) and go to your home folder
3. Find (or create) a folder named `.claude/skills` (on Mac, press `Cmd+Shift+.` in Finder to see hidden folders starting with a dot)
4. Drag the `feiyun_architect` folder (the one containing `SKILL.md`) into `.claude/skills`
5. Restart Claude Code / start a new conversation

**Using it**: just say "set up a loop that does XXX" (or in Chinese, "帮我建个 loop：XXX") in a conversation, or type "/feiyun_architect XXX". No need to memorize any command — plain language works.

### What it actually looks like (example)

```
You:    set up a loop that rewrites this paragraph until it stops sounding like AI wrote it, max 5 tries
Claude: (asks 1-2 quick questions if needed, e.g. "where should the result go?")
        Here's my plan: I'll use /goal, rewrite → self-check → repeat, stop when clean or after 5 rounds.
        Model: Sonnet, effort: medium (cheap enough for text edits).
        Boundaries: only touches this text, no other files, nothing gets published automatically.
        Want me to run it? (yes / just show me the plan / no)
You:    yes
Claude: (runs 2-3 rounds, shows you each draft + self-check result, stops when done)
```

### Files

- `SKILL.md` — the core flow: ask → select architecture → deliver a plan → confirmation gate → execute + log
- `template.md` — an 8-field task card template; every run gets logged as a card so you can say "run that one again"

### Read before you use it: real pros and cons

**Pros:**
1. You don't need to know what `/goal`, `/loop`, `/schedule`, or workflow mean — the AI decides which one fits
2. A confirmation gate — before anything runs, it lists what will be touched, what it'll cost, and how to undo it; you approve first
3. Built-in token-saving logic — routine tasks get routed to cheaper models / lower effort levels
4. Self-improving — lessons learned from real runs get written back into `SKILL.md` so the same mistake isn't repeated

**Caveats and limitations (judge for yourself whether this fits your workflow):**
1. `/goal`, `/loop`, `/schedule`, and workflow are **Claude Code-specific commands**; in other environments like Codex, this skill can only produce the plan, not execute those commands directly
2. **The AI grades its own "done" criteria** — that's not the same as objective fact. You're still the final judge
3. The AI may invent details to make output sound more "authentic" (e.g. fabricating a personal anecdote while writing a script for you) — always fact-check anything that goes out under your name
4. Complex tasks have a slower question phase (it needs to actually understand the task, sometimes via read-only probing first) — that's the cost of being careful
5. The "safety defaults" section in `SKILL.md` intentionally leaves placeholder notes (like "replace this line with your own boundaries") — **that's a spot for you to customize, not something to copy verbatim from the original author's setup**
6. However thorough the confirmation gate is, it's meaningless if you approve without reading it — responsibility always stays with the user

One-line summary: it lowers the bar for "getting an AI to run automation" down to one sentence — but whether to let it act, and whether to trust its results, is still on you.

---

## 中文

灵感来自 Claude Code 官方文章《Getting started with loops》里的 Loop Engineering 概念：把「AI 反复干活直到满足停止条件」这套方法论，做成一句话就能触发的可复用 skill。

### 这个 skill 解决什么问题

用惯 AI 编程/办公工具的人，大多还停留在「一句一句提示」的阶段——每次都要盯着、追问、复述需求。这个 skill 把「怎么组织一次自动化任务」的判断交给 AI：

- 你说「帮我建个 loop：XXX」
- 它自己判断这事需要哪种架构，信息不够就问（问到有把握才罢休）
- 给你一份说明白的执行计划 + 可以直接复制粘贴的命令
- **停下来等你点头**，你确认了才真正执行

### 前置条件

你得先装好 [Claude Code](https://claude.com/claude-code)（或 Codex），并且已经登录、有可用额度。这个仓库只是一份"技能说明文件"，不是独立的软件——如果你从没用过 Claude Code，先去装好、打开能正常对话，再回来做下面这步。

### 怎么安装

**如果你会用终端：**

```bash
git clone https://github.com/FeiYun-Novel/feiyun_architect.git
cp -r feiyun_architect/feiyun_architect ~/.claude/skills/   # Claude Code
cp -r feiyun_architect/feiyun_architect ~/.codex/skills/    # Codex（如果你也用 Codex 才需要）
```

（Windows/PowerShell 用户：把 `cp -r` 换成 `Copy-Item -Recurse`，把 `~/.claude/skills/` 换成 `$env:USERPROFILE\.claude\skills\`）

**如果你不会用终端——完全不需要打命令：**

1. 在本页面点绿色的 **Code** 按钮 → **Download ZIP**，下载后解压
2. 打开你电脑的文件管理器（Mac 是访达 Finder，Windows 是文件资源管理器），进入你的用户主目录
3. 找到（或新建）一个叫 `.claude/skills` 的文件夹（Mac 上在访达按 `Cmd+Shift+.` 可以看到以点开头的隐藏文件夹）
4. 把 `feiyun_architect` 这个文件夹（里面装着 `SKILL.md` 那个）拖进 `.claude/skills` 里
5. 重启 Claude Code，或者开一个新对话

**怎么用**：在对话里直接说「帮我建个 loop：XXX」，或者输入「/feiyun_architect XXX」，都会自动触发——不用背命令，说人话就行。

### 实际长什么样（示例）

```
你：       帮我建个 loop：把这段话改到不像 AI 写的为止，最多改 5 次
Claude：   （需要的话先问一两句，比如"结果放哪给你看"）
           我的方案：用 /goal，改写→自查→再改，查干净了或者改满5轮就停。
           模型用 Sonnet，档位 medium（改文字这种活用不着更贵的）。
           边界：只碰这段文字，不动别的文件，不会自动发布到任何地方。
           要不要现在执行？（要 / 先只看方案 / 不要）
你：       要
Claude：   （跑 2-3 轮，每轮都给你看草稿和自查结果，改好就停）
```

### 文件说明

- `SKILL.md`——核心流程：提问 → 选型 → 交付方案 → 确认关卡 → 执行 + 存档
- `template.md`——任务卡片模板（八字段），每次跑起来的任务会存一张卡片，方便"上次那个再跑一次"

### 使用前必读：这个 skill 的真实优缺点

**优点：**
1. 不用你懂 `/goal`、`/loop`、`/schedule`、workflow 是什么，AI 自己判断该用哪个
2. 有确认关卡——执行前会把要动什么、花多少、怎么反悔一次列全，你点头才动
3. 内置省 token 策略——机械性任务会建议用便宜模型/低 effort 档位
4. 会自我进化——用出来的坑，规则会写进 SKILL.md 里避免重犯

**注意事项与局限（请自行判断是否适合你）：**
1. `/goal`、`/loop`、`/schedule`、workflow 是 **Claude Code 专属命令**；在 Codex 等其他环境里，这个 skill 只能帮你出方案，不能直接执行这些命令
2. **AI 自查的"达标"是它自己打的分**，不是客观事实——最终裁判应该是你自己
3. AI 有可能为了让结果看起来更"真实"而编造细节（比如帮你写口播稿时编个不存在的个人经历）——凡是以你的名义对外的内容，发布前务必核实
4. 复杂任务的提问阶段会比较慢（要问清楚、可能要先做只读侦查），这是"稳"的代价
5. `SKILL.md` 里的"安全默认值"部分保留了几个占位提示（如"把这一行改成你自己的禁区清单"）——**这是给你自定义的位置，不是要照抄原作者的配置**
6. 确认关卡列得再全，如果你不看内容就点头，这层保护形同虚设——责任始终在使用者手上

一句话总结：它把"怎么让 AI 自动干活"的门槛降到一句话，但"让不让它动手、信不信它的结果"，责任还在你自己手里。

---

## License

MIT
