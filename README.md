# Word Shredder

A strict word trainer (words, phrases, sentences, EN ↔ RU) with a Christmas ski-resort look.

| File | What it is |
|---|---|
| `index.html` | The app on his phone |
| `editor.html` | **Studio**: add words and media on the PC, then *Publish to site* |
| `manifest.webmanifest`, `sw.js`, `icons/` | Make it installable and work offline |
| `content/` | Created by Studio when you publish: the word list, pictures and media |

## How it works

- **No self-grading.** Every card is a test: choose from 6, type it, hear it and type it, type the missing part, or build the sentence from word tiles. The last step before *Learned* is always typed.
- **Own keyboard.** There is no text field, so no autocorrect, suggestions, paste or voice typing.
- **Anti-cheat.** A time limit per answer, leaving the app during a card counts as a miss, no hints, a miss costs 3 points, and fast guesses, time-outs and app switches are logged.
- **Schedule.** Sessions per day in time windows. A session counts only if the timer is finished with enough correct answers. More sessions than scheduled count as extras.
- **Rewards.** Perfect week, extra sessions, every N learned items. Status: in progress → earned → paid.

## Media (labelled placeholders show until you load yours in Studio → Media & levels)

| Slot | Ratio | Format |
|---|---|---|
| Home scene | 16:9 | silent loop, 6–10 s, MP4 or GIF |
| Session finished video | 16:9 | MP4 with sound, about 10 s |
| "Correct" reaction | 16:9 | silent, 2–3 s |
| "Wrong" reaction | 16:9 | silent, 2–3 s |
| Word and verb pictures | 4:3 | PNG or JPG, e.g. 1200×900 (any size works; it is cropped to 4:3 from the centre) |
| Level pictures (15) | 1:1 | PNG or GIF |
| Avatars (up to 12) | 1:1 | PNG or JPG, shown as a circle. He picks one on the home screen, or uses his own photo |
| Reward animations | 1:1 | silent loop (stage 2, set in the admin page) |
| App icon (`icons/`) | 1:1 | PNG 180, 192, 512 px |

## Where your files go

| What | Where |
|---|---|
| Words, phrases, sentences (+ optional pictures) | Studio → **Words** → *Import Excel* or *+ Add word*, then drag the pictures onto the page |
| Irregular verb pictures (100) | Studio → **Irregular verbs** → drag all of them at once (named like the verb: `go.png`, `cut.jpg`) |
| Home scene, finished video, correct / wrong reactions | Studio → **Media & levels** |
| Avatars (up to 12), level pictures (15) | Studio → **Media & levels** |
| Reward animations | Admin page → **Rewards** → *Add animation* |
| App icon | Replace the files in `icons/` on GitHub |

Then **Publish to site** (Studio) or **Save & send to his phone** (admin page).

## Irregular verbs

100 verbs built into Studio, in learning order (10 sets of 10). Verbs have **their own button** (home screen and Verbs tab), their own blue practice window and their own score. Verb practice never fills a word session and does not count for word levels; word sessions contain no verbs. Admin page → Rules: *Verb practice length* (default 5 min) and *Irregular verbs in rotation* (default 6). Rewards can use the rule *Every N irregular verbs learned*. First meeting: pick the right forms out of 6. After that: type **both** the past simple and the past participle; one wrong form = miss. Both learnt/learned, burnt/burned, was/were and got/gotten are accepted. His **Verbs** tab shows the sets and his progress.

## Dad's desk (admin page): `admin.html`

Manage everything from anywhere: schedule, scoring, time limits, rewards with their animations, **Payment done**, his sessions and the honesty report.

**How the link works**

- A **private** repo `wordshredder-data` holds `rules.json` (your rules) and `log/` (his sessions).
- Your rules are **signed** with a key that stays in your browser. His phone only accepts rules with your signature, and never an older copy. If the file is changed by anyone else, the app ignores it and reports it to you.
- His phone has its own token that can only reach `wordshredder-data`.

**One-time setup**

1. On GitHub create a **private** repo named `wordshredder-data`.
2. Tokens (github.com → Settings → Developer settings → Fine-grained tokens), both with *Contents: Read and write*:
   - **Yours:** access to `wordshredder` and `wordshredder-data` (also use it in Studio).
   - **His phone's:** access to `wordshredder-data` only.
3. Open `https://YOUR-NAME.github.io/wordshredder/admin.html` → **Setup**:
   - paste your token → **Connect**
   - **Create a key** → **Back up the key** (keep the file safe)
   - set **Rules** and **Rewards** → **Save & send to his phone**
4. **Setup → Link his phone:** paste his phone's token → **Make the link** → send it to his phone → open it once in Chrome → delete the message.
5. On his phone: Chrome **⋮ → Add to Home screen**.

After that his phone sends each session when it has internet, and picks up your changes every time the app opens.

**Limits**

- Not instant: you see a session a few seconds to a minute after he finishes (or later if he was offline).
- Tokens expire after at most a year; make new ones and link again.
- A new PC needs your key backup (Setup → Restore), otherwise you must link his phone again.
- His phone's token can write the session log, so a determined kid with a PC could fake log entries. The GitHub history of `wordshredder-data` shows every change with date and time.
