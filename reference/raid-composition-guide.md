# TBC Party Group Composition & Buff Synergy Guide

## Overview

In TBC, many important buffs are **party-only** (affect only the 5 members in your party group), not raid-wide. This makes the composition of each 5-man group within a raid critically important for maximizing performance. This document covers all relevant party-only vs raid-wide buffs and provides group composition templates.

**TBC 20th Anniversary change:** Heroism/Bloodlust is now **raid-wide** (was party-only in original TBC). It also resets on boss kill or wipe. All other party-only buffs remain party-only.

**Important context:** Roster Machine does NOT run meta-optimized raid teams. We compose raids with whatever reliable members sign up.

> ⚠️ **Scope note:** Sections **§3, §4, §9** are **out of scope** for roster formation — they describe 5-man party-group breakdowns, which Roster Machine does not currently produce. Do not apply them when building a roster. Canonical rule: `rules/01-raid-compositions.md` → "Party groups (out of scope)". In-scope sections: §1, §2, §5, §6, §7, §8.

---

## 1. Complete Buff Scope Reference (Party-Only vs Raid-Wide)

### RAID-WIDE Buffs (affect all 25 players)

These can be placed on anyone regardless of group assignment. They do NOT drive group composition decisions.

| Buff | Source | Effect |
|------|--------|--------|
| Gift of the Wild | Druid (all) | +340 Armor, +14 all stats, +25 all resistances |
| Thorns | Druid (all) | 26 Nature damage to attackers |
| Arcane Brilliance | Mage (all) | +40 Intellect |
| Greater Blessing of Might | Paladin (all) | +220 Attack Power |
| Greater Blessing of Wisdom | Paladin (all) | +30 MP5 |
| Greater Blessing of Salvation | Paladin (all) | -30% threat generated |
| Greater Blessing of Kings | Paladin (Protection) | +10% all stats |
| Greater Blessing of Sanctuary | Paladin (Protection) | -80 damage taken, 46 Holy damage on block |
| Greater Blessing of Light | Paladin (all) | +580 Holy Light healing, +185 Flash of Light healing |
| Prayer of Fortitude | Priest (all) | +79 Stamina |
| Prayer of Shadow Protection | Priest (all) | +70 Shadow Resistance |
| Prayer of Spirit | Priest (Discipline) | +50 Spirit |
| Amplify Magic | Mage (all) | +120 spell damage taken, +240 healing taken |
| Dampen Magic | Mage (all) | -120 spell damage taken, -240 healing taken |
| Heroism / Bloodlust | Shaman (all) | +30% haste for 40 sec (Anniversary: raid-wide, resets on encounter end) |

### PARTY-ONLY Buffs (affect only the 5 players in the same group)

These are the buffs that **drive group composition decisions**. Placing the right players together to benefit from these is the core optimization challenge.

#### Druid

| Buff | Spec | Effect | Best For |
|------|------|--------|----------|
| **Moonkin Aura** | Balance | +5% spell crit to party | Caster DPS group |
| **Leader of the Pack** | Feral | +5% melee and ranged crit to party | Melee/physical DPS group |
| **Tree of Life Aura** | Restoration | +25% healing from spirit (to party) | Healer group |

#### Hunter

| Buff | Spec | Effect | Best For |
|------|------|--------|----------|
| **Trueshot Aura** | Marksmanship | +125 Attack Power to party | Physical DPS group |
| **Ferocious Inspiration** | Beast Mastery | +3% all damage to party (on pet crit, high uptime) | Any DPS group; stacks with multiple BM Hunters |
| **Aspect of the Wild** | All | +70 Nature Resistance to party | Situational |

#### Paladin (Auras are party-only; Blessings are raid-wide)

| Buff | Spec | Effect | Best For |
|------|------|--------|----------|
| **Devotion Aura** | All | +861 Armor to party | Tank group |
| **Concentration Aura** | All | +35% spell pushback resistance to party | Healer group |
| **Sanctity Aura** | Retribution | +10% Holy damage to party | Niche (Ret Paladin self-buff mostly) |
| **Retribution Aura** | All | 26 Holy damage to attackers | Tank group (minor) |
| **Fire/Frost/Shadow Resistance Aura** | All | +70 respective resistance to party | Situational per encounter |
| **Crusader Aura** | All | +20% mounted speed to party | Non-combat |

