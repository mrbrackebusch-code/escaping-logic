# Escaping Logic

### @explicitHints true

## Welcome to the observatory

The observatory is awake, but its mechanisms only react to rules you write. You begin in the workshop, where the magnetic crank is at the upper left. Walk with the arrow keys. Near a mechanism, press **A** to open it; use **left/right** to choose a visible test input and **A** to operate it. At a mechanism with several parts, **up/down** selects the part. **B** returns directly to the room. In the review carrier, **Z** or **Space** is **A**, and **X** is **B**. Solved mechanisms stay available, so change your code and test again.

Your saved checkpoints make testing local: return to a solved mechanism and operate it again after changing a branch. Finish the six mechanisms in a room to use the right-hand portal. Previously reached rooms remain available.

Each rule begins with one ``||escapeLab(noclick):when [beat] mechanism is operated||`` event. The event supplies the moment to decide; your native ``||logic(noclick):if then else||`` blocks decide what the room does. The supplied world never supplies that decision.

## 1. Pull the magnetic crank

The crank is out of reach. Open the crank, operate it once without the magnet, choose the `LargeMagnet` input, then operate it again.

### Find these blocks

From **Escape Room**, use ``||escapeLab(noclick):when [Crank] mechanism is operated||``, ``||escapeLab(noclick):player has [LargeMagnet]||``, and ``||escapeLab(noclick):make [CrankPull] happen||``. From **Logic**, use ``||logic(noclick):if then else||``.

### Make your code look like this

Build the event, put `player has LargeMagnet` in the test, then put `make CrankPull happen` in the true branch and `make CrankTwitch happen` in the else branch.

### What you should see

When the magnet is present, the crank scrapes across and snaps into reach. Without it, it only twitches. The nested actions are the two possible visible answers to one test.

### Find the native Blocks

![Find the native Blocks for Crank](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/6425df7618b6c19a/media/menu/01-crank-01-crank-menu.svg)

### One possible construction

![One possible construction for Crank](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/6425df7618b6c19a/media/assembled/01-crank-01-crank-assembled.svg)

### What the mechanism does

![What the mechanism does for Crank](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/6425df7618b6c19a/media/gameplay/01-crank-lesson-01-crank.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.Crank, function () {
    if (escapeLab.has(EscapeItem.LargeMagnet)) escapeLab.make(EscapeAction.CrankPull)
    else escapeLab.make(EscapeAction.CrankTwitch)
})
```

## 2. Start the generator

The generator needs the hand crank. Reuse the same two-branch shape: test ``||escapeLab(noclick):player has [HandCrank]||``; make `GeneratorSpin` when true and `GeneratorSputter` otherwise. Operate it with and without the crank. The belts and lamps should wake only in the true branch.

### One possible construction

![One possible construction for Generator](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/6425df7618b6c19a/media/assembled/02-generator-02-generator-assembled.svg)

### What the mechanism does

![What the mechanism does for Generator](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/6425df7618b6c19a/media/gameplay/02-generator-lesson-02-generator.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.Generator, function () {
    if (escapeLab.has(EscapeItem.HandCrank)) escapeLab.make(EscapeAction.GeneratorSpin)
    else escapeLab.make(EscapeAction.GeneratorSputter)
})
```

## 3. Retract the release case

At the case, test ``||escapeLab(noclick):is [LockFree]||``. Make `CaseRetract` when it is true; make `CaseRattle` otherwise. Change the panel input and operate it twice. A free lock slides the glass away; a locked one rattles in place.

### One possible construction

![One possible construction for Case](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/6425df7618b6c19a/media/assembled/03-case-03-case-assembled.svg)

### What the mechanism does

![What the mechanism does for Case](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/6425df7618b6c19a/media/gameplay/03-case-lesson-03-case.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.Case, function () {
    if (escapeLab.is(EscapeFact.LockFree)) escapeLab.make(EscapeAction.CaseRetract)
    else escapeLab.make(EscapeAction.CaseRattle)
})
```

## 4. Suppress the fire

Test ``||escapeLab(noclick):player has [WaterCanister]||`` in the **Fire** event. Make `FireSteam` for the true branch and `FireFlare` for the else branch. The canister turns flame into steam; no canister makes the flame flare again.

### One possible construction

![One possible construction for Fire](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/6425df7618b6c19a/media/assembled/04-fire-04-fire-assembled.svg)

### What the mechanism does

![What the mechanism does for Fire](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/6425df7618b6c19a/media/gameplay/04-fire-lesson-04-fire.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.Fire, function () {
    if (escapeLab.has(EscapeItem.WaterCanister)) escapeLab.make(EscapeAction.FireSteam)
    else escapeLab.make(EscapeAction.FireFlare)
})
```

## 5. Repair the climbing wall

Use ``||escapeLab(noclick):value of [InstalledHolds]||`` with a native `= 4` comparison. If all four holds are installed, make `WallClimb` happen; otherwise make `WallFlash` happen. Add and remove a hold with the panel before testing both branches. Four holds lock into a route; fewer make the wall flash.

### One possible construction

![One possible construction for Wall](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/6425df7618b6c19a/media/assembled/05-wall-05-wall-assembled.svg)

### What the mechanism does

![What the mechanism does for Wall](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/6425df7618b6c19a/media/gameplay/05-wall-lesson-05-wall.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.Wall, function () {
    if (escapeLab.number(EscapeMeter.InstalledHolds) == 4) escapeLab.make(EscapeAction.WallClimb)
    else escapeLab.make(EscapeAction.WallFlash)
})
```

## 6. Filter the footprints

The panel shows a step value. Test whether `value of StepValue + 3 ≤ 10`. Keep a safe print with `FootprintKeep`; drop an unsafe one with `FootprintDrop`. Try a value on each side of the boundary. The catwalk lights for a kept print and breaks under a dropped one.

### One possible construction

![One possible construction for Footprints](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/6425df7618b6c19a/media/assembled/06-footprints-06-footprints-assembled.svg)

### What the mechanism does

![What the mechanism does for Footprints](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/6425df7618b6c19a/media/gameplay/06-footprints-lesson-06-footprints.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.Footprints, function () {
    if (escapeLab.number(EscapeMeter.StepValue) + 3 <= 10) escapeLab.make(EscapeAction.FootprintKeep)
    else escapeLab.make(EscapeAction.FootprintDrop)
})
```

## 7. Reveal the shadow panel

Make the **Shadow** event test `value of Illumination ≥ 60`. Use `ShadowReveal` when it passes and `ShadowHide` when it does not. Move the illumination control below and above `60`. The hidden geometry fades in and out where your condition says it should.

### One possible construction

![One possible construction for Shadow](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/6425df7618b6c19a/media/assembled/07-shadow-07-shadow-assembled.svg)

### What the mechanism does

![What the mechanism does for Shadow](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/6425df7618b6c19a/media/gameplay/07-shadow-lesson-07-shadow.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.Shadow, function () {
    if (escapeLab.number(EscapeMeter.Illumination) >= 60) escapeLab.make(EscapeAction.ShadowReveal)
    else escapeLab.make(EscapeAction.ShadowHide)
})
```

## 8. Move portrait one

The first panel labels the choices **LEFT SHOE = 1** and **RIGHT SHOE = 2**. Test ``||escapeLab(noclick):value of [ShoeSide]||`` = `1`; make `PortraitLeft` when true and `PortraitRight` otherwise. The first portrait rolls along its rail each time you operate the panel.

### What the mechanism does

![What the mechanism does for Portrait1](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/6425df7618b6c19a/media/gameplay/08-portrait1-lesson-08-portrait1.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.Portrait1, function () {
    if (escapeLab.number(EscapeMeter.ShoeSide) == 1) escapeLab.make(EscapeAction.PortraitLeft)
    else escapeLab.make(EscapeAction.PortraitRight)
})
```

## 9. Move portrait two

Make a separate **Portrait2** event. Copy the portrait-one pattern, then change only the event to Portrait2. Test both shoe sides. This separate stack lets you compare the two rules if one portrait moves incorrectly.

### What the mechanism does

![What the mechanism does for Portrait2](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/6425df7618b6c19a/media/gameplay/09-portrait2-lesson-corrected-09-portrait2.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.Portrait2, function () {
    if (escapeLab.number(EscapeMeter.ShoeSide) == 1) escapeLab.make(EscapeAction.PortraitLeft)
    else escapeLab.make(EscapeAction.PortraitRight)
})
```

## 10. Move portrait three

Create the **Portrait3** event and adapt the same condition and actions. Operate portrait three with each shoe side. Its motion is independent of the first two portraits.

### What the mechanism does

![What the mechanism does for Portrait3](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/6425df7618b6c19a/media/gameplay/10-portrait3-lesson-corrected-10-portrait3.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.Portrait3, function () {
    if (escapeLab.number(EscapeMeter.ShoeSide) == 1) escapeLab.make(EscapeAction.PortraitLeft)
    else escapeLab.make(EscapeAction.PortraitRight)
})
```

## 11. Move portrait four

Create the **Portrait4** event and use the same left/right rule. Test each direction. Four small parallel stacks make the repeated decision easy to inspect and repair.

### What the mechanism does

![What the mechanism does for Portrait4](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/6425df7618b6c19a/media/gameplay/11-portrait4-lesson-corrected-11-portrait4.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.Portrait4, function () {
    if (escapeLab.number(EscapeMeter.ShoeSide) == 1) escapeLab.make(EscapeAction.PortraitLeft)
    else escapeLab.make(EscapeAction.PortraitRight)
})
```

## 12. Mix the mural lights

The mural begins with a rule requiring two lights. An ``||logic(noclick):and||`` test passes only when **both** parts are true. In the **MuralMix** event, join ``||escapeLab(noclick):is [YellowOn]||`` and ``||escapeLab(noclick):is [BlueOn]||`` with that block. Make `MuralBlend` when both are true; otherwise make `MuralDim` happen. Turn each light on and off to see why both parts must pass.

### Find the native Blocks

![Find the native Blocks for MuralMix](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/6425df7618b6c19a/media/menu/12-mural-mix-12-mural-mix-menu.svg)

### One possible construction

![One possible construction for MuralMix](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/6425df7618b6c19a/media/assembled/12-mural-mix-12-mural-mix-assembled.svg)

### What the mechanism does

![What the mechanism does for MuralMix](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/6425df7618b6c19a/media/gameplay/12-mural-mix-lesson-12-mural-mix.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.MuralMix, function () {
    if (escapeLab.is(EscapeFact.YellowOn) && escapeLab.is(EscapeFact.BlueOn)) escapeLab.make(EscapeAction.MuralBlend)
    else escapeLab.make(EscapeAction.MuralDim)
})
```

## 13. Block the red light

Now adapt the mural rule. ``||logic(noclick):not||`` asks for the false case: `not is RedOn` passes only while the red light is off. Keep yellow **and** blue, and add that not test. When all three requirements pass, make `MuralOpen` happen; otherwise use `MuralSpill`. Red light is an active spoiler, so its condition must be false before the compartment opens.

### Find the native Blocks

![Find the native Blocks for MuralReveal](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/6425df7618b6c19a/media/menu/13-mural-reveal-13-mural-reveal-menu.svg)

### One possible construction

![One possible construction for MuralReveal](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/6425df7618b6c19a/media/assembled/13-mural-reveal-13-mural-reveal-assembled.svg)

### What the mechanism does

![What the mechanism does for MuralReveal](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/6425df7618b6c19a/media/gameplay/13-mural-reveal-lesson-corrected-13-mural-reveal.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.MuralReveal, function () {
    if (escapeLab.is(EscapeFact.YellowOn) && escapeLab.is(EscapeFact.BlueOn) && !escapeLab.is(EscapeFact.RedOn)) escapeLab.make(EscapeAction.MuralOpen)
    else escapeLab.make(EscapeAction.MuralSpill)
})
```

## 14. Seat the stone

Compare `value of StoneColor` and `value of SocketColor`. Equal values make `StoneSnap` happen; unequal values make `StoneRepel` happen. Select one matching and one mismatching stone. A correct stone snaps and glows; a wrong stone bounces back.

### What the mechanism does

![What the mechanism does for Stones](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/6425df7618b6c19a/media/gameplay/14-stones-lesson-14-stones.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.Stones, function () {
    if (escapeLab.number(EscapeMeter.StoneColor) == escapeLab.number(EscapeMeter.SocketColor)) escapeLab.make(EscapeAction.StoneSnap)
    else escapeLab.make(EscapeAction.StoneRepel)
})
```

## 15. Focus the telescope

Test whether `value of Zoom ≥ 3`. Make `TelescopeFocus` if it is true and `TelescopeBlur` otherwise. Try zoom `2`, then `3`. The lettering sharpens exactly when the threshold is met.

### What the mechanism does

![What the mechanism does for Telescope](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/6425df7618b6c19a/media/gameplay/15-telescope-lesson-15-telescope.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.Telescope, function () {
    if (escapeLab.number(EscapeMeter.Zoom) >= 3) escapeLab.make(EscapeAction.TelescopeFocus)
    else escapeLab.make(EscapeAction.TelescopeBlur)
})
```

## 16. Read the thermal trail

This panel has three visible outcomes. Use the **+** on ``||logic(noclick):if then else||`` to add an **else if** test after the first test is false. If `value of Temperature < 20`, make `ThermalBlue` happen. Add an **else if** for `Temperature > 40` and make `ThermalRed` happen. In the final else, make `ThermalAmber` happen. Test cold, amber, and hot values; the final else covers temperatures from `20` through `40`.

### One possible construction

![One possible construction for Thermal](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/6425df7618b6c19a/media/assembled/16-thermal-16-thermal-assembled.svg)

### What the mechanism does

![What the mechanism does for Thermal](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/6425df7618b6c19a/media/gameplay/16-thermal-lesson-16-thermal.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.Thermal, function () {
    if (escapeLab.number(EscapeMeter.Temperature) < 20) escapeLab.make(EscapeAction.ThermalBlue)
    else if (escapeLab.number(EscapeMeter.Temperature) > 40) escapeLab.make(EscapeAction.ThermalRed)
    else escapeLab.make(EscapeAction.ThermalAmber)
})
```

## 17. Test the magnetic sample

The sample spikes only when it is metallic **and** the magnet is on. Join `is Metallic` and `is MagnetOn` with **and**. Make `SampleSpike` if both pass; otherwise make `SampleFlat` happen. Change one input at a time before trying both together.

### What the mechanism does

![What the mechanism does for Sample](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/6425df7618b6c19a/media/gameplay/17-sample-lesson-17-sample.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.Sample, function () {
    if (escapeLab.is(EscapeFact.Metallic) && escapeLab.is(EscapeFact.MagnetOn)) escapeLab.make(EscapeAction.SampleSpike)
    else escapeLab.make(EscapeAction.SampleFlat)
})
```

## 18. Stop the titration at the target

Use a three-way decision. If `value of Drops < 7`, make `TitrationClear` happen. Else if `Drops ≤ 9`, make `TitrationBloom` happen. Else make `TitrationOverflow` happen. Run a low, target, and too-high drop count. The bloom range is the only successful middle state.

### What the mechanism does

![What the mechanism does for Titration](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/6425df7618b6c19a/media/gameplay/18-titration-lesson-18-titration.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.Titration, function () {
    if (escapeLab.number(EscapeMeter.Drops) < 7) escapeLab.make(EscapeAction.TitrationClear)
    else if (escapeLab.number(EscapeMeter.Drops) <= 9) escapeLab.make(EscapeAction.TitrationBloom)
    else escapeLab.make(EscapeAction.TitrationOverflow)
})
```

## 19. Balance the sample

