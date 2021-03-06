# Map Transitions

(Will document this at some point in the future)

# Warp Stones

Note: This refers to the warp stones which bring up the warp stone select menu. The warpstone at plurkwood/forest night is not included.

A warp stone event has ID `32`. Which warp stone it is is specified by a type specifier event (i.e. ID+5000) just above the warp stone.

For example, the town warp stone has ID 5. The warp stone event is thus laid out like this:

```
+----+
|5005|
|----|
| 32 |
+----+
```

Each warp stone in Rabi-Ribi has a different ID.


### How Warp Stones work
**Short explanation**: The map you warp to is hardcoded in game. The actual location within the map depends on warp stone placement in map. If the target warp stone does not exist, you still warp but stay on the same tile.

**Proper explanation using an example**:
- Lets say from some other warp stone, you select Spectral Cave as your warp destination.
- According to the game's code, Spectral Cave is located in area0.
- Thus the game checks area0 and looks for the Spectral Cave warp stone.
    - If it finds the Spectral Cave warp stone in area0, it puts you at the location of the warp stone.
    - If it can't find the Spectral Cave warp stone in area0, it warps you to area0 anyway, but in the same tile as you were in before. We refer to this as a wrong warp.

# Direct Warps

Note: This refers to warps that directly bring you to another location, like the warp stone to plurkwood and the computer warp to system interior.

This can be used to:
1. Take the player to another map. (CROSS MAP X)
2. Take the player to another location, but in the same map. (CROSS MAP OFF)

**Event ID 208: Warp Entrance**
- This should be placed on the ground. The player presses Down while on the event tile to use the warp.
- The destination Tele ID and Map must be set before using the warp.
- A common practice is to surround the entrance with the Tele ID and Cross Map events.
   - This warp brings you to Map 8, Tele ID 4.
    ```
    +-----+-----+-----+-----+-----+
    | 250 | 250 | 250 | 250 | 250 | 
    |-----|-----|-----|-----|-----| 
    | 250 | 213 | 213 | 213 | 250 | 
    |-----|-----|-----|-----|-----| 
    | 250 | 213 | 208 | 213 | 250 | 
    +-----+-----+-----+-----+-----+
    ```

**Event ID 240: Warp Exit**
- The Tele ID event must be placed directly above the Warp Exit event.
    - This is a Tele ID 4 warp exit:
    ```
    +-----+
    | 213 |
    |-----|
    | 240 |
    +-----+
    ```

### Tele ID and Cross Map Events

- If you touch a Tele ID X event, the next warp you take will bring you to warp exit X.

- If you touch a CROSS MAP Y event, the next warp you take will bring you to map Y.

- If warp exit X does not exist in map Y, the warp will put you in the same location, but in map Y (wrong warp).

#### Tele ID Events:
```
209 - Tele ID 0
210 - Tele ID 1
211 - Tele ID 2
212 - Tele ID 3
213 - Tele ID 4
214 - Tele ID 5
215 - Tele ID 6
216 - Tele ID 7
217 - Tele ID 8
218 - Tele ID 9
219 - Tele ID 10
220 - Tele ID 11
```

#### Cross Map Events:
```
241 - CROSS MAP OFF
242 - CROSS MAP 0
243 - CROSS MAP 1
244 - CROSS MAP 2
245 - CROSS MAP 3
246 - CROSS MAP 4
247 - CROSS MAP 5
248 - CROSS MAP 6
249 - CROSS MAP 7
250 - CROSS MAP 8
251 - CROSS MAP 9
```
Note: If you touch CROSS MAP OFF, the next warp stone will not warp you to a different map.

**Event ID 112: Warp Stone Graphic**
  - Places a warp stone graphic 3 tiles below it. No actual effect on gameplay.
  - Only one warp stone can be placed per room
  
Note: Direct warps are disabled if the computer room background is used in the room. It is disabled until you trigger the event that activates the computer room.