**Key note:** Paladin Blessings (Kings, Might, Wisdom, Salvation, etc.) are all **raid-wide** via Greater Blessings. Only the auras are party-only. This means Paladin group placement matters only for their aura, not their blessings.

#### Priest

| Buff | Spec | Effect | Best For |
|------|------|--------|----------|
| **Vampiric Touch** | Shadow | Party members gain mana = 5% of Shadow damage dealt | Caster/healer mana battery |
| **Vampiric Embrace** | Shadow | Party members healed for 15% of Shadow damage dealt (25% with Improved talent) | Passive party healing |

**Key note:** Shadow Priest is often called a "mana battery." Vampiric Touch restores mana to the **party only**, making Shadow Priest placement in caster groups critically important.

#### Warrior

| Buff | Spec | Effect | Best For |
|------|------|--------|----------|
| **Battle Shout** | All | +306 melee Attack Power to party | Melee DPS group |
| **Commanding Shout** | All | +1,080 max health to party | Tank group |

**Key note:** Only one shout can be active at a time per Warrior. Battle Shout and Commanding Shout are mutually exclusive.

#### Warlock

| Buff | Spec | Effect | Best For |
|------|------|--------|----------|
| **Blood Pact** | All (Imp pet) | +70 Stamina to party | Any group (minor survivability) |

#### Shaman (ALL totems are party-only)

See Section 2 below for full totem details.

---

## 2. Shaman Totem Reference (All Party-Only)

Shaman totems are the single most important factor in group composition. Each totem belongs to one of four elements, and **only one totem per element can be active at a time**. This creates critical choices per group.

### Earth Totems (pick one)

| Totem | Effect | Best For |
|-------|--------|----------|
| **Strength of Earth** | +86 Strength to party | Melee DPS (Warriors, Ret Paladins, Feral Druids, Enhancement Shamans) |
| **Stoneskin** | -43 melee damage taken | Tank group |
| **Tremor** | Removes Fear/Sleep/Charm every 3 sec | Situational (fear encounters) |
| **Earth Elemental** | Summons Earth Elemental (emergency tank) | Emergency |

### Air Totems (pick one)

| Totem | Effect | Best For |
|-------|--------|----------|
| **Windfury** | 20% chance for extra attack with +445 AP | Melee DPS (especially Warriors, Rogues) |
| **Grace of Air** | +77 Agility to party | Physical DPS (Hunters, Rogues, Feral Druids) |
| **Wrath of Air** | +101 Spell Damage and Healing to party | Caster DPS and healers |
| **Tranquil Air** | -20% threat generated | Threat-sensitive groups |
| **Windwall** | -102 ranged damage taken | Situational |

**Totem Twisting (Enhancement Shaman only):** An advanced technique where the Shaman alternates between Windfury and Grace of Air totems every ~10 seconds, keeping both buffs active simultaneously. Windfury's buff persists for 10 seconds after the totem is replaced, allowing the Shaman to drop Grace of Air during that window. This is mana-intensive but provides the best possible physical DPS support. Enhancement Shamans in melee groups are expected to totem twist.

### Fire Totems (pick one)

| Totem | Effect | Best For |
|-------|--------|----------|
| **Totem of Wrath** | +3% spell hit AND +3% spell crit to party (Elemental only) | Caster DPS group (extremely powerful) |
| **Searing** | Deals Fire damage to nearby enemy | DPS filler |
| **Fire Elemental** | Summons Fire Elemental | Burst DPS |
| **Flametongue** | +19-59 Fire damage to melee attacks | Niche |
| **Fire/Frost Resistance** | +70 respective resistance | Situational |

### Water Totems (pick one)

| Totem | Effect | Best For |
|-------|--------|----------|
| **Mana Spring** | +20 mana every 2 sec to party (~50 MP5) | Casters, healers, any mana user |
| **Healing Stream** | +18 health every 2 sec to party | Minor passive healing |
| **Mana Tide** | +6% total mana every 3 sec for 12 sec (Restoration only, 5 min CD) | Healer group |
| **Poison Cleansing** | Removes 1 poison every 5 sec | Situational |
| **Disease Cleansing** | Removes 1 disease every 5 sec | Situational |

