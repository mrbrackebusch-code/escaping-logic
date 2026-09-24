# Escaping Logic

### @explicitHints true

## Welcome to the escape rooms

These five connected escape rooms react only to rules you write. Walk with the arrow keys. Near a lit mechanism, press **A** once to focus it. While focused, **left/right** adjust its visible setting and **up/down** choose a part of a multipart apparatus. Press **A** again to operate the focused mechanism; press **B** to return to walking. In MakeCode Arcade, **Z** or **Space** is **A**, and **X** is **B**. Use the simulator's fullscreen button when testing so you can see the room clearly. A solved mechanism stays in the room, so you can return and test a changed rule locally. Progress is saved in this project across simulator restarts and code edits. Keep using this same project, and follow the next gold light instead of replaying earlier rooms.

Each construction begins with ``||escapeLab(noclick):when [mechanism] is operated||``. The event supplies the moment; your native ``||logic(noclick):if then else||`` decides the response. The room does not supply a missing decision. A dim object is a future possibility, and the lit object is the one whose next reaction matters now.

## 1. Clear the fire channel

The fixed fire spout blocks the wall route. First build ``||escapeLab(noclick):when [fire spout] is operated||`` with ``||logic(noclick):if then else||``. Test ``||escapeLab(noclick):is [WaterFlowing]||``; make `FireSteam` happen when it is true and `FireFlare` otherwise. Then focus the fire spout and press **A** again to operate it. Because water is not flowing yet, `FireFlare` makes the explorer scurry briefly and safely. You need both branches because you will return after water reaches this spout; that alternate reaction lights the sealed case reservoir next.

### Find the native Blocks

![Find the native Blocks for Fire](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/3821640e629f7806/media/menu/01-fire-01-fire-menu.svg)

### One possible construction

![One possible construction for Fire](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/3821640e629f7806/media/assembled/01-fire-01-fire-assembled.svg)

### What the mechanism does

![What the mechanism does for Fire](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/3821640e629f7806/media/gameplay/01-fire-connected-v2-01-fire.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.Fire, function () {
    if (escapeLab.is(EscapeFact.WaterFlowing)) escapeLab.make(EscapeAction.FireSteam)
    else escapeLab.make(EscapeAction.FireFlare)
})
```

## 2. Open the reservoir case

The case button cannot release its fixed reservoir until power arrives. In ``||escapeLab(noclick):when [power case] is operated||``, test ``||escapeLab(noclick):is [PowerAvailable]||``. Make `CaseRetract` happen for true and `CaseRattle` happen for else, then operate the unpowered case once to see its restrained rattle. The generator handle is now the uncertain next light. Your rule is already waiting for the later return that makes the case open.

### One possible construction

![One possible construction for Case](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/3821640e629f7806/media/assembled/02-case-02-case-assembled.svg)

### What the mechanism does

![What the mechanism does for Case](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/3821640e629f7806/media/gameplay/02-case-connected-v2-02-case.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.Case, function () {
    if (escapeLab.is(EscapeFact.PowerAvailable)) escapeLab.make(EscapeAction.CaseRetract)
    else escapeLab.make(EscapeAction.CaseRattle)
})
```

## 3. Start the generator

The generator's handle turns only with a crank fitted to its rail. In ``||escapeLab(noclick):when [generator] is operated||``, test ``||escapeLab(noclick):is [CrankFitted]||``. Make `GeneratorSpin` happen when true and `GeneratorSputter` otherwise. Operate it once before the crank is fitted: the rotor stalls, then the magnet rail at the upper left becomes the next goal. This is another ordinary if/else rule whose successful branch will matter when you come back.

### One possible construction

![One possible construction for Generator](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/3821640e629f7806/media/assembled/03-generator-03-generator-assembled.svg)

### What the mechanism does

![What the mechanism does for Generator](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/3821640e629f7806/media/gameplay/03-generator-connected-v2-03-generator.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.Generator, function () {
    if (escapeLab.is(EscapeFact.CrankFitted)) escapeLab.make(EscapeAction.GeneratorSpin)
    else escapeLab.make(EscapeAction.GeneratorSputter)
})
```

## 4. Swing the mounted magnet

The magnet is mounted on a rail; it is not something to collect. In ``||escapeLab(noclick):when [magnet rail] is operated||``, test ``||escapeLab(noclick):is [MagnetTouchingCrank]||``. Make `CrankPull` happen when true and `CrankTwitch` otherwise. Focus the magnet rail, use **left/right** to swing the magnet near the crank, then press **A** to operate it. Choose the near position first: the crank travels along the rail to the generator. Return to the generator, then the case, then the fire spout. Your three earlier rules now spin the generator, open the reservoir, and turn the flame to steam.

### One possible construction

![One possible construction for Crank](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/3821640e629f7806/media/assembled/04-crank-04-crank-assembled.svg)

### What the mechanism does

![What the mechanism does for Crank](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/3821640e629f7806/media/gameplay/04-crank-connected-v2-04-crank.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.Crank, function () {
    if (escapeLab.is(EscapeFact.MagnetTouchingCrank)) escapeLab.make(EscapeAction.CrankPull)
    else escapeLab.make(EscapeAction.CrankTwitch)
})
```

## 5. Raise the wall holds

With the fire channel clear, the wall lever recovers the fixed holds. In ``||escapeLab(noclick):when [climb wall] is operated||``, test ``||escapeLab(noclick):value of [InstalledHolds]||`` = `4`; make `WallClimb` happen when it passes and `WallFlash` otherwise. Choose `4 HOLDS`, then operate the lever after the steam clears. The holds rise into a climbable route, and the lit footprints at the exit tell you what to test next.

### Find the native Blocks

![Find the native Blocks for Wall](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/3821640e629f7806/media/menu/05-wall-05-wall-comparisons-menu.svg)

### One possible construction

![One possible construction for Wall](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/3821640e629f7806/media/assembled/05-wall-05-wall-assembled.svg)

### What the mechanism does

![What the mechanism does for Wall](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/3821640e629f7806/media/gameplay/05-wall-connected-v2-05-wall.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.Wall, function () {
    if (escapeLab.number(EscapeMeter.InstalledHolds) == 4) escapeLab.make(EscapeAction.WallClimb)
    else escapeLab.make(EscapeAction.WallFlash)
})
```

## 6. Choose a safe footprint

The three marked stones show `8`, `7`, and `6`; any value with `+ 3 ≤ 10` is safe. In ``||escapeLab(noclick):when [footprint stones] is operated||``, test ``||escapeLab(noclick):value of [StepValue]|| + 3 ≤ 10``. Make `FootprintKeep` for true and `FootprintDrop` for else. Choose `7` or `6` first—this is a choice puzzle, so it can work immediately. A safe footprint opens the real passage into Room 2 and lights its shadow screen.

### One possible construction

![One possible construction for Footprints](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/3821640e629f7806/media/assembled/06-footprints-06-footprints-assembled.svg)

### What the mechanism does

![What the mechanism does for Footprints](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/3821640e629f7806/media/gameplay/06-footprints-connected-v2-06-footprints.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.Footprints, function () {
    if (escapeLab.number(EscapeMeter.StepValue) + 3 <= 10) escapeLab.make(EscapeAction.FootprintKeep)
    else escapeLab.make(EscapeAction.FootprintDrop)
})
```

## 7. Reveal the shadow route

The shadow screen needs an illumination of `60`, but the beam is still weak. In ``||escapeLab(noclick):when [shadow screen] is operated||``, test ``||escapeLab(noclick):value of [Illumination]|| ≥ 60``. Make `ShadowReveal` when true and `ShadowHide` otherwise. Operate it once to see the dim screen remain closed; the telescope is now lit because it is the missing source of light.

### One possible construction

![One possible construction for Shadow](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/3821640e629f7806/media/assembled/07-shadow-07-shadow-assembled.svg)

### What the mechanism does

![What the mechanism does for Shadow](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/3821640e629f7806/media/gameplay/07-shadow-connected-v2-07-shadow.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.Shadow, function () {
    if (escapeLab.number(EscapeMeter.Illumination) >= 60) escapeLab.make(EscapeAction.ShadowReveal)
    else escapeLab.make(EscapeAction.ShadowHide)
})
```

## 8. Focus the telescope

The telescope needs zoom `3`, though its lens has not yet seated. In ``||escapeLab(noclick):when [telescope] is operated||``, test ``||escapeLab(noclick):value of [Zoom]|| ≥ 3``. Make `TelescopeFocus` for true and `TelescopeBlur` otherwise. Its blurred beam points to the matching-stone socket. The stone is a physical choice you can solve on the first try.

### What the mechanism does

![What the mechanism does for Telescope](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/3821640e629f7806/media/gameplay/08-telescope-connected-v2-08-telescope.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.Telescope, function () {
    if (escapeLab.number(EscapeMeter.Zoom) >= 3) escapeLab.make(EscapeAction.TelescopeFocus)
    else escapeLab.make(EscapeAction.TelescopeBlur)
})
```

## 9. Seat the matching lens stone

Compare ``||escapeLab(noclick):value of [StoneColor]||`` with ``||escapeLab(noclick):value of [SocketColor]||``. In ``||escapeLab(noclick):when [stone sockets] is operated||``, make `StoneSnap` when they are equal and `StoneRepel` otherwise. Choose the matching stone: it seats as a lens, the telescope can now reach `3`, and its focused beam brings the shadow screen to `60`. Return to those two mechanisms; their existing rules reveal the first half of Room 2's exit.

### What the mechanism does

![What the mechanism does for Stones](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/3821640e629f7806/media/gameplay/09-stones-connected-v2-09-stones.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.Stones, function () {
    if (escapeLab.number(EscapeMeter.StoneColor) == escapeLab.number(EscapeMeter.SocketColor)) escapeLab.make(EscapeAction.StoneSnap)
    else escapeLab.make(EscapeAction.StoneRepel)
})
```

## 10. Mix the mural lights

The mural needs yellow and blue light, but its shutters have no power yet. In ``||escapeLab(noclick):when [mural colors] is operated||``, join ``||escapeLab(noclick):is [YellowOn]||`` and ``||escapeLab(noclick):is [BlueOn]||`` with ``||logic(noclick):and||``. Make `MuralBlend` when both pass and `MuralDim` otherwise. **And** needs both conditions, so its dim result points to the frozen portrait rails that will supply the light.

### Find the native Blocks

![Find the native Blocks for MuralMix](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/3821640e629f7806/media/menu/10-mural-mix-10-mural-logic-menu.svg)

### One possible construction

![One possible construction for MuralMix](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/3821640e629f7806/media/assembled/10-mural-mix-10-mural-mix-assembled.svg)

### What the mechanism does

![What the mechanism does for MuralMix](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/3821640e629f7806/media/gameplay/10-mural-mix-connected-v2-10-mural-mix.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.MuralMix, function () {
    if (escapeLab.is(EscapeFact.YellowOn) && escapeLab.is(EscapeFact.BlueOn)) escapeLab.make(EscapeAction.MuralBlend)
    else escapeLab.make(EscapeAction.MuralDim)
})
```

## 11. Open the mural compartment

Build the mural's second rule before its light sources are ready. In ``||escapeLab(noclick):when [mural latch] is operated||``, keep yellow **and** blue and add ``||logic(noclick):not||`` ``||escapeLab(noclick):is [RedOn]||``. Make `MuralOpen` when all three requirements pass; otherwise make `MuralSpill` happen. **Not** expresses the false case: red must be off. The first portrait plate is lit next, but its rail is frozen.

### One possible construction

![One possible construction for MuralReveal](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/3821640e629f7806/media/assembled/11-mural-reveal-11-mural-reveal-assembled.svg)

### What the mechanism does

![What the mechanism does for MuralReveal](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/3821640e629f7806/media/gameplay/11-mural-reveal-connected-v2-11-mural-reveal.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.MuralReveal, function () {
    if (escapeLab.is(EscapeFact.YellowOn) && escapeLab.is(EscapeFact.BlueOn) && !escapeLab.is(EscapeFact.RedOn)) escapeLab.make(EscapeAction.MuralOpen)
    else escapeLab.make(EscapeAction.MuralSpill)
})
```

## 12. Move portrait one

At the first footprint pressure plate, `1` means left and `2` means right. In ``||escapeLab(noclick):when [first portrait] is operated||``, test ``||escapeLab(noclick):value of [ShoeSide]|| = 1``; make `PortraitLeft` when true and `PortraitRight` otherwise. The rail cannot move while it is cold, so operate it once to see that physical limit. The warm bath is the next lit mechanism. Keep this complete stack: it will move portrait one after the bath thaws the rails.

### What the mechanism does

![What the mechanism does for Portrait1](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/3821640e629f7806/media/gameplay/12-portrait1-connected-v2-12-portrait1.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.Portrait1, function () {
    if (escapeLab.number(EscapeMeter.ShoeSide) == 1) escapeLab.make(EscapeAction.PortraitLeft)
    else escapeLab.make(EscapeAction.PortraitRight)
})
```

## 13. Thaw the portrait rails

The bath has cold, warm, and overheated responses. Use the **+** on ``||logic(noclick):if then else||`` to add ``||logic(noclick):else if||`` after a first test is false. In ``||escapeLab(noclick):when [warming bath] is operated||``, make `ThermalBlue` if `Temperature < 20`; make `ThermalRed` in an else-if when `Temperature > 40`; otherwise make `ThermalAmber`. This final else covers `20` through `40`. Choose either `20` or `40` for the warm range, then return to the first portrait: its written rule can now move that rail.

### Find the native Blocks

![Find the native Blocks for Thermal](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/3821640e629f7806/media/menu/13-thermal-13-thermal-elseif-menu.svg)

### One possible construction

![One possible construction for Thermal](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/3821640e629f7806/media/assembled/13-thermal-13-thermal-assembled.svg)

### What the mechanism does

![What the mechanism does for Thermal](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/3821640e629f7806/media/gameplay/13-thermal-connected-v2-13-thermal.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.Thermal, function () {
    if (escapeLab.number(EscapeMeter.Temperature) < 20) escapeLab.make(EscapeAction.ThermalBlue)
    else if (escapeLab.number(EscapeMeter.Temperature) > 40) escapeLab.make(EscapeAction.ThermalRed)
    else escapeLab.make(EscapeAction.ThermalAmber)
})
```

## 14. Move portrait two

Make a separate ``||escapeLab(noclick):when [second portrait] is operated||`` event with the same `ShoeSide = 1` test, `PortraitLeft` true action, and `PortraitRight` else action. A separate stack gives this rail its own rule. The warm bath has thawed it, so the left pressure plate can move it now.

### What the mechanism does

![What the mechanism does for Portrait2](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/3821640e629f7806/media/gameplay/14-portrait2-connected-v2-14-portrait2.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.Portrait2, function () {
    if (escapeLab.number(EscapeMeter.ShoeSide) == 1) escapeLab.make(EscapeAction.PortraitLeft)
    else escapeLab.make(EscapeAction.PortraitRight)
})
```

## 15. Move portrait three

Repeat the portrait rule in a ``||escapeLab(noclick):when [third portrait] is operated||`` event: test `value of ShoeSide = 1`, make `PortraitLeft` for true, and `PortraitRight` for else. This third rail responds to the same physical clue. Use its left plate to align the portrait.

### What the mechanism does

![What the mechanism does for Portrait3](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/3821640e629f7806/media/gameplay/15-portrait3-connected-v2-15-portrait3.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.Portrait3, function () {
    if (escapeLab.number(EscapeMeter.ShoeSide) == 1) escapeLab.make(EscapeAction.PortraitLeft)
    else escapeLab.make(EscapeAction.PortraitRight)
})
```

## 16. Move portrait four

Add the final matching stack in ``||escapeLab(noclick):when [fourth portrait] is operated||``. Use the same left/right condition and actions. Move the fourth portrait left. All four aligned portraits now light the mural's yellow and blue shutters; return to the mural mix and reveal to open the second exit half.

### What the mechanism does

![What the mechanism does for Portrait4](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/3821640e629f7806/media/gameplay/16-portrait4-connected-v2-16-portrait4.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.Portrait4, function () {
    if (escapeLab.number(EscapeMeter.ShoeSide) == 1) escapeLab.make(EscapeAction.PortraitLeft)
    else escapeLab.make(EscapeAction.PortraitRight)
})
```

