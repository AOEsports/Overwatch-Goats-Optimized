settings
{
main
{
Description: "Outback Brawl GOATS, based off of CGL GOATS\nMeant To Replicate Overwatch Patch 1.24\nVersion: 2.2\nMade By Aria Boyce and Headrammer\nModified by Gatt"
Mode Name: "AOEsports (CGL) GOATs"
}

    lobby
    {
    	Max Spectators: 12
    	Max Team 1 Players: 6
    	Max Team 2 Players: 6
    	Swap Teams After Match: No
    }

    modes
    {
    	Assault

    	Clash
    	{
    		Capture Speed Modifier: 45%
    	}

    	Control

    	Escort

    	Flashpoint

    	Hybrid

    	Push

    	General
    	{
    		Competitive Rules: On
    		Game Mode Start: Immediately
    		Kill Cam: Off
    		Tank Role Passive Health Bonus: Always Enabled
    	}
    }

    heroes
    {
    	General
    	{
    		Ultimate Generation - Combat: 120%

    		Ana
    		{
    			Ammunition Clip Size Scalar: 95%
    			Biotic Grenade Cooldown Time: 83%
    			Damage Dealt: 107%
    			Healing Dealt: 107%
    			Health: 80%
    			Sleep Dart Cooldown Time: 85%
    			Ultimate Generation Nano Boost: 115%
    		}

    		Brigitte
    		{
    			Barrier Shield Cooldown Time: 166%
    			Barrier Shield Recharge Rate: 125%
    			Healing Dealt: 10%
    			Repair Pack Cooldown Time: 120%
    			Shield Bash Cooldown Time: 120%
    			Ultimate Generation - Combat Rally: 80%
    			Ultimate Generation - Passive Rally: 75%
    			Ultimate Generation Rally: 100%
    			Whip Shot Knockback Scalar: 80%
    		}

    		D.Va
    		{
    			Boosters Cooldown Time: 125%
    			Defense Matrix Maximum Time: 85%
    			Defense Matrix Recharge Rate: 128%
    			Micro Missiles Cooldown Time: 114%
    		}

    		Lúcio
    		{
    			Damage Dealt: 55%
    			Health: 80%
    			Ultimate Generation Sound Barrier: 115%
    		}

    		Moira
    		{
    			Biotic Energy Maximum: 200%
    			Biotic Energy Recharge Rate: 0%
    			Biotic Orb Cooldown Time: 125%
    			Biotic Orb Max Healing Scalar: 120%
    			Health: 80%
    			Ultimate Generation Coalescence: 110%
    		}

    		Reinhardt
    		{
    			Barrier Field Recharge Rate: 138%
    			Damage Dealt: 25%
    		}

    		Roadhog
    		{
    			Chain Hook: Off
    			Pig Pen: Off
    			Primary Fire: Off
    			Quick Melee: Off
    			Take a Breather: Off
    			Ultimate Ability Whole Hog: Off
    		}

    		Winston
    		{
    			Barrier Projector Cooldown Time: 109%
    			Secondary Fire: Off
    		}

    		Zarya
    		{
    			Particle Barrier Cooldown Time: 0%
    			Projected Barrier Cooldown Time: 0%
    			Ultimate Generation Graviton Surge: 108%
    		}

    		Zenyatta
    		{
    			Ammunition Clip Size Scalar: 80%
    			Damage Dealt: 96%
    		}

    		enabled heroes
    		{
    			Ana
    			Brigitte
    			D.Va
    			Lúcio
    			Moira
    			Reinhardt
    			Winston
    			Zarya
    			Zenyatta
    		}
    	}
    }

    workshop
    {
    	Brig Passive Ult Gain: 1.000
    	Brig Ult Scalar: 0.900
    }

}

variables
{
global:
0: health_set
1: debug_mode
2: average_value
3: average_count
4: tick_time

    player:
    	0: role
    	1: base_health
    	2: base_armor
    	3: base_shield
    	4: self_move_speed
    	7: current_hero
    	8: tick_rate
    	9: setup_complete
    	10: debug_text
    	11: armor_tracking
    	12: current_shield_health
    	13: max_shield_health
    	14: time_since_damage_shield
    	15: health_ref
    	16: ult_charge
    	18: brig_shield_location
    	20: brig_inspire
    	21: brig_inspire_ref
    	22: brig_pack_ref
    	24: brig_rally_timer
    	25: brig_rally_armor_ref
    	26: brig_rally_armor_amount
    	27: brig_passive_ult_gain
    	28: brig_ult_gain_scalar
    	29: brig_shield_time
    	30: dva_state
    	31: dva_ult_state
    	32: team_in_range
    	33: team_out_range
    	34: team_minus_lucio
    	35: moira_resource
    	36: moira_heal_drain
    	37: moira_heal_passive
    	38: moira_heal_damage
    	39: moira_self_heal
    	40: winston_ult_health
    	41: zarya_hud_ref
    	42: zarya_shield_cooldown_1
    	43: zarya_shield_cooldown_2
    	46: temp_players
    	47: temp_damage
    	48: list_of_players
    	49: temp_heal
    	50: i
    	51: i_0
    	52: i_1
    	53: i_2
    	54: i_3
    	55: temp_health
    	56: temp_armor

}

subroutines
{
0: apply_custom_health
}

rule("Initial Global")
{
event
{
Ongoing - Global;
}

    actions
    {
    	Global.tick_time = 0.016;
    }

}

rule("Ana Sleep Dart")
{
event
{
Player Dealt Damage;
All;
Ana;
}

    conditions
    {
    	Event Ability == Button(Ability 1);
    }

    actions
    {
    	Wait(3, Ignore Condition);
    	If(Has Status(Victim, Asleep));
    		Clear Status(Victim, Asleep);
    		Wait(0.016, Ignore Condition);
    		Set Status(Victim, Null, Asleep, 3);
    	End;
    }

}

rule("Ana Nano Heal")
{
event
{
Player Dealt Healing;
All;
Ana;
}

    conditions
    {
    	Event Ability == Button(Ultimate);
    }

    actions
    {
    	Damage(Healee, Null, Event Healing * 2);
    }

}

rule("Hud Text")
{
event
{
Ongoing - Global;
}

    actions
    {
    	Global.debug_mode = False;
    	Disable Inspector Recording;
    	If(Global.debug_mode);
    		Create HUD Text(Null, Null, Null, Custom String("Server Load: {0}\nAverage: {1}\nPeak: {2}", Global.average_value,
    			Server Load Average, Server Load Peak), Right, 0, Color(White), Color(White), Color(White), Visible To and String,
    			Visible Always);
    	End;
    }

}