### Shaman Spec Summary for Group Assignment

| Shaman Spec | Unique Contribution | Ideal Group Placement |
|-------------|--------------------|-----------------------|
| **Enhancement** | Unleashed Rage (+10% melee AP to party), Windfury/Grace of Air totem twisting, Strength of Earth | Melee/physical DPS group |
| **Elemental** | Totem of Wrath (+3% spell hit/crit), Wrath of Air (+101 spell damage) | Caster DPS group |
| **Restoration** | Mana Tide Totem, Chain Heal, Wrath of Air or Grace of Air | Healer group or flexible |

---

## 3. Optimal Party Group Templates (25-Man)

> ⚠️ **Out of scope for roster formation.** See `rules/01-raid-compositions.md` → "Party groups (out of scope)". Do not apply this section when building a roster.

### Group 1: Melee / Physical DPS Group

**Goal:** Maximize physical damage output through stacked melee buffs.

| Slot | Class/Spec | Buff Contribution |
|------|-----------|-------------------|
| 1 | **Enhancement Shaman** | Windfury + Grace of Air (totem twisting), Strength of Earth, Unleashed Rage (+10% melee AP), Mana Spring |
| 2 | **Feral Druid** | Leader of the Pack (+5% melee/ranged crit) |
| 3 | **Arms Warrior** | Battle Shout (+306 AP), Blood Frenzy (+4% physical damage debuff, raid-wide) |
| 4 | **Combat Rogue** | Improved Expose Armor (raid-wide debuff) |
| 5 | **Fury Warrior / Ret Paladin / BM Hunter** | Flex DPS slot |

**Buffs stacking in this group:**
- +5% crit (Leader of the Pack)
- +306 AP (Battle Shout) + 220 AP (Blessing of Might)
- +86 Strength (Strength of Earth)
- Windfury procs (+445 AP extra attacks)
- +77 Agility (Grace of Air, via totem twisting)
- +10% melee AP (Unleashed Rage)

### Group 2: Ranged Physical DPS Group

**Goal:** Support BM Hunters and other physical ranged DPS.

| Slot | Class/Spec | Buff Contribution |
|------|-----------|-------------------|
| 1 | **Enhancement Shaman** or **Restoration Shaman** | Grace of Air (+77 Agi), Strength of Earth, Mana Spring |
| 2 | **Feral Druid** (if available) or **Survival Hunter** | Leader of the Pack (+5% crit) or Expose Weakness |
| 3 | **BM Hunter** | Ferocious Inspiration (+3% all damage) |
| 4 | **BM Hunter** | Ferocious Inspiration stacks (+3% more) |
| 5 | **BM Hunter / Fury Warrior** | Additional physical DPS |

**Notes:** Multiple BM Hunters in one group stack Ferocious Inspiration multiplicatively. 2-3 BM Hunters in a group is common and powerful.

### Group 3: Caster DPS Group (Warlock Stack)

**Goal:** Maximize spell damage through caster-specific party buffs.

| Slot | Class/Spec | Buff Contribution |
|------|-----------|-------------------|
| 1 | **Elemental Shaman** | Totem of Wrath (+3% spell hit/crit), Wrath of Air (+101 spell damage), Mana Spring |
| 2 | **Shadow Priest** | Vampiric Touch (mana battery: 5% of shadow damage as party mana), Shadow Weaving (+10% shadow damage debuff, raid-wide) |
| 3 | **Balance Druid** | Moonkin Aura (+5% spell crit), Improved Faerie Fire (+3% hit debuff, raid-wide) |
| 4 | **Destruction Warlock** | Improved Shadow Bolt (+20% shadow damage debuff, benefits all shadow casters) |
| 5 | **Destruction Warlock** | Stacking Warlock synergy |

**Buffs stacking in this group:**
- +5% spell crit (Moonkin Aura)
- +3% spell hit, +3% spell crit (Totem of Wrath)
- +101 spell damage (Wrath of Air)
- Mana restoration (Vampiric Touch)
- Passive healing (Vampiric Embrace)
- ~50 MP5 (Mana Spring Totem)

**This is the most important caster group in the raid.** The combination of Elemental Shaman + Shadow Priest + Balance Druid provides an enormous buff stack for Warlocks.