## 17. Test the magnetic sample

The sample needs a live magnet, but its coil has no allowed wire yet. In ``||escapeLab(noclick):when [magnet sample] is operated||``, join ``||escapeLab(noclick):is [Metallic]||`` and ``||escapeLab(noclick):is [MagnetOn]||`` with **and**. Make `SampleSpike` when both pass and `SampleFlat` otherwise. Its flat reaction lights the wire rack, which is a choice puzzle with an immediate usable answer.

### What the mechanism does

![What the mechanism does for Sample](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/3821640e629f7806/media/gameplay/17-sample-connected-v2-17-sample.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.Sample, function () {
    if (escapeLab.is(EscapeFact.Metallic) && escapeLab.is(EscapeFact.MagnetOn)) escapeLab.make(EscapeAction.SampleSpike)
    else escapeLab.make(EscapeAction.SampleFlat)
})
```

## 18. Install an allowed wire

At the coil, purple, red, and black are allowed. Join the three `value of WireColor =` comparisons with ``||logic(noclick):or||`` in ``||escapeLab(noclick):when [wire sorter] is operated||``. Make `WireInstall` when one comparison passes and `WireEject` otherwise. **Or** accepts at least one usable condition; choose an allowed wire. The energized coil turns on the magnet, so returning to the sample raises the first Room 3 exit catch.

### Find the native Blocks

![Find the native Blocks for Wires](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/3821640e629f7806/media/menu/18-wires-18-wires-or-menu.svg)

### One possible construction

![One possible construction for Wires](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/3821640e629f7806/media/assembled/18-wires-18-wires-assembled.svg)

### What the mechanism does

![What the mechanism does for Wires](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/3821640e629f7806/media/gameplay/18-wires-connected-v2-18-wires.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.Wires, function () {
    if (escapeLab.number(EscapeMeter.WireColor) == 1 || escapeLab.number(EscapeMeter.WireColor) == 2 || escapeLab.number(EscapeMeter.WireColor) == 3) escapeLab.make(EscapeAction.WireInstall)
    else escapeLab.make(EscapeAction.WireEject)
})
```

## 19. Reveal the heat vessel

The vessel needs a freed repair lever before it can seal, so it can only leak now. In ``||escapeLab(noclick):when [heat vessel] is operated||``, first test `is VesselRepaired` **and** `is VesselHot` and make `VesselReveal`. Add an else-if for `is VesselRepaired` that makes `VesselBlank`; make `VesselLeak` in the final else. Put the specific repaired-and-hot case first. The leak lights the plant pruner that can free the lever.

### What the mechanism does

![What the mechanism does for Vessel](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/3821640e629f7806/media/gameplay/19-vessel-connected-v2-19-vessel.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.Vessel, function () {
    if (escapeLab.is(EscapeFact.VesselRepaired) && escapeLab.is(EscapeFact.VesselHot)) escapeLab.make(EscapeAction.VesselReveal)
    else if (escapeLab.is(EscapeFact.VesselRepaired)) escapeLab.make(EscapeAction.VesselBlank)
    else escapeLab.make(EscapeAction.VesselLeak)
})
```

## 20. Free the repair lever

In ``||escapeLab(noclick):when [pruning lever] is operated||``, test ``||escapeLab(noclick):value of [LeafPoints]|| > 3``. Make `LeafClip` happen for true and `LeafKeep` otherwise. Choose a four-point leaf to clear the lever; then use the repair control and heat the vessel. Return to its three-way rule: the sealed hot vessel reveals the second exit catch.

### What the mechanism does

![What the mechanism does for Pruner](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/3821640e629f7806/media/gameplay/20-pruner-connected-v2-20-pruner.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.Pruner, function () {
    if (escapeLab.number(EscapeMeter.LeafPoints) > 3) escapeLab.make(EscapeAction.LeafClip)
    else escapeLab.make(EscapeAction.LeafKeep)
})
```

## 21. Test the titration target

The dropper cannot provide its target amount until the balance releases it. Still build the result rule in ``||escapeLab(noclick):when [titration] is operated||``: if `Drops < 7`, make `TitrationClear`; else if `Drops ≤ 9`, make `TitrationBloom`; otherwise make `TitrationOverflow`. Its low result lights the balance. The target bloom will be your payoff after the dropper can select `7` or `9`.

### What the mechanism does

![What the mechanism does for Titration](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/3821640e629f7806/media/gameplay/21-titration-connected-v2-21-titration.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.Titration, function () {
    if (escapeLab.number(EscapeMeter.Drops) < 7) escapeLab.make(EscapeAction.TitrationClear)
    else if (escapeLab.number(EscapeMeter.Drops) <= 9) escapeLab.make(EscapeAction.TitrationBloom)
    else escapeLab.make(EscapeAction.TitrationOverflow)
})
```

## 22. Balance the dropper

In ``||escapeLab(noclick):when [balance scale] is operated||``, test `value of LeftWeight = value of RightWeight` and make `ScaleLevel`. Add an else-if for left greater than right that makes `ScaleLeft`; make `ScaleRight` in the final else. Choose equal weights first: the balanced scale releases the dropper. Return to titration, choose `7` or `9`, and see the bloom raise the third catch.

### What the mechanism does

![What the mechanism does for Balance](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/3821640e629f7806/media/gameplay/22-balance-connected-v2-22-balance.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.Balance, function () {
    if (escapeLab.number(EscapeMeter.LeftWeight) == escapeLab.number(EscapeMeter.RightWeight)) escapeLab.make(EscapeAction.ScaleLevel)
    else if (escapeLab.number(EscapeMeter.LeftWeight) > escapeLab.number(EscapeMeter.RightWeight)) escapeLab.make(EscapeAction.ScaleLeft)
    else escapeLab.make(EscapeAction.ScaleRight)
})
```

## 23. Launch the pneumatic capsule

The selector needs a printed strip, so the empty tube drains at first. In ``||escapeLab(noclick):when [pneumatic tube] is operated||``, join ``||escapeLab(noclick):is [RouteA]||`` and ``||escapeLab(noclick):is [RouteB]||`` with **or**. Make `TubeLaunch` for true and `TubeDrain` otherwise. The drain lights the printer, whose missing paper source is still farther back in this connected chain.

### What the mechanism does

![What the mechanism does for Tube](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/3821640e629f7806/media/gameplay/23-tube-connected-v2-23-tube.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.Tube, function () {
    if (escapeLab.is(EscapeFact.RouteA) || escapeLab.is(EscapeFact.RouteB)) escapeLab.make(EscapeAction.TubeLaunch)
    else escapeLab.make(EscapeAction.TubeDrain)
})
```

## 24. Feed the message printer

The printer works through clear radio or a connected cable, neither of which is ready yet. In ``||escapeLab(noclick):when [message printer] is operated||``, join `is RadioClear` and `is CableConnected` with **or**. Make `PrinterFeed` when either route works and `PrinterJam` otherwise. The jam points to the noise mixer; its channels cannot all be quiet until a receiver generates a signal.

### What the mechanism does

![What the mechanism does for Printer](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/3821640e629f7806/media/gameplay/24-printer-connected-v2-24-printer.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.Printer, function () {
    if (escapeLab.is(EscapeFact.RadioClear) || escapeLab.is(EscapeFact.CableConnected)) escapeLab.make(EscapeAction.PrinterFeed)
    else escapeLab.make(EscapeAction.PrinterJam)
})
```

## 25. Clear the interference mixer

In ``||escapeLab(noclick):when [noise mixer] is operated||``, join `not is ScratchOn`, `not is BeepOn`, and `not is HumOn` with **and**. Make `NoiseClear` when every channel is off, or `NoiseDistort` otherwise. The receiver is now lit: its pedal produces the signal that lets the mixer quiet the channels. After that, return through mixer, printer, and tube to send the capsule to the exit latch.

### What the mechanism does

![What the mechanism does for Interference](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/3821640e629f7806/media/gameplay/25-interference-connected-v2-25-interference.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.Interference, function () {
    if (!escapeLab.is(EscapeFact.ScratchOn) && !escapeLab.is(EscapeFact.BeepOn) && !escapeLab.is(EscapeFact.HumOn)) escapeLab.make(EscapeAction.NoiseClear)
    else escapeLab.make(EscapeAction.NoiseDistort)
})
```

## 26. Tune the pedal receiver

Use a three-way ``||escapeLab(noclick):when [pedal receiver] is operated||`` rule: make `ReceiverClear` if `RPM ≥ 80`; else if `RPM ≥ 40`, make `ReceiverStatic`; otherwise make `ReceiverDead`. Choose `80 RPM`. That signal makes the mixer controls effective, so the forward chain now has a physical path all the way to the capsule.

### What the mechanism does

![What the mechanism does for Receiver](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/3821640e629f7806/media/gameplay/26-receiver-connected-v2-26-receiver.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.Receiver, function () {
    if (escapeLab.number(EscapeMeter.RPM) >= 80) escapeLab.make(EscapeAction.ReceiverClear)
    else if (escapeLab.number(EscapeMeter.RPM) >= 40) escapeLab.make(EscapeAction.ReceiverStatic)
    else escapeLab.make(EscapeAction.ReceiverDead)
})
```

## 27. Stabilize the pressure seal

Make a native ``||variables(noclick):Variables||`` variable named ``||variables(noclick):pressureReady||``: it remembers whether this local preparation succeeded. In ``||loops(noclick):on start||``, set it to ``||escapeLab(noclick):is [PressureReady]||`` so an earned seal checkpoint can return after reload. In ``||escapeLab(noclick):when [pressure stabilizer] is operated||``, test `value of pressure ≥ 48` **and** `value of pressure ≤ 50`; set `pressureReady` to `true` and make `SealStable` when true, otherwise set it to `false` and make `SealLeak`. Choose `48` or `50`; the stable seal makes the release control usable.

### Find the native Blocks

![Find the native Blocks for PressureStable](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/3821640e629f7806/media/menu/27-pressure-stable-27-pressure-and-pitch-variables-menu.svg)

### One possible construction

![One possible construction for PressureStable](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/3821640e629f7806/media/assembled/27-pressure-stable-27-pressure-stable-assembled.svg)

### What the mechanism does

![What the mechanism does for PressureStable](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/3821640e629f7806/media/gameplay/27-pressure-stable-connected-v2-27-pressure-stable.gif)

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

## 28. Release the pressure lift

In ``||escapeLab(noclick):when [pressure release] is operated||``, join your `pressureReady` variable with `value of pressure = 20`. Make `SealRetract` when both pass and `SealVent` otherwise. After the whole if/else, set `pressureReady` to `false`: every release attempt consumes this preparation. Stabilize first, then choose `20`; the hydraulic lift raises and lights the pitch controls.

### What the mechanism does

![What the mechanism does for PressureRelease](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/3821640e629f7806/media/gameplay/28-pressure-release-connected-v2-28-pressure-release.gif)

#### ~ tutorialhint

```blocks
let pressureReady = escapeLab.is(EscapeFact.PressureReady)

escapeLab.onAttempt(EscapeBeat.PressureRelease, function () {
    if (pressureReady && escapeLab.number(EscapeMeter.PressureTenths) == 20) escapeLab.make(EscapeAction.SealRetract)
    else escapeLab.make(EscapeAction.SealVent)
    pressureReady = false
})
```

## 29. Level the exit bridge

Make a native ``||variables(noclick):Variables||`` variable named ``||variables(noclick):angle||``. In ``||loops(noclick):on start||``, set it to ``||escapeLab(noclick):value of [PitchAngle]||``. In ``||escapeLab(noclick):when [pitch control] is operated||``, change `angle` by `value of PitchChange`, then pass `angle` to ``||escapeLab(noclick):set room pitch to [number]||``. The physical controls provide `+10`, `+25`, `-10`, and `-25`; your variable accumulates them. Bring the gauge to `0`, then use the feedback station.

### One possible construction

![One possible construction for PitchAdjust](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/3821640e629f7806/media/assembled/29-pitch-adjust-29-pitch-adjust-assembled.svg)

### What the mechanism does

![What the mechanism does for PitchAdjust](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/3821640e629f7806/media/gameplay/29-pitch-adjust-connected-v2-29-pitch-adjust.gif)

#### ~ tutorialhint

```blocks
let pressureReady = escapeLab.is(EscapeFact.PressureReady)

let angle = escapeLab.number(EscapeMeter.PitchAngle)

escapeLab.onAttempt(EscapeBeat.PitchAdjust, function () {
    angle += escapeLab.number(EscapeMeter.PitchChange)
    escapeLab.setPitch(angle)
})
```

## 30. Confirm the bridge is level

In ``||escapeLab(noclick):when [pitch display] is operated||``, test your `angle`. Make `PitchLevel` if `angle = 0`; else if `angle < 0`, make `PitchDown`; otherwise make `PitchUp`. Try the negative and positive responses through local control retests if you want to inspect them. Level is the forward result: the bridge settles and opens the final room.

### What the mechanism does

![What the mechanism does for PitchFeedback](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/3821640e629f7806/media/gameplay/30-pitch-feedback-connected-v2-30-pitch-feedback.gif)

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

## 31. Open a shutter route

The shutter bank needs a mapped remote sensor. Build ``||escapeLab(noclick):when [shutter bank] is operated||`` first: if `is WindowA` **or** `is WindowB`, make `ShutterOpen`; else if `is DangerousControl`, make `ShutterWarn`; otherwise make `ShutterClosed`. Its closed response points to the sensor mapper. Keep the usable-window rule first so it stays the main path.

### What the mechanism does

![What the mechanism does for Shutters](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/3821640e629f7806/media/gameplay/31-shutters-connected-v2-31-shutters.gif)

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

In ``||escapeLab(noclick):when [sensor map] is operated||``, use an else-if chain on `value of SensorNumber`: `1` makes `SensorLamp1`, `2` makes `SensorLamp2`, `3` makes `SensorLamp3`, and the final else makes `SensorDark`. Choose the sensor shown by the shutter wiring. Its lamp powers a shutter route, so return to the bank to open it.

### What the mechanism does

![What the mechanism does for Sensors](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/3821640e629f7806/media/gameplay/32-sensors-connected-v2-32-sensors.gif)

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

The rock path is dark until the constellation lights it. Build ``||escapeLab(noclick):when [rock path] is operated||`` now from the visible clue: **keep the color, change the pattern**. Join `is SameColor` and `not is SamePattern` with **and**. Make `RockBeam` for true and `RockCollapse` otherwise. The unlit path points to the constellation controls, where a matching choice can succeed immediately.

### What the mechanism does

![What the mechanism does for RockPath](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/3821640e629f7806/media/gameplay/33-rock-path-connected-v2-33-rock-path.gif)

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

In ``||escapeLab(noclick):when [constellation] is operated||``, join `is FrontMatch`, `is MiddleMatch`, and `is BackMatch` with **and**. Make `StarIgnite` only when all three pass; otherwise make `StarFizzle`. Align the three visible layers. Their flare lights the rock path; return to it and choose same color with a different pattern to cross the bridge.

### What the mechanism does

![What the mechanism does for Constellation](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/3821640e629f7806/media/gameplay/34-constellation-connected-v2-34-constellation.gif)

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

The synchronizer receives the power, pressure, and signal you restored in earlier rooms. In ``||escapeLab(noclick):when [synchronizer] is operated||``, join `is PowerReady`, `is PressureSystemReady`, `is SignalReady`, and `not is AlarmOn` with **and**. Make `SyncLock` when all four requirements pass and `SyncReject` otherwise. With the shutter route and rock bridge complete, the machines phase-lock and light the final lever.

### What the mechanism does

![What the mechanism does for Synchronize](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/3821640e629f7806/media/gameplay/35-synchronize-connected-v2-35-synchronize.gif)

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

In ``||escapeLab(noclick):when [final lever] is operated||``, test `value of CoreLights = 3` **and** `not is AlarmOn`. Make `LeverPull` when it passes and `LeverReject` otherwise. At the first ending, press **B** to start the full replay. It clears room and mechanism checkpoints while retaining first-clear history; a second escape receives its distinct ending.

### What the mechanism does

![What the mechanism does for FinalLever](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/3821640e629f7806/media/gameplay/36-final-lever-connected-v2-36-final-lever.gif)

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

```template
// Logic Escape Room
```

