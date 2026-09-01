UI & UX SYSTEM SPECIFICATION
Document: UI_UX_SPEC Version: 1.0 Status: Design Locked Purpose: Defines the player-facing interface, navigation, information architecture, responsive behaviour and interaction patterns for the persistent, UI-driven RPG.
 
⸻
 
1. DESIGN PHILOSOPHY
The game is a mobile-first persistent RPG web application.
The interface should feel like a classic fantasy RPG without reproducing the usability problems of older game interfaces.
The design direction is:
Retro-inspired fantasy presentation with modern, clean usability.
The interface should feel atmospheric and distinctive while remaining fast, readable and intuitive on a phone.
 
⸻
 
2. PRIMARY UX PRINCIPLES
The interface must prioritise:
Clarity
Fast interaction
Readability
Low cognitive friction
Strong narrative atmosphere
Discoverability
Mobile usability
Consistency
Appropriate information hiding
Responsive performance
Context-appropriate actions
The UI should make a complex RPG feel approachable without removing the underlying depth of its systems.
 
⸻
 
3. MOBILE-FIRST
The application is designed mobile-first.
Primary design assumptions:
one-handed interaction should be possible for common actions
touch targets must be sufficiently large
important information must remain readable on small screens
navigation must work without hover
panels must adapt vertically
complex screens should use progressive disclosure
player actions should remain within the relevant screen or tab
Desktop layouts are derived from the mobile information architecture rather than the reverse.
 
⸻
 
4. RESPONSIVE DESIGN
The interface must support:
mobile portrait
mobile landscape
tablet
desktop
large desktop displays
The layout should reflow rather than simply scale.
Example:
MOBILE
[Header]
[Primary Content]
[Contextual Content]
[Relevant Screen Actions]
[Bottom/Primary Navigation]

DESKTOP
[Sidebar] [Primary Content] [Contextual Information]
Actions should remain attached to the screen or tab that owns them. Responsive layouts may reposition action controls, but should not move them into unrelated navigation areas.
 
⸻
 
5. VISUAL DIRECTION
The visual style is:
Retro-inspired fantasy + modern interface design.
The interface may use:
fantasy typography
parchment-inspired surfaces
subtle pixel-art influence
illustrated icons
restrained ornamental framing
fantasy-inspired dividers
atmospheric backgrounds
strong location-specific motifs
However:
Decoration must never compromise usability.
The game should feel like a world rather than a generic CRUD web application.
 
⸻
 
6. WORLD-SPECIFIC VISUAL IDENTITY
The UI should reflect the established world and its three starting regions.
The interface may subtly adapt to the current protagonist/location.
Examples:
FOREST
Natural / rural / earthy visual language

COAST
Merchant / maritime / urban visual language

MOUNTAINS
Stone / forge / dwarven visual language
These are presentation differences, not separate UI systems.
The underlying interaction patterns remain consistent.
 
⸻
 
7. PRIMARY NAVIGATION
The game uses a persistent RPG-style navigation bar.
The navigation should remain recognisable throughout the application.
Primary destinations include the established major systems, such as:
Explore/Navigation
Character
Inventory
Skills
Journal
Shop when available
Combat when active
World/Map where applicable
The primary navigation provides access to major screens and tabs. It must not become a catch-all location for actions belonging to other systems.
Exact labels and ordering should be refined during implementation.
 
⸻
 
8. SCREEN AND TAB OWNERSHIP
Every player action must belong to the screen or tab that provides the context required to perform it.
The interface should follow this rule:
Actions stay with the system they affect.
Examples:
EXPLORE / NAVIGATION TAB
Travel
Choose destination
Interact with NPC
Enter dungeon
Inspect location
Rest where available

SHOP TAB
Browse stock
Inspect item
Buy
Sell where permitted
Compare equipment

COMBAT TAB
Attack
Use ability
Defend
Retreat where permitted
Inspect enemy
Review combat details

