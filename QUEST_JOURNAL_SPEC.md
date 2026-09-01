QUEST & JOURNAL SYSTEM SPECIFICATION
Document: QUEST_AND_JOURNAL_SPEC Version: 0.4 Status: Active Design Purpose: Defines the Journal Story Bite system, authored narrative progression, gameplay triggers, shared world events, and persistent player knowledge.
 
⸻
 
1. DESIGN PHILOSOPHY
There is no standalone Quest system.
All narrative progression is handled through the Journal and its Story Bites.
Gameplay actions, exploration, conversations, discoveries, combat encounters, item acquisition, world events, faction developments, and story milestones can unlock additional Story Bites.
The Journal tells the player:
What has happened, what has been learned, and what remains to be discovered.
The player does not determine the direction or outcome of the Main Story.
The player experiences an authored narrative as it unfolds through the world.
Player story agency is limited to:
when they progress the Main Story
when they investigate or progress Side Stories
which available Side Stories they choose to pursue
which optional discoveries they make
the order in which available narrative content is experienced, where supported
The player cannot alter the central events, outcomes, character arcs, faction resolutions, or final direction of the Main Story.
The Main Story focuses on immediate and human-scale pressures affecting the world:
monsters threatening civilians
economic scarcity
disrupted trade
political intrigue
factional conflict
military and civic responses
relationships between individuals and factions
The ancient civilisation and major catastrophic events are worldbuilding context.
They may appear through optional discoveries, historical references, environmental details, Story Relics, and Side Story Bites, but they do not form the central Main Story conflict.
 
⸻
 
2. STORY BITES
A Story Bite is a short, self-contained piece of narrative information.
Story Bites are the game’s primary unit of narrative delivery.
A Story Bite may describe:
a major story development
a character event
a monster threat
an economic shortage
a political development
a faction conflict
a discovery
a historical clue
a world event
a mystery
a consequence of an authored story event
a new understanding of an existing situation
Story Bites should be concise and focused on one meaningful piece of information.
Example:
A miner has stopped returning from the lower tunnels.
The dwarves have closed the deepest passages.
The settlement is already running short of ore.
 
⸻
 
3. STORY BITE CLASSIFICATION
Every Story Bite is classified as either:
MAIN
SIDE
Main
Main Story Bites advance the protagonist’s authored primary narrative or reveal essential information about the immediate wider conflict.
Main Story Bites focus primarily on:
monsters threatening civilians
economic scarcity
disrupted trade
political intrigue
factional relationships
military, civic, or commercial responses
personal consequences of wider events
Main Story Bites are displayed with gold icons.
Main Story Bites follow a predetermined authored sequence or authored progression structure.
The player may delay Main Story progression, but cannot change its fundamental direction or outcome.
Side
Side Story Bites provide optional character, faction, historical, regional, or world content.
Side Story Bites may explore:
local history
ancient ruins
the lost ancient civilisation
old catastrophes
religious interpretations
regional traditions
optional faction disputes
additional character background
environmental mysteries
Side Story Bites are displayed with grey icons.
Side Stories are authored narrative threads that the player may choose to begin, continue, postpone, or leave incomplete.
The player may choose whether to experience available Side Stories, but cannot alter their authored outcomes.
The classification is fixed by authored content and does not change based on how the player discovers the entry.
 
⸻
 
4. JOURNAL FUNCTION
The Journal is the complete narrative record available to the player.
It allows the player to:
review unlocked Story Bites
revisit earlier discoveries
follow the progression of the Main Story
explore optional Side content
understand the relationship between personal events and wider world events
preserve discoveries made through exploration and gameplay
track how monsters, scarcity, politics, and factions affect the world
retain optional historical and worldbuilding discoveries
see which narrative threads remain undiscovered
The Journal is not a task list and does not contain conventional quest objectives.
The Journal does not present branching choices or alternate narrative outcomes.
 
⸻
 
5. JOURNAL ENTRY STORAGE
Each unlocked Story Bite is stored under the location where it was unlocked.
The location may be:
a settlement
a region
a dungeon
a landmark
a building
a road or route
a battlefield
a mine
a ruin
another authored world location
The Journal interface allows the player to browse entries by location and re-read any unlocked entry.
A Story Bite may reference other locations, but its Journal record belongs to the location where it was unlocked.
 
⸻
 
