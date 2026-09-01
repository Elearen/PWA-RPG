# PROJECT CONTEXT

## Purpose

This document provides the high-level context required for an AI coding agent working on the PWA RPG project.

The detailed specification files in this repository are the authoritative sources for individual systems. This document does **not** replace those specifications and should not be used as a substitute for reading the relevant specification when implementing a feature.

When a detailed specification conflicts with assumptions made by the coding agent, the specification takes precedence.

---

# 1. PROJECT OVERVIEW

PWA RPG is a persistent, story-driven, mobile-first RPG delivered as a Progressive Web Application.

The game combines:

* exploration
* automated/state-based combat
* character progression
* skills and abilities
* equipment and generated loot
* inventory management
* quests
* journeys
* dungeons
* NPCs and factions
* a persistent evolving world
* Journal-based narrative
* multiple interconnected story perspectives

The game is fundamentally a **single-player RPG**.

An optional no-stakes duel simulator allows players to compare character builds against other players without turning the main game into a multiplayer campaign.

The project is designed for incremental development using an AI coding platform, initially targeting **Bolt for development, hosting and managed backend/database infrastructure**.

---

# 2. DESIGN PHILOSOPHY

The project prioritises:

* depth over unnecessary visual complexity
* meaningful progression
* exploration and discovery
* interconnected systems
* strong worldbuilding
* persistent consequences
* readable mobile-first interfaces
* modular implementation
* extensible authored content
* maintainable AI-generated code

The game is intentionally not designed as a graphics-heavy action RPG.

Its complexity comes primarily from:

* systems
* character builds
* equipment
* combat
* progression
* world state
* exploration
* narrative
* relationships between systems

The UI should make these systems understandable without making the underlying game shallow.

---

# 3. NARRATIVE IDENTITY

The game is a story-driven RPG in which narrative remains important despite automated/state-based combat.

The narrative should primarily emerge through:

* exploration
* locations
* encounters
* NPCs
* quests
* Points of Interest
* Journal entries
* Story Bites
* discoveries
* world events
* consequences of events occurring elsewhere

The game should generally favour **small, meaningful discoveries** over large blocks of exposition.

The Journal is an important interface between gameplay and narrative.

Story should feel embedded in the world rather than separated into long conventional dialogue scenes.

Refer to `STORY_NARRATIVE_SPEC.md` for the authoritative narrative design.

---

# 4. THREE-PROTAGONIST STRUCTURE

The game contains three canonical protagonists and three distinct starting locations.

The three protagonists are not separate universes or unrelated campaigns.

They exist within the same world and broader timeline.

Each starting storyline provides a different perspective on the same developing world.

The three perspectives broadly begin from:

* a forest/farming settlement and military environment
* a coastal trading environment
* a human mountain settlement connected to dwarven society

The player therefore learns about the wider world differently depending on the selected starting storyline.

Events experienced directly by one protagonist may appear indirectly to another through:

* rumours
* trade disruption
* refugees
* military developments
* NPC reports
* environmental changes
* Journal discoveries
* changes in regional conditions

The world should feel interconnected rather than consisting of isolated campaign zones.

---

# 5. WORLD IDENTITY

The setting is grounded, relatively low-magic fantasy.

The present-day world should feel believable and geographically connected.

It contains diverse environments and societies including:

* kingdoms
* forests
* mountains
* dwarven settlements
* coastal regions
* deserts
* marshes
* ruins
* dangerous wilderness
* trade routes
* political centres
* guilds
* settlements
* battlefields

The world contains deeper mysteries and remnants of an older magical past, but this should not turn the present-day setting into a conventional high-magic world.

Political, economic, social and environmental pressures are important parts of the setting alongside monsters and supernatural mysteries.

The detailed world, geography and lore are defined by `WORLD_EXPLORATION_SPEC` and `STORY_NARRATIVE_SPEC`.

---

# 6. NARRATIVE PROGRESSION

The main narrative has a coherent overarching progression while allowing substantial freedom within available regions.

The player should generally understand **what they are trying to discover or accomplish** without always being given a rigid sequence of exact actions.

Exploration should help the player determine how to progress.

The game distinguishes between:

* required narrative progression
* optional discoveries
* flavour content
* side stories
* world lore

A player should not be able to permanently destroy the main campaign merely by failing to interact with one particular NPC or location.

---

# 7. CHARACTER PHILOSOPHY

Characters are designed around flexible builds rather than rigid permanent RPG classes.

A character's identity emerges from their:

* attributes
* equipment
* weapon use
* skills
* abilities
* progression choices
* combat behaviour

The player should be able to develop a character organically.

The protagonists are intentionally relatively open-ended rather than heavily authored personalities. Their starting circumstances provide narrative identity without requiring extensive dialogue-choice roleplay.

Refer to `CHARACTER_FOUNDATION_SPEC.md` for the authoritative character model.

---

# 8. CORE SYSTEMS

The project is divided into distinct but interconnected systems.

Major domains include:

