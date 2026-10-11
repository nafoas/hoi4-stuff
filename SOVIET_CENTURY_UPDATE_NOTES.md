# Soviet Century: update to HoI4 1.19 and Red World: Alien Nation

The mod lives in `soviet-century/`. Copy that folder (with `descriptor.mod`) into
`Documents/Paradox Interactive/Hearts of Iron IV/mod/`, add a matching `.mod` file
pointing at it, and load it after **Red World: Alien Nation**.

## How the two mods were combined
- For every file both mods ship, the fork's current version is the base, and Soviet
  Century's content is layered back on top. Nothing is blanket-overwritten.
- Content only in Soviet Century (its countries, trees, events, ideas, characters,
  icons, text) is kept. Content only in the fork is kept.
- Where both define the same focus, event, idea, character or text, Soviet Century's
  version stays if it ties into Soviet Century's own content or clearly has more to it.
  Otherwise the fork's newer version is used.
- Focuses are merged field by field: the fork's position, icon and cost, plus Soviet
  Century's rewards where they hook into its content. Soviet Century branches that
  overlapped the fork's new USA (Rumsfeld/Bush/Cheney) and American State branches
  were moved sideways.
- Characters use the fork's ideology and portraits but keep Soviet Century's extra
  roles and leader traits.
- Duplicate sprites and text that just copied the fork were removed. Soviet Century's
  text for its own events and focuses is in `localisation/english/replace/`, so it wins.

## Deliberate choices you may want to revisit
- **The fork's annexation decisions and events are enabled** (Soviet Century's empty
  override files were removed). The nine breakaway tags have no annexation decisions
  of their own, because the fork doesn't know about them.
- **British events: Soviet Century renumbered the old fork's events.** It moved them to
  britain.507–574 / 740–744 and reused the old numbers (mostly britain.229–311) for its
  own new events. The fork reused those same numbers for different events. All 82 events
  Soviet Century wrote its own text for (78 British, 3 USA, 1 American State) are back
  to Soviet Century's version, with its text in `localisation/english/replace/`. Six fork
  events (britain.7, 11, 120, 142, 143, 144) are also back to Soviet Century's version,
  because the fork's versions call the reused numbers and would land on Soviet Century's
  events.
- **The fork's own British date-triggered events** were checked one by one. Nothing in
  Soviet Century calls them or depends on anything they set (flags, ideas, characters).
  - Kept switched off (marked `# Soviet Century:` in `events/Britain.txt`):
    - britain.244, 260, 261, 262: renumbered duplicates of Soviet Century's britain.519
      (McCluskey meets Galloway) and 534/536/538 (Tony Benn rushed to hospital). Turning
      them on would fire those stories twice.
    - britain.168, 169 (2011/2014 general elections): these set the ruling party and the
      fork's cabinet, and would override Soviet Century's storyline. Soviet Century has
      its own elections (britain.170, 258, 565, 567, …).
    - britain.167 (Parliamentary Vote on Terms): only sets up the fork's 4-year election
      cycle that 168/169 belong to.
  - Left on: britain.166, 174, 177, 178 (2010/2014 Conservative and 2012/2015 Labour
    leadership elections). They only promote a party leader, call nothing else and don't
    clash with Soviet Century.
- `remote_file_id` was removed from `descriptor.mod`, since it belongs to the original
  author's Workshop item.

## Rename/duplicate audit (event IDs, flags, focuses, ideas)
Everything that two mods could name differently, or define twice, was cross-checked:
- **Shared focuses, ideas, decisions, characters and traits where the fork's version won:**
  Soviet Century never wrote its own text for any of them, so they were old-fork copies,
  not reused names. Where they differ a lot, the fork's versions are the 1.19 updates.
- **Events Soviet Century calls from the fork (95, mostly news.*):** all still point to
  the same story in the fork. None were renumbered.
- **Event numbers both mods use for different events:** where the fork still needs its
  event (it fires on its own, or other fork content calls it), Soviet Century's event was
  moved to a new number and the fork's event put back at its original number:
  - britain.229–233, 238, 239 → Soviet Century's are now britain.2229–2239. The fork's
    Liberal Democrat / SDP leadership elections are back.
  - britain.252–254 → 2252–2254. The fork's Maoist-coup chain from britain.142–144 is back.
  - britain.306–308, 311 → 2306–2311. The fork's Ireland storyline from britain.7/11 is back.
  - pence.5, pence.6 → pence.105, pence.106. The fork's "'No Nose' Passes Away" and
    "High Command Defects" are back. The fork's Commonwealth events call pence.6.
  Soviet Century's own callers and text keys were updated to the new numbers.
- britain.7, 11, 120, 142, 143, 144 use the fork's versions. britain.120's calls to the
  fork's renumbered Galloway/Corbyn events point to Soviet Century's copies (515, 516).
