# Forbidden Lands — Chapter 1 GM Intervention Map

> Scope: Player's Handbook, Chapter 1 — Introduction only.
> Purpose: Identify responsibilities that Chapter 1 assigns to the GM and
> therefore cannot automatically be assumed to be player decisions.

## 1. Describe the World

**GM responsibility:** Describe the Forbidden Lands and what the PCs perceive.

The player decides what the PC thinks, feels, says, and does.
The GM determines/describes what happens around and to the PC.

Engine implication:
- Requires a world-description / reveal layer.
- Must distinguish `WORLD_TRUTH` from `PLAYER_KNOWLEDGE`.

Type:
- `GM_DESCRIPTION`
- `HIDDEN_WORLD_STATE`
- potentially automatable from established world state

---

## 2. Control NPCs

**GM responsibility:** Play the people encountered by the PCs.

Includes:
- NPC behavior
- NPC dialogue
- NPC reactions
- NPC decisions

Engine implication:
- Cannot simply expose NPC state to the player.
- NPC actions need a resolver based on established facts, motivations,
  rules, tables, or oracle when genuinely uncertain.

Type:
- `GM_DECISION`
- `HIDDEN_WORLD_STATE`

---

## 3. Control Monsters

**GM responsibility:** Control monsters roaming the world.

Includes:
- what monsters do
- how they react to PCs
- their actions when encountered

Engine implication:
- Combat mechanics may be deterministic,
  but monster decision-making is a separate GM function.

Type:
- `GM_DECISION`
- `NPC/CREATURE_AI`

---

## 4. Determine Treasure Placement

**GM responsibility:** Decide where treasure is buried / located.

This is explicitly assigned to the GM in Chapter 1.

Engine implication:
- Treasure location must not be chosen by the player.
- It may be established beforehand or generated secretly.
- Player UI must not reveal undiscovered treasure.

Type:
- `HIDDEN_GM_PROCEDURE`
- `WORLD_GENERATION`

---

## 5. Present Obstacles and Challenges

**GM responsibility:** Put obstacles in the PCs' path and challenge them.

Important constraint:

The GM does **not** decide the story's outcome beforehand.
The purpose is to present situations and challenges and then discover
through play what happens.

Engine implication:
- Do not implement a "story director" that forces predetermined outcomes.
- Challenges should arise from rules, world content, encounters,
  established state, or constrained generation.

Type:
- `GM_PROCEDURE`
- `CONTENT_SELECTION`

---

## 6. Determine When an Outcome Is Uncertain Enough to Require Resolution

Normal play is a conversation until a critical situation occurs
where the outcome is uncertain; then dice are used.

Chapter 1 establishes this responsibility conceptually,
although the detailed rules are deferred to Chapter 3.

Engine implication:
- Not every declared action should automatically produce a skill roll.
- Engine eventually needs a distinction between:

    automatic success
    automatic impossibility
    uncertain / consequential action → resolution

Type:
- `GM_JUDGMENT`

Status:
- `DETAILS_DEFERRED_TO_CHAPTER_3`

---

## 7. Generate / Select Journey Encounters

Chapter 1 states that the GM has tools in the Gamemaster's Guide
for creating encounters during wilderness exploration.

Engine implication:
- Journey encounters belong to the GM/world side.
- Exact procedure is not defined in Chapter 1.

Type:
- `HIDDEN_GM_PROCEDURE`

Status:
- `DETAILS_DEFERRED_TO_GMG`

---

## 8. Determine Which Adventure Site Corresponds to a Map Symbol

The map contains symbols for:

- Village
- Castle
- Dungeon

But the exact Adventure Site represented by a particular symbol
is explicitly up to the GM.

Engine implication:

    map symbol
        ↓
    Village / Castle / Dungeon
        ↓
    GM secretly determines actual Adventure Site

The player should not automatically know the site's identity/content
merely because the map contains a symbol.

Type:
- `HIDDEN_GM_DECISION`
- `WORLD_GENERATION`

Possible resolver:
- predefined official Adventure Site
- GMG generation procedure
- Solo procedure
- constrained oracle
- human decision

---

## 9. Create Adventure Sites

The GMG provides:
- complete Adventure Sites
- tools for generating new Adventure Sites using dice

Chapter 1 therefore expects the GM to supply the actual contents
of sites when required.

Engine implication:
- Adventure Site generation belongs to hidden world generation.
- Generated truth should be separated from what the player has discovered.

Type:
- `HIDDEN_GM_PROCEDURE`

Status:
- `DETAILS_DEFERRED_TO_GMG`

---

## 10. Reveal Legends

The PCs gradually learn the world's history through Legends concerning:

- places
- people
- artifacts

The GM gives these Legends to the players.

Engine implication:
- Legends are knowledge objects.
- Existence of a Legend in world data does not mean the player knows it.
- Engine needs explicit discovery/reveal state.

Example:

    legend.exists = true
    legend.playerKnows = false

    discovery trigger
        ↓
    legend.playerKnows = true

Type:
- `GM_INFORMATION_REVEAL`
- `PLAYER_KNOWLEDGE`

---

## 11. Maintain Behind-the-Scenes World Information

Chapter 1 establishes that larger schemes can exist behind the scenes
while PCs remain free to travel and act as they wish.

This is especially explicit in the description of Raven's Purge:
characters, locations, legends, and events exist without imposing
a predetermined linear story.

Engine implication:
- Hidden world state is legitimate.
- Hidden state must not imply a scripted plot.
- PCs discover/interact with it through play.

Type:
- `HIDDEN_WORLD_STATE`

---

## 12. Share Descriptive Authority When Desired

Chapter 1 explicitly encourages the GM to let players help describe
an NPC, ruin, etc. when useful.

This is advice rather than a mandatory mechanic.

Engine implication:
- No required automation.
- Could simply remain player-facing narrative freedom.

Type:
- `OPTIONAL_NARRATIVE_AUTHORITY`

Priority:
- LOW

---

## 13. Know / Consult the GM Rules

Chapter 1 expects the GM to be familiar with both:
- Player's Handbook
- Gamemaster's Guide

Players only need the basics of the PHB.

Engine implication:
- A solo engine effectively assumes part of this GM-side rules burden.
- GM-only information must therefore remain inaccessible to the player UI.

Type:
- `ENGINE_REQUIREMENT`

---

# Chapter 1 Summary

The important GM boundary established by Chapter 1 is:

PLAYER
    ↓
declares PC intentions and actions

GM / SOLO ENGINE
    ↓
describes perceived world
controls NPCs
controls monsters
maintains hidden world truth
places/reveals treasure
presents obstacles
determines/resolves uncertainty
generates/selects encounters
assigns Adventure Sites
maintains Adventure Site contents
reveals Legends

RULES / DICE
    ↓
resolve uncertain situations

WORLD STATE
    ↓
changes according to the result

PLAYER KNOWLEDGE
    ↓
only receives information actually discovered

## Core Principle

The GM presents and resolves the world,
but does **not** determine the story's ending.

Therefore the Solo Engine should replace:

    GM procedure + GM hidden information + necessary GM judgment

but should **not** replace:

    player decisions

and should **not** become:

    a story director that decides what should happen next.
