TECHNICAL ARCHITECTURE SPECIFICATION
Document: TECHNICAL_ARCHITECTURE_SPEC Version: 2.0 Status: Design Locked Purpose: Defines the technical architecture required to implement the RPG as a persistent, mobile-first web application using Bolt for application development, hosting and managed database infrastructure, with authoritative server-side game logic, persistent player accounts, shared world state, and an optional no-stakes PvP duel simulator.
 
⸻
 
1. ARCHITECTURAL OBJECTIVE
The game is a persistent, server-backed, single-player RPG delivered as a web application.
The architecture must support:
persistent player accounts
three canonical protagonists
multiple character/playthrough slots
persistent character progression
persistent shared world state
deep combat and progression systems
generated equipment and loot
quests and Journal/Story Bites
Journey and Dungeon systems
server-authoritative game calculations
mobile-first responsive UI
optional player-vs-player duel simulation
future expansion of authored game content
The architecture should remain relatively simple for the initial implementation while maintaining clean boundaries for future growth.
 
⸻
 
2. CORE TECHNOLOGY DIRECTION
The initial implementation is designed around:
                    BOLT
             ┌────────┴────────┐
             │                 │
        Web Application   Managed Backend
             │                 │
             │          ┌──────┴──────┐
             │          │             │
             │      PostgreSQL    Server Logic
             │          │             │
             └──────────┴─────────────┘
                        │
                        ↓
              Persistent Game State
Bolt is the initial development, hosting and backend environment.
The implementation should favour the capabilities of Bolt’s managed platform rather than introducing unnecessary external infrastructure.
The architecture should nevertheless keep the game domain logic and data structures sufficiently portable that the backend can be migrated to another PostgreSQL-based platform later if required.
 
⸻
 
3. INITIAL DEPLOYMENT PHILOSOPHY
The initial architecture should be:
Simple to build, but structured to scale.
Do not prematurely introduce:
microservices
dedicated game servers
message brokers
Kubernetes
complex distributed infrastructure
unnecessary caching layers
external backend services where Bolt already provides the required capability
The game does not require this complexity at launch.
However, code and data boundaries must allow individual infrastructure components to be replaced or separated later if the game grows substantially.
 
⸻
 
4. APPLICATION LAYERS
The system should conceptually separate into:
PRESENTATION
    ↓
CLIENT APPLICATION
    ↓
SERVER / APPLICATION LOGIC
    ↓
GAME LOGIC
    ↓
DATA ACCESS
    ↓
BOLT DATABASE
These boundaries should remain understandable even if Bolt implements several layers within the same project.
 
⸻
 
5. FRONTEND
The frontend is responsible for:
rendering the UI
navigation
user input
local UI state
temporary presentation state
loading states
error presentation
animations
responsive layouts
displaying server-authoritative results
The frontend must not be considered authoritative for gameplay.
 
⸻
 
6. CLIENT STATE
Client state should be divided into:
UI State
Examples:
selected tab
open modal
current filter
tooltip state
expanded item
scroll position
Cached Game State
Recently retrieved state used to render the interface.
Authoritative Game State
State confirmed by the server.
The client must clearly distinguish between these categories.
 
⸻
 
7. SERVER-AUTHORITATIVE GAME LOGIC
The server is authoritative for progression-critical calculations.
This includes:
combat outcomes
damage
healing
skill effects
XP
level progression
loot generation
item generation
item statistics
gold changes
purchases
quest rewards
quest completion
death penalties
world-event progression
NPC/faction state changes
Story Bite discovery
character progression
The client may predict or display calculations for responsiveness, but the server determines the final result.
 
⸻
 
8. BALANCED SERVER/CLIENT RESPONSIBILITY
The architecture uses a balanced approach.
Client
Suitable for:
UI calculations
display formatting
sorting
filtering
animation
visual transitions
non-authoritative derived presentation
Server
Required for:
anything affecting persistent progression
anything affecting the economy
anything affecting combat results
anything affecting item generation
anything affecting world state
anything that could be exploited for advantage
 
⸻
 
9. BOLT PLATFORM
Bolt provides the initial application hosting and managed backend environment.
The initial implementation should use Bolt-provided capabilities for:
application hosting
database
authentication where supported
server-side application logic
secrets/environment configuration
persistent game data
The project should avoid introducing Supabase or another external backend solely to recreate functionality already provided by Bolt.
The architecture should remain PostgreSQL-oriented so that the database layer remains portable.
 