6. JOURNAL ICON STATES
The Journal displays potential and unlocked entries as icons.
Potential Entry
A Story Bite that exists in the authored content but has not yet been unlocked.
Displayed as:
dimmed icon
no title
no text
no category information
no indication of its subject
Potential entries provide a sense of undiscovered content without revealing information.
Unlocked Main Entry
Displayed as:
gold icon
readable title
readable Story Bite text
available for re-reading
Unlocked Side Entry
Displayed as:
grey icon
readable title
readable Story Bite text
available for re-reading
 
⸻
 
7. BASIC WORLD-BUILDING EXCLUSIONS
Not every interaction creates a Journal entry.
Basic worldbuilding and flavour content should remain lightweight.
The following generally do not create Story Bites:
ordinary greetings
routine shop dialogue
ambient comments
common local information
flavour descriptions
repeated conversations
minor environmental observations
non-significant NPC reactions
ordinary item descriptions
routine travel dialogue
These interactions can still provide atmosphere and context without adding Journal clutter.
Ancient history and catastrophic events should generally remain within this lightweight layer unless they provide a meaningful optional discovery or directly affect the player’s understanding of a current situation.
 
⸻
 
8. STORY BITE UNLOCKING
Story Bites are unlocked by gameplay triggers.
Possible triggers include:
LOCATION_DISCOVERED
LOCATION_VISITED
NPC_INTERACTION
ITEM_ACQUIRED
STORY_RELIC_ACQUIRED
DUNGEON_COMPLETED
COMBAT_ENCOUNTER
WORLD_EVENT_STARTED
WORLD_EVENT_UPDATED
FACTION_STATE_CHANGED
STORY_MILESTONE_REACHED
ENVIRONMENTAL_DISCOVERY
MONSTER_THREAT_REVEALED
SCARCITY_REVEALED
POLITICAL_DEVELOPMENT
TRADE_DISRUPTION
SIDE_STORY_STARTED
SIDE_STORY_PROGRESS_REACHED
The following trigger is not used:
PLAYER_CHOICE
A trigger alone does not guarantee an unlock.
The Story Bite must also satisfy its authored progression conditions.
 
⸻
 
9. PROGRESSIVE UNLOCKING
Story Bites unlock progressively as the authored story advances.
A Story Bite may require:
a previous Story Bite
a story milestone
a world-event state
a location state
a character relationship
a faction state
a protagonist-specific condition
a required discovery
a required item
a previous encounter
a known monster threat
an established scarcity
a political development
a trade or supply disruption
a Main Story progression point
a Side Story progression point
Story Bite conditions determine when authored content becomes available.
They do not create alternate narrative branches.
This prevents later information from appearing before the player has the necessary context.
 
⸻
 
10. STORY BITE PROGRESSION
A narrative situation may unfold through a sequence of Story Bites.
Example:
Something is attacking travellers.
        ↓
Several civilians have disappeared.
        ↓
The attacks are disrupting local trade.
        ↓
The authorities disagree about how to respond.
        ↓
A faction is using the crisis to gain political influence.
        ↓
The protagonist becomes involved in the established response.
Each entry is unlocked separately and stored at the location where the relevant discovery occurred.
The sequence and outcome are authored.
The player may determine when to continue the sequence, but not how the sequence ultimately resolves.
 
⸻
 
11. STORY BITE SOURCES
Story Bites can be unlocked through:
exploration
significant NPC conversations
major character events
discoveries
dungeons
combat encounters
Story Relics
world events
faction activity
settlement changes
major consequences
progression milestones
evidence of monster activity
economic disruption
political developments
faction negotiations
Main Story progression
Side Story progression
Routine interactions should not create entries unless they reveal meaningful narrative information.
 
⸻
 
12. STORY BITE TYPES
Story Bite types are optional metadata used for authoring and filtering.
Suggested types include:
OBSERVATION
RUMOUR
MEMORY
DISCOVERY
HISTORY
CHARACTER
EVENT
MONSTER
SCARCITY
POLITICS
FACTION
MYSTERY
REVELATION
The player does not need to see these metadata labels.
 
⸻
 
13. STORY BITE KNOWLEDGE STATES
Story Bites may represent different levels of understanding.
Conceptually:
RUMOUR
  ↓
SUSPICION
  ↓
OBSERVATION
  ↓
CONFIRMED FACT
  ↓
UNDERSTANDING
These states describe the content of the Story Bite, not separate quest states.
A rumour may later be contradicted, confirmed, or reinterpreted by another Story Bite.
These contradictions are authored narrative developments, not player-created branches.
 
