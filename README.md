# Shin Pokémon Red and Blue: Lite Patch

Future bugfixes here will be eventually migrated to the Shin Pokemon Red/Blue master branch

Download the IPS patch file of the version you want and apply it to its respective USA rom.  
Always apply patches to a fresh USA ROM or else strange glitches will occur.  

Important Note: If you are using a save file from a previous version, you might be blocked by invisible walls upon loading the game.
To fix this, you must use the Softlock Warp detailed below to teleport back to Palette Town.

This is primarily a fix-it patch of pokemon red & blue based on the Pret team's disassembly.  
The Lite patch, unlike the full Shin Pokemon Red/Blue, tries to fix bugs and improve the AI with little else changed.
It was done to serve as a codebase for others to start their own romhacks.


#Latest Fixes:
---------------
- Removed the girl from outside Bill's house. She is only supposed to be in the master branch.
- Reverted the bush in celadon city
- made checking the ghost marowak flag more robust
- fixed some text in the saffron house with the pidgey
- fixed some badge house guy text
- fixed map objects and text in celadon


#Bugfixes:
-----------

- Battle engine fixes
  - Moves no longer have a default 1/256 chance to miss
  - Fixed freeze that occurs in defense stat scaling (def < 4 glitch)
  - Enemy ai ignores type effectiveness for moves that have zero power
     - prevents things like spamming agility against poison pkmn
  - Enemy ai ignores super-effectiveness for moves that do static amounts of damage
  - Fixed skipping move-learn on level-up glitch. 
     - when gaining multiple levels at a time, each in-between level is incrementally checked for moves learned
     - this prevents a pkmn from skipping learnable moves if gaining multiple levels in battle
	 - also does this when evolving via level-up for the new evolution's movelist
  - Burn & Paralyze stat penalties are now properly applied after Speed & Attack stats get updated/recalculated
  - Badge stat-ups no longer stack when stat-up/down effects are applied to the player's pkmn
  - If player is frozen, the hyperbeam recharge bit is now cleared
     - now matches how enemy mon's recharge bit is cleared upon being frozen
     - this prevents getting stuck in a loop unable to do anything on your turn
  - Blaine will not use a healing item at full HP
  - Move slots cannot be rearranged when transformed (prevents acquiring glitch moves).
  - The BIRD type has been reinstated and renamed to TYPELESS. It acts as a universally neutral type (particularly for Struggle)
  - AI trainers have priority on switching or using an item
  - AI type effectiveness function now takes type 1 and 2 into account together 
	 - Before AI would only look at the type it encountered first in a list search
     - AI will now treat a move as neutral if type 1 makes it supereffective but type 2 makes it not effective
  - Stat changes from burn and paralyze are applied when the ai sends out a pkmn with those conditions
  - New custom function for undoing the stat changes of burn and paralysis
	 - undoing paralysis is accurate to within 0 to -3 points
	 - undoing burn is accurate to within 0 to -1 point
  - AI routine #2 (prioritize buffing or use a status move) now activates on the 1st turn after sendout instead of the 2nd
  - AI using full heal now reverts brn/par stat changes
  - Condition healing items (including using Full Restore at max hp) no longer reset all stats
	 - Burn heal undoes the attack stat changes
	 - Paralyze heal undoes the speed stat changes
	 - Full restore at max hp undoes the stat changes of brn/par
  - Full Restore when used in battle to heal HP now undoes the stat changes of brn/par
  - Haze and status-curing items now clear the toxic counter
  - The function that applies badge stat-ups now selectively boosts the correct stat when called during a stat-up/down effect
  - A wild marowak is no longer assumed to be the ghost marowak
  - Pokedoll is disallowed during ghost marowak battle

