NPC & FACTION SYSTEM SPECIFICATION
Document: NPC_AND_FACTION_SPEC Version: 0.1 Status: Active Design Purpose: Defines NPCs, societies, factions, political relationships, social structures, static dialogue, Journal relevance, and their integration with the established world, narrative, exploration, and progression systems.
 
⸻
 
1. DESIGN PHILOSOPHY
NPCs and factions exist to make the world feel inhabited.
They are not primarily:
quest dispensers
combat-stat containers
vendors with interchangeable dialogue
alignment labels
exposition machines
They are members of societies with their own:
interests
relationships
beliefs
fears
economic pressures
political concerns
knowledge
loyalties
conflicts
The player should gradually understand the world by interacting with these people.
NPCs and factions are static by default. Their identities, locations, relationships, behaviour, and dialogue do not change during ordinary gameplay.
Most NPC interactions are flavour and worldbuilding. They do not create quests, update the Journal, alter progression, or produce other persistent effects unless the interaction is explicitly connected to a main story or side story.
The only permitted additions are explicitly authored main-story or side-story dialogue values, story-specific dialogue entries, and story-specific Journal updates. These additions do not replace the NPC’s established identity or create general-purpose dynamic behaviour.
 
⸻
 
2. STATIC NPC AND FACTION MODEL
The world and its NPCs are authored as fixed content.
Unless explicitly defined as part of a main story or side story:
NPCs do not change allegiance.
NPCs do not change occupation.
NPCs do not change location.
NPCs do not die.
NPCs do not disappear.
NPCs do not gain or lose relationships.
Factions do not dynamically reorganise.
Faction relationships do not change.
Dialogue does not react to ordinary player actions.
Dialogue does not react to optional quests unless those quests are authored side stories.
Dialogue does not react to reputation.
Dialogue does not react to world-state simulation.
Journal entries are not created for ordinary flavour interactions.
Points of interest do not automatically create Journal entries.
The player may discover additional information about an NPC or faction, but the underlying NPC or faction remains unchanged.
 
⸻
 
3. STORY-SPECIFIC DIALOGUE AND JOURNAL ADDITIONS
Main stories and side stories may provide additional dialogue values for existing NPCs.
These additions may be triggered by explicitly authored story conditions such as:
reaching a story milestone
completing a required story objective
discovering a major story fact
entering a required story location
beginning a story chapter
completing a side-story objective
discovering a side-story location or event
Story-specific dialogue additions are additive.
They may:
provide new information
acknowledge a story event
reveal a new perspective
direct the player toward a story objective
clarify an existing relationship
record a new Journal entry
provide context for a main story or side story
They must not:
kill or remove the NPC
permanently relocate the NPC
rewrite the NPC’s identity
create unrestricted dynamic dialogue
cause the NPC to react to unrelated optional actions
create a general faction simulation system
create Journal entries for unrelated flavour content
Conceptually:
Static NPC Dialogue
        +
Story-Specific Dialogue Values
        ↓
Available Dialogue
Only dialogue that communicates information relevant to a main story or side story may update the Journal.
 
⸻
 
4. LOW-MAGIC SOCIAL MODEL
The setting is fundamentally a grounded fantasy world.
Magic is not an everyday utility.
Most ordinary people do not routinely encounter powerful magic.
This has important consequences for NPC behaviour.
A farmer, merchant, soldier, or craftsman should generally react to supernatural events as unusual or significant rather than treating them as mundane.
NPCs should not casually possess magical knowledge simply because magic exists somewhere in the world.
 
⸻
 
5. MAGIC IN SOCIETY
The ancient world possessed magical capabilities far beyond those of the present.
That knowledge has largely been lost.
The present world therefore contains:
very limited common magical knowledge
rare powerful practitioners
fragments of ancient knowledge
supernatural remnants
misunderstood ancient artefacts
NPCs should not casually possess knowledge that belongs to the lost civilisation.
 
⸻
 
6. WIZARDS AND WITCHES
Powerful wizards and witches exist.
They are generally:
rare
reclusive
suspicious of strangers
independent from ordinary society
They should feel exceptional.
A wizard encountered by the player should therefore be a meaningful character rather than simply another shopkeeper.
Their knowledge can be substantially greater than that of ordinary NPCs, but even powerful modern practitioners need not understand the full truth of the ancient civilisation.
Their dialogue remains static unless additional dialogue is explicitly authored as part of a main story or side story.
 
⸻
 
7. RELIGION AS BACKGROUND WORLDbuilding
Religion exists throughout the world, but it is primarily background culture and worldbuilding rather than a major gameplay system.
Different cultures generally worship different groups of gods.
There is no universally dominant pantheon across the world.
Religious traditions therefore developed independently among the descendants of the ancient civilisation.
Religion may influence:
local customs
names
festivals
burial practices
architecture
sayings
personal beliefs
interpretations of unusual events
These details should help distinguish cultures without making religion a central system of progression, faction simulation, or routine quest delivery.
Religious content should generally remain incidental unless it is explicitly used in a small side story or, more rarely, a main-story event.
 
⸻
 
