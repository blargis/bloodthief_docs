# Bloodthief Mapping Guide
This guide is meant to be used like a wiki for you to reference for all your mapping needs. Trenchbroom is the software that is used to make Bloodthief maps. It is free, open source, and used to make maps for many games, such as Quake, Dusk, Wrath: Aeon of Ruin, and many more. Trenchbroom is great because it’s specifically designed for making interactive maps, which makes getting started making a real level easy, but the possibilities are still limitless!

## Get Started
* [Watch the official get started tutorial](https://youtu.be/09mth4fUaH0)
* [Bloodthief mapping assets](https://drive.google.com/file/d/1EJCwpfn2qqMdu4Z0kc1seRDttNC1SqMr/view?usp=drive_link)
* [Example Map - Time Tomb](https://drive.google.com/file/d/1ug1_SbQ-79RKrOdk9USPT0Q1SCSGNpa7/view?usp=drive_link)
* [Trenchbroom Manual](https://trenchbroom.github.io/manual/latest/)
* [Dumptruck_ds Trenchbroom Tutorial Series](https://www.youtube.com/watch?v=gONePWocbqA&list=PLgDKRPte5Y0AZ_K_PZbWbgBAEt5xf74aE&index=1)
* [Entity Reference](/entity-reference)


## Getting Set Up
1. Download [Trenchbroom](https://github.com/TrenchBroom/TrenchBroom/releases/tag/v2025.3)
2. Navigate to the folder where you downloaded Trenchbroom and click inside the Trenchbroom folder. Click inside the "games" folder. Download the [Bloodthief mapping assets](https://drive.google.com/file/d/1EJCwpfn2qqMdu4Z0kc1seRDttNC1SqMr/view?usp=drive_link). Unzip it, open it, and drag the "BloodthiefMapping" folder into the "games" folder mentioned above
3. Now open up the Trenchbroom.exe which is at the root of the trenchbroom folder
4. Click New Map, then click Open Preferences
5. You should see BloodthiefMapping as an option. Click it, and on the righthand side set the "Game Path" to the BloodthiefMapping folder that you put inside the games folder in step 2. So if you downloaded Trenchbroom to your Desktop, the path might be C:\users\yourname\Desktop\TheTrenchbroomFolderName\games\BloodthiefMapping
6. Hit Apply, then OK.
7. Now you're ready to start mapping! Open the game, hit Play, go to the My Maps tab and hit "Create New Map". When the map starts, in the pause menu you should see an option to "Open Map Data Folder". When you open that map, you should see a .map file. Open that file in Trenchbroom! (see next section)

!!!info "Important Tip"
	#### Opening Map Files in Trenchbroom
	You can either open Trenchbroom normally, then click File -> Open Document and find the map file in the folder in Step 8 above, or you can set up Trenchbroom to be the "default program" for MAP files that way when you double click on your map file in the file explorer, and your map automatically opens in Trenchbroom.

	#### Setting Trenchbroom to be the "default program" for MAP files.
	1. Right click on the MAP file in Step 8 of [Getting Set Up](getting-set-up) and hover over "Open With" and click "Choose another app". 
	2. Scroll down to "More Apps" 
	3. Scroll Down to "Look for another app on this PC"
	4. Locate where you downloaded Trenchbroom, click on the Trenchbroom.exe file and hit "Open". Now MAP files will automatically open with Trenchbroom when you double click them. 

## FAQs
### Why does water look weird sometimes?
Water and lava are prone to weird visual artifacts, like this:
![Bad water](attachments/bad_water.png)

You can prevent this by clipping the top/exposed parts of the water or lava.
![clip_brush.png](attachments/clip_brush.png)

You can do this by making the whole brush a clip brush, then shift-clicking the faces you want to make the water texture, and selecting the water texture.

You will use the clip texture a lot. I assigned a hotkey so I don’t have to find the clip texture every time I need to apply it to something. Go to view -> preferences -> keyboard and find “Tags/turn selection into Clip” and assign that to your key of choice. I used backtick (`).

### Why is enemy navigation / pathfinding not working? 
When your map is really big, navigation can start to perform poorly and overall just start to work badly if you don't do any optimization. Take this example

![nav_e1.png](attachments/nav_e1.png)
In this example, I am running the game in debug mode so I can see all of the navigable area (unfortunately this isn't possible for mappers to do, but it is useful for this example nonetheless). 

By default **everything is navigable**. For this example we have an enemy in a playable area with some obstacles, with big red walls on the side. Notice how the tops of the big red walls are blue, showing that the tops of the walls are navigable. This is wasteful and causes enemy navigation to take longer for no good reason, because no enemies are ever going to get up there! Ideally only places where enemies actually need to traverse are navigable. 

We can optimize this by explicitly specifying the areas we want to be navigable. First we must select the ground floor and make it a `func_geo` entity. `func_geo` has more features than the default brush type which is `worldspawn`. We will then give the ground a property `navigable` with value `1`. This will switch the map builder to a new mode, where now *only geometry specified to be navigable* will be treated as such. If we build we get this. Notice the tops of the walls are no longer blue. But now we have a new problem!

![attachments/nav_e2.png](attachments/nav_e2.png)
If you look closely, our ground region is no longer snaking around the obstacles, it is going right through them - so the enemy will not avoid the obstacles and will try to run right through them. We can fix this by selecting the inner obstacles and making them `func_detail` entities and setting the `navigable` property to `1` for those. Then we get this:
![nav_e3.png](attachments/nav_e3.png)
Now the region is properly snaking around the obstacles. Note that we made the inner obstacles `func_detail`, but `func_geo` would have worked also. I chose `func_detail` because our obstacles have transparent materials. func_detail entities don't cull objects behind them, so it is good to use that entity when using transparent materials. See [Geometry becoming invisible behind materials with transparency](#geometry-becoming-invisible-behind-materials-with-transparency)


### My map is completely broken suddenly. What happened??
This issue is usually caused by empty properties in various entities. For example, if one of your entities has “property 1” in it, you should remove that. Sometimes this can happen if you hit the plus sign to add a property and forget to remove it later. If you suspect this could be the issue you can hit ctrl + A to select all entities and look at the properties panel to see if you see any strange / bad looking properties in your entire map.

### Why is geometry becoming invisible behind materials with transparency?
This is due to occlusion culling. The mesh in front is culling the mesh behind. If you don’t want the mesh in front to do any culling, make it a func_detail or func_detail_illusionary

![render_bad.gif](attachments/render_bad.gif)


### How do I set up shielded enemies?
You can give an enemy a shield simply by adding a `bubble_shield_id` property to that enemy and giving the property *any value*.

If you want a mage to be the source of the shield, so when you kill the mage, the shield goes away, assign the enemy a `targetname` of any value, and assign the mage a `target` of the same value. 

#### Mages that shield multiple enemies at once
Simply give all the enemies shielded by a mage the same `bubble_shield_id` and the same `targetname`. Note that enemies with a different `targetname` but the same `bubble_shield_id` will still lose their shields when the mage dies that is shielding other enemies with the same `bubble_shield_id`.


### How do I lock a door so one or more keys is required to open it?
1. Place a `vt_key_pickup` entity and give it a unique `key_name`, such as `key1`
2. Create a `vt_mover` - this will be your door so give it `tb_translation` `0 0 320` to have it go up 320 Trenchbroom Units when activated. Give it targetname `door1`
3. Create a `vt_trigger_area` and give it a `target` of `door1` 
4. Now the door will open when we go in the trigger area-  but we want to require that you have the key first!
5. To make it so the key is required, put your unique key name in the `required_keys_comma_sep` field of the vt_trigger_area. Now the trigger wont fire until you have the key. 
6. To require multiple keys, simply put them all in the `required_keys_comma_sep` field, separated by a comma, like this `key1,key2,key3,key4`. Now all 4 of those keys will be required to open the door. Make sure there is a corresponding `vt_key_pickup` with `key_name` set for each of those 4 keys!  

### How do I use custom textures in my map?

1. Go to the `textures` folder inside your `BloodthiefMapping` game folder (the one you set up in [Getting Set Up](getting-set-up)). Create a new folder there called `custom`.
2. Put your texture image files inside that `custom` folder. They'll now show up in Trenchbroom's texture browser under `custom/` so you can paint your brushes with them.
3. To make the textures actually appear in-game, copy that entire `custom` folder into your map's folder, inside a folder called `textures`. So the final structure should look like this:

```
<your map folder>/
	YourMap.map
	textures/
		custom/
			your_texture.png
			another_texture.png
```

You can open your map's folder from the pause menu in-game via "Open Map Data Folder". Once the `textures/custom` folder is in place, your custom textures will render when you play the map, and they'll automatically travel with the map if you upload it to the Steam Workshop.

!!!info "Tip"
	Keep your custom textures inside the `custom` folder (not loose in `textures`) so the name you paint with in Trenchbroom (e.g. `custom/your_texture`) matches what the game looks for.

### How do I link maps together (map bundles)?
You can link maps so that beating one drops you straight into the next when you hit Continue on the end level screen. This is how you'd make a hub world, or a few levels in a row.

Make all your maps normally first and get them working on their own. Then pick one to be the "root map" (the one people launch and see in the maps list) and the rest become "submaps" that you only reach by going through another map.

1. In the root map's folder, make a folder called `submaps`.
2. Copy each submap's folder into it, so you end up with:

```
hub_map/
	hub_map.map
	hub_map_data.json
	textures/
	submaps/
		submap1/
			submap1.map
			submap1_data.json
			textures/
		submap2/
			submap2.map
			submap2_data.json
```

3. Open the root map in Trenchbroom and find the `vt_end_level_area` you want to lead somewhere. Add a `next_map` property and set it to the path of the next map, relative to the root folder and without the `.map`. For the layout above, going to submap1 is `submaps/submap1/submap1`.

Now when you reach that end level area and hit Continue, it loads submap1.

You can do this from any map in the bundle, including pointing back at the hub:

* submap to another submap: `submaps/submap2/submap2`
* back to the hub: just `hub_map` (the root map sits at the top, so its path is just its name)

So a hub is the hub map pointing out to each submap, and each submap pointing back with `hub_map`.

A few things to watch out for:

* Like any map, a submap's `.map` and `_data.json` have to share a name (`submap1.map`, `submap1_data.json`). That's already true for maps you made normally.
* Every map name in the bundle has to be unique, and no submap can have the same name as the root, or their saves and leaderboards will clash.
* If a submap doesn't have its own `textures/` folder it'll just use the root's.

You only upload the root map. Everything in `submaps/` rides along with it, and every map gets its own leaderboard once it's on the Workshop.

### Why is the collision for my vt_breakable not working? 
Breakables need to be **one brush per breakable**. For example, this will not work:


![Breakables](attachments/bad_breakable.png)

Notice how there are two shapes/brushes, but both are assigned to one overarching "breakable" entity. You need to break these up into two breakables. You can do this by clicking on one of the shapes and assigning that singular shape to it's own breakable. Now it will look like this, which is correct:

![good_breakable](attachments/good_breakable.png)