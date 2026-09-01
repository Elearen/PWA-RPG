PROGRESSION & ECONOMY SYSTEM SPECIFICATION
Document: PROGRESSION_AND_ECONOMY_SPEC Version: 0.1 Status: Active Design Purpose: Defines character progression, experience, levels, gold, rewards, item-level progression, equipment-quality thresholds, and the economic relationship between journeys, combat, and equipment.
 
⸻
 
1. DESIGN GOALS
The progression system should provide:
Long-term character development.
Meaningful rewards for exploration and combat.
Clear numerical progression.
Strong interaction between character level and equipment.
Controlled scaling throughout the game.
A sustainable long-term gameplay loop.
Meaningful equipment upgrades without requiring uncontrolled stat inflation.
Distinct and understandable equipment-quality tiers.
A quality system that rewards exceptional items without allowing quality to overpower item-level progression.
The game should feel increasingly powerful as the player progresses, while retaining meaningful challenge.
 
⸻
 
2. PROGRESSION LAYERS
Character progression is composed of several related but distinct systems.
Character Progression
 ├── Character Level
 ├── Experience
 ├── Attributes
 ├── Weapon Skills
 ├── Abilities
 └── Equipment
       ├── Item Level
       ├── Quality
       ├── Quality Tier
       └── Generated Stats
These systems should not be collapsed into one universal progression number.
 
⸻
 
3. CHARACTER LEVEL
The character has a level representing broad overall progression.
Character level may influence:
available content
base character power
ability access
equipment eligibility
enemy scaling
rewards
The exact maximum character level remains TBD.
 
⸻
 
4. EXPERIENCE
Experience is awarded primarily through gameplay.
Potential sources include:
combat
journey completion
quests
story events
dungeon completion
bosses
other authored progression events
The exact XP reward formula belongs to the relevant content and reward definitions.
 
⸻
 
5. XP RETENTION
Experience already earned is retained when the character is defeated.
Normal journey defeat does not remove XP.
Therefore:
Defeat is a setback to the current expedition, not a rollback of character progression.
 
⸻
 
6. LEVEL-UP
When accumulated XP reaches the required threshold, the character gains a level.
Level progression should be deterministic.
A level-up can trigger:
increased character power
attribute progression
access to abilities
access to equipment
access to content
The exact level-up reward structure is defined by the Character Foundation and Skills systems.
 
⸻
 
7. CHARACTER POWER VS ITEM POWER
Character level and equipment level are separate progression dimensions.
A player’s overall combat capability is therefore determined by a combination of:
Character
+
Skills
+
Abilities
+
Equipment
A high-level character should not automatically make every item irrelevant.
Likewise, an unusually strong item should not completely replace character progression.
 
⸻
 
8. ITEM LEVEL
Every generated equipment item has an item level.
Item level is a major determinant of the item’s total power.
The established design is:
Approximately 70% of item power comes from item level.
Item level therefore dominates item power.
 
⸻
 
9. ITEM QUALITY
Every generated equipment item also possesses an internal quality value.
Quality is:
generated internally
hidden from the player
used to modify total item power
used to determine the item’s visible quality tier
Quality can contribute:
Up to approximately 30% additional item power.
The quality contribution uses the established exponential scaling model, subject to the quality-base-threshold rules defined in this specification.
 
⸻
 
10. HIDDEN QUALITY
The player does not see a numerical quality score.
The player sees the resulting item statistics and visible rarity/presentation.
For example, two items may have:
Same template
Same item level
Different hidden quality
and therefore display different generated statistics.
The underlying quality value is an implementation detail.
 
⸻
 
11. QUALITY BASE THRESHOLD
Equipment quality uses a base threshold.
The base threshold is:
70% quality benefit
This means that quality values at or below the Common threshold do not reduce the item’s quality contribution below the 70% base benefit.
Conceptually:
Effective Quality Benefit = max(70%, Quality-Based Benefit)
The base threshold prevents low-quality items from receiving an excessively weak quality contribution while preserving meaningful differences among higher-quality items.
 
⸻
 
