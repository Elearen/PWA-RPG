SKILLS & ABILITIES SYSTEM SPECIFICATION
Document: SKILLS_AND_ABILITIES_SPEC Version: 0.3 Status: Active Design Purpose: Defines weapon skills, skill progression, passive statistical contributions and the relationship between character attributes, skills, equipment and combat statistics.
 
⸻
 
1. DESIGN GOALS
The Skills system should:
Support deep character builds.
Allow characters to develop organically.
Reward using different weapons.
Avoid rigid permanent classes.
Create meaningful specialisation.
Allow hybrid builds.
Integrate strongly with equipment and combat.
Remain understandable through a relatively simple UI.
Support fully deterministic combat resolution.
Allow combat outcomes to be pre-calculated from the initial combat state.
Allow every skill to be developed.
Preserve progression independence from action order.
Provide long-term progression through effectively uncapped skill levels.
The player should feel that their character becomes effective through the combination of:
attributes
weapon skills
equipment
special equipment effects
enemy properties
progression history
There are no character abilities that require selection or activation during combat.
 
⸻
 
2. CLASSLESS DEVELOPMENT
Characters do not select a permanent conventional class.
There is no requirement to choose:
Warrior
Mage
Rogue
Ranger
etc.
at character creation.
Instead, the character’s effective combat archetype emerges from their:
attributes
weapon skills
equipment
Story Relic
progression choices
gameplay history
The resulting combat identity is a description of the character’s current statistical and equipment-based development rather than a separate class system.
 
⸻
 
3. SKILL AVAILABILITY
All skills are pre-loaded on every new character.
At character creation:
every skill exists on the character
every skill begins at level zero
every skill is hidden from the player
no skill must be unlocked through a separate acquisition system
no skill is permanently unavailable
no skill requires a prerequisite path before it can be developed
A skill becomes visible to the player when it reaches level one.
The first relevant action that causes a level-zero skill to reach level one therefore also reveals that skill in the user interface.
Skills that remain at level zero remain hidden unless the UI explicitly provides a future way to inspect undiscovered skills.
 
⸻
 
4. WEAPON SKILLS
Weapon skills are learned and improved through relevant combat actions.
Using a particular weapon type contributes progression to the corresponding weapon skill.
Examples might include:
Sword
Axe
Mace
Spear
Bow
etc.
The final weapon-skill catalogue remains TBD.
Weapon skills contribute to combat statistics and may affect how efficiently a character uses the associated weapon.
 
⸻
 
5. RELEVANT COMBAT ACTIONS
Skill progression is awarded from relevant combat actions.
A relevant action is an action that directly corresponds to the skill being developed.
Examples may include:
attacking with the associated weapon
successfully using the associated weapon in combat
performing a weapon-specific combat action
other explicitly defined actions associated with that skill
The final mapping between combat actions and skills must be defined as data.
The system must not award skill progression based solely on:
menu selection
equipping an unused weapon
owning an item
selecting a build label
unrelated combat activity
The exact progression award rules remain TBD.
 
⸻
 
6. USE-BASED PROGRESSION
Weapon proficiency is not advanced purely by selecting a menu option.
The fundamental principle is:
Use it to improve it.
The character therefore develops naturally toward the weapons they actually use.
Repeated relevant combat actions progressively improve the associated skill.
Skill progression is based on the accumulated quantity of relevant development activity rather than the order in which that activity occurred.
Skill progression must be calculated and recorded by the server.
 
⸻
 
7. PATH INDEPENDENCE
Skill growth has no path dependency.
Two characters that perform the same relevant actions in different orders must achieve the same skill growth, assuming all other progression inputs are equivalent.
For example:
Character A:
Sword Action → Bow Action → Sword Action

Character B:
Sword Action → Sword Action → Bow Action
If both characters perform the same total number and type of relevant actions, they must have the same resulting skill XP and skill levels.
Skill progression must not depend on:
the order of actions
the order in which skills were first revealed
the order in which weapons were equipped
the character’s previous skill focus
hidden progression history
temporary path choices
unless an explicit future rule is added to the design.
 
⸻
 
