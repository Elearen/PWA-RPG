CHARACTER FOUNDATION SPECIFICATION
Document: CHARACTER_FOUNDATION_SPEC Version: 0.1 Status: Active Design Purpose: Defines the foundational character model, attributes, progression identity and build philosophy.
 
⸻
 
1. DESIGN PHILOSOPHY
The character system should support deep RPG builds without requiring traditional fixed classes.
The player’s character identity should emerge from:
attributes
equipment
weapon use
skills
abilities
progression choices
combat behaviour
rather than from selecting a permanent class at character creation.
The system should allow characters to evolve organically.
 
⸻
 
2. CHARACTER CLASS MODEL
There is no mandatory permanent character class.
The player does not select a conventional class such as:
Warrior
Mage
Rogue
Paladin
and become permanently restricted to that archetype.
Instead, the character’s build emerges from their actual development.
 
⸻
 
3. GENERATED COMBAT IDENTITY
The game may analyse the character’s developed statistics, equipment and/or weapon usage and assign an automatically generated combat/class-style label.
Examples might include:
Berserker
Duelist
Guardian
Ranger
Battlemage
etc.
These labels are:
Descriptive only.
They provide no direct mechanical benefit.
They do not:
modify statistics
unlock abilities
impose restrictions
determine equipment
determine progression
The label describes the character rather than defining them.
 
⸻
 
4. CORE ATTRIBUTES
The character has six core attributes:
Might
Agility
Vitality
Willpower
Endurance
Luck
These attributes form the foundation of the character’s derived statistics and build identity.
 
⸻
 
5. MIGHT
Might represents physical force and raw physical capability.
Might primarily contributes to physical combat power.
Its exact mathematical relationships to derived statistics are defined in the Combat specification.
The attribute should favour builds relying on physical force, particularly weapons and attacks that are designed to scale strongly from physical power.
 
⸻
 
6. AGILITY
Agility represents physical speed, coordination, precision and finesse.
Agility is intended to support builds that rely on:
speed
accuracy
precision
fast attacks
finesse
Its exact contribution to derived combat statistics is defined in the Combat specification.
 
⸻
 
7. VITALITY
Vitality represents physical robustness and life force.
It is intended to contribute primarily to:
survivability
maximum health
physical resilience
Exact formulas are defined in the Combat specification.
 
⸻
 
8. WILLPOWER
Willpower represents mental strength and determination.
It is intended to support:
mental resilience
concentration
resistance to appropriate effects
resource/control mechanics where applicable
Exact formulas are defined in the Combat and Skills specifications.
 
⸻
 
9. ENDURANCE
Endurance represents the character’s ability to sustain physical effort over time.
It is intended to support:
sustained combat
fatigue-related mechanics
physical resilience
long-duration activity
Exact formulas remain part of the Combat specification.
 
⸻
 
10. LUCK
Luck represents fortune and unusual positive outcomes.
It may influence systems where probabilistic or pseudo-random outcomes are appropriate.
Examples may include:
loot outcomes
rare events
critical outcomes
special discoveries
However:
Luck must not be used as a universal “better at everything” multiplier.
Its individual effects must be explicitly defined by the systems that use it.
 
⸻
 
11. ATTRIBUTE DESIGN PRINCIPLE
Attributes should have meaningful differences.
Avoid creating multiple attributes that perform essentially the same function.
Each attribute should have a recognisable build identity.
At the same time, attributes may influence multiple derived statistics where doing so creates useful build interactions.
Therefore:
One attribute ≠ one statistic.
but also:
One attribute should have a coherent mechanical identity.
 
⸻
 
12. ATTRIBUTE INTERACTION WITH EQUIPMENT
Equipment statistics are separate from base attributes.
Generated equipment receives its power from:
Item Level + Quality
and then allocates that power through its item template.
Character attributes do not determine the generated item’s power.
Instead:
Character attributes + Equipment statistics
combine during combat/stat calculation.
This separation prevents item generation from becoming dependent on the individual character.
 
⸻
 
13. ATTRIBUTE INTERACTION WITH WEAPONS
Different weapon types may scale differently from character attributes.
A weapon can define its own attribute scaling.
For example, a heavy weapon could derive more of its physical damage contribution from Might, while a finesse weapon could place greater emphasis on Agility.
Therefore there is no requirement that every weapon use the same attribute formula.
Weapon scaling belongs to the weapon/combat data definition.
 