### Group 4: Secondary Caster / Healer Hybrid Group

**Goal:** Support remaining casters and provide healing buffs.

| Slot | Class/Spec | Buff Contribution |
|------|-----------|-------------------|
| 1 | **Restoration Shaman** | Wrath of Air (+101 spell damage/healing), Mana Spring, Mana Tide (CD) |
| 2 | **Shadow Priest** (if 2nd available) or **Affliction Warlock** | Mana battery or Malediction (+3% spell damage debuff) |
| 3 | **Destruction Warlock** | DPS |
| 4 | **Arcane Mage / Fire Mage** | DPS |
| 5 | **Holy Paladin / Healer** | Concentration Aura for casters, healing |

### Group 5: Tank / Healer Group

**Goal:** Maximize tank survivability and healer efficiency.

| Slot | Class/Spec | Buff Contribution |
|------|-----------|-------------------|
| 1 | **Main Tank** (Prot Warrior / Prot Paladin / Feral Druid) | Commanding Shout if Warrior (+1,080 HP) |
| 2 | **Off-Tank** | Additional tanking |
| 3 | **Restoration Druid** | Tree of Life aura (+25% healing from spirit to party) |
| 4 | **Holy Paladin** | Devotion Aura (+861 armor to party), Concentration Aura if healers struggle |
| 5 | **Holy Priest / Restoration Shaman** | Healing + Mana Tide if Resto Shaman |

**Notes:** If running Restoration Druid as Tree of Life, the +healing aura benefits all healers in the group. Grouping healers together can maximize this, but some raids prefer spreading healers across groups for coverage.

---

## 4. Karazhan (10-Man) Group Composition

> ⚠️ **Out of scope for roster formation.** See `rules/01-raid-compositions.md` → "Party groups (out of scope)". Do not apply this section when building a roster.

With only 2 groups, you cannot optimize as thoroughly as in 25-man. The key is to split melee/physical and caster/healer interests.

### Typical Karazhan Composition: 2 Tanks, 3 Healers, 5 DPS

### Group 1: Melee / Physical Focus

| Slot | Role | Class/Spec |
|------|------|-----------|
| 1 | Tank | Feral Druid or Prot Warrior |
| 2 | Tank/DPS | Prot Paladin or Arms Warrior (flex) |
| 3 | Melee DPS | Rogue / Ret Paladin / Fury Warrior |
| 4 | Physical DPS | BM Hunter |
| 5 | Support | Enhancement Shaman (Windfury, Strength of Earth) or Feral Druid (Leader of the Pack) |

### Group 2: Caster / Healer Focus

| Slot | Role | Class/Spec |
|------|------|-----------|
| 1 | Healer | Holy Paladin / Resto Druid |
| 2 | Healer | Holy Priest / Resto Shaman |
| 3 | Healer | Resto Shaman / Resto Druid |
| 4 | Caster DPS | Warlock / Mage |
| 5 | Caster DPS / Support | Shadow Priest (mana battery) / Balance Druid / Elemental Shaman |

### Karazhan Priority Rules

1. **If you have an Enhancement Shaman:** Put them with melee DPS and tanks for Windfury.
2. **If you have an Elemental Shaman:** Put them with casters for Totem of Wrath + Wrath of Air.
3. **If you have a Shadow Priest:** Put them with mana-hungry casters (Warlocks, Mages) for Vampiric Touch.
4. **If you have a Balance Druid:** Group with casters for Moonkin Aura (+5% spell crit).
5. **If you have a Feral Druid tanking:** Their Leader of the Pack benefits melee DPS in the same group.
6. **Healers benefit from:** Mana Spring Totem, Wrath of Air (if healing), Tree of Life aura (if Resto Druid in group).

---

## 5. Buff Priority Ranking

When you cannot give every group optimal buffs (limited shamans, druids, etc.), prioritize based on DPS/HPS impact.

### Highest-Impact Party Buffs (prioritize these assignments first)