CHARACTER TAB
Equip
Unequip
Inspect equipment
Review stats
Manage abilities where applicable

INVENTORY TAB
Use item
Inspect item
Compare item
Equip item
Discard or manage item where permitted

JOURNAL TAB
Read entry
Filter
Search
Review discoveries
Actions should not be duplicated in unrelated tabs unless there is a clear, intentional shortcut that preserves the same context.
 
⸻
 
9. CONTEXTUAL ACTIONS
Although the primary navigation persists, available actions should change according to the active screen, tab and player state.
Actions must be presented within the relevant screen rather than in a generic global action area.
Examples:
EXPLORE / NAVIGATION
Travel
Visit NPC
Enter shop
Rest
Continue journey

SHOP
Buy
Sell
Inspect item
Compare equipment

DUNGEON
Explore
Fight
Retreat
Inspect discovery

COMBAT
Attack
Use ability
Defend
Inspect enemy

JOURNAL
Read
Filter
Search
Review discoveries
The interface should not expose irrelevant actions.
 
⸻
 
10. CURRENT STATE PROMINENCE
Every major screen should make the player’s current state immediately obvious.
Examples:
current location
current character
HP/resource state
active activity
active screen or tab
important available actions
relevant progression
The player should not need to navigate through several menus simply to understand where they are.
The active screen should also make its available actions obvious without requiring the player to search through unrelated navigation elements.
 
⸻
 
11. INFORMATION DENSITY
The game contains deep systems but the default interface should remain relatively simple.
The primary rule is:
Show what matters now; allow the player to inspect what matters in depth.
Advanced information should generally be hidden behind:
inspection
expansion
detail panels
tooltips
secondary views
Actions should remain visible at the point where the player needs them, while unrelated actions remain hidden.
 
⸻
 
12. PROGRESSIVE DISCLOSURE
Complex mechanics should be progressively revealed.
A player encountering a new item should first see its useful gameplay information.
They can then inspect deeper information if desired.
Conceptually:
ITEM
 ↓
Basic stats
 ↓
Detailed stats
 ↓
Advanced mechanics
This is particularly important because the RPG contains deep item generation and combat systems.
 
⸻
 
13. TOOLTIP SYSTEM
The game uses both:
quick tooltips
dedicated inspection panels
Tooltips should explain unfamiliar terms without forcing the player to leave the current screen.
Inspection panels provide the full explanation.
Tooltips and inspection panels must not relocate the player into an unrelated system merely to understand the current action or object.
 
⸻
 
14. HIDDEN ITEM QUALITY
The existing item system defines an underlying quality value that contributes to generated item power.
That quality is not directly exposed to the player.
The UI must therefore never present a raw field such as:
Quality: 82%
Instead, the player sees the resulting generated statistics.
The interface should preserve the intended discovery of item differences.
 
⸻
 
15. CHARACTER SCREEN
The Character screen presents the current protagonist.
It should provide access to:
level
XP
attributes
derived statistics
skills
equipment
relevant progression information
The presentation should prioritise the information required for making decisions.
Advanced calculations may be exposed through inspection.
Character actions such as equipping, unequipping and managing character-specific abilities should remain within the Character screen or its relevant sub-tabs.
 
⸻
 
16. EQUIPMENT SCREEN
The Equipment interface presents the established equipment slots.
The interface should clearly distinguish:
EQUIPPED
from:
SPARE INVENTORY
This distinction is particularly important because equipped items and spare items have different death-risk rules.
Equipment actions should remain within the Character/Equipment screen or the relevant item-management context. A global navigation area should not become the primary location for equipment actions.
 
⸻
 
17. INVENTORY
Inventory should prioritise:
item identification
quantity
equipment state
usability
comparison
item management
The interface should avoid displaying unnecessary technical information by default.
Inventory actions such as using, equipping, inspecting and managing items should be available within the Inventory screen or its item inspection flow.
 
