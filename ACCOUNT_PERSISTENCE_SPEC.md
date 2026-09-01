ACCOUNT & PERSISTENCE SYSTEM SPECIFICATION
Document: ACCOUNT_AND_PERSISTENCE_SPEC Version: 0.2 Status: Design Locked Purpose: Defines player accounts, the three canonical protagonists, persistent world state, character progression, server-authoritative saves, multi-device continuity, death persistence, recovery and the relationship between character knowledge and shared world state.
 
⸻
 
1. DESIGN PHILOSOPHY
The game is a persistent, server-backed web application.
A player’s progression is associated with their account rather than a particular device.
The intended experience is:
Device A
   ↓
Login
   ↓
Persistent Account
   ↓
Character + World State
   ↓
Device B
   ↓
Continue playing
There are no traditional manually managed save files.
The server is the authoritative source of persistent game state.
 
⸻
 
2. ACCOUNT STRUCTURE
One player account contains access to all three canonical protagonists.
ACCOUNT
│
├── FOREST PROTAGONIST
├── COASTAL PROTAGONIST
└── MOUNTAIN PROTAGONIST
Each protagonist has independent character progression and personal knowledge.
The three protagonists nevertheless exist within the same persistent canonical world.
 
⸻
 
3. THE THREE CANONICAL PROTAGONISTS
The game contains exactly three playable canonical protagonists:
Forest Protagonist
Beginning in the forest/village environment and eventually becoming involved with the kingdom and its military.
Coastal Protagonist
Beginning in coastal street life and progressing through the merchant world and its associated conflicts.
Mountain Protagonist
Beginning as a blacksmith apprentice and progressing into the dwarven/mountain setting and its associated conflicts.
These protagonists are not customisable character templates that the player creates.
Their identities, backgrounds and narrative roles are authored parts of the game.
 
⸻
 
4. ADDITIONAL PLAYTHROUGHS
Players may create additional character slots for replaying the canonical protagonists.
A replay does not create a new protagonist identity.
For example:
Account
 ├── Forest — Playthrough 1
 ├── Forest — Playthrough 2
 ├── Coastal — Playthrough 1
 └── Mountain — Playthrough 1
Each playthrough has independent progression.
The system must therefore distinguish:
Protagonist Definition
from
Character Instance / Playthrough
 
⸻
 
5. SHARED WORLD
All protagonists inhabit the same canonical world.
Major world events are shared.
If one protagonist causes or advances a canonical world event, the resulting world state is reflected when another protagonist plays within that same world.
Example:
Mountain protagonist
        ↓
Discovers major threat
        ↓
World Event advances
        ↓
Shared World State changes
        ↓
Coastal protagonist later encounters
the consequences
The game does not create three independent versions of the world.
 
⸻
 
6. WORLD STATE VS CHARACTER STATE
The architecture must maintain a strict distinction between:
Shared World State
What has actually happened in the canonical world.
Character State
What a particular protagonist has personally experienced.
Character Knowledge
What that protagonist currently knows.
These are not interchangeable.
 
⸻
 
7. EXAMPLE OF SHARED EVENT KNOWLEDGE
Suppose a major mining crisis becomes active.
The shared world may contain:
MOUNTAIN_MINING_CRISIS = ACTIVE
The mountain protagonist may know:
The mines are under attack.
The forest protagonist may know:
The army is concerned about weapons shortages.
The coastal protagonist may know:
Mountain shipments have stopped.
All three are observing the same canonical event from different perspectives.
 
⸻
 
8. CHARACTER KNOWLEDGE IS INDEPENDENT
Knowledge does not automatically transfer between protagonists.
If the mountain protagonist discovers a secret, the coastal protagonist does not automatically know that secret.
This applies to:
Journal entries
Story Bites
discovered mysteries
NPC information
historical discoveries
location knowledge
quest information
 
⸻
 
9. NO ACCOUNT-WIDE GAMEPLAY PROGRESSION
Gameplay progression is not shared between protagonists.
The following remain character/playthrough-specific:
level
XP
attributes
skills
equipment
inventory
gold
quests
Journal
Story Bites
character relationships
character-specific discoveries
character-specific progression
There are no account-wide gameplay advantages between protagonists.
 
⸻
 
10. NO ACCOUNT-WIDE COSMETIC PROGRESSION
Cosmetic unlocks are also not automatically shared between protagonists.
Each playthrough is intended to remain narratively and mechanically independent.
 
