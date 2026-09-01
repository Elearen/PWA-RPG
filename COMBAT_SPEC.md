COMBAT SYSTEM SPECIFICATION
Document: COMBAT_SPEC Version: 0.1 Status: Active Design Purpose: Defines the core combat model, combat resolution principles, damage, defence, status effects, penetration, combat timing and boss behaviour.
 
⸻
 
1. DESIGN GOALS
Combat should be:
Deep mechanically
Easy to understand at the UI level
Primarily automatic rather than requiring constant player input
Deterministic
Build-driven
Stat-driven
Capable of supporting substantial equipment and skill interactions
Suitable for a persistent, server-authoritative RPG
Suitable for UI-based presentation without requiring complex graphics
The complexity should come from:
character builds
equipment
weapon choice
abilities
enemy mechanics
stat interactions
status effects
encounter composition
rather than requiring twitch gameplay.
 
⸻
 
2. COMBAT MODEL
Combat is primarily an automated simulation.
Once combat begins, the game resolves actions according to the character’s:
statistics
equipment
weapon
skills
abilities
status effects
enemy statistics
enemy behaviour
combat rules
The player does not need to manually execute every basic attack.
The combat UI should communicate what is happening through a readable combat log and meaningful state indicators.
 
⸻
 
3. DETERMINISM
Combat must be reproducible.
The same:
character state
enemy state
equipment
abilities
encounter state
combat seed/state
must produce the same combat result.
Random-looking outcomes may exist, but they must be generated deterministically.
The implementation should therefore use a deterministic pseudo-random mechanism rather than relying on uncontrolled client-side randomness.
 
⸻
 
4. SERVER AUTHORITY
Combat outcomes are authoritative on the server.
The client may display and animate combat events, but it must not be trusted to determine:
damage
hits
criticals
status effects
loot
death
rewards
XP
item loss
The server calculates the authoritative result.
 
⸻
 
5. COMBAT STATE
A combat instance contains, at minimum:
Combat ID
Encounter ID
Combat Seed / Deterministic State

Combatants
    ├── Character
    └── Enemy / Enemies

Current Time / Combat Tick
Action State
Health State
Resource State
Status Effects
Cooldown State
Temporary Modifiers

Combat Result
Rewards
The exact database representation belongs to the technical architecture specification.
 
⸻
 
6. COMBATANTS
A combatant has:
current health
maximum health
offensive statistics
defensive statistics
speed/timing statistics
accuracy-related statistics
critical-related statistics
resistances
active status effects
available abilities
cooldowns
resource state
The precise statistic catalogue is defined by the Character, Skills and Enemy specifications.
 
⸻
 
7. ACTION RESOLUTION
Combat proceeds through discrete actions/events.
An action may be:
basic attack
special attack
ability
status-effect application
status-effect tick
defensive action
enemy ability
other explicitly defined combat event
The combat engine resolves each event in a deterministic order.
 
⸻
 
8. ATTACK RESOLUTION
A conventional attack follows a sequence conceptually equivalent to:
Determine acting combatant
        ↓
Select action
        ↓
Determine target
        ↓
Resolve hit/accuracy
        ↓
Resolve critical
        ↓
Calculate effective offensive power
        ↓
Apply penetration/modifiers
        ↓
Resolve target defence/resistance
        ↓
Calculate final damage
        ↓
Apply damage
        ↓
Apply secondary effects
        ↓
Update combat state
The exact sequence may differ for abilities that explicitly define alternate behaviour.
 
⸻
 
9. ACCURACY & EVASION
Accuracy/evasion are separate concepts.
An attacker’s Accuracy is compared against the target’s relevant avoidance statistic.
The exact formula is:
TBD
The system should avoid a pure binary “accuracy above evasion = always hit” model unless explicitly chosen later.
The final system should define:
hit chance
minimum hit chance
maximum hit chance
whether guaranteed hits exist
whether guaranteed misses exist
modifiers
boss exceptions
 
