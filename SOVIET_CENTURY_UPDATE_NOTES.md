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
- **The fork's annexation decisions and events stay disabled** (empty
  `annexation_decisions.txt` / `Annexations.txt`), as in the original submod. Delete
  those two files to get the fork's annexation system back.
- **The fork's UK date-triggered elections no longer fire on their own**
  (britain.166–169, 174, 177, 178, 244, 260–262), because they would run over Soviet
  Century's British storyline. Delete the `is_triggered_only` line marked
  "Soviet Century" in `events/Britain.txt` to restore any of them.
- `remote_file_id` was removed from `descriptor.mod`, since it belongs to the original
  author's Workshop item.

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
- Not checked against the game's own 1.19 `documentation/` files, which weren't
  provided. Run once with `-debug` and check `error.log` for anything left.