⸻
 
11. NO ACCOUNT-WIDE LORE PROGRESSION
Discovering lore with one protagonist does not automatically populate another protagonist’s Journal.
This preserves the game’s intended three-perspective narrative structure.
The player may personally understand a connection that the active protagonist does not.
That distinction is intentional.
 
⸻
 
12. CHARACTER PLAYTHROUGH STRUCTURE
Each playthrough should conceptually contain:
CHARACTER INSTANCE
│
├── Protagonist Definition
├── Level / XP
├── Stats
├── Skills
├── Equipment
├── Inventory
├── Currency
├── Quest State
├── Journal State
├── Knowledge State
├── Character Relationships
└── Character-Specific Flags
 
⸻
 
13. WORLD STRUCTURE
The persistent world should conceptually contain:
WORLD
│
├── Global Story State
├── World Events
├── Regional States
├── Faction States
├── NPC States
├── World Discoveries
└── Canonical World Flags
 
⸻
 
14. WORLD EVENT OWNERSHIP
A world event belongs to the shared world, not to a particular protagonist.
The protagonist may be responsible for advancing the event, but the resulting world state is canonical.
Example:
Character:
mountain_playthrough_01

Action:
Complete "Investigate the Deep Mine"

Result:
DEEP_MINE_THREAT → ESCALATING

Storage:
WORLD STATE
The event should not simply be stored as:
mountain_playthrough_01.deep_mine_threat = true
unless that flag specifically represents the character’s knowledge.
 
⸻
 
15. CHARACTER KNOWLEDGE OF WORLD EVENTS
A character can separately store their knowledge of an event.
Example:
WORLD:
DEEP_MINE_THREAT = ESCALATING

MOUNTAIN:
knowledge.deep_mine_threat = CONFIRMED

FOREST:
knowledge.deep_mine_threat = RUMOUR

COASTAL:
knowledge.deep_mine_threat = UNKNOWN
This is essential to the narrative architecture.
 
⸻
 
16. AUTHENTICATION
The game requires an authenticated account for persistent progression.
Authentication should preferably be delegated to a secure authentication service rather than implementing raw password management inside the game.
The final provider is an implementation decision.
The game backend receives an authenticated account identity and associates game data with it.
 
⸻
 
17. MULTI-DEVICE ACCESS
The same account can be accessed from multiple supported devices.
Supported targets are expected to include:
desktop browsers
laptop browsers
tablets
mobile browsers
The game should not require manual save-file transfer.
 
⸻
 
18. SIMULTANEOUS SESSIONS
Multiple simultaneous sessions are permitted.
For example:
Desktop
   │
   ├── Account
   │
Mobile
   │
   └── Same Account
The system must protect persistent state against conflicting operations.
 
⸻
 
19. CONCURRENT CHARACTER PLAY
Because simultaneous sessions are permitted, the architecture must support situations such as:
Device A → Forest protagonist
Device B → Coastal protagonist
These can operate concurrently provided their actions are valid.
If two sessions attempt to modify the same shared world state, the server must resolve the operations authoritatively.
 
⸻
 
20. CONCURRENT WORLD OPERATIONS
Shared-world modifications require transaction/conflict handling.
For example:
Session A
   ↓
World Event → ACTIVE

Session B
   ↓
World Event → RESOLVED
The server determines the valid resulting state according to the event’s progression rules.
The client must never determine the final world state itself.
 
⸻
 
21. SERVER AUTHORITY
The server is authoritative over all progression-critical state.
The client cannot independently determine:
XP
level
stats
item acquisition
item properties
gold
quest completion
Story Bite discovery
Journal progression
world-event progression
faction progression
death penalties
combat results
 
⸻
 
22. SAVE MODEL
Progression is saved automatically.
Players do not manually save the game.
Important state changes should be persisted as part of the operation that caused them.
Examples:
Complete quest → save
Finish combat → save
Acquire loot → save
Equip item → save
Discover Story Bite → save
Advance world event → save
Respawn after death → save
 
⸻
 
23. ATOMIC GAME OPERATIONS
Progression-changing operations should be atomic where practical.
Example:
QUEST COMPLETION
       ↓
Validate
       ↓
Grant XP
       ↓
Grant gold
       ↓
Grant items
       ↓
Update quest
       ↓
Unlock Story Bite
       ↓
