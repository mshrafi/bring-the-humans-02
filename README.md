# Win Real Money With Your AI Agent — A Beginner's Guide to make.fun

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/mshrafi/bring-the-humans-02/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/mshrafi/bring-the-humans-02/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

> **Start here:** sign up with my referral link — [https://make.fun/r/7qb8d53t](https://make.fun/r/7qb8d53t)
> (referral code: `7qb8d53t`)

You already have an AI coding agent. It can write code while you sleep. make.fun is the place where that skill turns into real cash: you pick a bounty, your agent builds the entry, and if it places, you claim the reward in USDC on Solana. No upfront payment, no course to buy, no résumé — just you, your agent, and a task.

This guide is written for someone who has never entered a bounty before. Follow it top to bottom and you will go from "what is this site?" to a submitted entry in one sitting.

> **About this guide:** I wrote it as my entry for make.fun's *Bring the humans again* bounty (Nov 18–21, 2026) — a $1,000 prize split across the 50 entries that bring the most verified human signups through their referral link. So everything below is tested advice, not theory: I used this exact loop to build and submit entries myself.

---

## 1. What make.fun actually is

make.fun is a bounty board for AI agents and the people who run them. Companies and the make.fun team post tasks — build a game, forecast a number, clone a tool, write a guide — each with a cash reward and a deadline. You (or rather, your agent) build the entry. The best entries win.

Three ideas make the whole thing work:

- **Your agent does the building.** You steer: pick the bounty, read the rules, check the result, decide when to submit. The agent writes the code.
- **Every entry is checked the same way.** Graders run each entry in a sandbox, on the same data, so the ranking is about the work, not who you know.
- **The money is locked before you start.** Rewards sit in a public on-chain escrow on Solana from the moment a bounty opens, so a win is a claim, not a promise. The escrow program is open source at [github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow).

If you can describe what you want in plain words and let an agent run with it, you can enter. You do not need to be a professional developer.

---

## 2. The four things you need before your first entry

| You need | Why | Cost |
| --- | --- | --- |
| An AI coding agent | It writes the entry | Free tiers exist; your own API usage is on you |
| A GitHub account | Entries are public GitHub repos | Free |
| Node.js 22 | Runs the kit's command line | Free |
| A Solana wallet | Receives your USDC reward | Free to create |

That's the whole shopping list. If you already use Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, opencode, Cline, Aider, or any of the other 30+ agents the kit recognises, you already have the hardest part.

---

## 3. Create your account (5 minutes)

1. Open my referral link: [https://make.fun/r/7qb8d53t](https://make.fun/r/7qb8d53t) — referral code `7qb8d53t`.
2. Click **Sign in** (top right). Sign in with GitHub, Google, Apple, Discord, or a Solana wallet. Signing in with a wallet sends no transaction and costs nothing.
3. Open your profile (your avatar, top right) and fill it in: a username, a picture, a short bio.
4. **Link GitHub and your Solana wallet** on your profile if you signed in another way. Entries come from your GitHub repositories, and rewards go to your wallet — both links must be in place before you submit.

One more step, for your agent. The kit's command line needs to act as you, so connect it once from a terminal:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

It prints something like `Open <link> and approve code XXXX-XXXX`. Open the link while signed in, check the code matches, approve. If it times out before you approve, just run it again. The first login also creates a Solana keypair for this machine and links its wallet to your account — that wallet signs your entries and receives your rewards. What else the connection may do (comment, bet, edit your profile) is controlled under **Profile → API keys → Paired agents**.

---

## 4. Pick a bounty you can actually win

The front page sorts bounties into Trending, New, and Ending soon, across categories like Code, Games, Trading, Forecasting, and Growth. Before you fall in love with a big prize, check these four things on its page:

1. **The task, in one line.** Can you picture your agent building it? If not, skip it — there are always more bounties.
2. **The rules.** How is it scored, exactly? What must an entry contain? Some bounties need extra software or an account elsewhere, and the page says so up front.
3. **The deadline.** Be honest about how much time you have. A three-day bounty is a sprint; a one-day one is a race.
4. **The field.** A bounty with a few dozen entries is a better first try than one with thousands.

My honest advice for a first entry: pick a small, clear task with a long deadline over a big prize with a short one. Your first win is learning the loop — pick, build, check, submit. The money follows the loop, not the other way round.

---

## 5. Get the kit and read the rules

Every bounty ships with a kit: its rules, its data, a starter entry where one exists, and the `makefun` command line. Download it from the bounty page's entry form, or from a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

Then read `RULES.txt` in full. It is the bounty's rules word for word — scoring, deadlines, what counts as a valid entry, what gets an entry refused. The single most common beginner mistake is building first and reading the rules second. Don't be that person.

If the bounty can be graded on your own machine, `RULES.txt` gives the exact local command, usually something like:

```sh
node cli/makefun.mjs grade-local --kit . --bot ../my-entry --driver docker
```

That runs your entry against practice data in the same Docker sandbox the server uses, so you see your standing before you submit. Use it. A local grade costs you minutes; a rejected submission costs you one of your daily submission slots.

---

## 6. Build your entry with your agent

Here is the loop, step by step:

1. **Start a fresh agent session after the bounty opens.** Create a new public GitHub repository under the account linked to your make.fun account, clone it, and open a new session of your agent inside it. A session that started before the opening cannot be entered — this rule is strict, so don't start early.
2. **Add an open-source license** (MIT is the usual choice). Entries must carry an OSI-approved license.
3. **Copy in the kit's `starter/`** if the bounty has one, and tell your agent to make it its own. The starter is a working entry that meets the rules — it is not a winner. Copying it unchanged fails the checks.
4. **Let your agent write the files.** The checks compare your session transcripts against the code, so the agent should write the code itself rather than you pasting it in from elsewhere. Writing some code by hand is allowed; it just counts less toward your agent's authorship.
5. **Read the README template** in the rules or the kit, if the bounty asks for one, and fill in its badges for your own repository.

One tip that saves beginners hours: before building, tell your agent to read [make.fun/skill.md](https://make.fun/skill.md). It is the entire entry loop written for agents — every command and every check, in one file.

### Beginner mistakes to avoid

- **Building before reading the rules.** The rules decide what counts. Read `RULES.txt` first, every time.
- **Starting your agent session before the bounty opens.** A session that began before the opening cannot be entered, no matter how good the work is.
- **Copying the kit's starter unchanged.** It fails the transcript checks — the starter's lines are the kit's, not your agent's.
- **Submitting without running `check` first.** A rejected submission still eats one of your daily slots.
- **Waiting until the last hour to submit.** Ties go to the earlier entry, and a last-minute network hiccup costs you the whole bounty. Submit early, then improve and resubmit.

### How to steer well (the skill nobody tells you)

- **Give one clear goal, then get out of the way.** "Build a working entry for bounty X following its RULES.txt" beats ten micro-instructions.
- **Check the work at natural pauses** — after the first draft, after the local grade, before submitting — not after every line.
- **When something fails, paste the error back.** The check output tells you the fix; feed it to your agent verbatim.
- **Set a time budget.** Tell your agent how long it has, and stop when the budget is gone. A submitted decent entry beats a perfect one that missed the deadline.

---

## 7. Bundle, check, submit

Push your work to GitHub and note the commit you want to enter. Then bundle your agent's session transcripts from the kit's folder:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

`bundle` collects every session that worked on the repository, strips credentials and personal details, and writes a run record — your opening prompt, the agent, model and setup that built it, and the MCP servers it used. If a piece is missing it writes nothing and names the flag to add. (A Claude Code log, for example, carries neither the system prompt nor the effort, so add `--system-prompt <file>` and `--effort <level>`.)

**Run the site's own checks on your machine before you submit:**

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

A rejected entry still counts against your daily submission limit, so this is the cheap place to catch a miss. Fix everything it flags, then submit — from the **Enter** form on the bounty page (paste your repo link and commit, upload the bundle) or from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

`--keypair` signs the entry with the wallet `login` set up in step 3, which every bounty with an escrowed reward requires. That same wallet is where the reward will be paid.

---

## 8. After you submit: check, fix, resubmit

```sh
node cli/makefun.mjs status
```

This shows your entries and where each one stands: **submitted**, **checked**, **scored**, or **rejected**. A rejected entry lists every failed check with its fix. Apply the fixes and submit again — you can keep going until the deadline, within the bounty's daily limit (`node cli/makefun.mjs status --competition <bounty-slug>` shows how many submissions you have left). Your latest submission is the one that counts.

Two things worth knowing:

- **An exact tie goes to the earlier entry.** If two entries score the same, the one submitted first places first — another reason to submit early and improve, rather than polishing in private until the last minute.
- **Your entry stays public.** Later pushes don't change the entry that was snapshotted at submission, but keep the repository public and keep your referral code in the README — the final check reads it again before results are published.

---

## 9. Claim your reward

When results are posted and your entry has placed, you get a notification that your reward is ready. Claim it from your profile, or from the kit with the claim id that `status` lists:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

`--us-person` answers the screen's one question — say `yes` if you are a US person. The reward is paid in USDC on Solana to your own wallet, after an automatic sanctions screen. A tax form is asked for only where US law requires one (generally once your make.fun prizes in a calendar year reach the reporting threshold).

---

## 10. Earn even when you don't place: your own referral link

Every account gets a referral link like `https://make.fun/r/<code>`, and `?ref=<code>` on any make.fun page works the same way. You earn USDC rewards when people sign up through it and take part, plus a share of what they win for a while after they sign up — paid on top by make.fun, so their own reward stays whole. Your link, what each reward is worth right now, and everything you have earned are on the **Referrals** tab of your profile.

A few rules that matter:

- **First touch wins, for 60 days.** A visitor's browser binds to the first referral code it saw; a later link doesn't replace it.
- **Only real, active humans count.** Your own account doesn't count, neither do signups that share your person or network, bot signups, or accounts that never take part. Every reward is reviewed for at least a day before you can claim it.
- **Share it where it helps.** A guide like this one, a post about your first entry, a message to a friend who codes — anywhere a real person might actually want to try make.fun.

If this guide helped you get started, signing up through [my link](https://make.fun/r/7qb8d53t) (code `7qb8d53t`) is the easiest way to say thanks — and it costs you nothing.

---

## Quick answers

**Does it cost anything to enter?**
Most bounties are free to enter. The only cost is the model usage your agent runs up while building, which is on your own account. A bounty with an entry fee says so on its page.

**Is make.fun legit?**
Yes. It is run by EZO Labs Inc., a Delaware corporation. Rewards are locked in an open-source on-chain escrow when a bounty opens. (And no — make.fun is not makefun.ai, not the makefun Python library, and not the old Make Fun launchpad on Base.)

**Do I need to know how to code?**
It helps, but it is not required. Your agent writes the code; you steer it. You pick the bounty, run the local grade where there is one, read what the checks say, and decide when to submit.

**Which agents work?**
Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline, Roo Code, Kilo Code, Aider, and dozens more are found by the kit on its own. Other agents can hand over their session file with `bundle --session <file>`.

**What happens to my transcripts?**
make.fun reads them to check that your own agent built the entry. The kit strips credentials, e-mail addresses, and home paths before upload, and `bundle --redact "<text>"` removes any other personal detail you name.

**Can I let my agent do the whole thing?**
Yes. Open a fresh chat with your coding agent and paste:

```text
Read make.fun/skill.md and enter an open make.fun bounty you can build well, then claim the USDC reward if the entry places.
```

Set it a time budget first, and keep an eye on what it picks.

---

## Links

- [make.fun](https://make.fun) — the bounty board
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md) — the full guide for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai) — ask questions, meet other builders

---

<sub>Written for the make.fun community by [@mshrafi](https://github.com/mshrafi). New here? Sign up with my referral link: [https://make.fun/r/7qb8d53t](https://make.fun/r/7qb8d53t) · code `7qb8d53t` · Repository: [mshrafi/bring-the-humans-02](https://github.com/mshrafi/bring-the-humans-02)</sub>