rule("On Death")
{
event
{
Ongoing - Each Player;
All;
All;
}

    actions
    {
    	Event Player.ult_charge = 0;
    	Event Player.brig_rally_timer = 0;
    }

}

rule("Slow Mode")
{
event
{
Ongoing - Global;
}

    conditions
    {
    	Server Load Average >= 254;
    }

    actions
    {
    	Set Slow Motion(25);
    	Wait Until(Server Load Average < 250, 5);
    	Set Slow Motion(100);
    }

}

rule("apply custom health")
{
event
{
Subroutine;
apply_custom_health;
}

    actions
    {
    	Set Healing Received(Event Player, 0);
    	Remove All Health Pools From Player(Event Player);
    	Wait(0.016, Ignore Condition);
    	Set Status(Event Player, Null, Unkillable, 5);
    	Wait(0.016, Ignore Condition);
    	Damage(Event Player, Null, 9999999.000);
    	Set Player Health(Event Player, 1);
    	Wait(0.016, Ignore Condition);
    	Add Health Pool To Player(Event Player, Health, 9999999.000, True, True);
    	Add Health Pool To Player(Event Player, Armor, 9999999.000, True, True);
    	Add Health Pool To Player(Event Player, Shields, 9999999.000, True, True);
    	Wait(0.016, Ignore Condition);
    	Remove All Health Pools From Player(Event Player);
    	Wait(0.016, Ignore Condition);
    	Set Healing Received(Event Player, 100);
    	Heal(Event Player, Null, 10000);
    	Wait(0.016, Ignore Condition);
    	If(Event Player.base_health > 0);
    		Add Health Pool To Player(Event Player, Health, Event Player.base_health - 1, True, True);
    		Event Player.health_ref = Last Created Health Pool;
    	End;
    	If(Event Player.base_armor > 0);
    		Add Health Pool To Player(Event Player, Armor, Event Player.base_armor, True, True);
    	End;
    	If(Event Player.base_shield > 0);
    		Add Health Pool To Player(Event Player, Shields, Event Player.base_shield, True, True);
    	End;
    	Clear Status(Event Player, Unkillable);
    	Wait(0.016, Ignore Condition);
    }

}

