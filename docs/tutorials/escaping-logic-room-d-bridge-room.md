# Escaping Logic — Room D: Bridge Room

### @explicitHints true

## Room D

This Recipe covers constructions **23–30**. If this room is not open in the game yet, [finish Room C: Garden Room first](#recipe:https://github.com/mrbrackebusch-code/escaping-logic/docs/tutorials/escaping-logic-room-c-garden-room).

## 23. Launch the pneumatic capsule

The selector needs a message strip, so the empty tube drains at first. In ``||escapeLab(noclick):when [(D) pneumatic tube] is operated||``, join ``||escapeLab(noclick):is [(D) RouteA]||`` and ``||escapeLab(noclick):is [(D) RouteB]||`` with **or**. Make `(D) TubeLaunch` for true and `(D) TubeDrain` otherwise. The drain lights the printer, where the strip can be made.

### What the mechanism does

![What the mechanism does for Tube](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/5da2db9300536c5c/media/gameplay/23-tube-connected-v2-physical-v6-01-23-tube.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.Tube, function () {
    if (escapeLab.is(EscapeFact.RouteA) || escapeLab.is(EscapeFact.RouteB)) escapeLab.make(EscapeAction.TubeLaunch)
    else escapeLab.make(EscapeAction.TubeDrain)
})
```

## 24. Feed the message printer

The printer works through clear radio or a connected cable, neither of which is ready yet. In ``||escapeLab(noclick):when [(D) message printer] is operated||``, join `is (D) RadioClear` and `is (D) CableConnected` with **or**. Make `(D) PrinterFeed` when either route works and `(D) PrinterJam` otherwise. The jam points to the noise mixer; its channels cannot all be quiet until a receiver makes a signal. When the printer later feeds, a message strip appears on its tray. Carry it to the tube pad, fit it, and operate the tube rule.

### What the mechanism does

![What the mechanism does for Printer](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/5da2db9300536c5c/media/gameplay/24-printer-connected-v2-physical-v6-01-24-printer.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.Printer, function () {
    if (escapeLab.is(EscapeFact.RadioClear) || escapeLab.is(EscapeFact.CableConnected)) escapeLab.make(EscapeAction.PrinterFeed)
    else escapeLab.make(EscapeAction.PrinterJam)
})
```

## 25. Clear the interference mixer

In ``||escapeLab(noclick):when [(D) noise mixer] is operated||``, join `not is (D) ScratchOn`, `not is (D) BeepOn`, and `not is (D) HumOn` with **and**. Make `(D) NoiseClear` when every channel is off, or `(D) NoiseDistort` otherwise. The mixer needs a signal module, so its distorted result points to the receiver. After fitting that module, return through mixer, printer, and tube to send the capsule to the exit latch.

### What the mechanism does

![What the mechanism does for Interference](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/5da2db9300536c5c/media/gameplay/25-interference-connected-v2-physical-v6-01-25-interference.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.Interference, function () {
    if (!escapeLab.is(EscapeFact.ScratchOn) && !escapeLab.is(EscapeFact.BeepOn) && !escapeLab.is(EscapeFact.HumOn)) escapeLab.make(EscapeAction.NoiseClear)
    else escapeLab.make(EscapeAction.NoiseDistort)
})
```

## 26. Tune the pedal receiver

Use a three-way ``||escapeLab(noclick):when [(D) pedal receiver] is operated||`` rule: make `(D) ReceiverClear` if `(D) RPM ≥ 80`; else if `(D) RPM ≥ 40`, make `(D) ReceiverStatic`; otherwise make `(D) ReceiverDead`. Choose `80 RPM`: a signal module appears on the receiver tray. Carry it to the noise-mixer pad, fit it, then return to the mixer and operate its rule. The forward chain now has a physical path all the way to the capsule.

### What the mechanism does

![What the mechanism does for Receiver](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/5da2db9300536c5c/media/gameplay/26-receiver-connected-v2-physical-v6-01-26-receiver.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.Receiver, function () {
    if (escapeLab.number(EscapeMeter.RPM) >= 80) escapeLab.make(EscapeAction.ReceiverClear)
    else if (escapeLab.number(EscapeMeter.RPM) >= 40) escapeLab.make(EscapeAction.ReceiverStatic)
    else escapeLab.make(EscapeAction.ReceiverDead)
})
```

## 27. Stabilize the pressure seal

Make a native ``||variables(noclick):Variables||`` variable named ``||variables(noclick):pressureReady||``: it remembers whether this local preparation succeeded. In ``||loops(noclick):on start||``, set it to ``||escapeLab(noclick):is [(D) PressureReady]||`` so an earned seal checkpoint can return after reload. In ``||escapeLab(noclick):when [(D) pressure stabilizer] is operated||``, test `value of (D) PressureTenths ≥ 48` **and** `value of (D) PressureTenths ≤ 50`; set `pressureReady` to `true` and make `(D) SealStable` when true, otherwise set it to `false` and make `(D) SealLeak`. Choose `48` or `50`; the stable seal makes the release control usable.

### Find the native Blocks

![Find the native Blocks for PressureStable](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/5da2db9300536c5c/media/menu/27-pressure-stable-27-pressure-and-pitch-variables-menu.svg)

### Build this rule

![Build this rule for PressureStable](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/5da2db9300536c5c/media/assembled/27-pressure-stable-27-pressure-stable-assembled.svg)

### What the mechanism does

![What the mechanism does for PressureStable](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/5da2db9300536c5c/media/gameplay/27-pressure-stable-connected-v2-physical-v6-01-27-pressure-stable.gif)

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

In ``||escapeLab(noclick):when [(D) pressure release] is operated||``, join your `pressureReady` variable with `value of (D) PressureTenths = 20`. Make `(D) SealRetract` when both pass and `(D) SealVent` otherwise. After the whole if/else, set `pressureReady` to `false`: every release attempt consumes this preparation. Stabilize first, then choose `20`; the hydraulic lift raises and lights the pitch controls.

### What the mechanism does

![What the mechanism does for PressureRelease](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/5da2db9300536c5c/media/gameplay/28-pressure-release-connected-v2-physical-v6-01-28-pressure-release.gif)

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

Make a native ``||variables(noclick):Variables||`` variable named ``||variables(noclick):angle||``. In ``||loops(noclick):on start||``, set it to ``||escapeLab(noclick):value of [(D) PitchAngle]||``. In ``||escapeLab(noclick):when [(D) pitch control] is operated||``, change `angle` by `value of (D) PitchChange`, then pass `angle` to ``||escapeLab(noclick):set room pitch to [number]||``. The physical controls provide `+10`, `+25`, `-10`, and `-25`; your variable accumulates them. Bring the gauge to `0`, then use the feedback station.

### Build this rule

![Build this rule for PitchAdjust](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/5da2db9300536c5c/media/assembled/29-pitch-adjust-29-pitch-adjust-assembled.svg)

### What the mechanism does

![What the mechanism does for PitchAdjust](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/5da2db9300536c5c/media/gameplay/29-pitch-adjust-connected-v2-physical-v6-01-29-pitch-adjust.gif)

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

In ``||escapeLab(noclick):when [(D) pitch display] is operated||``, test your `angle`. Make `(D) PitchLevel` if `angle = 0`; else if `angle < 0`, make `(D) PitchDown`; otherwise make `(D) PitchUp`. Try the negative and positive responses through local control retests if you want to inspect them. Level is the forward result: the bridge settles and opens Room E.

### What the mechanism does

![What the mechanism does for PitchFeedback](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/5da2db9300536c5c/media/gameplay/30-pitch-feedback-connected-v2-physical-v6-01-30-pitch-feedback.gif)

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

## Continue to Room E: Last Door

When this room's passage opens, [continue with Room E: Last Door](#recipe:https://github.com/mrbrackebusch-code/escaping-logic/docs/tutorials/escaping-logic-room-e-last-door).
