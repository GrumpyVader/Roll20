# D&D 5e General PowerCards Macros

These macros cover general rolls that are common to all Roll20 players/characters.

> These macros utilize the [PowerCards API](https://wiki.roll20.net/Script:PowerCards) which requires a Pro account in Roll20. Talk to you game master or the owner of the game session concerning this.

In order to use these macros you must create them either in your character sheet or in the macros list.

## Macro List

On the right hand pain you will see an icon with three lines next to the Settings gear. Click on the Collections icon and this will take you to the list of available Macros. These are macros that should be available to all players.

This create a new macro, just click on the [+Add] button, provide the name you want to call the macro and the paste the macro code in the Actions box. Lastly, if you want the macro to show when you select your token, check on Show as Token Action. This will display a macro button in the top portion of the VTT when ever you select your character token.

If you would prefer to see the macro button along the bottom of the screen, when you save the macro you can check On the In Bar option.

## Character Sheet
When you open your character sheet, along the top you have 3 tabs, one of them being Attributes & Abilities. Click on the Attributes & Abilities tab. In the Abilities section, click on the [+Add] button to create a new macro then move your mouse over the "New Ability 0" and then click on the little pencil icon. This will place you in Edit mode where you can specify the name of the macro and paste the macro code. Once done, click on the Checkmark to save it. Once saved, you can Check On the "Show in Macro Bar" and or "Show as Token Action".

**Table of contents**
[[TOC]]

## Initiative, Death and Fumble Rolls

### Initiative
This macro will take your Initiative Bonus and add it the a 1d20 roll and add your token to the Turn Order panel.

    !power {{
        --titlefontshadow|none
        --name|Initiative
        --tokenid|@{selected|token_id}
        --emote|@{selected|character_name} prepares for battle ...
        --Roll:|[[ [NH|TRKR] 1d20 + @{selected|initiative_bonus}[INIT] ]]
    }}


### Death Save

    !power {{
        --titlefontshadow|none
        --name|Death Save
        --tokenid|@{selected|token_id}
        --emote|@{selected|character_name} tries to find the will to live.
        --Roll:|[[ [$DEATH] 1d20 + @{selected|death_save_bonus} ]]
    }}

### Fumble/Fate

    !power {{
        --titlefontshadow|none
        --name|FUMBLE!
        --tokenid|@{selected|token_id}
        --emote|@{selected|character_name}...OMG! WTF Happened?!
        --!fumble:|Let's see what the have in store for you @{selected|character_name}.
        --I have Spoken:|[[ 4dF ]]
    }}


## Attribute Checks

### Strength Check

    !power {{
        --titlefontshadow|none
        --name|Strength Check
        --tokenid|@{selected|token_id}
        --emote|@{selected|character_name} attempts to overpower his opposition with brute strength!
        --Roll:|[[ [$ATT] ?{Check|Standard,1d20|Advantage,2d20kh1|Disadvantage,2d20kl1} + @{selected|strength_mod}[STR] ]]
    }}

### Dexterity Check

    !power {{
        --titlefontshadow|none
        --name|Dexterity Check
        --tokenid|@{selected|token_id}
        --emote|@{selected|character_name}
        --Roll:|[[ [$ATT] ?{Check|Standard,1d20|Advantage,2d20kh1|Disadvantage,2d20kl1} + @{selected|dexterity_mod}[DEX] ]]
    }}

### Constitution Check

    !power {{
        --titlefontshadow|none
        --name|Constitution Check
        --tokenid|@{selected|token_id}
        --emote|@{selected|character_name}
        --Constitution Check:|[[ [$ATT] ?{Check|Standard,1d20|Advantage,2d20kh1|Disadvantage,2d20kl1} + @{selected|constitution_mod}[CON] ]]
    }}

### Intelligence Check

    !power {{
        --titlefontshadow|none
        --name|Intelligence Check
        --tokenid|@{selected|token_id}
        --emote|@{selected|character_name}
        --Roll:|[[ [$ATT] ?{Check|Standard,1d20|Advantage,2d20kh1|Disadvantage,2d20kl1} + @{selected|intelligence_mod}[INT] ]]
    }}

### Wisdom Check

    !power {{
        --titlefontshadow|none
        --name|Wisdom Check
        --tokenid|@{selected|token_id}
        --emote|@{selected|character_name}
        --Roll:|[[ [$ATT] ?{Check|Standard,1d20|Advantage,2d20kh1|Disadvantage,2d20kl1} + @{selected|wisdom_mod}[WIS] ]]
    }}

### Charisma Check

    !power {{
        --titlefontshadow|none
        --name|Charisma Check
        --tokenid|@{selected|token_id}
        --emote|@{selected|character_name}
        --Roll:|[[ [$ATT] ?{Check|Standard,1d20|Advantage,2d20kh1|Disadvantage,2d20kl1} + @{selected|charisma_mod}[CHA] ]]
    }}


## Attribute Saves

### Strength Save

    !power {{
        --titlefontshadow|none
        --name|Strength Save
        --tokenid|@{selected|token_id}
        --emote|@{selected|character_name} summons all his strength to resist being overpowered!
        --Roll:|[[ [$ATT] ?{Save|Standard,1d20|Advantage,2d20kh1|Disadvantage,2d20kl1} + @{selected|strength_save_bonus}[STR] ]]
    }}

### Dexterity Save
    !power {{
        --titlefontshadow|none
        --name|Dexterity Save
        --tokenid|@{selected|token_id}
        --emote|@{selected|character_name}
        --Roll:|[[ [$ATT] ?{Save|Standard,1d20|Advantage,2d20kh1|Disadvantage,2d20kl1} + @{selected|dexterity_save_bonus}[DEX] ]]
    }}


### Constitution Save

    !power {{
        --titlefontshadow|none
        --name|Constitution Save
        --tokenid|@{selected|token_id}
        --emote|@{selected|character_name} digs deep to resist being debilitated.
        --Roll:|[[ [$ATT] ?{Save|Standard,1d20|Advantage,2d20kh1|Disadvantage,2d20kl1} + @{selected|constitution_save_bonus}[CON] ]]
    }}

### Intelligence Save

    !power {{
        --titlefontshadow|none
        --name|Intelligence Save
        --tokenid|@{selected|token_id}
        --emote|@{selected|character_name}
        --Roll:|[[ [$ATT] ?{Save|Standard,1d20|Advantage,2d20kh1|Disadvantage,2d20kl1} + @{selected|intelligence_save_bonus}[INT] ]]
    }}

### Wisdom Save

    !power {{
        --titlefontshadow|none
        --name|Wisdom Save
        --tokenid|@{selected|token_id}
        --emote|@{selected|character_name}
        --Roll:|[[ [$ATT] ?{Save|Standard,1d20|Advantage,2d20kh1|Disadvantage,2d20kl1} + @{selected|wisdom_save_bonus}[WIS] ]]
    }}

### Charisma Save

    !power {{
        --titlefontshadow|none
        --name|Charisma Save
        --tokenid|@{selected|token_id}
        --emote|@{selected|character_name}
        --Roll:|[[ [$ATT] ?{Save|Standard,1d20|Advantage,2d20kh1|Disadvantage,2d20kl1} + @{selected|charisma_save_bonus}[CHA] ]]
    }}


## Skill Checks

### Acrobatics

    !power {{
        --titlefontshadow|none
        --name|Acrobatics
        --tokenid|@{selected|token_id}
        --emote|@{selected|character_name} attempts to stay on his feet.
        --Skill Check:|[[ [$SKILL] ?{SkillCheck|Standard,1d20|Advantage,2d20kh1|Disadvantage,2d20kl1} + @{selected|acrobatics_bonus}[SKILL] ]]
    }}

### Animal Handling

    !power {{
        --titlefontshadow|none
        --name|Animal Handling
        --tokenid|@{selected|token_id}
        --emote|@{selected|character_name} tries to keep the animal calm.
        --Skill Check:|[[ [$SKILL] ?{SkillCheck|Standard,1d20|Advantage,2d20kh1|Disadvantage,2d20kl1} + @{selected|animal_handling_bonus}[SKILL] ]]
    }}

### Arcana

    !power {{
        --titlefontshadow|none
        --name|Arcana
        --tokenid|@{selected|token_id}
        --emote|@{selected|character_name} tries to remember anything he has learned.
        --Skill Check:|[[ [$SKILL] ?{SkillCheck|Standard,1d20|Advantage,2d20kh1|Disadvantage,2d20kl1} + @{selected|arcana_bonus}[SKILL] ]]
    }}

### Athletics

    !power {{
        --titlefontshadow|none
        --name|Athletics
        --tokenid|@{selected|token_id}
        --emote|@{selected|character_name} tries to get out of this difficult situation.
        --Skill Check:|[[ [$SKILL] ?{SkillCheck|Standard,1d20|Advantage,2d20kh1|Disadvantage,2d20kl1} + @{selected|athletics_bonus}[SKILL] ]]
    }}

### Deception

    !power {{
        --titlefontshadow|none
        --name|Deception
        --tokenid|@{selected|token_id}
        --emote|@{selected|character_name} tries to be misleading.
        --Skill Check:|[[ [$SKILL] ?{SkillCheck|Standard,1d20|Advantage,2d20kh1|Disadvantage,2d20kl1} + @{selected|deception_bonus}[SKILL] ]]
    }}

### History

    !power {{
        --titlefontshadow|none
        --name|History
        --tokenid|@{selected|token_id}
        --emote|@{selected|character_name} tries to remember events and people from the past.
        --Skill Check:|[[ [$SKILL] ?{SkillCheck|Standard,1d20|Advantage,2d20kh1|Disadvantage,2d20kl1} + @{selected|history_bonus}[SKILL] ]]
    }}

### Insight
    !power {{
        --titlefontshadow|none
        --name|Insight
        --tokenid|@{selected|token_id}
        --emote|@{selected|character_name} tries to determine @{target|character_name}'s intentions from their body language.
        --Skill Check:|[[ [$SKILL] ?{SkillCheck|Standard,1d20|Advantage,2d20kh1|Disadvantage,2d20kl1} + @{selected|insight_bonus}[SKILL] ]]
    }}

### Intimidation

This macro uses a random roll to decide what text to display for a battle cry

    !power {{
        --titlefontshadow|none
        --name|Intimidation
        --tokenid|@{selected|token_id}
        --emote|@{selected|character_name} yells across the battle field ...
        --hroll|[[ [$Rando] 1d8 ]]
        --?! $Rando -eq 1 !? Battle Cry:|Retreat now, or I will leave nothing but a crushed bones to bury!
        --?! $Rando -eq 2 !? Battle Cry:|This fight will be quick, but far from painless for you!
        --?! $Rando -eq 3 !? Battle Cry:|Have you ever been a liquid? I can change that!
        --?! $Rando -eq 4 !? Battle Cry:|Please, I’m curious: Did it take practice to be this much of a failure or does it come naturally to you?
        --?! $Rando -eq 5 !? Battle Cry:|Let your eyes look their last, for soon your eyes will be food for the crows!
        --?! $Rando -eq 6 !? Battle Cry:|This is the last time I kill you!
        --?! $Rando -eq 7 !? Battle Cry:|Hell hungers…and my maul shall feed it!
        --?! $Rando -eq 8 !? Battle Cry:|The next time we speak, you will be but a puddle at my feet!
        --Skill Check:|[[ [$Intim] ?{Attack|Standard,1d20|Advantage,2d20kh1|Disadvantage,2d20kl1} + @{selected|intimidation_bonus}[SKILL] ]]
    }}

### Investigation

    !power {{
        --titlefontshadow|none
        --name|Investigation
        --tokenid|@{selected|token_id}
        --emote|@{selected|character_name} looks around for clues.
        --Skill Check:|[[ [$SKILL] ?{SkillCheck|Standard,1d20|Advantage,2d20kh1|Disadvantage,2d20kl1} + @{selected|investigation_bonus}[SKILL] ]]
    }}

### Medicine
    !power {{
        --titlefontshadow|none
        --name|Medicine
        --tokenid|@{selected|token_id} tries to determin what is wrong in order to help.
        --emote|@{selected|character_name} 
        --Skill Check:|[[ [$SKILL] ?{SkillCheck|Standard,1d20|Advantage,2d20kh1|Disadvantage,2d20kl1} + @{selected|medicine_bonus}[SKILL] ]]
    }}

### Nature
    !power {{
        --titlefontshadow|none
        --name|Nature
        --tokenid|@{selected|token_id}
        --emote|@{selected|character_name} tries to remember details about the environment.
        --Skill Check:|[[ [$SKILL] ?{SkillCheck|Standard,1d20|Advantage,2d20kh1|Disadvantage,2d20kl1} + @{selected|nature_bonus}[SKILL] ]]
    }}

### Perception

    !power {{
        --titlefontshadow|none
        --name|Perception
        --tokenid|@{selected|token_id}
        --emote|@{selected|character_name} looks around to see if he detects the presence of anything lurking in the shadows.
        --Skill Check:|[[ [$SKILL] ?{SkillCheck|Standard,1d20|Advantage,2d20kh1|Disadvantage,2d20kl1} + @{selected|perception_bonus}[SKILL] ]]
    }}

### Performance

    !power {{
        --titlefontshadow|none
        --name|Performance
        --tokenid|@{selected|token_id}
        --emote|@{selected|character_name} tries to delight his fans.
        --Skill Check:|[[ [$SKILL] ?{SkillCheck|Standard,1d20|Advantage,2d20kh1|Disadvantage,2d20kl1} + @{selected|performance_bonus}[SKILL] ]]
    }}

### Persuasion
    !power {{
        --titlefontshadow|none
        --name|Persuasion
        --tokenid|@{selected|token_id}
        --emote|@{selected|character_name} tries to gain influence with his good nature.
        --Skill Check:|[[ [$SKILL] ?{SkillCheck|Standard,1d20|Advantage,2d20kh1|Disadvantage,2d20kl1} + @{selected|persuasion_bonus}[SKILL] ]]
    }}

### Religion

    !power {{
        --titlefontshadow|none
        --name|Religion
        --tokenid|@{selected|token_id}
        --emote|@{selected|character_name} tries to recall lore or prayers.
        --Skill Check:|[[ [$SKILL] ?{SkillCheck|Standard,1d20|Advantage,2d20kh1|Disadvantage,2d20kl1} + @{selected|religion_bonus}[SKILL] ]]
    }}

### Sleight of Hand

    !power {{
        --titlefontshadow|none
        --name|Sleight of Hand
        --tokenid|@{selected|token_id}
        --emote|@{selected|character_name} tries to be sneeky with the object.
        --Skill Check:|[[ [$SKILL] ?{SkillCheck|Standard,1d20|Advantage,2d20kh1|Disadvantage,2d20kl1} + @{selected|sleight_of_hand_bonus}[SKILL] ]]
    }}

### Stealth

    !power {{
        --titlefontshadow|none
        --name|Stealth
        --tokenid|@{selected|token_id}
        --emote|@{selected|character_name} tries to hide in the shadows so he is note detected.
        --Skill Check:|[[ [$SKILL] ?{SkillCheck|Standard,1d20|Advantage,2d20kh1|Disadvantage,2d20kl1} + @{selected|stealth_bonus}[SKILL] ]]
    }}

### Survival

    !power {{
        --titlefontshadow|none
        --name|Survival
        --tokenid|@{selected|token_id}
        --emote|@{selected|character_name} tries to identify signs in the wild.
        --Skill Check:|[[ [$SKILL] ?{SkillCheck|Standard,1d20|Advantage,2d20kh1|Disadvantage,2d20kl1} + @{selected|survival_bonus}[SKILL] ]]
    }}