⸻
 
10. DATABASE
The primary database is the PostgreSQL database provided through Bolt’s managed database infrastructure.
The database should be strongly relational while supporting JSON/JSONB fields where flexibility is genuinely useful.
This produces a hybrid model:
RELATIONAL STRUCTURE
        +
JSON/JSONB FLEXIBILITY
 
⸻
 
11. RELATIONAL DATA
Relational structures should be used for stable entities and relationships.
Examples:
accounts
characters
playthroughs
quests
locations
NPCs
factions
equipment
inventory
transactions
world events
progression records
Foreign keys and database constraints should be used where appropriate.
 
⸻
 
12. JSON DATA
JSON/JSONB fields may be used for flexible structures.
Examples include:
generated item stat sets
variable ability parameters
flexible narrative metadata
complex configuration
certain extensible game-state structures
JSON should not become a substitute for proper relational modelling.
If a value needs frequent querying, filtering, joining or integrity enforcement, it should generally receive an explicit database representation.
 
⸻
 
13. DATABASE SECURITY
Every player’s persistent data must be isolated.
Database-level security and server-side authorisation must enforce account-level access restrictions.
Conceptually:
PLAYER A
    ↓
Only PLAYER A data

PLAYER B
    ↓
Only PLAYER B data
A malicious client must not be able to retrieve or modify another player’s character data simply by changing an ID.
Where Bolt’s managed database provides database-level row security policies, those mechanisms should be used.
Where a particular Bolt database feature is not directly exposed, equivalent protection must be implemented through authenticated server-side access and explicit ownership checks.
Security must never rely solely on frontend filtering.
 
⸻
 
14. SERVER FUNCTIONS / SERVER ACTIONS
Server-side functions or equivalent Bolt server-side application operations provide the execution boundary for important game operations.
Examples:
resolveCombat()
generateLoot()
equipItem()
completeQuest()
purchaseItem()
processDeath()
advanceWorldEvent()
discoverStoryBite()
resolveDuel()
The exact function architecture is implementation-dependent.
The important requirement is that authoritative operations cannot be bypassed by manipulating the client.
 
⸻
 
15. TRANSACTIONAL OPERATIONS
Operations that modify multiple pieces of state should be processed transactionally where appropriate.
Example:
QUEST COMPLETION
      ↓
Validate
      ↓
Grant XP
      ↓
Grant Gold
      ↓
Grant Items
      ↓
Update Quest
      ↓
Unlock Story Bite
      ↓
Update World
      ↓
COMMIT
If the operation fails, partial progression should not be committed.
Use PostgreSQL transactions or equivalent transactional server-side mechanisms.
 
⸻
 
16. IDEMPOTENCY
Important operations must protect against duplicate execution.
For example, if a mobile connection causes a quest-completion request to be submitted twice, the player must not receive:
XP × 2
Gold × 2
Loot × 2
Operation/request identifiers should be used where appropriate.
Database constraints should be used where appropriate to make duplicate execution impossible rather than merely unlikely.
 
⸻
 
17. GAME CONTENT ARCHITECTURE
The game uses a hybrid content model.
Game Rules
Implemented as application/server logic.
Examples:
combat formulas
damage rules
loot algorithms
progression calculations
death rules
Authored Content
Stored as structured data.
Examples:
items
item templates
enemies
bosses
abilities
quests
Story Bites
NPCs
factions
locations
encounters
world events
This allows content to expand without rewriting the core game engine.
 
⸻
 
18. CONTENT IDENTIFIERS
Authored content should use stable IDs.
For example:
item_template_id
quest_id
npc_id
location_id
story_bite_id
enemy_id
ability_id
world_event_id
Display names must not be used as primary identifiers.
This allows names and descriptions to change without corrupting existing player data.
 
⸻
 
19. GENERATED ITEM ARCHITECTURE
The existing item system distinguishes:
ITEM TEMPLATE
      ↓
ITEM LEVEL
      ↓
QUALITY
      ↓
GENERATED POWER
      ↓
TEMPLATE ALLOCATION
      ↓
FINAL ITEM STATS
The underlying quality value remains hidden from the player.
The server must generate and persist the resulting item state authoritatively.
 