⸻
 
18. ITEM INSPECTION
Selecting an item opens an inspection view.
The inspection view may display:
item name
level
generated statistics
equipment slot
effects
requirements
relevant restrictions
comparison against equipped item
actions available for that item in the current context
The underlying hidden quality value remains hidden.
Item actions should remain attached to the item inspection context. For example, an item opened from a shop should expose shop-relevant actions such as Buy, while an item opened from Inventory should expose inventory-relevant actions such as Use or Equip.
 
⸻
 
19. ITEM COMPARISON
When an item can replace an equipped item, the UI should provide a clear comparison.
Conceptually:
CURRENT
    vs
NEW ITEM

Attack       42 → 47
Defence      18 → 16
Effect       ...
The player should be able to understand the practical impact without calculating it manually.
Comparison should be available from the relevant item context, such as Inventory, Shop or Equipment, without requiring the player to navigate to a separate unrelated action area.
 
⸻
 
20. SKILLS & ABILITIES
The Skills interface should present the established skill/ability system.
It should distinguish between:
available abilities
learned abilities
equipped/active abilities where applicable
unavailable abilities
ability requirements
effects
Detailed mechanical explanations should be available through inspection.
Skill and ability management actions should remain within the Skills screen or the relevant Character sub-tab.
 
⸻
 
21. COMBAT UI
Combat uses a visual-first presentation.
The primary interface should emphasise:
player state
enemy state
current combat situation
available actions
meaningful effects
important events
The combat log should not dominate the screen.
All primary combat actions must remain within the Combat screen or Combat tab.
 
⸻
 
22. COMBAT LOG
Detailed combat information remains available, but is secondary.
The player should be able to inspect the combat log when they want to understand:
damage
effects
ability outcomes
status changes
combat events
The normal combat experience should not require reading a large scrolling text log.
Combat details should be accessible from within the Combat screen rather than through a separate global notification or navigation action.
 
⸻
 
23. COMBAT ACTIONS
Combat actions should be immediately accessible within the Combat screen.
The interface should clearly distinguish:
standard actions
abilities
unavailable actions
actions with resource requirements
actions requiring specific conditions
Unavailable actions should communicate why they are unavailable where practical.
Combat actions should not be placed in the general navigation bar, Inventory tab or another unrelated screen.
 
⸻
 
24. ENEMY PRESENTATION
The enemy presentation should emphasise:
identity
threat level
health/state
relevant visible effects
important combat characteristics
Detailed enemy information may be available through inspection.
Enemy inspection should remain within the Combat screen or open as a contextual overlay from that screen.
 
⸻
 
25. BOSS PRESENTATION
Boss encounters may receive enhanced presentation.
A boss screen may use:
larger enemy presentation
stronger visual framing
dramatic transitions
special status displays
more prominent encounter information
This does not require complex real-time graphics.
Boss actions remain within the Combat screen.
 
⸻
 
26. STORY PRESENTATION
Story Bites are a primary narrative delivery mechanism.
A newly discovered Story Bite immediately interrupts gameplay with a dedicated story presentation.
The player reads the Story Bite before returning to gameplay.
The interruption may temporarily suspend the current screen, but returning from the Story Bite should restore the player to the same relevant screen or tab.
 
⸻
 
27. STORY BITE SCREEN
Story Bites should have a distinctive presentation.
The screen should feel like a deliberate narrative moment rather than a normal notification.
Possible elements:
atmospheric background
character/location artwork where available
narrative typography
short text blocks
continuation/dismissal action
subtle transition effects
The interface should remain fast and readable.
 
⸻
 
28. STORY BITE INTERRUPTION
The interruption should occur at an appropriate safe narrative boundary.
The game should avoid losing important gameplay state because of the interruption.
The Story Bite should be recorded as discovered before or as part of the relevant authoritative game operation.
After the Story Bite is dismissed, the player should return to the screen or tab from which the interruption occurred.
 