12. QUALITY TIERS
The quality value determines the item’s visible quality tier according to the following thresholds:
￼
The threshold boundaries are authoritative.
Therefore:
80.0%       → Common
80.000...%  → Uncommon
96.0%       → Uncommon
96.000...%  → Rare
99.5%       → Rare
99.500...%  → Epic
The implementation must use precise comparison rules to avoid ambiguity at boundary values.
 
⸻
 
13. COMMON QUALITY BENEFIT
All items with a quality value of 80% or less are Common.
Common items receive a fixed quality benefit of:
70%
Their quality value does not produce a variable benefit within the Common range.
Conceptually:
Quality = 0%   → Common → 70% benefit
Quality = 40%  → Common → 70% benefit
Quality = 70%  → Common → 70% benefit
Quality = 80%  → Common → 70% benefit
This creates a stable baseline for ordinary equipment.
 
⸻
 
14. UNCOMMON QUALITY BENEFIT
Items with a quality value above 80% and up to 96% are Uncommon.
Uncommon items receive a variable quality benefit.
The benefit increases according to the established quality curve as quality rises through the Uncommon range.
Conceptually:
80% < Quality ≤ 96%
The exact mathematical mapping from quality value to benefit remains governed by the exponential quality formula.
 
⸻
 
15. RARE QUALITY BENEFIT
Items with a quality value above 96% and up to 99.5% are Rare.
Rare items receive a variable quality benefit.
The benefit increases according to the established quality curve as quality rises through the Rare range.
Conceptually:
96% < Quality ≤ 99.5%
Rare items therefore represent highly exceptional quality outcomes.
 
⸻
 
16. EPIC QUALITY BENEFIT
Items with a quality value above 99.5% are Epic.
Epic items receive a variable quality benefit.
The benefit increases according to the established quality curve for values above the Epic threshold, subject to the global maximum quality contribution.
Conceptually:
Quality > 99.5%
Epic items represent the highest ordinary quality tier defined by this system.
 
⸻
 
17. QUALITY BENEFIT FUNCTION
The quality benefit function must apply the Common base threshold before calculating higher-tier variation.
Conceptually:
if Quality ≤ 80%:
    Quality Benefit = 70%
else:
    Quality Benefit = ExponentialQualityFunction(Quality)
The exponential function must be configured so that:
Common items receive exactly the 70% base benefit.
Uncommon items receive a variable benefit above the Common baseline.
Rare items receive a higher variable benefit than Uncommon items.
Epic items receive the highest ordinary variable benefit range.
The total quality contribution remains capped at approximately 30% of total item power.
 
⸻
 
18. QUALITY BENEFIT AND ITEM POWER
The conceptual item-power model is:
Total Item Power
    =
Level Contribution
    +
Quality Contribution
The intended distribution is approximately:
Level      ≈ 70%
Quality    ≤ 30%
The quality contribution is non-linear/exponential, with the Common base threshold applied.
This makes item level the dominant determinant while preserving meaningful excitement from unusually high-quality drops.
 
⸻
 
19. QUALITY TIER AND VISIBLE RARITY
Quality tier is the visible classification derived from the hidden quality value.
The player sees:
Common
Uncommon
Rare
Epic
The player does not see the underlying numerical quality value.
Quality tier communicates the item’s position within the quality distribution without exposing the exact generation value.
 
⸻
 
20. QUALITY AND RARITY
Quality and visible rarity are related but distinct concepts.
Quality is an internal numerical value.
Quality tier is the player’s visible classification.
Quality tier is derived from quality using the global thresholds defined above.
The thresholds are:
independent of item level
independent of item template
globally tunable
applied consistently across ordinary equipment
The quality thresholds must not change merely because an item has a different level or template.
 
⸻
 
21. HIDDEN QUALITY EXAMPLE
The following examples illustrate the quality-tier rules:
Quality = 65.0%
Tier    = Common
Benefit = 70% base benefit
Quality = 80.0%
Tier    = Common
Benefit = 70% base benefit
Quality = 85.0%
Tier    = Uncommon
Benefit = Variable benefit above the Common baseline
Quality = 96.0%
Tier    = Uncommon
Benefit = Variable Uncommon benefit
Quality = 97.0%
Tier    = Rare
Benefit = Variable Rare benefit
Quality = 99.5%
Tier    = Rare
Benefit = Variable Rare benefit
Quality = 99.6%
Tier    = Epic
Benefit = Variable Epic benefit
 