⸻
 
20. ITEM INSTANCE VS TEMPLATE
The architecture must distinguish between:
Item Template
Defines what an item fundamentally is.
Item Instance
Represents the specific copy owned by a player.
For example:
Iron Sword Template
        ↓
Player Item Instance
        ├── Level
        ├── Generated Stats
        ├── Quality
        └── Ownership
Two copies of the same template can therefore have different generated statistics.
 
⸻
 
21. CHARACTER DATA
A character/playthrough contains persistent state such as:
protagonist identity
level
XP
attributes
skills
equipment
inventory
gold
quest state
Journal state
knowledge
relationships
character-specific story state
campaign completion state
 
⸻
 
22. SHARED WORLD DATA
The shared world is stored independently from individual character progression.
It includes applicable:
world-event state
global story state
regional state
faction state
NPC state
canonical world progression
This separation is essential to the three-protagonist narrative structure.
 
⸻
 
23. CHARACTER KNOWLEDGE
Character knowledge is stored independently from objective world state.
Example:
WORLD
Mining Crisis = ACTIVE

MOUNTAIN
Knows = CONFIRMED

FOREST
Knows = RUMOUR

COASTAL
Knows = UNKNOWN
The UI should only expose information appropriate to the active character.
 
⸻
 
24. WORLD EVENT CONCURRENCY
The game is single-player, so simultaneous multiplayer world simulation is not required.
However, the same account may have multiple sessions or characters active simultaneously.
Shared-world mutations must therefore still be protected against conflicting requests.
Database transactions and appropriate locking/version checks should be used where necessary.
 
⸻
 
25. NO REAL-TIME GAMEPLAY REQUIREMENT
The core game does not require real-time networking.
Combat is not a real-time multiplayer system.
World exploration is not real-time multiplayer.
NPCs are not real-time multiplayer entities.
Therefore:
Real-time database synchronisation is not a core requirement.
The client can synchronise authoritative state at meaningful game operations.
 
⸻
 
26. OPTIONAL REAL-TIME FUNCTIONALITY
Bolt or a future backend may provide real-time functionality.
It should not be introduced merely because the platform supports it.
The initial game does not require:
real-time world synchronisation
real-time combat networking
persistent multiplayer simulation
Potential future uses could include:
duel invitations
social features
notifications
These are optional extensions.
 
⸻
 
27. SINGLE-PLAYER ARCHITECTURE
The fundamental game loop is:
ONE PLAYER
   ↓
ONE ACTIVE PLAYTHROUGH
   ↓
SERVER
   ↓
AUTHORITATIVE GAME STATE
Other players do not participate in the player’s campaign.
There is:
no shared cooperative campaign
no persistent competitive world
no player economy
 
⸻
 
28. OPTIONAL DUEL SYSTEM
The game includes an optional no-stakes PvP duel feature.
This is not traditional multiplayer combat.
It is a combat simulation allowing two players to compare their characters/builds.
Purpose:
Let players see which character would win in a simulated battle purely for fun.
 
⸻
 
29. DUEL PRINCIPLES
Duel outcomes have no gameplay consequences.
A duel must not modify:
HP
XP
level
equipment
inventory
gold
skills
quests
Journal
world state
death state
character progression
No items are consumed.
No equipment is damaged.
No death penalty occurs.
 
⸻
 
30. DUEL PARTICIPATION
A player may opt into a duel with another player.
Conceptually:
PLAYER A
Character Build
       │
       ├───────┐
               ↓
          DUEL SIMULATOR
               ↑
       ┌───────┘
       │
PLAYER B
Character Build
The system retrieves the relevant permitted character/build state and creates a temporary simulation.
 
⸻
 
31. DUEL SNAPSHOT
A duel should operate against a snapshot of the relevant character state.
This prevents the duel from accidentally modifying the live character.
Conceptually:
LIVE CHARACTER
      ↓
SNAPSHOT
      ↓
DUEL SIMULATION
      ↓
RESULT
      ↓
DISCARD SIMULATION
 
⸻
 
32. DUEL AUTHORITY
The duel simulation is server-authoritative.
The client cannot submit:
“I won.”
The server determines the result using the established combat system.
This ensures that the duel is a meaningful comparison of the actual RPG builds.
 