⸻
 
29. JOURNAL
The Journal contains the character’s accumulated knowledge.
It should provide access to categories such as:
Story Bites
people
places
factions
lore
mysteries
relevant quest information
The Journal should feel like an in-world record rather than simply a database browser.
Journal actions such as reading, filtering and searching should remain within the Journal screen.
 
⸻
 
30. JOURNAL VS WORLD TRUTH
The Journal reflects character knowledge, not the game’s omniscient world state.
The UI must not expose information merely because the server knows it.
This is especially important to the three-perspective narrative structure.
 
⸻
 
31. QUEST UI
Quest presentation should clearly communicate:
quest identity
current objective
progress
rewards where appropriate
relevant narrative information
current status
Completed objectives should be visually distinct.
Quest actions such as reviewing objectives, tracking progress and reading related information should remain within the Quest or Journal screen. Actions that change the world, such as travelling to a quest location or interacting with an NPC, should be performed from the relevant Explore/Navigation or NPC screen.
 
⸻
 
32. JOURNEY UI
The Journey system provides the player’s primary navigation through the world.
The interface should communicate:
current location
available destinations
journey status
hazards
encounters
relevant discoveries
available actions
Travel actions must remain within the Explore/Navigation or Journey screen.
The established Journey/Dungeon mechanics remain authoritative; this specification only defines their presentation.
 
⸻
 
33. WORLD NAVIGATION
World navigation is primarily UI/text-based rather than a graphical map-first interface.
The player should navigate through clearly presented:
locations
routes
destinations
regional information
contextual travel choices
A map may exist as a supporting visualisation, but it is not the primary navigation mechanism.
Travel, destination selection and location-based actions should remain within the Explore/Navigation tab.
 
⸻
 
34. DUNGEON UI
Dungeon screens should clearly communicate:
dungeon identity
current progression
current area/state
available actions
threats
discoveries
rewards
exit/retreat options
Dungeon navigation should feel distinct from ordinary world navigation without requiring complex graphical environments.
Dungeon actions should remain within the Dungeon or Explore/Navigation screen. They should not be moved into a generic global action menu.
 
⸻
 
35. NPC INTERFACE
NPC interactions should be presented as contextual interactions rather than generic database records.
An NPC screen may provide:
identity
contextual description
dialogue/story content
available interactions
relevant quests
faction context
relationship information where appropriate
NPC interaction actions must remain within the Explore/Navigation screen or the active NPC interaction view.
Examples include:
Talk
Trade where applicable
Accept or review relevant dialogue
Ask about available topics
Continue an NPC-related interaction
These actions should not be placed in the Shop, Character, Journal or global navigation areas unless the player has explicitly entered the corresponding system.
 
⸻
 
36. SHOP UI
Vendor screens should prioritise rapid comparison and decision-making.
The player should be able to:
browse stock
inspect items
compare equipment
buy
sell where permitted
understand prices
understand relevant restrictions
All shop actions must remain within the Shop screen or Shop tab.
The Shop tab should be entered from the relevant Explore/NPC interaction, but once active it owns the shop actions. Buying and selling should not be performed from the general Explore action area, Character screen or Inventory screen unless a deliberate contextual shortcut is provided.
 
⸻
 
37. ECONOMY DISPLAY
Gold should always be readily visible in relevant economic contexts.
The UI should clearly distinguish:
current gold
transaction cost
transaction result
Economic changes should provide immediate feedback.
Shop transaction feedback should appear within the Shop screen or its contextual transaction flow.
 
⸻
 
38. DEATH SCREEN
Death uses a dedicated dramatic death screen.
When the character enters the defeated state, the interface transitions away from normal gameplay into a distinctive death presentation.
The screen should communicate:
defeat
narrative/atmospheric significance
relevant next action
eventual return to gameplay
The death screen should not expose implementation details.
 
⸻
 
