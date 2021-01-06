# Roll20 D&D 5e General Macros using PowerCards

These macros cover general rolls that are common to all Roll20 players/characters.

> These macros utilize the [PowerCards API](https://wiki.roll20.net/Script:PowerCards) which requires a Pro account in Roll20. Talk to you game master or the owner of the game session concerning this.

In order to use these macros you must create them either in your character sheet or in the macros list.

## Spells

### Hex
	!power {{
		 --replaceattrs|S-|@{selected|character_id}
		 --replaceattrs|T-|@{target|character_id}
		 --replacespell|@{selected|character_id}|Hex
		 --titlefontshadow|none
		 --title|School: ~SP-SCHOOL$ ^^ Level: ~SP-LEVEL$ ^^ Components: V,S,M, A petrified eye of a newt ^^ Casting Time: ~SP-CASTINGTIME$ ^^ ~SP-ATHIGHER$
		 --name|~SP-NAME$
		 --leftsub|~SP-OUTPUT$
		 --rightsub|Range: ~SP-RANGE$
		 --tokenid|@{selected|token_id}
		 --target_list|@{target|token_id}
		 --emote|~S-CN$ places a curse on ~T-CN$
		 --hroll|[[ [$sLvl] ?{Cast at:|Level 1,1|Level 2,2|Level 3,3|Level 4,4|Level 5,5|Level 6,6|Level 7,7|Level 8,8|Level 9,9} + 0d0 ]]
		 --Spell Cast at:|Level ?{Cast at:}
		 --Target:|A creature that you can see within range

		 --!hrule1|~~~
		 --?? ?{Cast at:} < 3 ?? Duration:| ~SP-DURATION$
		 --?+ ?{Cast at:} >= 3 AND ?{Cast at:} < 5 +? Duration:|Up to 8 hours
		 --?+ ?{Cast at:} >= 5 +? Duration:|Up to 24 hours

		 --:EndOfCard|
		 --!hrule2|~~~
		 --!desc|**Description:** ~SP-DESCRIPTION$
		 --api_token-mod| _ids @{target|token_id} _ignore-selected _set statusmarkers|bleeding-eye
	 
	}}

### Eldritch Blast
	!power {{
		--replaceattrs|S-|@{selected|character_id}
		--replaceattrs|T-|@{target|character_id}
		--replacespell|@{selected|character_id}|Eldritch Blast
		--titlefontshadow|none
		--title|School: ~SP-SCHOOL$ ^^ Level: ~SP-LEVEL$ ^^ Components: V,S ^^ Duration: Instantaneous ^^ ~SP-ATHIGHER$
		--name|~SP-NAME$
		--leftsub|~SP-OUTPUT$
		--rightsub|Range: ~SP-RANGE$
		--tokenid|@{selected|token_id}
		--target_list|@{target|token_id}
		--emote|~S-CN$ focuses dark energies into a beam of death in to ~T-CN$
		--Attack:|[[ [$Atk] ?{Attack|Standard,1d20|Advantage,2d20kh1|Disadvantage,2d20kl1} + ~S-MCHA$[CHA] + @{selected|pb}[PROF] ]] vs AC
		--hroll|[[ [$Hexed] ?{Apply Hex?|No, 0|Yes, 1} + 0d0 ]]
		--Target:|A creature within range
		--?? $Atk.base >= @{selected|default_critical_range} ?? skipto*1|Critical
		--?? $Atk.base == 1 ?? skipto*2|Fumble
		--?? $Atk.total >= @{target|npc_ac} ?? skipto*3|Hit

		--:Miss| Since we didn't skip to anywhere else, assume a miss
		--!hrule1|~~~
		--Miss:|Your attack missed.
		--skipto*4|EndOfCard

		--:Fumble|
		--!hrule2|~~~
		--Fumble:|OMG! WTF Happened?!
		--api_fumble|
		--skipto*5|EndOfCard

		--:Hit|
		--?? $Hexed == 0 ?? skipto*6|HitDmg
		--?? $Hexed == 1 ?? skipto*7|HitDmgHex

		--:HitDmg|
		--!hrule3|~~~
		--Hit: *1|Your attack hits for [#[ [$dmg1] ~SP-DAMAGE$ + ~S-MCHA$[CHA] ]#] points of //~SP-DAMAGETYPE$// damage!
		--alterbar1|_target|@{target|token_id} _bar|1 _amount|-[^dmg1.total] _show|all
		--skipto*8|EndOfCard

		--:HitDmgHex|
		--Cursed (HEX): *1|I can smell death emanating from those wounds.
		--!hrule4|~~~
		--Hit: *2|Your attack hits for [#[ [$dmg2] (~SP-DAMAGE$ + ~S-MCHA$[CHA]) + @{selected|repeating_damagemod_$0_global_damage_damage}[Hex] ]#] points of //~SP-DAMAGETYPE$// and //@{selected|repeating_damagemod_$0_global_damage_type}// damage!
		--alterbar2|_target|@{target|token_id} _bar|1 _amount|-[^dmg2.total] _show|all
		--skipto*9|EndOfCard

		--:Critical|
		--?? $Hexed == 0 ?? skipto*10|CritDmg
		--?? $Hexed == 1 ?? skipto*11|CritDmgHex

		--:CritDmg|
		--!hrule5|~~~
		--Critical Hit: *1|You strike a decisive blow for [#[ [$dmg3] (~SP-DAMAGE$ + ~S-MDEX$[DEX]) + (~SP-DAMAGE$ + ~SP-DAMAGE$) ]#] points of //~PCA-dmgtype$// damage!
		--alterbar3|_target|@{target|token_id} _bar|1 _amount|-[^dmg3.total] _show|all
		--skipto*10|EndOfCard

		--:CritDmgHex|
		--Cursed (HEX): *2|Oh, this is going to hurt special like!
		--!hrule6|~~~
		--Critical Hit: *2|You strike a decisive blow for [#[ [$dmg4] (~SP-DAMAGE$ + ~S-MDEX$[DEX]) + (~SP-DAMAGE$ + ~SP-DAMAGE$) + (@{selected|repeating_damagemod_$0_global_damage_damage}[Hex] + @{selected|repeating_damagemod_$0_global_damage_damage}[Hex]) ]#] points of //~SP-DAMAGETYPE$// and //@{selected|repeating_damagemod_$0_global_damage_type}// damage!
		--alterbar4|_target|@{target|token_id} _bar|1 _amount|-[^dmg4.total] _show|all

		--:EndOfCard|
		--!hrule7|~~~
		--!desc|**Description:** ~SP-DESCRIPTION$
	}}

### Thunderwave
	!power {{
		--replaceattrs|S-|@{selected|character_id}
		--replaceattrs|T-|@{target|character_id}
		--replacespell|@{selected|character_id}|Thunderwave
		--titlefontshadow|none
		--title|School: ~SP-SCHOOL$ ^^ Level: ~SP-LEVEL$ ^^ Components: V,S ^^ Duration: Instantaneous ^^ ~SP-ATHIGHER$
		--name|~SP-NAME$
		--leftsub|~SP-OUTPUT$
		--rightsub|Range: ~SP-RANGE$
		--tokenid|@{selected|token_id}
		--target_list|@{target|token_id}
		--emote|~S-CN$ focuses dark energies into a wave of death
		--hroll|[[ [$sLvl] ?{Cast at:|Level 1,1|Level 2,2|Level 3,3|Level 4,4|Level 5,5|Level 6,6|Level 7,7|Level 8,8|Level 9,9} + 0d0 ]]
		--hroll|[[ [$Hexed] ?{Apply Hex?|No, 0|Yes, 1} + 0d0 ]]
		--Spell Cast at:|Level ?{Cast at:}
		--Spell Save:|DC~S-SSDC$ vs ~SP-SAVE$
		--$saveroll|[#[ [$save] 1d20 + ~T-SBCON$ ]#]
		--?? $Hexed == 0 ?? Hex Applied:|No
		--?? $Hexed == 1 ?? Hex Applied:|Yes
		--?? $save.total < @{selected|spell_save_dc} ?? skipto*1|Hit
		--?? $save.total >= @{selected|spell_save_dc} ?? skipto*2|Saved

		--:Hit|
		--!hrule1|~~~
		--!ht|~T-CN$ take the full force of your attack!
		--?? ?{Cast at:} == 1 AND $Hexed == 0 ?? skipto*3|Lvl1Hit
		--?+ ?{Cast at:} == 1 AND $Hexed == 1 +? skipto*4|Lvl1HitHex
		--?+ ?{Cast at:} == 2 AND $Hexed == 0 +? skipto*5|Lvl2Hit
		--?+ ?{Cast at:} == 2 AND $Hexed == 1 +? skipto*6|Lvl2HitHex
		--?+ ?{Cast at:} == 3 AND $Hexed == 0 +? skipto*7|Lvl3Hit
		--?+ ?{Cast at:} == 3 AND $Hexed == 1 +? skipto*8|Lvl3HitHex
		--?+ ?{Cast at:} == 4 AND $Hexed == 0 +? skipto*9|Lvl4Hit
		--?+ ?{Cast at:} == 4 AND $Hexed == 1 +? skipto*10|Lvl4HitHex
		--?+ ?{Cast at:} == 5 AND $Hexed == 0 +? skipto*11|Lvl5Hit
		--?+ ?{Cast at:} == 5 AND $Hexed == 1 +? skipto*12|Lvl5HitHex
		--?+ ?{Cast at:} == 6 AND $Hexed == 0 +? skipto*13|Lvl6Hit
		--?+ ?{Cast at:} == 6 AND $Hexed == 1 +? skipto*14|Lvl6HitHex
		--?+ ?{Cast at:} == 7 AND $Hexed == 0 +? skipto*15|Lvl7Hit
		--?+ ?{Cast at:} == 7 AND $Hexed == 1 +? skipto*16|Lvl7HitHex
		--?+ ?{Cast at:} == 8 AND $Hexed == 0 +? skipto*17|Lvl8Hit
		--?+ ?{Cast at:} == 8 AND $Hexed == 1 +? skipto*18|Lvl8HitHex
		--?+ ?{Cast at:} == 9 AND $Hexed == 0 +? skipto*19|Lvl9Hit
		--?+ ?{Cast at:} == 9 AND $Hexed == 1 +? skipto*20|Lvl9HitHex

		--:Lvl1Hit|
		--Damage: *1|[#[ [$dmg1] ~SP-DAMAGE$ ]#] points of //~SP-DAMAGETYPE$// damage! 
		--alterbar1|_target|@{target|token_id} _bar|1 _amount|-[^dmg1.total] _show|all
		--skipto*21|EndOfCard

		--:Lvl1HitHex|
		--Damage: *2|[#[ [$dmg2] ~SP-DAMAGE$ + 1d6[Hex] ]#] points of //~SP-DAMAGETYPE$/Necrotic// damage!
		--alterbar2|_target|@{target|token_id} _bar|1 _amount|-[^dmg2.total] _show|all
		--skipto*22|EndOfCard

		--:Lvl2Hit|
		--Damage: *3|[#[ [$dmg3] ~SP-DAMAGE$ + 1d8[Lvl2] ]#] points of //~SP-DAMAGETYPE$// damage!
		--alterbar3|_target|@{target|token_id} _bar|1 _amount|-[^dmg3.total] _show|all
		--skipto*23|EndOfCard

		--:Lvl2HitHex|
		--Damage: *4|[#[ [$dmg4] ~SP-DAMAGE$ + 1d8[Lvl2] + 1d6[Hex] ]#] points of //~SP-DAMAGETYPE$/Necrotic// damage!
		--alterbar4|_target|@{target|token_id} _bar|1 _amount|-[^dmg4.total] _show|all
		--skipto*24|EndOfCard

		--:Lvl3Hit|
		--Damage: *5|[#[ [$dmg5] ~SP-DAMAGE$ + 2d8[Lvl3] ]#] points of //~SP-DAMAGETYPE$// damage!
		--alterbar5|_target|@{target|token_id} _bar|1 _amount|-[^dmg5.total] _show|all
		--skipto*25|EndOfCard

		--:Lvl3HitHex|
		--Damage: *6|[#[ [$dmg6] ~SP-DAMAGE$ + 2d8[Lvl3] + 1d6[Hex] ]#] points of //~SP-DAMAGETYPE$/Necrotic// damage!
		--alterbar6|_target|@{target|token_id} _bar|1 _amount|-[^dmg6.total] _show|all
		--skipto*26|EndOfCard

		--:Lvl4Hit|
		--Damage: *7|[#[ [$dmg7] ~SP-DAMAGE$ + 3d8[Lvl4] ]#] points of //~SP-DAMAGETYPE$// damage!
		--alterbar7|_target|@{target|token_id} _bar|1 _amount|-[^dmg7.total] _show|all
		--skipto*27|EndOfCard

		--:Lvl4HitHex|
		--Damage: *8|[#[ [$dmg8] ~SP-DAMAGE$ + 3d8[Lvl4] + 1d6[Hex] ]#] points of //~SP-DAMAGETYPE$/Necrotic// damage!
		--alterbar8|_target|@{target|token_id} _bar|1 _amount|-[^dmg8.total] _show|all
		--skipto*28|EndOfCard

		--:Lvl5Hit|
		--Damage: *9|[#[ [$dmg9] ~SP-DAMAGE$ + 4d8[Lvl5] ]#] points of //~SP-DAMAGETYPE$// damage!
		--alterbar9|_target|@{target|token_id} _bar|1 _amount|-[^dmg9.total] _show|all
		--skipto*29|EndOfCard

		--:Lvl5HitHex|
		--Damage: *10|[#[ [$dmg10] ~SP-DAMAGE$ + 4d8[Lvl5] + 1d6[Hex] ]#] points of //~SP-DAMAGETYPE$/Necrotic// damage!
		--alterbar10|_target|@{target|token_id} _bar|1 _amount|-[^dmg10.total] _show|all
		--skipto*30|EndOfCard

		--:Lvl6Hit|
		--Damage: *11|[#[ [$dmg11] ~SP-DAMAGE$ + 5d8[Lvl6] ]#] points of //~SP-DAMAGETYPE$// damage!
		--alterbar11|_target|@{target|token_id} _bar|1 _amount|-[^dmg11.total] _show|all
		--skipto*31|EndOfCard

		--:Lvl6HitHex|
		--Damage: *12|[#[ [$dmg12] ~SP-DAMAGE$ + 5d8[Lvl6] + 1d6[Hex] ]#] points of //~SP-DAMAGETYPE$/Necrotic// damage!
		--alterbar12|_target|@{target|token_id} _bar|1 _amount|-[^dmg12.total] _show|all
		--skipto*32|EndOfCard

		--:Lvl7Hit|
		--Damage: *13|[#[ [$dmg13] ~SP-DAMAGE$ + 6d8[Lvl7] ]#] points of //~SP-DAMAGETYPE$// damage!
		--alterbar13|_target|@{target|token_id} _bar|1 _amount|-[^dmg13.total] _show|all
		--skipto*33|EndOfCard

		--:Lvl7HitHex|
		--Damage: *14|[#[ [$dmg14] ~SP-DAMAGE$ + 6d8[Lvl7] + 1d6[Hex] ]#] points of //~SP-DAMAGETYPE$/Necrotic// damage!
		--alterbar14|_target|@{target|token_id} _bar|1 _amount|-[^dmg14.total] _show|all
		--skipto*34|EndOfCard

		--:Lvl8Hit|
		--Damage: *15|[#[ [$dmg15] ~SP-DAMAGE$ + 7d8[Lvl8] ]#] points of //~SP-DAMAGETYPE$// damage!
		--alterbar15|_target|@{target|token_id} _bar|1 _amount|-[^dmg15.total] _show|all
		--skipto*35|EndOfCard

		--:Lvl8HitHex|
		--Damage: *16|[#[ [$dmg16] ~SP-DAMAGE$ + 7d8[Lvl8] + 1d6[Hex] ]#] points of //~SP-DAMAGETYPE$/Necrotic// damage!
		--alterbar16|_target|@{target|token_id} _bar|1 _amount|-[^dmg16.total] _show|all
		--skipto*36|EndOfCard

		--:Lvl9Hit|
		--Damage: *17|[#[ [$dmg17] ~SP-DAMAGE$ + 8d8[Lvl9] ]#] points of //~SP-DAMAGETYPE$// damage!
		--alterbar17|_target|@{target|token_id} _bar|1 _amount|-[^dmg17.total] _show|all
		--skipto*37|EndOfCard

		--:Lvl9HitHex|
		--Damage: *18|[#[ [$dmg18] ~SP-DAMAGE$ + 8d8[Lvl9] + 1d6[Hex] ]#] points of //~SP-DAMAGETYPE$/Necrotic// damage!
		--alterbar18|_target|@{target|token_id} _bar|1 _amount|-[^dmg18.total] _show|all
		--skipto*38|EndOfCard

		--:Saved|
		--!hrule2|~~~
		--!sav|~T-CN$ dodges your attack and takes half damage.
		--?? ?{Cast at:} == 1 AND $Hexed == 0 ?? skipto*39|Lvl1Save
		--?+ ?{Cast at:} == 1 AND $Hexed == 1 +? skipto*40|Lvl1SaveHex
		--?+ ?{Cast at:} == 2 AND $Hexed == 0 +? skipto*41|Lvl2Save
		--?+ ?{Cast at:} == 2 AND $Hexed == 1 +? skipto*42|Lvl2SaveHex
		--?+ ?{Cast at:} == 3 AND $Hexed == 0 +? skipto*43|Lvl3Save
		--?+ ?{Cast at:} == 3 AND $Hexed == 1 +? skipto*44|Lvl3SaveHex
		--?+ ?{Cast at:} == 4 AND $Hexed == 0 +? skipto*45|Lvl4Save
		--?+ ?{Cast at:} == 4 AND $Hexed == 1 +? skipto*46|Lvl4SaveHex
		--?+ ?{Cast at:} == 5 AND $Hexed == 0 +? skipto*47|Lvl5Save
		--?+ ?{Cast at:} == 5 AND $Hexed == 1 +? skipto*48|Lvl5SaveHex
		--?+ ?{Cast at:} == 6 AND $Hexed == 0 +? skipto*49|Lvl6Save
		--?+ ?{Cast at:} == 6 AND $Hexed == 1 +? skipto*50|Lvl6SaveHex
		--?+ ?{Cast at:} == 7 AND $Hexed == 0 +? skipto*51|Lvl7Save
		--?+ ?{Cast at:} == 7 AND $Hexed == 1 +? skipto*52|Lvl7SaveHex
		--?+ ?{Cast at:} == 8 AND $Hexed == 0 +? skipto*53|Lvl8Save
		--?+ ?{Cast at:} == 8 AND $Hexed == 1 +? skipto*54|Lvl8SaveHex
		--?+ ?{Cast at:} == 9 AND $Hexed == 0 +? skipto*55|Lvl9Save
		--?+ ?{Cast at:} == 9 AND $Hexed == 1 +? skipto*56|Lvl9SaveHex

		--:Lvl1Save|
		--Damage: *19|[#[ [$dmg19] round(~SP-DAMAGE$ / 2) ]#] points of //~SP-DAMAGETYPE$// damage!
		--alterbar19|_target|@{target|token_id} _bar|1 _amount|-[^dmg19.total] _show|all
		--skipto*57|EndOfCard

		--:Lvl1SaveHex|
		--Damage: *20|[#[ [$dmg20] round(~SP-DAMAGE$ / 2) + 1d6[Hex] ]#] points of //~SP-DAMAGETYPE$/Necrotic// damage!
		--alterbar20|_target|@{target|token_id} _bar|1 _amount|-[^dmg20.total] _show|all
		--skipto*58|EndOfCard

		--:Lvl2Save|
		--Damage: *21|[#[ [$dmg21] round((~SP-DAMAGE$ + 1d8[Lvl2]) / 2) ]#] points of //~SP-DAMAGETYPE$// damage!
		--alterbar21|_target|@{target|token_id} _bar|1 _amount|-[^dmg21.total] _show|all
		--skipto*59|EndOfCard

		--:Lvl2SaveHex|
		--Damage: *22|[#[ [$dmg22] round((~SP-DAMAGE$ + 1d8[Lvl2]) / 2) + 1d6[Hex] ]#] points of //~SP-DAMAGETYPE$/Necrotic// damage!
		--alterbar22|_target|@{target|token_id} _bar|1 _amount|-[^dmg22.total] _show|all
		--skipto*60|EndOfCard

		--:Lvl3Save|
		--Damage: *23|[#[ [$dmg23] round((~SP-DAMAGE$ + 2d8[Lvl3]) / 2) ]#] points of //~SP-DAMAGETYPE$// damage!
		--alterbar23|_target|@{target|token_id} _bar|1 _amount|-[^dmg23.total] _show|all
		--skipto*61|EndOfCard

		--:Lvl3SaveHex|
		--Damage: *24|[#[ [$dmg24] round((~SP-DAMAGE$ + 2d8[Lvl3]) / 2) + 1d6[Hex] ]#] points of //~SP-DAMAGETYPE$/Necrotic// damage!
		--alterbar24|_target|@{target|token_id} _bar|1 _amount|-[^dmg24.total] _show|all
		--skipto*62|EndOfCard

		--:Lvl4Save|
		--Damage: *25|[#[ [$dmg25] round((~SP-DAMAGE$ + 3d8[Lvl4]) / 2) ]#] points of //~SP-DAMAGETYPE$// damage!
		--alterbar25|_target|@{target|token_id} _bar|1 _amount|-[^dmg25.total] _show|all
		--skipto*63|EndOfCard

		--:Lvl4SaveHex|
		--Damage: *26|[#[ [$dmg26] round((~SP-DAMAGE$ + 3d8[Lvl4]) / 2) + 1d6[Hex] ]#] points of //~SP-DAMAGETYPE$/Necrotic// damage!
		--alterbar26|_target|@{target|token_id} _bar|1 _amount|-[^dmg26.total] _show|all
		--skipto*64|EndOfCard

		--:Lvl5Save|
		--Damage: *27|[#[ [$dmg27] round((~SP-DAMAGE$ + 4d8[Lvl5]) / 2) ]#] points of //~SP-DAMAGETYPE$// damage!
		--alterbar27|_target|@{target|token_id} _bar|1 _amount|-[^dmg27.total] _show|all
		--skipto*65|EndOfCard

		--:Lvl5SaveHex|
		--Damage: *28|[#[ [$dmg28] round((~SP-DAMAGE$ + 4d8[Lvl5]) / 2) + 1d6[Hex] ]#] points of //~SP-DAMAGETYPE$/Necrotic// damage!
		--alterbar28|_target|@{target|token_id} _bar|1 _amount|-[^dmg28.total] _show|all
		--skipto*66|EndOfCard

		--:Lvl6Save|
		--Damage: *29|[#[ [$dmg29] round((~SP-DAMAGE$ + 5d8[Lvl6]) / 2) ]#] points of //~SP-DAMAGETYPE$// damage!
		--alterbar29|_target|@{target|token_id} _bar|1 _amount|-[^dmg29.total] _show|all
		--skipto*67|EndOfCard

		--:Lvl6SaveHex|
		--Damage: *30|[#[ [$dmg30] round((~SP-DAMAGE$ + 5d8[Lvl6]) / 2) + 1d6[Hex] ]#] points of //~SP-DAMAGETYPE$/Necrotic// damage!
		--alterbar30|_target|@{target|token_id} _bar|1 _amount|-[^dmg30.total] _show|all
		--skipto*68|EndOfCard

		--:Lvl7Save|
		--Damage: *31|[#[ [$dmg31] round((~SP-DAMAGE$ + 6d8[Lvl7]) / 2) ]#] points of //~SP-DAMAGETYPE$// damage!
		--alterbar31|_target|@{target|token_id} _bar|1 _amount|-[^dmg31.total] _show|all
		--skipto*69|EndOfCard

		--:Lvl7SaveHex|
		--Damage: *32|[#[ [$dmg32] round((~SP-DAMAGE$ + 6d8[Lvl7]) / 2) + 1d6[Hex] ]#] points of //~SP-DAMAGETYPE$/Necrotic// damage!
		--alterbar32|_target|@{target|token_id} _bar|1 _amount|-[^dmg32.total] _show|all
		--skipto*70|EndOfCard

		--:Lvl8Save|
		--Damage: *33|[#[ [$dmg33] round((~SP-DAMAGE$ + 7d8[Lvl8]) / 2) ]#] points of //~SP-DAMAGETYPE$// damage!
		--alterbar33|_target|@{target|token_id} _bar|1 _amount|-[^dmg33.total] _show|all
		--skipto*71|EndOfCard

		--:Lvl8SaveHex|
		--Damage: *34|[#[ [$dmg34] round((~SP-DAMAGE$ + 7d8[Lvl8]) / 2) + 1d6[Hex] ]#] points of //~SP-DAMAGETYPE$/Necrotic// damage!
		--alterbar34|_target|@{target|token_id} _bar|1 _amount|-[^dmg34.total] _show|all
		--skipto*72|EndOfCard

		--:Lvl9Save|
		--Damage: *35|[#[ [$dmg35] round((~SP-DAMAGE$ + 8d8[Lvl9]) / 2) ]#] points of //~SP-DAMAGETYPE$// damage!
		--alterbar35|_target|@{target|token_id} _bar|1 _amount|-[^dmg35.total] _show|all
		--skipto*73|EndOfCard

		--:Lvl9SaveHex|
		--Damage: *36|[#[ [$dmg36] round((~SP-DAMAGE$ + 8d8[Lvl9]) / 2) + 1d6[Hex] ]#] points of //~SP-DAMAGETYPE$/Necrotic// damage!
		--alterbar36|_target|@{target|token_id} _bar|1 _amount|-[^dmg36.total] _show|all 

		--:EndOfCard|
		--!hrule3|~~~
		--!desc|**Description:** ~SP-DESCRIPTION$
	
	}}

### Shatter
	!power {{
		--replaceattrs|S-|@{selected|character_id}
		--replaceattrs|T-|@{target|character_id}
		--replacespell|@{selected|character_id}|Shatter
		--titlefontshadow|none
		--title|School: ~SP-SCHOOL$ ^^ Level: ~SP-LEVEL$ ^^ Components: V,S,M A chip of mica ^^ Duration: Instantaneous ^^ ~SP-ATHIGHER$
		--name|~SP-NAME$
		--leftsub|~SP-OUTPUT$
		--rightsub|Range: ~SP-RANGE$
		--tokenid|@{selected|token_id}
		--target_list|@{target|token_id}
		--emote|~S-CN$ focuses dark energies into a sphere of destruction
		--hroll|[[ [$sLvl] ?{Cast at:|Level 2,2|Level 3,3|Level 4,4|Level 5,5|Level 6,6|Level 7,7|Level 8,8|Level 9,9} + 0d0 ]]
		--hroll|[[ [$Hexed] ?{Apply Hex?|No, 0|Yes, 1} + 0d0 ]]
		--Spell Cast at:|Level ?{Cast at:}
		--Spell Save:|DC~S-SSDC$ vs ~SP-SAVE$
		--$saveroll|[#[ [$save] 1d20 + ~T-SBCON$ ]#]
		--?? $Hexed == 0 ?? Hex Applied:|No
		--?? $Hexed == 1 ?? Hex Applied:|Yes
		--?? $save.total < @{selected|spell_save_dc} ?? skipto*1|Hit
		--?? $save.total >= @{selected|spell_save_dc} ?? skipto*2|Saved

		--:Hit|
		--!hrule1|~~~
		--!ht|~T-CN$ take the full force of your attack!
		--?? ?{Cast at:} == 2 AND $Hexed == 0 ?? skipto*3|Lvl2Hit
		--?+ ?{Cast at:} == 2 AND $Hexed == 1 +? skipto*4|Lvl2HitHex
		--?+ ?{Cast at:} == 3 AND $Hexed == 0 +? skipto*5|Lvl3Hit
		--?+ ?{Cast at:} == 3 AND $Hexed == 1 +? skipto*6|Lvl3HitHex
		--?+ ?{Cast at:} == 4 AND $Hexed == 0 +? skipto*7|Lvl4Hit
		--?+ ?{Cast at:} == 4 AND $Hexed == 1 +? skipto*8|Lvl4HitHex
		--?+ ?{Cast at:} == 5 AND $Hexed == 0 +? skipto*9|Lvl5Hit
		--?+ ?{Cast at:} == 5 AND $Hexed == 1 +? skipto*10|Lvl5HitHex
		--?+ ?{Cast at:} == 6 AND $Hexed == 0 +? skipto*11|Lvl6Hit
		--?+ ?{Cast at:} == 6 AND $Hexed == 1 +? skipto*12|Lvl6HitHex
		--?+ ?{Cast at:} == 7 AND $Hexed == 0 +? skipto*13|Lvl7Hit
		--?+ ?{Cast at:} == 7 AND $Hexed == 1 +? skipto*14|Lvl7HitHex
		--?+ ?{Cast at:} == 8 AND $Hexed == 0 +? skipto*15|Lvl8Hit
		--?+ ?{Cast at:} == 8 AND $Hexed == 1 +? skipto*16|Lvl8HitHex
		--?+ ?{Cast at:} == 9 AND $Hexed == 0 +? skipto*17|Lvl9Hit
		--?+ ?{Cast at:} == 9 AND $Hexed == 1 +? skipto*18|Lvl9HitHex

		--:Lvl2Hit|
		--Damage: *1|[#[ [$dmg1] ~SP-DAMAGE$ ]#] points of //~SP-DAMAGETYPE$// damage! 
		--alterbar1|_target|@{target|token_id} _bar|1 _amount|-[^dmg1.total] _show|all
		--skipto*19|EndOfCard

		--:Lvl2HitHex|
		--Damage: *2|[#[ [$dmg2] ~SP-DAMAGE$ + 1d6[Hex] ]#] points of //~SP-DAMAGETYPE$/Necrotic// damage!
		--alterbar2|_target|@{target|token_id} _bar|1 _amount|-[^dmg2.total] _show|all
		--skipto*20|EndOfCard

		--:Lvl3Hit|
		--Damage: *3|[#[ [$dmg3] ~SP-DAMAGE$ + 1d8[Lvl3] ]#] points of //~SP-DAMAGETYPE$// damage!
		--alterbar3|_target|@{target|token_id} _bar|1 _amount|-[^dmg3.total] _show|all
		--skipto*21|EndOfCard

		--:Lvl3HitHex|
		--Damage: *4|[#[ [$dmg4] ~SP-DAMAGE$ + 1d8[Lvl3] + 1d6[Hex] ]#] points of //~SP-DAMAGETYPE$/Necrotic// damage!
		--alterbar4|_target|@{target|token_id} _bar|1 _amount|-[^dmg4.total] _show|all
		--skipto*22|EndOfCard

		--:Lvl4Hit|
		--Damage: *5|[#[ [$dmg5] ~SP-DAMAGE$ + 2d8[Lvl4] ]#] points of //~SP-DAMAGETYPE$// damage!
		--alterbar5|_target|@{target|token_id} _bar|1 _amount|-[^dmg5.total] _show|all
		--skipto*23|EndOfCard

		--:Lvl4HitHex|
		--Damage: *6|[#[ [$dmg6] ~SP-DAMAGE$ + 2d8[Lvl4] + 1d6[Hex] ]#] points of //~SP-DAMAGETYPE$/Necrotic// damage!
		--alterbar6|_target|@{target|token_id} _bar|1 _amount|-[^dmg6.total] _show|all
		--skipto*24|EndOfCard

		--:Lvl5Hit|
		--Damage: *7|[#[ [$dmg7] ~SP-DAMAGE$ + 3d8[Lvl5] ]#] points of //~SP-DAMAGETYPE$// damage!
		--alterbar7|_target|@{target|token_id} _bar|1 _amount|-[^dmg7.total] _show|all
		--skipto*25|EndOfCard

		--:Lvl5HitHex|
		--Damage: *8|[#[ [$dmg8] ~SP-DAMAGE$ + 3d8[Lvl5] + 1d6[Hex] ]#] points of //~SP-DAMAGETYPE$/Necrotic// damage!
		--alterbar8|_target|@{target|token_id} _bar|1 _amount|-[^dmg8.total] _show|all
		--skipto*26|EndOfCard

		--:Lvl6Hit|
		--Damage: *9|[#[ [$dmg9] ~SP-DAMAGE$ + 4d8[Lvl6] ]#] points of //~SP-DAMAGETYPE$// damage!
		--alterbar9|_target|@{target|token_id} _bar|1 _amount|-[^dmg9.total] _show|all
		--skipto*27|EndOfCard

		--:Lvl6HitHex|
		--Damage: *10|[#[ [$dmg10] ~SP-DAMAGE$ + 4d8[Lvl6] + 1d6[Hex] ]#] points of //~SP-DAMAGETYPE$/Necrotic// damage!
		--alterbar10|_target|@{target|token_id} _bar|1 _amount|-[^dmg10.total] _show|all
		--skipto*28|EndOfCard

		--:Lvl7Hit|
		--Damage: *11|[#[ [$dmg11] ~SP-DAMAGE$ + 5d8[Lvl7] ]#] points of //~SP-DAMAGETYPE$// damage!
		--alterbar11|_target|@{target|token_id} _bar|1 _amount|-[^dmg11.total] _show|all
		--skipto*29|EndOfCard

		--:Lvl7HitHex|
		--Damage: *12|[#[ [$dmg12] ~SP-DAMAGE$ + 5d8[Lvl7] + 1d6[Hex] ]#] points of //~SP-DAMAGETYPE$/Necrotic// damage!
		--alterbar12|_target|@{target|token_id} _bar|1 _amount|-[^dmg12.total] _show|all
		--skipto*30|EndOfCard

		--:Lvl8Hit|
		--Damage: *13|[#[ [$dmg13] ~SP-DAMAGE$ + 6d8[Lvl8] ]#] points of //~SP-DAMAGETYPE$// damage!
		--alterbar13|_target|@{target|token_id} _bar|1 _amount|-[^dmg13.total] _show|all
		--skipto*31|EndOfCard

		--:Lvl8HitHex|
		--Damage: *14|[#[ [$dmg14] ~SP-DAMAGE$ + 6d8[Lvl8] + 1d6[Hex] ]#] points of //~SP-DAMAGETYPE$/Necrotic// damage!
		--alterbar14|_target|@{target|token_id} _bar|1 _amount|-[^dmg14.total] _show|all
		--skipto*32|EndOfCard

		--:Lvl9Hit|
		--Damage: *15|[#[ [$dmg15] ~SP-DAMAGE$ + 7d8[Lvl9] ]#] points of //~SP-DAMAGETYPE$// damage!
		--alterbar15|_target|@{target|token_id} _bar|1 _amount|-[^dmg15.total] _show|all
		--skipto*33|EndOfCard

		--:Lvl9HitHex|
		--Damage: *16|[#[ [$dmg16] ~SP-DAMAGE$ + 7d8[Lvl9] + 1d6[Hex] ]#] points of //~SP-DAMAGETYPE$/Necrotic// damage!
		--alterbar16|_target|@{target|token_id} _bar|1 _amount|-[^dmg16.total] _show|all
		--skipto*34EndOfCard

		--:Saved|
		--!hrule2|~~~
		--!sav|~T-CN$ dodges your attack and takes half damage.
		--?? ?{Cast at:} == 2 AND $Hexed == 0 ?? skipto*35|Lvl2Save
		--?+ ?{Cast at:} == 2 AND $Hexed == 1 +? skipto*36|Lvl2SaveHex
		--?+ ?{Cast at:} == 3 AND $Hexed == 0 +? skipto*37|Lvl3Save
		--?+ ?{Cast at:} == 3 AND $Hexed == 1 +? skipto*38|Lvl3SaveHex
		--?+ ?{Cast at:} == 4 AND $Hexed == 0 +? skipto*39|Lvl4Save
		--?+ ?{Cast at:} == 4 AND $Hexed == 1 +? skipto*40|Lvl4SaveHex
		--?+ ?{Cast at:} == 5 AND $Hexed == 0 +? skipto*41|Lvl5Save
		--?+ ?{Cast at:} == 5 AND $Hexed == 1 +? skipto*42|Lvl5SaveHex
		--?+ ?{Cast at:} == 6 AND $Hexed == 0 +? skipto*43|Lvl6Save
		--?+ ?{Cast at:} == 6 AND $Hexed == 1 +? skipto*44|Lvl6SaveHex
		--?+ ?{Cast at:} == 7 AND $Hexed == 0 +? skipto*45|Lvl7Save
		--?+ ?{Cast at:} == 7 AND $Hexed == 1 +? skipto*46|Lvl7SaveHex
		--?+ ?{Cast at:} == 8 AND $Hexed == 0 +? skipto*47|Lvl8Save
		--?+ ?{Cast at:} == 8 AND $Hexed == 1 +? skipto*48|Lvl8SaveHex
		--?+ ?{Cast at:} == 9 AND $Hexed == 0 +? skipto*49|Lvl9Save
		--?+ ?{Cast at:} == 9 AND $Hexed == 1 +? skipto*50|Lvl9SaveHex


		--:Lvl2Save|
		--Damage: *17|[#[ [$dmg17] round(~SP-DAMAGE$ / 2) ]#] points of //~SP-DAMAGETYPE$// damage!
		--alterbar17|_target|@{target|token_id} _bar|1 _amount|-[^dmg17.total] _show|all
		--skipto*51|EndOfCard

		--:Lvl2SaveHex|
		--Damage: *18|[#[ [$dmg18] round(~SP-DAMAGE$ / 2) + 1d6[Hex] ]#] points of //~SP-DAMAGETYPE$/Necrotic// damage!
		--alterbar18|_target|@{target|token_id} _bar|1 _amount|-[^dmg18.total] _show|all
		--skipto*52|EndOfCard

		--:Lvl3Save|
		--Damage: *19|[#[ [$dmg19] round((~SP-DAMAGE$ + 1d8[Lvl3]) / 2) ]#] points of //~SP-DAMAGETYPE$// damage!
		--alterbar19|_target|@{target|token_id} _bar|1 _amount|-[^dmg19.total] _show|all
		--skipto*53|EndOfCard

		--:Lvl3SaveHex|
		--Damage: *20|[#[ [$dmg20] round((~SP-DAMAGE$ + 1d8[Lvl3]) / 2) + 1d6[Hex] ]#] points of //~SP-DAMAGETYPE$/Necrotic// damage!
		--alterbar20|_target|@{target|token_id} _bar|1 _amount|-[^dmg20.total] _show|all
		--skipto*54|EndOfCard

		--:Lvl4Save|
		--Damage: *21|[#[ [$dmg21] round((~SP-DAMAGE$ + 2d8[Lvl4]) / 2) ]#] points of //~SP-DAMAGETYPE$// damage!
		--alterbar21|_target|@{target|token_id} _bar|1 _amount|-[^dmg21.total] _show|all
		--skipto*55|EndOfCard

		--:Lvl4SaveHex|
		--Damage: *22|[#[ [$dmg22] round((~SP-DAMAGE$ + 2d8[Lvl4]) / 2) + 1d6[Hex] ]#] points of //~SP-DAMAGETYPE$/Necrotic// damage!
		--alterbar22|_target|@{target|token_id} _bar|1 _amount|-[^dmg22.total] _show|all
		--skipto*56|EndOfCard

		--:Lvl5Save|
		--Damage: *23|[#[ [$dmg23] round((~SP-DAMAGE$ + 3d8[Lvl5]) / 2) ]#] points of //~SP-DAMAGETYPE$// damage!
		--alterbar23|_target|@{target|token_id} _bar|1 _amount|-[^dmg23.total] _show|all
		--skipto*57|EndOfCard

		--:Lvl5SaveHex|
		--Damage: *24|[#[ [$dmg24] round((~SP-DAMAGE$ + 3d8[Lvl5]) / 2) + 1d6[Hex] ]#] points of //~SP-DAMAGETYPE$/Necrotic// damage!
		--alterbar24|_target|@{target|token_id} _bar|1 _amount|-[^dmg24.total] _show|all
		--skipto*58|EndOfCard

		--:Lvl6Save|
		--Damage: *25|[#[ [$dmg25] round((~SP-DAMAGE$ + 4d8[Lvl6]) / 2) ]#] points of //~SP-DAMAGETYPE$// damage!
		--alterbar25|_target|@{target|token_id} _bar|1 _amount|-[^dmg25.total] _show|all
		--skipto*59|EndOfCard

		--:Lvl6SaveHex|
		--Damage: *26|[#[ [$dmg26] round((~SP-DAMAGE$ + 4d8[Lvl6]) / 2) + 1d6[Hex] ]#] points of //~SP-DAMAGETYPE$/Necrotic// damage!
		--alterbar26|_target|@{target|token_id} _bar|1 _amount|-[^dmg26.total] _show|all
		--skipto*60|EndOfCard

		--:Lvl7Save|
		--Damage: *27|[#[ [$dmg27] round((~SP-DAMAGE$ + 5d8[Lvl7]) / 2) ]#] points of //~SP-DAMAGETYPE$// damage!
		--alterbar27|_target|@{target|token_id} _bar|1 _amount|-[^dmg27.total] _show|all
		--skipto*61|EndOfCard

		--:Lvl7SaveHex|
		--Damage: *28|[#[ [$dmg28] round((~SP-DAMAGE$ + 5d8[Lvl7]) / 2) + 1d6[Hex] ]#] points of //~SP-DAMAGETYPE$/Necrotic// damage!
		--alterbar28|_target|@{target|token_id} _bar|1 _amount|-[^dmg28.total] _show|all
		--skipto*62|EndOfCard

		--:Lvl8Save|
		--Damage: *29|[#[ [$dmg29] round((~SP-DAMAGE$ + 6d8[Lvl8]) / 2) ]#] points of //~SP-DAMAGETYPE$// damage!
		--alterbar29|_target|@{target|token_id} _bar|1 _amount|-[^dmg29.total] _show|all
		--skipto*63|EndOfCard

		--:Lvl8SaveHex|
		--Damage: *30|[#[ [$dmg30] round((~SP-DAMAGE$ + 6d8[Lvl8]) / 2) + 1d6[Hex] ]#] points of //~SP-DAMAGETYPE$/Necrotic// damage!
		--alterbar30|_target|@{target|token_id} _bar|1 _amount|-[^dmg30.total] _show|all
		--skipto*64|EndOfCard

		--:Lvl9Save|
		--Damage: *31|[#[ [$dmg31] round((~SP-DAMAGE$ + 7d8[Lvl9]) / 2) ]#] points of //~SP-DAMAGETYPE$// damage!
		--alterbar31|_target|@{target|token_id} _bar|1 _amount|-[^dmg31.total] _show|all
		--skipto*65|EndOfCard

		--:Lvl9SaveHex|
		--Damage: *32|[#[ [$dmg32] round((~SP-DAMAGE$ + 7d8[Lvl9]) / 2) + 1d6[Hex] ]#] points of //~SP-DAMAGETYPE$/Necrotic// damage!
		--alterbar32|_target|@{target|token_id} _bar|1 _amount|-[^dmg32.total] _show|all

		--:EndOfCard|
		--!hrule3|~~~
		--!desc|**Description:** ~SP-DESCRIPTION$
	
	}}

### Armor of Agathys
	!power {{
		--replaceattrs|S-|@{selected|character_id}
		--replacespell|@{selected|character_id}|Armor of Agathys
		--titlefontshadow|none
		--title|School: ~SP-SCHOOL$ ^^ Level: ~SP-LEVEL$ ^^ Components: V,S,M, A cup of water ^^ Duration: 1 hour
		--name|~SP-NAME$
		--leftsub|~SP-OUTPUT$
		--rightsub|Range: ~SP-RANGE$
		--tokenid|@{selected|token_id}
		--emote|~S-CN$ weaves a magical force of enegry that reinforces their health.
		--hroll|[[ [$sLvl] ?{Cast at:|Level 1,1|Level 2,2|Level 3,3|Level 4,4|Level 5,5|Level 6,6|Level 7,7|Level 8,8|Level 9,9} + 0d0 ]]
		--Spell Cast at:|Level ?{Cast at:}

		--!hrule1|~~~
		--Spell Effect: *1|~S-CN$ has gained [[ [$heal] 5 * ?{Cast at:} ]] temporary hit points.
		--alterbar1|_target|@{selected|token_id} _bar|3 _amount|+[^heal] _show|none

		--:EndOfCard|
		--!hrule2|~~~
		--!desc|**Description:** ~SP-DESCRIPTION$
		--!hdesc|**At Higher Levels:** ~SP-ATHIGHER$
	}}

## Melee
	!power {{
		--replaceattrs|S-|@{selected|character_id}
		--replaceattrs|T-|@{target|character_id}
		--replacesection|@{selected|character_id}|Dagger|attack|atkname|PCA-
		--replacespell|@{selected|character_id}|Hex
		--titlefontshadow|none
		--name|~PCA-atkname$
		--leftsub|Melee/Ranged Attack
		--rightsub|Range:~PCA-atkrange$
		--tokenid|@{selected|token_id}
		--target_list|@{target|token_id}
		--emote|~S-CN$ attacks ~T-CN$
		--Critical Range:|@{selected|default_critical_range}+
		--Attack:|[[ [$Atk] ?{Attack|Standard,1d20|Advantage,2d20kh1|Disadvantage,2d20kl1} + ~S-MDEX$[DEX] + @{selected|pb}[PROF] ]] vs AC
		--hroll|[[ [$Hexed] ?{Apply Hex?|No, 0|Yes, 1} + 0d0 ]]
		--?? $Atk.base >= @{selected|default_critical_range} ?? skipto*1|Critical
		--?? $Atk.base == 1 ?? skipto*2|Fumble
		--?? $Atk.total >= @{target|npc_ac} ?? skipto*3|Hit

		--:Miss| Since we didn't skip to anywhere else, assume a miss
		--!hrule1|~~~
		--Miss:|Your attack missed.
		--skipto*4|EndOfCard

		--:Fumble|
		--!hrule2|~~~
		--Fumble:|OMG! WTF Happened?!
		--api_fumble|
		--skipto*5|EndOfCard

		--:Hit|
		--?? $Hexed == 0 ?? skipto*6|HitDmg
		--?? $Hexed == 1 ?? skipto*7|HitDmgHex

		--:HitDmg|
		--!hrule3|~~~
		--Hit: *1|Your attack hits for [#[ [$dmg1] ~PCA-dmgbase$ + ~S-MDEX$[DEX] ]#] points of //~PCA-dmgtype$// damage!
		--alterbar1|_target|@{target|token_id} _bar|1 _amount|-[^dmg1.total] _show|all
		--skipto*8|EndOfCard

		--:HitDmgHex|
		--Cursed (HEX): *1|I can smell death emanating from those wounds.
		--!hrule4|~~~
		--Hit: *2|Your attack hits for [#[ [$dmg2] (~PCA-dmgbase$ + ~S-MDEX$[DEX]) + @{selected|repeating_damagemod_$0_global_damage_damage}[Hex] ]#] points of //~PCA-dmgtype$// and //~SP-DAMAGETYPE$// damage!
		--alterbar2|_target|@{target|token_id} _bar|1 _amount|-[^dmg2.total] _show|all
		--skipto*9|EndOfCard

		--:Critical|
		--?? $Hexed == 0 ?? skipto*10|CritDmg
		--?? $Hexed == 1 ?? skipto*11|CritDmgHex

		--:CritDmg|
		--!hrule5|~~~
		--Critical Hit: *1|You strike a decisive blow for [#[ [$dmg3] (~PCA-dmgbase$ + ~S-MDEX$[DEX]) + ~PCA-dmgbase$ ]#] points of //~PCA-dmgtype$// damage!
		--alterbar3|_target|@{target|token_id} _bar|1 _amount|-[^dmg3.total] _show|all
		--skipto*10|EndOfCard

		--:CritDmgHex|
		--Cursed (HEX): *2|Oh, this is going to hurt special like!
		--!hrule6|~~~
		--Critical Hit: *2|You strike a decisive blow for [#[ [$dmg4] (~PCA-dmgbase$ + ~S-MDEX$[DEX]) + ~PCA-dmgbase$ + (@{selected|repeating_damagemod_$0_global_damage_damage}[Hex] + @{selected|repeating_damagemod_$0_global_damage_damage}[Hex]) ]#] points of //~PCA-dmgtype$// and //~SP-DAMAGETYPE$// damage!
		--alterbar4|_target|@{target|token_id} _bar|1 _amount|-[^dmg4.total] _show|all

		--:EndOfCard|
	
	}}

## Ranged
	!power {{
		--replaceattrs|S-|@{selected|character_id}
		--replaceattrs|T-|@{target|character_id}
		--replacesection|@{selected|character_id}|Light Crossbow|attack|atkname|PCA-
		--replacespell|@{selected|character_id}|Hex
		--titlefontshadow|none
		--name|~PCA-atkname$
		--leftsub|Melee/Ranged Attack
		--rightsub|Range:~PCA-atkrange$
		--tokenid|@{selected|token_id}
		--target_list|@{target|token_id}
		--emote|~S-CN$ attacks ~T-CN$
		--Critical Range:|@{selected|default_critical_range}+
		--Attack:|[[ [$Atk] ?{Attack|Standard,1d20|Advantage,2d20kh1|Disadvantage,2d20kl1} + ~S-MDEX$[DEX] + @{selected|pb}[PROF] ]] vs AC
		--hroll|[[ [$Hexed] ?{Apply Hex?|No, 0|Yes, 1} + 0d0 ]]
		--?? $Atk.base >= @{selected|default_critical_range} ?? skipto*1|Critical
		--?? $Atk.base == 1 ?? skipto*2|Fumble
		--?? $Atk.total >= @{target|npc_ac} ?? skipto*3|Hit

		--:Miss| Since we didn't skip to anywhere else, assume a miss
		--!hrule1|~~~
		--Miss:|Your attack missed.
		--skipto*4|EndOfCard

		--:Fumble|
		--!hrule2|~~~
		--Fumble:|OMG! WTF Happened?!
		--api_fumble|
		--skipto*5|EndOfCard

		--:Hit|
		--?? $Hexed == 0 ?? skipto*6|HitDmg
		--?? $Hexed == 1 ?? skipto*7|HitDmgHex

		--:HitDmg|
		--!hrule3|~~~
		--Hit: *1|Your attack hits for [#[ [$dmg1] ~PCA-dmgbase$ + ~S-MDEX$[DEX] ]#] points of //~PCA-dmgtype$// damage!
		--alterbar1|_target|@{target|token_id} _bar|1 _amount|-[^dmg1.total] _show|all
		--skipto*8|EndOfCard

		--:HitDmgHex|
		--Cursed (HEX): *1|I can smell death emanating from those wounds.
		--!hrule4|~~~
		--Hit: *2|Your attack hits for [#[ [$dmg2] (~PCA-dmgbase$ + ~S-MDEX$[DEX]) + @{selected|repeating_damagemod_$0_global_damage_damage}[Hex] ]#] points of //~PCA-dmgtype$// and //~SP-DAMAGETYPE$// damage!
		--alterbar2|_target|@{target|token_id} _bar|1 _amount|-[^dmg2.total] _show|all
		--skipto*9|EndOfCard

		--:Critical|
		--?? $Hexed == 0 ?? skipto*10|CritDmg
		--?? $Hexed == 1 ?? skipto*11|CritDmgHex

		--:CritDmg|
		--!hrule5|~~~
		--Critical Hit: *1|You strike a decisive blow for [#[ [$dmg3] (~PCA-dmgbase$ + ~S-MDEX$[DEX]) + ~PCA-dmgbase$ ]#] points of //~PCA-dmgtype$// damage!
		--alterbar3|_target|@{target|token_id} _bar|1 _amount|-[^dmg3.total] _show|all
		--skipto*10|EndOfCard

		--:CritDmgHex|
		--Cursed (HEX): *2|Oh, this is going to hurt special like!
		--!hrule6|~~~
		--Critical Hit: *2|You strike a decisive blow for [#[ [$dmg4] (~PCA-dmgbase$ + ~S-MDEX$[DEX]) + ~PCA-dmgbase$ + (@{selected|repeating_damagemod_$0_global_damage_damage}[Hex] + @{selected|repeating_damagemod_$0_global_damage_damage}[Hex]) ]#] points of //~PCA-dmgtype$// and //~SP-DAMAGETYPE$// damage!
		--alterbar4|_target|@{target|token_id} _bar|1 _amount|-[^dmg4.total] _show|all

		--:EndOfCard|
		
	}}