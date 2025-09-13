## If you are on GitHub this is a mirror, the original repository with the latest updates is at [https://forgejo.neoeden.org/ergo/mod-draenei-giantess](https://forgejo.neoeden.org/ergo/mod-draenei-giantess)
---

# mod-draenei-giantess

A mod for the finest of gentlemen.

![Draenei Giantess Image](/draenei-giantess.png)

This feature-packed mod leverages the latest technologies to add an NPC that you can put on the entrance to Exodar so players can receive a warm welcome each time they go through the gate.

Step 1 - Run the following SQL queries on acore_world:

```
-- Add the NPC to the database
DELETE FROM `creature_template` WHERE (`entry` = 777795);
INSERT INTO `creature_template` (`entry`, `difficulty_entry_1`, `difficulty_entry_2`, `difficulty_entry_3`, `KillCredit1`, `KillCredit2`, `name`, `subname`, `IconName`, `gossip_menu_id`, `minlevel`, `maxlevel`, `exp`, `faction`, `npcflag`, `speed_walk`, `speed_run`, `speed_swim`, `speed_flight`, `detection_range`, `scale`, `rank`, `dmgschool`, `DamageModifier`, `BaseAttackTime`, `RangeAttackTime`, `BaseVariance`, `RangeVariance`, `unit_class`, `unit_flags`, `unit_flags2`, `dynamicflags`, `family`, `trainer_type`, `trainer_spell`, `trainer_class`, `trainer_race`, `type`, `type_flags`, `lootid`, `pickpocketloot`, `skinloot`, `PetSpellDataId`, `VehicleId`, `mingold`, `maxgold`, `AIName`, `MovementType`, `HoverHeight`, `HealthModifier`, `ManaModifier`, `ArmorModifier`, `ExperienceModifier`, `RacialLeader`, `movementId`, `RegenHealth`, `mechanic_immune_mask`, `spell_school_immune_mask`, `flags_extra`, `ScriptName`, `VerifiedBuild`) VALUES
(777795, 0, 0, 0, 0, 0, 'Draenei Hottie', 'Giantess', NULL, 0, 30, 30, 0, 1638, 0, 1, 1.14286, 1, 1, 20, 1, 0, 0, 1, 2000, 2000, 1, 1, 2, 512, 2048, 0, 0, 0, 0, 0, 0, 7, 0, 0, 0, 0, 0, 0, 0, 0, 'SmartAI', 1, 1, 1, 1, 1, 1, 0, 0, 1, 0, 0, 2, '', 12340);


-- Ensure SmartAI is enabled for NPC 777795
UPDATE `creature_template` SET `AIName` = 'SmartAI' WHERE `entry` = 777795;

-- Add text for NPC to say with kiss emote
DELETE FROM `creature_text` WHERE `CreatureID` = 777795;
INSERT INTO `creature_text` (`CreatureID`, `GroupID`, `ID`, `Text`, `Type`, `Language`, `Probability`, `Emote`, `Duration`, `Sound`, `BroadcastTextId`, `TextRange`, `comment`) VALUES
(777795, 0, 0, 'Welcome to Sexodar! <3', 12, 0, 100, 17, 0, 0, 0, 0, 'NPC 777795 - Kiss Greeting');

-- Add SmartAI script for player within 10 yards
DELETE FROM `smart_scripts` WHERE `entryorguid` = 777795 AND `source_type` = 0;
INSERT INTO `smart_scripts` (`entryorguid`, `source_type`, `id`, `link`, `event_type`, `event_phase_mask`, `event_chance`, `event_flags`, `event_param1`, `event_param2`, `event_param3`, `event_param4`, `event_param5`, `event_param6`, `action_type`, `action_param1`, `action_param2`, `action_param3`, `action_param4`, `action_param5`, `action_param6`, `target_type`, `target_param1`, `target_param2`, `target_param3`, `target_x`, `target_y`, `target_z`, `target_o`, `comment`) VALUES
(777795, 0, 0, 0, 101, 0, 100, 0, 1, 10, 0, 10000, 10000, 0, 1, 0, 0, 0, 0, 0, 0, 1, 0, 0, 0, 0, 0, 0, 0, 'NPC 777795 - On 1+ Player Nearby (10yd) - Talk (Group 0) and Kiss');
```

Step 2 - Go to Exodar, find a good location and spawn the NPC with the following command:

``.npc add 777795``

Step 3 - Profit.

She will greet players who come within 5 yards once every 10 seconds.