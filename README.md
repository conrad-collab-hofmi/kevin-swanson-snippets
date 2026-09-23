# Kevin Swanson Snippets

A single-page tool for marking shareable moments in the Kevin Swanson conference
livestreams (recorded 2026-09-17), so snippets can be cut from the multicam later.

Reviewers watch the stream on YouTube and log the moments worth cutting. The page
produces a CSV that goes back to the editor.

## Using it

`snippet-log.html` is self-contained — no build step, no dependencies. Open it in a
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

| Session | Runtime | Note |
| --- | --- | --- |
| 1761 | ~145 min | Contains a recording restart ~62 min in |
| 1762 | ~45 min | |
| 1763 | ~66 min | |
| 1764 | ~41 min | |
| 1765 | ~74 min | |

Timestamps are relative to the **YouTube livestream start = 0**; the multicam angles
are aligned to that same zero point in Final Cut Pro.