```customts
// The learner-facing nouns. Decisions belong in native if / else blocks.
enum EscapeBeat {
    //% block="magnet rail"
    Crank,
    //% block="generator"
    Generator,
    //% block="power case"
    Case,
    //% block="fire spout"
    Fire,
    //% block="climb wall"
    Wall,
    //% block="footprint stones"
    Footprints,
    //% block="shadow screen"
    Shadow,
    //% block="first portrait"
    Portrait1,
    //% block="second portrait"
    Portrait2,
    //% block="third portrait"
    Portrait3,
    //% block="fourth portrait"
    Portrait4,
    //% block="mural colors"
    MuralMix,
    //% block="mural latch"
    MuralReveal,
    //% block="stone sockets"
    Stones,
    //% block="telescope"
    Telescope,
    //% block="warming bath"
    Thermal,
    //% block="magnet sample"
    Sample,
    //% block="titration"
    Titration,
    //% block="balance scale"
    Balance,
    //% block="wire sorter"
    Wires,
    //% block="pruning lever"
    Pruner,
    //% block="heat vessel"
    Vessel,
    //% block="pedal receiver"
    Receiver,
    //% block="noise mixer"
    Interference,
    //% block="message printer"
    Printer,
    //% block="pneumatic tube"
    Tube,
    //% block="pressure stabilizer"
    PressureStable,
    //% block="pressure release"
    PressureRelease,
    //% block="pitch control"
    PitchAdjust,
    //% block="pitch display"
    PitchFeedback,
    //% block="sensor map"
    Sensors,
    //% block="shutter bank"
    Shutters,
    //% block="constellation"
    Constellation,
    //% block="rock path"
    RockPath,
    //% block="synchronizer"
    Synchronize,
    //% block="final lever"
    FinalLever
}

enum EscapeItem { LargeMagnet, HandCrank, WaterCanister }

enum EscapeFact {
    LockFree, YellowOn, BlueOn, RedOn, Metallic, MagnetOn,
    VesselRepaired, VesselHot, ScratchOn, BeepOn, HumOn,
    RadioClear, CableConnected, RouteA, RouteB, PressureReady,
    WindowA, WindowB, DangerousControl, FrontMatch,
    MiddleMatch, BackMatch, SameColor, SamePattern,
    PowerReady, PressureSystemReady, SignalReady, AlarmOn,
    MagnetTouchingCrank, CrankFitted, PowerAvailable, WaterFlowing
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

// The room route and coordinates are shared by the engine and world artwork.
namespace escapeFlow {
    export const firstBeats = [0,1,2,3,4,5,6,7,11,13,14,15,16,17,18,19,20,21,22,23,24,25,26,28,30,31,32,33,34,35]
    export const lastBeats = [0,1,2,3,4,5,6,10,12,13,14,15,16,17,18,19,20,21,22,23,24,25,27,29,30,31,32,33,34,35]
    export const stationNames = [
        "MAGNET RAIL", "GENERATOR", "POWER CASE", "FIRE SPOUT", "CLIMB WALL", "FOOTPRINTS",
        "SHADOW SCREEN", "PORTRAIT RAILS", "COLOR MURAL", "STONE GRID", "TELESCOPE", "WARMING BATH",
        "MAGNET SAMPLE", "TITRATION", "BALANCE SCALE", "WIRE SORTER", "LIVING PLANT", "HEAT VESSEL",
        "PEDAL RECEIVER", "NOISE MIXER", "MESSAGE PRINTER", "PNEUMATIC TUBE", "PRESSURE SEAL", "PITCH BRIDGE",
        "REMOTE SENSORS", "SHUTTER BANK", "STAR WIRES", "ROCK PATH", "SYNCHRONIZER", "FINAL LEVER"
    ]
    export const roomNames = ["WARM WORKSHOP", "PRISM GALLERY", "GARDEN LABORATORY", "RELAY LOFT", "SKY VAULT"]
    export const clues = [
        "SWING THE MOUNTED MAGNET TO THE CRANK.", "FIT THE CRANK, THEN TURN THE HANDLE.", "POWER OPENS THE RESERVOIR CASE.",
        "TIP THE SPOUT WHEN WATER CAN FLOW.", "RAISE FOUR HOLDS IN THE CLEAR CHANNEL.", "A STEP PLUS 3 MUST BE AT MOST 10.",
        "THE BEAM REVEALS INK AT LIGHT 60.", "A LEFT PRESSURE PLATE SLIDES A PORTRAIT.",
        "YELLOW AND BLUE MAKE GREEN.", "MATCH STONE AND SOCKET COLORS.", "THE SEATED LENS ALLOWS ZOOM 3.",
        "20 TO 40 DEGREES THAWS THE RAILS.", "THE WIRED COIL RAISES A METAL SAMPLE.", "7 TO 9 DROPS BLOOM; 10 OVERFLOWS.",
        "EQUAL WEIGHTS RELEASE THE DROPPER.", "PURPLE, RED OR BLACK WIRES FIT.", "CLIP LEAVES WITH OVER 3 POINTS.",
        "FREE THE REPAIR LEVER, THEN WARM THE VESSEL.", "80 RPM STARTS THE SIGNAL.", "CLEAR SCRATCH, BEEP AND HUM.",
        "RADIO OR CABLE FEEDS THE PAPER STRIP.", "THE PRINTED STRIP ENABLES ROUTE A OR B.",
        "STABILIZE AT 48 TO 50; RELEASE AT 20.", "SOFT 10; HARD 25. LEVEL AT ZERO.",
        "SENSORS 1, 2, 3 LIGHT THEIR LAMPS.", "A OR B OPENS; RED CONTROL WARNS.",
        "MATCH ALL THREE STAR LAYERS.", "KEEP COLOR; CHANGE PATTERN.",
        "POWER, PRESSURE, SIGNAL; NO ALARM.", "THREE CORE LIGHTS; NO ALARM."
    ]
    const xs = [120,330,535,145,330,520, 95,280,510,160,375,545, 135,350,550,90,290,490, 120,320,520,180,385,550, 100,300,530,125,345,525]
    const ys = [125,120,130,315,320,318, 185,105,100,330,325,280, 125,155,160,330,330,335, 130,100,145,315,320,325, 145,110,165,330,325,345]
    export function x(station: number): number { return xs[station] }
    export function y(station: number): number { return ys[station] }
    // Only the solid base blocks walking. Recesses, rails and light cones remain traversable.
    export function width(station: number): number { return station % 6 == 4 ? 42 : station % 6 == 1 ? 54 : 48 }
    export function height(station: number): number { return station % 6 == 4 ? 30 : 34 }
    export function stationForBeat(b: number): number {
        for (let s = 0; s < 30; s++) if (b >= firstBeats[s] && b <= lastBeats[s]) return s
        return -1
    }
    // Positive entry means success; negative entry means a real alternate response
    // must first reveal the upstream apparatus. Zero-based beat b is stored as -(b+1).
    const route = [
        -4,-3,-2,1,2,3,4,5,6,
        -7,-15,14,15,7,-12,-13,-8,16,8,9,10,11,12,13,
        -17,20,17,-22,21,22,-18,19,18,
        -26,-25,-24,23,24,25,26,27,28,29,30,
        -32,31,32,-34,33,34,35,36
    ]
    export function routeEntry(index: number): number { return route[index] }
    export function routeStart(r: number): number { return [0,9,24,33,44][r] }
    export function routeEnd(r: number): number { return [9,24,33,44,52][r] }
    export function focusBeat(r: number, solved: number[], introduced: number[]): number {
        for (let i = routeStart(r); i < routeEnd(r); i++) {
            let entry = route[i]
            let b = entry < 0 ? -entry - 1 : entry - 1
            if (entry < 0 && !introduced[b] && !solved[b]) return b
            if (entry > 0 && !solved[b]) return b
        }
        return -1
    }
    export function available(station: number, solved: number[], introduced: number[], focus: number): boolean {
        if (station < 0 || station >= 30) return false
        if (station == stationForBeat(focus)) return true
        for (let b = firstBeats[station]; b <= lastBeats[station]; b++) if (solved[b] || introduced[b]) return true
        return false
    }
    export function roomComplete(r: number, solved: number[]): boolean {
        if (r == 0) return solved[5] == 1
        if (r == 1) return solved[6] == 1 && solved[12] == 1
        if (r == 2) return solved[16] == 1 && solved[21] == 1 && solved[17] == 1
        if (r == 3) return solved[25] == 1 && solved[29] == 1
        return solved[35] == 1
    }
    export function introTarget(b: number): number {
        if (b == 3) return 2
        if (b == 2) return 1
        if (b == 1) return 0
        if (b == 6) return 14
        if (b == 14) return 13
        if (b == 11) return 7
        if (b == 12) return 7
        if (b == 7) return 15
        if (b == 16) return 19
        if (b == 21) return 20
        if (b == 17) return 18
        if (b == 25) return 24
        if (b == 24) return 23
        if (b == 23) return 22
        if (b == 31) return 30
        if (b == 33) return 32
        return -1
    }
    export function introAction(b: number): number {
        if (b == 3) return EscapeAction.FireFlare
        if (b == 2) return EscapeAction.CaseRattle
        if (b == 1) return EscapeAction.GeneratorSputter
        if (b == 6) return EscapeAction.ShadowHide
        if (b == 14) return EscapeAction.TelescopeBlur
        if (b == 11) return EscapeAction.MuralDim
        if (b == 12) return EscapeAction.MuralSpill
        if (b == 7) return EscapeAction.PortraitRight
        if (b == 16) return EscapeAction.SampleFlat
        if (b == 21) return EscapeAction.VesselLeak
        if (b == 17) return EscapeAction.TitrationClear
        if (b == 25) return EscapeAction.TubeDrain
        if (b == 24) return EscapeAction.PrinterJam
        if (b == 23) return EscapeAction.NoiseDistort
        if (b == 31) return EscapeAction.ShutterClosed
        if (b == 33) return EscapeAction.RockCollapse
        return -1
    }
}

// Large, physical station props for the top-down escape world.  Each image has
// a transparent surround so it can sit directly on the room floor.
namespace escapeObjects {
    function oval(p: Image, cx: number, cy: number, rx: number, ry: number, c: number) {
        for (let row = -ry; row <= ry; row++) {
            let half = Math.floor(rx * Math.sqrt(Math.max(0, 1 - row * row / (ry * ry))))
            p.fillRect(cx - half, cy + row, half * 2 + 1, 1, c)
        }
    }
    function rounded(p: Image, x: number, y: number, w: number, h: number, c: number) {
        p.fillRect(x + 3, y, w - 6, h, c); p.fillRect(x, y + 3, w, h - 6, c)
        p.fillRect(x + 1, y + 1, w - 2, h - 2, c)
    }
    function shadow(p: Image, cx: number, y: number, rx: number = 45) { oval(p, cx, y, rx, 6, 12) }
    function bolt(p: Image, x: number, y: number) { p.fillCircle(x, y, 3, 6); p.fillCircle(x, y - 1, 2, 9); p.setPixel(x - 1, y - 2, 15) }
    function gear(p: Image, x: number, y: number, r: number, c: number, turn: number) {
        for (let i = 0; i < 8; i++) {
            let a = (i + turn) % 8
            if (a == 0) p.fillRect(x - 3, y - r - 4, 6, 9, c)
            else if (a == 1) p.fillRect(x + r - 2, y - r + 2, 7, 7, c)
            else if (a == 2) p.fillRect(x + r - 4, y - 3, 9, 6, c)
            else if (a == 3) p.fillRect(x + r - 4, y + r - 8, 7, 7, c)
            else if (a == 4) p.fillRect(x - 3, y + r - 4, 6, 9, c)
            else if (a == 5) p.fillRect(x - r - 4, y + r - 8, 7, 7, c)
            else if (a == 6) p.fillRect(x - r - 4, y - 3, 9, 6, c)
            else p.fillRect(x - r - 4, y - r + 2, 7, 7, c)
        }
        p.fillCircle(x, y, r, c); p.drawCircle(x, y, r - 4, 1); p.fillCircle(x, y, 5, 6); p.fillCircle(x, y, 2, 10)
    }
    function glass(p: Image, x: number, y: number, w: number, h: number) {
        p.fillRect(x, y, w, h, 12); p.drawRect(x, y, w, h, 9)
        p.fillRect(x + 3, y + 3, 3, h - 6, 15); p.fillRect(x + 7, y + 5, w - 13, 2, 11)
    }
    function good(station: number, response: number, done: boolean): boolean {
        if (response < 0) return done
        if (station == 0) return response == EscapeAction.CrankPull
        if (station == 1) return response == EscapeAction.GeneratorSpin
        if (station == 2) return response == EscapeAction.CaseRetract
        if (station == 3) return response == EscapeAction.FireSteam
        if (station == 4) return response == EscapeAction.WallClimb
        if (station == 5) return response == EscapeAction.FootprintKeep
        if (station == 6) return response == EscapeAction.ShadowReveal
        if (station == 7) return response == EscapeAction.PortraitLeft
        if (station == 8) return response == EscapeAction.MuralBlend || response == EscapeAction.MuralOpen
        if (station == 9) return response == EscapeAction.StoneSnap
        if (station == 10) return response == EscapeAction.TelescopeFocus
        if (station == 11) return response == EscapeAction.ThermalAmber
        if (station == 12) return response == EscapeAction.SampleSpike
        if (station == 13) return response == EscapeAction.TitrationBloom
        if (station == 14) return response == EscapeAction.ScaleLevel
        if (station == 15) return response == EscapeAction.WireInstall
        if (station == 16) return response == EscapeAction.LeafClip
        if (station == 17) return response == EscapeAction.VesselReveal
        if (station == 18) return response == EscapeAction.ReceiverClear
        if (station == 19) return response == EscapeAction.NoiseClear
        if (station == 20) return response == EscapeAction.PrinterFeed
        if (station == 21) return response == EscapeAction.TubeLaunch
        if (station == 22) return response == EscapeAction.SealStable || response == EscapeAction.SealRetract
        if (station == 23) return response == EscapeAction.PitchLevel
        if (station == 24) return response == EscapeAction.SensorLamp1 || response == EscapeAction.SensorLamp2 || response == EscapeAction.SensorLamp3
        if (station == 25) return response == EscapeAction.ShutterOpen
        if (station == 26) return response == EscapeAction.StarIgnite
        if (station == 27) return response == EscapeAction.RockBeam
        if (station == 28) return response == EscapeAction.SyncLock
        return response == EscapeAction.LeverPull
    }
    function pulse(response: number, frame: number): number { return response < 0 ? 0 : Math.max(0, Math.min(7, frame)) }

    export function prop(station: number, control: number, response: number, frame: number, done: boolean, part: number = 0, pitch: number = 0, portraitMask: number = 0): Image {
        let p = image.create(144, 112)
        // A completed machine stays visibly changed after its short animation.
        // A fresh learner response still takes precedence, including its else.
        if (response < 0 && done && station != 7) {
            const parked = [EscapeAction.CrankPull, EscapeAction.GeneratorSpin, EscapeAction.CaseRetract, EscapeAction.FireSteam, EscapeAction.WallClimb, EscapeAction.FootprintKeep, EscapeAction.ShadowReveal, EscapeAction.PortraitLeft, EscapeAction.MuralBlend, EscapeAction.StoneSnap, EscapeAction.TelescopeFocus, EscapeAction.ThermalAmber, EscapeAction.SampleSpike, EscapeAction.TitrationBloom, EscapeAction.ScaleLevel, EscapeAction.WireInstall, EscapeAction.LeafClip, EscapeAction.VesselReveal, EscapeAction.ReceiverClear, EscapeAction.NoiseClear, EscapeAction.PrinterFeed, EscapeAction.TubeLaunch, EscapeAction.SealStable, EscapeAction.PitchLevel, EscapeAction.SensorLamp1, EscapeAction.ShutterOpen, EscapeAction.StarIgnite, EscapeAction.RockBeam, EscapeAction.SyncLock, EscapeAction.LeverPull]
            response = parked[station]
            if (station == 8 && part == 1) response = EscapeAction.MuralOpen
            if (station == 22 && part == 1) response = EscapeAction.SealRetract
            if (station == 24) response = control == 1 ? EscapeAction.SensorLamp2 : control == 2 ? EscapeAction.SensorLamp3 : EscapeAction.SensorLamp1
            frame = 7
        }
        let ok = good(station, response, done), t = pulse(response, frame)
        if (station == 0) magnetCrank(p, control, response, t, ok)
        else if (station == 1) generator(p, control, response, t, ok)
        else if (station == 2) reservoir(p, control, response, t, ok)
        else if (station == 3) hearth(p, control, response, t, ok)
        else if (station == 4) climbingWall(p, control, response, t, ok)
        else if (station == 5) footprintPath(p, control, response, t, ok)
        else if (station == 6) shadowLantern(p, control, response, t, ok)
        else if (station == 7) portraits(p, control, response, t, ok, part, portraitMask)
        else if (station == 8) mural(p, control, response, t, ok)
        else if (station == 9) sockets(p, control, response, t, ok)
        else if (station == 10) telescope(p, control, response, t, ok)
        else if (station == 11) thermalBath(p, control, response, t, ok)
        else if (station == 12) filings(p, control, response, t, ok)
        else if (station == 13) titration(p, control, response, t, ok)
        else if (station == 14) balance(p, control, response, t, ok)
        else if (station == 15) wires(p, control, response, t, ok)
        else if (station == 16) plant(p, control, response, t, ok)
        else if (station == 17) heatVessel(p, control, response, t, ok)
        else if (station == 18) pedalRadio(p, control, response, t, ok)
        else if (station == 19) horns(p, control, response, t, ok)
        else if (station == 20) printer(p, control, response, t, ok)
        else if (station == 21) tubes(p, control, response, t, ok)
        else if (station == 22) pressure(p, control, response, t, ok)
        else if (station == 23) plank(p, control, response, t, ok, pitch)
        else if (station == 24) sensors(p, control, response, t, ok)
        else if (station == 25) shutters(p, control, response, t, ok)
        else if (station == 26) constellation(p, control, response, t, ok)
        else if (station == 27) rockPath(p, control, response, t, ok)
        else if (station == 28) interlocks(p, control, response, t, ok)
        else exitDoor(p, control, response, t, ok)
        return p
    }

    // 0. A real hanging magnet can pull the iron slider across its floor rail.
    function magnetCrank(p: Image, control: number, response: number, t: number, ok: boolean) {
        shadow(p, 70, 99, 57); p.fillRect(18, 83, 100, 8, 14); p.fillRect(20, 85, 96, 3, 6); p.fillRect(19, 91, 98, 4, 1)
        for (let x = 27; x < 112; x += 17) bolt(p, x, 87)
        let slide = response < 0 ? 0 : ok ? t * 4 : (t % 2) * 3
        rounded(p, 31 + slide, 75, 28, 13, 1); p.fillRect(34 + slide, 77, 22, 7, 6); p.fillRect(38 + slide, 78, 12, 2, 9); p.fillRect(34 + slide, 84, 20, 2, 14)
        p.fillRect(65, 7, 30, 5, 14); p.fillRect(68, 11, 4, 38, 6); p.fillRect(90, 11, 4, 38, 6); p.fillRect(66, 8, 27, 2, 15)
        let mx = control == 1 ? 47 : 80
        let my = control == 1 ? 9 : 0
        if (response >= 0) mx += ok ? t * 4 : (t % 2) * 3
        p.drawLine(80, 12, mx, 55 + my, 6); p.drawLine(81, 12, mx + 1, 55 + my, 9)
        rounded(p, mx - 15, 48 + my, 10, 19, 3); rounded(p, mx + 5, 48 + my, 10, 19, 3)
        p.fillRect(mx - 12, 49 + my, 7, 4, 4); p.fillRect(mx + 5, 49 + my, 7, 4, 4); p.fillRect(mx - 5, 60 + my, 10, 7, 15); p.fillRect(mx - 3, 63 + my, 6, 2, 9)
        p.fillRect(115, 63, 5, 25, 14); p.fillCircle(117, 60, 8, 5); p.fillCircle(117, 60, 4, 1); p.fillRect(113, 61, 8, 2, 15)
        let a = control % 2 == 0 ? -1 : 1; let turn = response >= 0 ? t - 4 : 0; p.drawLine(117, 60, 117 + a * 16, 60 + turn, 4); p.drawLine(117, 60, 117 + a * 16, 60 + turn + 2, 15); p.fillCircle(117 + a * 17, 60 + turn, 4, 3)
    }

    // 1. Copper generator: flywheel, belt, cable, and a deliberately separate socket.
    function generator(p: Image, control: number, response: number, t: number, ok: boolean) {
        shadow(p, 69, 101, 56); rounded(p, 19, 55, 70, 38, 1); rounded(p, 21, 53, 66, 37, 14); rounded(p, 25, 57, 58, 29, 2)
        p.fillRect(29, 63, 25, 18, 12); p.fillRect(32, 65, 19, 3, 15); p.fillRect(57, 61, 19, 21, 6); p.fillRect(60, 64, 14, 4, 14); bolt(p, 28, 85); bolt(p, 80, 85)
        gear(p, 55, 48, 25, 5, response >= 0 ? t : 0); p.fillCircle(55, 48, 19, 14); p.fillCircle(55, 48, 16, ok ? 10 : 4); p.drawCircle(55, 48, 12, 15); p.fillCircle(55, 48, 7, 6); p.fillCircle(55, 48, 3, 15)
        p.drawLine(77, 33, 106, 27 + (response >= 0 ? t : 0), 1); p.drawLine(77, 60, 106, 48 - (response >= 0 ? t : 0), 1)
        p.fillRect(100, 20, 25, 36, 1); p.fillRect(102, 22, 21, 32, 14); p.fillRect(105, 25, 15, 26, 12); p.fillCircle(112, 37, 8, 1); p.fillCircle(112, 37, 5, ok ? 10 : 3)
        if (control == 1) { p.drawLine(112, 37, 129, 37, 5); p.drawLine(129, 37, 129, 53, 5); p.fillCircle(129, 53, 4, 4) }
        p.fillRect(127, 44, 8, 31, 6); p.fillRect(125, 72, 12, 6, 14); p.fillCircle(131, 77, 3, 9)
        p.drawLine(26, 60, 15, 43, 4); p.fillCircle(14, 41, 5, 5); p.fillCircle(14, 41, 2, 15)
    }

    // 2. A glass case protecting a raised water reservoir, pipes, and mounting valve.
    function reservoir(p: Image, control: number, response: number, t: number, ok: boolean) {
        shadow(p, 72, 101, 53); p.fillRect(14, 84, 116, 10, 1); p.fillRect(18, 82, 108, 8, 14); p.fillRect(22, 85, 100, 3, 6)
        p.fillRect(38, 31, 54, 38, 1); oval(p, 65, 31, 27, 9, 14); oval(p, 65, 32, 23, 6, 12); p.fillRect(41, 34, 48, 30, 12); oval(p, 65, 62, 24, 6, 11); p.fillRect(45, 39, 40, 20, 11)
        p.fillRect(45, 37, 6, 24, 15); p.fillRect(55, 39, 26, 3, 9); p.fillRect(84, 35, 4, 28, 8); p.fillRect(54, 65, 20, 2, 9)
        p.drawLine(65, 69, 65, 79, 14); p.drawLine(65, 79, 104, 79, 14); p.drawLine(66, 81, 104, 81, 6); p.fillCircle(106, 80, 8, 5); p.fillCircle(106, 80, 4, 1); p.drawLine(106, 80, 111, 75 + (response >= 0 && ok ? t : 0), ok ? 10 : 3)
        let open = response >= 0 && ok ? t * 4 : 0; let gx = 18 + open
        // The cover is outline-and-glint glass so its copper tank remains visible.
        p.drawRect(gx, 14, 101, 67, 9); p.fillRect(gx + 3, 17, 2, 59, 15); p.fillRect(gx + 7, 18, 63, 2, 11); p.fillRect(gx + 96, 20, 2, 54, 14); p.fillRect(gx + 7, 77, 89, 2, 9)
        if (response >= 0 && !ok) { p.drawLine(25, 15, 20, 22 + t, 3); p.drawLine(112, 18, 119, 25 + t, 3) }
    }

    // 3. Hearth uses stacked stone, a live flame/steam reaction, and a fixed brass spout.
    function hearth(p: Image, control: number, response: number, t: number, ok: boolean) {
        shadow(p, 69, 101, 55); p.fillRect(14, 70, 95, 24, 1)
        for (let y = 72; y < 93; y += 7) for (let x = 19 + ((y / 7) % 2) * 7; x < 105; x += 18) { p.fillRect(x, y, 16, 6, 6); p.fillRect(x + 1, y + 1, 12, 2, 14) }
        p.fillRect(27, 38, 67, 34, 14); oval(p, 60, 38, 34, 10, 14); oval(p, 60, 39, 29, 7, 1); p.fillRect(33, 43, 55, 27, 1)
        p.drawLine(36, 66, 79, 48, 14); p.drawLine(41, 48, 83, 66, 5); p.drawLine(39, 64, 80, 46, 4)
        let flare = response >= 0 && !ok ? 10 + t * 2 : 0; let flame = response < 0 ? 23 : ok ? 6 : 29 + flare
        for (let i = 0; i < 3; i++) { let x = 43 + i * 12; let top = 66 - flame + (i % 2) * 7; p.fillCircle(x, 61 - flame / 3, 10, ok ? 11 : 3); p.fillRect(x - 7, top + 9, 14, 60 - top, ok ? 11 : 3); p.drawLine(x - 7, top + 12, x, top, ok ? 11 : 3); p.drawLine(x + 7, top + 12, x, top, ok ? 11 : 3); p.fillCircle(x, 61 - flame / 4, 6, ok ? 9 : 4); p.fillRect(x - 3, top + 15, 7, 48 - top, ok ? 9 : 10); p.drawLine(x - 3, top + 17, x, top + 8, ok ? 9 : 10); p.drawLine(x + 3, top + 17, x, top + 8, ok ? 9 : 10) }
        p.fillRect(94, 27, 10, 46, 5); p.fillRect(102, 28, 23, 9, 14); p.fillRect(122, 31, 12, 4, 10); p.fillCircle(128, 34, 4, 15)
        if (response >= 0 && ok) for (let i = 0; i < 4; i++) { p.fillCircle(45 + i * 15, 35 - ((t + i * 2) % 8), 4, 11); p.setPixel(46 + i * 15, 31 - ((t + i * 2) % 8), 9) }
    }

    // 4. Four stone holds grow from a tall climbing wall rather than an abstract control.
    function climbingWall(p: Image, control: number, response: number, t: number, ok: boolean) {
        shadow(p, 72, 102, 54); p.fillRect(25, 12, 84, 82, 1); p.fillRect(29, 15, 76, 76, 2)
        for (let y = 20; y < 86; y += 17) p.drawLine(31, y, 103, y + (y % 3), 6)
        let holdCount = control == 0 ? 3 : 4
        for (let i = 0; i < holdCount; i++) { let x = i % 2 == 0 ? 43 : 84; let y = 72 - Math.idiv(i, 2) * 26; let lit = i == control % 4; rounded(p, x - 11, y - 5, 23, 12, lit ? 10 : 6); p.fillRect(x - 7, y - 3, 13, 3, lit ? 15 : 5); p.setPixel(x + 7, y + 2, 1) }
        if (response >= 0 && ok) { p.drawLine(38, 87, 84, 25 + t, 10); p.fillCircle(87, 22 + t, 7, 7); p.fillRect(82, 28 + t, 10, 15, 7) }
        else if (response >= 0) { p.fillRect(49, 31 + (t % 2) * 4, 38, 10, 3); p.fillRect(53, 34 + (t % 2) * 4, 30, 2, 15) }
        p.fillRect(20, 91, 94, 5, 14)
    }

    // 5. Numbered footprint stones make a physical route over a deep gap.
    function footprintPath(p: Image, control: number, response: number, t: number, ok: boolean) {
        shadow(p, 72, 102, 61); p.fillRect(8, 27, 128, 65, 12)
        for (let x = 11; x < 136; x += 13) p.drawLine(x, 30, x - 8, 89, 14)
        let values = [8, 7, 6, 7, 6]
        for (let i = 0; i < 5; i++) { let x = 18 + i * 24; let y = 74 - (i % 2) * 21; if (response >= 0 && !ok && i == control % 3) y += t * 5; rounded(p, x, y, 21, 15, i == control % 3 ? 10 : 6); p.fillRect(x + 3, y + 3, 15, 3, 14); p.print("" + values[i], x + 8, y + 6, 1, image.font5); p.fillRect(x + 6, y - 5, 5, 5, 15); p.fillRect(x + 12, y + 1, 3, 6, 15) }
        p.fillRect(5, 90, 134, 7, 14); p.fillRect(7, 92, 130, 2, 5)
        if (response >= 0 && ok) for (let i = 0; i < 4; i++) p.drawLine(38 + i * 24, 75 - (i % 2) * 21, 44 + i * 24, 75 - ((i + 1) % 2) * 21, 7)
    }

    function shadowLantern(p: Image, control: number, response: number, t: number, ok: boolean) {
        shadow(p, 73, 101, 55); rounded(p, 39, 15, 51, 79, 1); rounded(p, 42, 18, 45, 73, 2)
        p.fillRect(48, 24, 33, 56, 9); p.fillRect(51, 27, 4, 50, 15)
        p.fillRect(14, 56, 14, 32, 14); p.fillCircle(21, 52, 11, 5); p.fillCircle(21, 52, 7, response >= 0 && ok ? 10 : 4); p.fillRect(15, 67, 12, 18, 4)
        p.drawLine(28, 55, 43, 49, response >= 0 && ok ? 10 : 6); p.drawLine(28, 62, 43, 58, response >= 0 && ok ? 10 : 6)
        if (response >= 0 && ok) { p.fillCircle(65, 42, 10, 1); p.fillRect(58, 49, 14, 23, 1); p.fillRect(54, 72, 8, 8, 1); p.fillRect(69, 72, 8, 8, 1) }
        else if (response >= 0) { p.fillRect(48, 25 + (t % 2) * 3, 33, 55, 1); p.fillCircle(21, 52, 7, 3) }
        p.fillRect(94, 35, 30, 7, 14); p.fillRect(101, 42, 5, 47, 14); p.fillCircle(103, 32, 6, control % 2 == 0 ? 11 : 3)
    }

    function portraits(p: Image, control: number, response: number, t: number, ok: boolean, part: number, portraitMask: number) {
        shadow(p, 71, 101, 58); p.fillRect(9, 18, 126, 72, 2); p.fillRect(11, 20, 122, 3, 14)
        for (let i = 0; i < 4; i++) { let parked = (portraitMask & (1 << i)) != 0; let shift = parked ? -5 : 0; if (response >= 0 && i == part) shift += ok ? -Math.min(5, t) : (t % 2) * 3; let x = 15 + i * 30 + shift
            p.fillRect(x, 29, 24, 47, 5); p.fillRect(x + 3, 32, 18, 41, i == part ? 10 : 14); p.fillCircle(x + 12, 44, 7, 15); p.fillRect(x + 7, 51, 10, 15, i % 2 == 0 ? 13 : 8); p.fillRect(x + 5, 66, 15, 4, 1); p.fillRect(x + 8, 39, 3, 2, 1); p.fillRect(x + 14, 39, 3, 2, 1) }
        p.fillRect(control == 1 ? 37 : 93, 85, 15, 7, control == 1 ? 10 : 3)
        p.fillRect(12, 78, 120, 5, 14); p.drawLine(17, 83, 27, 93, 6); p.drawLine(127, 83, 117, 93, 6)
    }

    function mural(p: Image, control: number, response: number, t: number, ok: boolean) {
        shadow(p, 72, 101, 54); p.fillRect(20, 15, 104, 75, 1); p.fillRect(24, 19, 96, 67, 5); p.fillRect(28, 23, 88, 59, 13)
        for (let x = 30; x < 115; x += 11) p.drawLine(x, 25, 110 - x / 3, 79, x % 3 == 0 ? 8 : 7)
        p.fillCircle(50, 45, 16, response >= 0 && ok ? 10 : 3); p.fillCircle(93, 48, 19, response >= 0 && ok ? 7 : 11); p.fillCircle(72, 59, 14, response >= 0 && ok ? 11 : 13)
        p.fillCircle(50, 45, 9, 4); p.fillCircle(93, 48, 12, 8); p.fillCircle(72, 59, 7, 15)
        if (response >= 0 && ok) { p.fillRect(63, 49 - t * 2, 18, 21, 10); p.fillRect(67, 53 - t * 2, 10, 13, 1) }
        else if (response >= 0) for (let i = 0; i < 8; i++) p.fillCircle(31 + (i * 17 + t * 3) % 80, 28 + (i * 11) % 48, 2, i % 2 == 0 ? 3 : 11)
        let yellow = control == 1 || control == 3 || control == 4
        let blue = control == 2 || control == 3 || control == 4
        let red = control == 4 || control == 5
        p.fillRect(33, 87, 80, 9, 14)
        p.fillCircle(46, 91, 4, yellow ? 5 : 6)
        p.fillCircle(73, 91, 4, blue ? 8 : 6)
        p.fillCircle(100, 91, 4, red ? 3 : 6)
    }

    function sockets(p: Image, control: number, response: number, t: number, ok: boolean) {
        shadow(p, 70, 101, 55); rounded(p, 19, 22, 103, 65, 1); rounded(p, 22, 25, 97, 59, 14)
        let socketColor = [8, 8, 5][control % 3]
        let stoneColor = [3, 8, 5][control % 3]
        for (let i = 0; i < 3; i++) { let x = 39 + i * 32; p.fillCircle(x, 50, 12, 1); p.fillCircle(x, 50, 8, [8,8,5][i]); p.fillCircle(x, 50, 3, 12); if (i == control % 3) p.drawCircle(x, 50, 13, 10) }
        let sx = 39 + control % 3 * 32 + (response >= 0 && !ok ? t * 3 : 0)
        p.fillCircle(sx, 72 - (response >= 0 && ok ? t : 0), 10, stoneColor); p.fillRect(sx - 5, 62 - (response >= 0 && ok ? t : 0), 10, 4, 15)
        p.fillRect(96, 72, 20, 8, socketColor)
        p.fillRect(14, 89, 116, 5, 6)
    }

    function telescope(p: Image, control: number, response: number, t: number, ok: boolean) {
        shadow(p, 71, 101, 54); p.fillRect(22, 17, 40, 22, 14); p.fillRect(25, 20, 34, 16, 8); p.fillCircle(27, 28, 10, 1); p.fillCircle(27, 28, 6, 11)
        p.drawLine(57, 20, 99, 43, 5); p.drawLine(54, 38, 96, 61, 14); p.fillRect(59, 24, 47, 20, 14); p.fillRect(63, 27, 39, 14, 12); p.fillCircle(105, 34, 12, 1); p.fillCircle(105, 34, ok && response >= 0 ? 8 : 13, ok ? 10 : 6)
        p.fillRect(77, 43, 5, 36, 6); p.drawLine(80, 76, 53, 94, 6); p.drawLine(80, 76, 102, 94, 6); p.drawLine(80, 76, 80 + (control % 3 - 1) * 12, 97, 6)
        if (response >= 0) for (let i = 0; i < 5; i++) p.fillCircle(117 + ((i * 7 + t) % 15), 20 + i * 11, 1, ok ? 10 : 13)
    }

    function thermalBath(p: Image, control: number, response: number, t: number, ok: boolean) {
        shadow(p, 71, 101, 57); rounded(p, 18, 34, 108, 55, 14); p.fillRect(23, 39, 98, 43, 1)
        let degrees = [19, 20, 40, 41][control % 4]
        let selected = control == 0 ? 0 : control == 3 ? 2 : 1
        let waterColor = response == EscapeAction.ThermalBlue ? 8 : response == EscapeAction.ThermalRed ? 3 : response == EscapeAction.ThermalAmber ? 10 : degrees < 20 ? 8 : degrees > 40 ? 3 : 10
        for (let i = 0; i < 3; i++) { let x = 29 + i * 31; p.fillRect(x, 45, 25, 29, 6); p.fillRect(x + 3, 48, 19, 22, i == selected ? waterColor : 8); p.fillRect(x + 5, 52, 15, 3, 15); p.fillCircle(x + 12, 76, 4, i == selected ? waterColor : 6) }
        p.print("" + degrees, 53, 58, 1, image.font5)
        p.fillRect(21, 83, 102, 8, 14); p.fillRect(28, 28, 88, 7, 6); p.fillRect(37, 25, 70, 3, 15)
        if (response == EscapeAction.ThermalAmber) { p.fillRect(29 + selected * 31, 42 - t * 2, 25, 6, 10); p.fillCircle(41 + selected * 31, 31 - t, 3, 11) }
    }

    function filings(p: Image, control: number, response: number, t: number, ok: boolean) {
        shadow(p, 71, 100, 55); glass(p, 25, 42, 88, 43); p.fillRect(30, 70, 78, 10, 1)
        for (let i = 0; i < 11; i++) { let x = 34 + i * 7; let h = response >= 0 && ok ? 12 + ((i + t) % 3) * 7 : 2 + (i % 2) * 2; p.drawLine(x, 70, x + (i % 2 == 0 ? -3 : 3), 70 - h, 6); if (response >= 0 && ok) p.setPixel(x + 1, 69 - h, 10) }
        rounded(p, 49, 13, 45, 22, 3); p.fillRect(55, 16, 33, 15, 4); p.fillRect(59, 18, 25, 3, 15); p.drawLine(71, 35, 71, 43, 5)
        let magnetOn = control == 0 || control == 2
        p.fillRect(22 + (magnetOn ? 0 : 92), 50, 6, 23, 14); p.fillCircle(25 + (magnetOn ? 0 : 92), 47, 6, magnetOn ? 10 : 6)
        p.print(control == 1 || control == 2 ? "IRON" : "WOOD", 48, 80, 15, image.font5)
    }

    function titration(p: Image, control: number, response: number, t: number, ok: boolean) {
        shadow(p, 72, 101, 56); p.fillRect(20, 16, 5, 72, 14); p.fillRect(16, 16, 13, 5, 6); p.fillRect(22, 23, 68, 4, 6)
        p.fillRect(74, 25, 8, 33, 15); p.fillRect(77, 29, 3, 23, 3); p.fillRect(69, 54, 18, 7, 14); p.fillCircle(78, 63 + (response >= 0 ? t : 0), 3, response == EscapeAction.TitrationOverflow ? 3 : 10); p.print("" + [6, 7, 9, 10][control % 4], 87, 55, 10, image.font5)
        let liquid = response == EscapeAction.TitrationClear ? 8 : response == EscapeAction.TitrationBloom ? 10 : response == EscapeAction.TitrationOverflow ? 3 : 8
        p.drawLine(46, 32, 46, 72, 9); p.drawLine(46, 32, 66, 32, 9); glass(p, 39, 59, 49, 29); p.fillRect(43, 76, 41, 8, liquid); p.drawLine(55, 61, 55, 86, 15); p.drawLine(63, 61, 63, 86, 15)
        if (response == EscapeAction.TitrationOverflow) for (let i = 0; i < 3; i++) p.fillCircle(88 + i * 5, 77 + t + i * 3, 3, 3)
        p.fillRect(96, 41, 20, 40, 14); p.fillRect(100, 45, 12, 28, 2); p.fillRect(102, 50 + control % 3 * 7, 8, 2, 10)
    }

    function balance(p: Image, control: number, response: number, t: number, ok: boolean) {
        let weight = [7, 5, 3, 5][control % 4]
        shadow(p, 72, 101, 55); let tilt = response == EscapeAction.ScaleLeft ? 7 : response == EscapeAction.ScaleRight ? -7 : response == EscapeAction.ScaleLevel ? 0 : weight > 5 ? 7 : weight < 5 ? -7 : 0
        p.drawLine(25, 52 + tilt, 119, 52 - tilt, 5); p.drawLine(25, 55 + tilt, 119, 55 - tilt, 14); p.fillRect(69, 53, 7, 34, 14); p.fillCircle(72, 51, 7, 10); p.fillRect(54, 87, 36, 6, 14)
        p.drawLine(30, 55 + tilt, 37, 75 + tilt, 6); p.drawLine(113, 55 - tilt, 106, 75 - tilt, 6); oval(p, 37, 78 + tilt, 19, 5, 5); oval(p, 106, 78 - tilt, 19, 5, 5)
        for (let i = 0; i < 3; i++) { let left = i <= control % 3; p.fillRect((left ? 31 : 100) + i * 3, (left ? 66 + tilt : 66 - tilt) - i * 5, 9, 8, i == control % 3 ? 10 : 6) }; p.print("" + weight, 32, 74 + tilt, 1, image.font5); p.print("5", 102, 74 - tilt, 1, image.font5)
        p.fillRect(19, 92, 107, 4, 1)
    }

    function wires(p: Image, control: number, response: number, t: number, ok: boolean) {
        shadow(p, 72, 101, 58); rounded(p, 18, 20, 108, 70, 14); p.fillRect(25, 28, 94, 54, 1)
        for (let i = 0; i < 4; i++) { let y = 36 + i * 11; let c = i == 0 ? 3 : i == 1 ? 11 : i == 2 ? 10 : 13; let end = response >= 0 && !ok && i == control % 4 ? 51 + t * 5 : 106; p.fillCircle(32, y, 5, c); p.drawLine(36, y, end, y + (i % 2 == 0 ? 4 : -4), c); p.fillCircle(end + 3, y + (i % 2 == 0 ? 4 : -4), 4, c) }
        p.fillRect(105, 32, 10, 45, 6); p.fillRect(108, 36, 4, 35, 15); p.fillCircle(110, 75, 6, response >= 0 && ok ? 10 : 3)
    }

    function plant(p: Image, control: number, response: number, t: number, ok: boolean) {
        shadow(p, 71, 101, 51); oval(p, 70, 88, 28, 9, 14); p.fillRect(46, 71, 48, 17, 2); oval(p, 70, 70, 24, 7, 6); p.drawLine(70, 71, 70, 24, 7)
        for (let i = 0; i < 7; i++) { let y = 31 + i * 6; let side = i % 2 == 0 ? -1 : 1; let x = 70 + side * (12 + (i % 3) * 5); let clipped = response >= 0 && ok && i == control % 7; p.drawLine(70, y + 5, x, y, 7); if (!clipped || response < 0) { oval(p, x + (clipped ? t * side * 3 : 0), y - (clipped ? t * 2 : 0), 11, 6, i % 3 == 0 ? 7 : 8); p.fillRect(x - 5, y - 2, 6, 2, 9) } }
        p.drawLine(108, 20, 96, 44, 15); p.drawLine(112, 21, 99, 45, 15); p.fillCircle(109, 18, 7, 3); p.fillCircle(99, 43, 7, 3); p.fillRect(103, 28, 4, 11, 5)
        p.fillRect(105, 78, 21, 6, 14); p.fillCircle(110 + control % 2 * 9, 75, 4, 10)
        p.fillRect(12, 20, 25, 15, 14); p.print(control == 0 ? "3 PT" : "4 PT", 14, 23, 1, image.font5)
    }

    function heatVessel(p: Image, control: number, response: number, t: number, ok: boolean) {
        shadow(p, 71, 102, 54); oval(p, 72, 78, 37, 16, 14); p.fillRect(35, 48, 74, 30, 14); oval(p, 72, 48, 37, 15, 5); oval(p, 72, 50, 30, 10, 1); p.fillRect(45, 53, 54, 21, 4)
        p.fillRect(58, 24, 28, 19, 14); oval(p, 72, 24, 14, 5, 6); p.fillRect(68, 15, 8, 10, 6); p.fillCircle(72, 13, 5, 10)
        p.fillRect(40, 58, 5, 13, 15); p.fillRect(99, 57, 5, 14, 15); p.fillRect(105, 61, 14, 7, 14)
        if (response == EscapeAction.VesselLeak) for (let i = 0; i < 4; i++) p.fillCircle(113 + t * 2, 67 + i * 6, 3, 11)
        if (response == EscapeAction.VesselBlank) { p.fillCircle(72, 61, 10, 6); p.fillRect(104, 55, 11, 11, 14) }
        if (response == EscapeAction.VesselReveal || response < 0 && ok) { p.fillCircle(72, 61, 10, 10); p.fillCircle(72, 61, 5, 4); for (let i = 0; i < 3; i++) p.fillCircle(59 + i * 10, 37 - ((t + i * 2) % 6), 3, 11) }
        p.fillRect(20, 89, 104, 6, 1); p.fillCircle(28 + control % 3 * 12, 87, 4, 3)
    }

    function pedalRadio(p: Image, control: number, response: number, t: number, ok: boolean) {
        shadow(p, 71, 101, 58); p.drawLine(31, 25, 31, 83, 6); p.drawLine(31, 50, 66, 70, 6); p.drawLine(31, 52, 53, 89, 6); p.fillCircle(31, 48, 20, 14); p.drawCircle(31, 48, 15, 5)
        for (let i = 0; i < 6; i++) p.drawLine(31, 48, 31 + Math.floor(15 * Math.cos((i + t) * Math.PI / 3)), 48 + Math.floor(15 * Math.sin((i + t) * Math.PI / 3)), 6)
        p.fillCircle(31, 48, 5, 10); p.drawLine(12, 77, 50, 77, 14); p.fillCircle(15, 77, 7, 6); p.fillCircle(47, 77, 7, 6)
        rounded(p, 71, 27, 52, 51, 14); p.fillRect(76, 33, 42, 26, 1); for (let i = 0; i < 7; i++) { let h = response == EscapeAction.ReceiverDead ? 1 : response == EscapeAction.ReceiverStatic ? 4 + (i % 2) * 5 : response == EscapeAction.ReceiverClear || response < 0 && ok ? 6 + ((i + t) % 4) * 4 : 2; p.fillRect(80 + i * 5, 55 - h, 3, h, response == EscapeAction.ReceiverClear || response < 0 && ok ? 7 : response == EscapeAction.ReceiverStatic ? 3 : 6) }
        p.fillCircle(112, 66, 7, control % 2 == 0 ? 10 : 3); p.drawLine(78, 28, 68, 12, 9); p.fillCircle(67, 10, 3, 10)
    }

    function horns(p: Image, control: number, response: number, t: number, ok: boolean) {
        shadow(p, 71, 100, 56); rounded(p, 30, 57, 82, 30, 14); p.fillRect(36, 63, 70, 18, 2)
        for (let i = 0; i < 3; i++) { let x = 33 + i * 36; let active = i == control % 3; p.drawLine(x + 13, 59, x + 18, 37, 5); p.fillRect(x + 9, 31, 18, 9, active && response >= 0 && ok ? 10 : 6); p.fillRect(x + 5, 27, 26, 17, active && response >= 0 && ok ? 10 : 14); p.fillRect(x + 8, 30, 20, 11, 1); p.fillCircle(x + 18, 35, 5, active && response >= 0 && ok ? 10 : 3) }
        if (response >= 0) for (let i = 0; i < 4; i++) p.drawLine(22 + control % 3 * 36, 29, 12 + control % 3 * 36 - i * 3, 25 - ((i + t) % 3) * 4, ok ? 11 : 3)
        p.fillRect(42, 83, 10, 7, 3); p.fillRect(67, 83, 10, 7, 11); p.fillRect(92, 83, 10, 7, 10)
    }

    function printer(p: Image, control: number, response: number, t: number, ok: boolean) {
        shadow(p, 71, 101, 56); rounded(p, 27, 42, 83, 45, 14); p.fillRect(32, 47, 73, 35, 2); p.fillRect(39, 53, 45, 16, 1); p.fillRect(42, 56, 39, 3, 9)
        p.fillCircle(93, 57, 7, 6); p.fillCircle(93, 57, 3, control % 2 == 0 ? 10 : 3); p.fillRect(35, 69, 66, 7, 6)
        let paper = response < 0 ? 0 : ok ? 10 + t * 5 : 8; p.fillRect(53, 77, 29, paper, 15); p.drawLine(56, 82, 78, 82, 1); p.drawLine(56, 87, 75, 87, 1); if (response >= 0 && !ok) p.drawLine(53, 80, 80, 92, 3)
        p.fillRect(18, 20, 18, 22, 14); p.fillRect(21, 23, 12, 14, 10); p.drawLine(36, 31, 52, 43, 6); p.fillRect(23, 87, 91, 6, 1)
    }

    function tubes(p: Image, control: number, response: number, t: number, ok: boolean) {
        shadow(p, 71, 101, 57); p.drawLine(31, 20, 31, 67, 9); p.drawLine(31, 20, 99, 20, 9); p.drawLine(31, 67, 99, 67, 9); p.drawLine(99, 20, 113, 38, 9); p.drawLine(99, 67, 113, 49, 9); p.drawLine(112, 38, 112, 84, 9)
        p.drawLine(34, 20, 34, 67, 15); p.drawLine(34, 23, 96, 23, 15); p.drawLine(34, 64, 96, 64, 15); p.drawLine(102, 22, 109, 38, 15); p.drawLine(102, 65, 109, 49, 15)
        let cx = response < 0 ? 26 : ok ? 32 + t * 11 : 32; let cy = response >= 0 && !ok ? 67 + t * 3 : control % 2 == 0 ? 20 : 67; rounded(p, cx, cy - 6, 15, 12, control % 3 == 0 ? 10 : control % 3 == 1 ? 3 : 11); p.fillRect(cx + 3, cy - 3, 8, 3, 15)
        p.fillRect(17, 84, 107, 7, 14); bolt(p, 31, 88); bolt(p, 112, 88)
    }

    function pressure(p: Image, control: number, response: number, t: number, ok: boolean) {
        shadow(p, 72, 101, 56); rounded(p, 19, 25, 67, 62, 14); p.fillRect(24, 30, 57, 52, 2); p.fillCircle(52, 52, 21, 15); p.fillCircle(52, 52, 18, 1); p.drawLine(52, 52, 52 + (ok ? 10 : -9 + t), 39, ok ? 10 : 3); p.fillCircle(52, 52, 3, 6)
        for (let i = 0; i < 5; i++) p.fillRect(36 + i * 8, 34, 2, 5, 9); p.fillRect(39, 73, 25, 4, 6)
        p.fillRect(96, 25, 14, 61, 14); p.fillRect(100, 30, 6, 50, 12); p.fillRect(92, 40 + control % 3 * 13, 22, 8, 5); p.fillRect(95, 42 + control % 3 * 13, 16, 3, ok ? 7 : 3)
        if (response >= 0 && !ok) for (let i = 0; i < 4; i++) p.fillCircle(116 + t * 2, 47 + i * 7, 3, 11); else if (response >= 0 && ok) p.fillRect(115, 43, 14, 31, 10)
        p.drawLine(64, 83, 124, 83, 6)
    }

    function plank(p: Image, control: number, response: number, t: number, ok: boolean, pitch: number) {
        shadow(p, 72, 101, 60); let tilt = Math.max(-12, Math.min(12, Math.idiv(pitch, 2))); if (response == EscapeAction.PitchLevel) tilt = 0; p.drawLine(17, 68 + tilt, 127, 68 - tilt, 5); p.drawLine(17, 72 + tilt, 127, 72 - tilt, 14)
        for (let x = 27; x < 118; x += 21) p.drawLine(x, 69 + tilt - 2, x + 12, 69 + tilt - 2, 15)
        p.fillRect(69, 72, 7, 20, 6); p.fillCircle(72, 70, 7, 10); p.drawLine(72, 22, 72, 68, 9); p.fillCircle(72, 20, 5, 14)
        let bx = response >= 0 && ok ? 71 : 36 + t * 6; p.fillCircle(bx, 59 + tilt, 8, 10); p.fillCircle(bx - 2, 56 + tilt, 2, 15); p.fillRect(16, 91, 112, 5, 1)
    }

    function sensors(p: Image, control: number, response: number, t: number, ok: boolean) {
        shadow(p, 72, 101, 58); p.fillRect(21, 28, 8, 57, 14); p.fillRect(24, 32, 3, 48, 9); p.drawLine(29, 39, 111, 39, 8); p.drawLine(29, 58, 111, 58, 8); p.drawLine(29, 77, 111, 77, 8)
        for (let i = 0; i < 3; i++) { let y = 39 + i * 19; p.fillRect(105, y - 9, 18, 18, 14); p.fillRect(108, y - 6, 12, 12, 1); let selected = control < 3 && i == control; let lit = response >= EscapeAction.SensorLamp1 && response <= EscapeAction.SensorLamp3 && i == response - EscapeAction.SensorLamp1; p.fillCircle(114, y, 5, lit || response < 0 && ok && selected ? 10 : selected && response >= 0 ? 3 : 6); p.print("" + (i + 1), 110, y - 3, 15, image.font5); if (lit) p.drawLine(45 + t * 2, y, 104, y, 11) }
        p.fillRect(17, 86, 110, 6, 1)
    }

    function shutters(p: Image, control: number, response: number, t: number, ok: boolean) {
        shadow(p, 72, 101, 59); p.fillRect(15, 18, 114, 74, 1)
        for (let i = 0; i < 3; i++) { let x = 22 + i * 35; let lift = response >= 0 && ok && i == control % 3 ? t * 5 : 0; p.fillRect(x, 25, 28, 57, 14); p.fillRect(x + 3, 28 - lift, 22, 50, 8); for (let y = 31 - lift; y < 75 - lift; y += 8) p.fillRect(x + 4, y, 20, 3, response >= 0 && !ok && i == control % 3 ? 3 : 6); p.fillRect(x + 10, 79, 8, 4, 5) }
        if (response >= 0 && ok) for (let i = 0; i < 5; i++) p.drawLine(21 + i * 23, 68, 31 + i * 23, 53 - (t % 3) * 3, 11)
        p.fillRect(13, 92, 118, 5, 14)
    }

    function constellation(p: Image, control: number, response: number, t: number, ok: boolean) {
        shadow(p, 72, 101, 54); p.fillRect(18, 19, 108, 72, 1); p.fillRect(22, 23, 100, 64, 12)
        for (let i = 0; i < 3; i++) { let r = 27 - i * 7; let phase = response >= 0 && ok ? (t + i * 2) : i * 2; p.drawCircle(72, 55, r, i == control % 3 ? 10 : (i == 1 ? 13 : 8)); for (let n = 0; n < 4; n++) { let q = (n + phase) % 4; let x = q == 0 ? 72 : q == 1 ? 72 + r - 2 : q == 2 ? 72 : 72 - r + 2; let y = q == 0 ? 55 - r + 2 : q == 1 ? 55 : q == 2 ? 55 + r - 2 : 55; p.fillCircle(x, y, i == control % 3 && response >= 0 && ok ? 3 : 2, 10) } }
        p.fillCircle(72, 55, 6, 15); p.fillCircle(72, 55, 3, 10); p.fillRect(39, 86, 66, 5, 14)
    }

    function rockPath(p: Image, control: number, response: number, t: number, ok: boolean) {
        shadow(p, 71, 102, 60); p.fillRect(7, 32, 130, 56, 12); p.drawLine(8, 38, 136, 51, 14); p.drawLine(10, 75, 132, 61, 14)
        for (let i = 0; i < 5; i++) { let x = 15 + i * 24; let y = 67 - (i % 2) * 18 + (response >= 0 && !ok && i > 2 ? t * 5 : 0); p.fillCircle(x, y, 14, i == control % 5 ? 10 : (i % 2 == 0 ? 6 : 14)); p.drawCircle(x, y, 13, 1); if ((control + i) % 3 == 0) p.fillRect(x - 6, y - 6, 8, 3, 15); else if ((control + i) % 3 == 1) { p.drawLine(x - 6, y - 5, x + 5, y + 5, 15); p.drawLine(x + 5, y - 5, x - 6, y + 5, 15) } else p.fillCircle(x, y, 4, 15); p.setPixel(x + 7, y + 5, 5) }
        if (response >= 0 && ok) for (let i = 0; i < 4; i++) p.drawLine(24 + i * 24, 66 - (i % 2) * 18, 30 + i * 24, 50 - ((i + 1) % 2) * 18, 7)
        // The two inset stones expose the exact choice: same color, different mark.
        let sameColor = control == 1 || control == 3 || control == 4
        let samePattern = control == 2 || control == 3
        p.fillRect(42, 10, 60, 19, 1)
        p.fillCircle(57, 19, 7, 8); p.fillCircle(87, 19, 7, sameColor ? 8 : 3)
        p.fillCircle(57, 19, 2, 15)
        if (samePattern) p.fillCircle(87, 19, 2, 15)
        else p.drawLine(82, 19, 92, 19, 15)
        p.fillRect(6, 89, 132, 7, 1)
    }

    function interlocks(p: Image, control: number, response: number, t: number, ok: boolean) {
        shadow(p, 72, 101, 56); p.fillRect(15, 23, 114, 67, 14); p.fillRect(19, 27, 106, 59, 2)
        for (let i = 0; i < 3; i++) { let x = 43 + i * 29; gear(p, x, 55, 17, i == control % 3 ? 10 : (i == 1 ? 13 : 5), response >= 0 ? (ok ? t + i : i * 2 + (i == control % 3 ? t : 0)) : i * 2); p.fillCircle(x, 55, 5, 6) }
        p.drawLine(31, 30, 113, 30, 9); p.drawLine(31, 80, 113, 80, 9); bolt(p, 27, 30); bolt(p, 117, 80)
        if (response >= 0 && !ok) { p.drawLine(21, 23, 123, 87, 3); p.drawLine(123, 23, 21, 87, 3) }
    }

    function exitDoor(p: Image, control: number, response: number, t: number, ok: boolean) {
        shadow(p, 72, 102, 59); p.fillRect(20, 12, 76, 82, 1); p.fillRect(25, 17, 66, 77, 14); p.fillRect(29, 21, 58, 69, 12); p.fillRect(32, 24, 52, 63, 2)
        for (let y = 30; y < 82; y += 15) p.drawLine(35, y, 81, y, 14); p.fillCircle(76, 57, 4, 10)
        p.fillRect(104, 31, 8, 57, 14); p.fillCircle(108, 28, 8, 5); p.fillCircle(108, 28, 4, 10); let pull = response >= 0 && ok ? t * 4 : 0; p.drawLine(108, 35, 108 + pull, 65, ok ? 10 : 3); p.fillCircle(108 + pull, 67, 6, 3)
        if (response >= 0 && ok) { p.fillRect(29 + t * 3, 21, 52, 63, 1); for (let i = 0; i < 5; i++) p.drawLine(91, 49, 132, 28 + i * 15, 11) }
        else if (response >= 0) { p.fillCircle(108, 18 + (t % 2) * 3, 4, 3); p.fillRect(101, 91, 24, 4, 3) }
        p.fillRect(15, 94, 116, 5, 6); p.fillCircle(34 + control % 3 * 17, 92, 3, 10)
    }
}

// Physical room composition. Objects, paths and floor are readable from above.
namespace escapeArt {
    const shortNames = ["Swing magnet", "Turn generator", "Open water case", "Tip water spout", "Raise wall holds", "Cross numbered steps", "Light shadow screen", "Move portraits", "Mix mural lights", "Seat colored stones", "Focus telescope", "Warm the bath", "Pulse magnet", "Open dropper", "Balance weights", "Connect wires", "Prune plant", "Warm repaired vessel", "Pedal receiver", "Quiet the noise", "Print the strip", "Send the capsule", "Prepare pressure lift", "Level the bridge", "Aim sensors", "Open shutters", "Align star rings", "Cross patterned rocks", "Join the systems", "Pull exit lever"]
    const roomTitles = ["THE WORKSHOP", "THE LIGHT GALLERY", "THE GARDEN ROOM", "THE BRIDGE ROOM", "THE LAST DOOR"]
    const linksA = [0,1,2,3,4,9,10,11,7,15,16,14,18,19,20,22,24,26,25,27,28]
    const linksB = [1,2,3,4,5,10,6,7,8,12,17,13,19,20,21,23,25,27,28,28,29]
    const darkMap = [0,1,12,2,6,6,12,14,12,6,6,14,12,12,12,6]

    export function installPalette() {
        image.setPalette(hex`00000018182e4b3045bd4b53ed8756d8ac69706a757fc09a398b9bd4e5cff7d87966cddd283b547c66a83f6582f7f2dd`)
    }

    function oval(p: Image, cx: number, cy: number, rx: number, ry: number, color: number) {
        for (let y = -ry; y <= ry; y++) {
            let w = Math.round(rx * Math.sqrt(Math.max(0, 1 - y * y / (ry * ry))))
            p.fillRect(cx - w, cy + y, w * 2 + 1, 1, color)
        }
    }

    function words(p: Image, value: string, x: number, y: number, color: number, scale: number) {
        if (scale == 1) { p.print(value, x, y, color); return }
        let label = image.create(Math.max(1, value.length * 6), 9)
        label.print(value, 0, 0, color)
        for (let py = 0; py < 9; py++) for (let px = 0; px < label.width; px++) {
            let c = label.getPixel(px, py)
            if (c) p.fillRect(x + px * scale, y + py * scale, scale, scale, c)
        }
    }

    function stationDone(s: number, solved: number[]): boolean {
        for (let b = escapeFlow.firstBeats[s]; b <= escapeFlow.lastBeats[s]; b++) if (!solved[b]) return false
        return true
    }

    // Draw the physical setting that the learner's predicate actually reads.
    // A selected control cannot visually supply a missing lens, current or water.
    function visibleControl(b: number, control: number, solved: number[]): number {
        if (b == 1 && !solved[0]) return 0
        if (b == 3 && !solved[2]) return 0
        if (b == 4 && !solved[3]) return 0
        if (b == 6 && !solved[14]) return 0
        if (b >= 7 && b <= 10 && !solved[15]) return 0
        if (b == 14 && !solved[13]) return 0
        if ((b == 11 || b == 12) && !(solved[7] && solved[8] && solved[9] && solved[10])) return control == 4 ? 5 : 0
        if (b == 16 && !solved[19]) return control == 0 ? 3 : 1
        if (b == 17 && !solved[18]) return 0
        if (b == 21 && !solved[20]) return control == 1 || control >= 3 ? 1 : 0
        if (b == 23 && !solved[22]) return 3
        if (b == 24 && !solved[23]) return 0
        if (b == 25 && !solved[24]) return 0
        if (b == 31 && !solved[30]) return control == 2 ? 2 : 3
        if (b == 33 && !solved[32]) return 0
        return control
    }

    function floor(p: Image, room: number) {
        p.fill(12)
        // Perimeter wall thickness and the continuous floor establish the top-down room.
        p.fillRect(16, 48, 608, 388, 2)
        p.fillRect(22, 52, 596, 376, 5)
        p.fillRect(34, 67, 572, 349, 9)
        let seam = room == 2 ? 7 : room == 1 ? 11 : 5
        for (let y = 68; y < 416; y += 38) {
            p.drawLine(34, y, 605, y, 15)
            for (let x = 34 + (Math.idiv(y, 38) % 2) * 38; x < 606; x += 76) p.drawLine(x, y, x, Math.min(y + 37, 415), seam)
        }
        // Interior skirting and edge shadows; no decorative blockers in the walking lane.
        p.fillRect(34, 64, 572, 5, 6)
        p.fillRect(31, 68, 4, 348, 6)
        p.fillRect(605, 68, 4, 348, 6)
        p.fillRect(34, 416, 572, 7, 15)
        p.fillRect(38, 72, 564, 2, 15)
        // Small masonry variations fill spare wall space after puzzle placement.
        for (let x = 42; x < 605; x += 67) {
            p.drawLine(x, 51, x, 61, 4)
            p.drawLine(x + 22, 425, x + 22, 433, 4)
        }
        if (room > 0) {
            p.fillRect(12, 212, 27, 61, 1)
            p.fillRect(17, 218, 22, 48, 9)
            p.drawLine(21, 242, 31, 232, 5)
            p.drawLine(21, 242, 31, 252, 5)
        } else {
            // A small reset lever at the entrance is distinct from the puzzle furniture.
            p.fillRect(17, 227, 14, 30, 6)
            p.drawLine(23, 246, 27, 232, 4)
            p.fillCircle(27, 232, 4, 3)
        }
    }

    function connection(p: Image, a: number, b: number, done: boolean, frame: number) {
        let ax = escapeFlow.x(a), ay = escapeFlow.y(a)
        let bx = escapeFlow.x(b), by = escapeFlow.y(b)
        let color = done ? 8 : 6
        // Pipes and rails follow the floor instead of becoming more furniture.
        p.drawLine(ax, ay + 35, bx, ay + 35, 6)
        p.drawLine(ax, ay + 39, bx, ay + 39, color)
        p.drawLine(bx, ay + 35, bx, by, color)
        p.drawLine(bx + 4, ay + 35, bx + 4, by, 6)
        if (done) {
            let t = (frame % 8) / 8
            p.fillCircle(Math.round(ax + (bx - ax) * t), ay + 37, 3, 10)
        }
    }

    function door(p: Image, room: number, solved: number[]) {
        let open = escapeFlow.roomComplete(room, solved)
        p.fillRect(602, 206, 30, 73, 1)
        p.fillRect(607, 210, 21, 66, open ? 15 : 4)
        if (open) {
            p.fillRect(597, 219, 31, 48, 9)
            for (let i = 0; i < 3; i++) p.drawLine(607 + i * 6, 237, 612 + i * 6, 242, 8)
            for (let i = 0; i < 3; i++) p.drawLine(607 + i * 6, 247, 612 + i * 6, 242, 8)
        } else {
            p.fillRect(610, 218, 3, 48, 5)
            p.fillRect(619, 218, 3, 48, 2)
            p.fillCircle(618, 245, 3, 10)
            // Each finished chain retracts its own real door catch.
            let catches = room == 0 ? [5] : room == 1 ? [6,12] : room == 2 ? [16,21,17] : room == 3 ? [25,29] : [31,33,34]
            for (let i = 0; i < catches.length; i++) {
                let y = 242 - (catches.length - 1) * 10 + i * 20
                let released = solved[catches[i]] == 1
                p.fillRect(released ? 615 : 601, y - 2, released ? 5 : 19, 5, released ? 7 : 6)
                p.fillCircle(624, y, 3, released ? 7 : 3)
            }
        }
    }

    export function world(room: number, solved: number[], introduced: number[], focusBeat: number, activeBeat: number, controls: number[], response: number, reactionFrame: number, pitch: number, firstClear: number): Image {
        let p = image.create(640, 480)
        floor(p, room)
        let focus = escapeFlow.stationForBeat(focusBeat)
        let active = activeBeat < 0 ? -1 : escapeFlow.stationForBeat(activeBeat)
        for (let l = 0; l < linksA.length; l++) if (Math.idiv(linksA[l], 6) == room) connection(p, linksA[l], linksB[l], stationDone(linksA[l], solved), reactionFrame)
        door(p, room, solved)
        // Back-to-front placement keeps overlapping physical silhouettes legible.
        for (let row = 0; row < 2; row++) for (let local = 0; local < 6; local++) {
            let s = room * 6 + local
            let x = escapeFlow.x(s), y = escapeFlow.y(s)
            if ((y < 250 ? 0 : 1) != row) continue
            let b = s == active ? activeBeat : solved[escapeFlow.lastBeats[s]] ? escapeFlow.lastBeats[s] : escapeFlow.firstBeats[s]
            let done = stationDone(s, solved)
            let available = escapeFlow.available(s, solved, introduced, focusBeat)
            oval(p, x + 4, y + 43, 53, 11, 6)
            if (s == focus) {
                oval(p, x, y + 47, 62, 12, 5)
                oval(p, x, y + 46, 57, 8, 10)
                oval(p, x, y + 46, 48, 5, 9)
            }
            let portraitMask = solved[7] + 2 * solved[8] + 4 * solved[9] + 8 * solved[10]
            let object = escapeObjects.prop(s, visibleControl(b, controls[b] || 0, solved), s == active ? response : -1, reactionFrame, solved[b] == 1, s == 7 ? b - 7 : b - escapeFlow.firstBeats[s], pitch, portraitMask)
            if (!available) {
                for (let py = 0; py < object.height; py++) for (let px = 0; px < object.width; px++) {
                    let c = object.getPixel(px, py)
                    if (c) object.setPixel(px, py, darkMap[c])
                }
            }
            p.drawTransparentImage(object, x - 72, y - 56)
            if (s == focus) {
                p.fillRect(x - 3, y - 57, 7, 5, 10)
                p.drawLine(x - 8, y - 52, x, y - 45, 10)
                p.drawLine(x + 8, y - 52, x, y - 45, 10)
            }
            // Only the current object receives an interaction caption; the room is not a label grid.
            if (s == active || s == focus) {
                let name = shortNames[s]
                let left = Math.max(38, Math.min(600 - name.length * 6, x - name.length * 3))
                p.fillRect(left - 4, y + 53, name.length * 6 + 8, 12, 12)
                words(p, name, left, y + 55, 15, 1)
            }
        }
        p.fillRect(0, 0, 640, 42, 12)
        words(p, roomTitles[room], 18, 9, 15, 2)
        words(p, "ROOM " + (room + 1) + "/5", 535, 13, 10, 1)
        p.fillRect(0, 441, 640, 39, 12)
        if (activeBeat >= 0) {
            words(p, escapeLab.readout(activeBeat), 14, 445, 15, 2)
            words(p, "A OPERATE   LEFT/RIGHT ADJUST   UP/DOWN PART   B WALK", 14, 467, 10, 1)
        } else {
            let target = focus < 0 ? "Walk to the open doorway" : "Next: " + shortNames[focus]
            words(p, target, 14, 445, 15, 2)
            words(p, "ARROWS WALK   A INTERACT   GOLD LIGHT GUIDES YOU", 14, 467, 10, 1)
        }
        return p
    }

    export function explorer(direction: number, step: number): Image {
        let p = image.create(32, 40)
        oval(p, 16, 36, 11, 3, 6)
        let stride = step % 3 == 0 ? 0 : step % 3 == 1 ? 2 : -2
        p.fillRect(8, 28 + stride, 6, 9, 12)
        p.fillRect(19, 28 - stride, 6, 9, 12)
        p.fillRect(8, 35 + stride, 8, 3, 2)
        p.fillRect(19, 35 - stride, 8, 3, 2)
        p.fillRect(7, 16, 20, 15, 8)
        p.fillRect(10, 17, 14, 5, 11)
        p.fillRect(5, 21 - stride, 4, 10, 5)
        p.fillRect(26, 21 + stride, 4, 10, 5)
        p.fillRect(8, 3, 18, 15, 4)
        p.fillRect(10, 8, 14, 11, 5)
        p.fillRect(7, 2, 21, 5, 2)
        p.fillRect(8, 5, 5, 6, 2)
        if (direction == 3) p.fillRect(10, 7, 15, 13, 2)
        else if (direction == 1) { p.fillRect(9, 12, 3, 3, 1); p.fillRect(6, 16, 5, 3, 4) }
        else if (direction == 2) { p.fillRect(22, 12, 3, 3, 1); p.fillRect(24, 16, 5, 3, 4) }
        else { p.fillRect(12, 12, 3, 3, 1); p.fillRect(21, 12, 3, 3, 1); p.fillRect(15, 18, 6, 2, 4) }
        return p
    }

    export function ending(firstClear: number, secondClear: number, phase: number): Image {
        let p = image.create(640, 480)
        p.fill(9)
        p.fillRect(0, 305, 640, 175, 7)
        for (let i = 0; i < 7; i++) {
            oval(p, 50 + i * 92, 314, 70, 16, 8)
            p.fillCircle(48 + i * 92, 298, 4 + (phase + i) % 3, 10)
        }
        p.fillRect(223, 79, 194, 230, 2)
        p.fillRect(235, 90, 170, 220, 5)
        p.fillRect(248, 101, 144, 209, 15)
        p.fillRect(278, 122, 84, 188, 9)
        p.drawTransparentImage(explorer(0, phase % 3), 304, 269)
        words(p, secondClear ? "YOU DID IT!" : "YOU FOUND THE WAY OUT!", secondClear ? 253 : 194, 34, 12, 2)
        words(p, secondClear ? "Every room works because of your code." : "Your rules brought every room to life.", 94, 356, 12, 2)
        words(p, secondClear ? "Two complete escapes. Congratulations!" : "B: play the whole adventure once more", 98, 389, 12, 2)
        words(p, "Your completion is saved.", 175, 435, 2, 2)
        return p
    }
}

namespace userconfig {
    export const ARCADE_SCREEN_WIDTH = 640
    export const ARCADE_SCREEN_HEIGHT = 480
}

//% color=#4767ac icon="\uf11b" block="Escape Room" weight=90
namespace escapeLab {
    const saveKey = "logic-escape-room:v2"
    const legacyKey = "logic-escape-room:v1"
    const saveVersion = 2
    let handlers: (() => void)[] = []
    let solved: number[] = []
    let introduced: number[] = []
    let controls: number[] = []
    let room = 0
    let firstClear = 0
    let secondClear = 0
    let ending = 0
    let pitch = -20
    let pressureReady = false
    let player: Sprite = null
    let focused = false
    let station = -1
    let beat = -1
    let fixture = 0
    let response = -1
    let credible = true
    let phase = 0
    let inAttempt = false
    let lastWorldX = 320
    let lastWorldY = 235
    let resetArmed = false
    let explorerFacing = 0
    let reactionFrame = -1
    let scurryFrames = 0
    let flame: Sprite = null
    let busy = false

    const firstBeats = escapeFlow.firstBeats
    const lastBeats = escapeFlow.lastBeats
    const stationNames = escapeFlow.stationNames
    const roomNames = escapeFlow.roomNames
    const clues = escapeFlow.clues

    function fresh() {
        room = 0
        ending = 0
        pitch = -20
        pressureReady = false
        solved = []
        introduced = []
        controls = []
        for (let i = 0; i < 36; i++) { solved.push(0); introduced.push(0); controls.push(0) }
    }

    function safeInteger(value: number, fallback: number, low: number, high: number): number {
        // Settings storage is outside this game. Accept only finite whole
        // values, then keep it within a deliberately broad game-safe range.
        if (value != Math.round(value) || value <= -1000000 || value >= 1000000) return fallback
        return Math.max(low, Math.min(high, value))
    }

    function load() {
        let data = settings.readNumberArray(saveKey)
        let legacy = false
        if (!data || data.length != 115 || data[0] != saveVersion) {
            data = settings.readNumberArray(legacyKey)
            legacy = !!data && data.length == 43 && data[0] == 1
        }
        if (!data || (!legacy && (data.length != 115 || data[0] != saveVersion))) {
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
        introduced = []
        controls = []
        for (let i = 0; i < 36; i++) {
            introduced.push(legacy ? 0 : data[43 + i] == 1 ? 1 : 0)
            controls.push(legacy ? 0 : safeInteger(data[79 + i], 0, 0, 4))
        }
        // Old successes count only when their new physical source also exists.
        if (legacy) {
            const source = [-1,0,1,2,3,4,14,15,15,15,15,7,11,-1,13,-1,19,18,-1,-1,-1,20,-1,22,23,24,-1,26,27,28,-1,30,-1,32,31,34]
            for (let pass = 0; pass < 36; pass++) {
                for (let b = 0; b < 36; b++) if (source[b] >= 0 && !solved[source[b]]) solved[b] = 0
                if (!solved[7] || !solved[8] || !solved[9] || !solved[10]) solved[11] = 0
                if (!solved[31] || !solved[33] || !solved[1] || !solved[27] || !solved[25] || !solved[30]) solved[34] = 0
            }
            if (!solved[35]) ending = 0
            for (let r = 0; r < room; r++) if (!escapeFlow.roomComplete(r, solved)) { room = r; break }
            save()
        }
    }

    function save() {
        let data = [saveVersion, room, firstClear, secondClear, ending, pitch, pressureReady ? 1 : 0]
        for (let i = 0; i < 36; i++) data.push(solved[i])
        for (let i = 0; i < 36; i++) data.push(introduced[i])
        for (let i = 0; i < 36; i++) data.push(controls[i])
        settings.writeNumberArray(saveKey, data)
    }

    function clearThisGame() {
        resetArmed = false
        // A replay clears the current run while preserving earned finish history.
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

    function stationX(local: number): number { return escapeFlow.x(room * 6 + local) }
    function stationY(local: number): number { return escapeFlow.y(room * 6 + local) }

    function nearestStation(): number {
        let best = -1
        let distance = 10000
        for (let local = 0; local < 6; local++) {
            let dx = player.x - stationX(local)
            let dy = player.y - stationY(local)
            let d = dx * dx + dy * dy
            if (d < distance) { distance = d; best = room * 6 + local }
        }
        return distance < 8500 ? best : -1
    }

    function enterStation(s: number) {
        station = s
        beat = firstBeats[s]
        for (let i = firstBeats[s]; i <= lastBeats[s]; i++) if (!solved[i]) { beat = i; break }
        fixture = controls[beat]
        response = -1
        credible = true
        focused = true
        lastWorldX = player.x
        lastWorldY = player.y
        controller.moveSprite(player, 0, 0)
        draw()
    }

    function prerequisitesMet(b: number): boolean {
        if (b == 1) return solved[0] == 1
        if (b == 2) return solved[1] == 1
        if (b == 3) return solved[2] == 1
        if (b == 4) return solved[3] == 1
        if (b == 5) return solved[4] == 1
        if (b == 6) return solved[14] == 1
        if (b >= 7 && b <= 10) return solved[15] == 1
        if (b == 11) return solved[7] == 1 && solved[8] == 1 && solved[9] == 1 && solved[10] == 1
        if (b == 12) return solved[11] == 1
        if (b == 14) return solved[13] == 1
        if (b == 16) return solved[19] == 1
        if (b == 17) return solved[18] == 1
        if (b == 21) return solved[20] == 1
        if (b == 23) return solved[22] == 1
        if (b == 24) return solved[23] == 1
        if (b == 25) return solved[24] == 1
        if (b == 27) return solved[26] == 1
        if (b == 28) return solved[27] == 1
        if (b == 29) return solved[28] == 1 && solved[27] == 1
        if (b == 31) return solved[30] == 1
        if (b == 33) return solved[32] == 1
        if (b == 34) return solved[31] == 1 && solved[33] == 1
        if (b == 35) return solved[34] == 1
        return true
    }

    function leaveStation() {
        scurryFrames = 0
        flame.setFlag(SpriteFlag.Invisible, true)
        focused = false
        station = -1
        beat = -1
        fixture = 0
        response = -1
        credible = true
        player.setPosition(lastWorldX, lastWorldY)
        controller.moveSprite(player, 150, 150)
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
        if (b == 0) return ["MAGNET FAR", "MAGNET TOUCHING CRANK"][f]
        if (b == 1) return ["CRANK LOOSE", "CRANK FITTED"][f]
        if (b == 2) return ["BUTTON UP", "BUTTON PRESSED"][f]
        if (b == 3) return ["SPOUT CLOSED", "SPOUT TIPPED"][f]
        if (b == 4) return ["3 HOLDS", "4 HOLDS"][f]
        if (b == 5) return ["STEP 8 + 3", "STEP 7 + 3", "STEP 6 + 3"][f]
        if (b == 6) return ["LIGHT 59", "LIGHT 60"][f]
        if (b >= 7 && b <= 10) return ["RIGHT PLATE = 2", "LEFT PLATE = 1"][f]
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
        if (fact == EscapeFact.LockFree) return beat == 2 && fixture == 1 && solved[1] == 1
        if (fact == EscapeFact.MagnetTouchingCrank) return beat == 0 && fixture == 1
        if (fact == EscapeFact.CrankFitted) return beat == 1 && fixture == 1 && solved[0] == 1
        if (fact == EscapeFact.PowerAvailable) return solved[1] == 1
        if (fact == EscapeFact.WaterFlowing) return beat == 3 && fixture == 1 && solved[2] == 1
        if (fact == EscapeFact.YellowOn) return (fixture == 1 || fixture >= 3) && solved[7] == 1 && solved[8] == 1 && solved[9] == 1 && solved[10] == 1
        if (fact == EscapeFact.BlueOn) return (fixture == 2 || fixture >= 3) && solved[7] == 1 && solved[8] == 1 && solved[9] == 1 && solved[10] == 1
        if (fact == EscapeFact.RedOn) return fixture == 4
        if (fact == EscapeFact.Metallic) return beat == 16 && fixture > 0
        if (fact == EscapeFact.MagnetOn) return beat == 16 && solved[19] == 1 && (fixture == 0 || fixture == 2)
        if (fact == EscapeFact.VesselRepaired) return beat == 21 && solved[20] == 1 && fixture >= 2
        if (fact == EscapeFact.VesselHot) return beat == 21 && (fixture == 1 || fixture >= 3)
        if (fact == EscapeFact.ScratchOn) return beat == 23 && (fixture == 0 || fixture == 3 || !solved[22])
        if (fact == EscapeFact.BeepOn) return beat == 23 && (fixture == 1 || fixture == 3 || !solved[22])
        if (fact == EscapeFact.HumOn) return beat == 23 && (fixture == 2 || fixture == 3 || !solved[22])
        if (fact == EscapeFact.RadioClear) return beat == 24 && (fixture == 1 || fixture == 3) && solved[22] == 1 && solved[23] == 1
        if (fact == EscapeFact.CableConnected) return beat == 24 && (fixture == 2 || fixture == 3) && solved[23] == 1
        if (fact == EscapeFact.RouteA) return beat == 25 && fixture == 1 && solved[24] == 1
        if (fact == EscapeFact.RouteB) return beat == 25 && fixture == 2 && solved[24] == 1
        if (fact == EscapeFact.PressureReady) return pressureReady
        if (fact == EscapeFact.WindowA) return beat == 31 && solved[30] == 1 && (fixture == 0 || fixture == 4)
        if (fact == EscapeFact.WindowB) return beat == 31 && solved[30] == 1 && fixture == 1
        if (fact == EscapeFact.DangerousControl) return beat == 31 && fixture == 2
        if (fact == EscapeFact.FrontMatch) return beat == 32 && fixture != 0
        if (fact == EscapeFact.MiddleMatch) return beat == 32 && fixture != 1
        if (fact == EscapeFact.BackMatch) return beat == 32 && fixture != 2
        if (fact == EscapeFact.SameColor) return beat == 33 && solved[32] == 1 && (fixture == 1 || fixture >= 3)
        if (fact == EscapeFact.SamePattern) return beat == 33 && solved[32] == 1 && (fixture == 2 || fixture == 3)
        if (fact == EscapeFact.PowerReady) return beat == 34 && fixture != 0 && solved[1] == 1
        if (fact == EscapeFact.PressureSystemReady) return beat == 34 && fixture != 1 && solved[26] == 1 && solved[27] == 1 && solved[31] == 1
        if (fact == EscapeFact.SignalReady) return beat == 34 && fixture != 2 && solved[22] == 1 && solved[23] == 1 && solved[24] == 1 && solved[25] == 1 && solved[30] == 1
        if (fact == EscapeFact.AlarmOn) return (beat == 34 && fixture == 3) || (beat == 35 && fixture == 1)
        return false
    }

    function meterValue(m: EscapeMeter): number {
        if (m == EscapeMeter.InstalledHolds) return fixture == 0 || !solved[3] ? 3 : 4
        if (m == EscapeMeter.StepValue) return [8,7,6][fixture]
        if (m == EscapeMeter.Illumination) return fixture == 0 || !solved[14] ? 59 : 60
        if (m == EscapeMeter.ShoeSide) return fixture == 0 || !solved[15] ? 2 : 1
        if (m == EscapeMeter.StoneColor) return [1,2,3][fixture]
        if (m == EscapeMeter.SocketColor) return [2,2,3][fixture]
        if (m == EscapeMeter.Zoom) return fixture == 0 || !solved[13] ? 2 : 3
        if (m == EscapeMeter.Temperature) return [19,20,40,41][fixture]
        if (m == EscapeMeter.Drops) return !solved[18] ? 6 : [6,7,9,10][fixture]
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
        if (b >= 7 && b <= 10) return a == EscapeAction.PortraitLeft
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
        if (b == 0) return a == (factValue(EscapeFact.MagnetTouchingCrank) ? EscapeAction.CrankPull : EscapeAction.CrankTwitch)
        if (b == 1) return a == (factValue(EscapeFact.CrankFitted) ? EscapeAction.GeneratorSpin : EscapeAction.GeneratorSputter)
        if (b == 2) return a == (factValue(EscapeFact.PowerAvailable) ? EscapeAction.CaseRetract : EscapeAction.CaseRattle)
        if (b == 3) return a == (factValue(EscapeFact.WaterFlowing) ? EscapeAction.FireSteam : EscapeAction.FireFlare)
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
        if (b == 29) return a == (pitch == 0 && solved[27] ? EscapeAction.PitchLevel : pitch < 0 ? EscapeAction.PitchDown : EscapeAction.PitchUp)
        if (b == 30) return a == (fixture == 0 ? EscapeAction.SensorLamp1 : fixture == 1 ? EscapeAction.SensorLamp2 : fixture == 2 ? EscapeAction.SensorLamp3 : EscapeAction.SensorDark)
        if (b == 31) return a == (factValue(EscapeFact.WindowA) || factValue(EscapeFact.WindowB) ? EscapeAction.ShutterOpen : factValue(EscapeFact.DangerousControl) ? EscapeAction.ShutterWarn : EscapeAction.ShutterClosed)
        if (b == 32) return a == (factValue(EscapeFact.FrontMatch) && factValue(EscapeFact.MiddleMatch) && factValue(EscapeFact.BackMatch) ? EscapeAction.StarIgnite : EscapeAction.StarFizzle)
        if (b == 33) return a == (factValue(EscapeFact.SameColor) && !factValue(EscapeFact.SamePattern) ? EscapeAction.RockBeam : EscapeAction.RockCollapse)
        if (b == 34) return a == (factValue(EscapeFact.PowerReady) && factValue(EscapeFact.PressureSystemReady) && factValue(EscapeFact.SignalReady) && !factValue(EscapeFact.AlarmOn) ? EscapeAction.SyncLock : EscapeAction.SyncReject)
        if (b == 35) return a == (meterValue(EscapeMeter.CoreLights) == 3 && !factValue(EscapeFact.AlarmOn) ? EscapeAction.LeverPull : EscapeAction.LeverReject)
        return false
    }

    export function focusStation(): number { return station }
    export function readout(b: number): string {
        if (!focused || b != beat) return ""
        if (b == 14) return "ZOOM " + meterValue(EscapeMeter.Zoom) + (solved[13] ? "" : " - LENS EMPTY")
        if (b == 6) return "LIGHT " + meterValue(EscapeMeter.Illumination) + (solved[14] ? "" : " - BEAM DIM")
        if (b >= 7 && b <= 10) return solved[15] ? inputLabel(b, fixture) : "RAILS FROZEN - RIGHT PLATE"
        if (b == 17) return meterValue(EscapeMeter.Drops) + " DROPS" + (solved[18] ? "" : " - DROPPER HELD")
        if (b == 4) return meterValue(EscapeMeter.InstalledHolds) + " HOLDS"
        if (b == 28 && !solved[27]) return "HYDRAULIC LIFT IS DOWN"
        if (b == 28 || b == 29) return "BRIDGE " + pitch + " DEGREES - " + inputLabel(b, fixture)
        if (b == 0 && fixture == 1) return "MAGNET SWINGS TO CRANK"
        if (b == 1 && fixture == 1 && !solved[0]) return "CRANK RAIL EMPTY"
        if (b == 2 && !solved[1]) return "CASE MOTOR HAS NO POWER"
        if (b == 3 && !solved[2]) return "SPOUT RESERVOIR EMPTY"
        if (b == 21 && !solved[20]) return "REPAIR LEVER TRAPPED"
        if (b == 23 && !solved[22]) return "RECEIVER SILENT - CHANNELS HISS"
        if (b == 24 && !solved[23]) return "NOISE BLOCKS THE SIGNAL CONDUIT"
        if (b == 25 && !solved[24]) return "SELECTOR WAITS FOR PAPER STRIP"
        if (b == 31 && !solved[30]) return "SHUTTER SENSORS UNMAPPED"
        if (b == 33 && !solved[32]) return "ROCK PATH UNLIT"
        return inputLabel(b, fixture)
    }
    function draw() {
        if (ending > 0) scene.setBackgroundImage(escapeArt.ending(firstClear, secondClear, phase))
        else scene.setBackgroundImage(escapeArt.world(room, solved, introduced, escapeFlow.focusBeat(room, solved, introduced), focused ? beat : -1, controls, response, reactionFrame, pitch, firstClear))
    }

    function keepPlayerOnPaths() {
        if (focused || ending > 0) return
        player.x = Math.max(40, Math.min(600, player.x))
        player.y = Math.max(76, Math.min(420, player.y))
        // The feet collide with solid bases only, leaving rails and shadows walkable.
        for (let local = 0; local < 6; local++) {
            let s = room * 6 + local
            let x = stationX(local)
            let y = stationY(local)
            let halfW = Math.idiv(escapeFlow.width(s), 2) + 9
            let halfH = Math.idiv(escapeFlow.height(s), 2) + 7
            let dx = player.x - x
            let dy = player.y - y
            if (Math.abs(dx) >= halfW || Math.abs(dy) >= halfH) continue
            if (Math.abs(dx) * halfH > Math.abs(dy) * halfW) player.x = x + (dx < 0 ? -halfW : halfW)
            else player.y = y + (dy < 0 ? -halfH : halfH)
        }
    }

    function updateExplorer() {
        if (ending > 0) return
        let moving = Math.abs(player.vx) + Math.abs(player.vy) > 1
        if (Math.abs(player.vx) > Math.abs(player.vy) && Math.abs(player.vx) > 1) explorerFacing = player.vx < 0 ? 1 : 2
        else if (Math.abs(player.vy) > 1) explorerFacing = player.vy < 0 ? 3 : 0
        player.setImage(escapeArt.explorer(explorerFacing, moving ? phase % 3 + 1 : 0))
    }

    //% block="when $b is operated" draggableParameters=reporter
    //% weight=100
    export function onAttempt(b: EscapeBeat, handler: () => void) { handlers[b] = handler }

    // Legacy compatibility for older saves; new construction uses physical facts.
    //% blockHidden=true
    export function has(item: EscapeItem): boolean {
        if (!focused) return false
        if (item == EscapeItem.LargeMagnet) return factValue(EscapeFact.MagnetTouchingCrank)
        if (item == EscapeItem.HandCrank) return factValue(EscapeFact.CrankFitted)
        if (item == EscapeItem.WaterCanister) return factValue(EscapeFact.WaterFlowing)
        return false
    }

    //% block="is $fact" weight=80
    export function is(fact: EscapeFact): boolean { return factValue(fact) }

    //% block="value of $meter" weight=70
    export function number(meter: EscapeMeter): number { return meterValue(meter) }

    //% block="make $action happen" weight=60
    export function make(action: EscapeAction) {
        if (!focused || !inAttempt || !actionBelongs(beat, action)) return
        response = action
        credible = matchesInput(beat, action)
        reactionFrame = 0
        if (action == EscapeAction.FireFlare && credible) {
            scurryFrames = 12
            flame.setFlag(SpriteFlag.Invisible, false)
        }
        if (action == EscapeAction.SealStable) pressureReady = credible
        if (action == EscapeAction.SealLeak) pressureReady = false
        if (beat == 27) pressureReady = false
        let success = credible && prerequisitesMet(beat) && progressAction(beat, action)
        if (success) {
            solved[beat] = 1
            if (action == EscapeAction.LeverPull) {
                if (firstClear == 0) { firstClear = 1; ending = 1 }
                else { secondClear = 1; ending = 2 }
                focused = false
                player.setFlag(SpriteFlag.Invisible, true)
            }
        } else if (credible && action == escapeFlow.introAction(beat) && !solved[beat] && escapeFlow.focusBeat(room, solved, introduced) == beat) {
            let prerequisite = escapeFlow.introTarget(beat)
            if (prerequisite >= 0 && !solved[prerequisite]) introduced[beat] = 1
        }
        save()
        draw()
    }

    //% block="set room pitch to $newAngle" weight=50
    export function setPitch(newAngle: number) {
        if (!focused || !inAttempt || beat != 28 || !prerequisitesMet(beat)) return
        credible = newAngle == pitch + meterValue(EscapeMeter.PitchChange)
        pitch = newAngle
        if (credible) solved[28] = 1
        response = EscapeAction.PitchUp
        reactionFrame = 0
        save()
        draw()
    }

    controller.A.onEvent(ControllerButtonEvent.Pressed, function () {
        if (ending > 0) return
        if (focused) {
            if (busy) return
            busy = true
            response = -1
            reactionFrame = 0
            draw()
            let operatedBeat = beat
            pause(360)
            if (!focused || beat != operatedBeat) { busy = false; return }
            let handler = handlers[beat]
            if (handler) { inAttempt = true; handler(); inAttempt = false }
            busy = false
            draw()
            return
        }
        if (resetArmed) {
            cancelReset()
            return
        }
        if (player.x >= 588 && player.y >= 205 && player.y <= 275 && room < 4) {
            if (escapeFlow.roomComplete(room, solved)) { room++; player.setPosition(52, 240); save(); draw() }
            else player.sayText("The exit still needs its catches", 900, false)
            return
        }
        if (player.x <= 52 && player.y >= 205 && player.y <= 275 && room > 0) { room--; player.setPosition(588, 240); save(); draw(); return }
        let s = nearestStation()
        if (s >= 0 && escapeFlow.available(s, solved, introduced, escapeFlow.focusBeat(room, solved, introduced))) enterStation(s)
    })

    controller.B.onEvent(ControllerButtonEvent.Pressed, function () {
        if (ending > 0) {
            fresh()
            save()
            control.reset()
            return
        }
        if (focused) {
            leaveStation()
            save()
            return
        }
        if (room == 0 && player.x <= 52) {
            if (resetArmed) clearThisGame()
            else {
                resetArmed = true
                player.sayText("Press B again to reset. A cancels.", 1500, false)
            }
        }
    })

    controller.left.onEvent(ControllerButtonEvent.Pressed, function () {
        if (!focused) { cancelReset(); return }
        fixture = (fixture + fixtureCount(beat) - 1) % fixtureCount(beat)
        controls[beat] = fixture
        save()
        response = -1
        draw()
    })
    controller.right.onEvent(ControllerButtonEvent.Pressed, function () {
        if (!focused) { cancelReset(); return }
        fixture = (fixture + 1) % fixtureCount(beat)
        controls[beat] = fixture
        save()
        response = -1
        draw()
    })
    controller.up.onEvent(ControllerButtonEvent.Pressed, function () {
        if (!focused) { cancelReset(); return }
        if (beat <= firstBeats[station]) return
        beat--
        fixture = controls[beat]
        response = -1
        draw()
    })
    controller.down.onEvent(ControllerButtonEvent.Pressed, function () {
        if (!focused) { cancelReset(); return }
        if (beat >= lastBeats[station]) return
        beat++
        fixture = controls[beat]
        response = -1
        draw()
    })

    load()
    escapeArt.installPalette()
    player = sprites.create(escapeArt.explorer(0, 0), SpriteKind.Player)
    player.setPosition(320, 235)
    controller.moveSprite(player, 150, 150)
    player.setStayInScreen(true)
    let flameImage = image.create(10, 14)
    flameImage.setPixel(4, 0, 4)
    flameImage.setPixel(5, 1, 4)
    flameImage.fillRect(3, 3, 5, 8, 4)
    flameImage.fillRect(4, 6, 3, 7, 5)
    flame = sprites.create(flameImage, SpriteKind.Projectile)
    flame.setFlag(SpriteFlag.Invisible, true)
    if (ending > 0) { player.setFlag(SpriteFlag.Invisible, true); controller.moveSprite(player, 0, 0) }
    game.onUpdateInterval(120, function () {
        phase++
        if (reactionFrame >= 0) {
            reactionFrame++
            if (reactionFrame > 16) { reactionFrame = -1; response = -1 }
        }
        if (scurryFrames > 0) {
            let elapsed = 12 - scurryFrames
            player.setPosition(lastWorldX + (elapsed < 4 ? (elapsed + 1) * 5 : elapsed < 8 ? (8 - elapsed) * 5 : 0), lastWorldY + (elapsed < 8 ? 7 : 0))
            flame.setPosition(player.x + 6, player.y - 24)
            scurryFrames--
            if (scurryFrames == 0) { player.setPosition(lastWorldX, lastWorldY); flame.setFlag(SpriteFlag.Invisible, true) }
        }
        keepPlayerOnPaths()
        updateExplorer()
        draw()
    })
    draw()
}
```
