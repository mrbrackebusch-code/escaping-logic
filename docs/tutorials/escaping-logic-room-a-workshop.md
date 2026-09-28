# Escaping Logic — Room A: Workshop

### @explicitHints true

## Room A

This Recipe covers constructions **1–6**. Start with construction 1 below.

## 1. Clear the fire channel

The fixed fire spout blocks the wall route. First build ``||escapeLab(noclick):when [(A) fire spout] is operated||`` with ``||logic(noclick):if then else||``. Test ``||escapeLab(noclick):is [(A) WaterFlowing]||``; make `(A) FireSteam` happen when it is true and `(A) FireFlare` otherwise. Press **A** at the fire spout to operate it; do not hold **B**. Because water is not flowing yet, `(A) FireFlare` briefly catches the explorer's coat while you keep moving. You need both branches because you will return after water reaches this spout; that alternate reaction lights the sealed case reservoir next.

### Find the native Blocks

![Find the native Blocks for Fire](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/195095bc6924706a/media/menu/01-fire-01-fire-menu.svg)

### Build this rule

![Build this rule for Fire](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/195095bc6924706a/media/assembled/01-fire-01-fire-assembled.svg)

### What the mechanism does

![What the mechanism does for Fire](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/195095bc6924706a/media/gameplay/01-fire-connected-v2-physical-v7-01-01-fire.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.Fire, function () {
    if (escapeLab.is(EscapeFact.WaterFlowing)) escapeLab.make(EscapeAction.FireSteam)
    else escapeLab.make(EscapeAction.FireFlare)
})
```

## 2. Open the reservoir case

The case button cannot release its fixed reservoir until power arrives. Press **A** at the case to run your rule; do not hold **B**. In ``||escapeLab(noclick):when [(A) power case] is operated||``, test ``||escapeLab(noclick):is [(A) PowerAvailable]||``. Make `(A) CaseRetract` happen for true and `(A) CaseRattle` happen for else, then press **A** at the case to see its restrained rattle; do not hold **B**. The generator handle is now the uncertain next light. When you return with power, press **A** at the case to run your rule and open it. Pick up the water canister from its tray with **A**, carry it to the fire-spout pad, and press **A** to fit it. Return to the spout and press **A** to run your fire rule. None of these steps uses **B**.

### Build this rule

![Build this rule for Case](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/195095bc6924706a/media/assembled/02-case-02-case-assembled.svg)

### What the mechanism does

![What the mechanism does for Case](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/195095bc6924706a/media/gameplay/02-case-connected-v2-physical-v7-01-02-case.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.Case, function () {
    if (escapeLab.is(EscapeFact.PowerAvailable)) escapeLab.make(EscapeAction.CaseRetract)
    else escapeLab.make(EscapeAction.CaseRattle)
})
```

## 3. Start the generator

The generator's handle turns only with a crank fitted to its rail. Before the crank is fitted, press **A** at the generator to see it stall; do not hold **B**. In ``||escapeLab(noclick):when [(A) generator] is operated||``, test ``||escapeLab(noclick):is [(A) CrankFitted]||``. Make `(A) GeneratorSpin` happen when true and `(A) GeneratorSputter` otherwise. Operate it once before the crank is fitted: the rotor stalls, then the magnet rail at the upper left becomes the next goal. This is another ordinary if/else rule whose successful branch will matter when you come back.

### Build this rule

![Build this rule for Generator](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/195095bc6924706a/media/assembled/03-generator-03-generator-assembled.svg)

### What the mechanism does