rule("Spawn in")
{
event
{
Ongoing - Each Player;
All;
All;
}

    conditions
    {
    	Hero Of(Event Player) != Event Player.current_hero;
    }

    actions
    {
    	Event Player.setup_complete = False;
    	Set Ability 1 Enabled(Event Player, True);
    	Set Ability 2 Enabled(Event Player, True);
    	Set Jump Vertical Speed(Event Player, 100);
    	Event Player.base_armor = 0;
    	Event Player.base_health = 0;
    	Event Player.base_shield = 0;
    	Event Player.self_move_speed = 100;
    	Event Player.role = 0;
    	Event Player.tick_rate = 0.016;
    	Destroy HUD Text(Event Player.zarya_hud_ref);
    	Set Knockback Received(Event Player, 100);
    	Remove All Health Pools From Player(Event Player);
    	Destroy HUD Text(Event Player.debug_text);
    	If(Global.debug_mode);
    	End;
    	If(Hero Of(Event Player) == Hero(Ana));
    		Event Player.role = 0;
    		Event Player.current_hero = Hero(Ana);
    		Event Player.base_armor = 0;
    		Event Player.base_health = 200;
    		Event Player.base_shield = 0;
    		Event Player.self_move_speed = 100;
    		While(Max Health Of Type(Event Player, Health) != Event Player.base_health || Max Health Of Type(Event Player, Armor)
    			!= Event Player.base_armor || Max Health Of Type(Event Player, Shields) != Event Player.base_shield);
    			Set Healing Received(Event Player, 0);
    			Remove All Health Pools From Player(Event Player);
    			Wait(0.016, Ignore Condition);
    			Set Status(Event Player, Null, Unkillable, 5);
    			Wait(0.016, Ignore Condition);
    			Damage(Event Player, Null, 9999999.000);
    			Set Player Health(Event Player, 1);
    			Wait(0.016, Ignore Condition);
    			Add Health Pool To Player(Event Player, Health, 9999999.000, True, True);
    			Add Health Pool To Player(Event Player, Armor, 9999999.000, True, True);
    			Add Health Pool To Player(Event Player, Shields, 9999999.000, True, True);
    			Wait(0.016, Ignore Condition);
    			Remove All Health Pools From Player(Event Player);
    			Wait(0.016, Ignore Condition);
    			Set Healing Received(Event Player, 100);
    			Heal(Event Player, Null, 10000);
    			Wait(0.016, Ignore Condition);
    			If(Event Player.base_health > 0);
    				Add Health Pool To Player(Event Player, Health, Event Player.base_health - 1, True, True);
    				Event Player.health_ref = Last Created Health Pool;
    			End;
    			If(Event Player.base_armor > 0);
    				Add Health Pool To Player(Event Player, Armor, Event Player.base_armor, True, True);
    			End;
    			If(Event Player.base_shield > 0);
    				Add Health Pool To Player(Event Player, Shields, Event Player.base_shield, True, True);
    			End;
    			Clear Status(Event Player, Unkillable);
    			Wait(0.250, Ignore Condition);
    			Wait(0.100, Ignore Condition);
    		End;
    	Else If(Hero Of(Event Player) == Hero(Brigitte));
    		Set Max Health(Event Player, 240);
    		Event Player.role = 0;
    		Event Player.brig_passive_ult_gain = Workshop Setting Real(Custom String("Settings"), Custom String("Brig Passive Ult Gain"), 1, 0,
    			2, 0);
    		Event Player.brig_ult_gain_scalar = Workshop Setting Real(Custom String("Settings"), Custom String("Brig Ult Scalar"), 1, 0, 2, 1);
    		Event Player.self_move_speed = 100;
    		Event Player.base_armor = 50;
    		Event Player.base_health = 200;
    		Event Player.base_shield = 0;
    		Event Player.current_hero = Hero(Brigitte);
    		Event Player.brig_shield_location = Eye Position(Event Player) + Facing Direction Of(Event Player) * 0.850;
    		While(Max Health Of Type(Event Player, Health) != Event Player.base_health || Max Health Of Type(Event Player, Armor)
    			!= Event Player.base_armor || Max Health Of Type(Event Player, Shields) != Event Player.base_shield);
    			Set Healing Received(Event Player, 0);
    			Remove All Health Pools From Player(Event Player);
    			Wait(0.016, Ignore Condition);
    			Set Status(Event Player, Null, Unkillable, 5);
    			Wait(0.016, Ignore Condition);
    			Damage(Event Player, Null, 9999999.000);
    			Set Player Health(Event Player, 1);
    			Wait(0.016, Ignore Condition);
    			Add Health Pool To Player(Event Player, Health, 9999999.000, True, True);
    			Add Health Pool To Player(Event Player, Armor, 9999999.000, True, True);
    			Add Health Pool To Player(Event Player, Shields, 9999999.000, True, True);
    			Wait(0.016, Ignore Condition);
    			Remove All Health Pools From Player(Event Player);
    			Wait(0.016, Ignore Condition);
    			Set Healing Received(Event Player, 100);
    			Heal(Event Player, Null, 10000);
    			Wait(0.016, Ignore Condition);
    			If(Event Player.base_health > 0);
    				Add Health Pool To Player(Event Player, Health, Event Player.base_health - 1, True, True);
    				Event Player.health_ref = Last Created Health Pool;
    			End;
    			If(Event Player.base_armor > 0);
    				Add Health Pool To Player(Event Player, Armor, Event Player.base_armor, True, True);
    			End;
    			If(Event Player.base_shield > 0);
    				Add Health Pool To Player(Event Player, Shields, Event Player.base_shield, True, True);
    			End;
    			Clear Status(Event Player, Unkillable);
    			Wait(0.250, Ignore Condition);
    			Wait(0.100, Ignore Condition);
    		End;
    	Else If(Hero Of(Event Player) == Hero(D.Va));
    		Event Player.dva_state = 2;
    		Event Player.base_armor = 200;
    		Event Player.base_health = 400;
    		Event Player.base_shield = 0;
    		Event Player.dva_ult_state = 1;
    		Event Player.role = 1;
    		While(Max Health(Event Player) != 600);
    			Start Rule(apply_custom_health, Do Nothing);
    			Wait(0.016, Ignore Condition);
    			Wait(0.016, Ignore Condition);
    			If(Is In Alternate Form(Event Player));
    				Break;
    			End;
    		End;
    		Set Knockback Received(Event Player, 166);
    		Event Player.dva_state = 0;
    	Else If(Hero Of(Event Player) == Hero(Lúcio));
    		Event Player.team_in_range = Null;
    		Event Player.team_out_range = Null;
    		Event Player.self_move_speed = 100;
    		Event Player.base_health = 200;
    		Event Player.current_hero = Hero(Lúcio);
    		While(Max Health Of Type(Event Player, Health) != Event Player.base_health || Max Health Of Type(Event Player, Armor)
    			!= Event Player.base_armor || Max Health Of Type(Event Player, Shields) != Event Player.base_shield);
    			Set Healing Received(Event Player, 0);
    			Remove All Health Pools From Player(Event Player);
    			Wait(0.016, Ignore Condition);
    			Set Status(Event Player, Null, Unkillable, 5);
    			Wait(0.016, Ignore Condition);
    			Damage(Event Player, Null, 9999999.000);
    			Set Player Health(Event Player, 1);
    			Wait(0.016, Ignore Condition);
    			Add Health Pool To Player(Event Player, Health, 9999999.000, True, True);
    			Add Health Pool To Player(Event Player, Armor, 9999999.000, True, True);
    			Add Health Pool To Player(Event Player, Shields, 9999999.000, True, True);
    			Wait(0.016, Ignore Condition);
    			Remove All Health Pools From Player(Event Player);
    			Wait(0.016, Ignore Condition);
    			Set Healing Received(Event Player, 100);
    			Heal(Event Player, Null, 10000);
    			Wait(0.016, Ignore Condition);
    			If(Event Player.base_health > 0);
    				Add Health Pool To Player(Event Player, Health, Event Player.base_health - 1, True, True);
    				Event Player.health_ref = Last Created Health Pool;
    			End;
    			If(Event Player.base_armor > 0);
    				Add Health Pool To Player(Event Player, Armor, Event Player.base_armor, True, True);
    			End;
    			If(Event Player.base_shield > 0);
    				Add Health Pool To Player(Event Player, Shields, Event Player.base_shield, True, True);
    			End;
    			Clear Status(Event Player, Unkillable);
    			Wait(0.250, Ignore Condition);
    			Wait(0.100, Ignore Condition);
    		End;
    	Else If(Hero Of(Event Player) == Hero(Moira));
    		Event Player.base_health = 200;
    		Event Player.moira_resource = 100;
    		Event Player.moira_heal_drain = 7.051;
    		Event Player.moira_heal_passive = 2.400;
    		Event Player.moira_heal_damage = 7.782;
    		Event Player.current_hero = Hero(Moira);
    		Event Player.tick_rate = 0.320;
    		While(Max Health Of Type(Event Player, Health) != Event Player.base_health || Max Health Of Type(Event Player, Armor)
    			!= Event Player.base_armor || Max Health Of Type(Event Player, Shields) != Event Player.base_shield);
    			Set Healing Received(Event Player, 0);
    			Remove All Health Pools From Player(Event Player);
    			Wait(0.016, Ignore Condition);
    			Set Status(Event Player, Null, Unkillable, 5);
    			Wait(0.016, Ignore Condition);
    			Damage(Event Player, Null, 9999999.000);
    			Set Player Health(Event Player, 1);
    			Wait(0.016, Ignore Condition);
    			Add Health Pool To Player(Event Player, Health, 9999999.000, True, True);
    			Add Health Pool To Player(Event Player, Armor, 9999999.000, True, True);
    			Add Health Pool To Player(Event Player, Shields, 9999999.000, True, True);
    			Wait(0.016, Ignore Condition);
    			Remove All Health Pools From Player(Event Player);
    			Wait(0.016, Ignore Condition);
    			Set Healing Received(Event Player, 100);
    			Heal(Event Player, Null, 10000);
    			Wait(0.016, Ignore Condition);
    			If(Event Player.base_health > 0);
    				Add Health Pool To Player(Event Player, Health, Event Player.base_health - 1, True, True);
    				Event Player.health_ref = Last Created Health Pool;
    			End;
    			If(Event Player.base_armor > 0);
    				Add Health Pool To Player(Event Player, Armor, Event Player.base_armor, True, True);
    			End;
    			If(Event Player.base_shield > 0);
    				Add Health Pool To Player(Event Player, Shields, Event Player.base_shield, True, True);
    			End;
    			Clear Status(Event Player, Unkillable);
    			Wait(0.250, Ignore Condition);
    			Wait(0.100, Ignore Condition);
    		End;
    	Else If(Hero Of(Event Player) == Hero(Reinhardt));
    		Set Max Health(Event Player, 133.333);
    		Set Knockback Received(Event Player, 166);
    		Event Player.base_armor = 200;
    		Event Player.base_shield = 0;
    		Event Player.base_health = 300;
    		Event Player.self_move_speed = 100;
    		Event Player.role = 1;
    		Event Player.current_hero = Hero(Reinhardt);
    		While(Max Health Of Type(Event Player, Health) != Event Player.base_health || Max Health Of Type(Event Player, Armor)
    			!= Event Player.base_armor || Max Health Of Type(Event Player, Shields) != Event Player.base_shield);
    			Set Healing Received(Event Player, 0);
    			Remove All Health Pools From Player(Event Player);
    			Wait(0.016, Ignore Condition);
    			Set Status(Event Player, Null, Unkillable, 5);
    			Wait(0.016, Ignore Condition);
    			Damage(Event Player, Null, 9999999.000);
    			Set Player Health(Event Player, 1);
    			Wait(0.016, Ignore Condition);
    			Add Health Pool To Player(Event Player, Health, 9999999.000, True, True);
    			Add Health Pool To Player(Event Player, Armor, 9999999.000, True, True);
    			Add Health Pool To Player(Event Player, Shields, 9999999.000, True, True);
    			Wait(0.016, Ignore Condition);
    			Remove All Health Pools From Player(Event Player);
    			Wait(0.016, Ignore Condition);
    			Set Healing Received(Event Player, 100);
    			Heal(Event Player, Null, 10000);
    			Wait(0.016, Ignore Condition);
    			If(Event Player.base_health > 0);
    				Add Health Pool To Player(Event Player, Health, Event Player.base_health - 1, True, True);
    				Event Player.health_ref = Last Created Health Pool;
    			End;
    			If(Event Player.base_armor > 0);
    				Add Health Pool To Player(Event Player, Armor, Event Player.base_armor, True, True);
    			End;
    			If(Event Player.base_shield > 0);
    				Add Health Pool To Player(Event Player, Shields, Event Player.base_shield, True, True);
    			End;
    			Clear Status(Event Player, Unkillable);
    			Wait(0.250, Ignore Condition);
    			Wait(0.100, Ignore Condition);
    		End;
    	Else If(Hero Of(Event Player) == Hero(Winston));
    		Event Player.base_health = 400;
    		Event Player.base_armor = 100;
    		Set Max Health(Event Player, 92.308);
    		Set Damage Dealt(Event Player, 85.714);
    		Event Player.current_hero = Hero(Winston);
    		Event Player.role = 1;
    		Set Knockback Received(Event Player, 166);
    		While(Max Health Of Type(Event Player, Health) != Event Player.base_health || Max Health Of Type(Event Player, Armor)
    			!= Event Player.base_armor || Max Health Of Type(Event Player, Shields) != Event Player.base_shield);
    			Set Healing Received(Event Player, 0);
    			Remove All Health Pools From Player(Event Player);
    			Wait(0.016, Ignore Condition);
    			Set Status(Event Player, Null, Unkillable, 5);
    			Wait(0.016, Ignore Condition);
    			Damage(Event Player, Null, 9999999.000);
    			Set Player Health(Event Player, 1);
    			Wait(0.016, Ignore Condition);
    			Add Health Pool To Player(Event Player, Health, 9999999.000, True, True);
    			Add Health Pool To Player(Event Player, Armor, 9999999.000, True, True);
    			Add Health Pool To Player(Event Player, Shields, 9999999.000, True, True);
    			Wait(0.016, Ignore Condition);
    			Remove All Health Pools From Player(Event Player);
    			Wait(0.016, Ignore Condition);
    			Set Healing Received(Event Player, 100);
    			Heal(Event Player, Null, 10000);
    			Wait(0.016, Ignore Condition);
    			If(Event Player.base_health > 0);
    				Add Health Pool To Player(Event Player, Health, Event Player.base_health - 1, True, True);
    				Event Player.health_ref = Last Created Health Pool;
    			End;
    			If(Event Player.base_armor > 0);
    				Add Health Pool To Player(Event Player, Armor, Event Player.base_armor, True, True);
    			End;
    			If(Event Player.base_shield > 0);
    				Add Health Pool To Player(Event Player, Shields, Event Player.base_shield, True, True);
    			End;
    			Clear Status(Event Player, Unkillable);
    			Wait(0.250, Ignore Condition);
    			Wait(0.100, Ignore Condition);
    		End;
    	Else If(Hero Of(Event Player) == Hero(Zarya));
    		Event Player.base_health = 200;
    		Event Player.base_shield = 200;
    		Create HUD Text(Event Player, Null, Null, Custom String(
    			"\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n    {0}                                                                    {1}             {2}",
    			Custom String(
    			"                                                                                                                      "),
    			Custom String("{0}{1}", Custom String("                                                                                "),
    			Round To Integer(Event Player.zarya_shield_cooldown_1, Up)), Round To Integer(Event Player.zarya_shield_cooldown_2, Up)), Left,
    			1, Color(White), Color(Black), Color(White), String, Visible Never);
    		Event Player.zarya_hud_ref = Last Text ID;
    		Event Player.tick_rate = 0.240;
    		Event Player.role = 1;
    		Event Player.max_shield_health = 200;
    		Set Knockback Received(Event Player, 166);
    		Event Player.current_shield_health = Health Of Type(Event Player, Shields);
    		While(Max Health Of Type(Event Player, Health) != Event Player.base_health || Max Health Of Type(Event Player, Armor)
    			!= Event Player.base_armor || Max Health Of Type(Event Player, Shields) != Event Player.base_shield);
    			Set Healing Received(Event Player, 0);
    			Remove All Health Pools From Player(Event Player);
    			Wait(0.016, Ignore Condition);
    			Set Status(Event Player, Null, Unkillable, 5);
    			Wait(0.016, Ignore Condition);
    			Damage(Event Player, Null, 9999999.000);
    			Set Player Health(Event Player, 1);
    			Wait(0.016, Ignore Condition);
    			Add Health Pool To Player(Event Player, Health, 9999999.000, True, True);
    			Add Health Pool To Player(Event Player, Armor, 9999999.000, True, True);
    			Add Health Pool To Player(Event Player, Shields, 9999999.000, True, True);
    			Wait(0.016, Ignore Condition);
    			Remove All Health Pools From Player(Event Player);
    			Wait(0.016, Ignore Condition);
    			Set Healing Received(Event Player, 100);
    			Heal(Event Player, Null, 10000);
    			Wait(0.016, Ignore Condition);
    			If(Event Player.base_health > 0);
    				Add Health Pool To Player(Event Player, Health, Event Player.base_health - 1, True, True);
    				Event Player.health_ref = Last Created Health Pool;
    			End;
    			If(Event Player.base_armor > 0);
    				Add Health Pool To Player(Event Player, Armor, Event Player.base_armor, True, True);
    			End;
    			If(Event Player.base_shield > 0);
    				Add Health Pool To Player(Event Player, Shields, Event Player.base_shield, True, True);
    			End;
    			Clear Status(Event Player, Unkillable);
    			Wait(0.250, Ignore Condition);
    			Wait(0.100, Ignore Condition);
    		End;
    	Else If(Hero Of(Event Player) == Hero(Zenyatta));
    		Event Player.role = 0;
    		Event Player.self_move_speed = 100;
    		Event Player.base_health = 50;
    		Event Player.base_shield = 150;
    		Event Player.base_armor = 0;
    		Event Player.current_hero = Hero(Zenyatta);
    		Event Player.max_shield_health = 150;
    		Set Knockback Dealt(Event Player, 10);
    		While(Max Health Of Type(Event Player, Health) != Event Player.base_health || Max Health Of Type(Event Player, Armor)
    			!= Event Player.base_armor || Max Health Of Type(Event Player, Shields) != Event Player.base_shield);
    			Set Healing Received(Event Player, 0);
    			Remove All Health Pools From Player(Event Player);
    			Wait(0.016, Ignore Condition);
    			Set Status(Event Player, Null, Unkillable, 5);
    			Wait(0.016, Ignore Condition);
    			Damage(Event Player, Null, 9999999.000);
    			Set Player Health(Event Player, 1);
    			Wait(0.016, Ignore Condition);
    			Add Health Pool To Player(Event Player, Health, 9999999.000, True, True);
    			Add Health Pool To Player(Event Player, Armor, 9999999.000, True, True);
    			Add Health Pool To Player(Event Player, Shields, 9999999.000, True, True);
    			Wait(0.016, Ignore Condition);
    			Remove All Health Pools From Player(Event Player);
    			Wait(0.016, Ignore Condition);
    			Set Healing Received(Event Player, 100);
    			Heal(Event Player, Null, 10000);
    			Wait(0.016, Ignore Condition);
    			If(Event Player.base_health > 0);
    				Add Health Pool To Player(Event Player, Health, Event Player.base_health - 1, True, True);
    				Event Player.health_ref = Last Created Health Pool;
    			End;
    			If(Event Player.base_armor > 0);
    				Add Health Pool To Player(Event Player, Armor, Event Player.base_armor, True, True);
    			End;
    			If(Event Player.base_shield > 0);
    				Add Health Pool To Player(Event Player, Shields, Event Player.base_shield, True, True);
    			End;
    			Clear Status(Event Player, Unkillable);
    			Wait(0.250, Ignore Condition);
    			Wait(0.100, Ignore Condition);
    		End;
    	End;
    	Event Player.current_hero = Hero Of(Event Player);
    	Event Player.setup_complete = True;
    	Event Player.armor_tracking = Health Of Type(Event Player, Armor);
    }

}