8. SKILL PROGRESSION XP
Each skill has its own XP total.
Relevant combat actions add XP to the associated skill.
Conceptually:
Skill XP
    ├── Current Level
    ├── Total XP
    └── XP Toward Next Level
Skill XP is independent for each skill.
Using one weapon does not directly grant XP to unrelated weapon skills.
The exact XP award per relevant action remains TBD.
 
⸻
 
9. SKILL LEVEL REQUIREMENTS
Skills level similarly to character level.
Each skill level requires an increased amount of XP compared with the previous level.
The required XP scales upward as the skill level increases.
Conceptually:
XP Required for Skill Level N
    >
XP Required for Skill Level N - 1
The exact progression formula remains TBD.
The progression curve must create meaningful early advancement while requiring substantially more long-term activity for higher levels.
 
⸻
 
10. INFINITE SKILL LEVELS
Skills have no hard maximum level.
A skill can continue to gain XP indefinitely.
The XP required for each additional level scales exponentially, creating an effective soft cap.
This means:
there is no final skill level
continued development is always possible
high levels require increasingly substantial investment
practical progression slows significantly at high levels
the system avoids a strict hard cap while preventing unlimited rapid scaling
The exact exponential formula and balancing constants remain TBD.
 
⸻
 
11. SKILL LEVEL VISIBILITY
All skills begin hidden at level zero.
When a skill reaches level one:
the skill becomes visible to the player
its name is shown
its current level is shown
its progression state is shown
its relevant statistical contributions may be shown
future progression for that skill becomes trackable
There is no separate discovery delay.
The skill appears immediately when the level-one transition is processed.
A skill that has reached level one remains visible permanently unless an explicit future rule states otherwise.
 
⸻
 
12. WEAPON SKILL LEVEL
Each weapon skill has an independent progression state.
Conceptually:
Weapon Skill
    ├── Skill ID
    ├── Current Level
    ├── Total XP
    ├── XP Toward Next Level
    ├── Visibility State
    └── Derived statistical contributions
The exact implementation may use a different internal representation.
Weapon skill levels do not grant character abilities.
They contribute to the character’s calculated combat statistics and may affect the relationship between those statistics and equipped weapons.
 
⸻
 
13. WEAPON SKILL EFFECTS
Weapon skill may influence relevant combat statistics.
Potential effects include:
damage
accuracy
critical chance
attack speed
defence
resistance
penetration
other explicitly defined combat statistics
The exact relationship between proficiency and combat statistics is TBD.
Weapon skill should not be treated merely as another generic damage multiplier.
Weapon mastery should create a meaningful distinction between:
“I can equip this weapon”
and:
“I am highly proficient with this weapon.”
The final implementation must define which statistics are affected by each weapon skill and how those contributions are calculated.
 
⸻
 
14. SKILL SPECIALISATION
Weapon skills should support specialisation without permanently preventing experimentation.
A character who spends significant time using one weapon type should become meaningfully better with it.
However, switching weapons remains possible, and all other skills remain available for future development.
The system therefore supports:
specialisation
experimentation
hybrid builds
changing builds over time
long-term development of multiple skills
Specialisation should affect the character’s statistical profile rather than unlock a separate active combat kit.
 
⸻
 
15. CROSS-WEAPON DEVELOPMENT
Weapon skills are independently tracked.
Improving Sword skill does not automatically grant the same level of proficiency with:
Axe
Bow
Spear
etc.
Any shared weapon-family bonuses must be explicitly designed.
If weapon families share statistical effects, those relationships must be defined as data rather than inferred by the combat engine.
 
⸻
 
16. NO CHARACTER ABILITIES
Characters do not possess active or passive abilities that independently execute during combat.
There are no character abilities that:
require manual activation
are selected by combat AI
use an ability priority system
trigger as separate character actions
apply independently authored ability effects
Combat outcomes are determined through the character’s calculated statistics and the rules governing their interaction with:
enemy statistics
equipment
equipment effects
enemy effects
combat timing
status effects
encounter conditions
The term “ability” should not be used for character mechanics unless it refers to a future system explicitly added to the design.
 
⸻
 
