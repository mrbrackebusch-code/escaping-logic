# Escaping Logic — Room A: Workshop

### @explicitHints true

## Room A

This Recipe covers constructions **1–6**. Start with construction 1 below.

## 1. Clear the fire channel

The fixed fire spout blocks the wall route. First build ``||escapeLab(noclick):when [(A) fire spout] is operated||`` with ``||logic(noclick):if then else||``. Test ``||escapeLab(noclick):is [(A) WaterFlowing]||``; make `(A) FireSteam` happen when it is true and `(A) FireFlare` otherwise. Then press **A** near the fire spout to operate it. Because water is not flowing yet, `(A) FireFlare` briefly catches the explorer's coat while you keep moving. You need both branches because you will return after water reaches this spout; that alternate reaction lights the sealed case reservoir next.

### Find the native Blocks

![Find the native Blocks for Fire](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/f873e84e6ab7e9a4/media/menu/01-fire-01-fire-menu.svg)

### Build this rule

![Build this rule for Fire](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/f873e84e6ab7e9a4/media/assembled/01-fire-01-fire-assembled.svg)

### What the mechanism does

![What the mechanism does for Fire](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/f873e84e6ab7e9a4/media/gameplay/01-fire-connected-v2-physical-v6-01-01-fire.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.Fire, function () {
    if (escapeLab.is(EscapeFact.WaterFlowing)) escapeLab.make(EscapeAction.FireSteam)
    else escapeLab.make(EscapeAction.FireFlare)
})
```

## 2. Open the reservoir case

The case button cannot release its fixed reservoir until power arrives. In ``||escapeLab(noclick):when [(A) power case] is operated||``, test ``||escapeLab(noclick):is [(A) PowerAvailable]||``. Make `(A) CaseRetract` happen for true and `(A) CaseRattle` happen for else, then operate the unpowered case once to see its restrained rattle. The generator handle is now the uncertain next light. When you return with power, the open case puts a water canister on its tray: pick it up, carry it to the fire-spout pad, fit it, then operate your fire rule.

### Build this rule

![Build this rule for Case](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/f873e84e6ab7e9a4/media/assembled/02-case-02-case-assembled.svg)

### What the mechanism does

![What the mechanism does for Case](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/f873e84e6ab7e9a4/media/gameplay/02-case-connected-v2-physical-v6-01-02-case.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.Case, function () {
    if (escapeLab.is(EscapeFact.PowerAvailable)) escapeLab.make(EscapeAction.CaseRetract)
    else escapeLab.make(EscapeAction.CaseRattle)
})
```

## 3. Start the generator

The generator's handle turns only with a crank fitted to its rail. In ``||escapeLab(noclick):when [(A) generator] is operated||``, test ``||escapeLab(noclick):is [(A) CrankFitted]||``. Make `(A) GeneratorSpin` happen when true and `(A) GeneratorSputter` otherwise. Operate it once before the crank is fitted: the rotor stalls, then the magnet rail at the upper left becomes the next goal. This is another ordinary if/else rule whose successful branch will matter when you come back.

### Build this rule

![Build this rule for Generator](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/f873e84e6ab7e9a4/media/assembled/03-generator-03-generator-assembled.svg)

### What the mechanism does

![What the mechanism does for Generator](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/f873e84e6ab7e9a4/media/gameplay/03-generator-connected-v2-physical-v6-01-03-generator.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.Generator, function () {
    if (escapeLab.is(EscapeFact.CrankFitted)) escapeLab.make(EscapeAction.GeneratorSpin)
    else escapeLab.make(EscapeAction.GeneratorSputter)
})
```

## 4. Swing the mounted magnet

The magnet is mounted on a rail; it is not something to collect. In ``||escapeLab(noclick):when [(A) magnet rail] is operated||``, test ``||escapeLab(noclick):is [(A) MagnetTouchingCrank]||``. Make `(A) CrankPull` happen when true and `(A) CrankTwitch` otherwise. Hold **B** on the magnet rail's pad, use **left/right** to swing the magnet near the crank, then press **A** to operate it and release **B**. Choose the near position first: a crank appears on its tray. Pick it up with **A**, carry it to the generator pad, and press **A** to fit it. Return to the generator, then the case, then the fire spout, and operate each of your three earlier rules.

### Build this rule

![Build this rule for Crank](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/f873e84e6ab7e9a4/media/assembled/04-crank-04-crank-assembled.svg)

### What the mechanism does

![What the mechanism does for Crank](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/f873e84e6ab7e9a4/media/gameplay/04-crank-connected-v2-physical-v6-01-04-crank.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.Crank, function () {
    if (escapeLab.is(EscapeFact.MagnetTouchingCrank)) escapeLab.make(EscapeAction.CrankPull)
    else escapeLab.make(EscapeAction.CrankTwitch)
})
```

## 5. Raise the wall holds

With the fire channel clear, the wall lever recovers the fixed holds. In ``||escapeLab(noclick):when [(A) climb wall] is operated||``, test ``||escapeLab(noclick):value of [(A) InstalledHolds]||`` = `4`; make `(A) WallClimb` happen when it passes and `(A) WallFlash` otherwise. Choose `4 HOLDS`, then operate the lever after the steam clears. The holds rise into a climbable route, and the lit footprints at the exit tell you what to test next.

### Find the native Blocks

![Find the native Blocks for Wall](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/f873e84e6ab7e9a4/media/menu/05-wall-05-wall-comparisons-menu.svg)

### Build this rule

![Build this rule for Wall](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/f873e84e6ab7e9a4/media/assembled/05-wall-05-wall-assembled.svg)

### What the mechanism does

![What the mechanism does for Wall](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/f873e84e6ab7e9a4/media/gameplay/05-wall-connected-v2-physical-v6-01-05-wall.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.Wall, function () {
    if (escapeLab.number(EscapeMeter.InstalledHolds) == 4) escapeLab.make(EscapeAction.WallClimb)
    else escapeLab.make(EscapeAction.WallFlash)
})
```

## 6. Choose a safe footprint

The three marked stones show `8`, `7`, and `6`; any value with `+ 3 ≤ 10` is safe. In ``||escapeLab(noclick):when [(A) footprint stones] is operated||``, test ``||escapeLab(noclick):value of [(A) StepValue]|| + 3 ≤ 10``. Make `(A) FootprintKeep` for true and `(A) FootprintDrop` for else. Choose `7` or `6` first—this is a choice puzzle, so it can work immediately. A safe footprint opens the real passage into Room B and lights its shadow screen.

### Build this rule

![Build this rule for Footprints](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/f873e84e6ab7e9a4/media/assembled/06-footprints-06-footprints-assembled.svg)

### What the mechanism does

![What the mechanism does for Footprints](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/f873e84e6ab7e9a4/media/gameplay/06-footprints-connected-v2-physical-v6-01-06-footprints.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.Footprints, function () {
    if (escapeLab.number(EscapeMeter.StepValue) + 3 <= 10) escapeLab.make(EscapeAction.FootprintKeep)
    else escapeLab.make(EscapeAction.FootprintDrop)
})
```

## Continue to Room B: Light Gallery

When this room's passage opens, [continue with Room B: Light Gallery](#recipe:https://github.com/mrbrackebusch-code/escaping-logic/docs/tutorials/escaping-logic-room-b-light-gallery).
