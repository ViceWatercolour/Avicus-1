*Keep in mind [the docs](docs.avicus.net) when building your YML*

First, you do some basic YML things like the info section, loadouts, and drop modifications
```
info:
  title: Fossil Canyon (CTF)
  world: FossilCanyonCTF
  version: 1.0
  type: ctw
  creators:
  - timaeusTestified
  contributors:
  - steven5703
  spawn: 22.5,122,4.5,90,0
  ```
Make sure that the `type:` is set to `ctw`
Loadout can be changed to your liking!
```
repair-drops:
- iron sword
- bow
remove-drops:
- leather helmet
- leather chestplate
- leather leggings
- leather boots
loadout:
  effects:
  - damage resistance:5,5
  helmet:
    item: leather_helmet
  chestplate:
    item: leather_chestplate
  leggings:
    item: leather_leggings
  boots:
    item: leather_boots
  0:
    item: iron sword
  1:
    item: bow
    enchants:
    - arrow_infinite:1
  2:
    item: golden_apple
    amount: 3
  8:
    item: steak
    amount: 6
  28:
    item: arrow
    amount: 1
```
This is the teams part, and this is when it starts to get tricky.
```
teams:
  red:
    spawn: -66.5,72,-84.5,-45,0
    title: Red Team
    max: 25
    wools:
      red:
        name: Red Flag
        chest: 7,63,-3
        monument: -35,73,-33
  purple:
    spawn: -7.5,72,91.5,135,0
    title: Purple Team
    max: 25
    wools:
      purple:
        name: Purple Flag
        chest: 7,63,-6
        monument: -40,73,39
```
Of course, you can customize the team name, the spawn, title, max, flag color, flag name, ect.
But what is important is `chest:`. You must hide two chests anywhere in the map (don't go far away from the map and load chunks and put it there).
It doesn't matter where, just make sure that no one can reach it. Put the coords of the chest in `monument:` for each team.
I'm not actually sure if you need to have a chest or put a random coord, but just do that to be sure.
The `monument:` is just where you would place the wool, like a standard CTW map.
```
regions:
  global:
    type: global
    flags:
      build:
        who: '*'
        message: '&7[&8&lCTF&r&7] &cYou cannot build on CTF maps!'
        triggers:
          ignite_tnt:
            delay: 3
            block-damage: false
      kill_player:
        who: '*'
        triggers:
          give_loadout:
            loadout:
              2:
                item: golden_apple
```
You can make it if you can build or not, that's your choice.
```
  boundary:
    type: cuboid
    min: 5,88,104
    max: -79,63,-98
    invert: true
    flags:
      build:
        who: '*'
        message: '&cYou may not build beyond this map''s restriction boundaries.'
```
  purple-wool:
    type: cuboid
    min: -7,69,-83
    max: -5,69,-85
    flags:
      enter:
        who: 'purple'
        allow: true
        message: '&7[&8&lCTF&r&7] &aYou have been given the &9PURPLE &awool! Run to your victory monument on your team''s side!'
        triggers:
          give_loadout:
            loadout:
              effects:
              - speed:2,10
              0:
                item: wool:10
  red-wool:
    type: cuboid
    min: -70,69,91
    max: -68,69,89
    flags:
      enter:
        who: 'red'
        allow: true
        message: '&7[&8&lCTF&r&7] &aYou have been given the &4RED &awool! Run to your victory monument on your team''s side!'
        triggers:
          give_loadout:
            loadout:
              effects:
              - speed:2,10
              0:
               item: wool:14
  red-tele:
    type: cuboid
    min: -74,72,-84
    max: -74,74,-83
    flags:
      enter:
        who: 'red'
        allow: true
        message: '&aSuccessfuly teleported, but you got some &c&ostrange side effects...'
        triggers:
          teleport:
            to: -15.5,77.5,-64.5,-150,20
          give_loadout:
            loadout:
              effects:
              - wither:2,5
              - confusion:1,10
              - slow:1,10
  purple-tele:
    type: cuboid
    min: 0,72,90
    max: 0,74,89
    flags:
      enter:
        who: 'purple'
        allow: true
        message: '&aSuccessfuly teleported, but you got some &c&ostrange side effects...'
        triggers:
          teleport:
            to: -58.5,77.5,71.5,30,20
          give_loadout:
            loadout:
              effects:
              - wither:2,5
              - confusion:1,10
              - slow:1,10