1. **Windfury Totem** in a melee group with Warriors and Rogues (massive DPS gain from extra attacks)
2. **Totem of Wrath + Wrath of Air** in main caster group (spell hit + crit + spell power is huge)
3. **Shadow Priest (Vampiric Touch)** in caster group with Warlocks (mana sustain enables longer DPS)
4. **Leader of the Pack** in melee/physical group (+5% crit is significant for physical DPS)
5. **Moonkin Aura** in caster group (+5% spell crit for all casters)
6. **Ferocious Inspiration** with BM Hunter stack (+3% damage, stacks)
7. **Unleashed Rage** in melee group (+10% melee AP)
8. **Tree of Life Aura** in healer group (if healers are grouped together)

### Medium-Impact Party Buffs

9. **Grace of Air Totem** (+77 Agility) for physical DPS
10. **Strength of Earth Totem** (+86 Strength) for melee
11. **Mana Spring Totem** (~50 MP5) for casters/healers
12. **Battle Shout** (+306 AP) for melee
13. **Wrath of Air** in healer group (+101 healing power)
14. **Concentration Aura** for healer group (spell pushback resistance)
15. **Devotion Aura** for tank group (+861 armor)

---

## 6. Drums of Battle (Leatherworking)

Drums are party-only consumables crafted by Leatherworkers. In TBC Anniversary:

| Drum | Effect | Duration | Best For |
|------|--------|----------|----------|
| **Drums of Battle** | +80 haste rating to party | 30 sec | All DPS/healers |
| **Drums of War** | +60 Attack Power and +30 Spell Power to party | 30 sec | Any group |
| **Drums of Restoration** | +15 MP5 to party | 30 sec | Healer/caster group |

**Tinnitus debuff** (introduced in TBC Classic Phase 4): After being affected by drums, players receive a 2-minute Tinnitus debuff preventing them from benefiting from drums again. This means you only need **one Leatherworker per group** for drum coverage, not the entire raid.

**Ideal setup:** One Leatherworker with Drums of Battle in each of the 4 DPS/healing groups. Druids make ideal drummers since they can use drums while shapeshifted.

---

## 7. Common Raid-Wide Debuffs (Not Party-Dependent, But Composition-Relevant)

These debuffs affect the boss and benefit the entire raid, but require specific specs to be present somewhere in the raid (group placement irrelevant):

| Debuff | Source | Effect |
|--------|--------|--------|
| Misery | Shadow Priest | +5% spell damage taken by target |
| Shadow Weaving | Shadow Priest | +10% shadow damage taken (5 stacks of 2%) |
| Improved Faerie Fire | Balance Druid | +3% melee/ranged hit chance vs target |
| Curse of Elements | Warlock | +10% Fire/Frost damage taken, -88 resistances |
| Curse of Recklessness | Warlock | -800 armor on target |
| Curse of Shadow | Warlock | +10% Shadow/Arcane damage taken, -88 resistances |
| Improved Shadow Bolt | Destruction Warlock | +20% shadow damage taken (on crit) |
| Blood Frenzy | Arms Warrior | +4% physical damage taken |
| Expose Armor | Rogue | Reduces armor significantly |
| Expose Weakness | Survival Hunter | +25% of Agi as AP for all attackers |
| Judgement of Wisdom | Paladin | Attacks restore mana |
| Judgement of Light | Paladin | Attacks restore health |
| Judgement of the Crusader | Paladin | +219 Holy damage taken |
| Sunder Armor | Warrior | Reduces armor (5 stacks) |

---

## 8. Quick Reference: Number of Each Spec Typically Desired

### 25-Man Raid (General Guidelines)

| Spec | Typical Count | Reason |
|------|--------------|--------|
| Enhancement Shaman | 1-2 | Melee group totem twisting |
| Elemental Shaman | 0-1 | Caster group Totem of Wrath |
| Restoration Shaman | 1-3 | Chain Heal + totems for healer/caster groups |
| Shadow Priest | 1-2 | Mana battery for caster groups |
| Balance Druid | 1 | Moonkin Aura + Improved Faerie Fire |
| Feral Druid | 1-2 | Tank + Leader of the Pack |
| Restoration Druid | 1-2 | Tree of Life + HoTs |
| BM Hunter | 2-4 | Top physical DPS + Ferocious Inspiration |
| Survival Hunter | 0-1 | Expose Weakness |
| Destruction Warlock | 3-5 | Top caster DPS, stack well |
| Affliction Warlock | 0-1 | Malediction (+3% spell damage debuff) |
| Arms Warrior | 1 | Blood Frenzy debuff |
| Fury Warrior | 0-2 | Strong physical DPS |
| Protection Warrior | 0-1 | Main tank |
| Protection Paladin | 0-1 | AoE tank |
| Combat Rogue | 1-2 | Improved Expose Armor |
| Holy Paladin | 1-2 | Strong single-target heals + auras |
| Holy Priest | 1 | Versatile healing |
| Fire/Arcane Mage | 1-2 | Arcane Brilliance + DPS |
| Retribution Paladin | 0-1 | Sanctity Aura (niche), Judgements |