⸻
 
14. STORY BITE UPDATES
Story Bites should normally remain readable as historical records.
When new information deepens an existing subject, the system should generally unlock a new Story Bite rather than silently rewriting the old one.
Example:
Initial Entry:
Ore shipments have stopped.

Later Entry:
Several mountain mines have been closed.

Later Entry:
The mines were closed after repeated attacks
from creatures in the deep tunnels.

Later Entry:
The closure is causing shortages in tools,
weapons, and construction materials.
This preserves the player’s discovery history.
 
⸻
 
15. DUPLICATE INFORMATION
The same underlying fact should not create unnecessary duplicate entries.
Repeated encounters can instead:
unlock a new perspective
add a later Story Bite
confirm an earlier entry
contradict an earlier entry through authored narrative
advance a mystery
provide a protagonist-specific interpretation
reveal a political or economic consequence
The Journal should remain readable and meaningful rather than becoming a transcript of every interaction.
 
⸻
 
16. STORYLINES
There are three principal starting storylines.
Each begins from a different social and geographic perspective.
Forest protagonist
Village
 ↓
Forest
 ↓
Kingdom
 ↓
King's Army
 ↓
Monster threats, military pressure, and political conflict
Coastal protagonist
Street life
 ↓
Merchant household
 ↓
Trade
 ↓
Coastal criminal activity
 ↓
Scarcity, trade disruption, and factional intrigue
Mountain protagonist
Blacksmith apprenticeship
 ↓
Mountain settlement
 ↓
Dwarven city
 ↓
Mining crisis
 ↓
Monster threats, resource scarcity, and factional conflict
These are distinct perspectives on one canonical world.
Each protagonist follows an authored Main Story progression.
 
⸻
 
17. SHARED WORLD
The three storylines do not represent alternate universes.
They occur within the same world and share major events.
A major event may be encountered:
at different times
from different locations
through different information sources
with different personal consequences
through different Main or Side Story Bites
The shared world is primarily connected through:
monster activity
economic scarcity
disrupted trade
political decisions
military responses
factional relationships
civilian consequences
Ancient history and past catastrophes may provide background context but are not the central connective structure of the Main Story.
 
⸻
 
18. SHARED WORLD EVENTS
A World Event is a significant occurrence that exists independently of a particular protagonist.
Examples include:
major monster activity
attacks on civilians
political unrest
trade disruption
shortages of food, ore, tools, or weapons
military mobilisation
factional disputes
criminal activity
border tensions
desert raids
supernatural discoveries
optional historical discoveries
World Events can affect multiple regions, factions, NPCs, and Story Bite unlock conditions.
World Events are authored and progress according to predetermined conditions.
The player may encounter their consequences at different times, but does not determine their fundamental occurrence or resolution.
 
⸻
 
19. WORLD EVENT PROPAGATION
A World Event follows this general chain:
WORLD EVENT
     ↓
World State
     ↓
Affected Regions
     ↓
Affected Factions
     ↓
Affected NPCs
     ↓
Gameplay Consequences
     ↓
Story Bite Unlock
     ↓
Journal Entry
This is the primary mechanism by which the world feels interconnected.
 
⸻
 
20. DIFFERENT PERSPECTIVES
The same event should not necessarily produce the same Story Bite for every protagonist.
For example:
Mountain protagonist
The lower mines have been closed after repeated attacks.
Coastal protagonist
Ore shipments from the mountains have stopped arriving.
Forest protagonist
The army is concerned about shortages of weapons and tools.
The player eventually understands that these entries describe consequences of the same World Event.
The different perspectives change what the player learns and when they learn it, not the underlying event or its authored outcome.
 
⸻
 
21. WORLD EVENT STATES
World Events may use the following progression:
DORMANT
 ↓
EMERGING
 ↓
ACTIVE
 ↓
ESCALATING
 ↓
CRISIS
 ↓
RESOLVED
Not every World Event requires every state.
World Event state can determine which Story Bites are available.
World Event state is not determined by player choice.
It advances through authored progression conditions, time, Main Story milestones, Side Story milestones, or other server-controlled narrative triggers.
 
⸻
 
22. STORY PROGRESSION
The Main Story uses explicit progression milestones.
Conceptually:
STORYLINE
 ├── Chapter
 │    ├── Milestones
 │    ├── Main Story Bites
 │    ├── Side Story Bites
 │    └── World Events