- Move fixes
  - dire hit/focus energy now quadruples crit rate instead of quarters
  - sleep now normal-chance hits a pkmn recharging from hyperbeam, but has no effect if it's already status-effected
  - the fly/dig invulnerability bit is cleared when a pkmn hurts itself from confusion or is fully paralyzed
  - psywave damage is always min 1 be it an opponent or yourself (prevents desync)
  - Substitute fixes
    - all hp drain moves (including dream eater and leech seed) miss against substitute
    - substitute will not work if it would bring you to exactly 0 hp
    - zero power moves that inflict stat-downs, sleep, or paralyze will not affect a substitute
    - the confusion side-effect of damaging moves is blocked by a substitute
	- recoil damage from jump kicks or hurting oneself in confusion is now applied to user's substitute
  - healing moves work with restoring exactly 255 or 511 hp 
  - light screen and reflect now have a cap of 999
  - haze removing sleep/freeze will not prevent a multi-turn move from getting stuck
     - Fixed by allowing sleeping/frozen pkmn to use a move after haze restores them
     - on the plus size, haze now restores both opponent and user's status conditions as was intended in gen 1
  - Rest now does the following:
     - also clears the toxic bit and toxic counter
     - also undoes the stat-downs of burn and paralyze
  - fixed-damage moves (seismic toss, dragon rage, etc) can no longer critically hit
  - fixed-damage moves now obey type immunities
  - Transform will no longer copy the opponent's Transform move. It's swapped-out for Struggle
  - Struggle is now TYPELESS so that it can always neutrally damage something
  - Metronome & mirror move will not increment PP if the user is transformed
     - This prevents adding PP to hidden dummy moves that prevent a pkmn from going into Struggle
     - This also prevents Disable from freezing the game by targeting a dummy move
  - Mirror Move is checked against partial trapping moves in a link battle to prevent desync
  - Bide's accumulated damage bytes are now both set to zero on an enemy faint in order to prevent desync
  - Jump Kick moves now do the correct recoil damage on a miss
  - The effects of Leech Seed and Toxic no longer stack
  - Trapping effects only clear the hyperbeam recharge bit on a hit, preventing its automatic use on a miss
  - Trapping move PP can no longer underflow due to an opponent switching pkmn
  - Raging and Thrashing no longer suffers from accuracy degradation
  - Breaking a substitute does not nullify explosion/self-destruct, hyper beam recharge, or recoil damage
  - Hyper beam must recharge if it knocks out the opposing pkmn
  - Bugfixes involving Counter:
    - works against BIRD type, which is now typeless and assigned only to STRUGGLE
    - To prevent desync, pressing B to get out of the move selection menu zeros-out the ram location for selected move & move power
    - last damage dealt is zeroed in these cases (also fixes some issues with Bide):
	  - it's the start of the round without a trapping move active (fixes most issues since Counter always goes second)
	  - player/enemy pkmn is fully paralyzed or after hurting itself in confusion
    - Crash damage from jump kicks and pkmn hurting itself cannot be Countered

- Misc. fixes
  - Great ball has a ball factor of 12 now, and Safari Ball looks like it was supposed to be factor 8
  - Cinnabar/seafoam islands coast glitch fixed (no more missingo or artificially loading pokemon data)
  - Stone evolutions cannot be triggered via level-up anymore
  - Catching a transformed pokemon no longer defaults to catching a ditto
  - Returning from the status screen when an opponent is in substitute/minimize no longer glitches the graphics
  - PP-up uses are disregarded when determining to use STRUGGLE if one or more moves are disabled
  - PC graphic restored to celadon hotel
  - A tile in cinnabar mansion 3f is slightly modified to prevent getting permanently stuck
  - A tile in cerulean cave 1f adjusted so there isn't a walkable cliff tile
  - Ether and elixer now account for PP-ups used when determining if move is at full PP
  - Vending machine now checks for the correct amount of money
  - Prevented byte overflow when determining the trash can with 2nd switch in vermillion gym
  - Hidden nugget in safari entrance now obtainable
  - EXP ALL should now dispense the correct exp if multiple pokemon take place in a battle
  - EXP ALL no longer counts fainted pokemon when dividing exp
  - Enemy DVs can no longer be manipulated by having it use transform multiple times
  - Fixed a bug where itemfinder can't locate objects with a zero x or y coord
  - After defeating the cerulean burglar rocket, the guard itself always moves to prevent getting stuck in the front door
  - Slot machine reel bug fixed
  - Fixed oversights in reel functionality to better match Gamfreak's intent
  - Surfboard bugfixes:
	  - cannot use the surfboard if being forced to ride the bicycle
	  - no longer freezes the game when using it from the item menu to get back on land
	  - the menu text will glitch a little, but only for a split-second and does not impact gameplay
  - The ABCD teleport glitch has been fixed
  - The lift key in the rocket hideout drops during the end of battle text like in Yellow-version
  - A statue base is now blocking terrain while surfing.
  - Trainer escape glitch has been plugged. Using fly/teleport/escape rope is negated entirely if spotted by a trainer.
  - No more fishing or surfing in statue bases