rule("Inbetween rounds")
{
event
{
Ongoing - Each Player;
All;
All;
}

    conditions
    {
    	!Is Game In Progress == True;
    	Is Between Rounds == True;
    }

    actions
    {
    	Respawn(All Dead Players(All Teams));
    	All Players(All Teams).brig_rally_armor_amount = 0;
    	Wait(10, Ignore Condition);
    	Wait Until(Is In Spawn Room(Event Player), 100);
    	Remove All Health Pools From Player(Event Player);
    	Wait(0.016, Ignore Condition);
    	Set Max Health(Event Player, 100.100);
    	Wait(0.016, Ignore Condition);
    	Set Max Health(Event Player, 100);
    	Heal(Event Player, Null, 999999);
    	Event Player.setup_complete = False;
    	Event Player.current_hero = Null;
    }

}

rule("Damage on occassion")
{
event
{
Ongoing - Each Player;
All;
All;
}

    conditions
    {
    	Health(Event Player) < Max Health(Event Player);
    }

    actions
    {
    	Damage(Event Player, Null, 0.010);
    	Heal(Event Player, Null, 0.010);
    	Wait(2.400, Ignore Condition);
    	Loop If Condition Is True;
    }

}

rule("Armor Tracking and tank headshot")
{
event
{
Player Took Damage;
All;
All;
}

    conditions
    {
    	Event Player.role == 1;
    }

    actions
    {
    	If(Event Was Critical Hit);
    		If(Event Player.armor_tracking > 0);
    			Damage(Victim, Attacker, (Event Damage + 10) * 0.250 - 10);
    		Else;
    			Damage(Victim, Attacker, Event Damage * 0.250);
    		End;
    	End;
    }

}