17. FULLY PRE-CALCULATED COMBAT
Combat does not contain active ability decisions, manual ability selection or runtime ability-priority logic.
All combat-relevant character state is determined before combat begins from the character’s:
attributes
weapon skills
equipment
Story Relic
equipment effects
current status effects
encounter state
The complete combat result can therefore be pre-calculated from the initial combat state.
The combat engine may still represent combat as a sequence of deterministic events for logging and presentation, but no player input or mid-combat character decision is required.
Skill XP resulting from combat is calculated from the authoritative combat actions and applied by the server after the combat result is resolved.
 
⸻
 
18. STAT-BASED COMBAT
Combat performance is determined by statistics rather than character abilities.
Relevant statistics may include:
offensive power
defensive power
accuracy
evasion
critical chance
critical damage
attack speed
penetration
health
resistances
other explicitly defined combat statistics
The final statistic catalogue and formulas are defined by the Character and Combat specifications.
Skills and equipment contribute to these statistics.
The combat engine resolves outcomes by applying the relevant formulas and interactions.
 
⸻
 
19. EQUIPMENT EFFECTS
Some equipment may confer special combat effects.
These effects modify:
character statistics
enemy statistics
the relationship between statistics
damage calculation
defence calculation
penetration
resistances
timing
status effects
other explicitly defined combat rules
Equipment effects are not character abilities.
They are properties of the relevant equipment and are active only when the equipment is equipped and its conditions are satisfied.
Examples may include:
increasing penetration against high-Defence enemies
converting one statistic into another
reducing the effectiveness of a target’s Defence
modifying critical calculations
changing how a resistance is applied
altering the relationship between attack speed and action timing
All equipment effects must be explicitly authored and deterministic.
 
⸻
 
20. ENEMY EFFECTS
Some enemies may confer special combat effects.
Enemy effects may modify:
their own statistics
the character’s statistics
the relationship between statistics
damage calculation
defence calculation
penetration
resistances
timing
status effects
other explicitly defined combat rules
Enemy effects are properties of the enemy or encounter.
They are not character abilities and do not require character decision-making.
Enemy effects may be:
permanent for the encounter
active during a phase
conditional
triggered by a defined combat event
applied at the start of combat
applied through a status effect
All enemy effects must be explicitly authored and deterministic.
 
⸻
 
21. STAT RELATIONSHIPS
Some equipment or enemies may affect how one statistic interacts with another.
Examples include:
penetration becoming more effective against high Defence
Defence contributing differently against a particular damage type
accuracy being reduced by a specific enemy effect
critical chance being converted into another statistic
resistance modifying the effectiveness of a status effect
attack speed being altered by a weapon or enemy property
These effects modify the combat formulas or their inputs.
They must not be implemented as hidden or implicit exceptions.
Each altered relationship must define:
the affected statistics
the condition
the order of application
the resulting formula or modifier
whether the effect is additive, multiplicative or substitutive
whether it applies before or after other modifiers
 
⸻
 
22. STAT MODIFIERS
Stat modifiers may be provided by:
character attributes
weapon skills
equipment
Story Relics
enemy effects
encounter conditions
status effects
other explicitly defined progression systems
Modifiers must be categorised clearly.
Potential categories include:
flat modifiers
percentage modifiers
conversion modifiers
conditional modifiers
relationship modifiers
caps or floors
overrides
The final modifier-ordering rules remain TBD.
 
⸻
 
23. STAT CALCULATION ORDER
The final system must define a canonical order for calculating combat statistics.
Conceptually:
Base Attributes
        ↓
Weapon Skill Contributions
        ↓
Equipment Statistics
        ↓
Story Relic Contributions
        ↓
Equipment Effects
        ↓
Encounter Effects
        ↓
Enemy Effects
        ↓
Status Effects
        ↓
Final Combat Statistics
This is a conceptual model only.
The exact ordering must be defined before implementation because modifier order can materially affect combat outcomes.
 
⸻
 
