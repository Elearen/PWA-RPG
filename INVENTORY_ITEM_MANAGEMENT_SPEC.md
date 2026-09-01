INVENTORY & ITEM MANAGEMENT SYSTEM SPECIFICATION
Document: INVENTORY_AND_ITEM_MANAGEMENT_SPEC Version: 0.1 Status: Active Design Purpose: Defines player inventory capacity, equipment storage, item slots, item accessibility, journey loot reservation, pending loot, and item-loss behaviour.
 
⸻
 
1. DESIGN GOALS
The inventory system should be:
Simple to understand.
Deliberately constrained.
Meaningful as part of journey preparation.
Integrated with the game’s risk/reward model.
Compatible with automated journeys.
Persistent across platforms.
Server-authoritative.
Inventory space is intended to be a meaningful resource rather than an effectively unlimited storage system.
 
⸻
 
2. TOTAL INVENTORY CAPACITY
Each character has exactly:
50 inventory slots
This is the player’s complete personal item storage capacity.
There is no automatic expansion of the base inventory in this specification.
 
⸻
 
3. ONE ITEM PER SLOT
Every individual item occupies exactly one inventory slot.
Items do not stack.
For example:
Potion ×1 = 1 slot
Potion ×10 = 10 slots
Sword ×1 = 1 slot
Sword ×5 = 5 slots
Identical items therefore still consume separate slots.
 
⸻
 
4. NO SEPARATE STORAGE
The game does not provide separate:
bank
stash
warehouse
equipment storage
secondary personal inventory
The 50 slots represent the character’s complete personal item storage.
Equipment is not moved into a separate storage system when equipped.
 
⸻
 
5. EQUIPMENT SLOTS
The character has the following equipment slots:
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
The Story Relic slot is treated as a normal equipment slot for equipment-management purposes.
 
⸻
 
6. EQUIPPED ITEMS
Equipped items are distinct from spare items carried in the bag.
An equipped item occupies an equipment slot.
The equipped item is therefore not treated as an ordinary spare item in the bag for item-loss calculations.
 
⸻
 
7. EQUIPPED ITEM PROTECTION
Equipped items are never lost as a consequence of ordinary journey defeat.
This applies regardless of item quality.
Therefore:
Equipped Common     → Protected
Equipped Uncommon   → Protected
Equipped Rare       → Protected
Equipped Epic       → Protected
Equipped Legendary  → Protected
Equipped Story      → Protected
This ensures that ordinary defeat cannot destroy the player’s active build.
 
⸻
 
8. ITEM QUALITY PROTECTION
Item quality affects whether an item is at risk when it is a spare item.
The following item categories are permanently protected from ordinary defeat loss:
Epic
Legendary
Story
This protection applies whether the item is:
equipped
carried as a spare item
pending travel loot
 
⸻
 
9. SPARE ITEM RISK
Common, Uncommon and Rare items carried as spare items in the bag are eligible to be lost through the game’s journey-loss mechanic.
Therefore:
                    EQUIPPED       BAGGED SPARE
Common              Protected      At Risk
Uncommon            Protected      At Risk
Rare                Protected      At Risk
Epic                Protected      Protected
Legendary           Protected      Protected
Story               Protected      Protected
 
⸻
 
10. ITEM LOSS IS NOT UNIVERSAL
The game does not destroy arbitrary items from the character’s entire inventory.
Only items that satisfy the loss criteria are placed into the loss pool.
The loss pool consists of:
Common + Uncommon + Rare spare items
Equipped items and protected-quality items are excluded.
 
⸻
 
11. INVENTORY MANAGEMENT LOCATION
Inventory management is only available at a safe location.
The player cannot manage inventory while travelling.
This includes:
opening/managing the bag
moving items
selling items
equipping items
unequipping items
using consumables
while travelling.
 
⸻
 
12. SAFE-AREA MANAGEMENT
At a safe location the player can perform normal inventory management.
This creates a clear gameplay boundary:
SAFE LOCATION
    ↓
Inventory management
    ↓
Equipment configuration
    ↓
Consumable use
    ↓
Journey preparation
    ↓
DEPARTURE
    ↓
Inventory locked
 
⸻
 
13. INVENTORY LOCK DURING JOURNEY
Once a character departs on a journey, their inventory becomes unavailable for manual management.
The player cannot:
equip an item
unequip an item
swap equipment
sell an item
move items between slots
use a consumable
until the character returns to a safe location.
 