rule("Average of Average Tracking")
{
event
{
Ongoing - Global;
}

    actions
    {
    	If(Server Load Average > 50);
    		Global.average_value *= Global.average_count;
    		Global.average_value += Server Load Average;
    		Global.average_count += 1;
    		Global.average_value /= Global.average_count;
    	End;
    	Wait(1, Ignore Condition);
    	Loop;
    }

}

rule("Brig Action")
{
event
{
Ongoing - Each Player;
All;
Brigitte;
}

    actions
    {
    	If(Is Button Held(Event Player, Button(Secondary Fire)));
    		Event Player.brig_shield_time = 0;
    	Else;
    		Event Player.brig_shield_time += 0.120;
    	End;
    	If(Is Using Ability 2(Event Player));
    		Event Player.temp_players = Players in View Angle(Event Player, Team Of(Event Player), 90);
    		If(Event Player.temp_players.brig_rally_armor_amount > 0);
    			Remove Health Pool From Player(Event Player.temp_players.brig_rally_armor_ref);
    			Damage(Event Player.temp_players, Null, 0.010);
    			Add Health Pool To Player(Event Player.temp_players, Armor, Event Player.temp_players.brig_rally_armor_amount, False, True);
    			Event Player.temp_players.brig_rally_armor_ref = Last Created Health Pool;
    		End;
    		Damage(Event Player.temp_players, Null, 0.010);
    	End;
    	If(Is Button Held(Event Player, Button(Secondary Fire)) && Is Firing Primary(Event Player));
    		Event Player.self_move_speed += 50;
    		Set Move Speed(Event Player, Event Player.self_move_speed);
    		Wait Until(!Is Firing Primary(Event Player), 1);
    		Event Player.self_move_speed -= 50;
    		Set Move Speed(Event Player, Event Player.self_move_speed);
    	End;
    	Wait(0.120, Ignore Condition);
    	Loop If(Hero Of(Event Player) == Hero(Brigitte));
    }

}