24. CONDITIONAL EFFECTS
Equipment and enemies may provide conditional effects.
A conditional effect must define:
its condition
when the condition is evaluated
whether it affects initial statistics
whether it can change during combat
whether it affects one event or the entire encounter
whether it expires
whether it can be replaced or overridden
Examples include:
increased damage against enemies above a Health threshold
increased Defence while above a Health threshold
increased penetration against targets with high Defence
reduced resistance while affected by a particular status
altered attack speed during a boss phase
All conditions must be deterministic and evaluable from known combat state.
 
⸻
 
25. PERIODIC AND EVENT-BASED EFFECTS
Although character abilities do not exist, equipment and enemies may create effects that occur:
at combat start
at a defined time
at regular intervals
when damage is dealt
when damage is received
when a threshold is reached
when a status effect is applied
when a combat phase changes
when a combatant is defeated
These effects are part of the equipment or enemy rules.
They must be explicitly authored and resolved by the Combat System.
If an effect can change the combat result, it must be included in the deterministic combat calculation.
 
⸻
 
26. STATUS EFFECTS
Equipment and enemies may apply status effects.
The status-effect engine follows the rules established in COMBAT_SPEC.md:
Effect Power is compared against relevant Resistance.
Resistance affects intensity.
Resistance affects duration.
Resistance does not automatically purge an existing effect.
Different effects coexist by default.
Same-effect applications are continuously recalculated.
Explicit interactions must be authored.
The Skills system does not define character abilities that apply status effects.
Instead, status effects may originate from:
equipment effects
enemy effects
combat rules
encounter mechanics
other explicitly defined systems
The Combat system defines how those effects resolve.
 
⸻
 
27. EQUIPMENT REQUIREMENTS
The only equipment requirement is character level.
Each equipment item has an inherent level.
A character may equip an item only when the character’s level meets or exceeds the item’s inherent level.
Conceptually:
Can Equip Item =
Character Level >= Item Level
Equipment does not require:
weapon skill level
attribute thresholds
progression state
Story Relics
quest or story progression
any other prerequisite
The item’s inherent level is an intrinsic property of the item and is separate from the character’s current level.
Equipment requirements do not create character abilities.
 
⸻
 
28. WEAPON-SPECIFIC STATISTICS
Weapons may be associated with specific weapon skills.
A weapon may:
require a particular weapon type
contribute statistics based on the associated weapon skill
scale its effectiveness from weapon skill
modify the relationship between statistics
become less effective when used with low proficiency
provide special combat effects
This supports meaningful weapon mastery without introducing character abilities.
Weapon skill does not determine whether an item can be equipped.
Only character level compared with the item’s inherent level determines equipment eligibility.
 
⸻
 
29. GENERIC EQUIPMENT EFFECTS
Not every equipment effect needs to be weapon-specific.
Generic equipment effects can support:
universal defensive mechanics
healing modifiers
utility
general combat mechanics
resistance changes
statistical conversions
combat-formula modifications
There is no combat resource other than Health Points.
Equipment effects must not require or consume mana, stamina, energy, rage or any other combat resource unless a future specification explicitly changes this rule.
The game can therefore contain both:
Weapon-specific equipment effects
and:
General equipment effects.
 
⸻
 
30. RESOURCE SYSTEM
The only combat resource is Health Points (HP).
Characters and enemies have:
Maximum HP
Current HP
Damage reduces Current HP.
Healing restores Current HP, subject to the rules defined by the Combat System.
There is no:
mana
stamina
energy
rage
action-point resource
ability-charge resource
other combat resource
Character abilities do not require resources because character abilities do not exist.
Equipment and enemy mechanics must not introduce additional combat resources.
All combat effects must operate through:
HP
statistics
timing
status effects
equipment effects
enemy effects
encounter rules
unless a future specification explicitly changes this invariant.
 
⸻
 
31. STAT SCALING
Combat statistics may be derived from:
character attributes
weapon skills
weapon statistics
equipment
Story Relics
target properties
enemy properties
encounter conditions
other explicitly defined variables
Each statistic should explicitly define its calculation model.
There is no universal requirement that all statistics scale from the same attribute or source.
 
⸻
 
32. STAT INTERACTIONS
Statistics may interact with:
equipment
weapon skills
attributes
status effects
enemy properties
Story Relics
encounter conditions
other statistics
Interactions should be explicit.
The system must not infer interactions merely because two mechanics happen to share a statistic or keyword.
All interactions must remain deterministic and suitable for pre-calculation.
 