39. RESPAWN
The respawn interaction occurs through the death flow.
The player should understand:
DEFEATED
 ↓
Death Screen
 ↓
Respawn
 ↓
Death Consequences
 ↓
Return to Game
The exact penalty calculation remains defined by the existing Death and Persistence specifications.
Respawn actions belong exclusively to the Death screen and should not appear in normal navigation or unrelated tabs.
 
⸻
 
40. CHARACTER SWITCHING
Character switching occurs through a dedicated character-selection/account screen.
It is not a casual action embedded throughout gameplay.
This reinforces that switching protagonists is a meaningful change of playthrough.
 
⸻
 
41. CHARACTER SELECTION
The character-selection screen should present the three protagonists distinctly.
Each should communicate:
protagonist identity
current progression
current location
campaign status
relevant save/playthrough information
The player should be able to select an existing playthrough or begin an additional playthrough where permitted.
Character-selection actions should remain within the Character Selection screen.
 
⸻
 
42. COMPLETED CAMPAIGNS
A completed campaign should be visibly marked as complete.
The interface should not imply that the main story can continue indefinitely after its final state.
Completed campaigns can remain accessible for review/replay management.
Campaign review and replay-management actions should remain within the Character Selection or Account screen.
 
⸻
 
43. NOTIFICATION SYSTEM
Notifications should be reserved for useful events.
Examples:
new item
quest update
new Journal entry
Story Bite
level increase
important world development
Notifications should not replace the dedicated presentation of major narrative events.
Notifications may direct the player to the relevant screen, but the underlying action must be completed in that screen. For example, a shop-related notification may direct the player to the Shop tab, while a combat notification may direct the player to the Combat tab.
 
⸻
 
44. ERROR PRESENTATION
Errors should be understandable to ordinary players.
Avoid exposing technical messages such as:
500 INTERNAL SERVER ERROR
DATABASE TRANSACTION FAILED
Instead:
Something went wrong.
Your progress has not been lost.
Please try again.
Technical details should be logged separately.
When an action fails, the error should appear in the screen or tab where the action was attempted.
 
⸻
 
45. SAVE / SYNC FEEDBACK
Because saving is automatic, the UI should provide subtle confirmation where useful.
Examples:
syncing
saved
connection interrupted
reconnecting
The system should not repeatedly interrupt gameplay with unnecessary save messages.
Save and sync indicators may be global because they describe application state, but they must not replace or obscure the relevant screen action.
 
⸻
 
46. CONNECTION STATE
The interface should communicate meaningful connection problems.
For example:
ONLINE

RECONNECTING…

OFFLINE
The game should distinguish between:
cached/read-only functionality
operations requiring server authority
When a server-authoritative action cannot be completed, the message should appear in the relevant screen or tab.
 
⸻
 
47. LOADING STATES
Loading states should be designed deliberately.
Avoid blank screens where possible.
Use:
contextual loading indicators
skeleton states
subtle transitions
retained existing content while refreshing
The game should feel responsive even when waiting for server operations.
Loading indicators should be local to the affected screen or action where practical. For example, buying an item should show a transaction loading state in the Shop tab rather than blocking unrelated navigation.
 
⸻
 
48. TOUCH INTERACTION
Touch controls must be the primary interaction model.
Important actions should use sufficiently large touch targets.
The UI should avoid relying on:
hover
tiny icons
precision mouse interactions
right-click
drag-only operations
Actions within each screen or tab should be grouped clearly so that players can identify the relevant controls quickly.
 
⸻
 
49. DESKTOP INTERACTION
Desktop users should receive additional layout space rather than a completely different application.
The same core navigation and interaction model should remain consistent.
Desktop may use:
side panels
multi-column layouts
expanded inspection views
additional simultaneous information
Additional desktop space may allow contextual actions to appear beside the relevant content, but actions must remain associated with their owning screen or tab.
 
⸻
 
