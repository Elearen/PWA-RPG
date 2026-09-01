EQUIPMENT & LOOT SYSTEM SPECIFICATION
Document: EQUIPMENT_AND_LOOT_SPEC Version: 0.1 Status: Design Specification Purpose: Defines equipment, inventory, procedural loot, item quality, rarity, item generation, Legendary items, Story Relics, item loss and related death mechanics.
 
⸻
 
1. CORE DESIGN PRINCIPLES
The equipment and loot system is designed around:
Deep procedural loot
Deterministic generation
Meaningful statistical differences between items
Controlled item templates
Hidden item quality
Visible rarity
Strong distinction between generated equipment and special authored equipment
Meaningful risk during dangerous journeys
Protection for exceptional/special items
No unnecessary item-management complexity
The system should create interesting loot without requiring the player to understand the underlying generation mathematics.
 
⸻
 
2. EQUIPMENT SLOTS
Each character has exactly 11 equipment slots:
Weapon
Shield
Head
Body
Back
Legs
Feet
Hands
Neck
Accessory
Story Relic
All slots are genuine equipment slots.
 
⸻
 
3. EQUIPMENT MANAGEMENT
Equipment can be managed at safe locations.
At a safe location, the player can:
equip items
unequip items
replace equipped items
change Story Relics
manage inventory
sell equipment
use consumables
Once a journey begins:
The entire equipment loadout becomes locked.
The player cannot change equipment during the journey.
This applies equally to:
Weapon
Shield
Armour
Accessories
Story Relic
The purpose is to make preparation at a safe location strategically meaningful.
 
⸻
 
4. WEAPON & SHIELD RULES
Weapons define their own hand requirements.
One-handed weapon
Can be equipped with a Shield.
Two-handed weapon
Occupies both hands and prevents simultaneous Shield use.
The system automatically enforces this compatibility.
Shield
A Shield primarily contributes Defence.
There is no universal Block statistic.
A Shield does not inherently impose penalties to:
Attack Power
Attack Speed
Accuracy
Critical
other combat statistics
Any such behaviour must be explicitly defined by an individual item/template.
 
⸻
 
5. ARMOUR RULES
Armour has no universal weight-class system.
There is no automatic:
Light Armour
Medium Armour
Heavy Armour
mechanic.
Armour does not automatically modify:
Agility
Attack Speed
Fatigue
movement
other statistics
Any such behaviour must be explicitly authored by the relevant item.
Class Restrictions
Equipment has no universal class restrictions.
Characters can equip any armour regardless of:
class
build
attribute distribution
Individual items may have explicitly defined requirements if such requirements are introduced later.
 
⸻
 
6. STORY RELICS
Story Relics occupy the dedicated:
Story Relic
equipment slot.
A Story Relic may provide:
narrative functionality
progression functionality
combat statistics
passive effects
special mechanics
combinations of the above
A Story Relic’s mechanical effects are active only while equipped.
Only one Story Relic can be equipped at a time.
Equipping another Story Relic automatically replaces the currently equipped relic.
The previous relic returns to inventory.
Story Relics follow exactly the same equipment-locking rules as every other equipment slot.
 
⸻
 
7. STORY RELIC SALE RULES
Story Relics do not share one universal sale rule.
Each Story Relic individually defines whether it is:
sellable
non-sellable
A Story Relic may therefore be sold if its individual definition permits it.
However:
Story Relics are always protected from item-loss mechanics.
Protection from loss and sellability are separate properties.
 
⸻
 
8. INVENTORY
The character has exactly:
50 inventory slots
There is no stacking.
Every individual item occupies one slot.
Examples:
Iron Sword       = 1 slot
Iron Sword       = 1 additional slot
Iron Sword       = 1 additional slot
Potion           = 1 slot
Potion           = 1 additional slot
Three identical swords therefore consume three inventory slots.
Identical items are separate inventory entries even if their generated properties are identical.
 
⸻
 