⸻
 
33. DUEL RESULT
The duel should provide an understandable result.
Potential information includes:
winner
loser
simulated combat duration/turns
damage dealt
major abilities used
important combat events
remaining simulated HP
relevant reason for victory
The full combat simulation may optionally be inspectable.
 
⸻
 
34. DUEL DETERMINISM
Where practical, duel simulations should use a controlled random seed.
This allows a particular simulation to be reproduced for debugging or review.
Conceptually:
Character A
Character B
Combat Rules
Random Seed
       ↓
Deterministic Simulation
       ↓
Result
 
⸻
 
35. DUEL INVITATIONS
The initial implementation may use a simple invitation flow.
Conceptually:
Player A
   ↓
Invite Player B
   ↓
Player B accepts
   ↓
Snapshot characters
   ↓
Run duel
   ↓
Display result
The invitation itself has no gameplay consequence.
The duel system must not require persistent real-time multiplayer infrastructure.
 
⸻
 
36. DUEL PRIVACY
Duel participation requires explicit player opt-in.
The system must not expose a player’s private character state to arbitrary users.
The duel system should expose only the information required to:
create the duel snapshot
execute the simulation
display the result
Potential privacy controls may include:
allow anyone
invitation only
disable duels
The exact social model can be refined separately if required.
 
⸻
 
37. DUEL DATA RETENTION
Duel simulations should not need to become permanent character history.
The initial architecture should retain only the minimum information required for:
displaying the result
debugging if required
abuse investigation if required
Permanent storage of every simulated combat is unnecessary unless later product requirements justify it.
 
⸻
 
38. AUTHENTICATION
Authentication is handled through the authentication capabilities of the Bolt application/backend architecture.
The application should never store raw passwords itself.
Authentication establishes:
AUTHENTICATED USER
      ↓
ACCOUNT ID
      ↓
GAME DATA
The implementation should use the platform’s supported authentication mechanism rather than creating a custom authentication system.
 
⸻
 
39. AUTHORISATION
Authentication and authorisation are separate concepts.
Being logged in does not automatically grant permission to:
modify another character
access another account
initiate an unauthorised duel
alter world state
access restricted server operations
Permissions must be enforced server-side.
 
⸻
 
40. API / SERVER ACTION DESIGN
Game operations should be exposed as explicit actions rather than allowing arbitrary database mutation from the client.
Conceptually:
resolveCombat
completeQuest
equipItem
purchaseItem
travel
createDuel
The exact mechanism may be:
server functions
server actions
API endpoints
another Bolt-supported server-side mechanism
The implementation should choose the simplest secure mechanism provided by Bolt.
Avoid giving the client unrestricted write access to gameplay tables.
 
⸻
 
41. READ VS WRITE ACCESS
A useful architectural distinction is:
Read
The client may retrieve authorised game state.
Write
Progression-changing writes should pass through validated game operations.
This reduces the attack surface and centralises game rules.
 
⸻
 
42. VALIDATION
All server operations must validate:
authenticated account
character ownership
current game state
prerequisites
resource availability
item ownership
ability availability
quest state
world state
operation validity
Never trust values supplied by the client simply because they appear plausible.
 
⸻
 
43. SECURITY
Security priorities include:
authentication
database-level ownership protection
server-side authorisation
input validation
transaction integrity
rate limiting where appropriate
protection against duplicate operations
protection against client-side manipulation
secure server secrets
 
⸻
 
44. ECONOMY SECURITY
Because the game contains a persistent economy, all economy-changing actions must be server authoritative.
This includes:
earning gold
spending gold
selling items
purchasing items
rewards
death penalties
any future economy mechanics
 
⸻
 
45. COMBAT SECURITY
Combat results must be calculated or validated server-side.
The client should provide the player’s intended action rather than the claimed result.
Example:
CLIENT:
"Use Ability X"

SERVER:
Validate ability
Validate state
Calculate outcome
Apply result
Persist result
Return outcome
 
⸻
 
46. LOOT SECURITY
The client must never determine its own loot.
The server determines:
whether loot is awarded
what loot is awarded
generated item properties
quantities
rarity/quality outcomes
applicable restrictions
 
⸻
 