#TWEAKS:
-----------
- Loading AI trainer parties uses the code from pokemon Yellow so as to allow custom movelists
- If wGymLeaderNo is set to 9 when loading a battle, then the final battle music will play
- Softlock Warp 
  - instantly teleport back to your mom's house if you get stuck or are unable to move after updating to a new patch
  - Intructions to perform:
    - go to the start menu and put the cursor on OPTION
	- press and hold DOWN on the d-pad (the cursor will now be on EXIT)
	- while continuing to hold DOWN, press and hold SELECT
	- while continuing to hold those two buttons, press B
	- the start menu should close and you will warp back to your mom's house
- Slot machine coin counter runs twice as fast
- Interaction of slot reel modes tweaked for better gameplay
- The surfboard, a nugget, and TM 15 are hidden items added to the vermilion dock
- Blaine has a touched-up battle sprite so he doesn't look like an alien
  - Snagged this off reddit, but original artist unknown (let me know if this is yours)

- Fixed mistakes and made adjustments to the game text
  - When a pkmn is caught and fills the box, a reminder is printed that the box is full
  - Man in cinnabar won't mention raichu evolving
  - Koga correctly says soul badge increases speed
  - Lt. Surge correctly says thunder badge increases defense
  - Correct type effectiveness information & sfx should now be displayed when attacking dual-type pkmn
  - Viridian girl's notebook 2nd page revised for pkmn-catching effectiveness
  - Viridian blackboard BRN info corrected (BRN does not reduce speed)
  - Viridian Blackboard PAR info updated
  - TM 18 given an actual explanation 
  - New student in viridian school explains ohko moves
  - Cerulean badge-house guy has updated text
  - Prof. oak's speech plays the correct Nidorino cry
  - Text for using a TM/HM now refers to the "machine" rather than just "TM"
  - Fixed daycare man capitalization
  - Clarified "chem" to mean grade in chemistry
  - Fixed capitalization in safari zone entrance
  - PC has a text prompt to tell you if its full after depositing
  - Exp.all now prints one message when splitting exp instead of for each party member
  - text is now properly flipped in one of the saffron houses

- Adjustments to moves  
  - Stat-down moves no longer have a 25% miss chance in AI matches
  - Moves that hit multiple times in a turn now calculate damage and critical hits for each individual attack
  - Switching out of a trapping move ends it immediately and wastes its user's turn (prevents PP underflow glitch)
  - Ghost moves (i.e. just Lick) do 2x against psychic as was always intended
  - Changes to Bide
    - damage accumulation is done after taking a damaging hit instead of during turn execution (less room for glitches)
	- side effect: bide is buffed because multi-hit moves now add damage to bide for each of the 2 to 5 hits
	- changed to Typeless to play nicer with AI routine 3 (it ignores the type chart regardless)
  - Rest's sleep condition increased to 3 turns since attacking on wakeup is now allowed.
  - Acid armor's animation changed so that does not make its user disappear
  - Metronome now classified as a Typeless special damage move to play better with the AI

- Adjustment to stat mods, conditions, and items
  - Sleep does not prevent choosing a move
  - Waking up from sleep does not waste the turn and the chosen move is used
  - The effect of X Accuracy is no longer applied to one-hit K.O. moves (it originally made them auto-hit)
  - Upped the power of safari balls to account for lower ball factor
  