---

## 9. Practical Group Assignment Framework (Non-Meta Rosters)

> ⚠️ **Out of scope for roster formation.** See `rules/01-raid-compositions.md` → "Party groups (out of scope)". Do not apply this section when building a roster.

The templates in sections 3-4 assume ideal compositions. In reality, you'll often be missing key specs, have too many of one class, or have unusual comp combinations. Use this framework to make group assignments when the roster doesn't match any template.

### Step 1: Identify your buff providers

Before assigning groups, scan the roster and list who provides party-only buffs:

| Question | Look for |
|----------|----------|
| Do we have any Enhancement Shamans? | Windfury, totem twisting, Unleashed Rage |
| Do we have any Elemental Shamans? | Totem of Wrath, Wrath of Air |
| Do we have any Resto Shamans? | Mana Tide, Wrath of Air or Grace of Air |
| Do we have a Balance Druid? | Moonkin Aura |
| Do we have a Feral Druid (DPS or tank)? | Leader of the Pack |
| Do we have a Resto Druid? | Tree of Life Aura |
| Do we have a Shadow Priest? | Vampiric Touch (mana battery) |
| How many Paladins and what auras? | Devotion, Concentration, etc. |
| Do we have DPS Warriors? | Battle Shout for melee group |

If a buff provider is missing entirely, skip rules that depend on them — don't try to approximate.

### Step 2: Count your melee vs. caster/ranged DPS

Classify every DPS player:
- **Melee/physical:** Warriors (Arms, Fury), Rogues, Enhancement Shamans, Feral Druids, Ret Paladins
- **Ranged/caster:** Mages, Warlocks, Shadow Priests, Elemental Shamans, Balance Druids, Hunters

This ratio determines whether you lean groups toward melee or caster optimization. If you're heavy on one side, that side gets the best buff support.

### Step 3: Place buff providers using priority rules

Work through these in order. Each rule is independent — skip any that don't apply to your roster:

1. **Enhancement Shaman → group with the most melee DPS.** Windfury is wasted on casters. If you have 2+ Enhancement Shamans, spread them across melee-heavy groups.
2. **Elemental Shaman → group with the most caster DPS.** Totem of Wrath + Wrath of Air is the biggest caster buff stack. If no caster DPS available, put them with healers (Wrath of Air still helps).
3. **Feral Druid → group with physical DPS (melee or hunters).** Leader of the Pack benefits melee AND ranged physical. If the Feral is tanking, group melee DPS with them.
4. **Balance Druid → group with caster DPS.** Moonkin Aura benefits all spellcasters. If already in a group with Elemental Shaman, even better (buffs stack).
5. **Shadow Priest → group with the most mana-hungry casters.** Mages benefit most (pure mana dependency). Warlocks are second priority (life tap gives them an alternative mana source). If no casters, put with healers.
6. **Resto Druid → group with other healers** (if healers are grouped). Tree of Life Aura benefits all healers in the party.
7. **Resto Shaman → flexible.** Healer group (Mana Tide), caster group (Wrath of Air), or physical group (Grace of Air) depending on what the roster needs most.
8. **Paladin aura → match to group role.** Devotion Aura with tanks, Concentration Aura with healers/casters. If only one Paladin, prioritize the group that needs it most.
9. **DPS Warrior → group with other melee.** Battle Shout is party-only and only benefits melee.

### Step 4: Fill remaining slots by affinity

After buff providers are placed, fill remaining group slots:
- **Melee DPS** go with other melee (to share Windfury, Battle Shout, Leader of the Pack)
- **Caster DPS** go with other casters (to share Wrath of Air, Moonkin Aura, Totem of Wrath)
- **Hunters** are flexible — they benefit from Leader of the Pack and Grace of Air (physical group), but don't benefit from Windfury. Place them in whichever group has room, preferring physical buff groups.
- **Healers** can go anywhere, but benefit most from: Mana Spring Totem, Wrath of Air (increases healing), Tree of Life Aura, Concentration Aura