8. THE GODS
The gods are objectively real.
Each god has a distinct, mutually exclusive domain of influence.
A god’s domain is an absolute metaphysical boundary. Gods cannot freely act outside their domains, and no god possesses unlimited authority over every aspect of existence.
The gods are not ordinary NPCs, political rulers, or reliable sources of public instruction.
They regard humanity as interesting and entertaining distractions rather than subjects they actively govern.
Their long-term objectives are largely incomprehensible to mortals.
Their personalities and motivations tend to follow their domains.
A god may favour or influence mortals, but generally does not intervene unless doing so relates to its domain.
Divine actions may therefore be:
beneficial
harmful
indifferent
unsettling
contradictory
bizarre from a human perspective
depending on the god’s nature and domain.
For example:
The god of Agriculture genuinely wants crops and farmland to prosper.
The god of Death is not malicious. Death is simply part of its domain, and it patiently waits for each person’s appointed time.
A god’s domain remains an absolute metaphysical boundary even when mortals misunderstand the god’s actions.
 
⸻
 
9. DIVINE INTERVENTION
Gods rarely intervene directly in the mortal world.
A god can manifest physically, but doing so is exceptionally rare.
Devout lifelong servants may occasionally receive whispered answers to prayer.
Divine communication is therefore:
rare
ambiguous
difficult to verify
precious
open to interpretation
A whispered answer does not necessarily provide a complete explanation or clear instruction.
A mortal may misunderstand:
what god answered
what the answer referred to
whether the answer was literal
whether the answer was complete
what action the god expected
The gods’ intervention in the Ascension was an extraordinary event rather than normal divine behaviour.
It should be treated as a major historical and metaphysical exception, not as evidence that the gods routinely govern mortal affairs.
 
⸻
 
10. GODS ARE NOT AN EVERYDAY GAME SYSTEM
The world should not behave as though every major decision has an obvious divine answer.
NPCs can:
worship
doubt
pray
interpret events religiously
follow different traditions
disagree about the gods
preserve local customs
occasionally receive genuine divine communication
without the gods functioning as omnipresent quest-givers.
The gods do not provide routine objectives, constant dialogue, universal moral judgements, or guaranteed explanations.
The game should not include a general system in which ordinary player actions automatically gain divine approval, divine punishment, or religious consequences.
Direct divine appearances, communications, miracles, or interventions must be explicitly authored as part of a main story or side story.
Religion should not become a routine source of progression, combat abilities, faction reputation, or daily objectives.
 
⸻
 
11. PRIESTS
Priests are uncommon and primarily serve as background or worldbuilding NPCs.
A priest may be:
a local caretaker
a ritual specialist
a keeper of burial customs
a community adviser
a teacher of local tradition
an interpreter of unusual events
Most priests do not possess supernatural power.
A priest’s title does not guarantee divine favour, special knowledge, or objective correctness.
Powerful priests may exist, but they are rare and exceptional. Their presence should be reserved for explicitly authored story content, most likely a small side story.
Even a powerful priest is not omniscient and may not understand the gods’ motives or the full meaning of a divine event.
 
⸻
 
12. RELIGIOUS CONTENT SCOPE
Religious content should generally be limited to:
background dialogue
cultural details
local customs
burial practices
shrine or temple decoration
names and sayings
occasional references to gods
rare, explicitly authored side-story material
Religion should not normally provide:
a universal player faith system
routine divine quests
automatic divine approval or punishment
a broad priest class system
a dynamic religious faction simulation
regular supernatural communication
a universal pantheon
a general-purpose miracle system
A small side story may involve:
a sacred site
a disputed religious tradition
a rare answer to prayer
a priest protecting a community
an unusual divine event
a misunderstanding of a god’s domain
Such content must remain explicitly authored and self-contained.
 
⸻
 
13. RELIGIOUS INTERPRETATION
Different cultures may interpret the same god, event, or domain differently.
Religious traditions may contain:
genuine historical memories
partial truths
symbolic language
cultural adaptation
misunderstanding
deliberate invention
A priest may sincerely interpret an event incorrectly.
A local tradition may preserve a distorted memory of the Ascension.
A genuine divine event may still be misunderstood by the people who witness it.
The objective truth of a divine or supernatural event is determined by authored world and story content, not by the confidence of an NPC.
 
⸻
 
14. RELIGION AND ANCIENT KNOWLEDGE
The lost human civilisation complicates religious interpretation.
Ancient ruins, artefacts, and supernatural remnants may be interpreted as:
sacred sites
divine relics
evidence of an earlier age
forbidden objects
magical machines
signs of divine punishment
remnants of a civilisation later mistaken for gods
The ancient civilisation possessed magical capabilities far beyond those of the present.
Modern cultures may preserve distorted memories of that civilisation without understanding its true nature.
The existence of ancient magic does not automatically disprove religious belief, nor does religious interpretation automatically explain ancient magic.
The relationship between the ancient civilisation, the gods, and the Ascension remains part of the deeper mystery of the setting.
 
⸻
 
15. RELIGION AND SUPERNATURAL EVENTS
Supernatural events may produce different interpretations among different NPCs.
For example:
Farmer
 → "A curse."

Soldier
 → "An unexplained threat."

Priest
 → "A sign, warning, or test."

Wizard
 → "An unusual magical phenomenon."

Scholar
 → "Evidence requiring investigation."

Player
 → Gradually discovers what the event actually is.
No interpretation is automatically correct merely because it comes from a priest or wizard.
The player should be able to encounter uncertainty without the game treating every interpretation as equally valid.
Religious interpretations should remain flavour unless the event is explicitly connected to a main story or side story.
 
