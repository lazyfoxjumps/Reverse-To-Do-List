# Reverse To-Do List

A Claude Code skill for ADHD brains that lie to you.

## What this is, plainly

Regular to-do lists are a war crime against the ADHD nervous system. You stare at a list of unfinished shit, your brain reads "I haven't done X, Y, Z" as "I'm a failure," and now you're paralyzed in front of a 14-item list that was supposed to help you. Cool. Very productive.

Reverse To-Do flips it. You don't write down what you're going to do. You write down what you **actually did**, after you did it. Every small thing. Brushing your teeth on a depression day. Answering one text you'd been avoiding for a week. Staring at the ceiling for 20 minutes thinking about whether to apply to funeral director school (real example, no judgment).

Each thing you log gets a score from 0 to 100. A "full day" of human output is 100 points. So when your brain tells you at 9pm that you "didn't do anything today," you pull up the file and the file says 147, and now your brain has to argue with math instead of with you.

That's the whole skill. Receipts against the lie.

## Who this is for

People with ADHD. Specifically:

- People who delete their wins from memory the second they happen
- People who think "rest" is something other people get to have
- People who do six invisible-labor things before noon and then feel like they "haven't started the day"
- People whose brains have been telling them they're lazy since they were 12
- People who need proof, not pep talks

If you're a neurotypical person who already feels good about your output, this skill is not for you. You don't need it. Go enjoy your functional dopamine system, weirdo.

## The 6 categories

Everything you log goes in exactly one of these:

1. **Small Tasks.** Errands, replies, bills, dishes. The visible-productivity stuff.
2. **Self-Care.** Brushing teeth, eating real food, meds, therapy, showers. The bar is on the floor and it counts.
3. **Emotional Stuffs.** Hard conversations. Holding space. Masking through events. Sitting with feelings. The work no one can see. The work that costs the most.
4. **Big Brain Hours.** Focused thinking, deep work, hard decisions, learning. "Staring at the ceiling" goes here if your brain was actually working.
5. **Creative Time.** You made something. Doesn't matter if it's good. Doesn't matter if it shipped. You made it. It counts.
6. **Rest.** Active recovery. Deliberate downtime. Watching a show you actually like. This is OUTPUT, not absence of output.

## The three modes

### `log` (the default)

You tell me what you did. I categorize it, score it, write it down. You get a one-line confirmation in best-friend voice. That's it. No lecture. No "great job!" No productivity-bro garbage.

```
You: brushed teeth, took meds, finally answered Avi
Me: Logged. The Avi one had been sitting there for a week, didn't it. Got it at 28 total.
```

### `recap`

End of the day. I read back everything you did, total your score, and write a recap. Tone shifts based on the number:

- **Under 50:** gentle. Names what you did on a hard day.
- **50-99:** warm. Solid day, here's what was in it.
- **100-149:** blunt. "You hit X. Your brain is going to discount it. Don't let it."
- **150+:** louder. "X?? Sit down."

The recap gets saved to the file. If you're spiraling later that week, you can pull it back up.

### `review`

Weekly or monthly pattern detection. Not generic stats. Specific stuff like:

> "Your Mondays are consistently the highest-scoring day this week (avg 132) but Tuesdays drop to 41. You're cooking yourself on Monday and crashing the next day."

> "60% of your points this week came from Emotional Stuffs. That's not a normal distribution. Something hard is going on, or you're the designated feelings-holder for someone right now. Both are real, both are expensive."

The stuff your brain would never notice on its own.

## Where your data lives

Three places, kept in sync:

1. **Local markdown** at `~/reverse-todo/YYYY/MM/YYYY-MM-DD.md`. This is the source of truth. Plain text, greppable, portable, yours.
2. **Obsidian vault** at `~/Documents/Obsidian Vault/Reverse To-Do/`. Same files, with tags wired up so you can build dashboards if you want.
3. **Notion database** called "Reverse To-Do List." One page per day, properties for date / score / category breakdown / has-recap. Queryable. The first time you log, the skill asks where in your Notion you want it to live, then sets it up.

Local always wins. If Obsidian or Notion is down or unreachable, you still log. Nothing about this is fragile.