9. ITEM IDENTITY
The gameplay model does not require every item to have a unique gameplay identity.
Items are identified by their generated properties, including relevant:
item template
level
quality-derived statistics
rarity
effects
other generated properties
Two items with identical generated properties are effectively equivalent items.
However, inventory entries remain separate because items do not stack.
Implementation may use internal database identifiers for persistence and database integrity, but those identifiers do not constitute a gameplay mechanic.
 
⸻
 
10. GENERATED EQUIPMENT
Normal equipment is procedurally generated.
The generation pipeline is:
Source / Loot Table
        ↓
Item Template
        ↓
Item Level
        ↓
Hidden Quality
        ↓
Total Item Power
        ↓
Template Stat Allocation
        ↓
Rarity Classification
        ↓
Adjective / Name
        ↓
Final Item
The exact implementation order may vary as long as the resulting rules are equivalent.
 
⸻
 
11. ITEM LEVEL
Item level is a major determinant of equipment power.
Approximately:
70% of an item’s potential power comes from item level.
Item-level contribution scales linearly.
Higher item level therefore produces proportionally higher baseline equipment power.
Item level is intended to be the dominant progression factor.
 
⸻
 
12. ITEM QUALITY
Normal generated equipment has an internal:
Quality = 0–100
value.
Quality is completely hidden from the player.
The player never sees:
Quality score
Quality percentage
Quality bar
Quality rating
raw quality value
Quality is experienced indirectly through the item’s resulting statistics.
 
⸻
 
13. QUALITY POWER CONTRIBUTION
Quality can provide up to approximately:
30% additional item power
Quality contribution uses an exponential curve.
Therefore:
level provides the primary power progression
quality provides secondary power variation
high quality becomes increasingly valuable toward the upper end
Conceptually:
Item Level
    ↓
~70% baseline power

+

Quality
    ↓
0–30% additional power
(exponential)

=

Total Item Power
The exact mathematical curve is a balance parameter and remains TBD.
 
⸻
 
14. ITEM QUALITY VS RARITY
Quality and rarity are separate concepts.
Quality
hidden
continuous
0–100
contributes to item power
Rarity
visible
categorical
derived from quality
Standard generated equipment uses:
Common
Uncommon
Rare
Epic
The exact quality thresholds are global balance parameters and are not yet numerically locked.
The same thresholds apply regardless of:
item template
item type
item level
Rarity does not independently add another power multiplier.
 
⸻
 
15. RARITY PRINCIPLE
For normal generated equipment:
Quality determines rarity.
Quality is the underlying continuous property.
Rarity is the player’s visible classification.
The player should infer quality from the generated statistics rather than being given a direct quality score.
 
⸻
 
16. TEMPLATE SYSTEM
Every generated equipment item originates from an item template.
A template defines the item’s intended identity.
A template controls:
permitted equipment slot
permitted statistics
stat allocation weights
permitted special effects
permitted adjectives
naming behaviour
other generation constraints
Templates prevent procedurally generated items from producing nonsensical combinations.
 
⸻
 
17. STAT GENERATION
The core model is:
Item Level + Quality → Total Power
Then:
Item Template → Power Allocation
The item template determines how the available power is allocated between its eligible statistics.
There is no generic random stat-distribution layer.
The template’s allocation weights directly determine the resulting statistical distribution.
 
⸻
 
18. STAT DISTRIBUTION
Templates define weighted allocation between eligible statistics.
Example:
Iron Sword Template

Attack Power    60%
Accuracy        25%
Critical        15%
The item’s available power is distributed according to these template-defined weights.
Two items with the same:
template
item level
quality
will have the same statistical distribution.
Variation between items therefore primarily comes from differences in:
item level
hidden quality
template
permitted effects
permitted naming/adjective configuration
 
⸻
 
