# Escaping Logic — Room E: Last Door

### @explicitHints true

## Room E

This Recipe covers constructions **31–36**. If this room is not open in the game yet, [finish Room D: Bridge Room first](#recipe:https://github.com/mrbrackebusch-code/escaping-logic/docs/tutorials/escaping-logic-room-d-bridge-room).

## 31. Open a shutter route

The shutter bank needs a sensor card. Build ``||escapeLab(noclick):when [(E) shutter bank] is operated||`` first: if `is (E) WindowA` **or** `is (E) WindowB`, make `(E) ShutterOpen`; else if `is (E) DangerousControl`, make `(E) ShutterWarn`; otherwise make `(E) ShutterClosed`. Its closed response points to the sensor mapper. Keep the usable-window rule first so it stays the main path.

### What the mechanism does

![What the mechanism does for Shutters](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/195095bc6924706a/media/gameplay/31-shutters-connected-v2-physical-v7-01-31-shutters.gif)

#### ~ tutorialhint

```blocks
let pressureReady = escapeLab.is(EscapeFact.PressureReady)

let angle = escapeLab.number(EscapeMeter.PitchAngle)

escapeLab.onAttempt(EscapeBeat.Shutters, function () {
    if (escapeLab.is(EscapeFact.WindowA) || escapeLab.is(EscapeFact.WindowB)) escapeLab.make(EscapeAction.ShutterOpen)
    else if (escapeLab.is(EscapeFact.DangerousControl)) escapeLab.make(EscapeAction.ShutterWarn)
    else escapeLab.make(EscapeAction.ShutterClosed)
})
```

## 32. Map the remote sensors

In ``||escapeLab(noclick):when [(E) sensor map] is operated||``, use an else-if chain on `value of (E) SensorNumber`: `1` makes `(E) SensorLamp1`, `2` makes `(E) SensorLamp2`, `3` makes `(E) SensorLamp3`, and the final else makes `(E) SensorDark`. Hold **B** at the map pad and use **left/right** to select the sensor number shown by the shutter wiring; press **A** to map it. A sensor card appears on the tray; release **B** to walk. Carry it to the shutter-bank pad and fit it. Return to the bank, hold **B**, and use **left/right** to select `WINDOW A` or `WINDOW B`; press **A** to run your shutter rule, then release **B**. Either window can open the route.

### What the mechanism does

![What the mechanism does for Sensors](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/195095bc6924706a/media/gameplay/32-sensors-connected-v2-physical-v7-01-32-sensors.gif)

#### ~ tutorialhint

```blocks
let pressureReady = escapeLab.is(EscapeFact.PressureReady)

let angle = escapeLab.number(EscapeMeter.PitchAngle)

escapeLab.onAttempt(EscapeBeat.Sensors, function () {
    if (escapeLab.number(EscapeMeter.SensorNumber) == 1) escapeLab.make(EscapeAction.SensorLamp1)
    else if (escapeLab.number(EscapeMeter.SensorNumber) == 2) escapeLab.make(EscapeAction.SensorLamp2)
    else if (escapeLab.number(EscapeMeter.SensorNumber) == 3) escapeLab.make(EscapeAction.SensorLamp3)
    else escapeLab.make(EscapeAction.SensorDark)
})
```

## 33. Cross the rock path

The rock path is dark until it has a pattern plate. Build ``||escapeLab(noclick):when [(E) rock path] is operated||`` now from the visible clue: **keep the color, change the pattern**. Join `is (E) SameColor` and `not is (E) SamePattern` with **and**. Make `(E) RockBeam` for true and `(E) RockCollapse` otherwise. The unlit path points to the constellation controls, where a matching choice can make the plate.

### What the mechanism does

![What the mechanism does for RockPath](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/195095bc6924706a/media/gameplay/33-rock-path-connected-v2-physical-v7-01-33-rock-path.gif)

#### ~ tutorialhint

```blocks
let pressureReady = escapeLab.is(EscapeFact.PressureReady)

let angle = escapeLab.number(EscapeMeter.PitchAngle)

escapeLab.onAttempt(EscapeBeat.RockPath, function () {
    if (escapeLab.is(EscapeFact.SameColor) && !escapeLab.is(EscapeFact.SamePattern)) escapeLab.make(EscapeAction.RockBeam)
    else escapeLab.make(EscapeAction.RockCollapse)
})
```

## 34. Light the constellation

In ``||escapeLab(noclick):when [(E) constellation] is operated||``, join `is (E) FrontMatch`, `is (E) MiddleMatch`, and `is (E) BackMatch` with **and**. Make `(E) StarIgnite` only when all three pass; otherwise make `(E) StarFizzle`. At the constellation pad, hold **B** and use **left/right** to select the single visible `ALL MATCH` option; press **A** once to run your rule, then release **B**. This one choice sets all three match facts for this beat. A pattern plate appears on the tray when your rule makes `(E) StarIgnite`. Carry it to the rock-path pad and fit it, then return to the rock-path pad, hold **B**, and use **left/right** to choose the same color with a different pattern; press **A** to cross, then release **B**.

### What the mechanism does

![What the mechanism does for Constellation](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/195095bc6924706a/media/gameplay/34-constellation-connected-v2-physical-v7-01-34-constellation.gif)

#### ~ tutorialhint

```blocks
let pressureReady = escapeLab.is(EscapeFact.PressureReady)

let angle = escapeLab.number(EscapeMeter.PitchAngle)

escapeLab.onAttempt(EscapeBeat.Constellation, function () {
    if (escapeLab.is(EscapeFact.FrontMatch) && escapeLab.is(EscapeFact.MiddleMatch) && escapeLab.is(EscapeFact.BackMatch)) escapeLab.make(EscapeAction.StarIgnite)
    else escapeLab.make(EscapeAction.StarFizzle)
})
```

## 35. Synchronize the restored systems

The synchronizer receives the power, pressure, and signal you restored in earlier rooms. In ``||escapeLab(noclick):when [(E) synchronizer] is operated||``, join `is (E) PowerReady`, `is (E) PressureSystemReady`, `is (E) SignalReady`, and `not is (E) AlarmOn` with **and**. Make `(E) SyncLock` when all four requirements pass and `(E) SyncReject` otherwise. With the shutter route and rock bridge complete, press **A** at the synchronizer to run your rule; do not hold **B**. When the rule makes `(E) SyncLock`, an interlock key appears on the tray. Pick it up, carry it to the final-lever pad, and press **A** to fit it.

### What the mechanism does

![What the mechanism does for Synchronize](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/195095bc6924706a/media/gameplay/35-synchronize-connected-v2-physical-v7-01-35-synchronize.gif)

#### ~ tutorialhint

```blocks
let pressureReady = escapeLab.is(EscapeFact.PressureReady)

let angle = escapeLab.number(EscapeMeter.PitchAngle)

escapeLab.onAttempt(EscapeBeat.Synchronize, function () {
    if (escapeLab.is(EscapeFact.PowerReady) && escapeLab.is(EscapeFact.PressureSystemReady) && escapeLab.is(EscapeFact.SignalReady) && !escapeLab.is(EscapeFact.AlarmOn)) escapeLab.make(EscapeAction.SyncLock)
    else escapeLab.make(EscapeAction.SyncReject)
})
```

## 36. Pull the final lever

In ``||escapeLab(noclick):when [(E) final lever] is operated||``, test `value of (E) CoreLights = 3` **and** `not is (E) AlarmOn`. Make `(E) LeverPull` when it passes and `(E) LeverReject` otherwise. After you fit the interlock key, press **A** at the final lever to run this rule; do not hold **B**. At the first ending, press **B** to start the full replay. It clears room and mechanism checkpoints while retaining first-clear history; a second escape receives its distinct ending.

### What the mechanism does

![What the mechanism does for FinalLever](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/195095bc6924706a/media/gameplay/36-final-lever-connected-v2-physical-v7-01-36-final-lever.gif)

#### ~ tutorialhint

```blocks
let pressureReady = escapeLab.is(EscapeFact.PressureReady)

let angle = escapeLab.number(EscapeMeter.PitchAngle)

escapeLab.onAttempt(EscapeBeat.FinalLever, function () {
    if (escapeLab.number(EscapeMeter.CoreLights) == 3 && !escapeLab.is(EscapeFact.AlarmOn)) escapeLab.make(EscapeAction.LeverPull)
    else escapeLab.make(EscapeAction.LeverReject)
})
```

## What you used

You used native ``||logic(noclick):if then else||`` blocks for visible two-way reactions, then used **else if**, **and**, **or**, and **not** when a physical mechanism needed more cases or requirements. `pressureReady` and `angle` remember choices that a nearby later mechanism needs. Every room keeps its mechanisms available for local retesting, and the second completion gives you a fresh ending to reach.

## Replay or review

At the game's first ending, press **B** to begin the built-in full replay. To review instructions for a construction, open its room Recipe directly: [Room A](#recipe:https://github.com/mrbrackebusch-code/escaping-logic/docs/tutorials/escaping-logic-room-a-workshop), [Room B](#recipe:https://github.com/mrbrackebusch-code/escaping-logic/docs/tutorials/escaping-logic-room-b-light-gallery), [Room C](#recipe:https://github.com/mrbrackebusch-code/escaping-logic/docs/tutorials/escaping-logic-room-c-garden-room), [Room D](#recipe:https://github.com/mrbrackebusch-code/escaping-logic/docs/tutorials/escaping-logic-room-d-bridge-room), or [Room E](#recipe:https://github.com/mrbrackebusch-code/escaping-logic/docs/tutorials/escaping-logic-room-e-last-door).