* Account & Persistence
* Character Foundation
* Progression & Economy
* Combat
* Skills & Abilities
* Equipment & Loot
* Inventory & Item Management
* Enemy & Boss
* Journey & Dungeon
* World & Exploration
* NPC & Faction
* Quest & Journal
* Story & Narrative
* UI & UX
* Technical Architecture

Each domain has a dedicated specification.

The specifications should be treated as the authoritative definition of that system.

---

# 9. SYSTEM OWNERSHIP

Every significant rule should have a clear owning system.

For example:

```text
Character
    owns character identity and foundation

Progression
    owns progression rules

Combat
    owns combat resolution

Equipment & Loot
    owns item generation and loot behaviour

Inventory
    owns item ownership and storage

Quest & Journal
    owns quest progression and journal state

World
    owns world structure and exploration

Story
    owns narrative structure and story content

Technical Architecture
    owns implementation boundaries and persistence architecture
```

Do not duplicate rules between systems.

If a feature touches several systems, identify which system owns each part before implementing it.

---

# 10. CROSS-SYSTEM DESIGN

Systems should communicate through clear interfaces and operations.

Avoid allowing one system to directly manipulate another system's internal state without an explicit reason.

Prefer:

```text
SYSTEM A
   ↓
Defined operation/result
   ↓
SYSTEM B
```

rather than tightly coupling every system to every other system.

The goal is to make individual systems replaceable and understandable.

---

# 11. GAMEPLAY AUTHORITY

The client is not authoritative over persistent gameplay.

Anything affecting meaningful game state must ultimately be validated and resolved by the server-side game logic.

This includes areas such as:

* combat
* progression
* economy
* item generation
* loot
* quest rewards
* world-state changes
* character progression

Client-side calculations may be used for presentation or responsiveness, but they must not become the source of truth.

Refer to `TECHNICAL_ARCHITECTURE_SPEC.md` for implementation requirements.

---

# 12. PERSISTENCE

The game is persistent.

Player accounts and their game state must survive:

* closing the application
* leaving the game
* changing devices
* reconnecting
* normal application updates

The architecture supports multiple character/playthrough states while maintaining strict account ownership.

Persistent world state and character-specific state are conceptually separate.

---

# 13. SHARED WORLD VS CHARACTER KNOWLEDGE

The world has an objective state independent of what an individual character knows.

A character may:

* know something
* suspect something
* have heard a rumour
* have discovered evidence
* remain unaware of an event

The player's UI and Journal should reflect the character's knowledge rather than simply exposing the complete world state.

This distinction is important to the three-perspective narrative structure.

---

# 14. ITEMS AND EQUIPMENT

The item system distinguishes between authored item definitions and individual generated item instances.

The project supports deep equipment progression and generated statistics.

Items should therefore be treated as data-driven game objects rather than hard-coded UI objects.

The detailed item-generation, equipment and loot rules belong to:

`EQUIPMENT_LOOT_SPEC.md`

Inventory ownership and management belong to:

`INVENTORY_ITEM_MANAGEMENT_SPEC.md`

Do not duplicate item-generation logic inside inventory or UI code.

---

# 15. COMBAT

Combat is a core gameplay system rather than merely a presentation layer.

The combat engine should be implemented independently from the combat UI.

The same underlying combat rules should support normal PvE combat and the optional duel simulator.

The UI presents combat results; it should not contain the authoritative combat rules.

Refer to `COMBAT_SPEC.md` and `SKILLS_ABILITIES_SPEC.md`.

---

# 16. DUEL SYSTEM

The optional duel feature is a simulation rather than a transition to multiplayer gameplay.

Its purpose is to allow two players to compare their developed characters.

Duels:

* do not become part of the normal campaign
* do not create a shared world
* do not create a player economy
* do not alter the participating characters
* should operate using isolated character snapshots
* should reuse the normal combat engine

The duel system should remain architecturally separate from the core single-player gameplay loop while sharing the underlying combat rules.

---

# 17. TECHNICAL ARCHITECTURE

The initial technical target is Bolt.

The intended architecture is broadly:

```text
Bolt
  ↓
Web Application
  ↓
Server/Game Logic
  ↓
PostgreSQL Database
  ↓
Persistent Game State
```

The application is designed to be mobile-first while remaining usable on desktop.

The backend should remain relatively simple initially.

Avoid introducing:

* microservices
* dedicated game servers
* unnecessary external infrastructure
* distributed systems
* complex caching
* other infrastructure that does not solve an actual project requirement

The technical architecture should remain sufficiently modular that individual infrastructure components can be replaced later if necessary.

---

# 18. DATABASE AND DATA MODEL

The database is relational and PostgreSQL-based.

Use relational structures for stable entities and relationships.

Flexible JSON/JSONB structures may be used where appropriate, but should not replace proper relational modelling when data requires frequent querying, relationships or integrity enforcement.

The data model should clearly distinguish:

* account-owned state
* character/playthrough state
* item instances
* authored content
* shared world state
* character knowledge

---

# 19. SECURITY MODEL

Assume that the client can be manipulated.

Never rely on:

* hidden UI controls
* disabled buttons
* client-side validation
* obscured identifiers

as the primary security mechanism.

Server-side validation and account ownership protection are required.

