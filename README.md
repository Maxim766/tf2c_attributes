# tf2c_attributes

TF2C Attributes x64 SourceMod plugin

TF2 attributes plugin port for TF2 Classified. Changes:
1. Actualized version of gamedata for TF2C
2. Introduced small changes to the `tf2attributes.sp` and verified functionality via `tf2attributes_test.smx` plugin

Based on this fork (for TF2x64): https://github.com/Malifox/tf2attributes

AlliedModders link for additional info: https://forums.alliedmods.net/showthread.php?t=210221

NOTE: Because Sourcemod is not fully compatible with x64 source games (in particular sdktools and dhooks are still in hard development) this plugin uses virtual address method. If you have some problems with this plugin - please, open issue.

## Now featuring the following functionality from [nosoop/tf2attributes](https://github.com/nosoop/tf2attributes)

Add / remove temporary attributes on the player (using the game's own time-based expiry
mechanism for it).

```sourcepawn
// replicates the temporary health bonus granted by the Dalokohs Bar:
TF2Attrib_AddCustomPlayerAttribute(client, "hidden maxhealth non buffed", 50.0, 30.0);
```

Adds the game's "attribute hook" mechanism that collates values using an attribute class:

```sourcepawn
// computes the final damage multiplier based on the given item and owner's attributes:
float damageBonus = TF2Attrib_HookValueFloat(1.0, "mult_dmg", weapon);
```

Support for setting / getting attribute values via strings:

```sourcepawn
// set an entity's custom projectile model:
TF2Attrib_SetFromStringValue(entity, "custom projectile model", "models/weapons/c_models/c_grenadelauncher/c_grenadelauncher.mdl");

// get the name from an item:
TF2Attrib_HookValueString("NO NAME", "custom_name_attr", entity, buffer, sizeof(buffer));
```

Setting custom names / descriptions is not possible.  String values that are set by this plugin
are not replicated to the client &mdash; this is fine for attributes that are only accessed on
the server, but if you set any that the client will read, the client will crash on access.

## Installing 1.7.5C

1. Make sure you have the latest version of Metamod:Source (dev 2.0 build 1387 or later)
2. Make sure you have the latest version of Sourcemod (dev 1.13 build 7293 or later)
3. Download this repository.
2. Copy `tf2attributes.smx` to `addons/sourcemod/plugins/`.
3. Copy `tf2.attributes.txt` to `addons/sourcemod/gamedata/`.
4. If you're a developer, copy `tf2attributes.inc` to `addons/sourcemod/scripting/include/`
(or the appropriate path for your compiler toolchain / project).