⸻
 
16. RELIGION AND HAUNTED BATTLEFIELDS
Different societies may interpret haunted battlefields differently.
Examples of perspectives include:
soldiers remembering fallen comrades
locals fearing ghosts
priests describing the site through local burial traditions
treasure hunters seeking lost equipment
scholars investigating historical events
wizards examining magical remnants
A priest may describe a battlefield using spiritual or cultural language without knowing whether the cause is divine, magical, historical, or something else.
A haunted battlefield updates the Journal only when its information is relevant to a main story or side story.
 
⸻
 
17. RELIGION AND ANCIENT RUINS
Ancient ruins may be interpreted differently by local communities.
Religious NPCs may:
avoid them
maintain local customs around them
regard them as sacred
regard them as dangerous
preserve stories associated with them
misunderstand their original purpose
A priest may recognise that a ruin is culturally significant without knowing whether it was built by worshippers, ancient magicians, or a civilisation later mistaken for gods.
A point of interest does not create a Journal entry merely because the player visits it or hears a religious NPC mention it.
A Journal entry requires a connection to a main story or side story.
 
⸻
 
18. RELIGIOUS FACTIONS
Religious factions are not a major category of active faction gameplay.
They may exist as authored background elements such as:
local temples
shrine communities
burial societies
priestly households
monastic communities
religious schools
charitable institutions
They should generally function as static worldbuilding rather than autonomous political organisations.
A religious group may be relevant to a small side story, but it should not normally receive a full faction progression system, dynamic relationship model, or independent simulation.
 
⸻
 
19. RELIGIOUS QUESTS
Religious NPCs may appear in quests, but religious quests should be uncommon and limited in scope.
A small side story may involve:
protecting a shrine
recovering a religious object
investigating an unusual event
helping a priest protect a community
resolving a dispute over local tradition
discovering the history of a sacred site
witnessing a rare and ambiguous answer to prayer
A religious quest does not prove that the associated religious interpretation is correct.
The quest may reveal information, create uncertainty, or expose contradictions between belief and reality.
Religious quests are authored content.
Completing an optional religious quest does not change the priest’s identity, location, relationships, dialogue, or survival status unless the quest is explicitly authored as a side story.
A religious quest updates the Journal only if it is designated as part of a main story or side story.
 
⸻
 
20. RELIGION AND THE PLAYER
The player is not required to adopt a religion in order to interact with religious NPCs or receive religious information.
The player may:
listen
doubt
respect
reject
investigate
compare interpretations
remain uncertain
The game should not require a universal player faith system unless a separate specification explicitly defines one.
Ordinary player attitudes toward religion do not automatically alter NPC relationships, faction relationships, divine favour, or Journal content.
Any such consequence must be explicitly authored as part of a main story or side story.
 
⸻
 
21. RELIGIOUS RUMOURS AND OMENS
Religious rumours and omens are not necessarily facts.
An NPC may report:
a prayer that appeared to be answered
a vision
a miracle
a curse
a prophecy
a sacred sign
a story passed down through generations
a supernatural event interpreted through local tradition
The player should not automatically know whether the report is:
true
false
symbolic
misunderstood
deliberately fabricated
genuinely supernatural but incorrectly interpreted
The Journal should distinguish discovered information from objective truth where appropriate.
A religious rumour or omen updates the Journal only when it is relevant to a main story or side story.
Ordinary religious rumours remain dialogue and worldbuilding only.
 
⸻
 
22. RELIGION AND THE JOURNAL
Religious dialogue may update the Journal only when it communicates information relevant to a main story or side story.
The Journal should record what the player has discovered, not automatically validate a religious interpretation.
For example, a Journal entry may record:
A priest claims that the ruined site is sacred and that strange events have occurred there.
It should not automatically record:
The gods have declared the site sacred.
unless the story has explicitly established that fact.
The Journal may preserve uncertainty through wording such as:
“The priest believes…”
“According to local tradition…”
“The player witnessed…”
“The event may be connected to…”
“The source remains unclear…”
 
⸻
 
23. HUMAN KINGDOM
The human kingdom forms one of the major political structures of the setting.
The king is broadly regarded as wise and retains significant support.
However, the kingdom is under pressure.
Problems include:
noble intrigue
civil unrest
crime
banditry
monster threats
external threats
disrupted trade
The kingdom should therefore feel functional but strained.
 
⸻
 
24. THE KING
The king is an important political NPC.
He should not be portrayed as an incompetent ruler simply because the kingdom has problems.
His position should instead demonstrate the difficulty of governing a world experiencing simultaneous crises.
The king’s support among the population provides an important counterweight to noble intrigue.
 
⸻
 
25. NOBILITY
Nobles have their own interests and political ambitions.
They can disagree with the king without necessarily being universally evil.
Noble intrigue may involve:
influence
wealth
succession
local power
military interests
trade
alliances
rivalry
The political system should support competing motivations rather than simple good-versus-evil faction labels.
 
⸻
 
26. KING’S ARMY
The King’s Army is an important institution.
It represents:
royal authority
organised military power
defence
law enforcement
responses to external threats
The forest protagonist eventually joins the army.
This provides that storyline with direct access to:
soldiers
officers
military missions
political information
reports from other regions
the kingdom’s response to emerging threats
 
⸻
 