- **Fork content checking flags that only the displaced fork events set:** the flags were
  added to Soviet Century's equivalent events or focuses:
  - royal_family_executed (britain.137), CAN_monarchy_exists_in_canada and
    CAN_andrew/edward_leads_exiles (britain.500): needed by the fork's Canada storyline.
  - USA_war_with_TEX (usa.5/usa.6): needed by the fork's Second Texan War decisions.
  - british_republic (focus ENG_The_Republic).
  - britain_shirley_williams_retirement (britain.511), ENG_corbyn_in_cabinet (britain.551).
- **Shared events where Soviet Century only added options:** these now use the fork's
  updated event plus Soviet Century's extra option. usa.2 gets the fork's cabinets plus
  the McAfee option, which the fork's new Rumsfeld/Cheney branches need. usa.3 gets the
  Liberty Front option. britain.170 gets the Green option.
- **Checks for the fork's UK focuses that Soviet Century's tree replaces:** three were
  pointed at Soviet Century's equivalents (Lower Company Taxes, Unite the Isle, Cut
  Military Spending). The rest have no equivalent; those fork branches stay inactive
  while Soviet Century's UK tree is in use.
- **Duplicates removed:**
  - `left_extended_tree.txt`: 66 focuses already in uk_shared.txt.
  - A second, dead `texas.112` event.
  - A second `idea_unitary_scotland` definition.
  - A shine sprite that shared its name with the icon it animates, overriding it.
- **Variables, event targets, cosmetic tags and missions:** clean.
- **Known fork-side issues left alone:** the fork's own usa.2 references an undefined
  idea `usa_nsm_robert_gates`. The fork's USA characters / leader traits define
  `USA_howard_lutnick` and `ideological_crusader` twice.

## 1.19 / fork compatibility fixes
- Dependency switched to `Red World: Alien Nation`, `supported_version = "1.19.*"`.
- `create_faction` changed to `create_faction_from_template` (generic template) and
  `add_threat` changed to `add_named_threat`, matching what the fork uses everywhere.
- The nine British breakaway tags (ABS, COW, EAG, KET, MCS, MER, NCS, NOF, WES) had
  history files and trees, but neither mod defined the countries. They now have tag
  definitions, colours, names and **simple placeholder flags** (`gfx/flags`). Replace
  the flags with proper art if you have it.
- Old ideology names were mapped to the fork's (e.g. green → liberal / green_liberal,
  juche → national_stalinist, united_labour → labourist). Capitalised names such as
  `Liberal` and `Monarchist` were lowercased. Two subideologies the submod still uses,
  `black_sun` and `reformism`, were added to the fork's lists.
- Non-existent OOBs (SCO_1962…, WAL_1962), naval techs and Scottish flavour events
  were removed from breakaway histories. Wrong capitals were fixed: Brittany, Cornwall,
  Aberdeenshire, Mercia and Kent.

- Every effect, trigger and modifier the submod uses was checked against the game's
  1.19 `documentation/` (effects, triggers, modifiers) plus the base game's and fork's
  scripts. Nothing invalid remains; deprecated-but-working effects are noted below.
- The fork's `equipment_l_english.yml` replaces the base game's and is missing 2,857
  1.19 keys (e.g. "Convoy", ship and armour descriptions). Soviet Century ships that
  file, so the missing base-game keys were added back to it.

## Bugs fixed in the original submod
- Brace errors that broke parsing in usa.txt, american_state.txt, Britain/Scotland
  events, Britain and Wales ideas, several UK trees, and the focus shine sprite file
  (rebuilt, 111 duplicate sprites removed).
- `uk_right_wing_tree.txt` (bare focuses outside any tree, all duplicated in
  uk_shared.txt) was removed.
- Disabled Scottish focuses whose bodies were still active were commented out properly.
- Typos in focus/idea/tag references: ENG_democratic_reform, ENG_Prepare_For_War,
  idea_lin_minorty_rescitance_N, CON → COW, `create_country_flag` → `set_country_flag`,
  `has_ideas` → `has_idea`, `defense_attack_against` → `attack_bonus_against`, and two
  dangling prerequisites (Texas Burr unification, American State family values).
- `idea_secret_police` (Britain) clashed with the fork's Cascadia idea, so it was
  renamed `idea_ENG_secret_police`.

## Known leftovers (already broken in the original submod)
- Ideas used but never defined: idea_state_investment, idea_building_business_centers,
  idea_introduce_minimum_wage, idea_send_in_the_army, idea_lin_exploited_mexican_workers,
  idea_lin_inuit_autonomy, idea_return_of_corbyn, britain_sic_jo_cox. These effects do
  nothing.
- Missing text for some events (texas.26/42/82/87/105–113, britain.526/536/571/1002,
  lin.25) will show raw keys.
- Breakaway country leaders still use the older `create_country_leader` /
  `create_navy_leader` syntax. It still works but is deprecated.
- Run once with `-debug` and check `error.log` for anything static checks can't catch.
