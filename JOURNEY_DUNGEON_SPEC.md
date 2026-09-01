JOURNEY & DUNGEON SYSTEM SPECIFICATION
Document: JOURNEY_AND_DUNGEON_SPEC Version: 0.1 Status: Active Design Purpose: Defines the player’s primary exploration loop, journeys, regions, encounters, safe areas, dungeon progression, automated progression and journey failure.
 
⸻
 
1. DESIGN GOALS
The Journey system is the primary structure connecting the RPG’s:
story
exploration
automated combat
loot
XP
gold
equipment
progression
death
safe areas
persistent character development
The system should support a player experience where the character can continue progressing without requiring constant manual interaction.
The player makes meaningful decisions primarily through:
preparation
destination selection
equipment
abilities
build
risk management
progression choices
rather than manually controlling every combat action.
 
⸻
 
2. CORE JOURNEY LOOP
The fundamental gameplay loop is:
Safe Location
      ↓
Prepare Character
      ↓
Select Journey / Destination
      ↓
Enter Unsafe Region
      ↓
Encounter
      ↓
Automatic Combat
      ↓
Victory
      ↓
Rewards / Progression
      ↓
Next Encounter
      ↓
Continue Journey
      ↓
Reach Destination / Safe Location
If the character is defeated:
Unsafe Region
      ↓
Defeat
      ↓
Retreat to Previous Safe Location
      ↓
Apply Defeat Consequences
 
⸻
 
3. SAFE LOCATIONS
Safe locations are areas where the player can safely manage their character.
Safe locations provide the natural boundary between:
Preparation
and:
Risk.
The exact catalogue of safe-location types remains TBD.
Potential functions include:
equipment management
inventory management
consumable use
character management
story interaction
journey selection
recovery
other non-combat systems
 
⸻
 
4. UNSAFE REGIONS
Unsafe regions are areas where the character is exposed to journey risk.
While travelling through an unsafe region, the character can encounter:
normal enemies
elite enemies
bosses
story encounters
other authored events
Combat is resolved automatically.
 
⸻
 
5. JOURNEYS
A Journey represents an automated progression path through the world.
A Journey contains an ordered sequence of:
regions
encounters
events
destinations
The player begins the journey from a safe location.
The journey then progresses automatically.
 
⸻
 
6. AUTOMATIC PROGRESSION
Once a journey begins, the character automatically proceeds through the journey.
The player does not need to manually initiate every individual encounter.
Conceptually:
Start Journey
     ↓
Travel
     ↓
Encounter
     ↓
Resolve
     ↓
Reward
     ↓
Continue
     ↓
Next Encounter
This is the core idle/automated gameplay loop.
 
⸻
 
7. PLAYER INTERACTION DURING JOURNEYS
The system is designed so that the character can continue making progress without constant player interaction.
The player may return to the game and review:
progress
encounters
rewards
character development
equipment
journey status
failures
discovered content
The exact set of actions available while a journey is running remains TBD.
 
⸻
 
8. OFFLINE PROGRESSION
Journeys are conceptually capable of continuing while the player is offline.
The server maintains the authoritative journey state.
When the player returns:
Last Known Server State
        +
Elapsed Valid Journey Time
        ↓
Server Reconciliation
        ↓
Resolve Eligible Progress
        ↓
Updated Character State
The client must not independently simulate and submit arbitrary offline rewards.
 
⸻
 
9. SERVER RECONCILIATION
Offline/idle progression must be server-authoritative.
The server determines:
how much journey progress occurred
which encounters occurred
combat outcomes
rewards
loot
XP
gold
defeat
retreat
final journey state
The client displays the reconciled result.
 
⸻
 
10. JOURNEY STATE
A journey has an explicit state.
Conceptually:
NOT_STARTED
ACTIVE
COMPLETED
DEFEATED
PAUSED / INTERRUPTED
The final state catalogue is TBD.
A journey must be recoverable from persistent server state.
 
⸻
 
11. JOURNEY POSITION
A journey tracks the character’s current position within its progression.
Conceptually:
Journey
 ├── Region
 ├── Encounter Index
 ├── Event Index
 └── Destination
The exact representation is implementation-dependent.
The important requirement is that progress is persistent.
 
⸻
 
12. JOURNEY CONTINUATION
After successfully defeating an encounter, the character continues along the journey.
Victory does not automatically return the character to safety.
Instead:
Victory advances the journey.
This allows a sequence of encounters to form a continuous expedition.
 
⸻
 
13. JOURNEY COMPLETION
A journey completes when the character reaches its defined destination or final objective.
Completion may trigger:
story progress
rewards
access to a new safe location
access to new journeys
new encounters
new equipment opportunities
other authored progression
The exact reward catalogue remains part of the Story and Progression specifications.
 
⸻
 