27. FOREST PROTAGONIST’S SOCIAL NETWORK
The forest protagonist begins as a young person from a small farming settlement.
Their social perspective therefore initially comes from:
farmers
families
local workers
hunters
travellers
nearby soldiers
Joining the King’s Army expands their social world dramatically.
The narrative progression should therefore naturally move from:
Village
 ↓
Local region
 ↓
Army
 ↓
Kingdom
 ↓
Wider world
 
⸻
 
28. COASTAL TRADING SOCIETY
The coastal protagonist begins in a trading town.
This society is shaped heavily by commerce.
Important groups include:
merchants
sailors
traders
labourers
craftsmen
travellers
criminals
smugglers
pirates
Economic disruption should therefore be visible to ordinary NPCs.
 
⸻
 
29. COASTAL PROTAGONIST
The coastal protagonist begins as an orphan and street rat.
Their social position is initially low.
They survive through the informal economy of the town.
After saving a merchant from bandits, they enter the merchant’s household.
This changes their access to society.
Their progression therefore moves from:
Street life
 ↓
Merchant household
 ↓
Trade network
 ↓
Wider commercial world
 ↓
Political/economic crisis
 
⸻
 
30. MERCHANTS
Merchants respond primarily to:
supply
demand
safety
routes
prices
information
political stability
They should be among the first groups to notice large-scale disruption elsewhere.
For example, reduced mountain ore production can eventually affect coastal merchants even if those merchants have never visited the mountains.
 
⸻
 
31. PIRATES
Pirates are a distinct criminal/maritime threat.
They are not simply generic hostile enemies.
Their existence is connected to the changing trade environment.
As legitimate trade routes become longer and more dangerous, piracy becomes increasingly consequential.
Pirates can therefore be involved in:
attacks
intimidation
stolen cargo
coastal rumours
criminal networks
political complications
 
⸻
 
32. SMUGGLERS
Smugglers operate between legitimate commerce and organised crime.
They may move:
restricted goods
stolen goods
scarce resources
information
people
Their relationships with merchants, pirates, and authorities should vary.
Not every smuggler needs to be malicious.
 
⸻
 
33. BANDITS
Banditry is a significant problem within the kingdom.
Bandits can emerge from:
lawlessness
poverty
political instability
opportunism
organised criminal networks
Bandits should therefore exist as a social phenomenon rather than merely being an enemy type.
The coastal protagonist’s first major event involves saving a merchant from bandits.
 
⸻
 
34. DWARVEN SOCIETY
Dwarves are an established civilisation within the mountain regions.
They possess important expertise in:
mining
metalworking
tools
ore
underground construction
Their cities are economically important to neighbouring human settlements.
 
⸻
 
35. HUMAN–DWARF RELATIONSHIP
The relationship between humans and dwarves includes practical economic interdependence.
The mountain protagonist regularly:
delivers tools to the nearby dwarven city
returns with ore
This provides an early demonstration that the societies are connected through trade.
The relationship should not be reduced to a generic fantasy “dwarves like mining” trope.
Their economic relationship matters directly to the wider world.
 
⸻
 
36. MOUNTAIN PROTAGONIST
The mountain protagonist begins as a blacksmith apprentice.
Their social network initially consists primarily of:
fellow craftsmen
family/community
miners
traders
dwarves
travellers through the mountain settlement
Their growing exposure to the dwarven city gives them an unusually early understanding of the mountain economy.
 
⸻
 
37. THE DEEP-MOUNTAIN THREAT
Monsters are emerging from the deep mountains.
This is a major threat to dwarven society.
The consequences include:
mining disruption
dangerous routes
reduced ore production
threats to dwarven settlements
threats to human settlements
trade disruption
Dwarven NPCs should therefore possess knowledge about the threat that ordinary distant humans may not have.
 
⸻
 
38. DIFFERENT INFORMATION NETWORKS
Each society receives different information.
For example:
Farmers
 → local attacks
 → rumours
 → refugees

Army
 → reports
 → military intelligence
 → strategic threats

Merchants
 → prices
 → shortages
 → route disruption

Dwarves
 → mining
 → underground activity
 → mountain threats

Pirates
 → shipping
 → coastal activity
 → smuggling

Priests
 → local traditions
 → burial customs
 → occasional interpretations of unusual events

Wizards
 → magical phenomena
 → ancient knowledge
No single faction should automatically know everything.
 
⸻
 
39. SHARED WORLD EVENTS
Major events exist independently of individual NPCs.
A world event can affect several factions differently.
Example:
Deep-Mountain Monster Activity
            │
     ┌──────┼──────┐
     ↓      ↓      ↓
 Dwarves  Merchants  Army
     │      │        │
 Mining   Trade     Defence
 crisis   crisis    response
This creates the same-world/different-perspective structure established by the narrative design.
 
⸻
 
40. FACTION KNOWLEDGE
Each faction can have its own knowledge state.
Conceptually:
Faction Knowledge
 ├── Known Events
 ├── Suspected Events
 ├── Rumours
 ├── Confirmed Information
 ├── False Beliefs
 └── Secret Information
This allows NPCs to disagree without breaking narrative consistency.
 
⸻
 
41. RUMOURS
Rumours are not necessarily facts.
An NPC may report:
something they personally witnessed
something another person told them
a distorted version of an event
a genuine clue
a completely incorrect interpretation
The Journal should distinguish discovered information from objective truth where appropriate.
 