19. ITEM NAMES
Generated equipment supports two naming approaches.
19.1 Fixed Template Name
Some templates simply use a fixed name.
Examples:
Iron Sword
Hunter’s Bow
Steel Shield
19.2 Generated Adjective
Some templates support a predefined adjective pool.
Examples:
Brutal Iron Sword
Swift Iron Sword
Sturdy Iron Sword
The adjective pool is defined by the item template.
The generation system selects an adjective from that permitted pool.
 
⸻
 
20. ADJECTIVE RULES
An adjective does not universally have one mechanical meaning.
The template determines whether an adjective is:
purely descriptive
mechanically meaningful
both
For example:
Brutal Iron Sword
could mean:
+Attack Power
if the template defines that relationship.
Another template could use “Brutal” purely as flavour.
The adjective system therefore cannot be interpreted as a universal rules dictionary.
 
⸻
 
21. NO QUALITY-BASED NAMING
Quality does not automatically generate names such as:
Fine
Exceptional
Masterwork
Similarly, rarity does not automatically become part of the item name.
Avoid:
Rare Iron Sword
as a procedural naming convention.
Instead:
Iron Sword Brutal Iron Sword
while rarity is displayed separately.
 
⸻
 
22. EPIC EQUIPMENT
Epic is the highest normal generated rarity.
Epic items can contain special effects.
Epic effects are controlled by the item’s template.
The template defines:
permitted effect pool
permitted combinations
number of effects
scaling behaviour
restrictions
Procedural generation therefore cannot arbitrarily combine every effect in the game.
Epic equipment represents:
Controlled procedural specialisation.
 
⸻
 
23. RARE SET EQUIPMENT
Rare equipment can belong to equipment sets.
Set pieces:
are Rare
occupy normal equipment slots
are generated through set-specific templates
can vary in generated quality/stat strength
A set defines:
participating equipment slots
set pieces
stat templates
total set size
one set bonus
one activation threshold
 
⸻
 
24. SET BONUS
Each equipment set has:
One set bonus
and:
One activation threshold
The bonus becomes active when the required number of pieces is equipped.
The bonus automatically scales with the number of equipped set pieces above the activation threshold.
The exact mathematical scaling formula remains a balance parameter.
Only equipped set pieces count toward the bonus.
Duplicate set items stored in inventory do not contribute.
 
⸻
 
25. LEGENDARY ITEMS
Legendary is not a normal generated rarity.
Legendary items are reserved for:
Special, handcrafted items.
They are fundamentally different from Common/Uncommon/Rare/Epic procedural equipment.
Legendary items are authored rather than procedurally rolled.
 
⸻
 
26. LEGENDARY STATISTICS
Legendary items have:
authored statistics
authored effects
authored identity
authored progression behaviour
Their numerical statistics use an explicitly authored progression formula.
They do not use the normal hidden-quality system.
Legendary items have:
No generated quality value.
 
⸻
 
27. LEGENDARY ITEM LEVEL
A Legendary has its own:
fixed item level
Its stats are determined from that item level using its authored scaling formula.
Legendary power does not automatically scale with the character.
If a player acquires a Level 20 Legendary and later reaches Level 40:
The Legendary remains Level 20.
 
⸻
 
28. LEGENDARY UPGRADING
Legendary items cannot be upgraded.
The player cannot:
increase Legendary item level
reroll its stats
reroll its effects
improve its quality
reforge it
apply upgrade materials
otherwise enhance it through a generic upgrade system
A Legendary is therefore a complete authored item.
 
⸻
 
29. LEGENDARY DUPLICATES
A character can obtain multiple copies of the same Legendary.
There is no universal one-copy-per-character restriction.
Duplicate Legendary items:
occupy separate inventory slots
do not stack
remain separate items
are protected from item loss
can be sold
There is no automatic duplicate conversion system.
 
⸻
 
30. LEGENDARY SALE
Legendary items are sellable.
Legendary protection means:
A Legendary cannot be lost through loss/death mechanics.
It does not mean:
A Legendary cannot be voluntarily sold.
 
⸻
 
