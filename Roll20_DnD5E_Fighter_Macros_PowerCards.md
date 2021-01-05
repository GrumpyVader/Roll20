# Roll20 D&D 5E Fighter Macros using PowerCards

These macros cover rolls that are specific to 5E Fighter Class characters.

> These macros utilize the [PowerCards API](https://wiki.roll20.net/Script:PowerCards) which requires a Pro account in Roll20. Talk to you game master or the owner of the game session concerning this.

In order to use these macros you must create them either in your character sheet or in the macros list.

## Macro List

On the right hand pain you will see an icon with three lines next to the Settings gear. Click on the Collections icon and this will take you to the list of available Macros. These are macros that should be available to all players.

This create a new macro, just click on the [+Add] button, provide the name you want to call the macro and the paste the macro code in the Actions box. Lastly, if you want the macro to show when you select your token, check on Show as Token Action. This will display a macro button in the top portion of the VTT when ever you select your character token.

If you would prefer to see the macro button along the bottom of the screen, when you save the macro you can check On the In Bar option.

## Character Sheet
When you open your character sheet, along the top you have 3 tabs, one of them being Attributes & Abilities. Click on the Attributes & Abilities tab. In the Abilities section, click on the [+Add] button to create a new macro then move your mouse over the "New Ability 0" and then click on the little pencil icon. This will place you in Edit mode where you can specify the name of the macro and paste the macro code. Once done, click on the Checkmark to save it. Once saved, you can Check On the "Show in Macro Bar" and or "Show as Token Action".

## Weapon Attacks

### Melee

    !power {{
        --replaceattrs|S-|@{selected|character_id}
        --replaceattrs|T-|@{target|character_id}
        --replacesection|@{selected|character_id}|Warhammer (One-Handed)|attack|atkname|PCA-
        --titlefontshadow|none
        --name|~PCA-atkname$
        --leftsub|Melee Attack
        --rightsub|Range:5' Reach
        --tokenid|@{selected|token_id}
        --target_list|@{target|token_id}
        --emote|~S-CN$ attacks ~T-CN$
        --Critical Range:|@{selected|default_critical_range}+
        --Attack:|[[ [$Atk] ?{Attack|Standard,1d20|Advantage,2d20kh1|Disadvantage,2d20kl1} + ~S-MSTR$[STR] + @{selected|pb}[PROF] ]] vs AC
        --?? $Atk.base >= @{selected|default_critical_range} ?? skipto*1|Critical
        --?? $Atk.base == 1 ?? skipto*2|Fumble
        --?? $Atk.total >= @{target|npc_ac} ?? skipto*3|Hit

        --:Miss| Since we didn't skip to anywhere else, assume a miss
        --Miss:|Your attack missed.
        --skipto*4|EndOfCard

        --:Fumble|
        --Fumble:|OMG! WTF Happened?!
        --api_fumble|
        --skipto*5|EndOfCard

        --:Hit|
        --Hit:|Your attack hit for [#[ [$Dmg] ~PCA-dmgbase$ + ~S-MSTR$[STR] ]#] points of //~PCA-dmgtype$// damage!
        --alterbar1|_target|@{target|token_id} _bar|1 _amount|-[^Dmg] _show|all
        --skipto*6|EndOfCard
        
        --:Critical|
        --Critical Hit:|You strike a decisive blow for [#[ [$CritDmg] (~PCA-dmgbase$ + ~S-MSTR$[STR]) + ~PCA-dmgbase$ ]#] points of //~PCA-dmgtype$// damage!
        --alterbar2|_target|@{target|token_id} _bar|1 _amount|-[^CritDmg] _show|all

        --:EndOfCard|
        --?? @{target|bar1} == 0 ?? api_token-mod| _ids @{target|token_id} _ignore-selected _set statusmarkers|dead
    }}

### Ranged

    !power {{
        --replaceattrs|S-|@{selected|character_id}
        --replaceattrs|T-|@{target|character_id}
        --replacesection|@{selected|character_id}|Light Crossbow|attack|atkname|PCA-
        --titlefontshadow|none
        --name|~PCA-atkname$
        --leftsub|Melee/Ranged Attack
        --rightsub|Range:~PCA-atkrange$
        --tokenid|@{selected|token_id}
        --target_list|@{target|token_id}
        --emote|~S-CN$ attacks ~T-CN$
        --Critical Range:|@{selected|default_critical_range}+
        --Attack:|[[ [$Atk] ?{Attack|Standard,1d20|Advantage,2d20kh1|Disadvantage,2d20kl1} + ~S-MSTR$[STR] + @{selected|pb}[PROF] ]] vs AC
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
        --!hrule3|~~~
        --Hit:|Your attack hits for [#[ [$dmg] ~PCA-dmgbase$ + ~S-MSTR$[STR] ]#] points of //~PCA-dmgtype$// damage!
        --alterbar1|_target|@{target|token_id} _bar|1 _amount|-[^dmg.total] _show|all
        --skipto*6|EndOfCard

        --:Critical|
        --!hrule4|~~~
        --Critical Hit:|You strike a decisive blow for [#[ [$CritDmg] (~PCA-dmgbase$ + ~S-MSTR$[STR]) + ~PCA-dmgbase$ ]#] points of //~PCA-dmgtype$// damage!
        --alterbar2|_target|@{target|token_id} _bar|1 _amount|-[^CritDmg.total] _show|all
        --skipto*7|EndOfCard

        --:EndOfCard|
        --?? @{target|bar1} == 0 ?? api_token-mod| _ids @{target|token_id} _ignore-selected _set statusmarkers|dead
    }}

## Traits

### Second Wind

    !power {{
        --replaceattrs|S-|@{selected|character_id}
        --titlefontshadow|none
        --name|@{selected|repeating_traits_$0_name}
        --leftsub|@{selected|repeating_traits_$0_source_type}
        --rightsub|Trait
        --tokenid|@{selected|token_id}
        --emote|The adrenaline of battle fuels the blood of ~S-CN$

        --Heath Restored:|[[ [$SW] 1d10 + ~S-L$[LVL] ]]

        --!hrule1|~~~
        --!TR|**Description:** @{selected|repeating_traits_$0_description}

        --:EndOfCard|
        --alterbar1|_target|@{selected|token_id} _bar|3 _amount|+[^SW.total] _show|none
    
    }}