⸻
 
42. NPC KNOWLEDGE LIMITS
NPCs should generally know things appropriate to:
their location
occupation
faction
social position
experience
education
story progression
A farmer should not casually explain the details of ancient portal technology.
A dwarven miner may know considerably more about underground disturbances.
A powerful wizard may recognise magical phenomena that ordinary people cannot.
A priest may know local religious traditions without knowing the gods’ motives or the objective cause of a supernatural event.
 
⸻
 
43. NPC PERSONALITY
Important NPCs should have distinct personalities.
Personality affects:
how they communicate
what they value
what they fear
how trustworthy they are
what information they reveal
how they react to the player
However, personality should support the authored narrative rather than create an enormous branching dialogue tree.
 
⸻
 
44. NPC DIALOGUE
Dialogue is concise and purposeful.
NPCs should communicate through:
short conversations
observations
rumours
instructions
reactions
journal-triggering discoveries
The game should avoid excessive dialogue walls.
Religious dialogue should generally remain brief background flavour unless it belongs to an explicitly authored side story or main-story event.
 
⸻
 
45. NPCS AS STORY DELIVERY
NPCs are one of several ways the player receives story information.
The information pipeline is:
NPC
 ↓
Conversation / Observation
 ↓
Story Bite
 ↓
Journal
The Journal remains the persistent record.
 
⸻
 
46. NPCS AS WORLD STATE INDICATORS
NPC dialogue should reflect authored world conditions.
If a settlement is suffering from shortages:
merchants should notice
prices may change
workers may complain
travellers may discuss it
If a route becomes dangerous:
travellers should know
guards may react
merchants may alter plans
This prevents the world from feeling static.
Religious NPCs may mention local customs or unusual events, but their dialogue should not imply a dynamic religious simulation.
 
⸻
 
47. FACTIONS
A faction is an organised group with shared interests.
A faction can represent:
political authority
military organisation
economic interests
criminal networks
cultural groups
adventuring organisations
religious institutions where relevant to authored background or story content
A faction does not necessarily need to be hostile or friendly to the player.
 
⸻
 
48. FACTION RELATIONSHIPS
Factions can have relationships such as:
allied
friendly
neutral
suspicious
hostile
actively opposed
These relationships are world-state data.
They should not be treated as a simple morality scale.
A merchant guild may cooperate with criminals in one situation and report them in another.
A noble may oppose the king politically while still defending the kingdom.
A pirate may assist a merchant for personal reasons.
Religious groups may have different traditions without being active political rivals.
 
⸻
 
49. FACTION MOTIVATIONS
Each significant faction should have:
goals
resources
territory/influence
allies
rivals
internal problems
information
limitations
This allows faction behaviour to emerge from their interests.
Religious groups are an exception in scope: unless explicitly used by a main story or side story, they remain background authored content rather than active simulated factions.
 
⸻
 
50. NO UNIVERSAL ALIGNMENT SYSTEM
The game should not require every faction to be assigned:
Good / Neutral / Evil
Political and social relationships are more useful than a simplistic alignment score.
A merchant guild may cooperate with criminals in one situation and report them in another.
A noble may oppose the king politically while still defending the kingdom.
A pirate may assist a merchant for personal reasons.
A religious group may perform beneficial, harmful, or strange actions depending on its beliefs and local traditions without being reduced to a moral alignment.
 
⸻
 
51. DESERT TRIBES
The desert contains multiple tribes.
A major current development is that these tribes have become unusually united.
This is significant precisely because such unity is not normal.
The united tribes are conducting raids against distant settlements.
Their actions therefore constitute a major geopolitical problem.
 
⸻
 
52. DESERT TRIBAL STRUCTURE
The tribes should not be treated as a single culturally homogeneous NPC group.
The larger united movement can contain:
individual tribes
tribal leaders
competing interests
alliances
internal disagreements
Their unusual unity itself can become a narrative question.
 
⸻
 
53. ADVENTURER GUILD
The Adventurer Guild provides a social structure for professional adventuring.
It can connect the player to:
jobs
exploration
dungeons
monster hunting
information
other adventurers
The guild should provide a grounded explanation for why adventurers exist as an organised profession.
 
⸻
 
54. TRADE GUILDS
Trade guilds represent organised commercial interests.
They can involve:
merchants
craftsmen
carriers
traders
suppliers
They become particularly important when trade routes are disrupted.
The player’s coastal storyline has a natural connection to this social layer.
 
⸻
 
55. CRAFTSMEN
Craftsmen are important to the functioning of settlements.
Examples include:
blacksmiths
toolmakers
miners
other skilled trades
The mountain protagonist’s blacksmith apprenticeship provides a direct connection to this social class.
Craftsmanship should feel economically important rather than merely being a crafting-game mechanic.
 
⸻
 
56. ANCIENT KNOWLEDGE
The lost human civilisation is a special case.
Modern societies possess fragments of its remains but do not collectively understand them.
Different NPCs may interpret ancient artefacts differently.
For example:
Farmer
 → "Old ruins."

Merchant
 → "Something valuable."

Priest
 → "A place with local or spiritual significance."

Scholar
 → "Evidence of an ancient civilisation."

Wizard
 → "A remnant of powerful magic."

Player
 → Gradually discovers the truth.