There are no separate quest records.
The authored Story Bite sequence defines the narrative progression.
The player may choose when to advance available Main Story progression, but cannot alter the sequence’s central events or outcomes.
The Main Story progression should focus on:
protecting civilians from monsters
responding to scarcity
navigating political intrigue
observing faction relationships
investigating the causes and consequences of current crises
experiencing established responses to current conflicts
 
⸻
 
23. STORY FLAGS
Story flags provide deterministic progression state.
Examples:
forest_joined_army = true
merchant_household_joined = true
dwarven_city_discovered = true
mountain_threat_revealed = true
desert_raids_known = true
ore_shortage_confirmed = true
civilian_attacks_reported = true
faction_dispute_exposed = true
ancient_ruin_discovered = true
Actual implementation should use stable IDs rather than human-readable text.
Story flags represent authored narrative state.
They do not represent player-created alternate outcomes.
Ancient-history flags should generally support Side Story progression unless a specific discovery has a direct effect on the current Main Story.
 
⸻
 
24. STORY MILESTONES
A Story Milestone represents an important authored narrative change.
Examples include:
joining the army
entering the merchant household
establishing a relationship with the dwarves
discovering a major monster threat
witnessing a major political development
confirming a serious scarcity
exposing a factional conflict
resolving a major civilian crisis
discovering an optional historical clue
Milestones can unlock:
Main Story Bites
Side Story Bites
regions
NPC states
dialogue
world events
additional gameplay triggers
The player can determine when to pursue available milestones, but cannot change their authored result.
 
⸻
 
25. PERSONAL AND WORLD STORY
The narrative has two connected layers.
Personal Story
The protagonist’s individual life and relationships.
World Story
Events affecting the wider world.
The strongest narrative moments occur when these layers intersect.
Example:
Personal:
A blacksmith apprentice must deliver tools.

World:
The mountain mines are becoming increasingly dangerous.

Intersection:
The delivery route exposes the protagonist
to evidence of the monster attacks and the resulting shortage.
The resulting discovery may unlock a Main or Side Story Bite.
The player experiences the protagonist’s personal story but does not redirect its authored arc.
 
⸻
 
26. CHARACTER-DRIVEN PROGRESSION
The protagonist should not feel like a random adventurer inserted into every crisis.
Early Main Story Bites should emerge naturally from the protagonist’s life.
Forest
Local life → military service → civilian protection and military pressure.
Coast
Street survival → merchant life → trade disruption and criminal influence.
Mountains
Craftsmanship → dwarven trade → monster attacks, scarcity, and factional conflict.
These progressions are authored and linear at the narrative level.
The player may delay progression or pursue available Side Stories, but cannot redirect the protagonist into a different central life path.
 
⸻
 
27. WORLD EVENTS BEFORE PLAYER INVOLVEMENT
The player is not necessarily the cause of every major event.
World Events may already be underway before the protagonist becomes involved.
The protagonist gradually discovers their significance through gameplay and Story Bite unlocks.
This makes the world feel larger than the player.
 
⸻
 
28. PLAYER ROLE
The player’s narrative role is to experience the protagonist’s authored progression.
The player may:
explore the world
decide when to continue the Main Story
decide whether to pursue available Side Stories
choose which optional locations to visit
choose which optional discoveries to make
determine the order of available non-critical narrative content
engage with gameplay systems between narrative milestones
The player does not:
choose the protagonist’s central beliefs
choose the protagonist’s major life direction
determine the outcome of the Main Story
determine which major factions ultimately prevail
determine whether canonical World Events occur
create alternate versions of major characters
create alternate endings
branch the central narrative
The player’s role progresses from:
Witness
 ↓
Participant
 ↓
Investigator
 ↓
Agent
 ↓
Major Actor within the authored story
This progression describes the protagonist’s increasing involvement, not increasing control over the narrative outcome.
 
⸻
 
29. JOURNAL MYSTERIES
Important mysteries should unfold through related Story Bites stored at different locations.
Main Story mysteries should primarily concern current threats and conflicts.
Example:
Mystery: The Mountain Attacks

Location A:
Travellers are disappearing on the mountain road.

Location B:
The lower mines have been closed.

Location C:
The attacks are coming from deeper underground.

Location D:
The mine closures are causing shortages across the region.

Location E:
Several factions are using the crisis to advance their own interests.

Later:
The protagonist becomes involved in the established settlement response.
Optional historical mysteries may use a separate structure:
Mystery: The Ancient Civilisation

Location A:
Ancient ruins exist.

