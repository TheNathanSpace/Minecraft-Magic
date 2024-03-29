# Minecraft Magic
Minecraft Magic hopes to add a magic system that allows the player to interact with the environment. It runs on [Minecraft Forge](https://files.minecraftforge.net/maven/net/minecraftforge/forge/index_1.13.2.html).

This page is acting as the wiki until the mod has enough content to need a separate one!

## Files
You can download the project in the ["Releases" tab](https://github.com/TheKingElessar/Minecraft-Magic/releases) on the GitHub project page. It will not be available on CurseForge until it is fully released.

**Naming convention:** `Minecraft_Magic_[mod version]_[Minecraft version].jar`

## Spells
There are 3 spells available. Spells are organized into one of 8 schools of magic.
- Conjuration
  - Conjure Fang
  - Conjure Fang Row
  - Conjure Fang Circle

### Conjure Fang
**Range:** 20 blocks

**Target:** Block or Entity

Summons a single fang where the caster is targeting.

### Conjure Fang Row
**Range:** 10 blocks

**Target:** Direction

Summons a row of fangs originating at the caster and extending to the range. In total, 8 fangs are summoned.

### Conjure Fang Circle
**Range:** Self

Summons two rings of fangs surrounding the caster. The first ring contains 5 fangs and is summoned 1.5 blocks away from the caster. The second ring contains 8 fangs and is summoned 2.5 blocks away from the caster.

## Items
Each spell has a corresponding item that is used to cast the spell. Right clicking while holding the spell's item will cast it.

## Entities
Only one entity is currently used:
- Evoker Fangs Rotatable
  - This is exactly like the vanilla Evoker Fangs entity; however, having a custom rendering class allows rotation to be more easily done. In the future this entity will probably be removed and the vanilla entity, with added Capabilities, will be used.

## A note on 1.14.2
This is currently updated to 1.13.2. At the moment, Forge 1.14.2 is not far enough along for me to want to update, but I expect in the next couple of weeks I will be able to.

## Versions
Current Version: v0.2-alpha.

Released: 06/18/2019

[Changelog](CHANGELOG.md)

# Developer Info
At the moment there is no API for adding new or using existing spells (such as having mobs in another mod cast spells), but in the future I hope to add one.

## Spell Structure
How a spell is structured:
- Item Class
  - When right clicked, the spell's constructor should be called.
  - Depending upon the results of the constructor, the spell's `castClient` method should be called.
- Spell Class
  - Constructor
    - The constructor should gather any needed information from the client. The most common is the target, taken from an instance of the ExtendedRange class.
  - `castClient` method
    - The `castClient` method should only be called on the client-side. It should verify that any needed information has been gathered, then send a packet with any needed information to the server.
  - `castServer` method
    - The `castServer` method should be a static method (because the server-side has no need to re-create an instance of the class). It should use data from the server to do all server-side work.
  - Other methods
    - Most spells should have server-side work split up into several methods, as they will be more complicated.
- Packet Class
  - Packets should include information sent from the client-side to the server-side. It will most commonly contain information on the spell's target. Sometimes no information is needed; however, packets should still be used to keep the regular structure between all spells and to more easily be updated and changed in the furture.
  - The server should, on a separate network thread, call the spell's `castServer` method using information contained in the packet.

## Resources
For information on using GitHub and Git, see [here](https://product.hubspot.com/blog/git-and-github-tutorial-for-beginners).

For information on GitHub formatting, see [here](https://help.github.com/en/articles/basic-writing-and-formatting-syntax).

For a simple online tool to make pixel textures, see [here](https://www.pixilart.com/draw).