This supports the mystery-driven narrative.
 
⸻
 
57. NPCS AND ANCIENT RUINS
Ancient ruins should therefore generate uncertainty.
NPCs may:
avoid them
loot them
study them
preserve traditions about them
misunderstand them
fear them
This produces different social reactions to the same physical location.
 
⸻
 
58. HAUNTED BATTLEFIELDS
Different societies may interpret haunted battlefields differently.
Examples of perspectives include:
soldiers remembering fallen comrades
locals fearing ghosts
priests applying local burial traditions
treasure hunters seeking lost equipment
scholars investigating historical events
The player can encounter these perspectives through NPCs and Journal discoveries.
 
⸻
 
59. NPC QUESTS
NPCs may give the player quests.
However, quests should arise naturally from:
personal problems
faction objectives
local events
economic needs
world events
story progression
They should not exist solely to produce rewards.
Religious NPCs should only provide quests when the content is explicitly authored, and such quests should generally be small side stories or rare main-story material.
 
⸻
 
60. FACTION QUESTS
Faction quests represent the interests of an organisation.
They may affect:
reputation
access
information
rewards
future interactions
Faction quests can be optional unless explicitly designated as main-story content.
Religious factions should not normally receive faction questlines unless explicitly authored as side-story content.
 
⸻
 
61. STORY FACTIONS
Some factions are directly involved in the main story.
Story factions should be controlled by the narrative system.
Their state can change as major events occur.
Examples of state changes:
Neutral
 ↓
Concerned
 ↓
Mobilised
 ↓
Under Pressure
 ↓
Crisis
 ↓
Resolution
Religious groups should only enter this structure when explicitly required by a main story or side story.
 
⸻
 
62. THREE STORYLINES AND FACTION ACCESS
The three protagonists begin with different social access.
Forest
Early access:
farming community
local settlement
King’s Army
kingdom institutions
Coast
Early access:
street community
merchant household
coastal traders
criminal networks
Mountains
Early access:
craftsmen
miners
human settlement
dwarven society
This difference is an important part of the narrative design.
 
⸻
 
63. CROSS-STORY INFORMATION
A faction can reference events that originate outside the player’s starting region.
The player may hear:
“The dwarves are having trouble getting ore out.”
before understanding why.
Later, exploration of the mountains reveals the actual cause.
This supports the game’s intended narrative rhythm:
Rumour
 ↓
Partial understanding
 ↓
Direct observation
 ↓
Journal discovery
 ↓
Connection to wider event
 
⸻
 
64. FACTION PROGRESSION
The player’s relationship with factions can develop through:
story progression
quests
discoveries
actions
reputation where applicable
However, faction reputation should not become a mandatory grind.
The primary progression remains the character/story progression.
Religious affiliation or divine favour is not a general progression system.
 
⸻
 
65. NPC AVAILABILITY
NPC availability can change based on:
location
time/world state
story progression
faction state
completed events
Important story NPCs should not disappear permanently in ways that can make required progression impossible.
 
⸻
 
66. NPC DEATH
NPC death must be categorised.
Narrative NPC
Death is controlled by authored story content.
Persistent World NPC
Death may occur only if explicitly supported by the world system.
Temporary Encounter NPC
Exists only for a specific encounter.
Required story NPCs must not be accidentally removed by ordinary gameplay.
 
⸻
 
67. FACTION TERRITORY
Factions can have geographic influence.
Examples include:
kingdom territory
dwarven territory
tribal territory
pirate-controlled waters
guild influence
Territory is primarily a worldbuilding and narrative concept unless explicitly made into a gameplay mechanic.
 
⸻
 
68. FACTION CONFLICT
Faction conflict should emerge from competing objectives.
Examples:
Kingdom
   ↕
Nobles

Merchants
   ↕
Smugglers

Merchants
   ↕
Pirates

Humans
   ↕
Dwarven interests

Kingdom
   ↕
Desert raiders
These relationships are not inherently permanent.
Religious groups may exist alongside these conflicts without becoming active participants unless explicitly authored.
 
⸻
 
69. NPC AND WORLD EVENTS
NPCs should react to major authored world events.
When an event occurs:
world state changes
affected factions update
relevant NPCs receive new knowledge/state
locations may change
new story bites become available
relevant dialogue changes
This makes the narrative and world systems interconnected.
Religious or divine events must be explicitly authored and must not be generated by an autonomous divine simulation.
 
⸻
 
70. JOURNAL INTEGRATION
NPC interactions should generate Journal content where appropriate.
The Journal stores the player’s discovered understanding rather than every line of dialogue.
This keeps the Journal useful and readable.
Religious dialogue, prayers, omens, and references to gods should only generate Journal content when explicitly connected to a main story or side story.
 
⸻
 
71. NPC DATA MODEL
Conceptually:
NPC
 ├── ID
 ├── Name
 ├── Location
 ├── Faction
 ├── Occupation
 ├── Personality
 ├── Knowledge
 ├── Relationships
 ├── Story Role
 ├── Availability
 ├── Dialogue/Story Bites
 └── World-State Conditions
 
⸻
 
72. FACTION DATA MODEL
Faction
 ├── ID
 ├── Name
 ├── Type
 ├── Territory
 ├── Goals
 ├── Resources
 ├── Relationships
 ├── Knowledge
 ├── Reputation Rules
 ├── World-State Conditions
 └── Story Role
 
