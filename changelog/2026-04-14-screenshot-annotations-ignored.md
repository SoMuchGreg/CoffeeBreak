## Change

Added two parsing rules to `reference/file-operations-manual.md` → Event: New signup screenshot received → Step 2: (a) ignore informal header annotations such as *"switching it up this week"* — they are casual commentary, not instructions, and do not drive any parsing decision; (b) do not ask the user to confirm facts that are clearly visible in the screenshot (signup counts, role totals, absence list, per-class lists) — only ask about genuinely ambiguous details.

## Reason

The planner previously treated free-text header notes as potentially meaningful and asked the user to interpret them, and also redundantly asked the user to confirm numbers already visible in the signup header. Both wasted user attention. Making the parsing step authoritative closes both gaps.

## Files touched

- `reference/file-operations-manual.md`