⸻
 
22. ITEM LEVEL SCALING
Item level scaling must remain controlled.
Increasing item level should increase item power substantially, but the progression curve must not produce uncontrolled numerical inflation.
The exact mathematical formula remains an implementation parameter.
The important invariant is:
Item-level progression must remain bounded and balanceable.
 
⸻
 
23. TEMPLATE-BASED STAT ALLOCATION
An item’s template determines how its total power is distributed between statistics.
Conceptually:
Item Level
      +
Hidden Quality
      ↓
Total Power
      ↓
Item Template
      ↓
Stat Allocation
      ↓
Generated Item
The template therefore defines the item’s intended mechanical identity.
 
⸻
 
24. TEMPLATE DETERMINISM
Given identical:
item template
item level
hidden quality
the generated item must have identical stat allocation.
There is no uncontrolled random stat allocation.
Therefore:
Same inputs = same generated item statistics.
The quality tier is derived from the hidden quality value and does not introduce an additional random stat-generation step.
 
⸻
 
25. ITEM GENERATION
Generated equipment is therefore deterministic.
An item can be represented conceptually as:
Template
+
Item Level
+
Quality
=
Quality Tier
+
Generated Statistics
This is important for:
balancing
reproducibility
debugging
server authority
predictable progression
economy control
 
⸻
 
26. RANDOMNESS
Randomness may determine which item/template/quality outcome is generated where the relevant loot system permits it.
However, once the generation inputs are established, stat generation itself is deterministic.
The game should not generate arbitrary stat combinations that cannot be reproduced from the item’s underlying parameters.
 
⸻
 
27. EQUIPMENT POWER PROGRESSION
The player should generally become stronger by finding or acquiring equipment with:
higher item levels
better generated statistics
better templates
higher-quality outcomes
higher quality tiers
However, higher item level should not guarantee that every item is automatically better for every build.
Template identity remains important.
 
⸻
 
28. BUILD-SPECIFIC EQUIPMENT
An item with lower total power can still be desirable when its template allocates power toward statistics that better suit the player’s build.
Therefore:
Item Power is not equivalent to Item Value.
A player should sometimes make meaningful decisions between different stat distributions.
 
⸻
 
29. EQUIPMENT QUALITY IS NOT THE WHOLE PROGRESSION
Quality is deliberately capped in influence.
Because quality contributes a maximum of approximately 30%, a very high-quality lower-level item cannot indefinitely outperform a substantially higher-level item.
The Common base threshold further ensures that ordinary low-quality items receive a stable minimum quality benefit rather than being excessively penalised.
This prevents the loot system from becoming dominated by lucky low-level drops while preserving meaningful quality differences among Uncommon, Rare and Epic items.
 
⸻
 
30. ECONOMIC CURRENCY
The primary general-purpose currency is:
Gold
Gold is used by the game’s economy.
Gold does not occupy inventory space.
 
⸻
 
31. GOLD SOURCES
Gold may be obtained from:
enemies
journeys
quests
dungeons
story rewards
selling items
other authored sources
Each source should have explicitly defined reward rules.
 
⸻
 
32. GOLD SINKS
Gold should have meaningful uses.
Potential sinks include:
purchases
services
equipment transactions
travel-related services
progression systems
other authored game systems
The final gold-sink catalogue remains TBD.
The economy should avoid introducing sinks merely to consume excess currency without gameplay purpose.
 
⸻
 
33. DEFEAT GOLD PENALTY
Normal journey defeat removes:
20% of the player’s current gold.
This percentage is fixed throughout the entire game.
It does not scale with:
character level
item level
enemy level
journey difficulty
location
The penalty is always 20%.
 
⸻
 
34. GOLD LOSS CALCULATION
The conceptual calculation is:
Gold Lost = Current Gold × 0.20
Gold Retained = Current Gold × 0.80
The server performs the authoritative calculation.
Rounding behaviour must be defined consistently in the technical implementation.
 