Location B:
The ruins contain unusual mechanisms.

Location C:
Their construction predates current kingdoms.

Location D:
Modern magic cannot reproduce some of their effects.

Location E:
Different societies remember them differently.
The second mystery is worldbuilding context and should not define the Main Story progression.
 
⸻
 
30. ANCIENT CIVILISATION
The lost ancient human civilisation is one of the world’s major historical mysteries.
Its remnants appear through:
ancient ruins
artefacts
magical remnants
historical records
unusual mechanisms
Story Relics
NPC interpretations
environmental discoveries
The ancient civilisation is not the central antagonist, cause, or objective of the Main Story.
Its history should be revealed primarily through Side Story Bites and optional exploration.
Ancient discoveries may occasionally intersect with current events, but such intersections should provide context rather than replace the Main Story’s focus on monsters, scarcity, politics, and factions.
 
⸻
 
31. MAJOR CATASTROPHIC EVENTS
Major catastrophic events belong to the world’s historical and cultural background.
They may explain:
abandoned settlements
regional traditions
old political boundaries
religious beliefs
unusual ruins
inherited fears
historical tensions between factions
They are not the central conflict of the Main Story.
References to past catastrophes should generally appear through:
Side Story Bites
historical records
environmental storytelling
NPC memories
optional discoveries
Story Relics
A past catastrophe may influence how factions behave in the present, but the Main Story should remain focused on current threats and current authored developments.
 
⸻
 
32. MAGIC MYSTERY
Modern magic should not immediately explain ancient phenomena.
A wizard may recognise:
“This is magic.”
without understanding:
“This is how the ancient civilisation created it.”
This distinction preserves the mystery of the setting.
Ancient magical phenomena should generally remain optional worldbuilding unless they directly affect a current monster threat, scarcity, political conflict, or factional dispute.
 
⸻
 
33. RELIGIOUS INTERPRETATIONS
Religious NPCs can provide interpretations of unusual events.
A Story Bite may record:
The priest believes the dead are being disturbed.
This should not automatically present the belief as objective truth.
Religious interpretations may be relevant to factional or political conflicts, but they should not automatically define the cause of the Main Story’s problems.
 
⸻
 
34. CONTRADICTORY ACCOUNTS
Different NPCs can provide conflicting interpretations.
Example:
Miner:
"Something is coming from below."

Priest:
"The dead beneath the mountain have awakened."

Wizard:
"The disturbance is magical."

Soldier:
"Whatever it is, it is attacking people."
Only significant contradictions should create Story Bites.
Routine differences in wording or opinion should remain ordinary dialogue.
Contradictions should primarily help the player understand:
what is happening
who is affected
which factions disagree
who benefits from a particular interpretation
what response the world is taking
The player does not choose which interpretation becomes canon.
 
⸻
 
35. PLAYER CHOICES
There are no branching narrative choices.
The player does not choose:
between alternate Main Story outcomes
which major faction wins
whether a canonical character lives or dies
which central political resolution occurs
which version of a World Event becomes true
which ending the story receives
whether the protagonist follows an alternate central path
The player may choose:
when to progress the Main Story
whether to progress an available Side Story
which Side Story to pursue first
whether to explore optional locations
whether to seek optional discoveries
whether to engage with optional historical content
how to approach ordinary gameplay encounters
These choices affect the timing and completeness of the player’s experience, not the authored narrative outcome.
 
⸻
 
36. NARRATIVE STRUCTURE
The game should favour:
authored narrative progression with optional discovery
over:
branching narrative choices
The Story Bite system should support:
a clear Main Story sequence
optional Side Story threads
different perspectives across protagonists
different discovery orders where appropriate
consistent canonical outcomes
persistent narrative knowledge
Side Stories may be skipped, delayed, or completed in different orders where supported, but their authored conclusions do not change.
 
⸻
 
37. CANONICAL STORY
All major events, character arcs, faction outcomes, World Event resolutions, and Main Story conclusions are canonical.
The player may influence:
when they experience them
what optional information they discover beforehand
which Side Stories they complete
which locations they visit
which perspectives they encounter
how much context they have when a Main Story event occurs
The player cannot alter:
the fundamental setting
the central narrative direction
the outcome of the Main Story
the final state of major authored conflicts
the canonical fate of major characters
the resolution of major World Events
The Main Story’s core concerns remain:
monsters threatening civilians
economic scarcity
political intrigue
factional relationships
the consequences of established world events
 
⸻
 