31. ITEM LOSS PROTECTION
The following item categories are permanently protected from item-loss mechanics:
Always protected
Equipped items
Epic items
Legendary items
Story Relics
Vulnerable
Common spare items
Uncommon spare items
Rare spare items
Protection applies regardless of whether the item is currently pending from a journey or stored in inventory.
 
⸻
 
32. ITEM LOSS SELECTION
When a loss event occurs, eligible vulnerable items are selected deterministically.
Every eligible item has:
Equal selection weight.
Selection is not weighted by:
item value
item quality
sale price
rarity within the vulnerable pool
equipment type
Therefore every eligible item is equally vulnerable.
 
⸻
 
33. DUPLICATE ITEM LOSS
Duplicate items are independent loss candidates.
Example:
Iron Sword A
Iron Sword B
Iron Sword C
All three are separate items and each can independently be selected.
Identical statistics do not cause the items to merge into one loss group.
 
⸻
 
34. ITEM LOSS QUANTITY
The quantity of vulnerable items lost is determined by the severity of the loss event.
The calculation is deterministic.
If the calculated loss exceeds the number of eligible vulnerable items:
All eligible vulnerable items are lost.
No protected items are substituted to satisfy a loss quantity.
The exact severity formula remains TBD.
 
⸻
 
35. JOURNEY PENDING LOOT
Loot generated during a journey is initially:
Pending Loot
Pending loot is not immediately available to the player.
The player cannot access it while travelling.
Pending loot becomes available according to the journey’s successful completion rules.
 
⸻
 
36. PENDING LOOT PROTECTION
The moment an Epic, Legendary or Story item is generated as pending loot, it becomes protected.
Therefore:
Epic pending loot cannot be lost.
Legendary pending loot cannot be lost.
Story pending loot cannot be lost.
Only vulnerable pending loot is subject to journey loot-loss mechanics.
 
⸻
 
37. PENDING LOOT LOSS
A journey/activity can define its own:
Loot-loss percentage
This is separate from gold loss.
The journey’s percentage determines how much vulnerable pending loot is at risk.
The exact rounding and quantity calculation remain TBD.
 
⸻
 
38. PENDING LOOT SELECTION
After determining the amount of vulnerable loot to lose:
Protected loot is excluded.
Vulnerable loot forms the eligible pool.
The loss amount is calculated.
Eligible items are selected deterministically.
Every eligible item has equal weighting.
Selected items are removed.
Remaining loot proceeds normally.
The item selection does not favour:
cheaper items
expensive items
Common items
Rare items
low-quality items
All vulnerable items are equally eligible.
 
⸻
 
39. DEATH
Death ends the current dangerous activity/journey.
Death causes:
Gold
20% of currently held gold is lost.
This percentage is fixed globally.
It does not scale with:
character level
item level
area
enemy difficulty
activity
journey difficulty
Spare Equipment
Vulnerable spare items may be lost through the deterministic item-loss system.
Pending Loot
Vulnerable pending loot is subject to the journey/activity-specific loot-loss percentage.
Protected Items
Never lost:
Equipped items
Epic items
Legendary items
Story Relics
Character Progression
Death does not:
remove XP
reduce level
reduce attributes
remove skills
apply a permanent character debuff
 
⸻
 
40. DEATH RETURN
After death:
The character returns to the most recent safe location.
This location functions as the practical journey checkpoint.
The player can then:
manage inventory
manage equipment
sell items
use consumables
prepare for another journey
 
⸻
 
41. DEATH RESOURCE MODEL
Death therefore follows three independent loss systems:
￼
These systems must remain independently configurable.
Changing the gold-loss percentage must not automatically change item-loss or pending-loot rules.
 
⸻
 
42. EQUIPMENT SALE
Equipment can be sold.
This includes:
Common
Uncommon
Rare
Epic
Legendary
Story Relics individually determine whether they are sellable.
Sale value is determined by the game’s economy system.
The sale-value formula is not yet finalised.
 
⸻
 