14. DEFEAT
Normal defeat occurs when the character reaches zero Health.
The character does not permanently die.
Instead:
The character retreats to the previous safe location.
This is the fundamental failure state for ordinary journeys.
 
⸻
 
15. DEFEAT CONSEQUENCES
Normal defeat causes:
loss of gold
loss of eligible spare/unequipped inventory items
retreat to the previous safe location
Normal defeat does not cause:
XP loss
permanent character death
loss of story progress
loss of equipped items
 
⸻
 
16. GOLD LOSS
The gold-loss penalty on normal defeat is:
20% of the character’s gold.
This is a flat percentage throughout the entire game.
It does not increase with:
character level
journey difficulty
enemy level
location
progression
The system must not introduce progressive death-tax scaling.
 
⸻
 
17. ITEM LOSS
Normal defeat can cause loss of items from the player’s inventory.
Only:
spare items in the bag
are eligible.
Equipped items are never lost.
 
⸻
 
18. PROTECTED ITEMS
The following categories are never lost through ordinary defeat:
equipped items
Epic items
Legendary items
Story items / Story Relics
This protection applies even when those items are being carried as spare inventory.
 
⸻
 
19. ITEM-LOSS POOL
When calculating defeat item loss, the game considers only eligible spare items in the bag.
Conceptually:
Inventory
 ├── Equipped Items → PROTECTED
 ├── Epic Items → PROTECTED
 ├── Legendary Items → PROTECTED
 ├── Story Items → PROTECTED
 └── Other Spare Items → LOSS ELIGIBLE
The exact number/selection algorithm for eligible item loss is defined by the Inventory specification.
 
⸻
 
20. EQUIPPED ITEM PROTECTION
Equipment currently occupying an equipment slot is permanently protected from normal journey defeat.
This means the player’s active build cannot be destroyed by ordinary failure.
The player can therefore take meaningful risks without the possibility of losing the equipment currently defining their build.
 
⸻
 
21. STORY ITEM PROTECTION
Story-critical items are permanently protected.
A normal defeat cannot cause the player to lose:
Story Relics
required story objects
other items designated as story-critical
Story progression must therefore remain recoverable.
 
⸻
 
22. STORY PROGRESS PROTECTION
Normal defeat does not reverse story progress.
If the player has:
completed a quest
unlocked a story stage
discovered a location
defeated a required story enemy
ordinary defeat does not undo that progress.
 
⸻
 
23. EXPERIENCE PROTECTION
Normal defeat does not remove XP already earned.
The character retains their accumulated progression.
Therefore:
Death is a setback, not a rollback of character development.
 
⸻
 
24. BOSS CONSEQUENCES
Major bosses may have authored consequences beyond normal defeat.
A boss encounter may therefore behave differently from an ordinary encounter.
However:
Boss consequences must not permanently block completion of the game’s story.
The player must always retain a viable path to continue the main story.
 
⸻
 
25. RISK / REWARD PHILOSOPHY
The journey system intentionally creates a risk/reward relationship.
Entering unsafe territory exposes the player to:
enemy encounters
possible defeat
gold loss
possible spare-item loss
while also providing:
XP
gold
loot
equipment
story progress
exploration
access to new content
The player therefore balances:
How far can I safely push this journey?
against:
What can I gain by continuing?
 
⸻
 
26. SAFE-AREA RETURN
When defeated, the character returns to the previous safe location, not necessarily the original starting location of the entire game.
This creates meaningful geographical progression.
Safe locations therefore act as journey checkpoints.
 
⸻
 
27. CHECKPOINT PRINCIPLE
Unlocking or reaching a safe location effectively establishes a new fallback point.
Conceptually:
Safe Area A
    ↓
Unsafe Region
    ↓
Safe Area B
    ↓
Unsafe Region
    ↓
Safe Area C
If defeated between B and C:
Return to B.
This prevents failure from unnecessarily replaying the entire world.
 
⸻
 
28. DUNGEONS
Dungeons are specialised journey structures.
A dungeon consists of a sequence of encounters and/or events contained within a defined location.
A dungeon may contain:
normal enemies
elite enemies
environmental/story events
treasure
minibosses
boss encounters
a final objective
 
⸻
 
29. DUNGEON PROGRESSION
Dungeon progression is automated once the player commits to the dungeon journey.
The character progresses through its encounters in order.
A dungeon can therefore function as:
A structured expedition containing multiple sequential challenges.
 
⸻
 
30. DUNGEON FAILURE
Unless explicitly authored otherwise, dungeon defeat follows the standard journey defeat rules:
retreat to the previous safe location
lose 20% of gold
potentially lose eligible spare inventory items
retain XP
retain story progress
retain equipped items
retain Epic/Legendary/Story items
Boss-specific authored consequences may override portions of this behaviour where explicitly defined.
 
⸻
 
31. DUNGEON COMPLETION
Completing a dungeon may:
advance the story
unlock a safe location
unlock a new journey
grant a boss reward
unlock new content
provide progression rewards
The dungeon itself should be considered complete only when its authored completion condition has been satisfied.
 
