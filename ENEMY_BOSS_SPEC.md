ENEMY & BOSS SYSTEM SPECIFICATION
Document: ENEMY_AND_BOSS_SPEC Version: 0.1 Status: Active Design Purpose: Defines enemies, enemy archetypes, enemy statistics, enemy scaling, encounters, elite enemies, bosses and deterministic enemy behaviour.
 
⸻
 
1. DESIGN ROLE
Enemies are the primary opposing force in the RPG’s automated combat system.
Enemy design should provide depth through:
distinct mechanical identities
meaningful strengths and weaknesses
stat interactions
abilities
resistances
encounter composition
scaling
specialised counters
bosses with bespoke mechanics
Difficulty should not simply mean:
“Give the enemy more HP and damage.”
Enemies should instead create different problems that interact with the player’s build.
 
⸻
 
2. RELATIONSHIP TO PLAYER BUILDS
The player develops without a permanent class.
Enemy design therefore must support a wide range of player builds.
A character’s effectiveness against an enemy can depend on:
attributes
weapon
weapon proficiency
equipment
abilities
penetration
resistances
status effects
Story Relic
combat strategy
Enemies should therefore create opportunities for different builds to excel.
 
⸻
 
3. ENEMY ARCHETYPES
Enemies are built from archetypes rather than being completely independent collections of statistics.
An archetype establishes an enemy’s intended mechanical identity.
Possible archetype categories include:
offensive
defensive
fast
ranged
support
control
status-focused
high-health
high-defence
glass-cannon
summoner
The final canonical archetype catalogue is TBD.
Archetypes should be data-driven so new enemy types can be introduced without modifying the core combat engine.
 
⸻
 
4. ENEMY STATISTICS
An enemy may possess:
Maximum Health
Attack Power
Defence
Accuracy
Evasion
Critical Chance
Critical Damage
Attack Speed
resistances
status-effect power
status-effect resistance
other explicitly defined statistics
An enemy does not need to possess every possible statistic.
Statistics should only exist where they contribute to the enemy’s mechanical identity.
 
⸻
 
5. SPECIALISED ELITE ENEMIES
Elite enemies are stronger versions of ordinary enemies with a single specialised archetype.
An Elite should have:
increased statistics
one specialised archetype
any abilities associated with that archetype
altered resistances or weaknesses where appropriate
improved rewards
potential special loot opportunities
The specialised archetype defines the Elite’s primary mechanical identity.
Examples include:
High-Defence Elite
Tests:
Defence Penetration
raw offensive power
alternative damage mechanics
Fast Elite
Tests:
Accuracy
defensive statistics
attack-speed interactions
Status Elite
Tests:
status resistance
cleansing
burst damage
interrupting the enemy before effects accumulate
Defensive Elite
Tests:
sustained damage
penetration
appropriate counter abilities
An Elite should not combine multiple specialised archetypes unless that combination is explicitly authored as a boss or other exceptional encounter.
Elites should not simply be ordinary enemies with inflated HP.
The exact Elite-generation model is TBD.
 
⸻
 
6. DEFENCE SPECIALISTS
High-Defence enemies are an intentional combat niche.
The game should contain enemies whose Defence is sufficiently high relative to ordinary player offensive power that they create a meaningful problem.
This makes:
Defence Penetration
a genuine build consideration rather than a minor stat that is useful against everything equally.
The player may therefore encounter specialised High-Defence Elites that strongly reward penetration-focused builds.
 
⸻
 
7. ENEMY WEAKNESSES
Enemies should be capable of having meaningful weaknesses.
A weakness may involve:
low Defence
low resistance
vulnerability to a damage type
vulnerability to a status effect
susceptibility to a weapon mechanic
conditional vulnerability
a boss-specific mechanic
Weaknesses should be authored rather than universally inferred from an enemy’s archetype.
 
⸻
 