38. EXPLORATION AND STORY BITES
Exploration can unlock Story Bites directly.
Example:
Explore forest
 ↓
Discover abandoned settlement
 ↓
Find evidence of monster attacks
 ↓
Unlock Main Story Bite
 ↓
Journal entry stored at abandoned settlement
 ↓
Additional Story Bite becomes available later
Another example:
Explore ruin
 ↓
Discover ancient mechanism
 ↓
Unlock Side Story Bite
 ↓
Journal entry stored at ruin
 ↓
Optional historical mystery advances
Exploration should be narratively valuable without turning every discovery into a Journal entry.
Exploration may reveal content earlier than the Main Story would otherwise present it, provided the Story Bite’s authored prerequisites are satisfied.
 
⸻
 
39. DUNGEONS AND STORY BITES
Dungeons can provide:
Main Story Bites
Side Story Bites
evidence of monster activity
faction-related discoveries
historical clues
Story Relics
major combat encounters
World Event developments
location-specific discoveries
A dungeon does not need a separate quest record.
Dungeons connected to the Main Story should primarily support current conflicts rather than ancient-history revelations.
Dungeon outcomes are authored.
The player may choose whether and when to enter optional dungeons, but cannot change the canonical result of a Main Story dungeon.
 
⸻
 
40. STORY RELICS
Story Relics are special narrative objects.
Acquiring one can:
unlock a Story Bite
reveal historical information
provide a new perspective
trigger a World Event
connect otherwise separate clues
unlock a later Story Bite
Story Relics associated with ancient civilisation content should generally support Side Story progression.
Story Relics may support Main Story progression when they provide actionable information about:
monster threats
scarcity
political activity
factional plans
current regional conflicts
Story Relics remain subject to the established equipment and defeat rules.
 
⸻
 
41. REWARDS AND STORY PROGRESSION
Narrative progression is represented by Story Bite unlocks rather than quest rewards.
Gameplay rewards may still include:
XP
gold
equipment
items
access
reputation
locations
Story Relics
crafting access
faction standing
political influence
A Story Bite itself is a narrative reward for meaningful discovery or progression.
Narrative rewards do not create alternate story outcomes.
 
⸻
 
42. MULTI-PROTAGONIST JOURNALS
Each protagonist has an individual Journal.
Their Journal reflects their own experiences and discoveries.
For example:
Mountain Journal
→ Mining crisis and monster attacks

Coastal Journal
→ Trade disruption and merchant pressure

Forest Journal
→ Military mobilisation and civilian protection
These entries may eventually reveal that the protagonists are experiencing different consequences of the same World Event.
Each protagonist follows an authored Main Story path.
 
⸻
 
43. SHARED KNOWLEDGE
Some discoveries may become broadly known within the world.
When appropriate, a World Event can make related Story Bites available to multiple protagonists.
Each protagonist should still receive information through their own narrative context and at the appropriate progression point.
Shared knowledge should primarily concern:
major monster threats
severe shortages
political decisions
military actions
trade disruption
factional conflict
Optional historical discoveries should remain protagonist-specific unless they become broadly known through a significant event.
 
⸻
 
44. STORYLINE SYNCHRONISATION
The three storylines do not need to progress at the same pace.
Each protagonist can encounter shared events at different narrative moments.
The underlying World Event remains canonical.
The Journal records only what that protagonist has personally learned or been told through a significant narrative event.
The player may choose when to advance each protagonist’s Main Story, but cannot change the authored sequence or outcome.
 
⸻
 
45. JOURNAL BROWSING
The Journal interface should allow the player to:
browse locations
view potential dimmed entries
open unlocked Main entries
open unlocked Side entries
re-read unlocked Story Bites
distinguish Main and Side content through icon colour
review entries in the context of their unlock location
follow current Main Story developments
revisit optional historical and regional discoveries
identify available or incomplete Side Story content without revealing hidden details
The Journal should not expose hidden titles, subjects, or categories for dimmed entries.
 
⸻
 
46. JOURNAL PRESENTATION
The Journal should feel like:
My record of this world.
It should not feel like:
A database of every conversation.
The interface should prioritise:
location
discovery
progression
readability
re-reading
curiosity
distinction between current conflicts and optional worldbuilding
clarity of Main Story progression
visibility of optional Side Story content
 
⸻
 