Update Journal
       ↓
Apply world effects
       ↓
Commit
Either the operation succeeds consistently or the persistent state remains unchanged.
 
⸻
 
24. DUPLICATE REQUEST PROTECTION
Important operations must protect against duplicate execution.
This includes protection from:
double clicks
network retries
browser refreshes
mobile reconnection
client bugs
repeated API requests
A player must not receive duplicate quest rewards because the same operation was submitted twice.
 
⸻
 
25. TRANSACTION IDENTIFIERS
Progression-changing requests should support unique operation/request identifiers where appropriate.
Conceptually:
operation_id = unique identifier
The server can recognise that an operation has already been processed.
 
⸻
 
26. CHARACTER PROGRESSION
Character progression is persistent and playthrough-specific.
At minimum:
Level
XP
Attributes
Skills
Equipment
Inventory
Gold
Quest State
Journal State
Knowledge State
Story Progression
 
⸻
 
27. INVENTORY PERSISTENCE
Inventory is persistent.
The server stores individual item instances and quantities.
An item instance can include:
Item ID
Template ID
Level
Generated Stats
Quality
Equipped State
Protection State
The player’s visible representation may hide some underlying item properties.
 
⸻
 
28. EQUIPMENT PERSISTENCE
Equipped equipment persists between sessions.
The previously established rule remains:
Equipped items are never lost through the normal death penalty.
 
⸻
 
29. SPARE ITEM PERSISTENCE
Spare equipment held in the bag is persistent but can be subject to the established death-loss rules.
This distinction is important:
Equipped Item
→ Protected

Spare Bag Item
→ Potentially at risk
 
⸻
 
30. ITEM RARITY PROTECTION
The established protection rules remain:
Epic, Legendary and Story items are never at risk of being lost through the death mechanic.
This applies regardless of whether the item is equipped or is a spare item in the bag.
 
⸻
 
31. GOLD PERSISTENCE
Gold is persistent character state.
The established death penalty remains:
20% of gold is lost on death.
The percentage is flat throughout the game.
 
⸻
 
32. DEATH STATE
Death does not immediately apply the death penalty.
Instead:
ACTIVE
  ↓
DEFEATED
  ↓
RESPAWN
  ↓
DEATH PENALTY
  ↓
PERSIST
  ↓
ACTIVE
The exact player interaction during the DEFEATED state belongs to the Death/Combat specification.
 
⸻
 
33. DEATH TRANSACTION
When the player respawns, the death consequences should be processed atomically.
Conceptually:
RESPAWN
 ↓
Determine gold loss
 ↓
Determine at-risk spare items
 ↓
Apply losses
 ↓
Restore character to valid active state
 ↓
Persist
The server must ensure the same death cannot be processed twice.
 
⸻
 
34. QUEST PERSISTENCE
Quest state is stored per character/playthrough.
Persistent data includes:
available quests
active quests
completed quests
failed quests
objective progress
choices
quest consequences
 
⸻
 
35. JOURNAL PERSISTENCE
Journal state is stored per character/playthrough.
This includes:
Story Bites
Journal entries
updated entries
discovered people
discovered places
factions
historical information
mysteries
The Journal represents character knowledge rather than the complete objective world state.
 
⸻
 
36. WORLD DISCOVERY
World discovery is primarily character-specific.
If the mountain protagonist discovers a dungeon, this does not automatically mean that the forest protagonist has discovered it.
The underlying location nevertheless exists in the shared world.
 
⸻
 
37. NPC STATE
NPCs can have shared world state and character-specific relationship/knowledge state.
For example:
WORLD:
NPC exists
NPC is alive
NPC has changed location

CHARACTER:
Relationship = FRIEND
Knowledge = KNOWN
Quest interaction = COMPLETE
The implementation must distinguish these scopes.
 
⸻
 
38. FACTION STATE
Factions can have shared world state while individual characters can have different relationships with them.
Example:
WORLD:
Dwarven faction → Mining crisis

MOUNTAIN:
Dwarven reputation → High

COASTAL:
Dwarven reputation → Unknown
 
⸻
 
39. STORY FLAGS
Story flags must have explicit scope.
Possible scopes:
GLOBAL
WORLD
REGION
FACTION
NPC
CHARACTER
A flag must never accidentally become global merely because it was stored in a convenient location.
 
⸻
 