![What the mechanism does for Generator](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/195095bc6924706a/media/gameplay/03-generator-connected-v2-physical-v7-01-03-generator.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.Generator, function () {
    if (escapeLab.is(EscapeFact.CrankFitted)) escapeLab.make(EscapeAction.GeneratorSpin)
    else escapeLab.make(EscapeAction.GeneratorSputter)
})
```

## 4. Swing the mounted magnet

The magnet is mounted on a rail; it is not something to collect. In ``||escapeLab(noclick):when [(A) magnet rail] is operated||``, test ``||escapeLab(noclick):is [(A) MagnetTouchingCrank]||``. Make `(A) CrankPull` happen when true and `(A) CrankTwitch` otherwise. Hold **B** on the magnet pad and use **left/right** to choose the labeled near position; press **A** to swing the magnet. The crank appears on its tray when it touches. Release **B** to walk. Pick it up with **A**, carry it to the generator pad, and press **A** to fit it. That same **A** interaction immediately invokes the child's generator handler; the installed crank alone does not grant power unless your code makes `(A) GeneratorSpin` when `CrankFitted` is true. Then press **A** at the case to open it and collect the water canister, fit it at the fire spout with **A**, and press **A** there to run the fire rule. Press **A** at each mechanism; do not open menus with **B**.

### Build this rule

![Build this rule for Crank](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/195095bc6924706a/media/assembled/04-crank-04-crank-assembled.svg)

### What the mechanism does

![What the mechanism does for Crank](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/195095bc6924706a/media/gameplay/04-crank-connected-v2-physical-v7-01-04-crank.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.Crank, function () {
    if (escapeLab.is(EscapeFact.MagnetTouchingCrank)) escapeLab.make(EscapeAction.CrankPull)
    else escapeLab.make(EscapeAction.CrankTwitch)
})
```

## 5. Raise the wall holds

With the fire channel clear, the wall lever recovers the fixed holds. In ``||escapeLab(noclick):when [(A) climb wall] is operated||``, test ``||escapeLab(noclick):value of [(A) InstalledHolds]||`` = `4`; make `(A) WallClimb` happen when it passes and `(A) WallFlash` otherwise. At the wall pad, hold **B** and use **left/right** to select `4 HOLDS`; press **A** to raise them after the steam clears, then release **B**. The holds rise into a climbable route. Press **A** at the footprint stones to run your rule; do not hold **B**. The lit footprints tell you what to test next.

### Find the native Blocks

![Find the native Blocks for Wall](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/195095bc6924706a/media/menu/05-wall-05-wall-comparisons-menu.svg)

### Build this rule

![Build this rule for Wall](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/195095bc6924706a/media/assembled/05-wall-05-wall-assembled.svg)

### What the mechanism does

![What the mechanism does for Wall](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/195095bc6924706a/media/gameplay/05-wall-connected-v2-physical-v7-01-05-wall.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.Wall, function () {
    if (escapeLab.number(EscapeMeter.InstalledHolds) == 4) escapeLab.make(EscapeAction.WallClimb)
    else escapeLab.make(EscapeAction.WallFlash)
})
```

## 6. Choose a safe footprint

The three marked stones show `8`, `7`, and `6`; any value with `+ 3 ≤ 10` is safe. In ``||escapeLab(noclick):when [(A) footprint stones] is operated||``, test ``||escapeLab(noclick):value of [(A) StepValue]|| + 3 ≤ 10``. Make `(A) FootprintKeep` for true and `(A) FootprintDrop` for else. At the footprint pad, hold **B** and use **left/right** to choose the labeled `7` or `6` stone; press **A** to step on it. This choice can work immediately; release **B** to walk. A safe footprint opens the real passage into Room B and lights its shadow screen.

### Build this rule

![Build this rule for Footprints](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/195095bc6924706a/media/assembled/06-footprints-06-footprints-assembled.svg)

### What the mechanism does

![What the mechanism does for Footprints](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/195095bc6924706a/media/gameplay/06-footprints-connected-v2-physical-v7-01-06-footprints.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.Footprints, function () {
    if (escapeLab.number(EscapeMeter.StepValue) + 3 <= 10) escapeLab.make(EscapeAction.FootprintKeep)
    else escapeLab.make(EscapeAction.FootprintDrop)
})
```

## Continue to Room B: Light Gallery

When this room's passage opens, [continue with Room B: Light Gallery](#recipe:https://github.com/mrbrackebusch-code/escaping-logic/docs/tutorials/escaping-logic-room-b-light-gallery).
