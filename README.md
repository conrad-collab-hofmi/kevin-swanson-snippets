# Kevin Swanson Snippets

A single-page tool for marking shareable moments in the Kevin Swanson conference
livestreams (recorded 2026-09-17), so snippets can be cut from the multicam later.

Reviewers watch the stream on YouTube and log the moments worth cutting. The page
produces a CSV that goes back to the editor.

**Live page → https://conrad-collab-hofmi.github.io/kevin-swanson-snippets/**

No sign-in, no install. Open it in a browser and start marking.

## Using it

`index.html` is self-contained — no build step, no dependencies. Open it in a
browser, or publish it and share the link.

For each moment a reviewer wants:

1. On YouTube: **Share → tick "Start at" → Copy**, then paste the link into the page.
   The timestamp comes across in the URL, so nothing has to be typed by hand.
2. Type roughly what was said.
3. Add an optional end time, a note, and a priority.

When they're done, **Copy CSV** and send it to the editor.

Marks are held in the reviewer's own browser (`localStorage`), so closing the tab is
safe — but nothing reaches anyone until the CSV is sent.

## Output

```csv
session,t_in,t_out,quote,note,priority,marked_by
1763,00:41:30,00:42:45,"if you don't disciple your children, the world will",strong cold open,1,Dana
```

| Column | Notes |
| --- | --- |
| `session` | `1761`–`1765`, matching the footage folder names |
| `t_in` | `HH:MM:SS` from the **start of the YouTube stream** |
| `t_out` | Same format; may be empty |
| `quote` | Roughly what was said — required |
| `note` | Why it's worth cutting; may be empty |
| `priority` | `1` must cut, `2` good, `3` maybe |
| `marked_by` | Reviewer's name; may be empty |

## Why the quote is required and the out-point isn't

A timestamp on its own is fragile: reviewers pause late, and YouTube time is not the
multicam's timeline time. A quoted phrase is self-correcting — given a transcript, the
exact sentence can be located and the in/out snapped to real sentence boundaries.

So the timestamp only has to be close enough to identify *which* occurrence of the
phrase is meant. Reviewers can be ~30s off at no cost, which is the whole point.

## Sessions

Times are the source recording runtimes, used by the page to flag a timestamp that
lands past the end of a session (usually a sign the wrong session was selected).

| Session | Title | Runtime | Stream |
| --- | --- | --- | --- |
| 1761 | How Should You Teach Your Children | ~145 min | [BfvcDfdTD_4](https://youtube.com/live/BfvcDfdTD_4) |
| 1762 | 10 Principles in Education | ~45 min | [d_cMRbvAtLI](https://youtube.com/live/d_cMRbvAtLI) |
| 1763 | Which Curriculum: What Do We Teach? | ~66 min | [FpJJKVkaQlQ](https://youtube.com/live/FpJJKVkaQlQ) |
| 1764 | Facing the Political and Cultural Barriers | ~41 min | [FmD_uX9Fx1w](https://youtube.com/live/FmD_uX9Fx1w) |
| 1765 | Q&A with Kevin Swanson & Bill Jack | ~74 min | [nwpRtjTbG0o](https://youtube.com/live/nwpRtjTbG0o) |

Session 1761 contains a recording restart about 62 minutes in.

The five streams are built into the page: each session links straight out to its
video, and pasting a link from any of them selects the matching session
automatically, so a reviewer cannot file a mark against the wrong one.

Timestamps are relative to the **YouTube livestream start = 0**; the multicam angles
are aligned to that same zero point in Final Cut Pro.