⸻
 
35. ITEM SALES
Spare equipment can potentially be sold for gold.
Selling is performed from a safe location.
Selling is therefore part of the inventory/economy management loop.
The exact sell-value formula remains TBD.
Sell value may use:
item level
quality tier
template
generated statistics
item category
content source
The final formula must not undermine the intended value of protected Epic, Legendary or Story items.
 
⸻
 
36. LOOT REWARDS
Combat and journey rewards can include generated equipment.
Generated equipment follows the item-generation rules:
Loot Selection
      ↓
Template
      ↓
Item Level
      ↓
Quality
      ↓
Quality Tier
      ↓
Generated Stats
The Loot System determines what can drop.
The Item Generation System determines what the resulting item actually is.
 
⸻
 
37. LOOT QUALITY DISTRIBUTION
The probability distribution of quality should be controlled by loot tables and content configuration.
The system must not assume that every item has an equal chance of every quality.
Content may define:
minimum quality
maximum quality
weighted quality ranges
quality-tier eligibility
template eligibility
item-level range
source-specific quality modifiers
The quality thresholds remain globally consistent even when different content uses different quality distributions.
 
⸻
 
38. QUALITY-TIER ELIGIBILITY
Loot tables may restrict which quality tiers can be generated.
For example, content may define:
Early Content
    Common only
Intermediate Content
    Common and Uncommon
Advanced Content
    Common through Rare
Endgame Content
    Common through Epic
These restrictions affect generation eligibility, not the meaning of the global quality thresholds.
 
⸻
 
39. RARITY PROGRESSION
Visible quality tier communicates the item’s quality range to the player without exposing the hidden quality number.
The player therefore evaluates equipment primarily through:
visible quality tier
generated statistics
item level
template
build compatibility
rather than a raw hidden-quality value.
 
⸻
 
40. EPIC, LEGENDARY AND STORY ITEMS
Epic, Legendary and Story items have special protection in the journey-loss system.
They are never lost through ordinary defeat.
This does not require them to use the same generation process as ordinary equipment.
In particular:
Epic items are generated through the ordinary quality system when their quality exceeds 99.5%.
Legendary items may be specially generated or authored.
Story items are authored around narrative requirements.
Story Relics are protected equipment.
The exact Legendary and Story generation rules belong to the Equipment & Loot specification.
 
⸻
 
41. REWARD PROGRESSION
Rewards should scale appropriately with the content that produced them.
The system should distinguish between:
character progression
journey progression
equipment progression
economic rewards
story rewards
quality-tier progression
This prevents one reward system from becoming the sole progression path.
 
⸻
 
42. PROGRESSION AND JOURNEYS
Journeys are the primary recurring progression loop.
Conceptually:
Prepare
 ↓
Journey
 ↓
Combat
 ↓
XP + Gold + Loot
 ↓
Character / Equipment Progression
 ↓
Harder Journey
 ↓
Better Rewards
The loop should remain viable for both active and returning/idle players.
 
⸻
 
43. PROGRESSION AND DEFEAT
Defeat deliberately preserves long-term progress.
The player loses:
20% gold
potentially eligible spare items
The player retains:
XP
character levels
equipped equipment
Epic items
Legendary items
Story items
Story progress
This creates risk without making failure feel like a complete reset.
 
⸻
 
44. CONTROLLED POWER CURVE
The game’s progression must maintain a controlled power curve.
Particular attention should be paid to:
character levels
item levels
enemy levels
Defence
penetration
damage
health
status effects
quality-tier distribution
quality contribution
No individual scaling system should be allowed to grow independently without considering the others.
 
⸻
 
45. LEVEL-BASED POWER VS LUCK-BASED POWER
The item system intentionally favours progression over luck.
Approximately:
70% of item power is driven by item level.
Therefore:
progressing through the game reliably increases potential item power
lucky high-quality drops provide excitement
quality cannot completely replace item-level progression
Common items remain viable through the 70% quality base benefit
Uncommon, Rare and Epic items provide increasingly valuable quality outcomes
This is a core design principle.
 
⸻
 