⸻
 
33. STAT EFFECTS
A mechanic can contain multiple deterministic statistical effects.
Conceptually:
Combat Modifier
 ├── Requirements
 ├── Conditions
 └── Effects
      ├── Flat Stat Modifier
      ├── Percentage Stat Modifier
      ├── Stat Conversion
      ├── Relationship Modifier
      ├── Damage Modifier
      ├── Defence Modifier
      ├── Penetration Modifier
      ├── Resistance Modifier
      ├── Timing Modifier
      └── Other Authored Effect
The actual effects are resolved by the Combat System.
The source of the modifier may be:
equipment
enemy
encounter
status effect
Story Relic
another explicitly defined system
 
⸻
 
34. EFFECT INTERACTIONS
Equipment effects and enemy effects may interact with:
weapon skills
attributes
statistics
status effects
other equipment effects
other enemy effects
Story Relics
encounter conditions
Interactions should be explicit.
The system must not infer interactions merely because two effects happen to share a statistic or keyword.
All interactions must remain deterministic and suitable for pre-calculation.
 
⸻
 
35. COMBAT IDENTITY
The game may calculate a descriptive combat identity based on the character’s development.
This can produce a label such as a class/archetype.
The label is:
automatically generated
descriptive
potentially dynamic
It provides:
No mechanical benefit.
It does not grant:
statistics
abilities
equipment access
bonuses
penalties
The label is derived from the character’s actual attributes, skills, equipment and resulting statistical profile.
 
⸻
 
36. RESPECIALISATION
Characters should be able to experiment with different weapons and builds.
Because weapon skills are use-based, switching weapon types naturally causes development to shift over time.
All skills remain available for development.
There is no requirement to reset or respecialise a skill in order to develop another skill.
The exact rules for:
changing equipment configurations
changing Story Relic configurations
remain TBD.
No automatic skill reset should be implemented.
 
⸻
 
37. SKILL LOSS AND DELAY
Skills do not decay.
A skill does not lose levels or XP because it is unused.
There is no progression delay.
Once relevant combat actions have been resolved, the corresponding skill XP is awarded without an additional waiting period.
The following rules are fixed:
no skill loss
no skill decay
no skill regression
no delayed skill progression
no temporary skill suppression
no path-dependent penalty for changing weapons
 
⸻
 
38. NON-COMBAT SKILLS
There are no non-combat skills.
The Skills system covers combat and weapon skills only.
The following are not part of the game’s skill system:
crafting
gathering
cooking
lockpicking
trading
other non-combat skill categories
No non-combat skill data, progression, UI or server logic should be implemented unless a future specification explicitly changes this rule.
 
⸻
 
39. DETERMINISTIC DEVELOPMENT
Skill progression must remain compatible with the game’s deterministic architecture.
The server remains authoritative for:
skill XP
skill levels
skill visibility
equipment state
equipment eligibility
equipment effects
combat statistics
combat effects
The client cannot directly modify skill progression, equipment state or combat statistics.
All combat-relevant character state must be known before combat simulation begins.
Skill XP awards must be derived from the authoritative combat result and the relevant combat actions performed during that result.
Because skill progression is path-independent, the final skill state must be determined by the total valid progression inputs rather than their order.
 
⸻
 
40. DATA MODEL
Conceptually:
Character
 ├── Attributes
 ├── Level
 ├── Skills
 │    ├── Skill ID
 │    ├── Level
 │    ├── Total XP
 │    ├── XP Toward Next Level
 │    └── Visibility State
 │
 ├── Equipment
 │    ├── Equipment ID
 │    ├── Slot
 │    ├── Item Level
 │    ├── Statistics
 │    └── Effects
 │
 └── Derived Combat Statistics
      ├── Base Values
      ├── Modified Values
      └── Final Values
A new character conceptually begins with:
All Skills
    ├── Level: 0
    ├── XP: 0
    └── Visibility: Hidden
When a skill reaches level one:
Skill
    ├── Level: 1
    ├── XP: At or above Level 1 threshold
    └── Visibility: Visible