47. DATABASE MIGRATIONS
Database schema changes must use versioned migrations wherever supported by the Bolt database workflow.
Development should not depend on manually editing production database structures.
Schema changes should be reproducible.
If Bolt’s managed database workflow changes how migrations are represented, the implementation should preserve the underlying principle of version-controlled, reproducible schema changes.
 
⸻
 
48. GAME DATA MIGRATIONS
Game-state changes may require migration logic.
Examples:
Old item structure
       ↓
Migration
       ↓
New item structure
Players must not lose progression because the game evolves.
 
⸻
 
49. CONTENT VERSIONING
Authored content should use stable IDs and versioning where required.
Changes to content must consider existing player state.
For example, changing the definition of an item template must not accidentally corrupt existing item instances.
 
⸻
 
50. ERROR HANDLING
The server should return structured errors.
The client translates these into player-friendly messages.
Example:
SERVER:
ITEM_REQUIREMENT_NOT_MET

CLIENT:
"You don't meet the requirements to equip this item."
Technical errors should not be exposed unnecessarily.
 
⸻
 
51. LOGGING
The backend should log important operational events where supported.
Examples:
authentication failures
server errors
failed game operations
economy changes
unusual combat requests
duel simulations
database failures
Logs support debugging but must not become the authoritative source of game state.
Do not build a comprehensive analytics or administration system for the initial game.
 
⸻
 
52. OBSERVABILITY
Initial implementation should use the monitoring and error-reporting capabilities naturally available through Bolt and the underlying application stack.
Do not introduce a separate observability platform unless a concrete need emerges.
Potential future capabilities include:
error monitoring
performance monitoring
database monitoring
server-function monitoring
application health monitoring
 
⸻
 
53. BACKUP & RECOVERY
Persistent player data must have reliable backup/recovery mechanisms appropriate to the capabilities of the managed Bolt database.
The architecture must support recovery from:
application bugs
database errors
failed migrations
accidental changes
serious data corruption
Where managed database backup functionality is provided by Bolt, use it.
If additional recovery requirements emerge, an external PostgreSQL backup strategy may be introduced later.
 
⸻
 
54. SCALABILITY
The architecture should initially scale through Bolt’s managed hosting and database infrastructure.
If the game grows substantially, individual workloads can later be separated.
Potential future scaling boundary:
Web Client
     ↓
Server / Game Functions
     ↓
PostgreSQL
Independent services should only be introduced where justified by actual requirements.
 
⸻
 
55. CACHING
Caching may be introduced for relatively static content.
Good candidates:
item templates
enemy definitions
ability definitions
location definitions
Story Bite content
other immutable authored content
Authoritative mutable player/world state should not rely on stale client caches.
 
⸻
 
56. STATIC ASSETS
Static visual assets should be delivered through Bolt’s hosting/CDN infrastructure where appropriate.
The application should avoid embedding large assets directly into database records.
 
⸻
 
57. PERFORMANCE PRINCIPLE
Optimise for the actual game rather than hypothetical scale.
The game is:
UI-driven
turn/state based
mostly asynchronous
not graphically intensive
not real-time multiplayer
This dramatically reduces infrastructure requirements compared with an action RPG or MMO.
 
⸻
 
58. OFFLINE BEHAVIOUR
Offline authoritative gameplay is not required.
The application may cache static information and provide appropriate offline/reconnection handling.
Progression-changing operations require server connectivity.
 
⸻
 
59. NETWORK FAILURE
The client should safely handle:
request timeout
connection loss
duplicate submission
server rejection
reconnection
A failed request must not leave the player believing that an operation succeeded when the server did not commit it.
Where an operation’s final state is uncertain, the client should re-query authoritative state rather than blindly retrying a potentially non-idempotent mutation.
 
⸻
 
60. ARCHITECTURAL BOUNDARIES
The following boundaries should remain explicit:
AUTHENTICATION
     │
ACCOUNT
     │
CHARACTER / PLAYTHROUGH
     │
GAME STATE
     │
WORLD STATE
     │
GAME RULES
     │
CONTENT DEFINITIONS
     │
UI
This structure is more important than specific folder names or framework conventions used by Bolt.
 
⸻
 
61. CORE DOMAIN MODULES
The implementation should maintain logical modules corresponding to the established specifications:
Account
Character
Combat
Skills
Equipment
Items
Loot
Inventory
Progression
Economy
Enemies
Bosses
Journey
Dungeons
World
Exploration
NPCs
Factions
Quests
Journal
Story
Persistence
Duels
These should remain modular even if some are implemented within shared files during early development.
 