⸻
 
10. CRITICAL HITS
Critical hits are a distinct combat outcome.
The system must eventually define:
Critical Chance
Critical Damage
minimum/maximum critical chance
critical modifiers
guaranteed critical effects
anti-critical effects
Exact formulas remain:
TBD
Critical Damage is intended to be meaningfully distinct from normal damage.
 
⸻
 
11. DAMAGE TYPES
The final game may support multiple damage types.
Any damage type must have a clear mechanical identity.
Damage types should not be introduced solely for naming variety.
The final catalogue of damage types and associated resistances is:
TBD
 
⸻
 
12. PHYSICAL DAMAGE
Physical attacks generally interact with the target’s:
Defence
Physical damage should therefore normally pass through the Defence-resolution system before final damage is applied.
The exact formula remains TBD.
 
⸻
 
13. DEFENCE
Defence reduces incoming physical damage.
Defence is a core defensive statistic.
It should not simply create an all-or-nothing armour check.
The final damage-reduction relationship must be:
monotonic
predictable
resistant to runaway scaling
useful throughout progression
Exact formula:
TBD
 
⸻
 
14. DEFENCE PENETRATION
Defence Penetration is an offensive mechanic that reduces the effectiveness of the target’s Defence.
Penetration should be treated separately from raw Attack Power.
It is intended to be especially valuable against enemies whose Defence is unusually high relative to the attacker’s offensive power.
This supports specialised anti-armour builds.
 
⸻
 
15. HIGH-DEFENCE SPECIALISATION
The game explicitly supports the concept of builds that specialise in fighting enemies with extremely high Defence.
This is a meaningful combat niche rather than simply a larger version of ordinary Attack Power.
The final specification must define:
flat penetration
percentage penetration
penetration ordering
penetration caps
whether penetration can reduce effective Defence below zero
interaction with enemy special Defence mechanics
Exact formulas remain TBD.
 
⸻
 
16. ATTACK SPEED / COMBAT TIMING
Combat is time-based rather than simply alternating turns.
Combatants have an attack/action timing characteristic.
Attack Speed determines how frequently a combatant can perform applicable actions.
The exact timing model remains TBD.
The implementation should support:
different attack speeds
ability cooldowns
status durations
temporary speed modifiers
slow/haste effects
simultaneous or near-simultaneous events
 
⸻
 
17. COMBAT EVENT ORDER
When multiple events occur at effectively the same time, the engine must use a deterministic ordering rule.
The final ordering must be explicitly defined.
Potential priority categories include:
Pre-action effects
Action
Damage
On-hit effects
Death checks
Post-action effects
Periodic status effects
The exact canonical order is:
TBD
This is important because event ordering can materially affect outcomes.
 
⸻
 
18. HEALTH
Every combatant has:
Maximum Health
Current Health
Damage reduces Current Health.
When Current Health reaches zero:
The combatant is defeated.
The exact maximum-health formula from Vitality and other modifiers belongs to the Character/Combat specifications.
 
⸻
 
19. OVERKILL
Damage beyond the target’s remaining Health does not continue to reduce Health below zero.
Conceptually:
Final Health = max(0, Current Health - Damage)
The system may record overkill internally for statistics, but it has no additional combat effect unless explicitly defined.
 
⸻
 
20. DEATH CHECK
After every damaging event, the combat engine checks whether the target has been defeated.
Death must be resolved before subsequent events that require the target to remain alive.
The exact interaction between simultaneous events is determined by the canonical combat event-ordering rule.
 
⸻
 
21. HEALING
Healing restores Current Health.
Healing cannot normally increase Current Health above Maximum Health.
The exact healing formula and healing modifiers remain:
TBD
 
⸻
 
22. STATUS EFFECTS
Status effects are first-class combat mechanics.
Examples may include:
damage-over-time
healing-over-time
slow
haste
defensive reduction
offensive reduction
crowd-control effects
other authored effects
The final status-effect catalogue belongs in the Skills/Abilities and Enemy specifications.
 