⸻
 
14. CONSUMABLES
Consumables can only be used in safe areas.
They cannot be used:
during combat
while travelling
between encounters
in unsafe regions
This intentionally makes consumables a preparation/recovery resource rather than a routine combat action.
 
⸻
 
15. JOURNEY INVENTORY RESERVATION
Before departing on a journey, the system checks whether sufficient inventory capacity is available for expected equipment drops.
A minimum of:
5 inventory slots
is always reserved for potential journey loot.
However, the reservation can be larger when the journey’s deterministic maximum equipment-drop capacity requires it.
Conceptually:
Reserved Slots =
max(5, deterministic maximum equipment drops)
 
⸻
 
16. RESERVATION TIMING
The inventory reservation is checked:
Before departure.
The character cannot begin a journey if the required reservation cannot be satisfied.
This prevents the character from entering a journey with insufficient space to receive its guaranteed/possible equipment rewards.
 
⸻
 
17. RESERVATION IS NOT PERMANENT STORAGE
Reserved slots are not additional inventory capacity.
They are a journey-entry validation mechanism.
The character still has exactly:
50 total inventory slots.
The reservation simply ensures that enough capacity exists for the journey’s expected equipment drops.
 
⸻
 
18. PENDING TRAVEL LOOT
Loot generated during a journey is tracked separately as:
Pending Travel Loot
Pending Travel Loot is not immediately inserted into the player’s accessible 50-slot bag.
It is held by the journey state.
 
⸻
 
19. PENDING LOOT ACCESS
Pending Travel Loot is inaccessible to the player while travelling.
The player cannot:
inspect it for management purposes
equip it
sell it
discard it
move it
otherwise manipulate it
while the character remains on the journey.
 
⸻
 
20. PENDING LOOT AND INVENTORY CAPACITY
Pending Travel Loot does not allow the player to circumvent the 50-slot inventory limit.
The journey reservation exists specifically to ensure the relevant equipment loot can ultimately be accommodated.
The pending-loot system is therefore a temporary holding state, not a second inventory.
 
⸻
 
21. PENDING LOOT AND DEFEAT
Pending Travel Loot is subject to the journey’s defeat/loss rules.
If the character is defeated before successfully returning with the loot, eligible pending items may be lost.
However:
Epic, Legendary and Story items are protected immediately when generated.
Therefore a protected-quality item does not become vulnerable simply because it is currently pending.
 
⸻
 
22. PENDING LOOT PROTECTION
Pending loot follows the same fundamental protection hierarchy:
Epic       → Protected
Legendary  → Protected
Story      → Protected

Common     → Potentially vulnerable
Uncommon   → Potentially vulnerable
Rare       → Potentially vulnerable
The exact percentage/selection of vulnerable pending loot is determined by the Journey/death rules.
 
⸻
 
23. RETURNING FROM A JOURNEY
When a journey successfully reaches a safe location:
Journey progression is resolved.
Pending loot is finalised.
Protected items remain protected.
Eligible loot is transferred into the character’s inventory.
Inventory capacity is validated.
The journey is completed.
The exact ordering of reward resolution and inventory insertion belongs to the journey transaction model.
 
⸻
 
24. JOURNEY DEFEAT
If the character is defeated:
the character retreats to the previous safe location
20% of gold is lost
eligible spare items may be lost
equipped items are protected
Epic items are protected
Legendary items are protected
Story items are protected
XP is retained
The Inventory system supplies the eligible item-loss pool.
The Journey system controls the defeat event itself.
 
⸻
 
25. GOLD
Gold is not an inventory item and does not occupy an inventory slot.
Normal defeat removes:
20% of current gold
This percentage remains flat throughout the game.
Gold does not require a reserved inventory slot.
 
⸻
 
26. ITEM IDENTITY
Every individual item should have its own persistent identity.
Conceptually:
Item
 ├── Item ID
 ├── Template ID
 ├── Level
 ├── Quality
 ├── Generated Stats
 ├── Location
 └── Ownership
The exact data model belongs to the Technical Architecture specification.
 
⸻
 
27. ITEM LOCATION STATES
An item should have an explicit location/state.
At minimum:
EQUIPPED
BAG
PENDING_TRAVEL_LOOT
Additional internal states may exist for transactions.
This prevents ambiguity when calculating:
accessibility
inventory capacity
equipment state
item-loss eligibility
 