⸻
 
62. CROSS-SYSTEM DEPENDENCY PRINCIPLE
Systems should interact through explicit operations rather than directly modifying each other’s internal state.
Example:
Combat
   ↓
Combat Result
   ↓
Progression
   ↓
XP Award
rather than:
Combat directly modifies
every character database field
This will make the system easier to test and modify.
 
⸻
 
63. DOMAIN LOGIC VS UI
Game rules must not depend on UI components.
For example:
BAD
Combat formula inside CombatScreen.
GOOD
Combat Engine
     ↓
Combat Result
     ↓
Combat Screen
This separation is especially important for the duel simulator, which must reuse the same combat rules without requiring the normal combat UI.
 
⸻
 
64. SHARED COMBAT ENGINE
The normal game combat system and duel system should use the same underlying combat rules.
             COMBAT ENGINE
              /          \
             /            \
       PVE COMBAT        DUEL
           │                │
      Persistent         Temporary
        Result             Result
The duel system must not create a second independent combat implementation.
 
⸻
 
65. GAME RULES AS REUSABLE SERVICES
Important mechanics should be represented as reusable functions/services.
Examples:
calculateDamage()
calculateDefence()
generateItem()
calculateItemPower()
calculateLoot()
awardXP()
processDeath()
resolveCombat()
resolveDuel()
Exact naming is implementation-dependent.
The principle is that one authoritative implementation of each important rule should exist.
 
⸻
 
66. TESTABILITY
Game logic should be callable independently of the UI.
This allows automated testing of:
combat
item generation
loot
progression
economy
quests
death
duel simulations
world events
The exact testing framework is implementation-dependent.
 
⸻
 
67. CONTENT EXPANSION
The architecture must make it practical to add:
new enemies
new bosses
new items
new abilities
new quests
new locations
new dungeons
new Story Bites
new NPCs
new factions
new world events
without rewriting unrelated systems.
 
⸻
 
68. VIBE-CODING COMPATIBILITY
The architecture must be understandable to an AI coding platform.
Avoid unnecessarily clever abstractions.
Prefer:
explicit modules
predictable naming
typed data structures
clear database schemas
small reusable functions
documented relationships
explicit business rules
isolated features
The codebase should be easy for an AI coding agent to reason about.
 
⸻
 
69. AI IMPLEMENTATION PRINCIPLE
When implementing a feature, the coding agent should be able to determine:
Which specification owns the rule?
Which database entities are affected?
Which server operation performs the mutation?
Which UI displays the result?
Which other systems depend on the result?
Which tests validate the behaviour?
This is one of the primary reasons the game has been divided into isolated specifications.
 
⸻
 
70. DEVELOPMENT ENVIRONMENTS
The project should have clear separation between:
development
testing/staging
production
Production data must not be casually modified during development.
If Bolt’s free environment does not provide fully independent environments, the implementation should use the safest practical separation available and avoid destructive development operations against production data.
 
⸻
 
71. SECRETS
Secrets and privileged credentials must remain server-side.
The frontend must never contain:
database administrative credentials
privileged API keys
private signing keys
server-only secrets
Only values explicitly intended for browser exposure may be included in client-side code.
 
⸻
 
72. DATA OWNERSHIP
Every persistent object should have an explicit ownership model.
For example:
Account
   ↓ owns
Playthrough
   ↓ owns
Character State
   ↓ owns
Inventory
   ↓ owns
Item Instances
Shared world entities should explicitly identify themselves as world-scoped rather than account-scoped.
 
⸻
 
73. MULTI-ACCOUNT ISOLATION
The database and server must enforce strict separation between accounts.
The architecture must assume that a malicious player will attempt to manipulate IDs or requests.
Security must therefore not depend solely on the frontend hiding another player’s records.
 
⸻
 
74. DUEL CROSS-ACCOUNT ACCESS
The duel system is the controlled exception where one player needs limited information about another player’s character.
The architecture must expose only the information required to perform/display the duel.
A player must not receive unrestricted access to another account’s private game state.
Conceptually:
PLAYER A
   ↓
Duel Permission
   ↓
Approved Character Snapshot
   ↓