## Install

1. Clone this repo into your Claude Code skills folder:

   ```bash
   git clone https://github.com/lazyfoxjumps/reverse-todo.git ~/.claude/skills/reverse-todo
   ```

2. Copy the example config:

   ```bash
   cp ~/.claude/skills/reverse-todo/config.example.json ~/.claude/skills/reverse-todo/config.json
   ```

3. Open `config.json` and tweak:
   - `log_dir` if you want logs somewhere other than `~/reverse-todo`
   - `sync.obsidian.vault_path` to point at your actual vault (or set `enabled: false` to skip)
   - `sync.notion.enabled: false` if you don't use Notion. If you DO use it, leave the IDs as null and the skill will set them up on your first log.

4. Make sure the Notion MCP is connected in Claude Code if you want Notion sync. Obsidian doesn't need anything special, it's just file writes.

5. Trigger the skill: `/reverse-todo brushed teeth, ate breakfast, answered 2 emails`.

## How to use it

Just talk to me. Anything that sounds like "here's what I did" triggers the log mode:

- `/reverse-todo brushed teeth and ate lunch`
- `I just got off a hard call with my mom`
- `logged: paid 2 bills, answered 3 emails, made a real dinner`

Or use the explicit commands:

- `/reverse-todo recap` at end of day
- `/reverse-todo review week` on Sundays (or whenever your week ends)
- `/reverse-todo review month` once a month

If you're spiraling about "not doing anything," just say "I didn't do anything today" and I'll pull up the file and read it back at you. That's the whole point of this thing.

## What this skill will never do

- Lecture you
- Tell you what you "should" do tomorrow
- Use the word "grind" or "hustle" or "crush it"
- Pretend rest doesn't count
- Compare you to anyone else
- Compare you to your peak day
- Use em-dashes (banned forever, on principle)
- Tell you you're enough in some empty affirmation way

What it will do is keep the receipts and hand them back when your brain tries to rewrite history. That's the gig.

## Hard mode (coming in future versions)

The roadmap has more ADHD-specific stuff queued up:

- **Time blindness tooling:** soft check-ins, time-since-last-log, transition friction tracking, time-distortion call-outs ("you logged 6 things on Wednesday and felt like you did nothing, the math says 94, your sense of time was off that day")
- **Self-perception correction:** a win archive you can search on bad mental health days, a "compare today to my actual worst day" mode, monthly highlight reels you can bring to your therapist, a `/reverse-todo prove it` emergency mode that drops all the formatting and just reads receipts at you when you're in a hole
- **Burnout prediction:** crash-risk scoring from rolling 7-day patterns, pre-crash alerts when you're sprinting past sustainable, automatic recovery-window detection that softens the voice and bumps the multipliers when you're crashing, quarterly rollups built to bring to therapy

None of that ships until you have enough data for it to be honest. No "your sustainable median is 78" with 4 days of logs. We earn the insights.

## Files in this skill

```
reverse-todo/
  SKILL.md                    the skill itself, the 3-mode dispatch
  config.json                 paths, sync settings, categories
  README.md                   this file
  CHANGELOG.md                version history
  references/
    categories.md             the 6 buckets and what counts in each
    scoring.md                the 0-100 rubric with anchor examples
    voice.md                  the best-friend voice, what's banned, examples
    recap-template.md         end-of-day report structure
    review-template.md        weekly / monthly rollup structure
    sync-obsidian.md          Obsidian vault write rules
    sync-notion.md            Notion database schema + setup flow
```

## A note on the voice

This skill talks like a best friend who's known you for years. It knows your patterns, it knows your bullshit, it loves you anyway. It will swear when it lands. It will call out self-sabotage. It will not coddle and it will not coach.

If that's not the voice you want, the voice lives in `references/voice.md` and is the most editable part of the skill. Make it sound like whoever YOU need it to sound like.

## Why I made this

ADHD brains delete wins instantly. Mine does it too. I needed a thing that holds the receipts for me so my brain has something to argue with at 9pm when it's trying to convince me I wasted the day. So I built it. Maybe it helps you too.

If your brain is mean to you, this skill might be the friend you need on your machine.