First test `value of LeftWeight = value of RightWeight` and make `ScaleLevel` happen. Else if left is greater, make `ScaleLeft` happen; otherwise make `ScaleRight` happen. Move the two weights through all three outcomes and watch the physical scale follow your rule.

### What the mechanism does

![What the mechanism does for Balance](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/6425df7618b6c19a/media/gameplay/19-balance-lesson-19-balance.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.Balance, function () {
    if (escapeLab.number(EscapeMeter.LeftWeight) == escapeLab.number(EscapeMeter.RightWeight)) escapeLab.make(EscapeAction.ScaleLevel)
    else if (escapeLab.number(EscapeMeter.LeftWeight) > escapeLab.number(EscapeMeter.RightWeight)) escapeLab.make(EscapeAction.ScaleLeft)
    else escapeLab.make(EscapeAction.ScaleRight)
})
```

## 20. Sort the thermal wires

Some wire colors are allowed. An ``||logic(noclick):or||`` test passes when **either** condition is true; it fails only when every joined choice is false. Join native comparisons for purple, red, and black with **or**. If the joined test passes, make `WireInstall` happen; otherwise make `WireEject` happen. Try an allowed color and one other color.

### Find the native Blocks

![Find the native Blocks for Wires](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/6425df7618b6c19a/media/menu/20-wires-20-wires-menu.svg)

### One possible construction

![One possible construction for Wires](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/6425df7618b6c19a/media/assembled/20-wires-20-wires-assembled.svg)

### What the mechanism does

![What the mechanism does for Wires](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/6425df7618b6c19a/media/gameplay/20-wires-lesson-20-wires.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.Wires, function () {
    if (escapeLab.number(EscapeMeter.WireColor) == 1 || escapeLab.number(EscapeMeter.WireColor) == 2 || escapeLab.number(EscapeMeter.WireColor) == 3) escapeLab.make(EscapeAction.WireInstall)
    else escapeLab.make(EscapeAction.WireEject)
})
```

## 21. Prune the living plant

Test `value of LeafPoints > 3`. Make `LeafClip` happen when true; make `LeafKeep` happen otherwise. Select a four-point leaf and a three-point leaf. The clipped leaf falls away while the allowed leaf stays in the silhouette.

### What the mechanism does

![What the mechanism does for Pruner](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/6425df7618b6c19a/media/gameplay/21-pruner-lesson-21-pruner.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.Pruner, function () {
    if (escapeLab.number(EscapeMeter.LeafPoints) > 3) escapeLab.make(EscapeAction.LeafClip)
    else escapeLab.make(EscapeAction.LeafKeep)
})
```

## 22. Reveal the heat vessel

Build three states in order. If `is VesselRepaired` **and** `is VesselHot`, make `VesselReveal` happen. Else if it is repaired, make `VesselBlank` happen. Otherwise make `VesselLeak` happen. Try broken, repaired-cool, and repaired-hot states. Put the more specific repaired-and-hot test first so it is not swallowed by the repaired-only branch.

### What the mechanism does

![What the mechanism does for Vessel](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/6425df7618b6c19a/media/gameplay/22-vessel-lesson-22-vessel.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.Vessel, function () {
    if (escapeLab.is(EscapeFact.VesselRepaired) && escapeLab.is(EscapeFact.VesselHot)) escapeLab.make(EscapeAction.VesselReveal)
    else if (escapeLab.is(EscapeFact.VesselRepaired)) escapeLab.make(EscapeAction.VesselBlank)
    else escapeLab.make(EscapeAction.VesselLeak)
})
```

## 23. Tune the pedal receiver

If `value of RPM ≥ 80`, make `ReceiverClear` happen. Else if `RPM ≥ 40`, make `ReceiverStatic` happen. Else make `ReceiverDead` happen. Test slow, middle, and fast pedaling. Because the highest threshold is first, fast pedaling reaches clear instead of stopping at static.

### What the mechanism does

![What the mechanism does for Receiver](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/6425df7618b6c19a/media/gameplay/23-receiver-lesson-23-receiver.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.Receiver, function () {
    if (escapeLab.number(EscapeMeter.RPM) >= 80) escapeLab.make(EscapeAction.ReceiverClear)
    else if (escapeLab.number(EscapeMeter.RPM) >= 40) escapeLab.make(EscapeAction.ReceiverStatic)
    else escapeLab.make(EscapeAction.ReceiverDead)
})
```

## 24. Clear the interference

The message is clear only if three noise channels are off. Each ``||logic(noclick):not||`` turns an “is on” reporter into the test that it is off. Join `not is ScratchOn`, `not is BeepOn`, and `not is HumOn` with **and**. Make `NoiseClear` when all pass; otherwise make `NoiseDistort` happen. Turn off each channel, then turn one back on to check the alternate branch.

### What the mechanism does

![What the mechanism does for Interference](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/6425df7618b6c19a/media/gameplay/24-interference-lesson-24-interference.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.Interference, function () {
    if (!escapeLab.is(EscapeFact.ScratchOn) && !escapeLab.is(EscapeFact.BeepOn) && !escapeLab.is(EscapeFact.HumOn)) escapeLab.make(EscapeAction.NoiseClear)
    else escapeLab.make(EscapeAction.NoiseDistort)
})
```

## 25. Print the message

The printer may use a clear radio **or** a connected cable. Join `is RadioClear` and `is CableConnected` with **or**. Make `PrinterFeed` if either route works; otherwise make `PrinterJam` happen. Test each usable route on its own, then test neither.

### What the mechanism does

![What the mechanism does for Printer](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/6425df7618b6c19a/media/gameplay/25-printer-lesson-25-printer.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.Printer, function () {
    if (escapeLab.is(EscapeFact.RadioClear) || escapeLab.is(EscapeFact.CableConnected)) escapeLab.make(EscapeAction.PrinterFeed)
    else escapeLab.make(EscapeAction.PrinterJam)
})
```

## 26. Open the pneumatic lock

Either traced route can unlock the tube. Join `is RouteA` and `is RouteB` with **or**. Make `TubeLaunch` if the condition passes and `TubeDrain` otherwise. Trace route A, then route B, then an invalid route. The capsule launches for either accepted path.

### What the mechanism does

![What the mechanism does for Tube](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/6425df7618b6c19a/media/gameplay/26-tube-lesson-26-tube.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.Tube, function () {
    if (escapeLab.is(EscapeFact.RouteA) || escapeLab.is(EscapeFact.RouteB)) escapeLab.make(EscapeAction.TubeLaunch)
    else escapeLab.make(EscapeAction.TubeDrain)
})
```

## 27. Stabilize the pressure seal

Create a native ``||variables(noclick):Variables||`` variable named ``||variables(noclick):pressureReady||`` because the next beat needs to remember whether this setup succeeded. In ``||loops(noclick):on start||``, set it to ``||escapeLab(noclick):is [PressureReady]||`` so a previously earned seal checkpoint can return after a reload. In the **PressureStable** event, test ``||escapeLab(noclick):value of [pressure]||`` ≥ `48` **and** ``||escapeLab(noclick):value of [pressure]||`` ≤ `50`. When true, set ``||variables(noclick):pressureReady||`` to `true` and make `SealStable` happen; otherwise set ``||variables(noclick):pressureReady||`` to `false` and make `SealLeak` happen. Try visible whole-number readings `47`, `48`, `50`, and `51`.

The value in `pressureReady` remembers your decision from this station. When you return to a previously stabilized seal, the supplied world restores that recorded checkpoint. The release attempt will use up this preparation, so the next attempt starts with this rule again.

### Find the native Blocks

![Find the native Blocks for PressureStable](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/6425df7618b6c19a/media/menu/27-pressure-stable-27-pressure-stable-menu.svg)

### One possible construction

![One possible construction for PressureStable](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/6425df7618b6c19a/media/assembled/27-pressure-stable-27-pressure-stable-assembled.svg)

### What the mechanism does

![What the mechanism does for PressureStable](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/6425df7618b6c19a/media/gameplay/27-pressure-stable-lesson-corrected-27-pressure-stable.gif)

#### ~ tutorialhint

```blocks
let pressureReady = escapeLab.is(EscapeFact.PressureReady)

escapeLab.onAttempt(EscapeBeat.PressureStable, function () {
    if (escapeLab.number(EscapeMeter.PressureTenths) >= 48 && escapeLab.number(EscapeMeter.PressureTenths) <= 50) {
        pressureReady = true
        escapeLab.make(EscapeAction.SealStable)
    } else {
        pressureReady = false
        escapeLab.make(EscapeAction.SealLeak)
    }
})
```

## 28. Release the pressure seal

In **PressureRelease**, join your `pressureReady` variable with ``||escapeLab(noclick):value of [pressure]||`` = `20`. Make `SealRetract` when both pass; otherwise make `SealVent` happen. After the whole **if/else** block, set `pressureReady` to `false`: either attempt uses up the preparation. Stabilize first, then set the visible whole-number pressure to `20`. Try `20` again without stabilizing to see why both parts matter. Use **up** to prepare the seal again nearby.

### What the mechanism does

![What the mechanism does for PressureRelease](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/6425df7618b6c19a/media/gameplay/28-pressure-release-lesson-corrected-28-pressure-release.gif)

#### ~ tutorialhint

```blocks
let pressureReady = escapeLab.is(EscapeFact.PressureReady)

escapeLab.onAttempt(EscapeBeat.PressureRelease, function () {
    if (pressureReady && escapeLab.number(EscapeMeter.PressureTenths) == 20) escapeLab.make(EscapeAction.SealRetract)
    else escapeLab.make(EscapeAction.SealVent)
    pressureReady = false
})
```

## 29. Correct the room pitch

Create a ``||variables(noclick):Variables||`` variable named ``||variables(noclick):angle||``. In ``||loops(noclick):on start||``, set it to ``||escapeLab(noclick):value of [PitchAngle]||`` so the displayed horizon and your variable begin together after a saved return. In **PitchAdjust**, change ``||variables(noclick):angle||`` by ``||escapeLab(noclick):value of [PitchChange]||``, then pass ``||variables(noclick):angle||`` to ``||escapeLab(noclick):set room pitch to [number]||``. The panel supplies `+10`, `+25`, `-10`, or `-25`; your variable stores the accumulated angle. The supplied pitch block uses that value to tilt the horizon and objects, but it does not add the changes for you. Combine controls until the gauge reaches `0`.

### Find the native Blocks

![Find the native Blocks for PitchAdjust](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/6425df7618b6c19a/media/menu/29-pitch-adjust-29-pitch-adjust-menu.svg)

### One possible construction

![One possible construction for PitchAdjust](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/6425df7618b6c19a/media/assembled/29-pitch-adjust-29-pitch-adjust-assembled.svg)

### What the mechanism does

![What the mechanism does for PitchAdjust](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/6425df7618b6c19a/media/gameplay/29-pitch-adjust-lesson-29-pitch-adjust.gif)

#### ~ tutorialhint

```blocks
let pressureReady = escapeLab.is(EscapeFact.PressureReady)

let angle = escapeLab.number(EscapeMeter.PitchAngle)

escapeLab.onAttempt(EscapeBeat.PitchAdjust, function () {
    angle += escapeLab.number(EscapeMeter.PitchChange)
    escapeLab.setPitch(angle)
})
```

## 30. Give pitch feedback

In **PitchFeedback**, test your `angle`. If `angle = 0`, make `PitchLevel` happen. Else if `angle < 0`, make `PitchDown` happen; otherwise make `PitchUp` happen. Test a negative, zero, and positive angle. The room's feedback should match the value you have been changing.

### What the mechanism does

![What the mechanism does for PitchFeedback](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/6425df7618b6c19a/media/gameplay/30-pitch-feedback-lesson-corrected-30-pitch-feedback.gif)

#### ~ tutorialhint

```blocks
let pressureReady = escapeLab.is(EscapeFact.PressureReady)

let angle = escapeLab.number(EscapeMeter.PitchAngle)

escapeLab.onAttempt(EscapeBeat.PitchFeedback, function () {
    if (angle == 0) escapeLab.make(EscapeAction.PitchLevel)
    else if (angle < 0) escapeLab.make(EscapeAction.PitchDown)
    else escapeLab.make(EscapeAction.PitchUp)
})
```

## 31. Map the remote sensors

Use an **else if** chain on `value of SensorNumber`: map `1` to `SensorLamp1`, `2` to `SensorLamp2`, and `3` to `SensorLamp3`. In the final else, make `SensorDark` happen. Change the remote input and confirm each lamp is a distinct visible response.

### What the mechanism does

![What the mechanism does for Sensors](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/6425df7618b6c19a/media/gameplay/31-sensors-lesson-31-sensors.gif)

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

## 32. Open the shutter bank safely

If `is WindowA` **or** `is WindowB`, make `ShutterOpen` happen. Else if `is DangerousControl`, make `ShutterWarn` happen. Otherwise make `ShutterClosed` happen. Test an openable window, a dangerous control, and one other control. Put the usable window rule first so it remains the main path.

### What the mechanism does

![What the mechanism does for Shutters](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/6425df7618b6c19a/media/gameplay/32-shutters-lesson-32-shutters.gif)

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

## 33. Ignite the constellation core

Join `is FrontMatch`, `is MiddleMatch`, and `is BackMatch` with **and**. Make `StarIgnite` only when all three are true; otherwise make `StarFizzle` happen. Change one layer at a time, then align all three. The three cable layers flare together only for the complete match.

### What the mechanism does

![What the mechanism does for Constellation](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/6425df7618b6c19a/media/gameplay/33-constellation-lesson-33-constellation.gif)

#### ~ tutorialhint

```blocks
let pressureReady = escapeLab.is(EscapeFact.PressureReady)

let angle = escapeLab.number(EscapeMeter.PitchAngle)

escapeLab.onAttempt(EscapeBeat.Constellation, function () {
    if (escapeLab.is(EscapeFact.FrontMatch) && escapeLab.is(EscapeFact.MiddleMatch) && escapeLab.is(EscapeFact.BackMatch)) escapeLab.make(EscapeAction.StarIgnite)
    else escapeLab.make(EscapeAction.StarFizzle)
})
```

## 34. Cross the rock path

This route's visible clue says: **keep the color, change the pattern**. Join `is SameColor` with `not is SamePattern` using **and**. Make `RockBeam` when both parts pass; otherwise make `RockCollapse` happen. The panel labels color and pattern, so solve each local move from what you can see instead of decoding a hidden rule.

### What the mechanism does

![What the mechanism does for RockPath](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/6425df7618b6c19a/media/gameplay/34-rock-path-lesson-34-rock-path.gif)

#### ~ tutorialhint

```blocks
let pressureReady = escapeLab.is(EscapeFact.PressureReady)

let angle = escapeLab.number(EscapeMeter.PitchAngle)

escapeLab.onAttempt(EscapeBeat.RockPath, function () {
    if (escapeLab.is(EscapeFact.SameColor) && !escapeLab.is(EscapeFact.SamePattern)) escapeLab.make(EscapeAction.RockBeam)
    else escapeLab.make(EscapeAction.RockCollapse)
})
```

## 35. Synchronize the three systems

Join `is PowerReady`, `is PressureSystemReady`, `is SignalReady`, and `not is AlarmOn` with **and**. Make `SyncLock` only when every system is ready and the alarm is off; otherwise make `SyncReject` happen. Toggle one condition at a time, then bring all four into the required state.

### What the mechanism does

![What the mechanism does for Synchronize](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/6425df7618b6c19a/media/gameplay/35-synchronize-lesson-35-synchronize.gif)

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