40. STORY PROGRESSION
Main-story progression is character-specific unless the relevant event is explicitly a shared-world event.
This allows:
Mountain:
Chapter 4

Forest:
Chapter 2

Coastal:
Chapter 3
while still maintaining:
Shared World Event:
ACTIVE
 
⸻
 
41. CANONICAL WORLD TIMELINE
The shared world has a canonical sequence of major events.
Character stories intersect with this timeline at different points.
The player can therefore experience the same event from multiple perspectives.
 
⸻
 
42. JOURNAL KNOWLEDGE
The Journal does not automatically reflect the entire canonical timeline.
A character records only what they have:
experienced
discovered
been told
inferred
learned through gameplay
This preserves narrative mystery.
 
⸻
 
43. CHARACTER KNOWLEDGE AFTER REPLAY
When replaying a protagonist through a new character slot, the new playthrough begins with that protagonist’s normal narrative knowledge.
It does not inherit the previous playthrough’s discoveries.
This prevents previous knowledge from breaking story progression.
 
⸻
 
44. COMPLETED CAMPAIGN
When the main campaign reaches its final narrative state, that campaign ends.
There is no intended infinite post-story world state.
The player can retain the completed character and replay the campaign through another character/playthrough slot.
 
⸻
 
45. POST-CAMPAIGN STATE
A completed playthrough is retained as completed historical state.
It should not continue advancing the canonical story after the final campaign conclusion.
 
⸻
 
46. CHARACTER SLOT MODEL
Conceptually:
ACCOUNT
│
├── PLAYTHROUGH
│    ├── Protagonist = Forest
│    └── State
│
├── PLAYTHROUGH
│    ├── Protagonist = Coastal
│    └── State
│
└── PLAYTHROUGH
     ├── Protagonist = Mountain
     └── State
The number of replay slots should be configurable.
 
⸻
 
47. ACCOUNT DELETION
Account deletion should eventually be supported.
The implementation must consider:
authentication deletion
gameplay data
backups
audit records
privacy requirements
legal retention requirements
Exact retention policy is an implementation/production decision.
 
⸻
 
48. ADMINISTRATIVE RECOVERY
Administrators must have controlled tools for correcting serious progression problems.
Possible recovery operations include:
restoring an earlier character state
correcting inventory
correcting gold
correcting XP
correcting quest state
correcting world-state errors
Administrative actions must be authenticated and audited.
 
⸻
 
49. ROLLBACK
Administrative rollback is supported.
The system should maintain sufficient historical information to restore a player’s state following a serious server-side error.
Rollback should not be an ordinary player-facing feature.
 
⸻
 
50. AUDIT TRAIL
Important economy and progression operations should be auditable.
Examples:
GOLD +100
Source: QUEST_REWARD
Character: X
Quest: Y
Timestamp: Z
ITEM REMOVED
Reason: DEATH_PENALTY
Character: X
Item: Y
Timestamp: Z
WORLD EVENT ADVANCED
Event: DEEP_MINE_THREAT
From: ACTIVE
To: ESCALATING
Triggered By: CHARACTER_ACTION
Timestamp: Z
 
⸻
 
51. DATA VERSIONING
Persistent data must be versioned.
Game updates must be capable of migrating older player data to newer schemas.
Conceptually:
Save Schema v1
      ↓
Migration
      ↓
Save Schema v2
Players should not lose progression because the game’s database schema changed.
 
⸻
 
52. CONTENT VERSIONING
Authored game content should also be version-aware where necessary.
This is particularly important for:
quests
Story Bites
item definitions
progression rules
world events
Persistent player state should reference stable IDs rather than relying on mutable display names.
 
⸻
 
53. STATIC CONTENT VS PLAYER STATE
The architecture must separate:
Static Game Content
Authored definitions:
protagonists
quests
Story Bites
items
item templates
NPCs
locations
factions
world events
Dynamic Player State
Generated through gameplay:
level
XP
inventory
equipment
quest progress
Journal
knowledge
relationships
choices
 
⸻
 
54. STATIC CONTENT VS SHARED WORLD STATE
There is a third important category:
Dynamic World State
Examples:
event progression
NPC state
faction state
regional conditions
global story flags
Thus the complete architecture separates:
STATIC CONTENT
      +
PLAYER STATE
      +
WORLD STATE
 
⸻
 
55. CLIENT/SERVER ARCHITECTURE
The conceptual architecture is:
WEB CLIENT
    ↓