A player must never gain access to another player's private game state simply by manipulating requests.

The duel system is the controlled exception and must expose only the minimum information required for an approved duel.

---

# 20. AI CODING PRINCIPLES

The project is specifically designed to be understandable to an AI coding agent.

When implementing anything:

1. Identify the relevant specification.
2. Read the relevant specification before modifying behaviour.
3. Identify the system that owns the rule.
4. Identify the data affected.
5. Identify the server-side operation required.
6. Identify the UI that presents the result.
7. Identify dependencies on other systems.
8. Add or update tests where appropriate.
9. Preserve existing behaviour outside the requested change.

Do not invent mechanics simply because something seems like a conventional RPG feature.

Do not silently reinterpret established design decisions.

If a requirement is genuinely ambiguous, ask for clarification rather than inventing a new rule.

---

# 21. SPECIFICATION AUTHORITY

The repository's specification documents are the authoritative design source.

Current specifications include:

* `ACCOUNT_PERSISTENCE_SPEC.md`
* `CHARACTER_FOUNDATION_SPEC.md`
* `COMBAT_SPEC.md`
* `ENEMY_BOSS_SPEC.md`
* `EQUIPMENT_LOOT_SPEC.md`
* `INVENTORY_ITEM_MANAGEMENT_SPEC.md`
* `JOURNEY_DUNGEON_SPEC.md`
* `NPC_FACTION_SPEC.md`
* `PROGRESSION_ECONOMY_SPEC.md`
* `QUEST_JOURNAL_SPEC.md`
* `SKILLS_ABILITIES_SPEC.md`
* `STORY_NARRATIVE_SPEC.md`
* `TECHNICAL_ARCHITECTURE_SPEC.md`
* `UI_UX_SPEC.md`
* `WORLD_EXPLORATION_SPEC`

These documents collectively define the game design and implementation requirements.

When working on a feature, the coding agent should read the relevant specification rather than relying only on this context document.

---

# 22. CHANGE DISCIPLINE

Do not modify established systems unnecessarily.

A change requested for one feature should not result in unrelated redesign of other systems.

Before changing an established rule:

* identify the specification that owns it
* check dependencies
* determine whether the change affects other systems
* update the appropriate specification if the design itself has changed

Code should implement the specifications, not silently become a new source of design decisions.

---

# 23. IMPLEMENTATION STYLE

Prefer:

* clear TypeScript/types where applicable
* small functions
* explicit data structures
* predictable naming
* modular domain logic
* reusable services
* isolated UI components
* clear database relationships
* straightforward code
* testable game logic

Avoid unnecessary abstraction for its own sake.

The primary goal is code that another AI agent can understand reliably several development phases later.

---

# 24. UI PRINCIPLES

The application is mobile-first.

The interface should prioritise:

* readability
* clear hierarchy
* touch-friendly interaction
* fast navigation
* information density without clutter
* meaningful feedback
* clear presentation of complex RPG systems

UI components should present game state rather than becoming the source of game rules.

Refer to `UI_UX_SPEC.md` for detailed interface requirements.

---

# 25. CONTENT ARCHITECTURE

The game is intended to expand through authored content rather than constant rewrites of core systems.

The architecture should make it practical to add:

* enemies
* bosses
* items
* equipment
* abilities
* quests
* locations
* dungeons
* NPCs
* factions
* Story Bites
* encounters
* world events

without rewriting unrelated systems.

Where appropriate, content should be data-driven.

---

# 26. TESTING MINDSET

Game logic should be testable independently from the UI.

Important systems should be capable of deterministic or controlled testing where practical.

Particular attention should be given to:

* combat
* progression
* item generation
* loot
* economy
* quests
* world-state changes
* character state
* duel simulations

Do not rely exclusively on manually clicking through the UI to verify game rules.

---

# 27. CURRENT DEVELOPMENT PHILOSOPHY

The project should be developed incrementally.

Do not attempt to implement the entire RPG in one step.

Build a small functional foundation first, then progressively add systems while keeping the architecture coherent.

Each implementation phase should:

* build on the existing foundation
* remain testable
* avoid unnecessary scope expansion
* preserve established design
* leave the application in a usable state

---

# 28. IMPORTANT AGENT BEHAVIOUR

When asked to implement a feature:

**Do not assume.**

First determine:

```text
What is being changed?
        ↓
Which specification owns it?
        ↓
What existing systems does it touch?
        ↓
What data changes?
        ↓
What server operation is required?
        ↓
What UI changes?
        ↓
What tests are required?
```

If the requested implementation conflicts with an existing specification, stop and identify the conflict rather than silently choosing one interpretation.

If the requested feature is already defined elsewhere in the repository, use the existing specification rather than creating a parallel design.

---

# 29. FINAL PRINCIPLE

This project is being built from a deliberately separated set of specifications.

The AI coding agent should therefore treat the repository as a **design system**, not merely a collection of prompts.

The specifications define the game.

This document provides the shared context.

The code implements the specifications.

The AI agent's role is to connect those three layers without inventing new game design unnecessarily.

When in doubt:

**Read the relevant specification first.**