### Step 5: Handle common "missing piece" scenarios

| Scenario | Adaptation |
|----------|------------|
| **No Shaman in a group** | That group loses totems entirely. Prioritize putting Shamans in the groups where their totems matter most (melee group > caster group > healer group). A group without a Shaman is fine — just less optimized. |
| **No Shadow Priest** | Casters/healers lose their mana battery. Consider placing a Resto Shaman with casters for Mana Spring. Healers may need to drink more between pulls. |
| **No Balance Druid** | Casters lose +5% spell crit. No substitute — just stack other caster buffs (Totem of Wrath, Wrath of Air). |
| **No Feral Druid** | Physical DPS lose +5% crit. No direct substitute. |
| **Only 1 Shaman for 2+ groups that want one** | Use the buff priority ranking (Section 5). Windfury in a melee-heavy group generally beats Wrath of Air in a caster group, but depends on the ratio. |
| **Too many melee, not enough ranged (or vice versa)** | Don't force a melee/caster split. Make mixed groups and put the Shaman with whichever type dominates the group (Windfury if melee-heavy, Wrath of Air if caster-heavy). |
| **Only 1 healer for a 10-man group** | Put the healer with the tank group. The other group has to rely on off-healing, bandages, and healthstones. |
| **Multiple Warriors in one group** | Only one Battle Shout active at a time — spread Warriors across groups when possible so more groups benefit from it. |

### Karazhan-Specific (2 groups of 5)

With only 2 groups, perfect splits are rarely possible. Follow these priorities:

1. **Tanks go in Group 1** (they need the Shaman/Paladin defensive buffs most).
2. **Enhancement Shaman with tanks + melee DPS** (Windfury for tanks is huge for threat, plus melee DPS benefit).
3. **Healers lean toward Group 2** (with casters), but split if you have a Resto Shaman (totems benefit healers) and a Paladin healer (Concentration Aura for casters).
4. **If you only have 1 Shaman total**, they go in whichever group has the most players who benefit from their spec's totems.
5. **Caster DPS with healers is fine** — they share Wrath of Air and Mana Spring benefits.
6. **A Hunter can go in either group** — they don't need Windfury but benefit from Leader of the Pack. Place based on what fills groups evenly.

### The "Good Enough" Principle

Not every group will be optimally buffed. That's fine. The goal is:
- Every Shaman is in a group where their totems help the most people
- Melee and casters are separated where possible (so Windfury doesn't go to waste on casters)
- No buff provider is isolated in a group where nobody benefits from their buff
- When in doubt, even distribution is better than one super-buffed group and one naked group

---

## Sources

- [Wowhead: Burning Crusade Classic Buffs & Debuffs By Class](https://www.wowhead.com/tbc/guide/raid-buffs-debuffs-by-class-wow-burning-crusade-classic)
- [Wowhead: Raid Composition Guide for 25 Man Raids](https://www.wowhead.com/tbc/guide/raid-composition-guide-25-man-burning-crusade-classic-wow)
- [Wowhead: Best 25-Player Raid Composition for TBC Anniversary Phase 1](https://www.wowhead.com/tbc/news/the-best-25-player-raid-composition-for-the-burning-crusade-anniversary-phase-1-380393)
- [Icy Veins: Raid Composition Guide for TBC Classic](https://www.icy-veins.com/tbc-classic/raid-composition-guide)
- [IGGM: 4 Essential Group Setups Every Raid Needs](https://www.iggm.com/news/wow-tbc-classic-anniversary-phase-1-4-group-setups-every-raid-needs)
- [EU Forums: Optimal 25man Composition with Raid-Wide Heroism](https://eu.forums.blizzard.com/en/wow/t/what-is-the-optimal-25man-raid-composition-now-that-heroismbloodlust-is-raid-wide/596453)
- [IGGM: TBC Anniversary vs Original TBC Gameplay Changes](https://www.iggm.com/news/wow-tbc-classic-anniversary-vs-original-tbc-gameplay-changes-in-2026)