AUTHENTICATED API
    ↓
GAME SERVER
    ↓
GAME LOGIC
    ↓
DATABASE
The client is responsible for presentation and interaction.
The server is responsible for authoritative game logic and persistence.
 
⸻
 
56. CLIENT CACHING
The client may cache static or safely reproducible content.
Examples:
item definitions
NPC descriptions
location descriptions
Story Bite text
UI assets
Mutable authoritative state remains server controlled.
 
⸻
 
57. OFFLINE MODE
The initial game does not require offline authoritative gameplay.
An internet connection is required for progression-changing operations.
Local caching may still be used for:
faster loading
static content
UI performance
temporary resilience during brief connection interruptions
 
⸻
 
58. CONNECTION INTERRUPTION
If the connection is interrupted:
the client should detect the loss
pending operations should be safely recoverable where possible
operations must not be duplicated
authoritative state remains on the server
the player should be returned to a consistent state
The design must account for mobile network instability.
 
⸻
 
59. PERFORMANCE
The game should not write to the database for every UI interaction.
Examples:
Open inventory
→ No persistent write required

Change inventory tab
→ No persistent write required

Equip item
→ Persist

Complete combat
→ Persist

Complete quest
→ Persist

Discover Story Bite
→ Persist

Advance world event
→ Persist
 
⸻
 
60. SECURITY
The system must enforce:
authenticated requests
authorisation
input validation
server-side calculations
rate limiting where appropriate
transaction integrity
The client must never be trusted to supply authoritative progression totals.
 
⸻
 
61. ANTI-CHEAT PRINCIPLE
The server calculates or validates progression-critical outcomes.
The client should not be trusted for:
damage
loot
gold
XP
item generation
quest completion
death results
world-event advancement
 
⸻
 
62. DESIGN INVARIANTS
One account can contain all three canonical protagonists.
There are exactly three canonical protagonist identities.
Additional playthroughs use character slots rather than custom protagonists.
Each playthrough has independent gameplay progression.
The three protagonists inhabit one canonical shared world.
Major world events are shared.
Character knowledge is independent.
One protagonist’s Journal does not automatically populate another’s.
Gameplay progression is not account-wide.
Cosmetic progression is not account-wide.
Lore progression is not account-wide.
Multiple simultaneous sessions are permitted.
Concurrent shared-world changes are server-authoritative.
Progression is automatically persisted.
There are no manually managed save files.
Important progression operations are atomic.
Duplicate requests cannot duplicate rewards.
The server is authoritative over progression.
Equipped items are never lost through normal death.
Epic, Legendary and Story items are never at risk.
Spare bag items can be subject to death loss according to the established rules.
Gold loss on death is a flat 20%.
Death enters a temporary DEFEATED state before respawn processing.
Death penalties are applied atomically during respawn.
Quest state is character-specific.
Journal state is character-specific.
Character discovery is character-specific.
World events are shared.
World state and character knowledge are separate.
NPC and faction state can contain both shared and character-specific components.
Story flags have explicit scopes.
Replayed characters do not inherit previous playthrough knowledge.
The campaign ends at its final narrative state.
Completed campaigns do not continue advancing the main story.
Administrative rollback is supported.
Important progression/economy operations are auditable.
Persistent data is versioned.
Content and player state are separate.
Static content, player state and world state are distinct architectural layers.
The client is not an authority over game state.
The system is designed for persistent web access across multiple device types.
Offline authoritative progression is not required for the initial release.
 
⸻
 
63. DEPENDENCIES
Depends on
Authentication
Character System
Combat
Equipment
Inventory
Loot
Economy
Quest
Journal
World
NPCs
Factions
Used by
Entire game
Account system
Character selection
Save system
Server API
UI
Administration
Analytics
Recovery systems
 
⸻
 
64. IMPLEMENTATION NOTE
This specification intentionally does not lock the project to a specific database, authentication provider, hosting provider or backend framework.
Those decisions belong in the later Technical Architecture Specification, where they can be selected based on the chosen vibe-coding platform and the requirements of the complete game.
The architecture must, however, preserve the separation between:
ACCOUNT
CHARACTER / PLAYTHROUGH
CHARACTER KNOWLEDGE
SHARED WORLD
STATIC CONTENT
This separation is a core architectural requirement, not an implementation detail.
 
⸻
 
END OF SPECIFICATION