47. STORY BITE PACING
Story Bites should appear frequently enough to maintain narrative momentum but not so frequently that the Journal becomes noise.
A Story Bite should do at least one of the following:
reveal meaningful information
change the player’s interpretation
establish an important character detail
introduce a significant current mystery
explain a consequence
connect separate events
reward meaningful exploration
advance the Main Story
deepen optional content
clarify a faction’s position
reveal the effects of scarcity
establish the consequences of monster activity
Ancient history and past catastrophes should not dominate Story Bite pacing.
 
⸻
 
48. CONTENT DATA MODEL
Conceptually:
StoryBite
 ├── id
 ├── classification
 ├── type
 ├── title
 ├── text
 ├── unlock_location
 ├── storyline
 ├── prerequisites
 ├── triggers
 ├── world_event
 ├── story_milestone
 ├── current_story_relevance
 ├── authored_sequence
 └── related_story_bites

WorldEvent
 ├── id
 ├── state
 ├── triggers
 ├── affected_regions
 ├── affected_factions
 ├── affected_npcs
 ├── current_conflict_type
 ├── authored_progression
 └── progression_effects

JournalLocation
 ├── id
 ├── display_name
 └── story_bite_ids
There is no Quest entity in this model.
There is no player-choice branch entity in this model.
 
⸻
 
49. STORY BITE AUTHORING
Story Bites should be authored independently from individual gameplay triggers.
A single Story Bite may have multiple possible unlock triggers.
Example:
StoryBite: ore_shipments_declining

Classification:
MAIN

Unlock Location:
Coastal Merchant House

Authored Sequence:
Mountain Crisis, Stage 2

Possible Triggers:
- speak_to_merchant
- inspect_delayed_shipment
- reach_dwarven_city
- mountain_event_active
Another example:
StoryBite: ancient_mechanism_discovered

Classification:
SIDE

Unlock Location:
Ancient Ruin

Authored Sequence:
Ancient History, Stage 1

Possible Triggers:
- inspect_ruin
- acquire_story_relic
- complete_optional_exploration
This avoids duplicating narrative content.
 
⸻
 
50. POTENTIAL ENTRY AUTHORING
Potential Journal entries must be authored as part of the location’s Journal content even before they are unlocked.
The player can see that an undiscovered entry exists through its dimmed icon, but cannot see:
its title
its text
its classification
its subject
its unlock condition
its narrative outcome
 
⸻
 
51. JOURNAL PRIVACY
Each protagonist’s Journal is personal progression state.
A protagonist does not automatically know what another protagonist has discovered.
This preserves the distinct-perspective narrative.
 
⸻
 
52. REPLAYABILITY
If the player experiences all three protagonists, they should gain a more complete understanding of the shared world.
The three campaigns should provide complementary information.
A player who experiences only one protagonist should still receive a complete and satisfying Main Story.
Experiencing the others should provide:
additional context
alternate perspectives
previously unseen consequences
deeper understanding
additional mysteries
additional Side Story Bites
connections between apparently separate events
different views of monster threats
different views of scarcity and trade
different views of political and factional conflict
The ancient civilisation and past catastrophes may become more understandable across multiple protagonists, but this additional understanding remains optional worldbuilding rather than the central narrative objective.
The three protagonists do not provide alternate endings or player-selected narrative branches.
 
⸻
 
53. THREE-PERSPECTIVE NARRATIVE MODEL
The overall structure is:
                  SHARED WORLD
                       │
        ┌──────────────┼──────────────┐
        │              │              │
     FOREST          COAST         MOUNTAINS
        │              │              │
     Army          Merchant        Dwarves
        │              │              │
        └──────────────┼──────────────┘
                       │
          Monsters, Scarcity, Politics,
             Trade, and Faction Conflict
                       │
                Local Consequences
                       │
                Shared World Events
                       │
              Optional Historical Context
The player’s understanding grows vertically through their own Story Bites and horizontally through the wider world.
The narrative outcome remains authored across all three perspectives.
 
⸻
 
54. STORY PACING
The narrative should alternate between:
Personal
 ↓
Local
 ↓
Current threat or conflict
 ↓
Wider implication
 ↓
Personal consequence
 ↓
Factional or political response
This prevents the story from becoming a sequence of disconnected global crises.
Optional historical discoveries can interrupt this structure as Side content, but should not displace the Main Story’s focus.
 
⸻
 
55. PERSISTENCE
The server stores:
unlocked Story Bites
Story Bite unlock locations
Main and Side classifications
Journal location state
story milestones
story flags
World Event state
discovered locations
Side Story progression
protagonist-specific progression
The server does not store branching narrative choices because the narrative does not branch.
Unlocked entries remain available for re-reading across sessions.
 