Equipment eligibility is determined by:
Character Level >= Item Level
Conceptually, enemy combat data may contain:
Enemy
 ├── Base Statistics
 ├── Equipment-Like Effects
 ├── Status Effects
 ├── Conditional Effects
 └── Combat Relationship Modifiers
The final database schema belongs to the Technical Architecture specification.
 
⸻
 
41. DESIGN INVARIANTS
The character system is classless.
All skills are pre-loaded on a new character.
All skills begin at level zero.
All level-zero skills are hidden from the player.
A skill becomes visible when it reaches level one.
Skill visibility occurs immediately at the level-one transition.
Every skill can be developed.
No skill requires a separate unlock path.
Weapon proficiency is learned through relevant combat actions.
Weapon skills are independently tracked.
Weapon specialisation is meaningful.
Characters can change weapon focus.
Skill progression has no path dependency.
The order of relevant actions does not affect final skill growth.
Skills level through accumulated XP.
Each additional skill level requires more XP than the previous level.
Skill XP requirements scale exponentially.
Skills have no hard maximum level.
Skill progression has an effective soft cap.
Skills do not decay.
Skills do not lose XP or levels through inactivity.
Skill progression is not delayed after valid progression is earned.
Characters have no active combat abilities.
Characters have no passive combat abilities.
Combat outcomes are determined through statistics and authored combat rules.
Combat can be pre-calculated from the initial combat state.
Attributes contribute to combat statistics.
Weapon skills contribute to combat statistics.
Equipment contributes to combat statistics.
Equipment may modify the relationship between statistics.
Enemies may modify the relationship between statistics.
Equipment and enemy effects are explicitly authored.
Equipment and enemy effects are deterministic.
Status-effect application follows the Combat specification.
Combat identity labels are descriptive only.
Skill and equipment state is server-authoritative.
Skill progression cannot be directly manipulated by the client.
No mid-combat player input is required.
No character ability-priority system exists.
No character ability cooldown system exists.
No character ability resource system exists.
The only combat resource is Health Points.
No mana, stamina, energy, rage or other combat resource exists.
The only equipment requirement is character level.
Every equipment item has an inherent level.
A character may equip an item only when the character’s level meets or exceeds the item’s inherent level.
Weapon skill does not determine equipment eligibility.
Attributes do not determine equipment eligibility.
Story Relics do not determine equipment eligibility.
Quest or story progression does not determine equipment eligibility.
No non-combat skills exist.
Crafting, gathering, cooking, lockpicking and trading are not skill categories.
 
⸻
 
42. OPEN PARAMETERS
The following require explicit design decisions:
Weapon skill catalogue
Relevant combat actions for each skill
Skill XP awarded per relevant action
Whether all relevant actions award equal XP
Skill progression formula
Exponential scaling constants
Starting skill XP
Skill visibility UI
Skill-to-stat relationships
Weapon-to-skill relationships
Equipment effect catalogue
Enemy effect catalogue
Stat catalogue
Stat calculation order
Modifier ordering
Flat versus percentage modifier rules
Stat conversion rules
Statistical relationship modifiers
Conditional-effect evaluation
Periodic-effect model
Combat identity calculation
Pre-calculated combat result format
Combat event-log representation
Rules for changing equipment configurations
Rules for changing Story Relic configurations
The following are resolved:
All skills are pre-loaded.
All skills begin at level zero.
Level-zero skills are hidden.
Skills appear at level one.
All skills can be developed.
There is no skill loss.
There is no skill decay.
There is no progression delay.
There is no path dependency.
Skill XP requirements increase by level.
Skill levels have no hard maximum.
XP scaling creates an effective soft cap.
The only equipment requirement is character level.
Every equipment item has an inherent level.
There are no equipment requirements other than character level.
The only combat resource is Health Points.
No additional combat resources exist.
No non-combat skills exist.
 
⸻
 
43. DEPENDENCIES
Depends on
Character Foundation
Combat System
Equipment System
Progression System
Used by
Combat System
Enemy System
Journey System
Story System
UI
Server Simulation
 
⸻
 
END OF SPECIFICATION