- Trainer ai routine #1 (recognition of stats, hp, and conditions) has been modified
  - using a move with a dream eater effect is heavily discouraged against non-sleeping opponents
  - using a move with a dream eater effect is slightly encouraged against a sleeping opponent
  - using a zero-power confusion effect move is heavily discouraged against confused opponents
  - moves that would miss against an active substitute are heavily discouraged
  - stat buff/debuffs are heavily discouraged if it would have no effect due to hitting the buff/debuff stage limit
  - heavily discourage double-using lightscreen, reflect, mist, substitute, focus energy, and leech seed
  - leech seed won't be used against grass pkmn
  - do not use moves that would be blocked by an active mist effect
  - rules for using healing moves:
    - heavily discourage healing if at max hp
	- slightly encourage healing if below 1/3 hp
	- slightly discourage healing if above 1/2 hp
  - heavily discourage using Counter against a non-applicable move
  - heavily discourage roar, teleport, & whirlwind
  - heavily discourage disable against a pkmn already disabled
  - Substitute discouraged if less that 1/4 hp remains
  - Rage is heavily discouraged
  - Will discourage using Haze if unstatus'd or has net-neutral or better stat mods
  - Will heavily discourage boosting defense against special, OHKO, or static-damaging attacks

- Trainer ai routine #3 (choosing effective moves) has been modified
  - It now heavily discourages moves that would have no effect due to type immunity
  - zero-power buffing/debuffing moves are randomly preferenced 12.5% of the time to spice things up
  - zero-power buffing/debuffing moves are randomly discouraged 50% of the time to let ai always have a damage option
  - OHKO moves are heavily discouraged if the ai pkmn is slower than the player pkmn (they would never hit)
  - Static damage moves are randomly preferenced 25% of the time to spice things up
  - Thunder Wave is not used against immune types
  - Poisoning moves discouraged against poison types

- Trainer ai routine #4 is no longer unused. It now does rudimentary trainer switching.
  - 25% chance to switch if active pkmn is below 1/3 HP
  - chance to switch based on power of incoming supereffective move
  - 12.5% chance to switch if a move is disabled
  - 12.5% chance to switch if afflicted with leech seed
  - 50% chance to switch if afflicted with toxic poison
  - 25% chance to switch if opponent is using a trapping move
  - 25% chance to switch if active pkmn is confused
  - on the lowest stat mod, 12.5% chance to switch per lowered stage
  
- Trainer ai routine #3 added to the following trainer classes
  - jr trainer M, jr trainer F, hiker, supernerd, engineer, lass, chief, bruno, brock, gentleman, agatha
- Trainer ai routine #4 added to the following trainer classes
  -lass, jr trainer m/f, pokemaniac, supernerd, hiker, engineer, beauty, psychic, rocker, tamer, birdkeeper, cooltrainer m/f, gentleman
  -prof.oak, chief, gym leaders, e4
  
- Trainer AI battles now track which enemy pkmn have already been sent out, so allows for new functionality:
  - Trainer pkmn DVs are remembered between switching, and new ones won't be generated on every send-out
  - Trainer pkmn can now have stat experience assigned to them that is scaled to their level
  - These are real DVs and statEXP values that utilize the existing enemy party_struct which is normally unused by trainer AI
- Agatha & cooltrainers will not randomly switch since they now have ai routine 4
- Flags for dividing exp among active pokemon are now only reset after fainting an enemy pkmn
  - Originally these get reset every time the opponent send out a pkmn (even swithing)
  - Was never really noticed since most trainers never switch nor would have the opportunity
  - Changed based on user feedback since many trainers now try to switch

- Adjustments to learnsets and base stats
  - Mewtwo can learn Swift by TM 



#CREDITS / SPECIAL THANKS:
-----------
- The Pret team for providing the base disassembly and all the code comments that came with it.
- The following folks for their great tutorials, glitch videos, and explanations across the internet:
  - TheFakeMateo 
  - Crystal_
  - ChickasaurusGL
  - v0id19
- The following Redditors for their help in pointing out and diagnosing bugs 
  - kadetPirx
  - JOBOalthor1992
  - krazsen