50. ACCESSIBILITY
The UI should support:
readable typography
adequate contrast
scalable text where practical
keyboard navigation on desktop
screen-reader-friendly semantic structure
non-colour-only status indicators
clear focus states
accessible touch targets
Screen and tab ownership should be communicated semantically so that assistive technology users can identify the current context and available actions.
 
⸻
 
51. ANIMATION
Animation should be purposeful rather than decorative.
Good uses:
Story Bite transitions
item acquisition
level-up feedback
combat outcomes
major world events
death
important state changes
screen or tab transitions where they clarify context
Avoid excessive animation that slows navigation.
 
⸻
 
52. PERFORMANCE
The UI should remain lightweight.
The game does not require complex 3D rendering.
Performance priorities are:
fast initial load
responsive interactions
efficient network operations
minimal unnecessary rendering
efficient asset loading
good mobile performance
Screen-specific actions should not require loading unrelated systems or global action interfaces.
 
⸻
 
53. INFORMATION ARCHITECTURE
The high-level application structure is:
ACCOUNT
│
├── CHARACTER SELECT
│
└── ACTIVE CHARACTER
     │
     ├── EXPLORE / NAVIGATION
     │    ├── Current Location
     │    ├── Travel
     │    ├── NPC Interaction
     │    ├── Dungeon Navigation
     │    └── Location Actions
     │
     ├── SHOP
     │    ├── Browse Stock
     │    ├── Buy
     │    ├── Sell
     │    └── Compare
     │
     ├── COMBAT
     │    ├── Attack
     │    ├── Abilities
     │    ├── Defend
     │    └── Combat Details
     │
     ├── CHARACTER
     │    ├── Stats
     │    ├── Equipment
     │    └── Skills
     │
     ├── INVENTORY
     │    ├── Inspect
     │    ├── Use
     │    ├── Equip
     │    └── Manage
     │
     └── JOURNAL / QUESTS
          ├── Story Bites
          ├── People
          ├── Places
          ├── Factions
          ├── Lore
          └── Quest Information
The exact navigation labels can be refined during implementation.
The key structural rule is that each system owns its own actions.
 
⸻
 
54. DESIGN CONSISTENCY
The same interaction patterns should be reused throughout the game.
For example:
Select item
    ↓
Inspect
    ↓
Compare / Act
should behave consistently whether the item is encountered in:
inventory
loot
shop
equipment
quest reward
However, the available final action should respect the current screen context. For example:
INVENTORY
Inspect → Equip / Use

SHOP
Inspect → Buy / Compare

LOOT
Inspect → Take / Compare

EQUIPMENT
Inspect → Unequip / Compare
The interaction pattern remains consistent while the owning screen determines the available action.
 
⸻
 
55. DEEP SYSTEMS WITHOUT UI COMPLEXITY
The game should not simplify its underlying systems merely to make the UI simple.
Instead:
DEEP GAME SYSTEM
       ↓
CLEAR DEFAULT PRESENTATION
       ↓
OPTIONAL DETAIL
       ↓
FULL INSPECTION
       ↓
CONTEXT-APPROPRIATE ACTION
This allows the game to retain the depth established in the previous specifications while keeping actions discoverable and properly organised.
 
⸻
 
56. PLAYER FEEDBACK
Meaningful actions should produce immediate feedback within the relevant screen or tab.
Examples:
item equipped
ability activated
quest completed
level increased
loot acquired
Story Bite discovered
world event advanced
item purchased
item sold
destination selected
NPC interaction completed
Feedback should be concise and contextual.
 
⸻
 
57. NARRATIVE IMMERSION
UI elements should reinforce the world rather than constantly reminding the player they are using a web application.
Avoid unnecessary modern-app conventions where they conflict with the fantasy atmosphere.
The goal is:
A game interface that feels like an RPG first and a web application second.
Keeping actions within their relevant screens should support immersion by making each screen feel like a meaningful part of the world:
Explore represents movement and discovery.
NPC screens represent social interaction.
Shop screens represent commerce.
Combat represents immediate danger.
Character screens represent personal development.
The Journal represents memory and knowledge.
 