⸻
 
32. JOURNEY EVENTS
Journeys are not restricted to combat.
A journey may contain authored non-combat events.
Examples include:
story scenes
discoveries
treasure
choices
merchants
environmental events
special encounters
The event system should be extensible.
 
⸻
 
33. STORY INTEGRATION
Story progression can be embedded into journeys.
A story journey can therefore combine:
Travel
 ↓
Story Event
 ↓
Combat
 ↓
Story Event
 ↓
Loot
 ↓
Combat
 ↓
Boss
 ↓
Story Resolution
This allows the RPG to retain a strong narrative structure without abandoning its automated gameplay model.
 
⸻
 
34. JOURNEY REWARDS
Successful journey progression may grant:
XP
gold
generated equipment
authored equipment
consumables
Story items
Story Relics
access to new content
The Loot and Progression specifications determine how rewards are generated.
 
⸻
 
35. CONSUMABLES
Consumables can only be used in safe areas.
Therefore consumables are not an unrestricted mid-combat or mid-journey recovery mechanism.
This intentionally reduces the frequency and importance of consumable use during ordinary journeys.
Consumable design belongs to the Inventory/Loot specification.
 
⸻
 
36. JOURNEY PREPARATION
Before entering an unsafe journey, the player should be able to prepare their character.
Preparation may include:
equipping equipment
changing abilities
reviewing statistics
managing inventory
using consumables
selecting the journey
reviewing relevant information
The exact preparation UI is a UI specification concern.
 
⸻
 
37. PERSISTENCE
Journey progress must be persistently saved server-side.
A player closing the application must not inherently reset an active journey.
The system should support:
application closure
device switching
reconnecting
offline periods
server reconciliation
without losing legitimate progress.
 
⸻
 
38. MULTIPLATFORM REQUIREMENT
The journey system must be independent of the presentation platform.
The same journey state must be usable by:
web
mobile
desktop
other supported clients
The server remains the source of truth.
 
⸻
 
39. ANTI-EXPLOIT REQUIREMENTS
The client must not be trusted to determine journey progression.
The server must validate:
journey start
journey state
elapsed time
encounter completion
combat result
reward generation
defeat
retreat
item loss
gold loss
This prevents manipulation of idle progression.
 
⸻
 
40. JOURNEY DATA MODEL
Conceptually:
Journey Definition
 ├── Journey ID
 ├── Starting Location
 ├── Destination
 ├── Regions
 ├── Encounters
 ├── Events
 ├── Completion Conditions
 └── Reward Rules
Player Journey State:
Player Journey
 ├── Journey ID
 ├── Current Region
 ├── Current Encounter/Event
 ├── Previous Safe Location
 ├── Start Time
 ├── Last Server Resolution
 ├── Current State
 └── Deterministic Progress State
The final database schema belongs to the Technical Architecture specification.
 
⸻
 
41. DESIGN INVARIANTS
Journeys are automated.
Journeys progress through unsafe regions.
Encounters are resolved through automated combat.
Victory advances the journey.
Journeys can continue conceptually while the player is offline.
Offline progression is reconciled by the server.
The server is authoritative for journey state.
Safe locations provide fallback/checkpoint locations.
Normal defeat retreats the character to the previous safe location.
Normal defeat removes 20% of gold.
The 20% gold loss remains flat throughout the entire game.
Normal defeat can remove eligible spare items from the bag.
Equipped items can never be lost through normal defeat.
Epic items can never be lost through normal defeat.
Legendary items can never be lost through normal defeat.
Story items/Story Relics can never be lost through normal defeat.
XP is never lost through normal defeat.
Story progress is never lost through normal defeat.
Major bosses may have authored consequences.
Boss consequences cannot permanently prevent story completion.
Consumables can only be used in safe areas.
Journeys can contain both combat and non-combat/story events.
Dungeons are structured specialised journeys.
Journey state is persistent.
Journey progression is platform-independent.
 
⸻
 
42. OPEN PARAMETERS
The following still require explicit definition:
Safe-location catalogue
Journey catalogue
Region structure
Journey timing
Encounter frequency
Travel-time calculation
Offline progression limits, if any
Journey interruption rules
Active-journey management
Multiple simultaneous journey rules
Exact item-loss algorithm
Dungeon-specific rules
Event catalogue
Story-event integration
Journey reward calculations
Checkpoint unlocking rules
Boss-specific journey consequences
These are deliberately left open rather than inventing rules.
 
⸻
 
43. DEPENDENCIES
Depends on
Character Foundation
Combat
Skills & Abilities
Enemy & Boss
Equipment & Loot
Inventory
Progression
Story
Used by
Core Game Loop
Story
Combat
Loot
Progression
Persistence
Offline Simulation
UI
 
⸻
 
END OF SPECIFICATION