The final test is `value of CoreLights = 3` **and** `not is AlarmOn`. Make `LeverPull` when it passes; otherwise make `LeverReject` happen. First completion records the escape and offers an explicit full replay. Choose that replay to start again: it clears this run's room and mechanism checkpoints while keeping first-clear history. A second escape receives its distinct ending.

### What the mechanism does

![What the mechanism does for FinalLever](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/6425df7618b6c19a/media/gameplay/36-final-lever-lesson-36-final-lever.gif)

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

You used native ``||logic(noclick):if then else||`` blocks to make one visible choice at a time, then added **else if**, **and**, **or**, and **not** when the room needed more than two outcomes or more than one requirement. `pressureReady` and `angle` are variables because later beats use the values they remember. Every station remains available for local retries, so your changed condition can produce a changed visible result.

```template
// Logic Escape Room
```

```customts
// The learner-facing nouns. Decisions belong in native if / else blocks.
enum EscapeBeat {
    Crank, Generator, Case, Fire, Wall, Footprints,
    Shadow, Portrait1, Portrait2, Portrait3, Portrait4, MuralMix,
    MuralReveal, Stones, Telescope, Thermal, Sample, Titration,
    Balance, Wires, Pruner, Vessel, Receiver, Interference,
    Printer, Tube, PressureStable, PressureRelease, PitchAdjust,
    PitchFeedback, Sensors, Shutters, Constellation, RockPath,
    Synchronize, FinalLever
}

enum EscapeItem { LargeMagnet, HandCrank, WaterCanister }

enum EscapeFact {
    LockFree, YellowOn, BlueOn, RedOn, Metallic, MagnetOn,
    VesselRepaired, VesselHot, ScratchOn, BeepOn, HumOn,
    RadioClear, CableConnected, RouteA, RouteB, PressureReady,
    WindowA, WindowB, DangerousControl, FrontMatch,
    MiddleMatch, BackMatch, SameColor, SamePattern,
    PowerReady, PressureSystemReady, SignalReady, AlarmOn
}

enum EscapeMeter {
    InstalledHolds, StepValue, Illumination, ShoeSide,
    StoneColor, SocketColor, Zoom, Temperature, Drops,
    LeftWeight, RightWeight, WireColor, LeafPoints, RPM,
    //% block="pressure"
    PressureTenths, PitchChange, PitchAngle, SensorNumber,
    CoreLights
}

enum EscapeAction {
    CrankPull, CrankTwitch, GeneratorSpin, GeneratorSputter,
    CaseRetract, CaseRattle, FireSteam, FireFlare,
    WallClimb, WallFlash, FootprintKeep, FootprintDrop,
    ShadowReveal, ShadowHide, PortraitLeft, PortraitRight,
    MuralBlend, MuralDim, MuralOpen, MuralSpill,
    StoneSnap, StoneRepel, TelescopeFocus, TelescopeBlur,
    ThermalBlue, ThermalAmber, ThermalRed, SampleSpike,
    SampleFlat, TitrationClear, TitrationBloom, TitrationOverflow,
    ScaleLevel, ScaleLeft, ScaleRight, WireInstall, WireEject,
    LeafClip, LeafKeep, VesselReveal, VesselBlank, VesselLeak,
    ReceiverClear, ReceiverStatic, ReceiverDead, NoiseClear,
    NoiseDistort, PrinterFeed, PrinterJam, TubeLaunch, TubeDrain,
    SealStable, SealLeak, SealRetract, SealVent,
    PitchLevel, PitchDown, PitchUp, SensorLamp1, SensorLamp2,
    SensorLamp3, SensorDark, ShutterOpen, ShutterWarn,
    ShutterClosed, StarIgnite, StarFizzle, RockBeam,
    RockCollapse, SyncLock, SyncReject, LeverPull, LeverReject
}

// Code-native pixel art for the clockwork observatory.
namespace escapeArt {
    const shortNames = ["CRANK", "GENERATOR", "CASE", "SPRINKLER", "WALL", "STEPS", "SHADOW", "PORTRAITS", "MURAL", "STONES", "SCOPE", "THERMAL", "SAMPLE", "TITRATION", "BALANCE", "WIRES", "PLANT", "VESSEL", "RECEIVER", "NOISE", "PRINTER", "TUBE", "PRESSURE", "PITCH", "SENSORS", "SHUTTERS", "STAR WIRES", "ROCK PATH", "SYNC", "EXIT"]
    const roomNames = ["WARM WORKSHOP", "PRISM GALLERY", "GARDEN LAB", "RELAY LOFT", "SKY VAULT"]
    const responseNames = ["MAGNET PULLS IRON", "CRANK TWITCHES", "ROTOR SPINS", "ROTOR SPUTTERS", "CASE RELEASED", "LATCH RATTLES", "FLAME TO STEAM", "FLAME GROWS", "WALL CLIMBED", "WALL FLASHES", "SAFE STEP", "STEP FALLS", "SHADOW REVEALED", "SHADOW HIDDEN", "PORTRAIT MOVES LEFT", "PORTRAIT MOVES RIGHT", "COLORS BLEND", "MURAL DIMS", "MURAL OPENS", "COLOR SPILLS", "STONE SNAPS IN", "STONE REPELS", "SCOPE IN FOCUS", "SCOPE BLURS", "CACHE TURNS BLUE", "CACHE WARMS", "CACHE TURNS RED", "SPIKES RISE", "SAMPLE FLAT", "CLEAR SOLUTION", "SOLUTION BLOOMS", "SOLUTION OVERFLOWS", "SCALE LEVEL", "SCALE TILTS LEFT", "SCALE TILTS RIGHT", "WIRE INSTALLED", "WIRE EJECTED", "LEAF CLIPPED", "LEAF STAYS", "VESSEL REPAIRED", "VESSEL BLANK", "VESSEL LEAKS", "SIGNAL CLEARED", "STATIC RETURNS", "RECEIVER DEAD", "NOISE REMOVED", "NOISE DISTORTED", "MESSAGE PRINTED", "PRINTER JAMMED", "CAPSULE LAUNCHED", "CAPSULE DRAINS", "SEAL STABLE", "SEAL LEAKS", "DOOR RETRACTS", "PRESSURE VENTS", "ROOM LEVEL", "ROOM TILTS DOWN", "ROOM TILTS UP", "LAMP ONE ON", "LAMP TWO ON", "LAMP THREE ON", "LAMPS DARK", "SHUTTERS OPEN", "SHUTTER WARNING", "SHUTTERS CLOSED", "STARS ALIGN", "STAR FIZZLES", "ROCK BRIDGE", "BRIDGE COLLAPSES", "SYSTEMS SYNCED", "ALARM SOUNDS", "CORE LEVER PULLED", "ALARM SOUNDS"]

    export function installPalette() {
        // Dark ink, warm brass and cool observatory glass; index 0 stays transparent.
        image.setPalette(hex`00000018182e4b3045bd4b53ed8756d8ac69706a757fc09a398b9bd4e5cff7d87966cddd283b547c66a83f6582f7f2dd`)
    }

    function line(p: Image, x1: number, y1: number, x2: number, y2: number, color: number) {
        let dx = Math.abs(x2 - x1)
        let sx = x1 < x2 ? 1 : -1
        let dy = -Math.abs(y2 - y1)
        let sy = y1 < y2 ? 1 : -1
        let err = dx + dy
        while (true) {
            p.setPixel(x1, y1, color)
            if (x1 == x2 && y1 == y2) break
            let e2 = 2 * err
            if (e2 >= dy) { err += dy; x1 += sx }
            if (e2 <= dx) { err += dx; y1 += sy }
        }
    }

    function frame(p: Image, x: number, y: number, w: number, h: number, color: number) {
        p.drawRect(x, y, w, h, color)
        p.fillRect(x + 2, y + 2, w - 4, 2, color)
        p.fillRect(x + 2, y + h - 4, w - 4, 2, 1)
    }

    function rivets(p: Image, x: number, y: number, w: number, color: number) {
        p.fillRect(x, y, 2, 2, color)
        p.fillRect(x + w - 2, y, 2, 2, color)
    }

    function gear(p: Image, x: number, y: number, r: number, color: number, phase: number) {
        p.drawCircle(x, y, r, color)
        p.drawCircle(x, y, Math.max(2, r - 3), 5)
        p.fillRect(x - 1, y - r - 2 + phase % 2, 3, 4, color)
        p.fillRect(x - 1, y + r - 1, 3, 4, color)
        p.fillRect(x - r - 2, y - 1, 4, 3, color)
        p.fillRect(x + r - 1, y - 1, 4, 3, color)
        p.fillRect(x - 2, y - 2, 5, 5, 10)
    }

    function lamp(p: Image, x: number, y: number, color: number, phase: number) {
        p.fillRect(x - 5, y - 2, 10, 7, 1)
        p.fillRect(x - 3, y - 5, 6, 7, phase % 2 == 0 ? color : 10)
        p.fillRect(x - 3, y + 5, 6, 2, 5)
    }

    function solvedAt(s: number, solved: number[], first: number[], last: number[]): boolean {
        for (let b = first[s]; b <= last[s]; b++) if (solved[b] != 1) return false
        return true
    }

    function wallTrim(p: Image, room: number) {
        let wall = room == 0 ? 12 : room == 1 ? 14 : room == 2 ? 8 : room == 3 ? 12 : 1
        let trim = room == 0 ? 4 : room == 1 ? 11 : room == 2 ? 7 : room == 3 ? 13 : 10
        p.fill(wall)
        p.fillRect(0, 28, 320, 148, room == 0 ? 12 : room == 1 ? 14 : room == 2 ? 8 : room == 3 ? 12 : 1)
        // Tall wall panels and brass rails establish a room instead of a flat menu grid.
        for (let x = 8; x < 320; x += 40) {
            p.fillRect(x, 39, 2, 121, trim)
            p.fillRect(x + 4, 41, 30, 2, room == 4 ? 2 : 9)
        }
        p.fillRect(0, 34, 320, 4, 5)
        p.fillRect(0, 158, 320, 5, trim)
        p.fillRect(0, 163, 320, 4, 1)
        // Clockwork columns and ceiling lamps make each space feel inhabited.
        for (let x = 20; x < 320; x += 80) {
            p.fillRect(x, 39, 5, 118, 5)
            p.fillRect(x + 1, 44, 3, 106, wall)
            lamp(p, x + 13, 52, room == 4 ? 3 : 10, x + room)
        }
        p.fillRect(0, 167, 320, 73, room == 0 ? 2 : room == 1 ? 12 : room == 2 ? 5 : room == 3 ? 14 : 1)
        // Broad walking lanes stay clear at y=112, y=198 and the vertical aisles.
        p.fillRect(0, 112, 320, 13, room == 0 ? 5 : room == 1 ? 9 : room == 2 ? 10 : room == 3 ? 6 : 2)
        p.fillRect(0, 194, 320, 10, room == 0 ? 5 : room == 1 ? 9 : room == 2 ? 10 : room == 3 ? 6 : 2)
        for (let x = 105; x < 216; x += 16) p.fillRect(x, 114, 8, 2, trim)
        for (let x = 105; x < 216; x += 16) p.fillRect(x, 197, 8, 2, trim)
        p.fillRect(106, 124, 8, 34, trim)
        p.fillRect(206, 124, 8, 34, trim)
        // Outer scenery differs by room: chimney, stained glass, greenhouse, radio loft, core window.
        if (room == 0) {
            p.fillRect(278, 43, 31, 47, 1); frame(p, 280, 45, 27, 43, 5)
            for (let i = 0; i < 3; i++) p.fillRect(284 + i * 7, 49, 3, 30, i == 1 ? 4 : 8)
            gear(p, 22, 133, 12, 4, room)
        } else if (room == 1) {
            frame(p, 278, 42, 34, 52, 5)
            line(p, 280, 46, 295, 90, 11); line(p, 310, 46, 295, 90, 13)
            p.fillRect(291, 69, 9, 17, 10)
            for (let i = 0; i < 4; i++) p.fillRect(8 + i * 6, 146 - i * 5, 3, 10, 9)
        } else if (room == 2) {
            p.fillRect(280, 42, 31, 50, 7); frame(p, 280, 42, 31, 50, 9)
            p.fillRect(285, 47, 21, 39, 11)
            for (let i = 0; i < 3; i++) { line(p, 286 + i * 7, 83, 291 + i * 7, 56, 7); p.fillRect(287 + i * 7, 53, 5, 4, 10) }
            p.fillRect(12, 137, 24, 21, 2); p.fillRect(16, 130, 16, 9, 4)
        } else if (room == 3) {
            frame(p, 277, 43, 34, 47, 9)
            for (let i = 0; i < 4; i++) { line(p, 280, 50 + i * 9, 308, 50 + i * 9, 8); p.fillRect(302 - i * 3, 47 + i * 9, 3, 4, 10) }
            p.fillRect(10, 135, 28, 22, 1); gear(p, 24, 133, 8, 13, room)
        } else {
            for (let i = 0; i < 3; i++) { p.drawCircle(293, 65, 25 - i * 7, i == 1 ? 11 : 8) }
            lamp(p, 293, 65, 3, 1)
            p.fillRect(8, 141, 25, 17, 2); p.fillRect(12, 136, 17, 5, 10)
        }
    }

    function stationArt(p: Image, s: number, x: number, y: number, done: boolean, phase: number, pitch: number) {
        let metal = done ? 7 : 5
        let glow = done ? 10 : 8
        let motion = phase % 3
        // Each station has its own recognizable apparatus, even at room-map scale.
        if (s == 0) { p.fillRect(x - 23, y + 10, 46, 5, 1); p.fillRect(x - 18, y - 9, 10, 19, 5); gear(p, x + 12, y - 2, 9, metal, phase); line(p, x - 7, y - 5, x + 3, y - 5, 10) }
        else if (s == 1) { p.fillRect(x - 22, y - 12, 16, 25, 12); gear(p, x - 14, y, 7, metal, phase); p.fillRect(x + 6, y - 10, 15, 20, 5); line(p, x - 7, y - 7, x + 7, y - 7, 4); line(p, x - 7, y + 7, x + 7, y + 7, 4) }
        else if (s == 2) { frame(p, x - 19, y - 14, 38, 28, metal); p.fillRect(x - 3, y - 4, 8, 12, glow); p.fillRect(x - 23, y + 1, 5, 8, 4); line(p, x - 22, y - 2, x - 16, y - 2, done ? 7 : 2) }
        else if (s == 3) { p.fillRect(x - 22, y + 9, 44, 5, 5); for (let i = 0; i < 3; i++) p.fillRect(x - 15 + i * 13, y - 7 - (done ? 4 : 0), 7, done ? 5 : 17, done ? 11 : 3) }
        else if (s == 4) { p.fillRect(x - 23, y - 14, 46, 30, 12); for (let i = 0; i < 4; i++) p.fillRect(x - 17 + i * 12, y + (i % 2) * -7, 7, 5, done ? 7 : 5) }
        else if (s == 5) { for (let i = 0; i < 4; i++) { p.fillRect(x - 22 + i * 13, y + (i % 2) * -5 + (done && i == 3 ? 6 : 0), 9, 5, i == 3 && !done ? 3 : 10) } }
        else if (s == 6) { p.fillRect(x - 19, y - 13, 38, 27, 1); line(p, x - 8, y + 9, x + 7, y - 9, done ? 10 : 6); p.fillRect(x - 25, y - 8, 6, 15, 5) }
        else if (s == 7) { for (let i = 0; i < 4; i++) { frame(p, x - 25 + i * 13, y - 12, 10, 24, metal); p.fillRect(x - 22 + i * 13, y - 5, 4, 8, i == 1 && done ? 10 : 8) } }
        else if (s == 8) { line(p, x - 21, y - 11, x, y + 7, 5); line(p, x + 21, y - 11, x, y + 7, 8); p.fillRect(x - 9, y - 1, 18, 14, done ? 7 : 13); p.fillRect(x - 4, y + 2, 8, 6, glow) }
        else if (s == 9) { for (let i = 0; i < 4; i++) { frame(p, x - 23 + i * 12, y - 8, 9, 17, 6); p.fillRect(x - 20 + i * 12, y - 4, 4, 9, i == 2 && done ? 10 : 13) } }
        else if (s == 10) { p.fillRect(x - 21, y - 3, 27, 8, metal); p.fillRect(x - 17, y - 7, 14, 5, 8); p.drawCircle(x + 14, y, 12, 9); p.drawCircle(x + 14, y, 6, done ? 10 : 8) }
        else if (s == 11) { frame(p, x - 20, y - 13, 40, 26, 8); p.fillRect(x - 15, y - 8, 30, 16, done ? 4 : 11); p.fillRect(x - 3, y - 4, 7, 8, glow) }
        else if (s == 12) { frame(p, x - 20, y - 3, 40, 15, metal); p.fillRect(x - 15, y + 5, 30, 5, 1); for (let i = 0; i < 4; i++) line(p, x - 11 + i * 7, y + 4, x - 13 + i * 7, y - 11, done ? 10 : 13) }
        else if (s == 13) { p.drawRect(x - 15, y - 14, 30, 29, 9); p.fillRect(x - 11, y + (done ? -2 : 2), 22, done ? 9 : 12, done ? 10 : 8); p.fillRect(x - 3, y - 18, 7, 5, 5) }
        else if (s == 14) { line(p, x, y - 14, x, y + 12, 5); line(p, x - 21, y - (done ? 1 : 6), x + 21, y + (done ? 1 : 6), 9); p.fillRect(x - 23, y + 2, 10, 7, 10); p.fillRect(x + 13, y + 2, 10, 7, 10) }
        else if (s == 15) { for (let i = 0; i < 4; i++) line(p, x - 24, y - 10 + i * 6, x + (done ? -4 : 21), y - 10 + i * 6, i == 2 ? 3 : 8); p.fillRect(x + 16, y - 14, 7, 28, 10) }
        else if (s == 16) { line(p, x, y + 14, x, y - 11, 5); for (let i = 0; i < 3; i++) { p.fillRect(x - 15 + i * 9, y - 10 + i * 6, 13, 5, i == 2 && done ? 4 : 7) } }
        else if (s == 17) { p.drawRect(x - 15, y - 13, 30, 27, 9); p.fillRect(x - 11, y + 1, 22, 9, done ? 10 : 8); if (!done) p.fillRect(x + 15, y + 5, 3, 7, 11) }
        else if (s == 18) { frame(p, x - 22, y - 12, 44, 25, 1); for (let i = 0; i < 5; i++) p.fillRect(x - 16 + i * 7, y + (done ? -8 : -2) - (i % 2) * 5, 3, done ? 12 : 5, done ? 7 : 6) }
        else if (s == 19) { for (let i = 0; i < 3; i++) { line(p, x - 22, y - 9 + i * 9, x + 22, y - 9 + i * 9, done || i != 1 ? 8 : 2); if (!done && i == 1) p.fillRect(x - 8, y - 11, 19, 13, 3) } }
        else if (s == 20) { p.fillRect(x - 19, y - 13, 38, 25, 5); p.fillRect(x - 13, y - 8, 26, 11, 1); p.fillRect(x - 9, y + 11, 19, done ? 8 : 3, 15); if (done) p.print("OK", x - 5, y + 11, 8) }
        else if (s == 21) { line(p, x - 22, y, x, y, 6); line(p, x, y, x + 20, y - 10, 5); line(p, x, y, x + 20, y + 10, 5); p.fillRect(done ? x + 14 : x - 17, y - 3, 7, 7, 10) }
        else if (s == 22) { p.drawCircle(x - 10, y, 12, 9); line(p, x - 10, y, x - 6, y - (done ? 7 : 2), 3); p.fillRect(x + 7, y - 13, 15, 27, done ? 7 : 5) }
        else if (s == 23) { let tilt = Math.idiv(Math.max(-50, Math.min(50, pitch)), 10); line(p, x - 22, y + tilt, x + 22, y - tilt, 10); p.fillRect(x - 3, y + 5, 7, 7, 4); p.drawCircle(x + 15, y - 8, 4, 11) }
        else if (s == 24) { p.fillRect(x - 22, y - 11, 14, 22, 5); line(p, x - 8, y, x + 10, y, 8); for (let i = 0; i < 3; i++) lamp(p, x + 15, y - 10 + i * 10, done ? 10 : 3, phase + i) }
        else if (s == 25) { for (let i = 0; i < 3; i++) p.fillRect(x - 19 + i * 14, y - (done ? 12 : 8), 9, done ? 18 : 22, done ? 8 : 5); if (done) line(p, x - 20, y + 14, x + 20, y + 14, 11) }
        else if (s == 26) { for (let i = 0; i < 3; i++) { line(p, x - 21, y - 9 + i * 9, x + 21, y - 9 + i * 9, done ? 11 : 8); p.fillRect(x - 3 + i * 3, y - 11 + i * 9, 6, 5, 10) } }
        else if (s == 27) { for (let i = 0; i < 4; i++) { p.drawRect(x - 23 + i * 14, y - 5 + (i % 2) * 7, 12, 12, i % 2 == 0 ? 8 : 10); if (done && i < 3) line(p, x - 11 + i * 14, y + (i % 2) * 7, x - 8 + i * 14, y + 4 - (i % 2) * 7, 7) } }
        else if (s == 28) { for (let i = 0; i < 3; i++) { frame(p, x - 22 + i * 15, y - 12, 12, 25, done ? 7 : 9); line(p, x - 17 + i * 15, y - 8, x - 17 + i * 15 + (done ? 4 : i * 3), y + 9, done ? 11 : 2) } }
        else { p.fillRect(x - 18, y - 12, 10, 27, 5); line(p, x - 13, y - 8, x - 2, y - 1, 10); p.fillRect(x + 5, y - 15, 17, 33, done ? 10 : 12); if (done) p.fillRect(x + 9, y - 10, 9, 22, 11); else frame(p, x + 8, y - 8, 11, 18, 5) }
        // A visible completion lamp and brass foot make success readable at native size.
        p.fillRect(x - 23, y + 16, 46, 2, 1)
        lamp(p, x + 21, y - 14, done ? 10 : 3, phase)
    }

    export function explorer(direction: number, step: number): Image {
        let p = image.create(16, 20)
        p.fill(0)
        let stride = step == 0 ? 0 : step == 2 ? 2 : step == 1 ? -1 : 1
        // Hood, coat, brass pack and boots; face and pack placement show facing.
        p.fillRect(5, 1, 6, 2, 2)
        p.fillRect(3, 3, 10, 3, direction == 3 ? 5 : 4)
        p.fillRect(4, 6, 8, 2, direction == 3 ? 5 : 9)
        if (direction == 0) { p.fillRect(5, 8, 2, 2, 1); p.fillRect(9, 8, 2, 2, 1) }
        else if (direction == 1) { p.fillRect(4, 8, 2, 3, 1); p.fillRect(10, 7, 3, 7, 5) }
        else if (direction == 2) { p.fillRect(10, 8, 2, 3, 1); p.fillRect(3, 7, 3, 7, 5) }
        else { p.fillRect(4, 7, 8, 7, 5); p.fillRect(5, 8, 6, 5, 12); p.fillRect(3, 8, 2, 5, 4) }
        p.fillRect(4, 10, 8, 5, 3)
        p.fillRect(3, 11, 2, 4, 10); p.fillRect(11, 11, 2, 4, 10)
        p.fillRect(4, 15, 3, 3 + (stride < 0 ? 1 : 0), 2)
        p.fillRect(9, 15, 3, 3 + (stride > 0 ? 1 : 0), 2)
        p.fillRect(3 - (stride < 0 ? 1 : 0), 18, 5, 2, 1)
        p.fillRect(9 + (stride > 0 ? 1 : 0), 18, 5, 2, 1)
        return p
    }

    export function world(room: number, title: string, names: string[], solved: number[], first: number[], last: number[], pitch: number, phase: number, nearby: number = -1, firstClear: number = 0): Image {
        let p = image.create(320, 240)
        wallTrim(p, room)
        p.fillRect(0, 0, 320, 28, 1)
        p.fillRect(0, 25, 320, 3, room == 0 ? 4 : room == 1 ? 11 : room == 2 ? 7 : room == 3 ? 13 : 10)
        p.print("OBSERVATORY  /  " + roomNames[room], 7, 4, 15)
        let completeCount = 0
        for (let local = 0; local < 6; local++) if (solvedAt(room * 6 + local, solved, first, last)) completeCount++
        p.print("ROOM " + (room + 1) + "/5  " + (firstClear == 1 ? "CORE RESTORED" : "WAKE MACHINES"), 7, 16, 10)
        p.print(completeCount + "/6 MACHINES", 225, 16, 7)
        // Six open work bays sit in the architecture; they are not boxed menu tiles.
        for (let local = 0; local < 6; local++) {
            let s = room * 6 + local
            let x = 60 + (local % 3) * 100
            let y = 78 + Math.idiv(local, 3) * 84
            let done = solvedAt(s, solved, first, last)
            let near = nearby == s
            p.fillRect(x - 29, y + 14, 58, 4, 1)
            p.fillRect(x - 25, y + 11, 50, 3, done ? 7 : 5)
            p.fillRect(x - 24, y - 19, 48, 3, near ? 10 : 1)
            p.fillRect(x - 21, y - 16, 42, 2, room == 0 ? 4 : room == 1 ? 11 : room == 2 ? 7 : room == 3 ? 13 : 10)
            stationArt(p, s, x, y - 1, done, phase, pitch)
            if (near) { p.drawRect(x - 31, y - 22, 62, 41, 15); p.fillRect(x - 25, y - 21, 50, 2, 10) }
            p.fillRect(x - 29, y + 20, 58, 9, 1)
            p.print(shortNames[s], x - Math.idiv(shortNames[s].length * 6, 2), y + 20, done ? 10 : near ? 15 : 9)
            if (done) { p.fillRect(x - 27, y - 18, 4, 4, 10); p.fillRect(x - 26, y - 17, 2, 2, 15) }
        }
        // Directional room doors remain visible beyond the stations.
        let rightOpen = room < 4 && completeCount == 6
        p.fillRect(0, 183, 24, 49, room > 0 ? 5 : 1); p.fillRect(2, 187, 18, 41, room > 0 ? 8 : 2)
        p.fillRect(296, 183, 24, 49, room < 4 ? 5 : 1); p.fillRect(300, 187, 18, 41, room < 4 ? 8 : 2)
        if (room > 0) { p.fillRect(5, 193, 12, 26, 1); lamp(p, 11, 190, 10, phase) }
        if (rightOpen) { p.fillRect(303, 193, 11, 27, 1); lamp(p, 308, 190, 10, phase) }
        else if (room < 4) { p.fillRect(302, 191, 14, 30, 5); p.fillRect(306, 201, 6, 7, 10); p.fillRect(308, 207, 2, 6, 1) }
        p.print(room > 0 ? "<" : "X", 7, 199, 15); p.print(rightOpen ? ">" : room < 4 ? "!" : "X", 304, 199, 15)
        p.fillRect(24, 221, 272, 19, 1)
        p.print("ARROWS MOVE   A WORK / TRAVEL", 48, 226, 9)
        return p
    }

    function machineBack(p: Image, station: number, phase: number) {
        let room = Math.idiv(station, 6)
        p.fill(room == 0 ? 2 : room == 1 ? 12 : room == 2 ? 5 : room == 3 ? 14 : 1)
        // Large inset workbench, riveted architecture and room-colored windows.
        p.fillRect(0, 0, 320, 28, 1)
        p.fillRect(0, 28, 320, 3, room == 0 ? 4 : room == 1 ? 11 : room == 2 ? 7 : room == 3 ? 13 : 10)
        for (let x = 10; x < 320; x += 40) p.fillRect(x, 40, 2, 126, room == 0 ? 5 : room == 1 ? 8 : room == 2 ? 9 : room == 3 ? 6 : 5)
        for (let x = 18; x < 310; x += 76) { lamp(p, x, 48, 10, phase); p.fillRect(x - 16, 157, 32, 5, 1) }
        p.fillRect(14, 79, 292, 111, 1)
        p.fillRect(18, 83, 284, 103, 15)
        frame(p, 14, 79, 292, 111, room == 0 ? 4 : room == 1 ? 11 : room == 2 ? 7 : room == 3 ? 13 : 10)
        p.fillRect(14, 184, 292, 12, 5)
        p.fillRect(20, 186, 280, 3, 9)
        rivets(p, 18, 82, 284, 10)
    }

    function mechanism(p: Image, station: number, beat: number, fixture: number, response: number, pressureReady: boolean, pitch: number, phase: number) {
        let pulse = phase % 3
        // Physical apparatus fills the panel, with distinct locations and causal motion per device.
        if (station == 0) { // iron bar drawn across a brass floor rail
            p.fillRect(52, 158, 216, 7, 5); p.fillRect(61, 151, 198, 3, 1)
            p.fillRect(79, 104, 38, 49, 12); frame(p, 79, 104, 38, 49, 5); gear(p, 98, 116, 9, 4, phase)
            let pull = response == EscapeAction.CrankPull ? pulse * 15 : response == EscapeAction.CrankTwitch ? pulse % 2 * 5 : 0
            p.fillRect(125 + pull, 133, 29, 17, 5)
            p.fillRect(130 + pull, 127, 19, 8, response == EscapeAction.CrankTwitch && pulse % 2 == 1 ? 3 : 10)
            line(p, 117, 141, 126 + pull, 141, 8)
            for (let i = 0; i < 5; i++) p.fillRect(176 + i * 13, 145, 3, 2, 9)
        } else if (station == 1) { // hand wheel drives a belt and copper rotor
            p.fillRect(63, 112, 69, 49, 12); frame(p, 63, 112, 69, 49, 5); gear(p, 98, 136, 20, 4, phase)
            p.drawCircle(98, 136, 7, 10)
            p.fillRect(181, 109, 68, 55, 12); frame(p, 181, 109, 68, 55, 5)
            gear(p, 214, 136, 18, response == EscapeAction.GeneratorSpin ? 7 : 5, response == EscapeAction.GeneratorSpin ? phase : 0); let beltMove = response == EscapeAction.GeneratorSpin ? pulse * 4 : response == EscapeAction.GeneratorSputter ? pulse % 2 * 5 : 0; line(p, 117, 117 + beltMove, 196, 117, 4); line(p, 117, 154 - beltMove, 196, 154, 4)
            lamp(p, 266, 136, response == EscapeAction.GeneratorSpin ? 10 : response == EscapeAction.GeneratorSputter && pulse % 2 == 0 ? 3 : 1, phase)
        } else if (station == 2) { // latch withdraws and the glass lid slides open
            p.fillRect(76, 153, 168, 9, 5); p.fillRect(93, 147, 134, 6, 4)
            let caseMove = response == EscapeAction.CaseRetract ? pulse * 18 : response == EscapeAction.CaseRattle ? (pulse % 2 == 0 ? -3 : 3) : 0
            p.fillRect(90 + caseMove, 96 + (response == EscapeAction.CaseRattle ? pulse % 2 * 2 : 0), 140, 53, 11); frame(p, 90 + caseMove, 96 + (response == EscapeAction.CaseRattle ? pulse % 2 * 2 : 0), 140, 53, 8)
            p.fillRect(144, 115, 31, 26, 10); p.fillRect(150, 110, 19, 6, 4)
            p.fillRect(74, 130, 20, 14, fixture == 1 ? 7 : 3); line(p, 94, 136, 112, 136, fixture == 1 ? 7 : 2)
            if (response == EscapeAction.CaseRattle) { p.fillRect(108, 127 + pulse % 2 * 3, 10, 4, 10); p.fillRect(225, 127 - pulse % 2 * 3, 10, 4, 10) }
        } else if (station == 3) { // flame changes into drifting steam under a sprinkler
            p.fillRect(74, 159, 172, 7, 5); p.fillRect(97, 151, 126, 7, 4)
            p.fillRect(146, 94, 28, 20, 8); p.fillRect(158, 109, 4, 18, 5); p.fillRect(144, 125, 32, 5, 5)
            for (let i = 0; i < 5; i++) { let x = 92 + i * 31; let flameH = response == EscapeAction.FireSteam ? 5 : response == EscapeAction.FireFlare ? 38 : 26; p.fillRect(x, 151 - flameH, 11, flameH, response == EscapeAction.FireSteam ? 11 : 3); p.fillRect(x + 3, 151 - flameH + 5, 5, flameH - 8, response == EscapeAction.FireSteam ? 8 : 4) }
            if (response == EscapeAction.FireSteam) for (let i = 0; i < 4; i++) p.fillRect(104 + i * 32, 111 - pulse * 4, 8, 4, 11)
        } else if (station == 4) { // four individually visible handholds
            p.fillRect(85, 94, 150, 69, 12); p.fillRect(91, 99, 138, 58, 14)
            for (let i = 0; i < (fixture == 0 ? 3 : 4); i++) { let x = 105 + i * 31; let y = 143 - (i % 2) * 28; p.fillRect(x, y, 20, 10, response == EscapeAction.WallClimb ? 7 : 5); p.fillRect(x + 3, y + 2, 14, 4, 10) }
            if (response == EscapeAction.WallFlash) { p.fillRect(186, 116, 24, 16, 3); p.print("FLASH", 187, 120, 15) }
            if (response == EscapeAction.WallClimb) { line(p, 102, 159, 211, 99, 10); p.fillRect(199, 97, 13, 8, 2) }
        } else if (station == 5) { // footprints descend toward the next ledge
            p.fillRect(75, 158, 170, 6, 5)
            for (let i = 0; i < 5; i++) { let yy = 142 - (i % 2) * 19 + (response == EscapeAction.FootprintDrop && i == 4 ? 24 : 0); let xx = 83 + i * 33; p.fillRect(xx, yy, 20, 10, response == EscapeAction.FootprintKeep ? 7 : 8); p.fillRect(xx + 4, yy - 5, 7, 5, 10); p.fillRect(xx + 13, yy + 1, 4, 6, 10) }
            line(p, 76, 169, 244, 169, 1)
        } else if (station == 6) { // lantern, opaque screen and ink silhouette
            p.fillRect(98, 95, 125, 67, 1); frame(p, 98, 95, 125, 67, 9)
            p.fillRect(68, 112, 26, 37, 5); p.fillRect(73, 107, 16, 7, 4); lamp(p, 81, 128, fixture == 1 ? 10 : 3, phase)
            if (response == EscapeAction.ShadowReveal) { p.fillRect(142, 112, 35, 37, 2); p.fillRect(150, 102, 18, 12, 2); p.fillRect(135, 146, 49, 6, 2) }
            else if (response == EscapeAction.ShadowHide) { p.fillRect(101, 98, 119, 63, 2); p.fillRect(140, 110, 42, 41, 1); p.fillRect(78, 124, 7, 7, 3) }
            else { for (let i = 0; i < 5; i++) line(p, 109 + i * 23, 149, 121 + i * 23, 111, 6) }
        } else if (station == 7) { // four portrait frames; the selected shoe moves
            for (let i = 0; i < 4; i++) { let shift = beat == 7 + i && response == EscapeAction.PortraitLeft ? -10 : beat == 7 + i && response == EscapeAction.PortraitRight ? 10 : 0; let x = 48 + i * 58 + shift; frame(p, x, 101, 43, 58, i == beat - 7 ? 10 : 5); p.fillRect(x + 15, 111, 13, 17, 8); p.fillRect(x + 11, 129, 21, 17, 6); p.fillRect(x + (response == EscapeAction.PortraitLeft && i == beat - 7 ? 2 : 25), 148, 12, 5, 3); p.fillRect(x + 18, 106, 7, 3, 10) }
        } else if (station == 8) { // paired stained-glass beams blend at the mural
            p.fillRect(122, 119, 76, 46, 1); frame(p, 122, 119, 76, 46, 5); p.fillRect(130, 127, 60, 30, response == EscapeAction.MuralBlend ? 7 : response == EscapeAction.MuralOpen ? 11 : response == EscapeAction.MuralDim ? 2 : 13)
            line(p, 69, 102, 157, 136, fixture == 1 || fixture >= 3 ? 4 : 1); line(p, 251, 102, 157, 136, fixture == 2 || fixture >= 3 ? 8 : 1)
            p.fillRect(64, 95, 15, 12, 4); p.fillRect(245, 95, 15, 12, 8)
            if (response == EscapeAction.MuralOpen) { p.fillRect(148, 153 - pulse * 4, 18, 15, 10); p.fillRect(152, 157 - pulse * 4, 10, 8, 4) }
            if (response == EscapeAction.MuralSpill) for (let i = 0; i < 7; i++) p.fillRect(127 + (i * 19 + pulse * 3) % 63, 124 + (i * 11) % 33, 3, 3, i % 2 == 0 ? 4 : 8)
        } else if (station == 9) { // colored loose stones and four keyed sockets
            p.fillRect(72, 157, 176, 6, 5); for (let i = 0; i < 4; i++) { p.drawRect(91 + i * 37, 115, 29, 39, 8); p.fillRect(96 + i * 37, 120, 19, 27, 1); p.fillRect(100 + i * 37, 124, 11, 18, i + 7) }
            let sx = response == EscapeAction.StoneSnap ? 167 : response == EscapeAction.StoneRepel ? 208 + pulse * 8 : 91 + fixture * 37; p.fillRect(sx, 125, 21, 21, 10); p.fillRect(sx + 5, 121, 11, 4, 9)
        } else if (station == 10) { // long telescope, adjustable focus rings and star window
            p.fillRect(70, 133, 121, 15, 5); p.fillRect(82, 128, 89, 5, 8); p.fillRect(72, 127, 11, 28, 4); p.fillRect(184, 124, 10, 33, 5)
            p.drawCircle(224, 140, 28, 9); p.drawCircle(224, 140, response == EscapeAction.TelescopeBlur ? 24 : 21, response == EscapeAction.TelescopeFocus ? 10 : 6); p.drawCircle(224, 140, response == EscapeAction.TelescopeBlur ? 17 : 13, 8)
            for (let i = 0; i < 5; i++) p.fillRect(199 + i * 12, response == EscapeAction.TelescopeFocus ? 126 : response == EscapeAction.TelescopeBlur ? 120 : 132, 2, response == EscapeAction.TelescopeBlur ? 35 : 20, response == EscapeAction.TelescopeFocus ? 10 : 13)
            lamp(p, 88, 112, 10, phase)
        } else if (station == 11) { // three thermal drawers, only one temperature opens
            let thermalChoice = response == EscapeAction.ThermalBlue ? 0 : response == EscapeAction.ThermalAmber ? 1 : response == EscapeAction.ThermalRed ? 2 : fixture
            for (let i = 0; i < 3; i++) { let drawer = i == thermalChoice; p.fillRect(84 + i * 56, 103, 48, 59, 12); frame(p, 84 + i * 56, 103, 48, 59, drawer ? 10 : 5); p.fillRect(91 + i * 56, 111, 34, 39, i == 0 ? 8 : i == 1 ? 4 : 3); p.fillRect(100 + i * 56, drawer ? 150 : 155, 16, drawer ? 7 : 3, 10); p.print(i == 0 ? "COLD" : i == 1 ? "WARM" : "HOT", 91 + i * 56, 94, 1) }
            p.fillRect(139, 117, 42, 25, 1); p.fillRect(144, 121, 32, 17, response == EscapeAction.ThermalBlue ? 11 : response == EscapeAction.ThermalAmber ? 10 : response == EscapeAction.ThermalRed ? 3 : 2)
        } else if (station == 12) { // magnetic fluid in a glass trough forms spikes
            p.fillRect(88, 139, 144, 23, 12); frame(p, 88, 115, 144, 47, 9); p.fillRect(94, 140, 132, 17, 1)
            for (let i = 0; i < 7; i++) { let h = response == EscapeAction.SampleSpike ? 19 + (i % 3) * 5 : 0; line(p, 103 + i * 17, 143, 99 + i * 17, 143 - h, response == EscapeAction.SampleSpike ? 7 : 1) }
            p.fillRect(105, 164, 110, 4, 5)
        } else if (station == 13) { // measured drops enter a marked beaker
            p.fillRect(108, 101, 104, 62, 12); p.drawRect(111, 105, 98, 54, 9); p.fillRect(116, 137, 88, 18, response == EscapeAction.TitrationBloom ? 10 : response == EscapeAction.TitrationOverflow ? 3 : response == EscapeAction.TitrationClear ? 1 : 8)
            p.fillRect(143, 94, 34, 12, 5); p.fillRect(156, 102, 8, 9, 5)
            for (let i = 0; i < fixture + 1; i++) p.fillRect(127 + i * 14, 115 + pulse * 2, 4, 6, 11)
            p.fillRect(120, 126, 21, 2, 15); p.fillRect(178, 126, 21, 2, 15)
        } else if (station == 14) { // brass balance with visible pans and weight blocks
            p.fillRect(156, 101, 8, 60, 5); p.fillRect(139, 156, 42, 6, 4); p.fillRect(147, 162, 27, 4, 1)
            let shift = response == EscapeAction.ScaleLeft ? 13 : response == EscapeAction.ScaleRight ? -13 : 0
            line(p, 83, 121 + shift, 237, 121 - shift, 9); line(p, 84, 122 + shift, 237, 122 - shift, 1)
            line(p, 99, 123 + shift, 93, 143 + shift, 5); line(p, 222, 123 - shift, 228, 143 - shift, 5)
            p.fillRect(74, 143 + shift, 39, 6, 10); p.fillRect(209, 143 - shift, 39, 6, 10)
            p.fillRect(85, 128 + shift, 17, 13, 4); p.fillRect(213, 131 - shift, 17, 10, 8)
        } else if (station == 15) { // colored wires feed a sorter and eject tray
            p.fillRect(242, 96, 20, 73, 12); frame(p, 242, 96, 20, 73, 5)
            for (let i = 0; i < 4; i++) { let col = i == 0 ? 13 : i == 1 ? 3 : i == 2 ? 1 : 6; line(p, 62, 105 + i * 15, response == EscapeAction.WireEject ? 170 - pulse * 15 : 238, 105 + i * 15, col); p.fillRect(57, 102 + i * 15, 12, 7, col) }
            p.fillRect(180, 103, 40, 57, 5); frame(p, 180, 103, 40, 57, 9); lamp(p, 200, 130, response == EscapeAction.WireInstall ? 10 : 3, phase)
        } else if (station == 16) { // pruning shears above a branching plant
            p.fillRect(154, 130, 13, 35, 5); p.fillRect(157, 107, 7, 25, 7)
            for (let i = 0; i < 5; i++) { let yy = 111 + i * 10; let xx = i % 2 == 0 ? 127 : 165; let clipped = response == EscapeAction.LeafClip && i == 4; p.fillRect(xx, yy + (clipped ? pulse * 8 : 0), 28, 7, clipped ? 4 : 7); p.fillRect(xx + (i % 2 == 0 ? 2 : 21), yy - 3, 5, 5, 10) }
            p.fillRect(136, 164, 50, 4, 4); p.fillRect(146, 168, 30, 3, 2)
        } else if (station == 17) { // patched vessel, temperature column and visible leak
            p.fillRect(122, 96, 76, 67, 12); p.drawRect(126, 100, 68, 59, 9); p.fillRect(132, 135, 56, 20, response == EscapeAction.VesselReveal ? 10 : 8)
            p.fillRect(153, 86, 15, 15, 5); p.fillRect(157, 77, 7, 11, 3); p.fillRect(116, 121, 6, 19, response == EscapeAction.VesselLeak ? 3 : 7)
            if (response == EscapeAction.VesselLeak) for (let i = 0; i < 4; i++) p.fillRect(202 + i * 6, 145 + pulse * 4, 4, 8, 11)
            if (response == EscapeAction.VesselBlank) p.fillRect(133, 138, 55, 15, 1)
            if (response == EscapeAction.VesselReveal) { p.print("SUN", 144, 139, 1); p.drawCircle(160, 130, 7, 4) }
        } else if (station == 18) { // pedal receiver: lead, dial and waveform display
            p.fillRect(72, 143, 57, 18, 5); p.fillRect(82, 137, 38, 7, 4); p.fillRect(91, 161, 22, 5, 1)
            p.fillRect(139, 99, 113, 67, 1); frame(p, 139, 99, 113, 67, 9); p.drawCircle(94, 119, 20, 9); p.drawCircle(94, 119, 13, 5); line(p, 94, 119, 104, 108, 10)
            for (let i = 0; i < 8; i++) { let h = response == EscapeAction.ReceiverClear ? 25 : response == EscapeAction.ReceiverStatic ? 10 + ((i + pulse) % 3) * 8 : 4; p.fillRect(151 + i * 11, 151 - h, 6, h, response == EscapeAction.ReceiverClear ? 7 : 6) }
        } else if (station == 19) { // mixer console exposes three separate noisy faders
            p.fillRect(62, 101, 196, 64, 12); frame(p, 62, 101, 196, 64, 5)
            for (let i = 0; i < 3; i++) { let yy = 111 + i * 17; p.fillRect(76, yy, 168, 3, 8); let noisy = fixture == i || fixture == 3; let distort = response == EscapeAction.NoiseDistort; if ((noisy || distort) && response != EscapeAction.NoiseClear) for (let j = 0; j < (distort ? 11 : 9); j++) p.fillRect(82 + j * 14, yy - ((j + pulse) % 2) * (distort ? 9 : 5), 5, 11, 3); p.fillRect(91 + i * 42, yy - 4, 8, 11, 10); p.print(i == 0 ? "SCR" : i == 1 ? "BEEP" : "HUM", 215, yy - 5, noisy || distort ? 3 : 9) }
        } else if (station == 20) { // paper path exits a radio printer
            p.fillRect(81, 97, 157, 62, 5); frame(p, 81, 97, 157, 62, 4); p.fillRect(96, 106, 127, 29, 1); p.fillRect(105, 111, 108, 17, 12)
            p.fillRect(145, 158, 36, response == EscapeAction.PrinterFeed ? 18 + pulse * 3 : response == EscapeAction.PrinterJam ? 9 : 4, 15); p.fillRect(151, response == EscapeAction.PrinterJam ? 160 + pulse % 2 * 3 : 161, 24, 2, response == EscapeAction.PrinterJam ? 3 : 5)
            if (response == EscapeAction.PrinterFeed) { p.print("SIGNAL", 150, 165, 1); p.fillRect(151, 175, 21, 2, 6) }
            lamp(p, 99, 145, response == EscapeAction.PrinterFeed ? 10 : 3, phase)
        } else if (station == 21) { // branching pneumatic tube carries a colored capsule
            p.fillRect(52, 125, 68, 22, 6); p.drawCircle(120, 136, 10, 5); line(p, 120, 131, 219, 101, 5); line(p, 120, 141, 219, 171, 5); p.drawCircle(219, 101, 11, 8); p.drawCircle(219, 171, 11, 8)
            let cy = response == EscapeAction.TubeLaunch ? (fixture == 0 ? 101 : 171) : response == EscapeAction.TubeDrain ? 164 + pulse * 3 : 136; let cx = response == EscapeAction.TubeLaunch ? 156 + pulse * 19 : response == EscapeAction.TubeDrain ? 245 : 93; p.fillRect(cx, cy - 6, 13, 12, 10); p.fillRect(cx + 3, cy - 3, 7, 6, 4)
        } else if (station == 22) { // pressure gauge, repaired seal and sliding bulkhead
            let released = response == EscapeAction.SealRetract
            let sealed = response == EscapeAction.SealStable || pressureReady
            let fault = response == EscapeAction.SealLeak || response == EscapeAction.SealVent
            let gaugeColor = released || sealed ? 7 : fault ? 3 : 8
            p.drawCircle(103, 130, 31, 9); p.drawCircle(103, 130, 24, 15); p.drawCircle(103, 130, 2, 1); line(p, 103, 130, 103 + (fixture - 1) * 14, 111, gaugeColor)
            for (let i = 0; i < 4; i++) p.fillRect(84 + i * 13, 156, 8, 3, 10)
            p.fillRect(released ? 224 + pulse * 10 : 178, 92, 30, 78, released || sealed ? 7 : 5); p.fillRect(176, 92, 5, 78, 1)
            if (response == EscapeAction.SealLeak) for (let i = 0; i < 4; i++) p.fillRect(162 + pulse * 3, 106 + i * 12, 5, 4, 11)
            if (response == EscapeAction.SealVent) { p.fillRect(99, 98, 8, 32, 11); p.fillRect(89, 99, 8, 25, 11); p.fillRect(113, 99, 8, 25, 11) }
            p.print(released ? "RELEASE" : sealed ? "SEALED" : response == EscapeAction.SealLeak ? "LEAK" : response == EscapeAction.SealVent ? "VENT" : "OPEN", 83, 166, gaugeColor)
        } else if (station == 23) { // tilted floor, hanging plumb line and loose brass spheres
            let dy = Math.idiv(Math.max(-90, Math.min(90, pitch)), 9)
            line(p, 49, 132 + dy, 271, 132 - dy, response == EscapeAction.PitchLevel ? 10 : 5); line(p, 55, 136 + dy, 265, 136 - dy, 1)
            p.fillRect(98, 151 + Math.max(-8, Math.min(8, dy)), 17, 14, 8); p.fillRect(202, 151 - Math.max(-8, Math.min(8, dy)), 13, 11, 4)
            p.fillRect(155, 93, 4, 47, 9); p.fillRect(149, 138, 16, 15, 3); p.print("LEVEL", 142, 158, response == EscapeAction.PitchLevel ? 7 : 1)
        } else if (station == 24) { // distant lamps connected by a thin sensor bus
            p.fillRect(52, 107, 51, 56, 5); frame(p, 52, 107, 51, 56, 9); p.fillRect(61, 115, 33, 26, 1); p.print("SENSE", 60, 146, 1)
            line(p, 104, 134, 208, 134, 8); p.fillRect(129, 130, 43, 7, 5)
            for (let i = 0; i < 3; i++) { let active = response == EscapeAction.SensorLamp1 + i; lamp(p, 229, 107 + i * 28, active ? 10 : response == EscapeAction.SensorDark && phase % 2 == i % 2 ? 3 : 1, phase + i); line(p, 210, 107 + i * 28, 224, 107 + i * 28, 8) }
        } else if (station == 25) { // three shutters open to reveal moving air
            for (let i = 0; i < 3; i++) { let open = response == EscapeAction.ShutterOpen; let slam = response == EscapeAction.ShutterClosed && pulse % 2 == 0; p.fillRect(76 + i * 73, open ? 93 - pulse * 5 : slam ? 104 : 98, 39, open ? 21 : slam ? 67 : 74, response == EscapeAction.ShutterWarn ? 3 : 8); p.fillRect(79 + i * 73, 98, 33, 5, 5); p.fillRect(79 + i * 73, 166, 33, 5, 5) }
            if (response == EscapeAction.ShutterOpen) for (let i = 0; i < 5; i++) { line(p, 65 + i * 39, 151, 86 + i * 39, 137 - pulse * 4, 11); p.fillRect(80 + i * 38, 132 - pulse * 4, 4, 4, 15) }
            if (response == EscapeAction.ShutterWarn) { p.fillRect(140, 172, 40, 4, 3); p.print("WARNING", 140, 174, 15) }
        } else if (station == 26) { // three star circuits light in sequence and align
            for (let i = 0; i < 3; i++) { let yy = 105 + i * 22; line(p, 71, yy, 239, yy, response == EscapeAction.StarIgnite ? 11 : i == fixture ? 3 : 8); p.fillRect(85, yy - 4, 14, 8, i == fixture && response != EscapeAction.StarIgnite ? 3 : 5); p.fillRect(211, yy - 4, 14, 8, response == EscapeAction.StarIgnite ? 10 : 5); p.fillRect(151 + i * 7, yy - 5, 11, 11, 10) }
            p.drawCircle(261, 129, 14, response == EscapeAction.StarIgnite ? 10 : 6); p.drawCircle(261, 129, 6, 1)
            if (response == EscapeAction.StarFizzle) { p.fillRect(250, 111 + pulse * 3, 22, 3, 3); p.fillRect(253, 151 - pulse * 3, 15, 3, 3) }
        } else if (station == 27) { // loose stones form a persistent bridge or tumble away
            p.fillRect(55, 161, 212, 5, 1)
            for (let i = 0; i < 5; i++) { let bx = 64 + i * 42; let by = 137 + (i % 2) * 13 + (response == EscapeAction.RockCollapse && i > 3 ? pulse * 7 : 0); p.fillRect(bx, by, 32, 23, i % 2 == 0 ? 8 : 6); p.drawRect(bx, by, 32, 23, i % 2 == 0 ? 9 : 5); p.fillRect(bx + 5, by + 4, 8, 3, 10) }
            if (response == EscapeAction.RockBeam) for (let i = 0; i < 4; i++) line(p, 96 + i * 42, 145 + (i % 2) * 13, 107 + i * 42, 150 - (i % 2) * 13, 7)
        } else if (station == 28) { // independent power, pressure and signal needles synchronize
            for (let i = 0; i < 3; i++) { let x = 75 + i * 83; frame(p, x, 96, 52, 67, 9); p.fillRect(x + 6, 103, 40, 49, 1); p.drawCircle(x + 26, 125, 15, 8); p.drawCircle(x + 26, 125, 2, 10); line(p, x + 26, 125, x + 26 + (response == EscapeAction.SyncLock ? pulse * 2 : (i + pulse) * 3), 110 + i * 2, response == EscapeAction.SyncLock ? 11 : 3); p.print(i == 0 ? "PWR" : i == 1 ? "AIR" : "SIG", x + 10, 151, 9) }
            if (response == EscapeAction.SyncReject) { p.fillRect(132, 171, 56, 5, 3); p.print("ALARM", 137, 173, 15); for (let i = 0; i < 3; i++) p.fillRect(76 + i * 83, 96, 52, 67, 3) }
        } else { // final brass lever, sealed core door and room-filling light
            p.fillRect(79, 103, 51, 66, 12); frame(p, 79, 103, 51, 66, 5); p.fillRect(97, 120, 7, 27, 9); line(p, 101, 128, response == EscapeAction.LeverPull ? 146 : 119, response == EscapeAction.LeverPull ? 153 : 99, response == EscapeAction.LeverPull ? 10 : 4); p.fillRect(response == EscapeAction.LeverPull ? 141 : 116, response == EscapeAction.LeverPull ? 148 : 94, 12, 8, 3)
            p.fillRect(204, 90, 48, 88, response == EscapeAction.LeverPull ? 10 : 12); frame(p, 204, 90, 48, 88, response == EscapeAction.LeverPull ? 10 : 5); p.fillRect(212, 100, 32, 68, 1); p.fillRect(220, 105, 16, 57, response == EscapeAction.LeverPull ? 11 : 8)
            if (response == EscapeAction.LeverPull) { for (let i = 0; i < 6; i++) line(p, 114 + i * 15, 164, 278, 94 + i * 12, 11); lamp(p, 228, 131, 15, phase) }
            else if (response == EscapeAction.LeverReject) { lamp(p, 228, 131, phase % 2 == 0 ? 3 : 1, phase); p.fillRect(208, 174, 39, 5, 3); p.print("ALARM", 211, 174, 15) }
        }
    }

    export function panel(beat: number, station: number, fixture: number, input: string, clue: string, response: number, credible: boolean, solved: number[], pressureReady: boolean, pitch: number, phase: number): Image {
        let p = image.create(320, 240)
        machineBack(p, station, phase)
        p.fillRect(0, 0, 320, 28, 1)
        let room = Math.idiv(station, 6)
        p.print(roomNames[room] + "  " + shortNames[station] + "   " + (beat + 1), 8, 4, 15)
        let firstPart = station == 7 ? 7 : station == 8 ? 11 : station == 22 ? 26 : 28
        let partCount = station == 7 ? 4 : 2
        if (station == 7 || station == 8 || station == 22 || station == 23) p.print("PART " + (beat - firstPart + 1) + "/" + partCount, 246, 16, 10)
        p.fillRect(10, 33, 300, 13, 1); p.print(clue, 13, 35, 15)
        p.fillRect(10, 49, 300, 19, 5); p.fillRect(12, 51, 296, 2, 9)
        p.print("INPUT " + input, 17, 55, 1)
        mechanism(p, station, beat, fixture, response, pressureReady, pitch, phase)
        p.fillRect(12, 197, 296, 18, response >= 0 && !credible ? 3 : 12)
        p.fillRect(15, 199, 3, 14, response >= 0 && !credible ? 4 : 10)
        if (response < 0) p.print("READY: PRESS A TO OPERATE", 25, 202, 15)
        else if (!credible) p.print("CHECK YOUR RULE, THEN RETRY", 25, 202, 15)
        else p.print(responseNames[response] || "MACHINE RESPONDS", 25, 202, 15)
        p.print("LEFT/RIGHT INPUT  UP/DOWN PART  A GO  B ROOM", 12, 221, 9)
        if (solved[beat] && response < 0) { p.fillRect(246, 73, 57, 12, 7); p.print("RECORDED", 251, 75, 1) }
        return p
    }

    export function ending(kind: number, phase: number): Image {
        let p = image.create(320, 240)
        p.fill(kind == 1 ? 12 : 1)
        for (let i = 0; i < 15; i++) { let x = (i * 53 + phase * 5) % 320; let y = (i * 37 + phase * 3) % 240; p.drawCircle(x, y, i % 3 + 2, i % 2 == 0 ? 10 : 11); line(p, x - 7, y, x + 7, y, i % 2 == 0 ? 10 : 11) }
        for (let i = 0; i < 3; i++) p.drawCircle(160, 69, 58 - i * 15, i == 1 ? 11 : 5)
        p.fillRect(23, 91, 274, 83, 1); p.fillRect(27, 95, 266, 75, 15); frame(p, 23, 91, 274, 83, 10)
        p.print(kind == 1 ? "CORE RESTORED!" : "OBSERVATORY MASTER!", 55, 111, 1)
        p.print(kind == 1 ? "THE STARS RETURN TO VIEW." : "EVERY MACHINE ANSWERS.", 48, 133, 8)
        p.print("B: REPLAY THE ADVENTURE", 60, 153, 5)
        return p
    }
}

namespace userconfig {
    export const ARCADE_SCREEN_WIDTH = 320
    export const ARCADE_SCREEN_HEIGHT = 240
}

//% color=#4767ac icon="\uf11b" block="Escape Room" weight=90
namespace escapeLab {
    const saveKey = "logic-escape-room:v1"
    const saveVersion = 1
    let handlers: (() => void)[] = []
    let solved: number[] = []
    let room = 0
    let firstClear = 0
    let secondClear = 0
    let ending = 0
    let pitch = -20
    let pressureReady = false
    let player: Sprite = null
    let panel = false
    let station = -1
    let beat = -1
    let fixture = 0
    let response = -1
    let credible = true
    let phase = 0
    let lastWorldX = 160
    let lastWorldY = 190
    let resetArmed = false
    let explorerFacing = 0

    const firstBeats = [0,1,2,3,4,5,6,7,11,13,14,15,16,17,18,19,20,21,22,23,24,25,26,28,30,31,32,33,34,35]
    const lastBeats = [0,1,2,3,4,5,6,10,12,13,14,15,16,17,18,19,20,21,22,23,24,25,27,29,30,31,32,33,34,35]
    const stationNames = [
        "MAGNET CRANK", "GENERATOR", "RELEASE CASE", "FIRE SPRINKLER", "CLIMB WALL", "FOOTPRINTS",
        "SHADOW SCREEN", "FOUR PORTRAITS", "COLOR MURAL", "STONE GRID", "TELESCOPE", "THERMAL CACHE",
        "MAGNET SAMPLE", "TITRATION", "BALANCE SCALE", "WIRE SORTER", "LIVING PLANT", "HEAT VESSEL",
        "PEDAL RECEIVER", "NOISE MIXER", "MESSAGE PRINTER", "PNEUMATIC TUBE", "PRESSURE SEAL", "PITCH ROOM",
        "REMOTE SENSORS", "SHUTTER BANK", "STAR WIRES", "ROCK PATH", "SYNCHRONIZER", "FINAL LEVER"
    ]
    const roomNames = ["WARM WORKSHOP", "PRISM GALLERY", "GARDEN LABORATORY", "RELAY LOFT", "SKY VAULT"]
    const clues = [
        "A LARGE MAGNET PULLS IRON.", "THE HAND CRANK STARTS THE ROTOR.", "FREE THE LOCKING PIECE.",
        "WATER COLLAPSES THE FLAME.", "FOUR HOLDS COMPLETE THE WALL.", "A STEP PLUS 3 MUST BE AT MOST 10.",
        "INK SHOWS AT LIGHT 60 OR MORE.", "A LEFT SHOE SENDS A PORTRAIT LEFT.",
        "YELLOW AND BLUE MAKE GREEN.", "MATCH STONE AND SOCKET COLORS.", "ZOOM 3 SHARPENS THE VIEW.",
        "BELOW 20 BLUE; ABOVE 40 RED.", "METAL AND MAGNET MAKE SPIKES.", "7 TO 9 DROPS BLOOM; 10 OVERFLOWS.",
        "EQUAL WEIGHTS LEVEL THE SCALE.", "PURPLE, RED OR BLACK WIRES FIT.", "CLIP LEAVES WITH OVER 3 POINTS.",
        "REPAIR THE VESSEL, THEN HEAT IT.", "40 RPM STATIC; 80 RPM CLEAR.", "REMOVE SCRATCH, BEEP AND HUM.",
        "RADIO OR CABLE FEEDS THE PRINTER.", "PATH A OR B SENDS THE CAPSULE.",
        "STABILIZE AT 48 TO 50; RELEASE AT 20.", "SOFT 10; HARD 25. LEVEL AT ZERO.",
        "SENSOR 1, 2, 3 LIGHT THEIR OWN LAMPS.", "A OR B OPENS; RED CONTROL WARNS.",
        "MATCH ALL THREE STAR LAYERS.", "KEEP COLOR; CHANGE PATTERN.",
        "POWER, PRESSURE, SIGNAL; NO ALARM.", "THREE CORE LIGHTS; NO ALARM."
    ]

    function fresh() {
        room = 0
        ending = 0
        pitch = -20
        pressureReady = false
        solved = []
        for (let i = 0; i < 36; i++) solved.push(0)
    }

    function safeInteger(value: number, fallback: number, low: number, high: number): number {
        // Settings storage is outside this game. Accept only finite whole
        // values, then keep it within a deliberately broad game-safe range.
        if (value != Math.round(value) || value <= -1000000 || value >= 1000000) return fallback
        return Math.max(low, Math.min(high, value))
    }

    function load() {
        let data = settings.readNumberArray(saveKey)
        if (!data || data.length != 43 || data[0] != saveVersion) {
            firstClear = 0
            secondClear = 0
            fresh()
            return
        }
        room = safeInteger(data[1], 0, 0, 4)
        firstClear = data[2] == 1 ? 1 : 0
        secondClear = data[3] == 1 ? 1 : 0
        ending = safeInteger(data[4], 0, 0, 2)
        // Pitch is learner-owned arithmetic. Art may constrain its drawn tilt,
        // but a valid accumulated value must survive a restart unchanged.
        pitch = safeInteger(data[5], -20, -999999, 999999)
        pressureReady = data[6] == 1
        solved = []
        for (let i = 0; i < 36; i++) solved.push(data[7 + i] == 1 ? 1 : 0)
    }

    function save() {
        let data = [saveVersion, room, firstClear, secondClear, ending, pitch, pressureReady ? 1 : 0]
        for (let i = 0; i < 36; i++) data.push(solved[i])
        settings.writeNumberArray(saveKey, data)
    }

    function clearThisGame() {
        resetArmed = false
        firstClear = 0
        secondClear = 0
        fresh()
        save()
        control.reset()
    }

    function stationComplete(s: number): boolean {
        for (let i = firstBeats[s]; i <= lastBeats[s]; i++) if (!solved[i]) return false
        return true
    }

    function roomComplete(r: number): boolean {
        for (let s = r * 6; s < r * 6 + 6; s++) if (!stationComplete(s)) return false
        return true
    }

    function stationX(local: number): number { return 60 + (local % 3) * 100 }
    function stationY(local: number): number { return 78 + Math.idiv(local, 3) * 84 }

    function nearestStation(): number {
        let best = -1
        let distance = 10000
        for (let local = 0; local < 6; local++) {
            let dx = player.x - stationX(local)
            let dy = player.y - stationY(local)
            let d = dx * dx + dy * dy
            if (d < distance) { distance = d; best = room * 6 + local }
        }
        return distance < 1850 ? best : -1
    }

    function openPanel(s: number) {
        station = s
        beat = firstBeats[s]
        for (let i = firstBeats[s]; i <= lastBeats[s]; i++) if (!solved[i]) { beat = i; break }
        fixture = 0
        response = -1
        credible = true
        panel = true
        lastWorldX = player.x
        lastWorldY = player.y
        player.setFlag(SpriteFlag.Invisible, true)
        controller.moveSprite(player, 0, 0)
        draw()
    }

    function closePanel() {
        panel = false
        station = -1
        beat = -1
        fixture = 0
        response = -1
        credible = true
        player.setFlag(SpriteFlag.Invisible, false)
        player.setPosition(lastWorldX, lastWorldY)
        controller.moveSprite(player, 85, 85)
        draw()
    }

    function cancelReset() {
        if (!resetArmed) return
        resetArmed = false
        player.sayText("Reset cancelled", 700, false)
    }

    function fixtureCount(b: number): number {
        if (b == 11 || b == 12 || b == 21 || b == 23 || b == 24 || b == 31 || b == 32 || b == 33 || b == 34) return 5
        if (b == 15 || b == 17 || b == 18 || b == 19 || b == 22 || b == 26 || b == 27 || b == 30) return 4
        if (b == 5 || b == 13 || b == 16 || b == 25 || b == 29 || b == 35) return 3
        if (b == 28) return 4
        return 2
    }

    function inputLabel(b: number, f: number): string {
        if (b == 0) return ["EMPTY HAND", "LARGE MAGNET"][f]
        if (b == 1) return ["EMPTY SOCKET", "HAND CRANK"][f]
        if (b == 2) return ["LOCK ENGAGED", "LOCK FREE"][f]
        if (b == 3) return ["EMPTY CANISTER", "WATER CANISTER"][f]
        if (b == 4) return ["3 HOLDS", "4 HOLDS"][f]
        if (b == 5) return ["STEP 8 + 3", "STEP 7 + 3", "STEP 6 + 3"][f]
        if (b == 6) return ["LIGHT 59", "LIGHT 60"][f]
        if (b >= 7 && b <= 10) return ["RIGHT SHOE = 2", "LEFT SHOE = 1"][f]
        if (b == 11 || b == 12) return ["ALL OFF", "YELLOW", "BLUE", "YELLOW+BLUE", "ALL THREE"][f]
        if (b == 13) return ["RED / BLUE", "BLUE / BLUE", "GOLD / GOLD"][f]
        if (b == 14) return ["ZOOM 2", "ZOOM 3"][f]
        if (b == 15) return ["19 DEGREES", "20 DEGREES", "40 DEGREES", "41 DEGREES"][f]
        if (b == 16) return ["WOOD + MAGNET", "IRON, NO MAGNET", "IRON + MAGNET"][f % 3]
        if (b == 17) return ["6 DROPS", "7 DROPS", "9 DROPS", "10 DROPS"][f]
        if (b == 18) return ["LEFT HEAVY", "EQUAL", "RIGHT HEAVY", "EQUAL"][f]
        if (b == 19) return ["GREEN", "PURPLE", "RED", "BLACK"][f]
        if (b == 20) return ["3-POINT LEAF", "4-POINT LEAF"][f]
        if (b == 21) return ["BROKEN COLD", "BROKEN HOT", "REPAIRED COLD", "REPAIRED HOT", "REPAIRED HOT"][f]
        if (b == 22) return ["39 RPM", "40 RPM", "79 RPM", "80 RPM"][f]
        if (b == 23) return ["SCRATCH", "BEEP", "HUM", "ALL THREE", "QUIET"][f]
        if (b == 24) return ["NO SIGNAL", "RADIO", "CABLE", "BOTH", "NO SIGNAL"][f]
        if (b == 25) return ["DRAIN ROUTE", "ROUTE A", "ROUTE B"][f % 3]
        if (b == 26) return ["PRESSURE 47", "PRESSURE 48", "PRESSURE 50", "PRESSURE 51"][f]
        if (b == 27) return ["PRESSURE 20", "PRESSURE 30", "PRESSURE 20", "PRESSURE 30"][f]
        if (b == 28) return ["SOFT +10", "HARD +25", "SOFT -10", "HARD -25"][f]
        if (b == 29) return ["CURRENT PITCH", "CURRENT PITCH", "CURRENT PITCH"][f]
        if (b == 30) return ["SENSOR 1", "SENSOR 2", "SENSOR 3", "NO SENSOR"][f]
        if (b == 31) return ["WINDOW A", "WINDOW B", "RED HAZARD", "INERT CONTROL", "WINDOW A"][f]
        if (b == 32) return ["FRONT MISMATCH", "MIDDLE MISMATCH", "BACK MISMATCH", "ALL MATCH", "ALL MATCH"][f]
        if (b == 33) return ["NEITHER MATCH", "COLOR ONLY", "PATTERN ONLY", "BOTH MATCH", "COLOR ONLY"][f]
        if (b == 34) {
            if (f == 4 && (!solved[1] || !solved[26] || !solved[27] || !solved[31] || !solved[22] || !solved[23] || !solved[24] || !solved[25] || !solved[30])) return "REPAIR EARLIER MACHINES"
            return ["NO POWER", "NO PRESSURE", "NO SIGNAL", "ALARM", "ALL READY"][f]
        }
        return "CORE LIGHTS " + meterValue(EscapeMeter.CoreLights) + (f == 1 ? " + ALARM" : f == 0 ? " (ONE UNPLUGGED)" : " / QUIET")
    }

    function factValue(fact: EscapeFact): boolean {
        if (fact == EscapeFact.LockFree) return beat == 2 && fixture == 1
        if (fact == EscapeFact.YellowOn) return fixture == 1 || fixture >= 3
        if (fact == EscapeFact.BlueOn) return fixture == 2 || fixture >= 3
        if (fact == EscapeFact.RedOn) return fixture == 4
        if (fact == EscapeFact.Metallic) return beat == 16 && fixture > 0
        if (fact == EscapeFact.MagnetOn) return beat == 16 && (fixture == 0 || fixture == 2)
        if (fact == EscapeFact.VesselRepaired) return beat == 21 && fixture >= 2
        if (fact == EscapeFact.VesselHot) return beat == 21 && (fixture == 1 || fixture >= 3)
        if (fact == EscapeFact.ScratchOn) return beat == 23 && (fixture == 0 || fixture == 3)
        if (fact == EscapeFact.BeepOn) return beat == 23 && (fixture == 1 || fixture == 3)
        if (fact == EscapeFact.HumOn) return beat == 23 && (fixture == 2 || fixture == 3)
        if (fact == EscapeFact.RadioClear) return beat == 24 && (fixture == 1 || fixture == 3)
        if (fact == EscapeFact.CableConnected) return beat == 24 && (fixture == 2 || fixture == 3)
        if (fact == EscapeFact.RouteA) return beat == 25 && fixture == 1
        if (fact == EscapeFact.RouteB) return beat == 25 && fixture == 2
        if (fact == EscapeFact.PressureReady) return pressureReady
        if (fact == EscapeFact.WindowA) return beat == 31 && (fixture == 0 || fixture == 4)
        if (fact == EscapeFact.WindowB) return beat == 31 && fixture == 1
        if (fact == EscapeFact.DangerousControl) return beat == 31 && fixture == 2
        if (fact == EscapeFact.FrontMatch) return beat == 32 && fixture != 0
        if (fact == EscapeFact.MiddleMatch) return beat == 32 && fixture != 1
        if (fact == EscapeFact.BackMatch) return beat == 32 && fixture != 2
        if (fact == EscapeFact.SameColor) return beat == 33 && (fixture == 1 || fixture >= 3)
        if (fact == EscapeFact.SamePattern) return beat == 33 && (fixture == 2 || fixture == 3)
        if (fact == EscapeFact.PowerReady) return beat == 34 && fixture != 0 && solved[1] == 1
        if (fact == EscapeFact.PressureSystemReady) return beat == 34 && fixture != 1 && solved[26] == 1 && solved[27] == 1 && solved[31] == 1
        if (fact == EscapeFact.SignalReady) return beat == 34 && fixture != 2 && solved[22] == 1 && solved[23] == 1 && solved[24] == 1 && solved[25] == 1 && solved[30] == 1
        if (fact == EscapeFact.AlarmOn) return (beat == 34 && fixture == 3) || (beat == 35 && fixture == 1)
        return false
    }

    function meterValue(m: EscapeMeter): number {
        if (m == EscapeMeter.InstalledHolds) return fixture == 0 ? 3 : 4
        if (m == EscapeMeter.StepValue) return [8,7,6][fixture]
        if (m == EscapeMeter.Illumination) return fixture == 0 ? 59 : 60
        if (m == EscapeMeter.ShoeSide) return fixture == 0 ? 2 : 1
        if (m == EscapeMeter.StoneColor) return [1,2,3][fixture]
        if (m == EscapeMeter.SocketColor) return [2,2,3][fixture]
        if (m == EscapeMeter.Zoom) return fixture == 0 ? 2 : 3
        if (m == EscapeMeter.Temperature) return [19,20,40,41][fixture]
        if (m == EscapeMeter.Drops) return [6,7,9,10][fixture]
        if (m == EscapeMeter.LeftWeight) return [7,5,3,5][fixture]
        if (m == EscapeMeter.RightWeight) return 5
        if (m == EscapeMeter.WireColor) return fixture
        if (m == EscapeMeter.LeafPoints) return fixture == 0 ? 3 : 4
        if (m == EscapeMeter.RPM) return [39,40,79,80][fixture]
        if (m == EscapeMeter.PressureTenths) return beat == 26 ? [47,48,50,51][fixture] : [20,30,20,30][fixture]
        if (m == EscapeMeter.PitchChange) return [10,25,-10,-25][fixture]
        if (m == EscapeMeter.PitchAngle) return pitch
        if (m == EscapeMeter.SensorNumber) return [1,2,3,0][fixture]
        if (m == EscapeMeter.CoreLights) return Math.max(0, (solved[32] ? 1 : 0) + (solved[33] ? 1 : 0) + (solved[34] ? 1 : 0) - (beat == 35 && fixture == 0 ? 1 : 0))
        return 0
    }

    function actionBelongs(b: number, a: EscapeAction): boolean {
        if (b == 0) return a == EscapeAction.CrankPull || a == EscapeAction.CrankTwitch
        if (b == 1) return a == EscapeAction.GeneratorSpin || a == EscapeAction.GeneratorSputter
        if (b == 2) return a == EscapeAction.CaseRetract || a == EscapeAction.CaseRattle
        if (b == 3) return a == EscapeAction.FireSteam || a == EscapeAction.FireFlare
        if (b == 4) return a == EscapeAction.WallClimb || a == EscapeAction.WallFlash
        if (b == 5) return a == EscapeAction.FootprintKeep || a == EscapeAction.FootprintDrop
        if (b == 6) return a == EscapeAction.ShadowReveal || a == EscapeAction.ShadowHide
        if (b >= 7 && b <= 10) return a == EscapeAction.PortraitLeft || a == EscapeAction.PortraitRight
        if (b == 11) return a == EscapeAction.MuralBlend || a == EscapeAction.MuralDim
        if (b == 12) return a == EscapeAction.MuralOpen || a == EscapeAction.MuralSpill
        if (b == 13) return a == EscapeAction.StoneSnap || a == EscapeAction.StoneRepel
        if (b == 14) return a == EscapeAction.TelescopeFocus || a == EscapeAction.TelescopeBlur
        if (b == 15) return a >= EscapeAction.ThermalBlue && a <= EscapeAction.ThermalRed
        if (b == 16) return a == EscapeAction.SampleSpike || a == EscapeAction.SampleFlat
        if (b == 17) return a >= EscapeAction.TitrationClear && a <= EscapeAction.TitrationOverflow
        if (b == 18) return a >= EscapeAction.ScaleLevel && a <= EscapeAction.ScaleRight
        if (b == 19) return a == EscapeAction.WireInstall || a == EscapeAction.WireEject
        if (b == 20) return a == EscapeAction.LeafClip || a == EscapeAction.LeafKeep
        if (b == 21) return a >= EscapeAction.VesselReveal && a <= EscapeAction.VesselLeak
        if (b == 22) return a >= EscapeAction.ReceiverClear && a <= EscapeAction.ReceiverDead
        if (b == 23) return a == EscapeAction.NoiseClear || a == EscapeAction.NoiseDistort
        if (b == 24) return a == EscapeAction.PrinterFeed || a == EscapeAction.PrinterJam
        if (b == 25) return a == EscapeAction.TubeLaunch || a == EscapeAction.TubeDrain
        if (b == 26) return a == EscapeAction.SealStable || a == EscapeAction.SealLeak
        if (b == 27) return a == EscapeAction.SealRetract || a == EscapeAction.SealVent
        if (b == 29) return a >= EscapeAction.PitchLevel && a <= EscapeAction.PitchUp
        if (b == 30) return a >= EscapeAction.SensorLamp1 && a <= EscapeAction.SensorDark
        if (b == 31) return a >= EscapeAction.ShutterOpen && a <= EscapeAction.ShutterClosed
        if (b == 32) return a == EscapeAction.StarIgnite || a == EscapeAction.StarFizzle
        if (b == 33) return a == EscapeAction.RockBeam || a == EscapeAction.RockCollapse
        if (b == 34) return a == EscapeAction.SyncLock || a == EscapeAction.SyncReject
        if (b == 35) return a == EscapeAction.LeverPull || a == EscapeAction.LeverReject
        return false
    }

    function progressAction(b: number, a: EscapeAction): boolean {
        if (b >= 7 && b <= 10) return a == EscapeAction.PortraitLeft || a == EscapeAction.PortraitRight
        if (b == 15) return a == EscapeAction.ThermalAmber
        if (b == 30) return a >= EscapeAction.SensorLamp1 && a <= EscapeAction.SensorLamp3
        if (b == 29) return a == EscapeAction.PitchLevel
        const wins = [
            EscapeAction.CrankPull, EscapeAction.GeneratorSpin, EscapeAction.CaseRetract,
            EscapeAction.FireSteam, EscapeAction.WallClimb, EscapeAction.FootprintKeep,
            EscapeAction.ShadowReveal, EscapeAction.PortraitLeft, EscapeAction.PortraitLeft,
            EscapeAction.PortraitLeft, EscapeAction.PortraitLeft, EscapeAction.MuralBlend,
            EscapeAction.MuralOpen, EscapeAction.StoneSnap, EscapeAction.TelescopeFocus,
            EscapeAction.ThermalAmber, EscapeAction.SampleSpike, EscapeAction.TitrationBloom,
            EscapeAction.ScaleLevel, EscapeAction.WireInstall, EscapeAction.LeafClip,
            EscapeAction.VesselReveal, EscapeAction.ReceiverClear, EscapeAction.NoiseClear,
            EscapeAction.PrinterFeed, EscapeAction.TubeLaunch, EscapeAction.SealStable,
            EscapeAction.SealRetract, EscapeAction.PitchLevel, EscapeAction.PitchLevel,
            EscapeAction.SensorLamp1, EscapeAction.ShutterOpen, EscapeAction.StarIgnite,
            EscapeAction.RockBeam, EscapeAction.SyncLock, EscapeAction.LeverPull
        ]
        return a == wins[b]
    }

    // Causal credit observer only. It never selects or runs an action for the
    // learner; it prevents an unconditional action from banking a checkpoint.
    function matchesInput(b: number, a: EscapeAction): boolean {
        if (b == 0) return a == (has(EscapeItem.LargeMagnet) ? EscapeAction.CrankPull : EscapeAction.CrankTwitch)
        if (b == 1) return a == (has(EscapeItem.HandCrank) ? EscapeAction.GeneratorSpin : EscapeAction.GeneratorSputter)
        if (b == 2) return a == (factValue(EscapeFact.LockFree) ? EscapeAction.CaseRetract : EscapeAction.CaseRattle)
        if (b == 3) return a == (has(EscapeItem.WaterCanister) ? EscapeAction.FireSteam : EscapeAction.FireFlare)
        if (b == 4) return a == (meterValue(EscapeMeter.InstalledHolds) == 4 ? EscapeAction.WallClimb : EscapeAction.WallFlash)
        if (b == 5) return a == (meterValue(EscapeMeter.StepValue) + 3 <= 10 ? EscapeAction.FootprintKeep : EscapeAction.FootprintDrop)
        if (b == 6) return a == (meterValue(EscapeMeter.Illumination) >= 60 ? EscapeAction.ShadowReveal : EscapeAction.ShadowHide)
        if (b >= 7 && b <= 10) return a == (meterValue(EscapeMeter.ShoeSide) == 1 ? EscapeAction.PortraitLeft : EscapeAction.PortraitRight)
        if (b == 11) return a == (factValue(EscapeFact.YellowOn) && factValue(EscapeFact.BlueOn) ? EscapeAction.MuralBlend : EscapeAction.MuralDim)
        if (b == 12) return a == (factValue(EscapeFact.YellowOn) && factValue(EscapeFact.BlueOn) && !factValue(EscapeFact.RedOn) ? EscapeAction.MuralOpen : EscapeAction.MuralSpill)
        if (b == 13) return a == (meterValue(EscapeMeter.StoneColor) == meterValue(EscapeMeter.SocketColor) ? EscapeAction.StoneSnap : EscapeAction.StoneRepel)
        if (b == 14) return a == (meterValue(EscapeMeter.Zoom) >= 3 ? EscapeAction.TelescopeFocus : EscapeAction.TelescopeBlur)
        if (b == 15) return a == (meterValue(EscapeMeter.Temperature) < 20 ? EscapeAction.ThermalBlue : meterValue(EscapeMeter.Temperature) > 40 ? EscapeAction.ThermalRed : EscapeAction.ThermalAmber)
        if (b == 16) return a == (factValue(EscapeFact.Metallic) && factValue(EscapeFact.MagnetOn) ? EscapeAction.SampleSpike : EscapeAction.SampleFlat)
        if (b == 17) return a == (meterValue(EscapeMeter.Drops) < 7 ? EscapeAction.TitrationClear : meterValue(EscapeMeter.Drops) <= 9 ? EscapeAction.TitrationBloom : EscapeAction.TitrationOverflow)
        if (b == 18) return a == (meterValue(EscapeMeter.LeftWeight) == meterValue(EscapeMeter.RightWeight) ? EscapeAction.ScaleLevel : meterValue(EscapeMeter.LeftWeight) > meterValue(EscapeMeter.RightWeight) ? EscapeAction.ScaleLeft : EscapeAction.ScaleRight)
        if (b == 19) return a == (meterValue(EscapeMeter.WireColor) >= 1 && meterValue(EscapeMeter.WireColor) <= 3 ? EscapeAction.WireInstall : EscapeAction.WireEject)
        if (b == 20) return a == (meterValue(EscapeMeter.LeafPoints) > 3 ? EscapeAction.LeafClip : EscapeAction.LeafKeep)
        if (b == 21) return a == (factValue(EscapeFact.VesselRepaired) && factValue(EscapeFact.VesselHot) ? EscapeAction.VesselReveal : factValue(EscapeFact.VesselRepaired) ? EscapeAction.VesselBlank : EscapeAction.VesselLeak)
        if (b == 22) return a == (meterValue(EscapeMeter.RPM) >= 80 ? EscapeAction.ReceiverClear : meterValue(EscapeMeter.RPM) >= 40 ? EscapeAction.ReceiverStatic : EscapeAction.ReceiverDead)
        if (b == 23) return a == (!factValue(EscapeFact.ScratchOn) && !factValue(EscapeFact.BeepOn) && !factValue(EscapeFact.HumOn) ? EscapeAction.NoiseClear : EscapeAction.NoiseDistort)
        if (b == 24) return a == (factValue(EscapeFact.RadioClear) || factValue(EscapeFact.CableConnected) ? EscapeAction.PrinterFeed : EscapeAction.PrinterJam)
        if (b == 25) return a == (factValue(EscapeFact.RouteA) || factValue(EscapeFact.RouteB) ? EscapeAction.TubeLaunch : EscapeAction.TubeDrain)
        if (b == 26) return a == (meterValue(EscapeMeter.PressureTenths) >= 48 && meterValue(EscapeMeter.PressureTenths) <= 50 ? EscapeAction.SealStable : EscapeAction.SealLeak)
        if (b == 27) return a == (pressureReady && meterValue(EscapeMeter.PressureTenths) == 20 ? EscapeAction.SealRetract : EscapeAction.SealVent)
        if (b == 29) return a == (pitch == 0 ? EscapeAction.PitchLevel : pitch < 0 ? EscapeAction.PitchDown : EscapeAction.PitchUp)
        if (b == 30) return a == (fixture == 0 ? EscapeAction.SensorLamp1 : fixture == 1 ? EscapeAction.SensorLamp2 : fixture == 2 ? EscapeAction.SensorLamp3 : EscapeAction.SensorDark)
        if (b == 31) return a == (factValue(EscapeFact.WindowA) || factValue(EscapeFact.WindowB) ? EscapeAction.ShutterOpen : factValue(EscapeFact.DangerousControl) ? EscapeAction.ShutterWarn : EscapeAction.ShutterClosed)
        if (b == 32) return a == (factValue(EscapeFact.FrontMatch) && factValue(EscapeFact.MiddleMatch) && factValue(EscapeFact.BackMatch) ? EscapeAction.StarIgnite : EscapeAction.StarFizzle)
        if (b == 33) return a == (factValue(EscapeFact.SameColor) && !factValue(EscapeFact.SamePattern) ? EscapeAction.RockBeam : EscapeAction.RockCollapse)
        if (b == 34) return a == (factValue(EscapeFact.PowerReady) && factValue(EscapeFact.PressureSystemReady) && factValue(EscapeFact.SignalReady) && !factValue(EscapeFact.AlarmOn) ? EscapeAction.SyncLock : EscapeAction.SyncReject)
        if (b == 35) return a == (meterValue(EscapeMeter.CoreLights) == 3 && !factValue(EscapeFact.AlarmOn) ? EscapeAction.LeverPull : EscapeAction.LeverReject)
        return false
    }

    function draw() {
        if (ending > 0) scene.setBackgroundImage(escapeArt.ending(ending, phase))
        else if (panel) scene.setBackgroundImage(escapeArt.panel(beat, station, fixture, inputLabel(beat, fixture), clues[station], response, credible, solved, pressureReady, pitch, phase))
        else scene.setBackgroundImage(escapeArt.world(room, roomNames[room], stationNames, solved, firstBeats, lastBeats, pitch, phase, nearestStation(), firstClear))
    }

    function keepPlayerOnPaths() {
        if (panel || ending > 0) return
        player.x = Math.max(8, Math.min(312, player.x))
        player.y = Math.max(43, Math.min(214, player.y))
        // Device bases occupy only their small display footprints. The rows
        // immediately below them and the two vertical aisles remain open.
        for (let local = 0; local < 6; local++) {
            let x = stationX(local)
            let y = stationY(local)
            let dx = player.x - x
            let dy = player.y - y
            // The extra edge room accounts for the explorer sprite itself,
            // rather than allowing its feet to overlap a device base.
            if (Math.abs(dx) >= 34 || Math.abs(dy) >= 27) continue
            if (Math.abs(dx) * 27 > Math.abs(dy) * 34) player.x = x + (dx < 0 ? -34 : 34)
            else player.y = y + (dy < 0 ? -27 : 27)
        }
    }

    function updateExplorer() {
        if (panel || ending > 0) return
        let moving = Math.abs(player.vx) + Math.abs(player.vy) > 1
        if (Math.abs(player.vx) > Math.abs(player.vy) && Math.abs(player.vx) > 1) explorerFacing = player.vx < 0 ? 1 : 2
        else if (Math.abs(player.vy) > 1) explorerFacing = player.vy < 0 ? 3 : 0
        player.setImage(escapeArt.explorer(explorerFacing, moving ? phase % 3 + 1 : 0))
    }

    //% block="when $b mechanism is operated" draggableParameters=reporter
    //% weight=100
    export function onAttempt(b: EscapeBeat, handler: () => void) { handlers[b] = handler }

    //% block="player has $item" weight=90
    export function has(item: EscapeItem): boolean {
        if (!panel) return false
        if (item == EscapeItem.LargeMagnet) return beat == 0 && fixture == 1
        if (item == EscapeItem.HandCrank) return beat == 1 && fixture == 1 && solved[0] == 1
        if (item == EscapeItem.WaterCanister) return beat == 3 && fixture == 1
        return false
    }

    //% block="is $fact" weight=80
    export function is(fact: EscapeFact): boolean { return factValue(fact) }

    //% block="value of $meter" weight=70
    export function number(meter: EscapeMeter): number { return meterValue(meter) }

    //% block="make $action happen" weight=60
    export function make(action: EscapeAction) {
        if (!panel || !actionBelongs(beat, action)) return
        response = action
        credible = matchesInput(beat, action)
        if (action == EscapeAction.SealStable) pressureReady = credible
        if (action == EscapeAction.SealLeak) pressureReady = false
        if (beat == 27) pressureReady = false
        if (credible && progressAction(beat, action)) {
            solved[beat] = 1
            if (action == EscapeAction.LeverPull) {
                if (firstClear == 0) { firstClear = 1; ending = 1 }
                else { secondClear = 1; ending = 2 }
                panel = false
            }
        }
        save()
        draw()
    }

    //% block="set room pitch to $newAngle" weight=50
    export function setPitch(newAngle: number) {
        if (!panel || beat != 28) return
        credible = newAngle == pitch + meterValue(EscapeMeter.PitchChange)
        pitch = newAngle
        if (credible) solved[28] = 1
        response = EscapeAction.PitchUp
        save()
        draw()
    }

    controller.A.onEvent(ControllerButtonEvent.Pressed, function () {
        if (ending > 0) return
        if (panel) {
            response = -1
            let handler = handlers[beat]
            if (handler) handler()
            draw()
            return
        }
        if (resetArmed) {
            cancelReset()
            return
        }
        if (player.x > 292 && room < 4) {
            if (roomComplete(room)) { room++; player.setPosition(24, 190); save(); draw() }
            else player.sayText("Finish six mechanisms", 900, false)
            return
        }
        if (player.x < 28 && room > 0) { room--; player.setPosition(292, 190); save(); draw(); return }
        let s = nearestStation()
        if (s >= 0) openPanel(s)
    })

    controller.B.onEvent(ControllerButtonEvent.Pressed, function () {
        if (ending > 0) {
            fresh()
            save()
            control.reset()
            return
        }
        if (panel) {
            closePanel()
            save()
            return
        }
        if (room == 0 && player.x < 28) {
            if (resetArmed) clearThisGame()
            else {
                resetArmed = true
                player.sayText("Press B again to reset. A cancels.", 1500, false)
            }
        }
    })

    controller.left.onEvent(ControllerButtonEvent.Pressed, function () {
        if (!panel) { cancelReset(); return }
        fixture = (fixture + fixtureCount(beat) - 1) % fixtureCount(beat)
        response = -1
        draw()
    })
    controller.right.onEvent(ControllerButtonEvent.Pressed, function () {
        if (!panel) { cancelReset(); return }
        fixture = (fixture + 1) % fixtureCount(beat)
        response = -1
        draw()
    })
    controller.up.onEvent(ControllerButtonEvent.Pressed, function () {
        if (!panel) { cancelReset(); return }
        if (beat <= firstBeats[station]) return
        beat--
        fixture = 0
        response = -1
        draw()
    })
    controller.down.onEvent(ControllerButtonEvent.Pressed, function () {
        if (!panel) { cancelReset(); return }
        if (beat >= lastBeats[station]) return
        beat++
        fixture = 0
        response = -1
        draw()
    })

    load()
    escapeArt.installPalette()
    player = sprites.create(escapeArt.explorer(0, 0), SpriteKind.Player)
    player.setPosition(160, 190)
    controller.moveSprite(player, 85, 85)
    player.setStayInScreen(true)
    if (ending > 0) { player.setFlag(SpriteFlag.Invisible, true); controller.moveSprite(player, 0, 0) }
    game.onUpdateInterval(120, function () {
        phase++
        keepPlayerOnPaths()
        updateExplorer()
        draw()
    })
    draw()
}
```
