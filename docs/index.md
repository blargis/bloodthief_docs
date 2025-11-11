# Bloodthief Mapping Guide

This guide is meant to be used like a wiki for you to reference for all your mapping needs. [Trenchbroom](https://trenchbroom.github.io/) is the software that is used to make Bloodthief maps. It is free, open source, and used to make maps for many games, such as Quake, Dusk, Wrath: Aeon of Ruin, and many more. Trenchbroom is great because it’s *specifically designed for making **interactive** maps**,*** which makes getting started making a real level easy, but the possibilities are still limitless\!

## Where to start? 

**Watch the video getting started tutorial: [https://youtu.be/09mth4fUaH0](https://youtu.be/09mth4fUaH0)**

## Important Resources

You will need this resource folder to get started mapping: [bloodthief\_mapping\_resources.zip](https://drive.google.com/file/d/1IHrSjtdWp4tyQuInjpUgVuiSBSwXTLnh/view?usp=drive_link)  
Example Map: Time Tomb map from the main game [time\_tomb.map](https://drive.google.com/file/d/1ug1_SbQ-79RKrOdk9USPT0Q1SCSGNpa7/view?usp=drive_link)  
[Trenchbroom Manual](https://trenchbroom.github.io/manual/latest/)  
[Dumptruck\_ds Trenchbroom Tutorial Series](https://www.youtube.com/watch?v=gONePWocbqA&list=PLgDKRPte5Y0AZ_K_PZbWbgBAEt5xf74aE&index=1) (note: This tutorial series has a few sections specific to mapping for the game, Quake. You can ignore these parts). 

## Having Issues?

[Check Common Issues](#common-issues)

## Looking for tips?

[Check Pro Tips](#pro-tips)

## Deleting Your Own Custom Maps

Just delete the folder. Then go to Steam Workshop and delete the workshop entry. 

# Entity Reference

This will be quite overwhelming to read end-to-end. I recommend using this like a wiki or a reference manual and revisit it when you have a specific need or idea. Also use the section links on the far left to quickly jump to the documentation for a specific entity. 

## Point Entities

Point entities are what they sound like: Entities that are placed at a single point in the map.

### Enemies

All enemies pretty much share the same properties, so they will be lumped together in this section. Here are all the different enemies

* #### vt\_generic\_knight

* #### vt\_bow\_knight

* #### vt\_armored\_bow\_knight

* #### vt\_green\_knight

  * Note this is the generic armored knight. It’s called the green knight for legacy reasons. 

* #### vt\_black\_knight

  * special properties  
    * should\_move  
      * 0: Will not move. Will stand in place, even after becoming aggroed.  
      * 1: Will move toward player once aggroed

* #### vt\_spider

* #### vt\_cherub

  * Must be triggered to function (see targetname below)  
  * special properties  
    * should\_launch  
      * 0: Should not launch when triggered  
      * 1: Should launch when triggered (ie. fly upward briefly before firing)

* #### vt\_marble\_golem

* #### vt\_cyclops

* #### vt\_vampire

  * Must be triggered to function (see targetname below)  
  * special properties  
    * should\_launch  
      * 0: Should not launch when triggered  
      * 1: Should launch when triggered (ie. fly upward briefly before firing)

* #### vt\_god\_blood\_vessel

* #### vt\_skull

  * Must be triggered to function (see targetname below)  
  * special properties  
    * should\_launch  
      * 0: Should not launch when triggered  
      * 1: Should launch when triggered (ie. fly upward briefly before firing)

* #### vt\_mage

  * special properties  
    * target  
      * For the mage, the **target** property specifies the entity group that this mage should be tethered to with a magical shield link. Note the enemy it attaches to also needs a `bubble_shield_id`  
    * death\_target  
      * This is the entity that should be triggered when this mage dies. 

**All enemies have these key properties**

* hidden  
  * 0: The enemy will not be hidden when the game starts.   
  * 1: The enemy will be hidden and out of play when the game starts. Triggering the enemy will cause them to “unhide”  
* has\_spawn\_effect  
  * 0: When the enemy “unhides”, there will be no spawn effect  
  * 1: There will be a spawn effect when the enemy unhides  
* target  
  * This property designates the entity that should be triggered when this enemy **dies.** So for example, if you want `door1` to open when this enemy dies, you would specify `door1` for the target.   
* target\_func  
  * The function on the target that should be called when this entity dies. For example, if our target is a door, this can be set to `reverse_motion` to close a door when this entity dies  
* targetname:  
  * Use this to make the entity triggerable. This enemy will **unhide** when triggered. For example you can make an enemy hidden, and then give it targetname of `e1`. Then when `e1` is triggered, the enemy will unhide  
* bubble\_shield\_id  
  * Give this **any value** to give this enemy a bubble shield. In Bloodthief shields are typically tethered to a vt\_mage and are disabled when the mage dies. If the tethered mage is shielding two different enemies, **both enemies** should have the same bubble\_shield\_id.   
* shield\_type  
  * Only specify this property if bubble\_shield\_id is set.  
  * NO\_AIR\_DASH  
    * Applies a purple shield. Air dashes will be blocked while this enemy is shielded  
  * DAMAGE\_ON\_TOUCH  
    * Applies a red shield. The player can’t touch this shield or they will be damaged

### vt\_arrow\_pickup

* A pickup that gives you arrows. If you haven’t picked up a bow yet, you’ll pick it up automatically when arrows are picked up  
* Key Properties  
  * arrow\_count  
  * type  
    * The type of the arrow that should be picked up  
    * 1: Explosive arrows  
    * 2: Blood tether arrows

### vt\_artifact\_pickup

* Picks up an artifact part  
* Key properties  
  * artifact\_part\_name  
    *    NO\_ARTIFACT\_NAM  
    *     RUSTY\_BLADE\_POMME  
    *     DRAGON\_TOOTH\_SCABBAR  
    *     BATTERED\_SOUL\_OF\_PRISONE  
    *     RUSTY\_IRON\_RO  
    *     BENJIS\_STIC  
    *     ORNATE\_BLADE\_PART\_  
    *     ORNATE\_BLADE\_PART\_  
    *     STONE\_SWORD\_PART\_  
    *     STONE\_SWORD\_PART\_  
    *     STONE\_SWORD\_PART\_3  
    *     GLURMS\_WALKING\_STICK  
    *     GLURMS\_NOTES  
    *     KINGS\_BEATING\_HEART  
    *     KINGS\_BLADE\_PART\_2  
    *     ANCIENT\_BOOK  
    *     GOD\_KILLER\_BLADE\_PART\_2  
    *     STONE\_HEART  
    *     WIDGET  
    *     HOURGLASS  
    *     TRESS  
    *     TROWEL  
    *     FLAGELLUM  
    *     THREAD  
    *     GODSTEEL  
    *     SIN\_BOOK  
    *     TALKING\_SPIDER  
    *     BROTHERHOOD\_COIN  
    *     LENS  
    *     SCREAMING\_CRUCIBLE  
    *     VOW\_OF\_RETRIBUTION  
    *     MASK  
    *     BLESSED\_OIL  
    *     BLOOD\_CHALICE  
    *     FINETOOTH\_GEAR  
    *     EXQUISITE\_TOURBILLON  
    *     CALLUS  
    *     CAT\_TAIL  
    *     WEDDING\_RING   
    *     SEED  
    *     FINE\_WINE  
    *     GROTESQUE  
    *     LOADED\_DICE  
    *     TRIXIAN\_MANTLE  
    *     VASYLGLASS\_BANGLE  
    *     WIND\_ESSENCE  
    *     BLAST\_POWDER  
    *     THIEF\_SHIV  
    *     THEOLMORIN\_SHACKLE  
    *     OLD\_VARU\_KEY  
    *     PERMAFROST\_CHUNK  
    *     FIRE\_SLUG  
    *     CALMNESS\_SUPPRESSANT  
    *     TREESAP  
    *     RAGE\_MUSHROOM  
    *     TRIXIAN\_STEEL

### vt\_barrel

* An explosive barrel

### vt\_bat\_spinner

* A bat that flies in a circle.

### vt\_bell

* Ringing the bell creates a trigger event  
* key properties  
  * target  
    * The entity that should be triggered when the bell is rung

### vt\_blood\_fountain

* A triggerable blood fountain. Shoots blood in the air when triggered  
* key properties  
  * targetname  
    * When this targetname is triggered, blood will be shot into the air

### vt\_bow\_pickup

* A pickup that gives you either an explosive crossbow (arrow\_type=1) or a Blood Tether (arrow\_type \= 2\)  
* key properties  
  * arrow\_type  
    * 1: Grants Explosive crossbow  
    * 2: Grants Blood Tether  
  * targetname  
    * When this targetname is triggered, this pickup will be picked up. 

### vt\_color\_torch

* A torch that typically is used as a wall decoration. Can be any color  
* key properties  
  * light\_color  
    * The color of the light emitted from this torch in RGB (0-1) format. Use the Trenchbroom Color Picker to set this value  
  * color  
    * The color of the particles of the torch in RGB (0-1) format.  Use the Trenchbroom Color Picker to set this value.  
  * scale  
  * visibility\_range  
    * How far away the pixel fire is visible. Useful if `scale` is very high.

### vt\_crack

* Creates a crack decal. Typically used to indicate that a wall is breakable. Point it away from the wall for best results

### vt\_decor\_candle

* a candle purely for decoration

### vt\_decor\_smoke

* a smoke particle effect for decoration

### vt\_enemy\_shoot\_point

* Deprecated, not really useful. There was a point in time where enemies could shoot barrels but this proved to be frustrating so it was removed.

### vt\_environment

* Used to change the environment and skybox. **Only use one per map**  
* key properties  
  * environment: Use the dropdown to specify which level’s environment you want to use for your map. 

### vt\_eyeball\_pickup

* An eye of Ogamahn.   
* key properties  
  * target  
    * The entity that should be triggered when picked up  
  * eyeball\_name  
    * Each eyeball must have a unique name in your map for saving

### vt\_eyeball\_shrine

* A shrine of Ogamahn. 

### vt\_fish\_spinner

* A fish that spins in a circle

### vt\_floating\_candle

* a floating candle for decoration

### vt\_fmod\_sound

* A sound that plays on a loop in a particular spot  
* key properties  
  * guid  
    * The GUID of the sound to play. Possible values are   
      * ENEMY\_SKULL\_SKULL\_NESTING\_SOUND  
      * AMBIENT\_CRICKETS  
      * PLAYER\_HEART\_BEAT\_SPATIAL  
      * EFFECTS\_WATERFALL\_LOOP  
      * AMBIENT\_BIRDS  
      * AMBIENT\_DEFAULT\_AMBIENT\_SPATIAL

### vt\_generic\_pickup

* A powerup pickup  
* key properties  
  * powerup\_type  
    * BOUNCY\_DASH  
    * EXPLOSIVE\_AIR\_DASH  
    * SUPER\_SPEED  
    * SLIDE\_TO\_KILL  
    * UNLIMITED\_BLOOD  
  * target  
    * The target to trigger when this powerup is picked up  
  * target\_func  
    * The function on the target to call when this is picked up 

### vt\_health\_pickup

* A blood vial  
* key properties  
  * target  
    * The entity that should be triggered when picked up

### vt\_huddled\_god

### vt\_key\_pickup

* A key that can be used to lock doors or parts of the map. See vt\_trigger\_area for usage.   
* key properties  
  * key\_name  
    * The unique name of this key (not shown to the player)  
  * pick\_up\_message  
    * A message that appears when this key is picked up  
  * color  
    * The RGB (0-1) color of the key. Use the Trenchbroom color picker to set this  
  * display\_name  
    * The name of the key that is shown to the player when this key is picked up or when an area requiring this key is reached. 

### vt\_lantern

* Deprecated, lanterns are not used in isolation. See vt\_mage

### vt\_lever

* A triggerable lever  
* key properties  
  * scale  
    * Levers are pretty small by default. Set this to 4 for example to multiply the size by 4  
  * targetname  
    * Set this to make the lever triggerable. When the lever is triggered, the rod will pivot downward and the specified target will be triggered  
  * target  
    * The entity that should be triggered when this lever is triggered

### vt\_music

* Used to change the music of the map. Only use one per map  
* **Note:** all songs are "programmed" in a unique way, where the game transitions to a different part of the song depending on the "Intensity" of the game, controlled by `vt_intensity_change_area`.  
* key properties  
  * song  
    * use the dropdown to select the song you desire. Songs match the names of the songs in the Bloodthief OST

### vt\_pain\_vessel

* A vessel of pain. Hidden by default, must be triggered to appear  
* key properties  
  * targetname  
    * will appear when this targetname is triggered  
  * explosion\_force  
    * The force of the explosion when this vessel is killed  
  * should\_flash  
    * 0: Will not flash  
    * 1: Will flash

### vt\_player\_start

* The starting point of the player. The forward of this point entity matches the starting forward of the player  
* key properties  
  * targetname  
    * If this property is specified, instead of being the “start level” position for the player, this point will be the “checkpoint spawn” position for the checkpoint with a matching “target” property set. So for example if checkpoint 1 has a target of “foo”, and this vt\_player\_start has a targetname of “foo”, when the player spawns at checkpoint 1, they will spawn at the location of this entity. 

### vt\_portcullis

* deprecated 

### vt\_robed\_statue

* Can only be killed by players level 130 or higher  
* When killed, will trigger entities specified as the target  
* key properties  
  * target  
    * The entity that should be triggered when this statue dies

### vt\_sentient\_heart

* the sentient heart of theolmorin

### vt\_soul\_spinner

* A spinning soul

### vt\_stone\_god

* Theolmorin 

### vt\_sup\_light

* The main light entity in bloodthief  
* Key Properties  
  * light\_energy: The strength of the light  
  * light\_color: The color of the light, represented in RGB (0-1) format  
    * Note you can use Trenchbroom’s color picker in “float” mode to set the value of this property  
  * omni\_range: The Omnidirectional range of the light  
  * omni\_attenuation: The attenuation of the light

### vt\_swinging\_ax

* A swinging ax that can be used as an obstacle  
* key properties  
  * scale

### vt\_torch

* A decorative torch  
* key properties  
  * show\_mesh  
    * 0: Don’t show the little stick of the torch. Useful if you’re making a fireplace or a brazier or something  
  * scale  
  * light\_indirect\_energy  
  * visibility\_range  
    * How far away the pixel fire is visible. Useful if `scale` is very high.

### vt\_triggerable\_toast

* A dialogue that will appear when triggered  
* key properties  
  * targetname  
    * When this is triggered, the text will appear  
  * toast\_text  
    * the text that should appear  
  * should\_pause  
    * If the game should pause when the toast appears

### vt\_tutorial\_pickup

* A book that will show a tutorial when picked up  
* key properties  
  * tutorial\_title  
  * tutorial\_desc  
  * tutorial\_data\_path: Ignore this, not useful for custom maps

### vt\_util\_counter

* A triggerable entity that counts the amount of times it has been triggered and will emit a new trigger when the desired count is achieved  
* key properties  
  * trigger\_count  
    * how many times this entity should be triggered before emitting a new trigger  
  * targetname  
    * When this targetname is triggered, the counter increments the count  
  * target  
    * When trigger\_count is reached, this target is triggered  
  * target\_func  
    * The function on the target that should be called when the target is triggered

### vt\_util\_delayed\_trigger

* A triggerable entity that will emit a new trigger after a delay  
* key properties  
  * targetname  
    * When this targetname is triggered, target will be triggered after trigger\_delay seconds  
  * target  
    * the entity that should be triggered trigger\_delay seconds after this entity has been triggered  
  * target\_func  
    * The function that should be called on target when it is triggered  
  * trigger\_delay  
    * The delay in seconds that should be waited after this entity is triggered before target is in-turn triggered. 

### vt\_waypoint

* Not useful in custom maps right now

## Brush Entities

Brush entities are entities that are based on a brush, ie. some volume of space drawn in Trenchbroom. 

### func\_geo

* For the most part functions the same as worldspawn / default geometry, but with a few extra features  
* key properties  
  * surface\_type  
    * Impacts the sound your feet make when you walk on it. Use the dropdown  
  * window\_color  
    * If using one of the window textures, you can set this to color the window. use RGB (0-1)  
  * friction\_multiplier  
    * The friction of the surface  
  * chain\_speed  
    * If using the chain texture, this determines how fast the chains will move  
  * navigable  
    * COMING SOON: Use this to designate a piece of geo as navigable by enemies. Right now all geo is navigable in custom maps which is not very optimized. If you are running into optimization issues let me know and I’ll prioritize this. 

### func\_detail {#func_detail}

* Similar to func\_geo but with less properties. The main difference is that func\_detail do not have an occlusion shape built for them. You can use this entity as an optimization if your map has a bunch of little details that do not need occlusion shapes.  
* key properties  
  * window\_color  
  * navigable

### func\_detail\_illusionary

* Similar to func\_geo, but has no collision. Use this for pieces of geometry that are purely visual and the player and enemies should not collide with it  
* key properties  
  * window\_color

### vt\_blood\_area

* When the player is in this area, they rapidly increase the Blood bar and they move faster

### vt\_breakable

* A breakable object  
* key properties  
  * breakable\_type  
    * Use the dropdown to specify the type of the breakable  
  * gi\_mode  
    * Not relevant for mapping as there is only 1 gi\_mode in custom maps  
  * jib\_count\_multiplier  
    * Multiplies how many jibs that should emit when broken  
  * target  
    * The entity that should be triggered when broken  
  * target\_func  
    * The function on the entity that should be called when broken  
  * use\_fake\_rigidbodies  
    * 0: Don’t use fake rigidbodies  
    * 1: Use fake rigidbodies (more optimized but looks worse)  
  * bubble\_shield\_id  
    * When this is broken all entities with this bubble shield ID will have their shields removed  
  * has\_painting\_blend\_effect  
    * Does something interesting to sir\_brian\_tuke texture  
  * jib\_lifetime  
    * The lifetime of jibs once broken  
  * translation  
    * If set, this breakable also will function as a mover. See `vt_mover` for additional properties to use  
  * reverb\_level  
    * The reverb amount when broken (0-1 value)  
  * should\_jib  
    * 0: Jibs will not be emitted when broken  
    * 1: Jibs will be emitted when broken  
  * has\_collision:  
    * 0: No collision  
    * 1: Collision  
  * navigable:  
    * If this is navigable  
      * 0: No  
      * 1: Yes  
  * jib\_scale  
    * The scale of jibs  
  * jib\_type  
    * GORE, NON\_GORE, GLASS, GOD  
  * hide\_after\_checkpoint  
    * The checkpoint index at which this breakable becomes hidden  
  * friction\_multiplier  
    * The amount of friction the player’s movement has when standing on top of this breakable 

### vt\_checkpoint\_area

* A checkpoint. When the player respawns at checkpoint if the current checkpoint matches this area’s checkpoint index, the player will spawn here *at the bottom center* of this area facing in the direction specified by the angle property.   
* key properties  
  * checkpoint\_index  
    * When a level starts, the player starts at checkpoint 0\. When the player enters this area, the current checkpoint will be set to *at least* this index. So if this is set to 1, the player checkpoint will be set to checkpoint 1\. When the player respawns at checkpoint, they will spawn at *the bottom center* of this checkpoint by default. Alternatively, a specific point in space can be specified, see `target` property.   
  * checkpoint\_region  
    * An optional property that can be set to give your checkpoint a region. Regions can be used for “non-linear” maps that can be progressed in different orders. Perhaps the left path has a checkpoint with region “left” and checkpoint\_index 1 and the right path has region “right” with checkpoint\_index 1\. This allows the checkpoints to be reached in any order and still work as expected.   
  * angle  
    * This is the direction the player should be facing when spawning at checkpoint if `target` property is not set. In trenchbroom the direction the player will face is shown by a little arrow in the center of the checkpoint area.   
  * target  
    * optional property. Can be set to a vt\_player\_start with the same targetname to specify the exact point where the player should spawn when respawning at this checkpoint  
  * checkpoint\_active\_trigger\_count  
    * Zero by default. This is the amount of times this checkpoint must be triggered before it is reachable  
  * targetname  
    * When this targetname is triggered, the count corresponding to checkpoint\_active\_trigger\_count is incremented. 

### vt\_damage\_area

* If the player enters this area, they will die. **Note enemies will not be impacted by damage movers.**  
* key\_properties  
  * has\_piranhas  
    * If piranhas should emerge from the area when the player dies  
    * 0: no  
    * 1: yes

### vt\_damage\_mover

* Exactly the same as a `vt_mover` except it does damage when the player touches it.  
* key\_properties (Only showing the ones unique to this entity, see `vt_mover` for the other key properties)  
  * has\_spikes  
    * Whether spikes should be generated within the volume of this entity.   
    * **Note:** Spike generation looks for a nearby surface normal to determine the direction of the spikes. A proper vt\_damage\_mover placement with spikes would be a shallow (16-32 in depth) brush that is touching a `vt_mover` or a piece of solid geometry.   
    * 0: No spikes  
    * 1: Spikes  
  * damage\_type  
    * LAVA, NORMAL, DAMAGE\_AREA  
  * hardcoded\_normal  
    * See `has_spikes`. This will be the direction of the spikes if this value is set.

### vt\_end\_level\_area

* When this area is reached, the level ends

### vt\_intensity\_change\_area

* When this area is reached, the intensity of the level is set to *at least* intensity\_level. See `vt_music`.   
* key properties  
  * intensity\_level (0-1): The intensity that the level should be set to when reached

### vt\_launchpad

* A launchpad that bounces the player  
* key properties  
  * bounce\_force  
  * bounce\_force\_max  
  * overwrite\_velocity  
    * 0: no  
    * 1: yes  
  * launch\_dir  
    * optional, use this if the launch dir is different from the nearby surface normal of the launch pad  
  * translation  
    * optional. Use this for the launchpad to also function as a `vt_mover`

### vt\_lava

* lava

### vt\_magnet\_area

* a region that will very slightly magnetize the player toward the center 

### vt\_mover

* An entity that moves when triggered  
* key properties  
  * targetname  
    * when this targetname is triggered, the mover moves  
  * translation  
    * The translation that should occur when triggered, in **Godot Units / coordinate system.** Do not specify this if `tb_translation` is already set   
  * tb\_translation  
    * The translation that should occur when triggered, in **Trenchbroom Units / coordinate system.** Do not specify this if `translation` is already set   
  * duration  
    * How long in seconds the mover should take to perform the translation when triggered  
  * auto\_move\_after\_checkpoint  
    * When the player respawns at checkpoint index \>= this value, the mover will automatically teleport to its terminal position   
  * auto\_move\_after\_checkpoint\_region  
    * When the player respawns at checkpoint index \>= `auto_move_after_checkpoint`  and region \== this value, the mover will automatically teleport to its terminal position  
  * move\_delay  
    * The delay that should be waited after targetname is triggered before this mover will start moving  
  * trigger\_count  
    * How many times this mover should be triggered before moving. Default is 1  
  * gt\_mode  
    * Not needed for custom maps  
  * end\_position\_ratio\_in\_editor  
    * not used in custom maps  
  * play\_sound  
    * 0: Don’t play sound when moving  
    * 1: Do play sound  
  * start\_motion\_target  
    * The target that should be triggered when motion of this mover begins  
  * end\_motion\_target  
    * The target that should be triggered when motion of this mover ends  
  * end\_motion\_message  
    * A message that should display when motion ends  
  * start\_motion\_message   
    * A message that should display when motion begins  
  * move\_on\_start  
    * If this mover should start moving right away  
      * 1: yes  
      * 0: no  
  * oscillate  
    * 1: Immediately reverse motion when motion is finished  
    * 0: Stop when motion ends  
  * delay\_between\_oscillation  
    * Value in seconds that should be waited before reversing motion  
  * match\_speed\_with\_player  
    * 0: Dont match speed with player. Simply move at speed corresponding to `duration`  
    * 1: Move faster if player is moving faster  
  * start\_motion\_shake  
    * 0 to 1 value. The amount of shake that should happen when motion is started   
  * end\_motion\_shake  
    * 0 to 1 value. The amount of shake that should happen when motion is ended  
  * constant\_motion\_shake  
    * 0 to 1 value. The amount of shake that should happen when motion is playing  
  * reverb\_level  
    * The amount of reverb that should play when moving. See `play_sound`  
  * reverse\_motion\_duration  
    * If reverse duration is different than `duration`, set this value  
  * dont\_play\_stop\_sound\_for\_reverse\_motion  
    * 1: Don’t play sound reverse motion  
    * 0: Do play sound for reverse motion  
  * end\_motion\_target\_func  
    * The function to be called on `end_motion_target` when motion is ended  
  * should\_knock  
    * the mover will play a door knocking sound while untriggered, as if there is someone behind it  
    * 1: play the sound  
  * one\_more\_message  
    * When trigger\_count \> 2 and the entity has been triggered trigger\_count \- 1 times, this message will be shown  
  * disable\_collider\_on\_move  
    * Whether the collider should be disabled on move  
  * should\_loop  
    * Similar to `oscillate` except it teleports back to the beginning and immediately starts again when it reaches its terminal position  
  * ease\_type  
    * valid types are EASE\_IN\_OUT, EASE\_OUT\_IN, EASE\_IN, EASE\_OUT  
  * trans\_type  
    * valid types are TRANS\_BACK, TRANS\_BOUNCE, TRANS\_QUAD, TRANS\_QUINT, TRANS\_QUART, TRANS\_ELASTIC  
  * is\_wet  
    * Determines if a wet sound is played for this mover  
    * 1: yes  
  * player\_only\_world\_collision  
    * If the player is the only thing that should collide with this  
    * 1: yes  
    * 0: no

### vt\_oob\_area

* deprecated

### vt\_secret\_area

* Will notify the player that they found a secret when this area is entered  
* key properties  
  * secret\_name  
    * Required. Make sure to give it a unique name for the map.

### vt\_spinner\_solid

* A piece of geometry that will spin. Use the origin texture to set the origin of the geometry which determines the pivot of the spin. Otherwise it will just spin around the center of the geometry in the direction of the `rotation_axis`  
* key properties  
  * speed  
  * radius  
  * rotation\_axis

### vt\_toast\_area

* An area that displays dialogue on the screen when the player enters the area  
* key properties  
  * toast\_text  
  * should\_pause  
  * time\_scale  
  * toast\_type  
    * use the dropdown  
  * display\_condition  
    * Only displays if this condition has been met, possible options are  
      * has\_not\_yet\_been\_triggered  
      * has\_not\_yet\_been\_triggered\_and\_is\_godly  
  * is\_tutorial  
  * targetname  
  * full\_speed\_action  
  * should\_squash

### vt\_trigger\_area

* an area that will trigger the specified `target` when entered   
* key properties  
  * target  
    * The entity that should be triggered when this area is entered  
  * target\_func  
    * the function on the target that should be called  
  * trigger\_dependency\_count  
    * The amount of times this area must be triggered before it will emit a trigger when entered  
  * targetname  
    * use this to trigger the area corresponding to trigger\_dependency\_count  
  * required\_keys\_comma\_sep  
    * The keys that are required for this trigger area to trigger the target when entered. See `key_name` property on vt\_key  
    * required\_artifacts\_comma\_sep  
      * The artifact parts that must be collected for this trigger area to trigger the target when entered.   
    * trigger\_delay  
    * show\_locked\_message  
      * 0: Will not show any message when the player doesn’t have the required keys   
    * trigger\_once  
      * 1: When this area is entered consecutive times, it will not trigger the target again  
      * 0: When this area is entered consecutive times, it triggers the target each time  
    * exit\_target  
      * The target to trigger when this area is exited  
    * exit\_target\_func  
      * The target function to call  
    * is\_enemy\_trigger  
      * 1: This trigger area triggers when enemies enter it, instead of when the player enters it. 

### vt\_water

* Creates water that the player can swim in

## Pro Tips

### Clip Textures and water

Water and lava are prone to weird visual artifacts, like this 
![Bad water](attachments/bad_water.png)
You can prevent this by clipping the top / exposed parts of the water or lava  
![clip_brush.png](attachments/clip_brush.png)

You can do this by making the whole brush a clip brush, then shift-clicking the faces you want to make the water texture, and selecting the water texture

### Use a hotkey for clip texture

You will use the clip texture a lot. I assigned a hotkey so I don’t have to find the clip texture every time I need to apply it to something. Go to view \-\> preferences \-\> keyboard and find “Tags/turn selection into Clip” and assign that to your key of choice. I used backtick (\`). 

## Common Issues

### Random parts of my map stopped working for no reason

This issue is usually caused by empty properties in various entities. For example, if one of your entities has “property 1” in it, you should remove that. Sometimes this can happen if you hit the plus sign to add a property and forget to remove it later. **If you suspect this could be the issue you can hit ctrl \+ A to select all entities and look at the properties panel to see if you see any strange / bad looking properties in your entire map.**

### Geometry / Meshes becoming invisible behind materials with transparency

This is due to occlusion culling. The mesh in front is culling the mesh behind. If you don’t want the mesh in front to do any culling, make it a [func\_detail or func\_detail\_illusionary](#func_detail)  
![render_bad.gif](attachments/render_bad.gif)