⸻
 
73. RELATIONSHIP DATA MODEL
Faction A
      ↓
Relationship
      ↓
Faction B

Relationship:
 ├── Status
 ├── Reason
 ├── Modifiers
 └── World-State Conditions
Relationships should be able to change through story events.
 
⸻
 
74. SERVER AUTHORITY
The server is authoritative over:
NPC state
faction state
faction relationships
world-event reactions
NPC availability
story-critical NPC state
player/faction relationship state
explicitly authored religious or divine events
story-specific supernatural communication
The client renders the current state.
The server must not run an autonomous NPC, faction, religious, or divine simulation.
The server must not create Journal entries for ordinary religious dialogue, prayers, rumours, omens, or flavour interactions.
 
⸻
 
75. CONTENT AUTHORING
The system must allow content authors to define:
NPCs
factions
occupations
relationships
dialogue/story bites
knowledge
rumours
faction objectives
NPC conditions
world-event reactions
quest relationships
religious background details
local religious traditions
gods and their distinct domains
explicitly authored divine events
rare priest abilities
main-story dialogue additions
side-story dialogue additions
main-story conditions
side-story conditions
story-relevant Journal-triggering discoveries
flavour-only interactions
points of interest with story relevance
explicit Journal update conditions
Content authors must explicitly identify:
whether dialogue is flavour or story-relevant
whether a point of interest is connected to a main story or side story
whether an interaction creates a Journal entry
which story owns the Journal entry
any main-story or side-story exception that adds dialogue or changes an otherwise static story state
whether a priest possesses genuine supernatural abilities
whether a supernatural event is objectively divine, magical, historical, ambiguous, or otherwise defined by the story
whether a divine intervention is direct, indirect, ambiguous, or only interpreted as divine
which god, if any, is involved
the god’s domain
whether the event remains within that domain
whether the event is a rare answer to prayer, physical manifestation, miracle, omen, or other authored occurrence
without modifying the underlying engine.
 
⸻
 
76. DESIGN INVARIANTS
NPCs belong to the established world and its societies.
NPCs should have believable motivations.
NPC knowledge is limited by social position and experience.
NPCs do not automatically know the entire world’s truth.
Rumours may be inaccurate.
The world is low-magic.
Powerful magic users are rare.
Wizards and witches tend to be reclusive.
Religion is primarily background and worldbuilding.
Religious content is not a major gameplay system.
Different cultures generally worship different groups of gods.
There is no universally dominant pantheon across the world.
Religious traditions developed independently among descendants of the ancient civilisation.
The gods are objectively real.
Each god has a distinct, mutually exclusive domain of influence.
A god’s domain is an absolute metaphysical boundary.
Gods rarely intervene directly in the mortal world.
A god can manifest physically, but doing so is exceptionally rare.
Devout lifelong servants may occasionally receive whispered answers to prayer.
Divine communication is rare, ambiguous, and precious.
Gods regard humanity as interesting and entertaining distractions rather than subjects they actively govern.
The gods’ long-term objectives are largely incomprehensible to mortals.
Gods’ personalities and motivations tend to follow their domains.
Gods may favour or influence mortals when doing so relates to their domains.
Divine actions may be beneficial, harmful, indifferent, or bizarre from a human perspective.
The god of Agriculture genuinely wants crops and farmland to prosper.
The god of Death is not malicious; death is part of its domain.
The god of Death patiently waits for each person’s appointed time.
The gods are not ordinary NPCs or political actors.
The gods do not provide routine objectives or constant public instructions.
Divine intervention is rare and explicitly authored.
The gods’ intervention in the Ascension was an extraordinary event.
The Ascension is not evidence of normal divine behaviour.
Priests are uncommon.
Powerful priests exist but are rare and exceptional.
Not every priest possesses supernatural abilities.
A priest’s title does not guarantee that their interpretation is correct.
Powerful priests are not omniscient.
Religious traditions may contain partial truth, distortion, symbolism, or error.
No religious institution automatically possesses complete knowledge of the gods.
Gods are not treated as an everyday visible game mechanic.
The ancient civilisation possessed vastly greater magical capabilities.
Modern societies possess only fragments of that knowledge.
Ancient magic and divine power are not automatically treated as the same thing.
The relationship between the ancient civilisation and the gods remains part of the deeper mystery.
The King is broadly regarded as wise and supported.
The kingdom nevertheless suffers political and social instability.
Noble intrigue exists.
Crime and banditry exist.
The King’s Army is an important institution.
The forest protagonist eventually joins the King’s Army.
The coastal protagonist begins as an orphan/street rat.
The coastal protagonist enters a merchant household after saving a merchant from bandits.
Merchants are affected by wider trade disruption.
Pirates and smugglers are established parts of coastal society.
The mountain protagonist is a blacksmith apprentice.
The mountain protagonist regularly interacts with a nearby dwarven city.
Tools and ore form an established human-dwarven trade relationship.
Dwarven mining is affected by monsters emerging from the deep mountains.
The desert contains multiple tribes.
Those tribes have unusually united.
The united tribes raid distant settlements.
Adventurer guilds exist.
Trade guilds exist.
Factions are not reduced to Good/Evil alignment.
Factions have competing objectives and relationships.
Different factions possess different information about world events.
Shared world events affect multiple factions differently.
NPCs can provide rumours and partial information.
NPC information can feed the Journal/story-bite system when story-relevant.
NPC dialogue may reflect established world conditions.
Important NPCs should have distinct personalities.
Dialogue should remain concise and purposeful.
The game should not depend on large branching dialogue trees.
Main-story and side-story NPCs cannot accidentally disappear and block progression.
NPCs do not dynamically change through ordinary gameplay.
Factions do not dynamically change through ordinary gameplay.
NPCs do not die through ordinary gameplay.
NPCs do not relocate through ordinary gameplay.
NPC dialogue is static by default.
Only explicitly authored main-story or side-story dialogue values may be added.
Main-story and side-story dialogue additions do not create unrestricted dynamic dialogue.
Most NPC interactions are flavour and worldbuilding only.
Most points of interest are flavour and worldbuilding only.
Journal entries are created only when information relates to a main story or side story.
Ordinary dialogue does not automatically update the Journal.
Ordinary points of interest do not automatically update the Journal.
The three starting storylines provide different social perspectives.
The three perspectives eventually intersect through shared world events.
Ancient ruins and haunted battlefields provide different social interpretations of history.
The ancient civilisation remains a mystery that is gradually uncovered.
NPCs should contribute to the player’s understanding without immediately explaining the world’s deepest mysteries.
NPC and faction content is persistent.
NPC and faction content is data-driven.
NPC and faction content does not require autonomous simulation.
Optional quests do not alter NPC identity, survival, location, or dialogue unless explicitly authored as side stories.
Optional quests do not alter faction relationships unless explicitly authored as side stories.
Main-story and side-story exceptions must be explicitly authored.
The server is authoritative over NPC and faction content.
The client renders the authored state.
Journal updates must be explicitly tied to a main story or side story.
Flavour and worldbuilding interactions do not create persistent Journal entries.
Story relevance must be defined during content authoring.
Religious interpretations are not automatically objective truth.
Religious disagreement does not automatically identify one side as evil or correct.
A miracle does not automatically explain a god’s motives.
A supernatural event may be genuine without being correctly interpreted.
Direct divine appearances or communications require explicit story authoring.
The game does not include automatic divine approval or punishment for ordinary player actions.
Religious factions do not autonomously mobilise, split, reform, or change doctrine.
Religious content updates the Journal only when relevant to a main story or side story.
The objective truth of a story-relevant religious or supernatural event must be explicitly authored.
The source of a supernatural event may be divine, magical, historical, ambiguous, or otherwise defined by the story.
The player may encounter uncertainty about the gods without receiving an immediate definitive answer.
Religious content should generally remain background unless explicitly used in a small side story or main-story event.
A god cannot act outside its absolute domain.
Divine communication does not guarantee clarity or completeness.
The gods’ motives are not required to be understandable to mortals.
Divine actions may be beneficial, harmful, or bizarre without being morally simple.
The Ascension’s divine intervention must be treated as exceptional rather than routine.
 