rule("Brig: Reduce Armor From Damage")
{
event
{
Player Took Damage;
All;
All;
}

    conditions
    {
    	Event Player.brig_rally_armor_amount > 0;
    }

    actions
    {
    	Event Player.temp_damage = Event Damage;
    	Event Player.temp_damage -= Health Of Type(Event Player, Shields);
    	If(Event Player.temp_damage < 0);
    		Event Player.temp_damage = 0;
    	End;
    	Event Player.brig_rally_armor_amount -= Event Player.temp_damage;
    	If(Event Player.brig_rally_armor_amount < 0);
    		Event Player.brig_rally_armor_amount = 0;
    	End;
    }

}

rule("Brig Damage")
{
event
{
Player Dealt Damage;
All;
Brigitte;
}

    conditions
    {
    	Event Damage != Null;
    }

    actions
    {
    	If(Event Ability == Button(Primary Fire) && (Is Button Held(Event Player, Button(Secondary Fire))
    		|| Event Player.brig_shield_time < 0.250) && Ability Cooldown(Attacker, Button(Primary Fire)) == 0 && Ability Cooldown(
    		Attacker, Button(Secondary Fire)) == 0);
    		Set Status(Victim, Attacker, Stunned, 1);
    		Set Ability Cooldown(Event Player, Button(Primary Fire), 6);
    	Else If(Event Player.brig_inspire == 0);
    		Event Player.brig_inspire = 1;
    	End;
    }

}

rule("Brig Inspire")
{
event
{
Ongoing - Each Player;
All;
Brigitte;
}

    conditions
    {
    	Event Player.brig_inspire == 1;
    }

    actions
    {
    	Event Player.list_of_players = Players Within Radius(Position Of(Event Player), 20, Team Of(Event Player), Surfaces);
    	Stop Heal Over Time(Event Player.list_of_players.brig_inspire_ref);
    	Start Heal Over Time(Event Player.list_of_players, Event Player, 5, 14.500);
    	Event Player.list_of_players.brig_inspire_ref = Last Heal Over Time ID;
    	Wait(1, Ignore Condition);
    	Event Player.brig_inspire = 0;
    }

}

rule("Brig Repair Pack")
{
event
{
Player Dealt Healing;
All;
Brigitte;
}

    conditions
    {
    	Event Ability == Button(Ability 2);
    }

    actions
    {
    	Set Ability Charge(Event Player, Button(Ability 2), 0);
    	Set Ability Cooldown(Event Player, Button(Ability 2), 100);
    	Event Player.temp_heal = 150;
    	Event Player.temp_heal -= Min(Max Health(Healee) - Health(Healee), 150);
    	Heal(Healee, Healer, 150 - Event Player.temp_heal);
    	If(Event Player.temp_heal > 75);
    		Event Player.temp_heal = 75;
    	End;
    	Add Health Pool To Player(Healee, Armor, Event Player.temp_heal, False, True);
    	Event Player.brig_pack_ref = Last Created Health Pool;
    	Wait(5, Ignore Condition);
    	Remove Health Pool From Player(Event Player.brig_pack_ref);
    	Wait(1, Ignore Condition);
    	Set Ability Charge(Event Player, Button(Ability 2), 3);
    }

}

rule("Dva Death")
{
event
{
Player Died;
All;
D.Va;
}

    conditions
    {
    	Event Player.dva_state == 0;
    }

    actions
    {
    	Event Player.dva_state = 1;
    }

}

rule("Dva Ult")
{
event
{
Ongoing - Each Player;
All;
D.Va;
}

    conditions
    {
    	Is Using Ultimate(Event Player) == True;
    }

    actions
    {
    	Set Damage Dealt(Event Player, 20);
    	Wait(2, Ignore Condition);
    	Set Damage Dealt(Event Player, 100);
    }

}

rule("Dva Action")
{
event
{
Ongoing - Each Player;
All;
D.Va;
}

    actions
    {
    	If(Is In Alternate Form(Event Player) && Event Player.dva_state == 0);
    		While(Max Health(Event Player) != 150);
    			Event Player.base_armor = 0;
    			Event Player.base_health = 150;
    			Start Rule(apply_custom_health, Do Nothing);
    			Wait(0.016, Ignore Condition);
    			If(!Is In Alternate Form(Event Player));
    				Break;
    			End;
    		End;
    		Event Player.dva_state = 1;
    		Set Damage Dealt(Event Player, 100);
    	Else If(!Is In Alternate Form(Event Player) && Event Player.dva_state == 1);
    		Event Player.base_armor = 200;
    		Event Player.base_health = 400;
    		While(Max Health(Event Player) != 600);
    			Global.health_set = True;
    			Start Rule(apply_custom_health, Do Nothing);
    			Global.health_set = False;
    			Wait(0.016, Ignore Condition);
    			If(Is In Alternate Form(Event Player));
    				Break;
    			End;
    		End;
    		Event Player.dva_state = 0;
    		Set Damage Dealt(Event Player, 100);
    	End;
    	If(Is Using Ability 2(Event Player));
    		Set Damage Dealt(Event Player, 90);
    		Wait Until(!Is Using Ability 2(Event Player), 10);
    		Set Damage Dealt(Event Player, 100);
    	End;
    	Wait(0.200, Ignore Condition);
    	Loop If(Hero Of(Event Player) == Hero(D.Va));
    }

}