Duel Engine
NOT:
PLAYER A
   ↓
Full access to PLAYER B database
 
⸻
 
75. DUEL ISOLATION
Duel simulation state should be temporary.
It must never accidentally reference mutable live inventory/equipment objects in a way that allows the duel to modify them.
Use immutable snapshots or equivalent isolated simulation data.
 
⸻
 
76. FUTURE SOCIAL FEATURES
The architecture should not assume that the duel feature means the game is becoming an MMO.
Potential future social features can be added independently if desired.
The core architecture remains single-player.
 
⸻
 
77. BACKEND PORTABILITY
Although Bolt is the initial backend platform, the game should avoid unnecessary coupling between game rules and Bolt-specific infrastructure.
The following should remain portable where practical:
PostgreSQL schema
game-domain models
game rules
item generation
combat engine
progression logic
content definitions
migration concepts
Platform-specific code should primarily exist at the infrastructure boundary.
Conceptually:
                 GAME DOMAIN
                     │
          ┌──────────┴──────────┐
          │                     │
     Game Rules             Content
          │
          ↓
     Data Access
          │
          ↓
   BOLT DATABASE LAYER
This provides an escape route if the project eventually moves to Supabase or another backend.
 
⸻
 
78. BOLT-SPECIFIC PRINCIPLE
Do not recreate infrastructure that Bolt already provides.
If Bolt provides a secure mechanism for:
authentication
database access
server-side functions
secrets
hosting
deployment
prefer that mechanism rather than adding an unnecessary external service.
At the same time, do not make game logic depend directly on proprietary platform behaviour when a standard PostgreSQL/application pattern can achieve the same result.
 
⸻
 
79. ARCHITECTURAL INVARIANTS
The game is fundamentally single-player.
The game is delivered as a persistent web application.
The architecture is mobile-first but supports desktop.
Bolt provides the initial application hosting and backend platform.
PostgreSQL provides persistent game data.
Server-side operations provide authoritative game operations.
Database-level and server-side security isolate player accounts.
Real-time synchronisation is not required for the core game.
The client is not authoritative.
Progression-critical calculations are server-authoritative.
Authored content is stored as structured data.
Core game rules are implemented as reusable logic.
Stable IDs are used for authored content.
Item templates and item instances are separate.
Character state and shared world state are separate.
Character knowledge and objective world state are separate.
Important multi-state mutations are transactional.
Important operations are protected against duplicate execution.
The same combat engine powers both PvE and duels.
Duels are optional.
Duels have no gameplay stakes.
Duels cannot modify persistent character state.
Duels operate on temporary character snapshots.
Duel outcomes are server-authoritative.
Duel access to another player’s character is explicitly controlled.
No player economy exists between accounts.
No cooperative campaign exists.
No real-time multiplayer game server is required.
Database schema changes use reproducible migrations.
Persistent data must support migration across game versions.
Production data must be protected from development operations.
Secrets remain server-side.
Administrative functionality is not required for the initial game.
The architecture should remain simple initially.
The architecture must preserve clean boundaries for future scaling.
Game logic must remain testable independently of the UI.
The codebase must remain understandable to an AI coding platform.
The architecture must support expansion of authored content without rewriting core systems.
Bolt-specific infrastructure should remain isolated from portable game-domain logic.
The backend should be replaceable if future requirements justify migration.
 
⸻
 
80. DEPENDENCIES
This specification consumes the established specifications for:
Account & Persistence
Quest & Journal
NPC & Faction
World & Exploration
Story & Narrative
Progression & Economy
Inventory & Item Management
Journey & Dungeon
Enemy & Boss
Skills & Abilities
Combat System
Character Foundation
Equipment & Loot
UI & UX
This specification provides the technical foundation for:
Testing & Balance
Build Phases
Vibe-Coding implementation
A comprehensive Analytics/Admin/Operations subsystem is not required for the initial implementation.
 
⸻
 
81. NEXT IMPLEMENTATION DOCUMENT
The next practical document is:
PROJECT_CONTEXT.md
This will provide Bolt with a concise AI-facing overview of the project without duplicating the full individual specifications.
It will establish:
what the game is
the major systems
architectural boundaries
critical invariants
project structure
implementation principles
the current development phase

⸻
 
END OF SPECIFICATION