8. ENEMY RESISTANCES
Enemies can possess resistance to relevant effects.
Resistance interacts with combat according to the general Combat specification.
In particular:
resistance reduces status intensity
resistance reduces status duration
resistance does not automatically purge an already-applied effect
An enemy may be highly resistant to one effect while remaining vulnerable to another.
 
⸻
 
9. ENEMY SCALING
Enemy scaling must be controlled.
The game should avoid unrestricted exponential scaling where every statistic grows dramatically with level.
Scaling should maintain meaningful differences between:
player level
enemy level
enemy archetype
encounter difficulty
Elite status
The precise scaling formula is TBD.
 
⸻
 
10. SCALING LIMITS
Scaling should have explicit limits.
Enemy scaling must not be allowed to produce:
arbitrary stat explosions
effectively infinite Defence
unreachable hit chances
permanently invalidated player builds
runaway HP values without corresponding gameplay purpose
Where scaling curves are used, they should include deliberate caps or diminishing returns where appropriate.
 
⸻
 
11. ENEMY LEVEL
Enemies have an effective level used for progression and scaling.
Enemy level can influence:
base statistics
reward value
XP
loot
encounter difficulty
The exact relationship between enemy level and each of these systems is defined by their respective specifications.
 
⸻
 
12. ENEMY POWER
Enemy level is not necessarily a complete representation of difficulty.
Two enemies of the same level can have substantially different difficulty because of:
archetype
statistics
abilities
resistances
mechanics
Elite status
encounter composition
Therefore:
Enemy Level ≠ Enemy Difficulty
 
⸻
 
13. NORMAL ENEMIES
Normal enemies are designed around relatively understandable mechanics.
Their behaviour should generally be:
predictable
deterministic
inexpensive to simulate
appropriate for repeated encounters
Normal enemies should not require bespoke AI for every individual creature.
 
⸻
 
14. ELITE IDENTIFICATION
An Elite must be clearly distinguishable in the UI.
The player should be able to recognise that an enemy is substantially different from an ordinary enemy before or during combat.
The Elite’s specialised archetype should also be communicated where appropriate, allowing the player to understand the type of threat it presents.
The exact presentation is a UI decision.
 
⸻
 
15. BOSS DESIGN
Bosses are authored encounters rather than merely stronger ordinary enemies.
A boss may have:
unique statistics
unique abilities
phases
thresholds
scripted behaviour
conditional attacks
special resistances
special vulnerabilities
unique status effects
bespoke mechanics
Bosses are intended to be memorable encounters.
Bosses are not limited to the single-specialisation rule used by Elite enemies.
 
⸻
 
16. BOSS PHASES
A boss can transition between phases.
A phase transition can occur when:
HP reaches a threshold
a timer/event occurs
a specific mechanic is completed
another explicitly authored condition occurs
Phase changes may modify:
abilities
behaviour
statistics
targeting
resistances
attack patterns
The exact phase architecture remains TBD.
 
⸻
 
17. BOSS SPECIAL ATTACKS
Boss abilities do not have to obey the ordinary basic-attack formula.
A boss attack may explicitly:
use normal damage calculation
partially bypass Defence
completely bypass Defence
deal fixed damage
apply a status effect
alter combat state
trigger another boss mechanic
This allows bosses to challenge specific builds without requiring enormous numerical scaling.
 
⸻
 
18. BOSS MECHANICS
Boss mechanics should generally create a problem that the player can understand from the available information.
A mechanic should ideally have:
Problem
   ↓
Recognisable signal
   ↓
Build / preparation interaction
   ↓
Deterministic resolution
Bosses should not rely on hidden information to create difficulty.
 
⸻
 
19. BOSS SCRIPTING
Boss behaviour may be scripted.
A scripted boss can follow a sequence such as:
Phase 1
 ↓
Ability A
 ↓
Basic attacks
 ↓
Ability B
 ↓
HP threshold
 ↓
Phase 2
 ↓
Ability C
 ↓