⸻
 
56. SERVER AUTHORITY
The server is authoritative over all progression-critical narrative state.
The client cannot independently decide that:
a Story Bite is unlocked
a Journal entry is available
a Main Story milestone has been reached
a Side Story Bite has been discovered
a region is unlocked
a World Event has advanced
a story flag has changed
a Side Story has progressed
a canonical narrative event has resolved
The server validates gameplay triggers and authored progression conditions.
 
⸻
 
57. DESIGN INVARIANTS
There is no standalone Quest system.
All narrative progression is handled through the Journal and Story Bites.
Gameplay triggers unlock Story Bites.
Story Bites unlock progressively as the authored story advances.
Every Story Bite is classified as Main or Side.
Main Story Bites use gold icons.
Side Story Bites use grey icons.
Potential entries use dimmed icons.
Potential entries reveal no information.
Unlocked entries can be opened and re-read.
Journal entries are stored by unlock location.
The Journal is browsed through its interface.
Basic worldbuilding and flavour interactions do not create Story Bites.
Routine dialogue does not create Journal entries.
Story Bites are concise.
Story Bites are the primary narrative delivery mechanism.
The Journal represents what the protagonist has learned.
The Journal does not reveal undiscovered information.
The three protagonists have distinct narrative perspectives.
The three protagonists inhabit the same canonical world.
Major World Events can affect all three storylines.
The same event can produce different Story Bites for different protagonists.
NPCs only provide information appropriate to their knowledge.
Rumours may be incorrect.
The player gradually discovers the truth.
The Main Story focuses on monsters threatening civilians, economic scarcity, political intrigue, and factional relationships.
The ancient civilisation is worldbuilding context rather than the central Main Story conflict.
Major catastrophic events are worldbuilding context rather than the central Main Story conflict.
Ancient ruins provide optional historical clues.
Modern magic does not automatically explain ancient magic.
Powerful magical practitioners are rare.
Religious interpretations are not automatically objective truth.
Story Bites can be Main or Side regardless of whether they are discovered through exploration, NPCs, combat, items, or World Events.
Duplicate information should not create unnecessary duplicate entries.
New understanding should generally be represented by additional Story Bites.
Each protagonist has an individual Journal.
Journals should not reveal another protagonist’s discoveries.
Shared World Events remain canonical across protagonists.
World Events can change NPCs, factions, locations, gameplay, and Story Bite availability.
The player experiences the protagonist’s authored progression.
Personal stories remain connected to wider World Events.
The narrative favours authored progression over branching narrative choices.
The player may delay Main Story progression.
The player may choose whether to pursue available Side Stories.
The player cannot alter the central Main Story direction or outcome.
Side Stories have authored outcomes.
The player should understand the Main Story without completing every Side Story Bite.
Experiencing multiple protagonists provides additional perspective rather than alternate endings.
Story progression is persistent.
Journal progression is persistent.
Story Bite unlocks are server-authoritative.
World Event progression is server-authoritative.
Narrative content is data-driven.
Story content should not be hard-coded into UI components.
Story Bites should be independently authorable and reusable.
The Journal should remain useful after hundreds of hours of progression.
The narrative system must support the established world rather than impose a generic fantasy structure.
 
⸻
 
58. DEPENDENCIES
Depends on
World & Exploration
NPC & Faction
Character
Journey & Dungeon
Combat
Equipment & Loot
Persistence
Used by
World Events
NPCs
Factions
Exploration
Dungeons
Combat encounters
Story Relics
Journal
UI
Character progression
Save and persistence systems
 
⸻
 
59. OPEN CONTENT WORK
The following should be developed as narrative and content documents rather than hard-coded into this system specification:
Full three-protagonist story outline
Chapter structure
Main Story Bite sequences
Side Story Bite sequences
Story Bite unlock locations
Full World Event timeline
Monster threat progression
Economic scarcity progression
Political intrigue progression
Faction relationship progression
Civilian consequence progression
Optional ancient civilisation discovery sequence
Optional historical catastrophe content
Individual faction storylines
Individual NPC dialogue
Major character arcs
Story Relic narrative content
Main Story progression timing
Side Story availability and ordering rules
Canonical Main Story outcomes
Canonical Side Story outcomes
Main antagonist progression
Final narrative resolution
 
⸻
 
END OF SPECIFICATION