rule("Lucio Action")
{
event
{
Ongoing - Each Player;
All;
Lúcio;
}

    actions
    {
    	Event Player.team_minus_lucio = Remove From Array(All Players(Team Of(Event Player)), Event Player);
    	Event Player.team_in_range = Remove From Array(Players Within Radius(Position Of(Event Player), 12, Team Of(Event Player),
    		Surfaces And Enemy Barriers), Event Player);
    	Event Player.team_out_range = Remove From Array(Event Player.team_minus_lucio, Event Player.team_in_range);
    	If(Is In Alternate Form(Event Player));
    		If(Is Using Ability 2(Event Player));
    			Event Player.self_move_speed += 6.300;
    			Set Move Speed(Event Player, Event Player.self_move_speed);
    			Event Player.self_move_speed -= 6.300;
    			Event Player.i = 0;
    			While(Event Player.i < 5);
    				If(Event Player.team_in_range[Event Player.i] == Null);
    					Break;
    				End;
    				Event Player.team_in_range[Event Player.i].self_move_speed += 6.300;
    				Set Move Speed(Event Player.team_in_range[Event Player.i], Event Player.team_in_range[Event Player.i].self_move_speed);
    				Event Player.team_in_range[Event Player.i].self_move_speed -= 6.300;
    				Event Player.i += 1;
    			End;
    			Event Player.i_0 = 0;
    			While(Event Player.i_0 < 5);
    				If(Event Player.team_out_range[Event Player.i_0] == Null);
    					Break;
    				End;
    				Set Move Speed(Event Player.team_out_range[Event Player.i_0], Event Player.team_out_range[Event Player.i_0].self_move_speed);
    				Event Player.i_0 += 1;
    			End;
    		Else;
    			Event Player.self_move_speed += 4;
    			Set Move Speed(Event Player, Event Player.self_move_speed);
    			Event Player.self_move_speed -= 4;
    			Event Player.i_1 = 0;
    			While(Event Player.i_1 < 5);
    				If(Event Player.team_in_range[Event Player.i_1] == Null);
    					Break;
    				End;
    				Event Player.team_in_range[Event Player.i_1].self_move_speed += 4;
    				Set Move Speed(Event Player.team_in_range[Event Player.i_1], Event Player.team_in_range[Event Player.i_1].self_move_speed);
    				Event Player.team_in_range[Event Player.i_1].self_move_speed -= 4;
    				Event Player.i_1 += 1;
    			End;
    			Event Player.i_2 = 0;
    			While(Event Player.i_2 < 5);
    				If(Event Player.team_out_range[Event Player.i_2] == Null);
    					Break;
    				End;
    				Set Move Speed(Event Player.team_out_range[Event Player.i_2], Event Player.team_out_range[Event Player.i_2].self_move_speed);
    				Event Player.i_2 += 1;
    			End;
    		End;
    	Else;
    		Set Move Speed(Event Player, Event Player.self_move_speed);
    		Event Player.i_3 = 0;
    		While(Event Player.i_3 < 5);
    			If(Event Player.team_minus_lucio[Event Player.i_3] == Null);
    				Break;
    			End;
    			Set Move Speed(Event Player.team_minus_lucio[Event Player.i_3], Event Player.team_minus_lucio[Event Player.i_3].self_move_speed);
    			Event Player.i_3 += 1;
    		End;
    	End;
    	Wait(0.250, Ignore Condition);
    	Loop If(Hero Of(Event Player) == Hero(Lúcio));
    }

}

rule("Lucio Self Heal")
{
event
{
Player Received Healing;
All;
Lúcio;
}

    conditions
    {
    	Event Ability != Null;
    	Healer == Event Player;
    	!Is Using Ability 2(Event Player) == True;
    }

    actions
    {
    	Heal(Healee, Healee, Event Healing * 0.230);
    }

}

rule("Lucio Damage")
{
event
{
Player Dealt Damage;
All;
Lúcio;
}

    actions
    {
    	If(Event Ability == Button(Primary Fire));
    		Damage(Victim, Attacker, 18.364);
    	Else If(Event Ability == Button(Melee));
    		Damage(Victim, Attacker, 23.636);
    	End;
    }

}

rule("Moira Action")
{
event
{
Ongoing - Each Player;
All;
Moira;
}

    actions
    {
    	If(Is Firing Primary(Event Player));
    		Event Player.moira_resource -= Event Player.moira_heal_drain * Event Player.tick_rate;
    	Else;
    		Event Player.moira_resource += Event Player.moira_heal_passive * Event Player.tick_rate;
    	End;
    	If(Is Using Ability 1(Event Player));
    		Set Jump Vertical Speed(Event Player, 50);
    	Else If(Is Using Ultimate(Event Player));
    		Set Ability 1 Enabled(Event Player, False);
    		Event Player.self_move_speed += 7.200;
    		Set Move Speed(Event Player, Event Player.self_move_speed);
    		Start Damage Over Time(Event Player, Null, 100, 5);
    		Event Player.moira_self_heal = Last Damage Over Time ID;
    		Wait Until(!Is Using Ultimate(Event Player), 100);
    		Stop Damage Over Time(Event Player.moira_self_heal);
    		Event Player.self_move_speed -= 7.200;
    		Set Move Speed(Event Player, Event Player.self_move_speed);
    		Set Ability 1 Enabled(Event Player, True);
    	Else;
    		Set Jump Vertical Speed(Event Player, 100);
    	End;
    	If(Event Player.moira_resource > 100);
    		Event Player.moira_resource = 100;
    	End;
    	Set Ability Resource(Event Player, Button(Primary Fire), Event Player.moira_resource);
    	Wait(Event Player.tick_rate, Ignore Condition);
    	Loop If(Hero Of(Event Player) == Hero(Moira));
    }

}

rule("Moira Damage")
{
event
{
Player Dealt Damage;
All;
Moira;
}

    conditions
    {
    	Event Ability == Button(Secondary Fire);
    }

    actions
    {
    	Event Player.moira_resource += Event Player.moira_heal_damage * Event Player.tick_rate;
    }

}

rule("Moira Heal")
{
event
{
Player Dealt Healing;
All;
Moira;
}

    actions
    {
    	If(Event Ability == Button(Primary Fire));
    		Heal(Healee, Healer, Event Healing * 0.143);
    	End;
    }

}