Enrage / final phase
The sequence must remain deterministic.
Random variation may exist only where it is generated through the game’s deterministic combat state.
 
⸻
 
20. ENEMY AI
Enemy AI is intentionally simple.
Ordinary enemies and Elite enemies use the following behaviour:
Perform their basic attack repeatedly.
Track each attack and ability independently.
Use each attack or ability as soon as it becomes available.
Continue using all available attacks and abilities independently as their cooldowns expire.
Repeat this behaviour until combat ends.
Enemy attacks and abilities do not use a shared priority rotation unless explicitly authored as part of a boss mechanic.
An enemy does not wait for another ability before using an available ability.
An enemy does not choose between abilities through complex tactical decision-making.
This creates a predictable automated combat model while allowing enemies to differ through:
statistics
attack frequency
cooldowns
ability effects
resistances
specialised archetypes
boss-specific rules
 
⸻
 
21. TARGET SELECTION
Enemy target selection is an authored behaviour.
For ordinary enemies and Elites, the default target is the player character.
If an encounter contains multiple valid targets, the target-selection rule must be explicitly defined by the encounter or enemy definition.
Possible authored rules include:
attack the player
target the highest or lowest relevant statistic
target a specific combat role
select a target randomly using deterministic randomness
use a conditional target rule
The exact target-selection catalogue is TBD.
Target selection should not require general-purpose tactical AI.
 
⸻
 
22. DETERMINISTIC AI
Enemy behaviour is deterministic.
Given identical:
enemy state
player state
encounter state
combat state
deterministic seed
the enemy makes the same decisions.
For ordinary enemies and Elites, this means that each attack and ability follows its own cooldown and becomes available according to the same combat timeline every time.
This is important for:
server authority
reproducibility
debugging
balancing
anti-cheat
combat simulation
 
⸻
 
23. ENCOUNTERS
An encounter consists of one or more enemies.
An encounter defines:
enemies
enemy levels
composition
rewards
difficulty
special conditions
potential boss or Elite state
The encounter itself is data-driven.
 
⸻
 
24. ENCOUNTER COMPOSITION
Multiple enemies can be combined to create encounters with complementary mechanics.
For example:
Front-line defensive enemy
+
Support enemy
+
Offensive enemy
can create a substantially different challenge from three identical offensive enemies.
Encounter composition is therefore a major difficulty tool.
A single Elite should contribute one specialised archetype to the encounter rather than combining several Elite specialisations.
 
⸻
 
25. ENCOUNTER DIFFICULTY
Encounter difficulty should consider more than the sum of enemy statistics.
Important factors include:
enemy count
enemy synergy
abilities
resistances
control mechanics
damage output
defensive mechanics
healing/support
target selection
Elite status
specialised archetype
boss mechanics
This allows relatively modest individual enemies to create challenging encounters through composition.
 
⸻
 
26. REWARDS
Enemy and encounter difficulty contributes to:
XP
gold
loot
special rewards
Reward calculations belong to the Progression and Loot systems.
The Enemy system supplies the necessary enemy and encounter information.
Elites should generally provide improved rewards relative to comparable normal enemies.
Boss rewards are defined separately from ordinary Elite rewards.
 
⸻
 
27. LOOT RELATIONSHIP
Enemies may reference loot tables.
The enemy definition should not directly contain a hard-coded list of every possible item.
Instead:
Enemy
  ↓
Loot Table
  ↓
Item Generation
  ↓
Generated Item
This allows the same loot-generation engine to be reused across:
enemies
chests
quests
journeys
bosses
special events
 
⸻
 
28. BOSS LOOT
Bosses can reference specialised loot tables.
Boss loot may contain:
normal generated equipment
Epic equipment
Legendary items
Story-related items
other authored rewards
Legendary and Story items remain authored rather than being produced through ordinary quality-based generation.
 
⸻
 