43. SALE VALUE DESIGN PRINCIPLE
Equipment power and sale value should not scale identically.
Higher-quality equipment should generally be worth more, but the economy should use:
Limited sale-value scaling
rather than allowing high-power equipment to generate proportionally unlimited wealth.
The exact formula and limits remain TBD.
 
⸻
 
44. CONSUMABLES
Consumables occupy normal inventory slots.
Consumables:
do not stack
are individually represented
can only be used in safe areas
therefore have relatively low frequency of use during dangerous activities
Consumable details are part of the future Consumables/Economy specification.
 
⸻
 
45. INVENTORY RESERVATION FOR JOURNEYS
Before beginning a journey, the game determines the journey’s potential equipment-loot capacity requirement.
The player must have sufficient inventory capacity.
There is always a minimum reservation of:
5 inventory slots
The effective requirement is:
max(5, calculated journey equipment-loot requirement)
This is a pre-departure validation.
Once the journey begins, inventory is locked and pending loot is tracked separately.
 
⸻
 
46. DESIGN INVARIANTS
The following rules should be treated as hard invariants unless explicitly changed in a future specification revision:
Inventory capacity = 50 slots.
Items do not stack.
There are 11 equipment slots.
Equipment is locked during journeys.
Story Relic behaves as a normal equipment slot.
Quality is 0–100 internally.
Quality is hidden.
Level supplies approximately 70% of item power.
Quality supplies up to approximately 30% additional power.
Quality contribution is exponential.
Rarity is derived from quality.
Common/Uncommon/Rare/Epic are normal generated rarities.
Legendary is reserved for special authored items.
Legendary has no generated quality.
Legendary item level is fixed.
Legendary cannot be upgraded.
Legendary duplicates are allowed.
Legendary items can be sold.
Epic/Legendary/Story items cannot be lost.
Equipped items cannot be lost.
Common/Uncommon/Rare spare items can be lost.
Vulnerable loss selection is deterministic.
Vulnerable items have equal loss weighting.
Duplicate items are independent loss candidates.
Death always removes 20% of held gold.
Death returns the character to the most recent safe location.
Pending Epic/Legendary/Story loot is protected.
Pending vulnerable loot uses journey-specific loss percentages.
Story Relics individually determine whether they can be sold.
Generated stat allocation is controlled by the item template.
 
⸻
 
47. CURRENT TBD PARAMETERS
The following must be defined before implementation:
Exact item-power formula
Exact exponential quality curve
Exact rarity thresholds
Exact stat-allocation formula
Exact quality-to-rarity mapping
Exact item-level generation rules
Exact Epic effect-generation rules
Exact Rare set scaling formula
Exact item-loss severity formula
Exact pending-loot loss calculation/rounding
Exact deterministic selection algorithm
Exact equipment sale-value formula
Exact equipment level requirements
Exact loot-table probabilities/weights
Exact consumable catalogue
Exact interaction between equipment and character statistics
These are open parameters, not assumptions.
 
⸻
 
48. IMPLEMENTATION REQUIREMENTS
The implementation should keep the following concepts separate:
Item Template
Defines what an item is allowed to be.
Item Instance
Represents an occurrence of an item in inventory/equipment.
Item Level
Determines the primary progression component of generated item power.
Quality
Hidden 0–100 generated value.
Rarity
Visible classification derived from quality.
Total Power
Calculated from item level and quality.
Stat Allocation
Determined by the item template.
Adjective
Generated from the template’s permitted adjective pool.
Special Effects
Generated only from template-permitted effect pools.
Legendary Definition
Authored data rather than procedural generation.
Keeping these concepts separate is important for both game balance and implementation.
 
⸻
 
49. FUTURE EXTENSION
The system should support adding:
additional equipment templates
new adjectives
new Epic effects
new Legendary items
new equipment sets
new item types
new loot tables
new loss events
without requiring changes to the fundamental item-generation architecture.
New content should preferably be added as data/configuration, not new hard-coded logic.
 
⸻
 
END OF SPECIFICATION