⸻
 
23. STATUS EFFECT INTENSITY
Status effects use a deterministic effectiveness relationship between:
Effect Power
and:
Relevant Resistance
The conceptual relationship is:
Effectiveness = Effect Power / (Effect Power + Resistance)
This creates diminishing returns.
As resistance increases:
effect intensity decreases
the effect becomes less effective
As Effect Power increases:
effect intensity increases
the effect approaches, but does not exceed, its natural maximum
 
⸻
 
24. STATUS EFFECT DURATION
Resistance affects both:
intensity
duration
A high resistance therefore does not merely make an effect weaker; it also reduces how long it persists.
The exact duration formula remains TBD.
 
⸻
 
25. STATUS RESISTANCE
There is no universal:
Status Resistance
statistic.
Each status effect uses an appropriate resistance.
For example, a hypothetical effect may use:
Physical Resistance
Mental Resistance
Fire Resistance
Poison Resistance
depending on the eventual damage/effect taxonomy.
The resistance used by an effect is explicitly defined by that effect.
 
⸻
 
26. STATUS EFFECT REMOVAL
Resistance affects newly calculated effect strength and duration.
Resistance does not actively purge an already-applied status effect.
Once an effect has been applied:
It naturally expires according to its calculated duration.
An increase in resistance after application does not automatically remove it.
A dedicated cleanse/removal ability may remove it if explicitly designed to do so.
 
⸻
 
27. STATUS EFFECT STACKING
Repeated applications of the same status effect do not create arbitrary independent stacks.
Instead, the effect is treated as one continuously recalculated effect.
Additional applications contribute to the existing effect.
The system therefore avoids:
Poison x1
Poison x2
Poison x3
Poison x4
...
as a universal stacking model.
Instead, the effect state is recalculated according to its authored stacking behaviour.
 
⸻
 
28. STATUS EFFECT COEXISTENCE
Different status effects coexist by default.
Applying Effect B does not automatically remove Effect A.
There are no universal cancellation rules.
If two effects interact, that interaction must be explicitly authored.
Examples of explicit interactions could include:
one effect modifying another
one effect consuming another
one effect amplifying another
one effect preventing another
These interactions are data-defined rather than globally assumed.
 
⸻
 
29. RESOURCE SYSTEM
The final combat resource model is:
TBD
Potential resources may include:
mana
stamina
energy
rage
another custom resource
No resource should be implemented merely because it is traditional RPG convention.
A resource should exist only if it creates meaningful gameplay.
 
⸻
 
30. ABILITIES
Abilities are combat actions with explicitly authored rules.
An ability may:
deal damage
heal
apply status effects
modify statistics
alter timing
interact with equipment
alter combat state
trigger other defined effects
Ability design is specified separately in:
SKILLS_AND_ABILITIES_SPEC.md
The combat engine must nevertheless support arbitrary deterministic ability resolution.
 
⸻
 
31. ENEMY AI
Ordinary enemies should use relatively simple deterministic behaviour.
An ordinary enemy may have:
preferred attack
target-selection rule
ability priority
threshold behaviour
status interactions
The system should avoid unnecessary complex AI.
The challenge should primarily come from enemy statistics, abilities and encounter design.
 
⸻
 
32. BOSS AI
Bosses may have significantly more sophisticated deterministic behaviour.
Bosses can have:
phases
thresholds
special attacks
scripted sequences
conditional abilities
unique targeting
environmental mechanics
authored status interactions
Boss behaviour is content-driven.
A boss can therefore have bespoke mechanics without requiring the entire enemy system to become unnecessarily complicated.
 
⸻
 
33. BOSS SPECIAL ATTACKS
A boss special attack can define its own resolution method.
It may:
use normal Attack Power vs Defence
use another offensive statistic
use a different formula
deal fixed damage
bypass Defence
partially bypass Defence
apply a unique status effect
interact with specific resistances
use another explicitly authored deterministic rule
There is no requirement that every boss attack obey the normal basic-attack formula.
 
