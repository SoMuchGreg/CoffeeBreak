# 2026-04-16 — Paladin tank shortage exemption

## Change
Added an automatic exemption to the Karazhan Paladin tank requirement: when fewer Paladin tanks sign up than teams being formed, teams without a Paladin run 2 non-Paladin tanks instead of forcing a team-count drop. The insufficient-tanks override now only triggers when hard tank requirements can't be met.

## Reason
31 signups for 19.04 Karazhan with only 2 Paladin tanks. Dropping to 2 teams (benching 11) was disproportionate. The AoE coverage loss on one team is an acceptable trade-off.

## Files touched
- `rules/01-raid-compositions.md` — added exemption to Tank composition, narrowed insufficient-tanks override
- `sets/2026-04-19-sun-karazhan.md` — updated note from "user override" to "exemption applied"