46. POWER ALLOCATION
The item template is responsible for allocating total item power.
For example, a hypothetical template could define:
Weapon Template
    60% → Attack Power
    25% → Critical-related statistic
    15% → Secondary statistic
The actual percentages are template data.
The generation engine applies the template consistently.
The quality tier does not change the item’s template identity. It modifies total available item power through the quality contribution.
 
⸻
 
47. NO ARBITRARY STAT ROLLING
The game should not generate items by independently rolling every stat.
That would produce:
incoherent items
excessive balancing problems
unpredictable power
difficult reproduction
difficult server validation
Instead, item generation is template-driven.
 
⸻
 
48. SERVER AUTHORITY
The server is authoritative over:
XP
character level
gold
item level
item quality
quality tier
item statistics
rewards
item sales
defeat penalties
The client cannot directly modify progression values.
 
⸻
 
49. TRANSACTIONAL REWARDS
Rewards should be processed atomically.
For example, completing an encounter should not produce a state where:
XP was granted
but loot was not
or gold was granted twice
or the same item was generated twice
or an item’s quality tier does not match its quality value
Journey resolution should produce one authoritative state transition.
 
⸻
 
50. MULTIPLATFORM PERSISTENCE
Progression is attached to the server-side character/account state rather than the device.
The same progression must therefore be available across supported clients.
The player’s:
level
XP
gold
skills
abilities
equipment
inventory
journey state
item quality
quality tier
are persistent.
 
⸻
 
51. DESIGN INVARIANTS
Character level is distinct from item level.
XP is retained after normal defeat.
Gold is the primary general-purpose currency.
Gold occupies no inventory slots.
Normal defeat removes exactly 20% of current gold.
The 20% penalty remains flat throughout the entire game.
Item level is the dominant contributor to item power.
Approximately 70% of item power comes from item level.
Quality contributes up to approximately 30% additional power.
Quality contribution follows an exponential curve above the base threshold.
Quality is hidden from the player.
Quality values of 80% or less are Common.
Common items receive a fixed 70% quality benefit.
Quality values above 80% and up to 96% are Uncommon.
Uncommon items receive variable quality benefit.
Quality values above 96% and up to 99.5% are Rare.
Rare items receive variable quality benefit.
Quality values above 99.5% are Epic.
Epic items receive variable quality benefit.
Visible quality tier is derived from hidden quality.
Quality thresholds are globally configurable.
Quality thresholds do not depend on item level or template.
Item templates determine power allocation between stats.
Identical template + level + quality produces identical generated stats.
Item stat allocation is deterministic.
Higher item power does not automatically mean greater build value.
Item progression is controlled rather than unbounded.
Epic, Legendary and Story items are protected from ordinary defeat loss.
Story Relics are protected.
Equipped items are protected.
Character progression is not erased by normal defeat.
Progression state is server-authoritative.
Rewards are processed atomically.
Progression persists independently of client platform.
Quality tier must always match the authoritative quality value.
Common quality benefit cannot fall below the 70% base threshold.
Quality cannot contribute more than the configured maximum of approximately 30% of item power.
 
⸻
 
52. OPEN PARAMETERS
These are genuine remaining design parameters, not previously settled questions:
Maximum character level
XP curve
Character-level stat progression
Attribute gain per level
Gold sources
Gold sinks
Gold reward scaling
Item-level progression relative to character level
Exact 70/30 mathematical implementation
Exact exponential quality-benefit curve
Quality range and precision
Exact quality-benefit values at the Uncommon, Rare and Epic boundaries
Whether the Epic quality benefit has a hard upper bound or asymptotic cap
Exact boundary comparison implementation
Template catalogue
Template stat-allocation rules
Sell-value formula
Loot-quality distributions
Quality-tier eligibility by content
Economy inflation controls
Level caps/scaling boundaries
Exact rounding rules
 
⸻
 
53. DEPENDENCIES
Depends on
Character Foundation
Equipment & Loot
Inventory
Combat
Enemy & Boss
Journey & Dungeon
Story
Used by
Character
Equipment
Loot
Combat
Journey
Economy
Story
UI
Persistence
 
⸻
 
END OF SPECIFICATION