⸻
 
34. ENEMY DIFFICULTY
Difficulty should primarily emerge from:
enemy statistics
enemy composition
abilities
resistances
mechanics
encounter design
Rather than simply giving every enemy enormous numerical scaling.
High-level enemies should remain mechanically understandable.
 
⸻
 
35. COMBAT LOG
The UI should provide a readable combat history.
The log should communicate meaningful events such as:
attacks
hits/misses
criticals
damage
healing
status applications
status expiration
ability use
major enemy mechanics
deaths
The underlying combat event stream should be richer than the UI necessarily displays.
 
⸻
 
36. PLAYER CONTROL
The player should primarily influence combat through preparation and build configuration rather than constant manual input.
Important decisions occur before combat through:
equipment
abilities
skills
attributes
Story Relic
journey preparation
If active combat choices are introduced later, they must preserve the game’s suitability for UI-driven and idle/automated gameplay.
 
⸻
 
37. COMBAT RESULT
A completed combat produces an authoritative result containing, as applicable:
victory/defeat
remaining Health
remaining resources
status effects
cooldown state
XP
loot
gold
progression effects
journey state
Rewards are calculated by the server.
The client displays the result but does not determine it.
 
⸻
 
38. COMBAT SEEDING
Each combat should have deterministic state sufficient to reproduce its results.
Conceptually:
Character State
+
Enemy State
+
Encounter ID
+
Journey ID
+
Combat ID
+
Deterministic Seed
=
Reproducible Combat
The exact seed-generation algorithm belongs to the technical specification.
 
⸻
 
39. EXPLOIT RESISTANCE
Because combat is authoritative and deterministic:
clients must not submit damage values
clients must not submit loot results
clients must not submit hit results
clients must not submit XP rewards
clients must not submit death outcomes
The client submits player-authorised commands where applicable.
The server validates and resolves the resulting state.
 
⸻
 
40. DESIGN INVARIANTS
The following are hard combat principles:
Combat is deterministic.
Combat is server-authoritative.
Basic combat is primarily automated.
Builds strongly influence combat performance.
Defence is a meaningful defensive statistic.
Defence reduces physical damage.
Defence Penetration exists as a specialised offensive mechanic.
High-Defence enemies create a meaningful niche for penetration-focused builds.
Status effects use Effect Power vs relevant Resistance.
Resistance affects status intensity.
Resistance affects status duration.
Resistance does not automatically purge an existing effect.
Different status effects coexist by default.
Same-effect applications are continuously recalculated rather than creating arbitrary universal stacks.
Status interactions must be explicitly authored.
Bosses can use bespoke deterministic mechanics.
Boss attacks may use alternate formulas.
Ordinary enemy AI should remain relatively simple.
The client does not determine combat outcomes.
Combat state must be reproducible.
 
⸻
 
41. OPEN PARAMETERS
The following remain to be explicitly defined:
Exact damage formula
Exact Defence formula
Exact penetration formula
Accuracy formula
Evasion formula
Critical Chance formula
Critical Damage formula
Damage-type catalogue
Resistance catalogue
Attack-speed model
Combat tick/event model
Event ordering
Healing formula
Resource system
Status duration formula
Exact status stacking/recalculation formula
Status-effect catalogue
Target-selection rules
Ordinary enemy AI rules
Boss phase architecture
Combat reward calculation
XP calculation
Combat encounter scaling
These should be resolved before the combat engine is considered implementation-ready.
 
⸻
 
42. DEPENDENCIES
Depends on
Character Foundation
Progression
Skills & Abilities
Enemy System
Equipment & Loot
Used by
Journey System
Enemy System
Boss System
Loot System
Progression System
UI/Combat Log
Server Simulation
 
⸻
 
END OF SPECIFICATION
