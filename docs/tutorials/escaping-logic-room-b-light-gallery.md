# Escaping Logic — Room B: Light Gallery

### @explicitHints true

## Room B

This Recipe covers constructions **7–16**. If this room is not open in the game yet, [finish Room A: Workshop first](#recipe:https://github.com/mrbrackebusch-code/escaping-logic/docs/tutorials/escaping-logic-room-a-workshop).

## 7. Reveal the shadow route

The shadow screen needs an illumination of `60`, but the beam is still weak. It is a direct mechanism: press **A** at its pad to run your rule; do not hold **B**. In ``||escapeLab(noclick):when [(B) shadow screen] is operated||``, test ``||escapeLab(noclick):value of [(B) Illumination]|| ≥ 60``. Make `(B) ShadowReveal` when true and `(B) ShadowHide` otherwise. Press **A** to see the dim screen remain closed; do not hold **B**. The telescope is now lit because it is the missing source of light.

### Build this rule

![Build this rule for Shadow](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/195095bc6924706a/media/assembled/07-shadow-07-shadow-assembled.svg)

### What the mechanism does

![What the mechanism does for Shadow](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/195095bc6924706a/media/gameplay/07-shadow-connected-v2-physical-v7-01-07-shadow.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.Shadow, function () {
    if (escapeLab.number(EscapeMeter.Illumination) >= 60) escapeLab.make(EscapeAction.ShadowReveal)
    else escapeLab.make(EscapeAction.ShadowHide)
})
```

## 8. Focus the telescope

The telescope needs zoom `3`, though its lens has not yet seated. In ``||escapeLab(noclick):when [(B) telescope] is operated||``, test ``||escapeLab(noclick):value of [(B) Zoom]|| ≥ 3``. Make `(B) TelescopeFocus` for true and `(B) TelescopeBlur` otherwise. At the telescope pad, hold **B** and use **left/right** to choose the labeled zoom `3`; press **A** to focus, then release **B**. Its beam points to the matching-stone socket. After seating the lens stone, return to the telescope and use this same B + left/right choice before pressing **A**; then use **A** at the shadow screen. The stone is a physical choice you can solve on the first try.

### What the mechanism does

![What the mechanism does for Telescope](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/195095bc6924706a/media/gameplay/08-telescope-connected-v2-physical-v7-01-08-telescope.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.Telescope, function () {
    if (escapeLab.number(EscapeMeter.Zoom) >= 3) escapeLab.make(EscapeAction.TelescopeFocus)
    else escapeLab.make(EscapeAction.TelescopeBlur)
})
```

## 9. Seat the matching lens stone

Compare ``||escapeLab(noclick):value of [(B) StoneColor]||`` with ``||escapeLab(noclick):value of [(B) SocketColor]||``. In ``||escapeLab(noclick):when [(B) stone sockets] is operated||``, make `(B) StoneSnap` when they are equal and `(B) StoneRepel` otherwise. Hold **B** at the socket pad and use **left/right** to choose the stone whose color matches the socket label; press **A** to seat the choice. A lens stone appears on its tray; release **B** to walk. Pick it up, carry it to the telescope pad, and fit it with **A**. Return to the telescope, hold **B**, use **left/right** to choose zoom `3`, press **A** to focus, then release **B**. Press **A** at the shadow screen to run its rule; do not hold **B** there.

### What the mechanism does

![What the mechanism does for Stones](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/195095bc6924706a/media/gameplay/09-stones-connected-v2-physical-v7-01-09-stones.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.Stones, function () {
    if (escapeLab.number(EscapeMeter.StoneColor) == escapeLab.number(EscapeMeter.SocketColor)) escapeLab.make(EscapeAction.StoneSnap)
    else escapeLab.make(EscapeAction.StoneRepel)
})
```

## 10. Mix the mural lights

The mural needs yellow and blue light, but its color-filter slot is empty. In ``||escapeLab(noclick):when [(B) mural colors] is operated||``, join ``||escapeLab(noclick):is [(B) YellowOn]||`` and ``||escapeLab(noclick):is [(B) BlueOn]||`` with ``||logic(noclick):and||``. Make `(B) MuralBlend` when both pass and `(B) MuralDim` otherwise. **And** needs both conditions, so its dim result points to the frozen portrait rails that will supply the filters.

### Find the native Blocks

![Find the native Blocks for MuralMix](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/195095bc6924706a/media/menu/10-mural-mix-10-mural-logic-menu.svg)

### Build this rule

![Build this rule for MuralMix](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/195095bc6924706a/media/assembled/10-mural-mix-10-mural-mix-assembled.svg)

### What the mechanism does

![What the mechanism does for MuralMix](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/195095bc6924706a/media/gameplay/10-mural-mix-connected-v2-physical-v7-01-10-mural-mix.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.MuralMix, function () {
    if (escapeLab.is(EscapeFact.YellowOn) && escapeLab.is(EscapeFact.BlueOn)) escapeLab.make(EscapeAction.MuralBlend)
    else escapeLab.make(EscapeAction.MuralDim)
})
```

## 11. Open the mural compartment

Build the mural's second rule before its light sources are ready. In ``||escapeLab(noclick):when [(B) mural latch] is operated||``, keep yellow **and** blue and add ``||logic(noclick):not||`` ``||escapeLab(noclick):is [(B) RedOn]||``. Make `(B) MuralOpen` when all three requirements pass; otherwise make `(B) MuralSpill` happen. **Not** expresses the false case: red must be off. The first portrait plate is lit next, but its pad still needs a thawed weight.

### Build this rule

![Build this rule for MuralReveal](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/195095bc6924706a/media/assembled/11-mural-reveal-11-mural-reveal-assembled.svg)

### What the mechanism does

![What the mechanism does for MuralReveal](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/195095bc6924706a/media/gameplay/11-mural-reveal-connected-v2-physical-v7-01-11-mural-reveal.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.MuralReveal, function () {
    if (escapeLab.is(EscapeFact.YellowOn) && escapeLab.is(EscapeFact.BlueOn) && !escapeLab.is(EscapeFact.RedOn)) escapeLab.make(EscapeAction.MuralOpen)
    else escapeLab.make(EscapeAction.MuralSpill)
})
```

## 12. Move portrait one

At the first footprint pressure plate, `1` means left and `2` means right. In ``||escapeLab(noclick):when [(B) first portrait] is operated||``, test ``||escapeLab(noclick):value of [(B) ShoeSide]|| = 1``; make `(B) PortraitLeft` when true and `(B) PortraitRight` otherwise. Press **A** at the portrait pad to run the rule; its plate automatically selects the next unfinished/current portrait route stage. The rail cannot move until its pad has a thawed weight, so this first interaction shows that physical limit. The warm bath is the next lit mechanism. Keep this complete stack ready for the weight.

### What the mechanism does

![What the mechanism does for Portrait1](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/195095bc6924706a/media/gameplay/12-portrait1-connected-v2-physical-v7-01-12-portrait1.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.Portrait1, function () {
    if (escapeLab.number(EscapeMeter.ShoeSide) == 1) escapeLab.make(EscapeAction.PortraitLeft)
    else escapeLab.make(EscapeAction.PortraitRight)
})
```

## 13. Thaw the portrait rails

The bath has cold, warm, and overheated responses. Use the **+** on ``||logic(noclick):if then else||`` to add ``||logic(noclick):else if||`` after a first test is false. In ``||escapeLab(noclick):when [(B) warming bath] is operated||``, make `(B) ThermalBlue` if `(B) Temperature < 20`; make `(B) ThermalRed` in an else-if when `(B) Temperature > 40`; otherwise make `(B) ThermalAmber`. This final else covers `20` through `40`. At the bath pad, hold **B** and use **left/right** to select the labeled temperature `20` or `40`; press **A** to heat the bath. A thawed weight appears on the tray. Carry and fit it, then press **A** at each portrait pad; each interaction advances to the next unfinished portrait automatically, with no up/down selection. Carry it to the first portrait pad and fit it with **A**, then press **A** at portrait one to run your written rule. The portrait mechanism automatically advances to the next unfinished/current portrait stage; use the indicated LEFT/RIGHT footprint plate, never up/down to select a part.

### Find the native Blocks

![Find the native Blocks for Thermal](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/195095bc6924706a/media/menu/13-thermal-13-thermal-elseif-menu.svg)

### Build this rule

![Build this rule for Thermal](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/195095bc6924706a/media/assembled/13-thermal-13-thermal-assembled.svg)

### What the mechanism does

![What the mechanism does for Thermal](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/195095bc6924706a/media/gameplay/13-thermal-connected-v2-physical-v7-01-13-thermal.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.Thermal, function () {
    if (escapeLab.number(EscapeMeter.Temperature) < 20) escapeLab.make(EscapeAction.ThermalBlue)
    else if (escapeLab.number(EscapeMeter.Temperature) > 40) escapeLab.make(EscapeAction.ThermalRed)
    else escapeLab.make(EscapeAction.ThermalAmber)
})
```

## 14. Move portrait two

Make a separate ``||escapeLab(noclick):when [(B) second portrait] is operated||`` event with the same `(B) ShoeSide = 1` test, `(B) PortraitLeft` true action, and `(B) PortraitRight` else action. A separate stack gives this rail its own rule. The warm bath has thawed it. Press **A** at this portrait pad; it automatically selects the next unfinished portrait stage, and the left pressure plate moves it.

### What the mechanism does

![What the mechanism does for Portrait2](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/195095bc6924706a/media/gameplay/14-portrait2-connected-v2-physical-v7-01-14-portrait2.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.Portrait2, function () {
    if (escapeLab.number(EscapeMeter.ShoeSide) == 1) escapeLab.make(EscapeAction.PortraitLeft)
    else escapeLab.make(EscapeAction.PortraitRight)
})
```

## 15. Move portrait three

Repeat the portrait rule in a ``||escapeLab(noclick):when [(B) third portrait] is operated||`` event: test `value of (B) ShoeSide = 1`, make `(B) PortraitLeft` for true, and `(B) PortraitRight` for else. This third rail responds to the same physical clue. Press **A** at this portrait pad to advance automatically to the next unfinished portrait; use its left pressure plate to align it.

### What the mechanism does

![What the mechanism does for Portrait3](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/195095bc6924706a/media/gameplay/15-portrait3-connected-v2-physical-v7-01-15-portrait3.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.Portrait3, function () {
    if (escapeLab.number(EscapeMeter.ShoeSide) == 1) escapeLab.make(EscapeAction.PortraitLeft)
    else escapeLab.make(EscapeAction.PortraitRight)
})
```

## 16. Move portrait four

Add the final matching stack in ``||escapeLab(noclick):when [(B) fourth portrait] is operated||``. Use the same left/right condition and actions. Press **A** at this portrait pad to advance automatically to the current final portrait stage, then move it left. When all four align, color filters appear on the first portrait's tray. Carry them to the mural-colors pad and fit them, then return to the mural mix and reveal and operate those two rules to open the second exit half.

### What the mechanism does

![What the mechanism does for Portrait4](https://raw.githubusercontent.com/mrbrackebusch-code/escaping-logic/main/assets/195095bc6924706a/media/gameplay/16-portrait4-connected-v2-physical-v7-01-16-portrait4.gif)

#### ~ tutorialhint

```blocks
escapeLab.onAttempt(EscapeBeat.Portrait4, function () {
    if (escapeLab.number(EscapeMeter.ShoeSide) == 1) escapeLab.make(EscapeAction.PortraitLeft)
    else escapeLab.make(EscapeAction.PortraitRight)
})
```

## Continue to Room C: Garden Room

When this room's passage opens, [continue with Room C: Garden Room](#recipe:https://github.com/mrbrackebusch-code/escaping-logic/docs/tutorials/escaping-logic-room-c-garden-room).