⸻
 
14. BUILD DEVELOPMENT
The character’s build is not permanently selected.
A character can evolve toward different archetypes by:
increasing different attributes
using different weapons
acquiring different equipment
learning different skills
acquiring different abilities
This allows the same character to change their effective combat role over time.
 
⸻
 
15. WEAPON SKILL DEVELOPMENT
Weapon skills are developed through use.
The character learns and improves weapon proficiency through actually using the corresponding weapon type.
This is distinct from simply selecting a class.
The exact weapon-skill progression model belongs in:
SKILLS_AND_ABILITIES_SPEC.md
 
⸻
 
16. ATTRIBUTE CAPS
TBD
The maximum attainable value of each core attribute has not been safely recovered from the currently available design context.
Do not implement an assumed cap.
The final specification must explicitly define:
base attribute values
minimum values
maximum values
whether temporary bonuses can exceed the normal cap
whether equipment bonuses count toward the cap
 
⸻
 
17. ATTRIBUTE GAIN
TBD
The exact mechanism through which core attributes increase has not been safely recovered.
The final system must define whether attributes are increased through:
character levels
allocated points
equipment
skills
quests
permanent choices
other progression systems
Do not infer the answer from conventional RPG design.
 
⸻
 
18. CHARACTER LEVEL
TBD
The character has a progression level, but the exact:
starting level
maximum level
XP curve
level-up rewards
attribute-point relationship
level scaling rules
must be defined in the Progression specification.
 
⸻
 
19. EXPERIENCE
TBD
The exact XP system is not defined in this document.
The future Progression specification must define:
XP sources
XP calculation
XP thresholds
level-up behaviour
XP from combat
XP from quests
XP from exploration/journeys
XP handling after death
 
⸻
 
20. RESPEC
TBD
The availability and cost of changing permanent character-development decisions has not been established.
The final system must explicitly define whether players can:
reset attributes
reset skills
reset abilities
change build direction
and under what conditions.
 
⸻
 
21. TEMPORARY MODIFIERS
Temporary effects must remain distinct from permanent attributes.
Examples include:
buffs
debuffs
temporary bonuses
journey effects
consumable effects
These should modify derived statistics rather than permanently modifying the underlying attribute unless explicitly designed to do so.
 
⸻
 
22. ATTRIBUTE DATA MODEL
Conceptually, a character should maintain separate values for:
Base Attribute
Permanent Attribute Modifiers
Temporary Attribute Modifiers
Equipment Modifiers
Derived Statistics
The exact implementation schema belongs to the technical architecture specification.
The separation is important because temporary effects and equipment should not overwrite the character’s permanent attribute values.
 
⸻
 
23. DESIGN INVARIANTS
The following are currently treated as core character-design rules:
There are six core attributes.
The attributes are Might, Agility, Vitality, Willpower, Endurance and Luck.
Characters do not have mandatory permanent classes.
Character combat identity emerges from development.
Automatically generated class/combat labels are descriptive only.
Weapon skills develop through use.
Equipment power generation is independent of the individual character.
Weapon types may use different attribute-scaling profiles.
Attributes and equipment statistics remain conceptually separate.
Luck must have explicit uses rather than being a universal power multiplier.
Temporary modifiers must remain distinguishable from permanent character attributes.
 
⸻
 
24. OPEN PARAMETERS
The following must be explicitly defined before implementation:
Starting attribute values
Attribute progression
Attribute caps
Level cap
XP curve
Level-up rewards
Attribute-to-derived-stat formulas
Weapon attribute-scaling formulas
Temporary modifier rules
Respec rules
Exact Luck interactions
Exact Willpower interactions
Exact Endurance interactions
Exact Vitality interactions
Exact Agility interactions
Exact Might interactions
These are deliberately marked TBD rather than invented.
 
⸻
 
25. DEPENDENCIES
This specification is consumed by:
Combat System
Skills & Abilities
Equipment System
Progression System
Enemy System
Journey System
This specification depends on:
Core Game Rules
The exact numerical implementation should not be finalised until the Combat and Progression specifications are complete.
 
⸻
 
END OF SPECIFICATION