rule("Rein Action")
{
event
{
Ongoing - Each Player;
All;
Reinhardt;
}

    actions
    {
    	If(Is Using Ability 2(Event Player));
    		Set Ability Charge(Event Player, Button(Ability 2), 0);
    		Wait Until(Is Using Ability 2(Event Player) == False, 10);
    		Set Ability Cooldown(Event Player, Button(Ability 2), 6);
    	Else If(Is Firing Secondary(Event Player));
    		Event Player.self_move_speed -= 28;
    		Set Move Speed(Event Player, Event Player.self_move_speed);
    		Wait Until(!Is Firing Secondary(Event Player), 1000);
    		Event Player.self_move_speed += 28;
    		Set Move Speed(Event Player, Event Player.self_move_speed);
    	End;
    	Wait(0.333, Ignore Condition);
    	Loop If(Hero Of(Event Player) == Hero(Reinhardt));
    }

}

rule("Rein Damage")
{
event
{
Player Dealt Damage;
All;
Reinhardt;
}

    conditions
    {
    	Event Damage != Null;
    }

    actions
    {
    	If(Event Ability == Button(Primary Fire));
    		Damage(Victim, Attacker, 200);
    	Else If(Event Ability == Button(Ability 2));
    		Damage(Victim, Attacker, 280);
    	Else If(Event Ability == Button(Ability 1));
    		If(Event Damage > 20);
    			Damage(Victim, Attacker, 848);
    		Else;
    			Damage(Victim, Attacker, 150);
    		End;
    	Else If(Event Ability == Button(Ultimate) && !Event Was Critical Hit);
    		Damage(Victim, Attacker, 150);
    	End;
    }

}

rule("Winston Action")
{
event
{
Ongoing - Each Player;
All;
Winston;
}

    conditions
    {
    	Is Using Ultimate(Event Player) == True;
    }

    actions
    {
    	Set Damage Dealt(Event Player, 80);
    	Remove All Health Pools From Player(Event Player);
    	Add Health Pool To Player(Event Player, Health, 252, True, True);
    	Event Player.winston_ult_health = Last Created Health Pool;
    	Add Health Pool To Player(Event Player, Armor, 100, True, True);
    	Wait(10 - Global.tick_time * 2, Ignore Condition);
    	Event Player.temp_health = Health Of Type(Event Player, Health);
    	Event Player.temp_armor = Health Of Type(Event Player, Armor);
    	Wait(0.016, Ignore Condition);
    	Remove All Health Pools From Player(Event Player);
    	Add Health Pool To Player(Event Player, Health, 399, True, True);
    	Add Health Pool To Player(Event Player, Armor, 100, True, True);
    	Wait(0.016, Ignore Condition);
    	If(Event Player.temp_armor < 100);
    		Damage(Event Player, Null, 100 - Event Player.temp_armor + 10);
    	End;
    	If(Event Player.temp_health < 400);
    		Damage(Event Player, Null, 400 - Event Player.temp_health);
    	End;
    	Set Damage Dealt(Event Player, 85.714);
    }

}

rule("Zarya Action")
{
event
{
Ongoing - Each Player;
All;
Zarya;
}

    actions
    {
    	If(Is Using Ability 1(Event Player) && Event Player.zarya_shield_cooldown_1 == 0);
    		Wait(0.016, Ignore Condition);
    		Set Ability 1 Enabled(Event Player, False);
    		Event Player.zarya_shield_cooldown_1 = 10;
    	End;
    	If(Event Player.zarya_shield_cooldown_1 > 0);
    		Event Player.zarya_shield_cooldown_1 -= Event Player.tick_rate;
    	Else;
    		Event Player.zarya_shield_cooldown_1 = 0;
    		Set Ability 1 Enabled(Event Player, True);
    	End;
    	If(Is Using Ability 2(Event Player) && Event Player.zarya_shield_cooldown_2 == 0);
    		Wait(0.016, Ignore Condition);
    		Set Ability 2 Enabled(Event Player, False);
    		Event Player.zarya_shield_cooldown_2 = 8;
    	End;
    	If(Event Player.zarya_shield_cooldown_2 > 0);
    		Event Player.zarya_shield_cooldown_2 -= Event Player.tick_rate;
    	Else;
    		Event Player.zarya_shield_cooldown_2 = 0;
    		Set Ability 2 Enabled(Event Player, True);
    	End;
    	If(Event Player.current_shield_health < Event Player.max_shield_health);
    		Event Player.time_since_damage_shield += Event Player.tick_rate;
    		If(Event Player.time_since_damage_shield >= 3);
    			Heal(Event Player, Null, Min(20 * Event Player.tick_rate, Event Player.max_shield_health - Event Player.current_shield_health));
    			Event Player.current_shield_health += Min(20 * Event Player.tick_rate,
    				Event Player.max_shield_health - Event Player.current_shield_health);
    			If(Event Player.current_shield_health > Event Player.max_shield_health);
    				Event Player.current_shield_health = Event Player.max_shield_health;
    			End;
    		End;
    	End;
    	Wait(Event Player.tick_rate, Ignore Condition);
    	Loop If(Hero Of(Event Player) == Hero(Zarya));
    }

}

rule("Zarya Took Damage")
{
event
{
Player Took Damage;
All;
Zarya;
}

    conditions
    {
    	Event Ability != Null;
    }

    actions
    {
    	Event Player.time_since_damage_shield = 0;
    	Event Player.current_shield_health = Health Of Type(Event Player, Shields);
    }

}

rule("Zen Action")
{
event
{
Ongoing - Each Player;
All;
Zenyatta;
}

    actions
    {
    	If(Event Player.current_shield_health < Event Player.max_shield_health);
    		Event Player.time_since_damage_shield += 0.250;
    		If(Event Player.time_since_damage_shield >= 3);
    			Heal(Event Player, Null, Min(2, Event Player.max_shield_health - Event Player.current_shield_health));
    			Event Player.current_shield_health += Min(2, Event Player.max_shield_health - Event Player.current_shield_health);
    			If(Event Player.current_shield_health > Event Player.max_shield_health);
    				Event Player.current_shield_health = Event Player.max_shield_health;
    			End;
    		End;
    	End;
    	Wait(0.250, Ignore Condition);
    	Loop If(Hero Of(Event Player) == Hero(Zenyatta));
    }

}

rule("Zen Took Damage")
{
event
{
Player Took Damage;
All;
Zenyatta;
}

    conditions
    {
    	Event Ability != Null;
    }

    actions
    {
    	Event Player.time_since_damage_shield = 0;
    	Event Player.current_shield_health = Health Of Type(Event Player, Shields);
    }

}
