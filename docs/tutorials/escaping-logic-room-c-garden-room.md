# Escaping Logic — Room C: Garden Room

### @explicitHints true

## Room C

This Recipe covers constructions **17–22**. If this room is not open in the game yet, [finish Room B: Light Gallery first](#recipe:https://github.com/mrbrackebusch-code/escaping-logic/docs/tutorials/escaping-logic-room-b-light-gallery).

## 17. Test the magnetic sample

The sample needs a live magnet, but its coil has no allowed wire yet. In ``||escapeLab(noclick):when [(C) magnet sample] is operated||``, join ``||escapeLab(noclick):is [(C) Metallic]||`` and ``||escapeLab(noclick):is [(C) MagnetOn]||`` with **and**. Make `(C) SampleSpike` when both pass and `(C) SampleFlat` otherwise. Its flat reaction lights the wire rack, which is a choice puzzle with an immediate usable answer.

### What the mechanism does

![What the mechanism does for Sample](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/5da2db9300536c5c/media/gameplay/17-sample-connected-v2-physical-v6-01-17-sample.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.Sample, function () {
    if (escapeLab.is(EscapeFact.Metallic) && escapeLab.is(EscapeFact.MagnetOn)) escapeLab.make(EscapeAction.SampleSpike)
    else escapeLab.make(EscapeAction.SampleFlat)
})
```

## 18. Install an allowed wire

At the coil, purple, red, and black are allowed. Join the three `value of (C) WireColor =` comparisons with ``||logic(noclick):or||`` in ``||escapeLab(noclick):when [(C) wire sorter] is operated||``. Make `(C) WireInstall` when one comparison passes and `(C) WireEject` otherwise. **Or** accepts at least one usable condition; choose an allowed wire. A coil connector appears on the wire-sorter tray. Carry it to the magnet-sample pad, fit it, then return to the sample and operate its rule to raise the first Room C exit catch.

### Find the native Blocks

![Find the native Blocks for Wires](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/5da2db9300536c5c/media/menu/18-wires-18-wires-or-menu.svg)

### Build this rule

![Build this rule for Wires](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/5da2db9300536c5c/media/assembled/18-wires-18-wires-assembled.svg)

### What the mechanism does

![What the mechanism does for Wires](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/5da2db9300536c5c/media/gameplay/18-wires-connected-v2-physical-v6-01-18-wires.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.Wires, function () {
    if (escapeLab.number(EscapeMeter.WireColor) == 1 || escapeLab.number(EscapeMeter.WireColor) == 2 || escapeLab.number(EscapeMeter.WireColor) == 3) escapeLab.make(EscapeAction.WireInstall)
    else escapeLab.make(EscapeAction.WireEject)
})
```

## 19. Reveal the heat vessel

The vessel needs a repair patch before it can seal, so it can only leak now. In ``||escapeLab(noclick):when [(C) heat vessel] is operated||``, first test `is (C) VesselRepaired` **and** `is (C) VesselHot` and make `(C) VesselReveal`. Add an else-if for `is (C) VesselRepaired` that makes `(C) VesselBlank`; make `(C) VesselLeak` in the final else. Put the specific repaired-and-hot case first. The leak lights the plant pruner that can make the patch.

### What the mechanism does

![What the mechanism does for Vessel](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/5da2db9300536c5c/media/gameplay/19-vessel-connected-v2-physical-v6-01-19-vessel.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.Vessel, function () {
    if (escapeLab.is(EscapeFact.VesselRepaired) && escapeLab.is(EscapeFact.VesselHot)) escapeLab.make(EscapeAction.VesselReveal)
    else if (escapeLab.is(EscapeFact.VesselRepaired)) escapeLab.make(EscapeAction.VesselBlank)
    else escapeLab.make(EscapeAction.VesselLeak)
})
```

## 20. Free the repair lever

In ``||escapeLab(noclick):when [(C) pruning lever] is operated||``, test ``||escapeLab(noclick):value of [(C) LeafPoints]|| > 3``. Make `(C) LeafClip` happen for true and `(C) LeafKeep` otherwise. Choose a four-point leaf: a repair patch appears on the pruning-lever tray. Carry it to the heat-vessel pad and fit it. Then use the vessel's machine view to heat it and operate your three-way rule; the sealed hot vessel reveals the second exit catch.

### What the mechanism does

![What the mechanism does for Pruner](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/5da2db9300536c5c/media/gameplay/20-pruner-connected-v2-physical-v6-01-20-pruner.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.Pruner, function () {
    if (escapeLab.number(EscapeMeter.LeafPoints) > 3) escapeLab.make(EscapeAction.LeafClip)
    else escapeLab.make(EscapeAction.LeafKeep)
})
```

## 21. Test the titration target

The dropper cannot provide its target amount until the balance releases it. Still build the result rule in ``||escapeLab(noclick):when [(C) titration] is operated||``: if `(C) Drops < 7`, make `(C) TitrationClear`; else if `(C) Drops ≤ 9`, make `(C) TitrationBloom`; otherwise make `(C) TitrationOverflow`. Its low result lights the balance. The target bloom will be your payoff after the dropper can select `7` or `9`.

### What the mechanism does

![What the mechanism does for Titration](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/5da2db9300536c5c/media/gameplay/21-titration-connected-v2-physical-v6-01-21-titration.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.Titration, function () {
    if (escapeLab.number(EscapeMeter.Drops) < 7) escapeLab.make(EscapeAction.TitrationClear)
    else if (escapeLab.number(EscapeMeter.Drops) <= 9) escapeLab.make(EscapeAction.TitrationBloom)
    else escapeLab.make(EscapeAction.TitrationOverflow)
})
```

## 22. Balance the dropper

In ``||escapeLab(noclick):when [(C) balance scale] is operated||``, test `value of (C) LeftWeight = value of (C) RightWeight` and make `(C) ScaleLevel`. Add an else-if for left greater than right that makes `(C) ScaleLeft`; make `(C) ScaleRight` in the final else. Choose equal weights first: a measured dropper appears on the balance tray. Carry it to the titration pad and fit it. Return to titration, choose `7` or `9`, and operate your rule to see the bloom raise the third catch.

### What the mechanism does

![What the mechanism does for Balance](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/5da2db9300536c5c/media/gameplay/22-balance-connected-v2-physical-v6-01-22-balance.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.Balance, function () {
    if (escapeLab.number(EscapeMeter.LeftWeight) == escapeLab.number(EscapeMeter.RightWeight)) escapeLab.make(EscapeAction.ScaleLevel)
    else if (escapeLab.number(EscapeMeter.LeftWeight) > escapeLab.number(EscapeMeter.RightWeight)) escapeLab.make(EscapeAction.ScaleLeft)
    else escapeLab.make(EscapeAction.ScaleRight)
})
```

## Continue to Room D: Bridge Room

When this room's passage opens, [continue with Room D: Bridge Room](#recipe:https://github.com/mrbrackebusch-code/escaping-logic/docs/tutorials/escaping-logic-room-d-bridge-room).
