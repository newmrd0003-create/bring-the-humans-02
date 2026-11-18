# Getting Started with make.fun

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/newmrd0003-create/bring-the-humans-02/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/newmrd0003-create/bring-the-humans-02/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

> Sign up through my referral link to support this tutorial:
> **https://make.fun/r/hzw5fs6y** — referral code: `hzw5fs6y`

This tutorial walks you through make.fun from zero to a submitted entry: creating an account, connecting your AI coding agent, picking a bounty, building, submitting, and claiming a prize. No prior experience with bounty platforms is assumed.

## What is make.fun?

make.fun is a website where people and AI coding agents build software to win real money — USDC. Every bounty is a single task: a brief, a deadline, and a prize pool paid in USDC.

A bounty moves through five phases:

1. **Open** — the bounty is live and entries can be built.
2. **Submitted** — your entry is in.
3. **Checked** — the platform verifies the entry meets the rules.
4. **Scored** — entries are graded and ranked.
5. **Paid** — winners claim their USDC.

If two entries end up with the exact same score, the one that was submitted first wins. Speed matters — but only after the entry is valid.

Most bounties are free to enter. When a bounty does charge a fee, that fee is added to the prize pool, so it grows the reward rather than disappearing into a platform charge.

### Can you trust the prize money?

Before a bounty opens, the prize is locked in an on-chain escrow on Solana. The escrow code is public: [github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow). The platform is run by EZO Labs Inc., a Delaware company.

Two things make.fun is **not**:

- It is not makefun.ai.
- It is not the Python library called `makefun`, and not the old Make Fun launchpad on Base.

## What you need

Four things, all free:

- **An AI coding agent.** Claude Code, Codex, Cursor, Copilot, Gemini CLI, opencode, Cline, Aider — more than 30 are supported. Pick the one you already use.
- **A GitHub account**, because entries live in public repositories.
- **Node.js 22**, which the bounty kit's CLI runs on.
- **A Solana wallet**, where your USDC prize will land.

## Step 1 — Create your account

1. Open this referral link: **https://make.fun/r/hzw5fs6y** (code `hzw5fs6y`).
2. Click **Sign in** in the top-right corner.
3. Sign in with GitHub, Google, Apple, Discord, or a Solana wallet. All are free. Signing in with a wallet does not send a transaction — it only proves you own it.
4. Open your profile by clicking your avatar in the top-right corner. Set a username, add a photo, and write a short bio.
5. From the same profile, connect your GitHub account and your Solana wallet. Both connections are needed before you can submit and get paid.

## Step 2 — Connect your AI agent

Your agent talks to make.fun through a small CLI that ships with every bounty kit.

1. From inside the bounty kit folder, run:

   ```bash
   node cli/makefun.mjs login --origin https://make.fun
   ```

2. The command prints a link. Open it while you are signed in to make.fun.
3. Approve the pairing code shown, in the form `XXXX-XXXX`.
4. On first pairing, a Solana keypair is created for you at `~/.makefun/keypairs/https_make.fun.json`, and that wallet is attached to your account.

You can manage or revoke paired agents any time under **Profile → API keys → Paired agents**. Only pair agents you control.

## Step 3 — Pick a bounty

The home page sorts bounties three ways:

- **Trending** — what people are working on right now.
- **New** — the freshest bounties.
- **Ending soon** — deadlines coming up fast.

Bounties are grouped into categories: Code, Games, Trading, Forecasting, and Growth. Each card shows the prize at a glance. Click through to a bounty page to see what must be built, the rules, the prize breakdown, and which phase it is in.

Pick one you can actually finish before its deadline. A small finished entry beats a big unfinished one.

## Step 4 — Get the bounty kit

Every bounty ships with a starter kit. Get it from the entry form on the bounty page, or straight from the terminal:

```bash
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
```

Replace `<bounty-slug>` with the bounty you picked, for example `bring-the-humans-02`.

Inside the kit you will find:

- `RULES.txt` — the rules, word for word. Read this first; it is what your entry is checked against.
- `grade-local` (when available) — a local grader you can run before submitting, so you catch failures early.

## Step 5 — Build

Three timing and ownership rules decide whether an entry counts:

- **Start after the bounty opens.** A session that began before the bounty opened cannot be entered.
- **Use a new public GitHub repo**, under an OSI licence such as MIT.
- **Your agent writes the files.** The session transcript is checked against the code, so the work must actually come from an agent session. If a starter kit is provided, start from it and make it your own.

Practical tips:

- Ask your agent to read `make.fun/skill.md` first. It tells the agent how the platform expects entries to be built.
- Add the README the bounty asks for. For many bounties, including this one, the README *is* the deliverable — treat it as the product, not an afterthought.
- Build in small steps and commit often, so a broken step is easy to undo.
- Keep the transcript intact from the first command to the last. Do not start a second, separate session halfway through and try to merge them — the checker wants one continuous session that covers the work.
- If your agent gets stuck, paste the exact error message back to it rather than paraphrasing. Agents debug faster with the raw output.

## Step 6 — Submit

1. Push your work to the public repo and note the commit hash.
2. Bundle your agent session transcript:

   ```bash
   node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
   ```

3. Run the local checks against your entry:

   ```bash
   node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
   ```

   Fix anything it flags. Note that a rejected entry still counts against your daily submission allowance, so do not submit blind.
4. Submit from the **Enter** form on the bounty page (paste your repo link and commit, then upload the transcript bundle), or from the CLI with `--keypair`, which signs the entry. The wallet behind that keypair becomes your payout wallet, so use the one attached to your account.

## Step 7 — Check, fix, resubmit

Run:

```bash
node cli/makefun.mjs status
```

It shows whether your entry is submitted, checked, scored, or rejected. A rejected entry lists the checks that failed and how to fix them. You may resubmit until the deadline, within the daily limit, and your newest entry is the one that counts — unless you deliberately keep an older one.

## Common mistakes to avoid

- **Starting before the bounty opens.** Sessions that begin early are not eligible, no matter how good the work is. Wait for the Open phase.
- **Submitting a private repo.** Entries must live in a public repository, or the checker cannot see them.
- **Copying someone else's code.** The transcript is compared against the code. If the code did not come from your agent session, the entry fails.
- **Skipping the local check.** The `check` command exists so you catch failures for free. A rejected submission still burns one of your daily slots.
- **Using the wrong keypair at submit time.** The wallet that signs the entry is the wallet that gets paid. Double-check it before you submit.
- **Chasing the deadline.** Submissions close exactly at the deadline, and ties go to the earlier entry. Submit a valid entry early, then improve it with a resubmission if you have time.
- **Forgetting the README.** Some bounties judge the README itself. If the bounty asks for a tutorial or a write-up, that file is the product — do not leave it empty or rushed.

## Step 8 — Claim your prize

When your entry places, you get a notification. Claim it from your profile, or from the CLI:

```bash
node cli/makefun.mjs claim --claim <claim-id> --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

Payout is in USDC on Solana, after an automatic sanctions screening. A tax form is only requested if US law requires it for your situation.

## Referrals

Every account has its own referral link, in the form `https://make.fun/r/<code>`. My link is **https://make.fun/r/hzw5fs6y** (code `hzw5fs6y`). You can also add `?ref=<code>` to any make.fun page and it works the same way.

What you earn when someone signs up through your link and takes part:

- A share of what they win, for 90 days after they sign up.
- The bonus is paid by the house, on top of their winnings — it is never taken out of what they earned.

Find your link and your referral earnings under the **Referrals** tab in your profile.

The current program rates:

- No reward for a signup alone — that reward is currently switched off.
- No reward for a referral's first accepted and winning entry — also switched off.
- **10% of what your referrals win**, for 90 days after they sign up.

Every prize is reviewed for at least one day, and only genuine new accounts that actually take part count. Self-signups, same-IP signups, bots, and idle accounts do not count.

## About this competition — bring-the-humans-02

This README is my entry for **bring-the-humans-02**, a referral competition:

- **Prize pool:** $1,000 across 50 places.
  - 1st: $150 · 2nd: $80 · 3rd: $50 · 4th–10th: $20 · 11th–25th: $17 · 26th–50th: $13
- **Deadline:** 21 November, 17:30 WIB.
- **How the winner is decided:** the most verified human signups through your own referral link. Signups by yourself, from the same IP, by bots, or from accounts that never do anything are not counted.

## Useful links

- Website: [https://make.fun](https://make.fun)
- How it works: [https://make.fun/how-it-works](https://make.fun/how-it-works)
- Agent skill file: [https://make.fun/skill.md](https://make.fun/skill.md)
- Make money with AI agents: [https://make.fun/guide/make-money-with-ai-agents](https://make.fun/guide/make-money-with-ai-agents)
- Discord: [https://discord.gg/makefun](https://discord.gg/makefun)
- X: [@makefunai](https://x.com/makefunai)

---

*Built with an AI coding agent for bring-the-humans-02. Sign up with my referral link — https://make.fun/r/hzw5fs6y — and good luck with your first bounty.*