⸻
 
58. UI STATE VS GAME STATE
The UI must distinguish temporary presentation state from authoritative game state.
Examples of UI-only state:
selected tab
open tooltip
expanded panel
scroll position
current filter
selected item
open inspection view
Examples of persistent game state:
equipment
inventory
quest progress
Journal discovery
character progression
world progression
shop transactions
combat outcomes
travel outcomes
UI state must never accidentally modify authoritative game state.
The active screen or tab is UI state, while the action performed within that screen may modify authoritative game state through the appropriate server-authoritative operation.
 
⸻
 
59. DESIGN INVARIANTS
The interface is mobile-first.
Desktop and tablet are fully supported.
The visual direction is retro-inspired fantasy with modern usability.
The UI uses a persistent RPG-style navigation bar.
Contextual actions change according to the player’s state.
Player actions remain within the relevant screen or tab.
Travel actions belong to the Explore/Navigation or Journey screen.
NPC interaction actions belong to the Explore/Navigation or active NPC screen.
Shop actions belong to the Shop screen or Shop tab.
Combat actions belong to the Combat screen or Combat tab.
Character and equipment actions belong to the Character screen or relevant sub-tab.
Inventory actions belong to the Inventory screen or item-management context.
Journal actions belong to the Journal screen.
The world is primarily navigated through UI/text rather than a map-first system.
Combat is visual-first rather than combat-log-first.
Detailed combat information remains inspectable within the Combat screen.
Story Bites immediately interrupt gameplay with dedicated presentation.
Story Bite dismissal returns the player to the previous relevant screen or tab.
The Journal represents character knowledge.
Character knowledge is not equivalent to world state.
The three protagonists retain independent knowledge.
Character switching occurs through a dedicated character-selection screen.
Information density is deliberately restrained by default.
Advanced information is available through progressive disclosure.
Tooltips and dedicated inspection panels are both supported.
Hidden item quality remains hidden from the player.
Item comparison should clearly communicate practical differences.
Equipped and spare items must remain visually distinguishable.
Death uses a dedicated dramatic screen.
Respawn actions belong to the Death screen.
The death UI must respect the established defeated/respawn flow.
The interface does not require complex graphics.
The interface must work effectively with touch.
Hover cannot be a required interaction.
Desktop layouts may expose more simultaneous information.
Desktop layout changes must preserve screen and tab ownership of actions.
Accessibility is a first-class requirement.
Animation is purposeful and restrained.
UI performance is prioritised.
Loading and connection states are handled gracefully.
The client UI must never be treated as authoritative game state.
Static content and dynamic game state remain architecturally separate.
The interface should preserve the established narrative identity of the world.
The interface should support the three distinct starting regions and their visual identities.
The UI should make a complex RPG approachable without reducing mechanical depth.
The game should feel like an RPG first and a web application second.
Notifications may direct the player to a relevant screen but do not replace that screen’s actions.
Errors should appear in the context where the failed action occurred.
Global navigation should not become a generic container for unrelated player actions.
Each major system should own and present its own actions.
Contextual shortcuts must preserve the ownership and meaning of the underlying action.
The same interaction patterns should be reused while available actions remain context-sensitive.
 
⸻
 
60. DEPENDENCIES
This specification consumes the established:
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
It does not redefine those systems.
 
⸻
 
61. IMPLEMENTATION NOTE
This specification defines what the player should experience, not the frontend framework or implementation technology.
The Technical Architecture Specification will translate these requirements into:
application structure
frontend architecture
component architecture
state management
API interaction
responsive layout strategy
authentication
persistence
deployment
screen and tab ownership
contextual action placement
route and navigation structure
 
⸻
 
END OF SPECIFICATION