⸻
 
77. DEPENDENCIES
Depends on
World & Exploration
Story & Narrative
Journey & Dungeon
Quest
Journal
Persistence
Used by
Story
Journal
Quests
Exploration
Settlements
Merchants
Guilds
Supernatural events
Combat encounters
UI
World-state system
The World-state system may provide main-story or side-story conditions for additional dialogue values, supernatural events, and Journal updates, but it must not be interpreted as permission to dynamically alter NPCs, factions, religious institutions, or divine behaviour outside explicitly authored story content.
The Journal system must distinguish story-relevant information from flavour and worldbuilding content.
 
⸻
 
78. OPEN CONTENT WORK
The following are content-authoring tasks and should be developed separately:
Final NPC roster
Final faction roster
Exact faction names
Exact settlement populations
Individual NPC personalities
Individual NPC relationships
Final king/noble characters
Army hierarchy
Merchant organisations
Adventurer Guild structure
Trade Guild structure
Dwarven political structure
Desert tribal leadership
Pirate organisations
Local religious background
Cultural religious traditions
Names and domains of the gods
Relationships between different cultural pantheons
Historical religious interpretations of the Ascension
Individual wizard/witch characters
Individual priests
Rare powerful priest characters
Priest abilities
Sacred sites
Religious artefacts
Main antagonist/faction identities
Exact faction questlines
Final faction relationship matrix
Static dialogue for each NPC
Main-story dialogue additions
Side-story dialogue additions
Main-story conditions for additional dialogue
Side-story conditions for additional dialogue
Story-relevant Journal entries generated by NPC interactions
Story-relevant Journal entries generated by points of interest
Flavour-only dialogue and interactions
Flavour-only points of interest
Explicit documentation of any main-story or side-story NPC exception
Explicit documentation of which interactions update the Journal
Explicit documentation of which interactions remain flavour and worldbuilding only
Explicit documentation of the objective truth of religious and supernatural story events
Explicit documentation of whether each supernatural event is divine, magical, historical, ambiguous, or otherwise defined
Explicit documentation of religious interpretations and whether they are correct, incomplete, or false
Explicit documentation of any direct divine appearance, communication, miracle, or intervention
Explicit documentation of the gods’ absolute domains
Explicit documentation of the Ascension’s divine intervention and why it was exceptional
These should be derived from the established world rather than invented independently of it.
 
⸻
 
END OF SPECIFICATION