⸻
 
28. EQUIPMENT VS BAG
The system must maintain a clear distinction between:
Equipped Item
and:
Spare Bag Item
This distinction is important because quality alone does not determine risk.
For Common/Uncommon/Rare items:
equipped = protected
bagged spare = potentially lost
For Epic/Legendary/Story items:
equipped = protected
bagged spare = protected
 
⸻
 
29. STORY RELIC
The Story Relic is an equipment slot.
A Story Relic is therefore equipped and managed through the same general equipment framework as the other equipment slots.
However, Story Relics are protected from ordinary loss.
A Story Relic cannot be lost through ordinary journey defeat.
 
⸻
 
30. INVENTORY VALIDATION
The server must validate inventory operations.
The client cannot directly assert:
available capacity
item ownership
item location
equipment state
item quality
successful equipment
item transfer
All authoritative item state is maintained server-side.
 
⸻
 
31. ATOMIC ITEM TRANSACTIONS
Inventory-changing operations should be atomic.
For example, equipping an item should not produce a state where:
Item is removed from bag
AND
Item is not equipped
because of an interrupted request.
Likewise, journey reward insertion and defeat-loss processing must be handled as atomic server-side transactions.
 
⸻
 
32. CONCURRENCY
Because the game is persistent and multiplatform, inventory operations must account for multiple clients/devices potentially accessing the same account.
The server must prevent:
duplicated items
duplicated rewards
duplicated equipment
double-selling
conflicting equipment state
duplicated pending loot
The exact concurrency strategy belongs to the Technical Architecture specification.
 
⸻
 
33. ITEM STACKING
No item stacking is currently permitted.
If a player owns ten identical consumables:
10 consumables = 10 inventory slots
This deliberately makes inventory management meaningful.
 
⸻
 
34. INVENTORY PRESSURE
Inventory capacity is intended to create decisions.
The player must periodically decide whether to:
retain spare equipment
sell unwanted equipment
prepare for another journey
manage consumables
preserve valuable items
Because Epic, Legendary and Story items are protected, inventory pressure primarily affects lower-quality spare equipment.
 
⸻
 
35. DESIGN INVARIANTS
Base inventory capacity is exactly 50 slots.
Every individual item occupies one slot.
Items do not stack.
There is no bank.
There is no stash.
There is no separate equipment storage.
There are 11 equipment slots.
The Story Relic is a normal equipment slot.
Equipped items are never lost through ordinary defeat.
Epic items are never lost through ordinary defeat.
Legendary items are never lost through ordinary defeat.
Story items are never lost through ordinary defeat.
Common/Uncommon/Rare spare bag items can be lost.
Inventory management is restricted to safe locations.
Inventory cannot be manually managed during travel.
Consumables can only be used in safe areas.
A journey reserves at least five inventory slots.
The reservation can exceed five slots where the journey’s deterministic maximum equipment drops require it.
Reservation is validated before departure.
Reserved slots are not additional inventory capacity.
Pending travel loot is stored separately from the accessible bag.
Pending travel loot is inaccessible during travel.
Pending Epic/Legendary/Story items are protected immediately when generated.
Pending lower-quality items can be subject to journey loss.
Gold does not occupy inventory space.
Normal defeat removes 20% of gold.
Inventory state is server-authoritative.
Inventory-changing operations are atomic.
Item identity is persistent.
Equipped and spare-item states remain explicitly distinguishable.
 
⸻
 
36. DEPENDENCIES
Depends on
Equipment & Loot
Journey & Dungeon
Character Foundation
Story
Persistence
Used by
Equipment
Journey
Loot
Combat preparation
Economy
Story
UI
Server persistence
 
⸻
 
37. OPEN PARAMETERS
The following still require explicit definition:
Exact algorithm for selecting vulnerable Common/Uncommon/Rare items on defeat
Exact journey-specific pending-loot loss percentage
Whether item-loss selection is random or deterministic
Selling rules
Item destruction/discard rules
Maximum consumable catalogue
Exact inventory UI
Item sorting/filtering
Whether empty slots have explicit ordering
Transaction implementation
Exact server concurrency strategy
These are intentionally left open.
 
⸻
 
END OF SPECIFICATION