29. REPEATABLE ENCOUNTERS
The system should support repeatable encounters.
Repeated encounters must not require generating new bespoke game logic.
Their outcomes can vary through:
deterministic loot generation
player build changes
encounter state
progression
authored variation
 
⸻
 
30. CONTENT DATA MODEL
Conceptually:
Enemy Definition
 ├── ID
 ├── Name
 ├── Archetype
 ├── Elite State
 ├── Base Statistics
 ├── Scaling Profile
 ├── Resistances
 ├── Attacks
 ├── Abilities
 ├── Cooldowns
 ├── Target Rule
 ├── Loot Table
 └── Special Rules
Boss:
Boss Definition
 ├── Base Definition
 ├── Phases
 ├── Phase Conditions
 ├── Special Abilities
 ├── Scripts / State Machine
 ├── Target Rules
 ├── Loot Table
 └── Special Rules
These should be configuration/data structures rather than logic duplicated throughout the game.
For ordinary enemies and Elites, the combat engine should independently track each attack and ability cooldown.
 
⸻
 
31. IMPLEMENTATION PRINCIPLE
Adding a new ordinary enemy should ideally require:
Creating an enemy definition.
Selecting an archetype.
Defining statistics and scaling.
Selecting attacks and abilities.
Defining cooldowns.
Defining the target rule, if different from the default.
Assigning a loot table.
Adding a new Elite should additionally require:
Marking the enemy as Elite.
Selecting exactly one specialised archetype.
Defining Elite stat modifications.
Defining any archetype-specific abilities, resistances or weaknesses.
Assigning Elite rewards or loot modifications.
Adding a boss may additionally require:
Defining phases.
Defining transitions.
Defining bespoke abilities.
Defining scripted behaviour.
Defining unique rewards.
The core combat engine should not need modification for ordinary enemy or Elite content additions.
 
⸻
 
32. DESIGN INVARIANTS
Enemies are data-driven.
Enemy level is not synonymous with difficulty.
Enemy archetypes provide mechanical identities.
Elite enemies have a single specialised archetype.
High-Defence enemies are an intentional archetype.
Defence Penetration provides a meaningful counter to high Defence.
Enemy statistics should scale in a controlled manner.
Enemy scaling must not invalidate player builds through unrestricted numerical growth.
Ordinary enemy and Elite AI is simple and deterministic.
Enemies repeatedly perform their basic attacks.
Each enemy attack and ability operates independently on its own cooldown.
Available attacks and abilities are used as soon as they come off cooldown.
Ordinary enemies and Elites do not require complex tactical AI.
Bosses can use bespoke deterministic behaviour.
Bosses may use phases.
Boss abilities may use specialised damage or mechanical rules.
Encounter composition is a major difficulty mechanism.
Enemy behaviour is deterministic.
Enemy outcomes are server-authoritative through the Combat system.
Loot is generated through shared loot-generation systems.
Legendary items remain authored special items.
Story items remain authored special items.
Adding normal enemy or Elite content should not require modifying core combat logic.
 
⸻
 
33. OPEN PARAMETERS
These require explicit design decisions before implementation:
Canonical enemy archetype list
Canonical specialised Elite archetype list
Enemy base-stat formulas
Enemy level scaling
Enemy-to-player level scaling
Enemy difficulty scaling
Elite generation
Elite stat modifiers
Elite reward modifiers
Target-selection rules
Enemy attack catalogue
Enemy ability catalogue
Enemy cooldown rules
Enemy resistance catalogue
Boss phase rules
Boss scripting model
Encounter difficulty calculation
Enemy XP calculation
Enemy gold calculation
Enemy loot-table structure
Boss loot rules
Repeatable encounter rules
These are intentionally not invented.
 
⸻
 
34. DEPENDENCIES
Depends on
Character Foundation
Combat System
Skills & Abilities
Equipment & Loot
Progression
Journey System
Used by
Combat
Journeys
Dungeons
Story
Loot
Progression
UI
 
⸻
 
END OF SPECIFICATION
