# Escaping Logic — Setup and room selector

### @explicitHints true

## Welcome to the escape rooms

These five connected escape rooms react only to rules you write. The room prefix in a dropdown, from `(A)` through `(E)`, tells you where that mechanism belongs. Walk with the arrow keys. Press **A** at a tray to pick up its one visible part, at the matching machine pad to fit it, or at a machine to run its installed rule. Hold **B** while standing on a marked machine pad to open its machine view: **left/right** change a setting, **up/down** choose a multipart stage, and **A** runs the rule. Release **B** to walk right away. Carry one part at a time; trying to put it down elsewhere sends it back to its tray. In MakeCode Arcade, **Z** or **Space** is **A**, and **X** is **B**. Use the simulator's fullscreen button when testing so you can see the room clearly. A solved mechanism stays in the room, so you can return and test a changed rule locally. Your progress is saved as you go; follow the next gold light to see what needs your attention.

Each construction begins with ``||escapeLab(noclick):when [mechanism] is operated||``. The event supplies the moment; your native ``||logic(noclick):if then else||`` decides the response. The room does not supply a missing decision. A dim object is a future possibility, and the lit object is the one whose next reaction matters now.

## Start here

This setup makes your Escaping Logic project. After it opens, start with Room A. At the end of each room, use the link to continue to the next room.

## Start Room A: Workshop

[Open Room A: Workshop](#recipe:https://github.com/mrbrackebusch-code/escaping-logic/docs/tutorials/escaping-logic-room-a-workshop). Room A contains constructions **1–6**.

## Room selector

After setup, you can use these links to open any room you have reached. If a room is not available in the game yet, finish the previous room first.

- [Room A — Workshop, steps 1–6](#recipe:https://github.com/mrbrackebusch-code/escaping-logic/docs/tutorials/escaping-logic-room-a-workshop)
- [Room B — Light Gallery, steps 7–16](#recipe:https://github.com/mrbrackebusch-code/escaping-logic/docs/tutorials/escaping-logic-room-b-light-gallery)
- [Room C — Garden Room, steps 17–22](#recipe:https://github.com/mrbrackebusch-code/escaping-logic/docs/tutorials/escaping-logic-room-c-garden-room)
- [Room D — Bridge Room, steps 23–30](#recipe:https://github.com/mrbrackebusch-code/escaping-logic/docs/tutorials/escaping-logic-room-d-bridge-room)
- [Room E — Last Door, steps 31–36](#recipe:https://github.com/mrbrackebusch-code/escaping-logic/docs/tutorials/escaping-logic-room-e-last-door)

## Room-opening help

If you are coming back later, open your existing `logic-escape-room` project from MakeCode Home first, then open the room Recipe you want.

If a room Recipe opens in a blank or new project, exit the Recipe, return to MakeCode Home, reopen your existing `logic-escape-room` project, and then open the room Recipe again. If you do not have a `logic-escape-room` project yet, use this setup first.

```template
// Logic Escape Room
```

```customts
// The learner-facing nouns. Decisions belong in native if / else blocks.
enum EscapeBeat {
    // Room A
    //% block="(A) climb wall"
    Wall = 4,
    //% block="(A) fire spout"
    Fire = 3,
    //% block="(A) footprint stones"
    Footprints = 5,
    //% block="(A) generator"
    Generator = 1,
    //% block="(A) magnet rail"
    Crank = 0,
    //% block="(A) power case"
    Case = 2,
    // Room B
    //% block="(B) first portrait"
    Portrait1 = 7,
    //% block="(B) fourth portrait"
    Portrait4 = 10,
    //% block="(B) mural colors"
    MuralMix = 11,
    //% block="(B) mural latch"
    MuralReveal = 12,
    //% block="(B) second portrait"
    Portrait2 = 8,
    //% block="(B) shadow screen"
    Shadow = 6,
    //% block="(B) stone sockets"
    Stones = 13,
    //% block="(B) telescope"
    Telescope = 14,
    //% block="(B) third portrait"
    Portrait3 = 9,
    //% block="(B) warming bath"
    Thermal = 15,
    // Room C
    //% block="(C) balance scale"
    Balance = 18,
    //% block="(C) heat vessel"
    Vessel = 21,
    //% block="(C) magnet sample"
    Sample = 16,
    //% block="(C) pruning lever"
    Pruner = 20,
    //% block="(C) titration"
    Titration = 17,
    //% block="(C) wire sorter"
    Wires = 19,
    // Room D
    //% block="(D) message printer"
    Printer = 24,
    //% block="(D) noise mixer"
    Interference = 23,
    //% block="(D) pedal receiver"
    Receiver = 22,
    //% block="(D) pitch control"
    PitchAdjust = 28,
    //% block="(D) pitch display"
    PitchFeedback = 29,
    //% block="(D) pneumatic tube"
    Tube = 25,
    //% block="(D) pressure release"
    PressureRelease = 27,
    //% block="(D) pressure stabilizer"
    PressureStable = 26,
    // Room E
    //% block="(E) constellation"
    Constellation = 32,
    //% block="(E) final lever"
    FinalLever = 35,
    //% block="(E) rock path"
    RockPath = 33,
    //% block="(E) sensor map"
    Sensors = 30,
    //% block="(E) shutter bank"
    Shutters = 31,
    //% block="(E) synchronizer"
    Synchronize = 34
}

enum EscapeItem { LargeMagnet, HandCrank, WaterCanister }

enum EscapeFact {
    // Room A
    //% block="(A) CrankFitted"
    CrankFitted = 29,
    //% block="(A) LockFree"
    LockFree = 0,
    //% block="(A) MagnetTouchingCrank"
    MagnetTouchingCrank = 28,
    //% block="(A) PowerAvailable"
    PowerAvailable = 30,
    //% block="(A) WaterFlowing"
    WaterFlowing = 31,
    // Room B
    //% block="(B) BlueOn"
    BlueOn = 2,
    //% block="(B) RedOn"
    RedOn = 3,
    //% block="(B) YellowOn"
    YellowOn = 1,
    // Room C
    //% block="(C) MagnetOn"
    MagnetOn = 5,
    //% block="(C) Metallic"
    Metallic = 4,
    //% block="(C) VesselHot"
    VesselHot = 7,
    //% block="(C) VesselRepaired"
    VesselRepaired = 6,
    // Room D
    //% block="(D) BeepOn"
    BeepOn = 9,
    //% block="(D) CableConnected"
    CableConnected = 12,
    //% block="(D) HumOn"
    HumOn = 10,
    //% block="(D) PressureReady"
    PressureReady = 15,
    //% block="(D) RadioClear"
    RadioClear = 11,
    //% block="(D) RouteA"
    RouteA = 13,
    //% block="(D) RouteB"
    RouteB = 14,
    //% block="(D) ScratchOn"
    ScratchOn = 8,
    // Room E
    //% block="(E) AlarmOn"
    AlarmOn = 27,
    //% block="(E) BackMatch"
    BackMatch = 21,
    //% block="(E) DangerousControl"
    DangerousControl = 18,
    //% block="(E) FrontMatch"
    FrontMatch = 19,
    //% block="(E) MiddleMatch"
    MiddleMatch = 20,
    //% block="(E) PowerReady"
    PowerReady = 24,
    //% block="(E) PressureSystemReady"
    PressureSystemReady = 25,
    //% block="(E) SameColor"
    SameColor = 22,
    //% block="(E) SamePattern"
    SamePattern = 23,
    //% block="(E) SignalReady"
    SignalReady = 26,
    //% block="(E) WindowA"
    WindowA = 16,
    //% block="(E) WindowB"
    WindowB = 17
}

enum EscapeMeter {
    // Room A
    //% block="(A) InstalledHolds"
    InstalledHolds = 0,
    //% block="(A) StepValue"
    StepValue = 1,
    // Room B
    //% block="(B) Illumination"
    Illumination = 2,
    //% block="(B) ShoeSide"
    ShoeSide = 3,
    //% block="(B) SocketColor"
    SocketColor = 5,
    //% block="(B) StoneColor"
    StoneColor = 4,
    //% block="(B) Temperature"
    Temperature = 7,
    //% block="(B) Zoom"
    Zoom = 6,
    // Room C
    //% block="(C) Drops"
    Drops = 8,
    //% block="(C) LeafPoints"
    LeafPoints = 12,
    //% block="(C) LeftWeight"
    LeftWeight = 9,
    //% block="(C) RightWeight"
    RightWeight = 10,
    //% block="(C) WireColor"
    WireColor = 11,
    // Room D
    //% block="(D) PitchAngle"
    PitchAngle = 16,
    //% block="(D) PitchChange"
    PitchChange = 15,
    //% block="(D) PressureTenths"
    PressureTenths = 14,
    //% block="(D) RPM"
    RPM = 13,
    // Room E
    //% block="(E) CoreLights"
    CoreLights = 18,
    //% block="(E) SensorNumber"
    SensorNumber = 17
}

enum EscapeAction {
    // Room A
    //% block="(A) CaseRattle"
    CaseRattle = 5,
    //% block="(A) CaseRetract"
    CaseRetract = 4,
    //% block="(A) CrankPull"
    CrankPull = 0,
    //% block="(A) CrankTwitch"
    CrankTwitch = 1,
    //% block="(A) FireFlare"
    FireFlare = 7,
    //% block="(A) FireSteam"
    FireSteam = 6,
    //% block="(A) FootprintDrop"
    FootprintDrop = 11,
    //% block="(A) FootprintKeep"
    FootprintKeep = 10,
    //% block="(A) GeneratorSpin"
    GeneratorSpin = 2,
    //% block="(A) GeneratorSputter"
    GeneratorSputter = 3,
    //% block="(A) WallClimb"
    WallClimb = 8,
    //% block="(A) WallFlash"
    WallFlash = 9,
    // Room B
    //% block="(B) MuralBlend"
    MuralBlend = 16,
    //% block="(B) MuralDim"
    MuralDim = 17,
    //% block="(B) MuralOpen"
    MuralOpen = 18,
    //% block="(B) MuralSpill"
    MuralSpill = 19,
    //% block="(B) PortraitLeft"
    PortraitLeft = 14,
    //% block="(B) PortraitRight"
    PortraitRight = 15,
    //% block="(B) ShadowHide"
    ShadowHide = 13,
    //% block="(B) ShadowReveal"
    ShadowReveal = 12,
    //% block="(B) StoneRepel"
    StoneRepel = 21,
    //% block="(B) StoneSnap"
    StoneSnap = 20,
    //% block="(B) TelescopeBlur"
    TelescopeBlur = 23,
    //% block="(B) TelescopeFocus"
    TelescopeFocus = 22,
    //% block="(B) ThermalAmber"
    ThermalAmber = 25,
    //% block="(B) ThermalBlue"
    ThermalBlue = 24,
    //% block="(B) ThermalRed"
    ThermalRed = 26,
    // Room C
    //% block="(C) LeafClip"
    LeafClip = 37,
    //% block="(C) LeafKeep"
    LeafKeep = 38,
    //% block="(C) SampleFlat"
    SampleFlat = 28,
    //% block="(C) SampleSpike"
    SampleSpike = 27,
    //% block="(C) ScaleLeft"
    ScaleLeft = 33,
    //% block="(C) ScaleLevel"
    ScaleLevel = 32,
    //% block="(C) ScaleRight"
    ScaleRight = 34,
    //% block="(C) TitrationBloom"
    TitrationBloom = 30,
    //% block="(C) TitrationClear"
    TitrationClear = 29,
    //% block="(C) TitrationOverflow"
    TitrationOverflow = 31,
    //% block="(C) VesselBlank"
    VesselBlank = 40,
    //% block="(C) VesselLeak"
    VesselLeak = 41,
    //% block="(C) VesselReveal"
    VesselReveal = 39,
    //% block="(C) WireEject"
    WireEject = 36,
    //% block="(C) WireInstall"
    WireInstall = 35,
    // Room D
    //% block="(D) NoiseClear"
    NoiseClear = 45,
    //% block="(D) NoiseDistort"
    NoiseDistort = 46,
    //% block="(D) PitchDown"
    PitchDown = 56,
    //% block="(D) PitchLevel"
    PitchLevel = 55,
    //% block="(D) PitchUp"
    PitchUp = 57,
    //% block="(D) PrinterFeed"
    PrinterFeed = 47,
    //% block="(D) PrinterJam"
    PrinterJam = 48,
    //% block="(D) ReceiverClear"
    ReceiverClear = 42,
    //% block="(D) ReceiverDead"
    ReceiverDead = 44,
    //% block="(D) ReceiverStatic"
    ReceiverStatic = 43,
    //% block="(D) SealLeak"
    SealLeak = 52,
    //% block="(D) SealRetract"
    SealRetract = 53,
    //% block="(D) SealStable"
    SealStable = 51,
    //% block="(D) SealVent"
    SealVent = 54,
    //% block="(D) TubeDrain"
    TubeDrain = 50,
    //% block="(D) TubeLaunch"
    TubeLaunch = 49,
    // Room E
    //% block="(E) LeverPull"
    LeverPull = 71,
    //% block="(E) LeverReject"
    LeverReject = 72,
    //% block="(E) RockBeam"
    RockBeam = 67,
    //% block="(E) RockCollapse"
    RockCollapse = 68,
    //% block="(E) SensorDark"
    SensorDark = 61,
    //% block="(E) SensorLamp1"
    SensorLamp1 = 58,
    //% block="(E) SensorLamp2"
    SensorLamp2 = 59,
    //% block="(E) SensorLamp3"
    SensorLamp3 = 60,
    //% block="(E) ShutterClosed"
    ShutterClosed = 64,
    //% block="(E) ShutterOpen"
    ShutterOpen = 62,
    //% block="(E) ShutterWarn"
    ShutterWarn = 63,
    //% block="(E) StarFizzle"
    StarFizzle = 66,
    //% block="(E) StarIgnite"
    StarIgnite = 65,
    //% block="(E) SyncLock"
    SyncLock = 69,
    //% block="(E) SyncReject"
    SyncReject = 70
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

// Native tile walls and the visible bases, operating pads, and output trays
// share this one tile-grid layout. The room art remains the background layer.
namespace escapeFloor {
    const tile = 16
    const mapColumns = 40
    const mapRows = 30
    const baseColumns = 7
    const baseRows = 8
    const doorTop = 14
    const doorBottom = 15

    // Surface-bank keys. Rows 0–4 retain the original room floor; only the
    // feet-level rows 5–7 receive shaped paving and a walk-facing apron.
    // This avoids drawing a debug-like rectangle around collision geometry.
    const quietA = 0
    const quietB = 1
    const back = 2
    const bodyA = 3
    const bodyB = 4
    const sideLeft = 5
    const sideRight = 6
    const front = 7
    const frontJoint = 8
    const backLeft = 9
    const backRight = 10
    const frontLeft = 11
    const frontRight = 12
    const hearth = 13
    const soot = 14
    const hearthEdge = 15

    // One shared tile-index layout is stamped beneath every apparatus. It is
    // art only: baseWall remains the sole collision authority.
    const surfaceLayout = [
        quietA, quietB, quietA, quietB, quietA, quietB, quietA,
        quietB, quietA, quietB, quietA, quietB, quietA, quietB,
        quietA, quietB, quietA, quietB, quietA, quietB, quietA,
        backLeft, back, bodyA, back, bodyB, back, backRight,
        sideLeft, bodyA, bodyB, bodyA, bodyB, bodyA, sideRight,
        sideLeft, bodyB, bodyA, bodyB, bodyA, bodyB, sideRight,
        sideLeft, bodyA, bodyB, bodyA, bodyB, bodyA, sideRight,
        frontLeft, front, frontJoint, front, frontJoint, front, frontRight
    ]

    // Kept as a bank rather than freehand art so a native tilemap can consume
    // these exact images later if its layer no longer obscures the props.
    let surfaceBanks: Image[][] = []

    function materialBase(room: number): number {
        if (room == 0) return 5   // workshop: warm stone/brass
        if (room == 1) return 9   // gallery: pale ceramic
        if (room == 2) return 6   // garden: weathered stone
        if (room == 3) return 14  // bridge: blue steel
        return 2                  // last door: plum slate
    }

    function materialShade(room: number): number {
        if (room == 0) return 2
        if (room == 1) return 14
        if (room == 2) return 2
        if (room == 3) return 1
        return 1
    }

    function materialGrout(room: number): number {
        if (room == 0) return 4
        if (room == 1) return 11
        if (room == 2) return 5
        if (room == 3) return 12
        return 12
    }

    function materialLight(room: number): number {
        if (room == 0) return 10
        if (room == 1) return 15
        if (room == 2) return 7
        if (room == 3) return 11
        return 10
    }

    function clip(t: Image, leftEdge: boolean, rightEdge: boolean, frontEdge: boolean) {
        // A few transparent corner pixels let the original room floor show
        // through. The paving therefore steps into the walking lane instead
        // of reading as a straight-edged machine panel.
        if (leftEdge) {
            t.setPixel(0, 0, 0)
            t.setPixel(0, 1, 0)
            t.setPixel(1, 0, 0)
        }
        if (rightEdge) {
            t.setPixel(15, 0, 0)
            t.setPixel(15, 1, 0)
            t.setPixel(14, 0, 0)
        }
        if (frontEdge) {
            t.setPixel(0, 15, 0)
            t.setPixel(1, 15, 0)
            t.setPixel(15, 15, 0)
            t.setPixel(14, 15, 0)
        }
    }

    function makeSurfaceTile(room: number, key: number): Image {
        let t = image.create(tile, tile)
        let baseColor = materialBase(room)
        let shade = materialShade(room)
        let grout = materialGrout(room)
        let light = materialLight(room)
        t.fill(baseColor)

        if (key == quietA || key == quietB) return t

        if (key == hearth || key == soot || key == hearthEdge) {
            // Refractory workshop floor: separate heatproof stones, dark soot and irregular edging.
            t.fill(key == hearthEdge ? 6 : 4)
            t.drawRect(0, 0, 16, 16, key == hearthEdge ? 5 : 2)
            t.drawLine(2, 2, 13, 2, key == hearthEdge ? 15 : 10)
            t.drawLine(2, 13, 13, 13, 2)
            if (key == soot) {
                t.fillCircle(5, 5, 3, 1)
                t.fillCircle(11, 7, 2, 1)
                t.fillCircle(8, 12, 2, 2)
                t.setPixel(13, 3, 1)
            } else if (key == hearthEdge) {
                t.setPixel(3, 8, 5); t.setPixel(12, 11, 5)
                t.setPixel(8, 4, 15)
            } else {
                t.setPixel(3, 8, 6); t.setPixel(12, 5, 2)
                t.drawLine(6, 4, 9, 4, 10)
            }
            return t
        }

        // Every normal tile is a top-down slab/plate with a bright upper edge and darker lower edge.
        t.drawRect(0, 0, 16, 16, grout)
        t.drawLine(2, 2, 13, 2, light)
        t.drawLine(2, 13, 13, 13, shade)
        t.setPixel(2, 3, light)

        if (room == 0) {
            // Workshop stone has warm metal dust and occasional scorched chips.
            t.setPixel(key % 2 ? 5 : 11, 7, 4)
            t.setPixel(key % 3 ? 12 : 4, 11, 2)
            if (key == bodyB || key == frontJoint) t.drawLine(6, 5, 9, 8, 6)
        } else if (room == 1) {
            // Gallery ceramic carries a cool glass inlay that still lies flat on the floor.
            t.drawLine(6, 5, 9, 5, 11)
            t.drawLine(6, 6, 9, 6, 13)
            t.setPixel(key % 2 ? 4 : 11, 11, 15)
        } else if (room == 2) {
            // Garden flagstone: uneven veins and tiny mossy flecks.
            t.drawLine(4, 11, 7, 9, 5)
            t.drawLine(7, 9, 11, 10, 2)
            t.setPixel(12, 5, 7)
            t.setPixel(3 + key % 4, 6, 7)
        } else if (room == 3) {
            // Bridge steel plate: rivets and a brushed highlight.
            t.fillCircle(3, 4, 1, 11)
            t.fillCircle(12, 12, 1, 11)
            t.drawLine(5, 7, 11, 7, 8)
            t.setPixel(10, 6, 15)
        } else {
            // Last-door slate with sparse brass circuitry.
            t.drawLine(4, 5, 10, 5, 12)
            t.drawLine(10, 5, 10, 8, 10)
            t.setPixel(3, 11, 11)
            if (key == bodyB || key == frontJoint) t.fillCircle(11, 10, 1, 10)
        }

        if (key == frontJoint) t.drawLine(7, 4, 7, 12, shade)
        clip(t, key == backLeft || key == sideLeft || key == frontLeft,
            key == backRight || key == sideRight || key == frontRight,
            key == front || key == frontJoint || key == frontLeft || key == frontRight)
        return t
    }

    function surfaceBank(room: number): Image[] {
        if (surfaceBanks[room] != undefined) return surfaceBanks[room]
        let bank: Image[] = []
        for (let key = 0; key <= hearthEdge; key++) bank.push(makeSurfaceTile(room, key))
        surfaceBanks[room] = bank
        return bank
    }

    // Exposed for a later native tilemap path. The renderer below deliberately
    // stamps this bank into the background now, before props are composed.
    export function tileBank(room: number): Image[] {
        return surfaceBank(room)
    }

    export function surfaceLayoutKey(station: number, localCol: number, localRow: number): number {
        let key = surfaceLayout[localRow * baseColumns + localCol]
        // Station 3 is the workshop spout. Its visible feet-level patch is a
        // hearth floor: soot at the rear, refractory body, stone apron.
        if (station == 3) {
            if (localRow == 5 && localCol >= 1 && localCol <= 5) return soot
            if (localRow >= 4 && localRow <= 6 && localCol >= 1 && localCol <= 5) return hearth
            if (localRow >= 4 && (localCol == 0 || localCol == 6)) return hearthEdge
            if (localRow == 7) return hearthEdge
        }
        return key
    }

    function extendedLeftKey(localCol: number, localRow: number): number {
        // Left-edge apparatus silhouettes overhang their collision footprint.
        // The extra decorative paving grows toward the walker in two steps.
        if (localCol == -2) return localRow == 7 ? frontLeft : sideLeft
        return localRow == 7 ? front : localRow == 6 ? bodyB : bodyA
    }

    // These values are tile coordinates. Keeping the machine base on tile
    // boundaries makes the same shape suitable for native collision and art.
    export function left(station: number): number {
        let center = Math.idiv(escapeFlow.x(station), tile)
        // The two side doors need their neighboring walk cell free. Shift only
        // edge machinery inward; it keeps each seven-tile prop footprint whole.
        if (escapeFlow.x(station) < 160) return center - 2
        if (escapeFlow.x(station) > 500) return center - 4
        return center - Math.idiv(columns(station), 2)
    }

    export function top(station: number): number {
        // Apparatus art spans roughly y - 56 through y + 56. The marked
        // footprint covers that full body, rather than only its lower plinth.
        return Math.idiv(escapeFlow.y(station) - 56, tile)
    }

    export function columns(station: number): number {
        return baseColumns
    }

    export function rows(station: number): number {
        return baseRows
    }

    export function standX(station: number): number {
        return (left(station) + Math.idiv(columns(station), 2)) * tile + Math.idiv(tile, 2)
    }

    export function standY(station: number): number {
        return (top(station) + rows(station)) * tile + Math.idiv(tile, 2)
    }

    export function trayX(station: number): number {
        let direction = escapeFlow.x(station) > 400 ? -1 : 1
        return standX(station) + direction * tile * 2
    }

    export function trayY(station: number): number {
        return standY(station)
    }

    function isDoorGap(col: number, row: number): boolean {
        return (col == 1 || col == mapColumns - 2) && row >= doorTop && row <= doorBottom
    }

    function baseWall(room: number, col: number, row: number): boolean {
        for (let local = 0; local < 6; local++) {
            let station = room * 6 + local
            if (col >= left(station) && col < left(station) + columns(station)
                && row >= top(station) && row < top(station) + rows(station)) return true
        }
        return false
    }

    // This mirrors every wall installed below and gives recorders a pure,
    // deterministic view of the collision geometry.
    export function isWall(room: number, col: number, row: number): boolean {
        if (room < 0 || room > 4 || col < 0 || col >= mapColumns || row < 0 || row >= mapRows) return true
        // The outer map edge catches a player at a visual doorway while the
        // inset wall still has its two-tile opening for the engine interaction.
        if (col == 0 || col == mapColumns - 1) return true
        if ((col == 1 || col == mapColumns - 2) && !isDoorGap(col, row)) return true
        if (row == 3 || row == mapRows - 3) return true
        return baseWall(room, col, row)
    }

    function blankMap(): Buffer {
        // TileMapData reads two UInt16 dimensions followed by one tile index per cell.
        let data = control.createBuffer(4 + mapColumns * mapRows)
        data.setNumber(NumberFormat.UInt16LE, 0, mapColumns)
        data.setNumber(NumberFormat.UInt16LE, 2, mapRows)
        return data
    }

    export function install(room: number) {
        // The single transparent tile lets the artwork remain the room floor.
        let transparentTile = image.create(tile, tile)
        let layers = image.create(mapColumns, mapRows)
        tiles.setCurrentTilemap(tiles.createTilemap(blankMap(), layers, [transparentTile], TileScale.Sixteen))
        for (let row = 0; row < mapRows; row++) for (let col = 0; col < mapColumns; col++) {
            if (isWall(room, col, row)) tiles.setWallAt(tiles.getTileLocation(col, row), true)
        }
    }

    // Called while the room background is being composed, before apparatus
    // props. Native tiles remain transparent because their layer would sit on
    // top of those props; this image-stamped paving has the intended depth.
    export function drawSurfaces(p: Image, room: number) {
        let bank = surfaceBank(room)
        for (let local = 0; local < 6; local++) {
            let station = room * 6 + local
            let leftExtension = escapeFlow.x(station) < 160 ? 2 : 0
            let originX = (left(station) - leftExtension) * tile
            let originY = top(station) * tile
            // Rows 0–4 intentionally remain the original room floor. Only the
            // apparatus feet receive paving, from y + 24 through y + 64.
            for (let row = 5; row < baseRows; row++) for (let col = -leftExtension; col < baseColumns; col++) {
                // The rear extension starts one tile later, making the apron
                // widen as it comes toward the player.
                if (col == -2 && row == 5) continue
                let key = col < 0 ? extendedLeftKey(col, row) : surfaceLayoutKey(station, col, row)
                if (station == 3 && col < 0) key = hearthEdge
                p.drawTransparentImage(bank[key], originX + (col + leftExtension) * tile, originY + row * tile)
            }
        }
    }

    function markPad(p: Image, x: number, y: number, fill: number, edge: number) {
        // Small inset floor plate: shadow, clipped corners, luminous directional center.
        p.fillRect(x - 8, y - 5, 17, 12, 12)
        p.fillRect(x - 7, y - 7, 15, 15, 1)
        p.fillRect(x - 5, y - 5, 11, 11, fill)
        p.setPixel(x - 7, y - 7, 0); p.setPixel(x + 7, y - 7, 0)
        p.setPixel(x - 7, y + 7, 0); p.setPixel(x + 7, y + 7, 0)
        p.drawLine(x - 4, y - 5, x + 4, y - 5, edge)
        p.drawLine(x - 4, y + 5, x + 4, y + 5, 6)
        p.drawLine(x - 3, y, x + 3, y, edge)
        p.drawLine(x, y - 3, x, y + 3, edge)
        p.setPixel(x, y - 4, 15)
    }

    // Draw after the apparatus silhouettes. Surface art belongs behind the
    // props; this late pass is reserved for the familiar pad and output tray.
    export function drawPads(p: Image, room: number, focusStation: number, activeStation: number) {
        for (let local = 0; local < 6; local++) {
            let station = room * 6 + local
            let edge = station == activeStation ? 15 : station == focusStation ? 10 : 6
            let padFill = station == activeStation ? 15 : station == focusStation ? 10 : 6
            markPad(p, standX(station), standY(station), padFill, edge)
            // Only producer stations visibly advertise an output tray. Other
            // machines keep their geometric tray point for cargo routing.
            if (escapeCargo.sourceItem(station) >= 0) {
                let tx = trayX(station), ty = trayY(station)
                // Shallow receiving tray: dark shadow below a metal lip and three recessed ribs.
                p.fillRect(tx - 10, ty - 5, 21, 13, 12)
                p.fillRect(tx - 9, ty - 9, 19, 16, 1)
                p.fillRect(tx - 7, ty - 7, 15, 12, 14)
                p.drawLine(tx - 7, ty - 7, tx + 7, ty - 7, 15)
                p.drawLine(tx - 6, ty - 3, tx + 6, ty - 3, 8)
                p.drawLine(tx - 6, ty + 1, tx + 6, ty + 1, 8)
                p.drawLine(tx - 6, ty + 5, tx + 6, ty + 5, 6)
                p.setPixel(tx - 7, ty + 4, 10)
            }
        }
    }
}

// Physical outputs are supplied interaction state, never learner decisions.
namespace escapeCargo {
    export const count = 13
    export const names = ["CRANK", "WATER CANISTER", "LENS STONE", "THAWED WEIGHT", "COLOR FILTERS", "COIL CONNECTOR", "REPAIR PATCH", "MEASURED DROPPER", "SIGNAL MODULE", "MESSAGE STRIP", "SENSOR CARD", "PATTERN PLATE", "INTERLOCK KEY"]
    export const sources = [0,2,9,11,7,15,16,14,18,20,24,26,28]
    export const targets = [1,3,10,7,8,12,17,13,19,21,25,27,29]
    export const productionBeats = [0,2,13,15,10,19,20,18,22,24,30,32,34]
    export function sourceStation(id: number): number { return sources[id] }
    export function targetStation(id: number): number { return targets[id] }
    export function produceBeat(id: number): number { return productionBeats[id] }
    export function sourceItem(station: number): number {
        for (let i = 0; i < count; i++) if (sources[i] == station) return i
        return -1
    }
    export function targetItem(station: number): number {
        for (let i = 0; i < count; i++) if (targets[i] == station) return i
        return -1
    }
    export function ready(id: number, solved: number[]): boolean {
        if (id < 0 || id >= count || solved[productionBeats[id]] != 1) return false
        if (id == 4) return solved[7] == 1 && solved[8] == 1 && solved[9] == 1 && solved[10] == 1
        return true
    }
    export function requiredForBeat(beat: number): number {
        if (beat == 1) return 0
        if (beat == 3) return 1
        if (beat == 14) return 2
        if (beat >= 7 && beat <= 10) return 3
        if (beat == 11 || beat == 12) return 4
        if (beat == 16) return 5
        if (beat == 21) return 6
        if (beat == 17) return 7
        if (beat == 23) return 8
        if (beat == 25) return 9
        if (beat == 31) return 10
        if (beat == 33) return 11
        if (beat == 35) return 12
        return -1
    }
    export function installedForBeat(beat: number, itemStates: number[]): boolean {
        let id = requiredForBeat(beat)
        return id < 0 || itemStates[id] == 2
    }
    // Art worker owns this function and any art-only helpers below it.
    export function drawItem(id: number, phase: number): Image {
        let p = image.create(28, 28)
        p.fillCircle(14, 24, 11, 12)
        if (id == 0) { // crank — same socket disc, steel arm and red grip seen on the Workshop machines
            p.fillCircle(10, 14, 8, 1); p.fillCircle(10, 14, 6, 6); p.drawCircle(10, 14, 5, 15); p.fillCircle(10, 14, 2, 10)
            p.drawLine(14, 12, 22, 6, 14); p.drawLine(15, 14, 23, 8, 15); p.fillCircle(23, 6, 4, 3); p.fillCircle(23, 6, 2, 4)
            p.setPixel(7 + phase % 3, 10, 15)
        } else if (id == 1) { // water canister — blue glass body, metal neck and visible water window
            p.fillRect(6, 8, 16, 15, 1); p.fillRect(8, 6, 12, 18, 8); p.drawRect(8, 6, 12, 18, 15)
            p.fillRect(11, 3, 6, 4, 6); p.fillRect(10, 4, 8, 2, 14); p.fillRect(11, 13, 6, 7, 9); p.fillRect(10, 10, 2, 10, 15)
            p.setPixel(13 + phase % 3, 11, 11); p.fillRect(10, 22, 8, 2, 6)
        } else if (id == 2) { // lens stone — violet optical disc released by the colored-stone grid
            p.fillCircle(14, 15, 11, 1); p.fillCircle(14, 14, 9, 6); p.fillCircle(14, 14, 7, 13)
            p.fillCircle(11, 10, 3, 15); p.fillCircle(17, 17, 2, 9); p.drawCircle(14, 14, 9, 15)
            p.setPixel(19 - phase % 3, 9 + phase % 2, 11)
        } else if (id == 3) { // thawed weight — same handled steel block seated on the portrait pressure plate
            p.fillRect(6, 12, 16, 12, 1); p.fillRect(8, 11, 12, 12, 6); p.drawRect(8, 11, 12, 12, 15)
            p.fillRect(10, 7, 8, 5, 14); p.fillRect(12, 4, 4, 4, 15); p.fillRect(11, 15, 8, 3, 14)
            p.setPixel(18, 17 + phase % 3, 11); p.fillCircle(9, 23, 2, 11)
        } else if (id == 4) { // color filters — three framed gallery filters carried as one cassette
            p.fillRect(3, 8, 22, 15, 1); p.fillRect(4, 7, 7, 15, 5); p.fillRect(11, 5, 7, 17, 8); p.fillRect(18, 7, 6, 15, 3)
            p.drawRect(4, 7, 7, 15, 15); p.drawRect(11, 5, 7, 17, 15); p.drawRect(18, 7, 6, 15, 15)
            p.fillRect(6, 10 + phase % 2, 3, 7, 10); p.fillRect(13, 8, 3, 8, 11); p.fillRect(20, 10, 2, 7, 4)
            p.fillRect(7, 23, 14, 2, 6)
        } else if (id == 5) { // coil connector — copper spring bridge with two ceramic plugs
            p.fillRect(3, 11, 6, 8, 14); p.fillRect(19, 11, 6, 8, 14); p.drawRect(3, 11, 6, 8, 15); p.drawRect(19, 11, 6, 8, 15)
            p.fillCircle(7, 15, 2, 4); p.fillCircle(21, 15, 2, 4)
            for (let x = 9; x <= 19; x += 3) p.drawCircle(x, 14 + (phase % 2), 4, 10)
            p.drawLine(8, 15, 20, 15, 4); p.setPixel(14 + phase % 3, 10, 15)
        } else if (id == 6) { // repair patch — riveted copper plate with the same crossed seal marks as the vessel
            p.fillRect(4, 7, 20, 15, 1); p.fillRect(5, 6, 18, 15, 11); p.drawRect(5, 6, 18, 15, 15)
            p.fillCircle(8, 9, 2, 6); p.fillCircle(20, 18, 2, 6); p.drawLine(8, 10, 20, 18, 3); p.drawLine(8, 18, 20, 10, 3)
            p.setPixel(11 + phase % 7, 8, 15)
        } else if (id == 7) { // measured dropper — graduated glass tube, red bulb and amber measured droplet
            p.fillRect(11, 5, 7, 17, 1); p.fillRect(12, 4, 5, 18, 15); p.fillRect(13, 7, 3, 11, 9)
            p.fillRect(10, 3, 9, 5, 3); for (let y = 9; y <= 17; y += 3) p.drawLine(12, y, 14, y, 1)
            p.fillCircle(14, 22, 4, 10); p.setPixel(14, 26, 8); p.setPixel(15 + phase % 2, 10, 11)
        } else if (id == 8) { // signal module — steel receiver cartridge with lamp, aerial tab and copper contacts
            p.fillRect(4, 9, 20, 14, 1); p.fillRect(5, 7, 18, 15, 6); p.drawRect(5, 7, 18, 15, 15)
            p.fillRect(8, 10, 8, 8, 12); p.fillCircle(11, 14, 3, 10); p.fillCircle(11, 14, 1, 15)
            p.drawLine(19, 8, 23, 3, 15); p.fillCircle(23, 3, 2, 14); p.fillRect(17, 18, 4, 2, 4)
            p.fillRect(7, 22, 4, 3, 10); p.fillRect(17, 22, 4, 3, 10); p.setPixel(18, 13 + phase % 4, 8)
        } else if (id == 9) { // message strip — folded printer strip with route marks and feed edge
            p.fillRect(5, 6, 18, 17, 15); p.drawRect(5, 6, 18, 17, 6)
            p.fillRect(7, 8, 14, 3, 12); p.drawLine(8, 13, 20, 13, 1); p.drawLine(8, 17, 18, 17, 1); p.drawLine(8, 20, 21, 20, 1)
            p.fillRect(3, 9, 3, 11, 14); p.fillRect(22, 9, 3, 11, 14); p.setPixel(10 + phase % 8, 9, 10)
        } else if (id == 10) { // sensor card — three-channel remote reader card with gold edge contacts
            p.fillRect(4, 6, 20, 17, 1); p.fillRect(5, 5, 18, 17, 14); p.drawRect(5, 5, 18, 17, 15)
            for (let i = 0; i < 3; i++) { p.fillCircle(9 + i * 5, 11, 2, i == phase % 3 ? 10 : 8); p.setPixel(9 + i * 5, 10, 15) }
            p.drawLine(8, 16, 20, 16, 9); p.drawLine(8, 18, 20, 18, 6)
            for (let x = 8; x <= 20; x += 4) p.fillRect(x, 22, 2, 3, 10)
        } else if (id == 11) { // pattern plate — comparison tablet carrying both color and mark information
            p.fillRect(3, 7, 22, 16, 1); p.fillRect(4, 6, 20, 16, 6); p.drawRect(4, 6, 20, 16, 15)
            p.fillCircle(9, 13, 5, 8); p.fillCircle(19, 13, 5, phase % 2 ? 8 : 3)
            p.fillCircle(9, 13, 2, 15); if (phase % 2) p.fillCircle(19, 13, 2, 15); else p.drawLine(16, 13, 22, 13, 15)
            p.fillRect(7, 22, 14, 3, 14); p.setPixel(13 + phase % 4, 8, 10)
        } else { // interlock key — three-bus key that fits the final vault cylinder
            p.fillCircle(8, 12, 7, 1); p.fillCircle(8, 11, 6, 10); p.fillCircle(8, 11, 3, 14); p.fillCircle(8, 11, 1, 1)
            p.fillRect(13, 9, 12, 6, 10); p.fillRect(15, 10, 9, 2, 15)
            p.fillRect(20, 14, 5, 5, 10); p.fillRect(16, 14, 3, 3, 10)
            for (let i = 0; i < 3; i++) p.setPixel(6 + i * 2, 5 + (phase + i) % 2, i == phase % 3 ? 15 : 14)
        }
        return p
    }

    // Visual-only travel helpers. They never change item state or puzzle progress;
    // engine.ts uses them only to stage production and wrong-placement motion.
    //% blockHidden=true
    export function productionProgress(frame: number): number {
        if (frame < 3) return -1
        return Math.max(0, Math.min(1, (frame - 3) / 8))
    }
    //% blockHidden=true
    export function productionX(id: number, frame: number): number {
        let source = sourceStation(id)
        let t = productionProgress(frame)
        if (t < 0) return escapeFlow.x(source)
        return Math.round(escapeFlow.x(source) + (escapeFloor.trayX(source) - escapeFlow.x(source)) * t)
    }
    //% blockHidden=true
    export function productionY(id: number, frame: number): number {
        let source = sourceStation(id)
        let t = productionProgress(frame)
        if (t < 0) return escapeFlow.y(source) - 12
        return Math.round(escapeFlow.y(source) - 12 + (escapeFloor.trayY(source) - (escapeFlow.y(source) - 12)) * t - 18 * Math.sin(Math.PI * t))
    }

    export const returnFrames = 8
    //% blockHidden=true
    export function returnProgress(framesLeft: number): number {
        return Math.max(0, Math.min(1, (returnFrames - framesLeft) / returnFrames))
    }
    //% blockHidden=true
    export function returnX(id: number, startX: number, framesLeft: number): number {
        let source = sourceStation(id)
        let t = returnProgress(framesLeft)
        return Math.round(startX + (escapeFloor.trayX(source) - startX) * t)
    }
    //% blockHidden=true
    export function returnY(id: number, startY: number, framesLeft: number): number {
        let source = sourceStation(id)
        let t = returnProgress(framesLeft)
        return Math.round(startY + (escapeFloor.trayY(source) - startY) * t - 28 * Math.sin(Math.PI * t))
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
        // Pixel-rounded body with a small upper highlight and lower shade instead of a flat card.
        p.fillRect(x + 3, y, w - 6, h, c); p.fillRect(x, y + 3, w, h - 6, c)
        p.fillRect(x + 1, y + 1, w - 2, h - 2, c)
        if (w > 8) p.drawLine(x + 4, y + 1, x + w - 5, y + 1, 15)
        if (h > 8) p.drawLine(x + 3, y + h - 2, x + w - 4, y + h - 2, 6)
    }
    function shadow(p: Image, cx: number, y: number, rx: number = 45) {
        oval(p, cx + 2, y + 1, rx, 6, 12)
        oval(p, cx + 2, y + 1, Math.max(8, rx - 10), 3, 1)
    }
    function bolt(p: Image, x: number, y: number) {
        p.fillCircle(x, y + 1, 3, 1); p.fillCircle(x, y, 3, 6); p.fillCircle(x, y - 1, 2, 9)
        p.setPixel(x - 1, y - 2, 15); p.drawLine(x - 1, y, x + 1, y, 12)
    }
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
        p.fillCircle(x, y, r, c)
        // The teeth are symmetric, so retain one rotating spoke to make an
        // actual turn visible rather than only changing draw-call order.
        let spoke = ((turn % 4) + 4) % 4
        if (spoke == 0) p.drawLine(x, y - 5, x, y - r + 5, 15)
        else if (spoke == 1) p.drawLine(x + 5, y, x + r - 5, y, 15)
        else if (spoke == 2) p.drawLine(x, y + 5, x, y + r - 5, 15)
        else p.drawLine(x - 5, y, x - r + 5, y, 15)
        p.drawCircle(x, y, r - 4, 1); p.fillCircle(x, y, 5, 6); p.fillCircle(x, y, 2, 10)
    }
    function glass(p: Image, x: number, y: number, w: number, h: number) {
        // Dark frame, cool transparent body, bright left reflection and a restrained cyan catchlight.
        p.fillRect(x, y, w, h, 1)
        p.fillRect(x + 2, y + 2, w - 4, h - 4, 12)
        p.drawRect(x + 1, y + 1, w - 2, h - 2, 9)
        p.fillRect(x + 4, y + 4, 2, h - 8, 15)
        p.fillRect(x + 7, y + 5, Math.max(1, w - 13), 2, 11)
        if (w > 14 && h > 12) p.setPixel(x + w - 5, y + h - 5, 8)
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

    // `frame` belongs to the short response animation. `idleFrame` is a
    // separate world clock, so a prop does not freeze when a response ends.
    export function prop(station: number, control: number, response: number, frame: number, done: boolean, part: number = 0, pitch: number = 0, portraitMask: number = 0, idleFrame: number = 0, fitted: boolean = false, sourceState: number = -1, requiresPart: boolean = false): Image {
        let p = image.create(144, 112)
        // A completed machine stays visibly changed after its short animation.
        // A fresh learner response still takes precedence, including its else.
        let parked = response < 0 && done && station != 7
        if (parked) {
            const parked = [EscapeAction.CrankPull, EscapeAction.GeneratorSpin, EscapeAction.CaseRetract, EscapeAction.FireSteam, EscapeAction.WallClimb, EscapeAction.FootprintKeep, EscapeAction.ShadowReveal, EscapeAction.PortraitLeft, EscapeAction.MuralBlend, EscapeAction.StoneSnap, EscapeAction.TelescopeFocus, EscapeAction.ThermalAmber, EscapeAction.SampleSpike, EscapeAction.TitrationBloom, EscapeAction.ScaleLevel, EscapeAction.WireInstall, EscapeAction.LeafClip, EscapeAction.VesselReveal, EscapeAction.ReceiverClear, EscapeAction.NoiseClear, EscapeAction.PrinterFeed, EscapeAction.TubeLaunch, EscapeAction.SealStable, EscapeAction.PitchLevel, EscapeAction.SensorLamp1, EscapeAction.ShutterOpen, EscapeAction.StarIgnite, EscapeAction.RockBeam, EscapeAction.SyncLock, EscapeAction.LeverPull]
            response = parked[station]
            if (station == 8 && part == 1) response = EscapeAction.MuralOpen
            if (station == 22 && part == 1) response = EscapeAction.SealRetract
            if (station == 24) response = control == 1 ? EscapeAction.SensorLamp2 : control == 2 ? EscapeAction.SensorLamp3 : EscapeAction.SensorLamp1
            frame = 7
        }
        let ok = good(station, response, done), t = pulse(response, frame)
        let idle = Math.abs(idleFrame) % 16
        if (station == 0) magnetCrank(p, control, response, t, ok, idle, parked, sourceState)
        else if (station == 1) generator(p, control, response, t, ok, idle, parked, fitted)
        else if (station == 2) reservoir(p, control, response, t, ok, idle, parked)
        else if (station == 3) hearth(p, control, response, t, ok, idle, parked, fitted)
        else if (station == 4) climbingWall(p, control, response, t, ok)
        else if (station == 5) footprintPath(p, control, response, t, ok)
        else if (station == 6) shadowLantern(p, control, response, t, ok)
        else if (station == 7) portraits(p, control, response, t, ok, part, portraitMask, fitted, sourceState)
        else if (station == 8) mural(p, control, response, t, ok, part, fitted)
        else if (station == 9) sockets(p, control, response, t, ok, sourceState)
        else if (station == 10) telescope(p, control, response, t, ok, fitted)
        else if (station == 11) thermalBath(p, control, response, t, ok, sourceState)
        else if (station == 12) filings(p, control, response, t, ok, fitted)
        else if (station == 13) titration(p, control, response, t, ok, fitted)
        else if (station == 14) balance(p, control, response, t, ok, sourceState)
        else if (station == 15) wires(p, control, response, t, ok, sourceState)
        else if (station == 16) plant(p, control, response, t, ok, sourceState)
        else if (station == 17) heatVessel(p, control, response, t, ok, fitted)
        else if (station == 18) pedalRadio(p, control, response, t, ok, idle, parked, sourceState)
        else if (station == 19) horns(p, control, response, t, ok, fitted)
        else if (station == 20) printer(p, control, response, t, ok, sourceState)
        else if (station == 21) tubes(p, control, response, t, ok, fitted)
        else if (station == 22) pressure(p, control, response, t, ok, part)
        else if (station == 23) plank(p, control, response, t, ok, pitch, part)
        else if (station == 24) sensors(p, control, response, t, ok, sourceState)
        else if (station == 25) shutters(p, control, response, t, ok, fitted)
        else if (station == 26) constellation(p, control, response, t, ok, sourceState)
        else if (station == 27) rockPath(p, control, response, t, ok, fitted)
        else if (station == 28) interlocks(p, control, response, t, ok, idle, parked, sourceState)
        else exitDoor(p, control, response, t, ok, fitted)
        fixtureStatus(p, fitted, sourceState, requiresPart)
        ambientDetails(p, station, control, response, ok, idle, parked)
        return p
    }

    // 0. A suspended horseshoe magnet travels over a riveted rail and releases the hand crank.
    function magnetCrank(p: Image, control: number, response: number, t: number, ok: boolean, idle: number, parked: boolean, sourceState: number) {
        shadow(p, 70, 101, 59)
        // Heavy floor rail: sleepers, twin steel tracks, end stops and a removable crank carriage.
        p.fillRect(12, 84, 112, 10, 1); p.fillRect(15, 81, 106, 5, 6)
        for (let x = 20; x <= 112; x += 16) { p.fillRect(x, 79, 5, 14, 5); p.fillRect(x + 1, 80, 3, 12, 14) }
        p.drawLine(18, 83, 117, 83, 15); p.drawLine(18, 89, 117, 89, 9)
        p.fillRect(14, 78, 5, 16, 14); p.fillRect(118, 78, 5, 16, 14); bolt(p, 16, 86); bolt(p, 120, 86)

        let touching = control == 1
        let canPull = response == EscapeAction.CrankPull && touching
        let carriageX = 28 + (canPull ? t * 6 : response >= 0 && !canPull ? (t % 2) * 2 : 0)
        // Once the crank has been produced, the separate cargo sprite owns it; leave an empty carriage behind.
        if (sourceState <= 0) {
            rounded(p, carriageX, 70, 31, 14, 1); p.fillRect(carriageX + 3, 72, 25, 8, 6)
            p.fillRect(carriageX + 6, 73, 16, 2, 15); p.drawLine(carriageX + 20, 76, carriageX + 28, 69, 14)
            p.fillCircle(carriageX + 29, 68, 4, 3); p.fillCircle(carriageX + 29, 68, 2, 15)
        } else {
            p.drawRect(31, 72, 26, 10, 6); p.fillRect(35, 78, 18, 2, 1)
        }

        // Workshop gantry. The magnet position is the actual two-state fixture: far or touching the crank.
        p.fillRect(17, 13, 6, 63, 6); p.fillRect(97, 13, 6, 63, 6); p.fillRect(16, 10, 88, 7, 14)
        p.fillRect(20, 11, 80, 2, 15); p.fillRect(22, 17, 3, 56, 5); p.fillRect(95, 17, 3, 56, 5)
        bolt(p, 20, 14); bolt(p, 100, 14)
        let mx = touching ? 49 : 80
        let sway = response < 0 && !parked ? (idle < 4 || idle >= 12 ? -1 : 1) : 0
        if (response >= 0 && !canPull) mx += (t % 2) * 2
        p.fillRect(mx - 2, 16, 5, 26 + sway, 6); p.fillRect(mx - 1, 16, 2, 26 + sway, 15)
        // Horseshoe magnet: broad red poles, dark iron yoke, bright pole faces.
        p.fillRect(mx - 18, 41 + sway, 37, 8, 1); p.fillRect(mx - 16, 43 + sway, 33, 7, 3)
        p.fillRect(mx - 16, 48 + sway, 10, 22, 3); p.fillRect(mx + 7, 48 + sway, 10, 22, 3)
        p.fillRect(mx - 13, 49 + sway, 7, 4, 4); p.fillRect(mx + 7, 49 + sway, 7, 4, 4)
        p.fillRect(mx - 16, 66 + sway, 10, 5, 15); p.fillRect(mx + 7, 66 + sway, 10, 5, 15)
        p.fillRect(mx - 5, 43 + sway, 12, 5, 6); bolt(p, mx, 45 + sway)
        if (touching && sourceState <= 0) { p.drawLine(mx - 8, 71 + sway, carriageX + 11, 70, 10); p.setPixel(carriageX + 12, 69, 15) }

        // Side winch makes the operator's physical input visible without becoming the produced crank.
        p.fillRect(110, 49, 8, 35, 14); p.fillRect(112, 52, 4, 31, 5); p.fillCircle(114, 47, 10, 6)
        p.fillCircle(114, 47, 7, 5); p.fillCircle(114, 47, 3, 1)
        let handDir = control == 0 ? -1 : 1
        let handLift = response >= 0 ? (canPull ? t - 3 : (t % 2) * 2) : 0
        p.drawLine(114, 47, 114 + handDir * 16, 47 + handLift, 14); p.drawLine(114, 49, 114 + handDir * 16, 49 + handLift, 15)
        p.fillCircle(114 + handDir * 17, 47 + handLift, 4, 3); p.fillCircle(114 + handDir * 17, 47 + handLift, 2, 4)
        if (response >= 0 && !canPull) { p.fillCircle(59, 76 - (t % 3), 2, 3); p.setPixel(63, 74 + (t % 2), 10) }
    }

    // 1. Copper generator with a visible crank socket, flywheel, belt, coils and power lamp.
    function generator(p: Image, control: number, response: number, t: number, ok: boolean, idle: number, parked: boolean, fitted: boolean) {
        shadow(p, 70, 101, 58)
        // Cast base and copper coil housing.
        rounded(p, 16, 61, 78, 31, 1); p.fillRect(20, 62, 70, 26, 14); p.fillRect(24, 66, 62, 18, 2)
        p.fillRect(28, 68, 23, 14, 12); p.fillRect(31, 70, 17, 2, 15)
        for (let x = 57; x <= 78; x += 7) { p.fillRect(x, 67, 4, 16, 4); p.drawLine(x + 1, 68, x + 1, 81, 10) }
        p.fillRect(22, 86, 68, 5, 6); bolt(p, 24, 88); bolt(p, 87, 88)

        // A missing fitted crank is mechanically meaningful: the rotor can only jolt or sputter.
        let requestedSpin = response == EscapeAction.GeneratorSpin
        let poweredSpin = fitted && requestedSpin
        let spin = parked && ok && fitted ? idle : poweredSpin ? t * 2 : response >= 0 ? (t % 2) : 0
        gear(p, 54, 45, 25, 5, spin); p.fillCircle(54, 45, 19, 14); p.fillCircle(54, 45, 16, 4)
        p.drawCircle(54, 45, 12, 15); p.fillCircle(54, 45, 7, 6); p.fillCircle(54, 45, 3, 15)
        let marker = spin % 4
        if (marker == 0) p.drawLine(54, 39, 54, 29, 15)
        else if (marker == 1) p.drawLine(60, 45, 70, 45, 15)
        else if (marker == 2) p.drawLine(54, 51, 54, 61, 15)
        else p.drawLine(48, 45, 38, 45, 15)

        // Crank socket and installed hand crank are the same recognizable silhouette as cargo item 0.
        p.fillCircle(82, 44, 8, 1); p.fillCircle(82, 44, 5, fitted ? 10 : 6); p.fillCircle(82, 44, 2, 15)
        if (fitted) {
            // The selected physical fixture is visible even before A is pressed: RESTING and TURN
            // occupy different crank detents. During a response/solved idle the real rotor clock owns the pose.
            let crankPose = response < 0 && !parked ? control % 2 : spin % 4
            let ex = crankPose == 0 ? 100 : crankPose == 1 ? 101 : crankPose == 2 ? 65 : 64
            let ey = crankPose == 0 ? 33 : crankPose == 1 ? 53 : crankPose == 2 ? 55 : 35
            p.drawLine(84, 43, ex, ey, 14); p.drawLine(85, 45, ex + (ex >= 82 ? 1 : -1), ey + 2, 15)
            p.fillCircle(ex + (ex >= 82 ? 2 : -2), ey, 5, 3); p.fillCircle(ex + (ex >= 82 ? 2 : -2), ey, 2, 4)
        } else { p.drawLine(78, 40, 86, 48, 6); p.drawLine(86, 40, 78, 48, 6) }

        // Belted dynamo head and cable to the power terminal.
        p.drawLine(72, 29, 105, 26 + spin % 3, 1); p.drawLine(72, 54, 105, 49 - spin % 3, 1)
        rounded(p, 99, 19, 27, 38, 1); p.fillRect(102, 22, 21, 32, 14); p.fillRect(105, 25, 15, 26, 12)
        p.fillCircle(112, 37, 8, 1); p.fillCircle(112, 37, 5, parked && fitted ? 10 : poweredSpin ? 10 : response >= 0 ? 3 : 6)
        if (poweredSpin || parked && fitted) { p.fillCircle(112, 37, 2, 15); p.drawLine(119, 28, 125, 22, 10); p.setPixel(126, 21, 15) }
        else if (response >= 0) { p.setPixel(108 + t % 7, 29 + t % 5, 3); p.setPixel(118 - t % 5, 46, 10) }
        p.fillRect(126, 47, 9, 30, 6); p.fillRect(124, 73, 13, 6, 14); p.fillCircle(131, 78, 3, 9)
        p.drawLine(25, 66, 13, 53, 4); p.fillCircle(12, 51, 5, 5); p.fillCircle(12, 51, 2, 15)
    }

    // 2. Powered protective case around a raised copper-and-glass water reservoir.
    function reservoir(p: Image, control: number, response: number, t: number, ok: boolean, idle: number, parked: boolean) {
        shadow(p, 72, 101, 56)
        p.fillRect(12, 84, 120, 10, 1); p.fillRect(16, 81, 112, 8, 14); p.fillRect(20, 84, 104, 3, 6)
        bolt(p, 20, 86); bolt(p, 124, 86)

        // Raised tank with visibly contained liquid and a lower fill manifold.
        p.fillRect(37, 31, 56, 39, 1); oval(p, 65, 31, 28, 9, 5); oval(p, 65, 32, 24, 6, 14)
        p.fillRect(40, 34, 50, 29, 5); oval(p, 65, 62, 25, 7, 4)
        p.fillRect(45, 40, 40, 20, 8); p.fillRect(48, 42, 34, 16, 9); p.fillRect(48, 42, 4, 16, 15)
        let ripple = response < 0 && !parked ? idle % 7 : 2
        p.drawLine(55 + ripple, 51, 72 + ripple, 51, 15); p.setPixel(75 - ripple, 55, 11)
        p.fillRect(84, 36, 4, 27, 4); p.fillRect(54, 65, 22, 3, 14)
        p.drawLine(65, 69, 65, 78, 14); p.drawLine(65, 78, 105, 78, 14); p.drawLine(66, 80, 105, 80, 6)
        p.fillCircle(107, 79, 8, 5); p.fillCircle(107, 79, 4, 1)
        let valveTurn = response == EscapeAction.CaseRetract ? t : 0
        p.drawLine(107, 79, 112, 74 + valveTurn, ok ? 10 : 3)

        // Motor/button column makes the two fixture positions tangible.
        rounded(p, 106, 46, 22, 27, 1); p.fillRect(109, 49, 16, 21, 6)
        p.fillCircle(117, 57, 6, control == 1 ? 10 : 5); p.fillCircle(117, 57 + (control == 1 ? 2 : 0), 3, 15)
        p.fillRect(112, 67, 10, 2, 14)

        // Two-panel safety glass retracts sideways on success; failure rattles its latches instead.
        let retract = response == EscapeAction.CaseRetract ? Math.min(25, t * 4) : 0
        let shake = response >= 0 && response != EscapeAction.CaseRetract ? (t % 2) * 2 : 0
        let leftX = 15 - retract + shake, rightX = 69 + retract - shake
        p.drawRect(leftX, 13, 53, 67, 9); p.fillRect(leftX + 3, 17, 2, 58, 15); p.fillRect(leftX + 7, 18, 35, 2, 11)
        p.drawRect(rightX, 13, 53, 67, 9); p.fillRect(rightX + 48, 17, 2, 58, 15); p.fillRect(rightX + 10, 18, 34, 2, 11)
        p.fillRect(66 - retract, 15, 3, 62, 14); p.fillRect(68 + retract, 15, 3, 62, 14)
        if (response >= 0 && response != EscapeAction.CaseRetract) { p.fillCircle(66, 19 + t, 2, 3); p.fillCircle(72, 20 + t, 2, 3) }
    }

    // 3. Stone hearth: the installed water canister and tipped spout visibly determine steam versus flare.
    function hearth(p: Image, control: number, response: number, t: number, ok: boolean, idle: number, parked: boolean, fitted: boolean) {
        shadow(p, 70, 101, 57)
        // Irregular masonry body; the surrounding refractory paving remains owned by floor.ts.
        p.fillRect(12, 70, 99, 23, 1)
        for (let y = 72; y < 92; y += 7) for (let x = 16 + (Math.idiv(y, 7) % 2) * 8; x < 107; x += 19) {
            p.fillRect(x, y, 17, 6, 6); p.fillRect(x + 1, y + 1, 13, 2, 14); p.setPixel(x + 15, y + 4, 2)
        }
        // Fire bowl and grate.
        p.fillRect(25, 41, 71, 31, 14); oval(p, 60, 41, 36, 10, 6); oval(p, 60, 42, 31, 7, 1); p.fillRect(31, 46, 59, 24, 1)
        p.drawLine(35, 67, 83, 48, 14); p.drawLine(40, 48, 86, 67, 5); p.drawLine(39, 65, 82, 47, 4)

        let tipped = control == 1
        let steam = response == EscapeAction.FireSteam && fitted && tipped
        let flare = response == EscapeAction.FireFlare || response == EscapeAction.FireSteam && !steam
        let flame = response < 0 && !parked ? 20 + idle % 5 : steam ? Math.max(5, 20 - t * 3) : flare ? 24 + t * 4 : 12
        for (let i = 0; i < 3; i++) {
            let x = 42 + i * 13 + (response < 0 && !parked && (idle + i) % 5 == 0 ? 1 : 0)
            let top = 66 - flame + (i % 2) * 6
            let outer = steam ? 11 : 3, inner = steam ? 9 : 4
            p.fillCircle(x, 60 - Math.idiv(flame, 3), 9, outer); p.fillRect(x - 6, top + 9, 13, 59 - top, outer)
            p.drawLine(x - 6, top + 11, x, top, outer); p.drawLine(x + 6, top + 11, x, top, outer)
            p.fillCircle(x, 60 - Math.idiv(flame, 4), 5, inner); p.fillRect(x - 2, top + 15, 5, 47 - top, inner)
        }

        // Brass water stand. Fitted canister repeats cargo item's blue body and cap.
        p.fillRect(96, 26, 9, 48, 5); p.fillRect(101, 28, 24, 8, 14); p.fillRect(122, 30, 12, 5, 10); p.fillCircle(130, 33, 4, 15)
        if (fitted) { p.fillRect(108, 44, 17, 22, 8); p.drawRect(108, 44, 17, 22, 15); p.fillRect(112, 40, 9, 5, 6); p.fillRect(111, 54, 11, 8, 9); p.setPixel(114 + idle % 3, 49, 15) }
        else { p.drawRect(108, 45, 17, 21, 6); p.fillRect(112, 55, 9, 2, 1) }
        p.fillCircle(101, 46, 6, 5); p.fillCircle(101, 46, 3, 1)
        let leverY = tipped ? 52 : 42; p.drawLine(101, 46, 92, leverY, 14); p.fillCircle(91, leverY, 3, 10)

        if (steam) {
            p.drawLine(123, 35, 83, 50, 8); p.drawLine(122, 36, 83, 51, 11)
            for (let i = 0; i < 5; i++) { let sy = 42 - ((t * 2 + i * 5) % 20); p.fillCircle(40 + i * 12, sy, 4, 11); p.setPixel(41 + i * 12, sy - 3, 15) }
        } else if (response >= 0 && flare) {
            for (let i = 0; i < 5; i++) { p.fillCircle(33 + i * 15, 36 - ((t + i * 2) % 8), 2, i % 2 == 0 ? 4 : 10) }
        } else if (response < 0 && !parked) {
            p.setPixel(34 + idle % 25, 35 + idle % 3, 10); p.fillCircle(48 + (idle * 3) % 24, 31 - idle % 6, 1, 4)
        }
    }

    // 4. A real climbing wall exposes either three holds and an empty anchor, or four usable holds.
    function climbingWall(p: Image, control: number, response: number, t: number, ok: boolean) {
        shadow(p, 72, 102, 55)
        // Thick wall slab, cap and side returns give it depth instead of reading as a flat card.
        p.fillRect(22, 11, 90, 84, 1); p.fillRect(27, 14, 80, 78, 2); p.fillRect(30, 17, 74, 72, 6)
        p.fillRect(26, 12, 82, 5, 14); p.fillRect(104, 18, 5, 72, 5); p.fillRect(30, 86, 74, 5, 5)
        for (let y = 25; y < 84; y += 15) { p.drawLine(33, y, 101, y + (y % 2), 14); p.setPixel(39 + y % 11, y - 2, 5) }
        for (let x = 36; x < 100; x += 20) p.drawLine(x, 20, x - 4, 86, 5)

        let holdCount = control == 0 ? 3 : 4
        let hx = [43, 84, 45, 83], hy = [72, 58, 43, 29]
        for (let i = 0; i < 4; i++) {
            if (i < holdCount) {
                let lit = response == EscapeAction.WallClimb && i <= Math.min(3, Math.idiv(t + 1, 2))
                p.fillCircle(hx[i] + 2, hy[i] + 3, 8, 1); rounded(p, hx[i] - 10, hy[i] - 5, 22, 12, lit ? 10 : (i % 2 == 0 ? 5 : 4))
                p.fillRect(hx[i] - 6, hy[i] - 3, 12, 3, lit ? 15 : 14); p.setPixel(hx[i] + 6, hy[i] + 2, 1)
            } else {
                p.fillCircle(hx[i], hy[i], 6, 1); p.drawCircle(hx[i], hy[i], 5, 14); p.fillCircle(hx[i], hy[i], 2, 6)
            }
        }

        let canClimb = control == 1 && response == EscapeAction.WallClimb
        if (canClimb) {
            let cy = 82 - t * 7
            p.drawLine(61, 84, 80, 20, 10); p.fillCircle(65, cy - 7, 6, 7); p.fillRect(61, cy - 1, 9, 13, 7)
            p.drawLine(62, cy + 3, 49, cy + 10, 7); p.drawLine(69, cy + 3, 79, cy - 4, 7)
            p.drawLine(63, cy + 11, 55, cy + 18, 7); p.drawLine(68, cy + 11, 76, cy + 17, 7)
        } else if (response >= 0) {
            // WallFlash or an impossible climb request highlights the empty anchor instead of moving the climber.
            let ex = control == 0 ? hx[3] : 67, ey = control == 0 ? hy[3] : 24
            p.drawCircle(ex, ey, 9 + t % 3, 3); p.fillCircle(ex, ey, 2, 10)
            p.fillRect(48, 20 + (t % 2) * 3, 39, 5, 3); p.fillRect(53, 21 + (t % 2) * 3, 29, 2, 15)
        }
        p.fillRect(17, 91, 101, 6, 14); p.fillRect(21, 93, 93, 2, 5)
    }

    // 5. Three numbered choices cross a deep workshop trench; the selected stone must survive +3.
    function footprintPath(p: Image, control: number, response: number, t: number, ok: boolean) {
        shadow(p, 72, 102, 62)
        // Deep gap with masonry lips and perspective rails.
        p.fillRect(6, 27, 132, 64, 1); p.fillRect(9, 31, 126, 56, 12)
        for (let x = 10; x < 137; x += 14) p.drawLine(x, 32, x - 8, 86, 2)
        p.fillRect(5, 24, 134, 7, 14); p.fillRect(7, 26, 130, 2, 5)
        p.fillRect(5, 88, 134, 8, 14); p.fillRect(7, 89, 130, 2, 5)

        let values = [8, 7, 6]
        let selected = control % 3
        for (let i = 0; i < 3; i++) {
            let x = 20 + i * 40, y = i == 1 ? 48 : 66
            let validKeep = i != 0
            let dropping = response >= 0 && i == selected && (response == EscapeAction.FootprintDrop || response == EscapeAction.FootprintKeep && !validKeep)
            if (dropping) y += t * 6
            p.fillCircle(x + 12, y + 8, 13, 1); rounded(p, x, y, 25, 17, i == selected ? 10 : 6)
            p.fillRect(x + 3, y + 3, 19, 3, i == selected ? 15 : 14)
            p.print('' + values[i], x + 10, y + 7, 1, image.font5)
            // Distinct boot-print marks make these read as stepping stones rather than buttons.
            p.fillRect(x + 5, y - 5, 5, 5, 15); p.fillRect(x + 11, y - 2, 3, 6, 15); p.setPixel(x + 4, y - 6, 15)
            if (dropping) { p.fillCircle(x + 5, y - 4, 2, 6); p.fillCircle(x + 20, y - 2, 2, 6) }
        }
        // The far-side +3 marker is physical arithmetic context, not tutorial prose.
        p.fillRect(112, 34, 19, 17, 5); p.drawRect(112, 34, 19, 17, 15); p.print('+3', 116, 39, 1, image.font5)
        let keepValid = selected != 0
        if (response == EscapeAction.FootprintKeep && keepValid) {
            for (let i = 0; i < 5; i++) { p.drawLine(29 + i * 19, 78 - (i % 2) * 15, 39 + i * 19, 70 - ((i + 1) % 2) * 15, 7); p.setPixel(34 + i * 19, 73, 15) }
            p.fillCircle(123, 59, 5, 10); p.fillCircle(123, 59, 2, 15)
        } else if (response >= 0 && response == EscapeAction.FootprintKeep && !keepValid) {
            p.drawLine(18, 37, 128, 82, 3); p.drawLine(128, 37, 18, 82, 3)
        }
    }

    // 6. A gallery lantern projects across a calibrated light gate onto a treated shadow screen.
    // Control 0/1 is the real 59/60 illumination boundary used by the learner predicate.
    function shadowLantern(p: Image, control: number, response: number, t: number, ok: boolean) {
        shadow(p, 73, 102, 58)
        // Screen plinth and porcelain frame.
        p.fillRect(38, 14, 57, 82, 1); p.fillRect(42, 17, 49, 76, 14)
        p.fillRect(45, 20, 43, 61, 12); p.drawRect(46, 21, 41, 59, 9)
        p.fillRect(49, 24, 3, 53, 15); p.fillRect(84, 25, 2, 51, 11)
        p.fillRect(39, 82, 55, 8, 6); p.fillRect(43, 83, 47, 3, 15)
        bolt(p, 43, 91); bolt(p, 90, 91)

        // Lantern body, iris and brass focusing wheel.
        p.fillRect(8, 57, 25, 31, 1); rounded(p, 11, 55, 20, 31, 5)
        p.fillRect(14, 61, 14, 17, 4); p.fillCircle(21, 54, 12, 1); p.fillCircle(21, 54, 9, 6)
        p.fillCircle(21, 54, 6, control == 1 ? 10 : 4); p.fillCircle(19, 52, 2, 15)
        p.fillRect(15, 82, 13, 7, 14); p.fillRect(18, 84, 7, 2, 6)
        p.fillCircle(9, 68, 6, 14); p.fillCircle(9, 68, 3, 10); p.drawLine(5, 68, 12, 68, 1)

        // The beam gains one bright core at exactly LIGHT 60. At 59 it still reaches the
        // screen but cannot reveal the treated ink, matching the actual prerequisite.
        let beam = control == 1 || response == EscapeAction.ShadowReveal
        let beamColor = beam ? 10 : 6
        p.drawLine(31, 49, 46, 38, beamColor); p.drawLine(31, 59, 46, 64, beamColor)
        p.drawLine(32, 53, 46, 51, beam ? 15 : 14)
        if (beam) { p.drawLine(32, 55, 46, 56, 11); p.setPixel(38 + t % 6, 52, 15) }

        // Treated ink: a crisp keyhole/figure appears on success; hide gives an opaque wash.
        if (response == EscapeAction.ShadowReveal || response < 0 && ok) {
            let rise = response >= 0 ? Math.min(3, Math.idiv(t, 2)) : 3
            p.fillCircle(67, 41 - rise, 9, 1); p.fillRect(61, 49 - rise, 13, 19, 1)
            p.fillRect(56, 68 - rise, 9, 8, 1); p.fillRect(69, 68 - rise, 9, 8, 1)
            p.fillCircle(67, 43 - rise, 3, 13); p.setPixel(68, 42 - rise, 15)
            p.drawLine(59, 58 - rise, 74, 58 - rise, 2)
        } else if (response == EscapeAction.ShadowHide) {
            p.fillRect(48, 25 + (t % 2) * 2, 37, 52, 1)
            for (let y = 31; y < 75; y += 8) p.drawLine(51, y, 82, y + 4, 6)
            p.fillCircle(21, 54, 6, 3)
        } else {
            // Barely visible dormant ink makes the screen a material object without giving away success.
            p.drawCircle(67, 43, 7, 14); p.fillRect(64, 50, 7, 14, 14)
        }

        // Calibrated gallery photometer: two adjacent physical positions, 59 and 60.
        p.fillRect(101, 31, 27, 59, 1); rounded(p, 104, 34, 21, 53, 14)
        p.fillRect(108, 39, 13, 19, 2); p.print(control == 1 ? "60" : "59", 109, 45, control == 1 ? 10 : 15, image.font5)
        p.fillRect(111, 63, 7, 17, 6); p.fillCircle(114, control == 1 ? 66 : 75, 4, control == 1 ? 10 : 3)
        p.fillRect(104, 87, 21, 5, 6)
    }

    // 7. Four portraits share one physical rail but retain four independent solved beats.
    // The thawed weight is the actual pressure-plate fixture; portraitMask preserves history.
    function portraits(p: Image, control: number, response: number, t: number, ok: boolean, part: number, portraitMask: number, fitted: boolean, sourceState: number) {
        shadow(p, 72, 102, 63)
        // Marble-backed gallery rail with brass top/bottom guides.
        p.fillRect(5, 15, 134, 70, 1); p.fillRect(8, 18, 128, 64, 12)
        p.fillRect(10, 20, 124, 5, 14); p.fillRect(10, 75, 124, 6, 14)
        p.drawLine(12, 23, 132, 23, 15); p.drawLine(12, 77, 132, 77, 6)
        bolt(p, 12, 20); bolt(p, 132, 20); bolt(p, 12, 79); bolt(p, 132, 79)

        for (let i = 0; i < 4; i++) {
            let solvedBeat = (portraitMask & (1 << i)) != 0
            let active = i == part
            let slide = solvedBeat ? -5 : 0
            if (response >= 0 && active) slide += ok ? -Math.min(6, t) : Math.min(4, t % 4)
            let x = 13 + i * 30 + slide
            // Hanging carriage and deep frame.
            p.fillRect(x + 8, 23, 9, 6, 6); p.fillCircle(x + 12, 25, 3, 10)
            p.fillRect(x, 28, 25, 45, 1); p.fillRect(x + 2, 30, 21, 41, active ? 10 : 5)
            p.fillRect(x + 5, 33, 15, 35, solvedBeat ? 9 : 14)
            p.fillCircle(x + 12, 43, 6, i % 2 == 0 ? 15 : 13)
            p.fillRect(x + 8, 49, 9, 15, i % 2 == 0 ? 13 : 8)
            p.fillRect(x + 7, 63, 11, 3, 1); p.fillRect(x + 9, 39, 2, 2, 1); p.fillRect(x + 14, 39, 2, 2, 1)
            // A solved portrait exposes a colored optical filter tab on its rail.
            if (solvedBeat) { let cc = [5,8,3,11][i]; p.fillRect(x + 7, 69, 12, 3, cc); p.setPixel(x + 8, 69, 15) }
            if (active) { p.drawRect(x - 1, 27, 27, 47, 15); p.setPixel(x + 21, 32 + t % 7, 15) }
        }

        // Dual pressure plates. The left plate (value 1) only depresses credibly with the fitted thawed weight.
        p.fillRect(23, 87, 44, 9, 1); p.fillRect(79, 87, 44, 9, 1)
        p.fillRect(27, control == 1 ? 91 : 88, 36, 5, control == 1 ? 10 : 14)
        p.fillRect(83, control == 0 ? 91 : 88, 36, 5, control == 0 ? 3 : 14)
        p.print("1", 43, 86, 1, image.font5); p.print("2", 99, 86, 1, image.font5)
        if (fitted) {
            // Match cargo 3: block weight, steel handle and thawed highlight.
            p.fillRect(35, 76, 20, 13, 1); p.fillRect(38, 77, 14, 11, 6); p.drawRect(38, 77, 14, 11, 15)
            p.fillRect(41, 72, 8, 6, 14); p.fillRect(43, 70, 4, 3, 15); p.setPixel(50, 81, 11)
        } else {
            p.drawRect(37, 76, 17, 12, 6); p.drawLine(39, 86, 52, 78, 3)
        }

        // The source filter cassette appears only while the produced item remains at its source.
        p.fillRect(123, 86, 16, 11, 1)
        if (sourceState == 0 && portraitMask == 15) {
            p.fillRect(124, 86, 5, 8, 5); p.fillRect(129, 84, 5, 10, 8); p.fillRect(134, 86, 4, 8, 3)
            p.drawRect(123, 83, 16, 12, 15)
        } else { p.drawRect(123, 84, 16, 11, 6); p.fillRect(127, 88, 8, 2, 1) }
    }

    // 8. A three-lamp optical mural: part 0 proves additive Y+B blend; part 1 opens the hidden panel
    // only while red is absent. The fitted filter cassette is a visible physical prerequisite.
    function mural(p: Image, control: number, response: number, t: number, ok: boolean, part: number, fitted: boolean) {
        shadow(p, 72, 102, 59)
        // Deep gallery frame and translucent mosaic field.
        p.fillRect(17, 12, 110, 78, 1); p.fillRect(21, 16, 102, 70, 5); p.fillRect(25, 20, 94, 62, 13)
        p.drawRect(27, 22, 90, 58, 15)
        for (let x = 29; x < 116; x += 12) { p.drawLine(x, 24, 112 - Math.idiv(x, 4), 78, x % 3 == 0 ? 8 : 7); p.setPixel(x, 28 + x % 19, 15) }

        let yellow = fitted && (control == 1 || control == 3 || control == 4)
        let blue = fitted && (control == 2 || control == 3 || control == 4)
        let red = control == 5 || fitted && control == 4
        let blend = yellow && blue
        // Three actual filter lamps cast overlapping pools across the mural.
        p.fillCircle(49, 44, 17, yellow ? 5 : 6); p.fillCircle(92, 47, 19, blue ? 8 : 6); p.fillCircle(72, 61, 15, red ? 3 : (blend ? 7 : 6))
        p.fillCircle(49, 44, 9, yellow ? 10 : 4); p.fillCircle(92, 47, 11, blue ? 11 : 9)
        if (blend) { p.fillCircle(70, 52, 14, 7); p.fillCircle(70, 52, 7, 10) }
        if (red) { p.drawLine(61, 30, 82, 72, 3); p.drawLine(81, 30, 61, 72, 3) }

        // Hidden center panel: Blend confirms the green key; Open lifts the panel on beat 12.
        if (response == EscapeAction.MuralBlend || response < 0 && ok && part == 0) {
            p.fillRect(61, 45, 22, 25, 7); p.fillRect(65, 49, 14, 17, 10); p.drawRect(64, 48, 16, 19, 15)
            p.fillCircle(72, 57, 4, 1); p.setPixel(72, 54, 15)
        } else if (response == EscapeAction.MuralOpen || response < 0 && ok && part == 1) {
            let lift = response >= 0 ? Math.min(14, t * 2) : 14
            p.fillRect(59, 47 - lift, 26, 27, 1); p.fillRect(62, 50 - lift, 20, 21, 10); p.drawRect(62, 50 - lift, 20, 21, 15)
            p.fillRect(62, 58, 20, 17, 1); p.fillCircle(72, 65, 7, 11); p.fillCircle(72, 65, 3, 15)
        } else if (response == EscapeAction.MuralDim) {
            for (let i = 0; i < 5; i++) p.fillRect(31 + i * 17, 30 + (i % 2) * 22, 8, 5, 6)
        } else if (response == EscapeAction.MuralSpill) {
            for (let i = 0; i < 7; i++) p.fillCircle(34 + (i * 13 + t * 3) % 72, 28 + (i * 9 + t) % 46, 3, i % 2 == 0 ? 3 : 13)
        }

        // Physical three-filter light rack. Missing cargo is visibly an empty cassette slot.
        p.fillRect(30, 86, 84, 11, 1); p.fillRect(33, 88, 78, 7, 14)
        let cs = [5,8,3]
        for (let i = 0; i < 3; i++) {
            let on = i == 0 ? yellow : i == 1 ? blue : red
            p.fillRect(41 + i * 26, 84, 14, 11, fitted ? cs[i] : 6); p.drawRect(41 + i * 26, 84, 14, 11, 15)
            if (on) p.fillRect(44 + i * 26, 87, 8, 5, 15)
        }
        if (!fitted) { p.drawLine(37, 84, 109, 95, 3); p.drawLine(109, 84, 37, 95, 3) }
        p.fillRect(18, 91, 8, 5, part == 0 ? 10 : 11)
    }

    // 9. Three stone/socket pairings retain their actual color combinations. A successful matched
    // socket releases the separate lens stone output on its source tray.
    function sockets(p: Image, control: number, response: number, t: number, ok: boolean, sourceState: number) {
        shadow(p, 71, 102, 58)
        rounded(p, 15, 19, 112, 70, 1); rounded(p, 19, 23, 104, 62, 14)
        p.fillRect(23, 27, 96, 50, 2); p.drawRect(24, 28, 94, 48, 9)
        let socketColors = [8,8,5]
        let stoneColors = [3,8,5]
        for (let i = 0; i < 3; i++) {
            let x = 38 + i * 33
            p.fillCircle(x, 46, 14, 1); p.fillCircle(x, 46, 10, socketColors[i]); p.drawCircle(x, 46, 11, 15)
            p.fillCircle(x - 3, 42, 3, 11); p.fillCircle(x, 46, 3, 12)
            if (i == control % 3) p.drawCircle(x, 46, 15, 10)
        }
        let selected = control % 3
        let sx = 38 + selected * 33
        let sy = 71
        if (response == EscapeAction.StoneSnap) sy -= Math.min(22, t * 3)
        if (response == EscapeAction.StoneRepel) sx += (selected == 2 ? -1 : 1) * t * 4
        p.fillCircle(sx, sy, 11, 1); p.fillCircle(sx, sy, 8, stoneColors[selected]); p.drawCircle(sx, sy, 9, 15)
        p.fillCircle(sx - 3, sy - 3, 3, 15); p.setPixel(sx + 4, sy + 3, 6)
        if (response == EscapeAction.StoneRepel) { p.drawLine(sx - 8, sy - 9, sx + 8, sy + 9, 3); p.drawLine(sx + 8, sy - 9, sx - 8, sy + 9, 3) }
        if (response == EscapeAction.StoneSnap) { p.fillCircle(38 + selected * 33, 46, 5 + t % 3, 10); p.setPixel(38 + selected * 33, 40, 15) }

        // Lens-stone output cradle mirrors cargo 2's violet glass disc.
        p.fillRect(101, 80, 31, 15, 1); p.fillRect(104, 83, 25, 9, 6)
        if (sourceState == 0 && ok) { p.fillCircle(116, 83, 9, 1); p.fillCircle(116, 83, 6, 13); p.fillCircle(113, 80, 2, 15); p.drawCircle(116, 83, 8, 6) }
        else { p.drawCircle(116, 84, 8, 6); p.fillCircle(116, 84, 2, 1) }
        p.fillRect(12, 91, 119, 5, 6)
    }

    // 10. A brass telescope whose zoom carriage cannot reach 3 until the lens stone is physically fitted.
    function telescope(p: Image, control: number, response: number, t: number, ok: boolean, fitted: boolean) {
        shadow(p, 72, 102, 57)
        // Objective housing and long optical barrel.
        p.fillCircle(28, 31, 14, 1); p.fillCircle(28, 31, 11, 14); p.fillCircle(28, 31, 8, fitted ? 13 : 6)
        if (fitted) { p.fillCircle(28, 31, 6, 13); p.fillCircle(25, 28, 2, 15); p.drawCircle(28, 31, 9, 6) }
        else { p.drawCircle(28, 31, 7, 3); p.drawLine(23, 26, 33, 36, 3) }
        p.fillRect(38, 22, 68, 24, 1); p.fillRect(40, 24, 64, 20, 14); p.fillRect(45, 27, 54, 14, 12)
        p.fillRect(47, 29, 45, 4, 15); p.fillRect(96, 26, 14, 16, 5); p.fillCircle(108, 34, 13, 1); p.fillCircle(108, 34, 9, response == EscapeAction.TelescopeFocus || response < 0 && ok ? 10 : 9)
        p.fillCircle(105, 31, 3, 15)
        // Focusing carriage: zoom 2 versus 3 has a physically different extension.
        let ext = control == 1 && fitted ? 9 : 0
        p.fillRect(74 + ext, 43, 8, 35, 6); p.fillRect(76 + ext, 47, 4, 27, 14)
        p.drawLine(78 + ext, 75, 53, 96, 6); p.drawLine(78 + ext, 75, 103, 96, 6); p.drawLine(78 + ext, 75, 78 + ext, 99, 6)
        p.fillRect(61, 80, 35, 6, 14); p.fillCircle(78 + ext, 78, 5, 10)
        // Zoom scale makes the learner-visible physical input explicit.
        p.fillRect(48, 48, 48, 11, 1); p.fillRect(51, 51, 42, 5, 14)
        p.fillRect(control == 1 && fitted ? 79 : 62, 49, 7, 9, control == 1 && fitted ? 10 : 3)
        p.print(control == 1 && fitted ? "3" : "2", 81, 51, 1, image.font5)

        // Star target: crisp crosshair on Focus, doubled blur on failure/empty lens.
        p.fillRect(116, 14, 23, 54, 2); p.drawRect(117, 15, 21, 52, 9)
        for (let i = 0; i < 5; i++) {
            let yy = 21 + i * 10
            if (response == EscapeAction.TelescopeFocus || response < 0 && ok) { p.fillCircle(127 + (i % 2) * 4, yy, 1, 15); p.setPixel(127 + (i % 2) * 4, yy - 2, 11) }
            else { p.fillCircle(124 + (i % 2) * 5 + t % 2, yy, 2, 13); p.fillCircle(130 + (i % 2) * 3, yy + 2, 2, 6) }
        }
        if (response == EscapeAction.TelescopeFocus) { p.drawLine(121, 45, 135, 45, 10); p.drawLine(128, 38, 128, 52, 10) }
    }

    // 11. Four temperature settings select the actual 19/20/40/41 °C outcomes. Amber thaws the
    // physical weight; blue leaves frost and red overheats it. The released weight matches cargo 3.
    function thermalBath(p: Image, control: number, response: number, t: number, ok: boolean, sourceState: number) {
        shadow(p, 72, 102, 61)
        rounded(p, 12, 32, 120, 60, 1); rounded(p, 16, 35, 112, 54, 14)
        p.fillRect(20, 39, 104, 40, 2); p.drawRect(21, 40, 102, 38, 9)
        let degrees = [19,20,40,41][control % 4]
        let selected = control == 0 ? 0 : control == 3 ? 2 : 1
        let stateColor = response == EscapeAction.ThermalBlue ? 8 : response == EscapeAction.ThermalRed ? 3 : response == EscapeAction.ThermalAmber ? 10 : degrees < 20 ? 8 : degrees > 40 ? 3 : 10
        // Three physical bath wells: cold / amber band / hot.
        let basinColors = [8,10,3]
        for (let i = 0; i < 3; i++) {
            let x = 25 + i * 34
            p.fillRect(x, 44, 29, 31, 1); p.fillRect(x + 2, 46, 25, 27, 6)
            p.fillRect(x + 4, 51, 21, 18, i == selected ? stateColor : basinColors[i])
            p.drawLine(x + 5, 54, x + 23, 54, 15); p.setPixel(x + 7 + (t + i * 3) % 13, 61, 11)
            p.fillCircle(x + 14, 73, 5, i == selected ? stateColor : 6)
        }
        // Temperature selector / thermometer bank.
        p.fillRect(25, 19, 94, 15, 1); p.fillRect(29, 22, 86, 9, 14)
        p.print("" + degrees, 61, 24, 1, image.font5)
        p.fillRect(33 + (control % 4) * 21, 18, 13, 14, control == 0 ? 8 : control == 3 ? 3 : 10)
        p.drawRect(33 + (control % 4) * 21, 18, 13, 14, 15)

        // Weight sits in the selected well during the thermal reaction.
        let wx = 31 + selected * 34, wy = 56
        if (response == EscapeAction.ThermalAmber) wy -= Math.min(11, t * 2)
        p.fillRect(wx, wy, 16, 12, 1); p.fillRect(wx + 2, wy + 1, 12, 10, 6); p.drawRect(wx + 2, wy + 1, 12, 10, 15)
        p.fillRect(wx + 5, wy - 4, 7, 5, 14); p.fillRect(wx + 7, wy - 6, 3, 3, 15)
        if (response == EscapeAction.ThermalBlue) { p.setPixel(wx + 2, wy, 11); p.setPixel(wx + 14, wy + 4, 11); p.fillCircle(wx + 8, wy + 11, 2, 8) }
        if (response == EscapeAction.ThermalRed) { p.fillCircle(wx + 3, wy - 4 - t % 3, 2, 3); p.fillCircle(wx + 13, wy - 7 + t % 2, 2, 4) }
        if (response == EscapeAction.ThermalAmber) { p.fillCircle(wx + 4, wy + 10, 2, 11); p.fillCircle(wx + 13, wy + 11, 1, 11) }

        // Output rack: same thawed weight remains here only while sourceState is 0.
        p.fillRect(104, 80, 31, 16, 1); p.fillRect(107, 83, 25, 10, 6)
        if (sourceState == 0 && ok) {
            p.fillRect(111, 78, 16, 13, 1); p.fillRect(113, 79, 12, 11, 6); p.drawRect(113, 79, 12, 11, 15)
            p.fillRect(116, 75, 7, 5, 14); p.fillRect(118, 73, 3, 3, 15); p.setPixel(124, 84, 11)
        } else { p.drawRect(112, 80, 14, 10, 6); p.drawLine(114, 88, 124, 82, 3) }
        p.fillRect(11, 92, 124, 5, 6)
    }

    // 12. A sealed sample tray sits under a powered electromagnet.  The connector is a real prerequisite:
    // the selected fixture may ask for a magnet, but an empty coil socket cannot visually impersonate one.
    function filings(p: Image, control: number, response: number, t: number, ok: boolean, fitted: boolean) {
        shadow(p, 72, 101, 58)
        // Stone laboratory bench with a recessed filings tray.
        rounded(p, 16, 68, 112, 26, 6); p.fillRect(21, 73, 102, 15, 7); p.drawLine(23, 75, 120, 75, 15)
        glass(p, 28, 45, 82, 31); p.fillRect(33, 68, 72, 5, 5)
        // Electromagnet yoke and visible copper winding.
        p.fillRect(49, 12, 46, 11, 14); p.fillRect(54, 17, 9, 31, 14); p.fillRect(81, 17, 9, 31, 14)
        p.fillRect(58, 17, 28, 6, 6); p.drawRect(50, 12, 44, 10, 15)
        for (let y = 24; y <= 42; y += 5) { p.drawLine(55, y, 62, y, 4); p.drawLine(82, y, 89, y, 4) }
        // Connector socket: the received coil connector closes both copper terminals.
        p.fillRect(98, 17, 26, 17, 1); p.drawRect(99, 18, 24, 15, 6); p.fillCircle(104, 25, 3, 4); p.fillCircle(118, 25, 3, 4)
        if (fitted) { p.drawLine(106, 25, 116, 25, 10); p.drawLine(107, 23, 115, 23, 4); p.fillCircle(111, 24, 3, 15) }
        else { p.drawLine(107, 28, 115, 22, 3); p.drawLine(107, 22, 115, 28, 3) }

        let iron = control == 1 || control == 2
        let asksMagnet = control == 0 || control == 2
        let magnetOn = asksMagnet && fitted
        // Sample puck: wood is warm; iron is steel with a bright top edge.
        let sampleColor = iron ? 14 : 4
        rounded(p, 62, 55, 20, 10, sampleColor); p.drawLine(65, 57, 78, 57, iron ? 15 : 10)
        p.print(iron ? "IRON" : "WOOD", 58, 79, iron ? 15 : 4, image.font5)
        // Power lamp and feed line make requested-vs-actually-powered state unambiguous.
        p.fillCircle(22, 24, 7, 1); p.fillCircle(22, 24, 5, magnetOn ? 10 : asksMagnet ? 3 : 6)
        p.drawLine(29, 24, 49, 18, magnetOn ? 10 : 6)

        let spike = response == EscapeAction.SampleSpike && ok
        for (let i = 0; i < 13; i++) {
            let x = 34 + i * 6
            let baseY = 69 - (i % 2)
            if (spike) {
                let rise = 7 + ((i + t) % 4) * 4
                let lean = x < 72 ? 2 : -2
                p.drawLine(x, baseY, x + lean, baseY - rise, 6); p.setPixel(x + lean, baseY - rise - 1, 10)
            } else {
                p.drawLine(x, baseY, x + (i % 3) - 1, baseY - 3 - (i % 2), 6)
            }
        }
        if (response == EscapeAction.SampleFlat) { p.drawLine(42, 67, 101, 67, 3); p.fillCircle(116, 82, 4, 3) }
        if (spike) p.fillCircle(116, 82, 4, 10)
    }

    // 13. A measured dropper meters the selected count into a glass flask.  Clear, bloom and overflow
    // are separate physical outcomes; the mounted dropper is absent until Balance actually releases it.
    function titration(p: Image, control: number, response: number, t: number, ok: boolean, fitted: boolean) {
        shadow(p, 72, 101, 58)
        // Stand, clamp and burette/dropper cradle.
        p.fillRect(17, 16, 7, 73, 14); p.fillRect(14, 84, 40, 8, 6); p.drawLine(21, 20, 21, 84, 15)
        p.fillRect(21, 24, 66, 6, 6); bolt(p, 24, 27); p.fillRect(77, 21, 12, 13, 14)
        if (fitted) {
            p.fillRect(78, 30, 9, 31, 15); p.fillRect(80, 34, 5, 20, 9); p.fillRect(76, 19, 13, 7, 3)
            for (let y = 35; y <= 51; y += 4) p.drawLine(80, y, 83, y, 1)
            let dy = response >= 0 ? Math.min(12, t * 2) : 0
            p.fillCircle(82, 63 + dy, 3, response == EscapeAction.TitrationOverflow ? 3 : 10)
        } else {
            p.drawRect(78, 31, 9, 30, 6); p.drawLine(79, 57, 86, 34, 3); p.fillCircle(82, 64, 2, 6)
        }
        let drops = [6,7,9,10][control % 4]
        // Flask with narrow neck and liquid chamber.
        p.fillRect(54, 42, 10, 23, 9); p.drawLine(54, 42, 64, 42, 15)
        glass(p, 39, 60, 42, 28); p.fillRect(43, 75, 34, 9, response == EscapeAction.TitrationBloom ? 10 : response == EscapeAction.TitrationOverflow ? 3 : 8)
        if (response == EscapeAction.TitrationBloom) { p.fillCircle(55, 73, 3, 11); p.fillCircle(69, 79, 2, 13); p.fillCircle(62, 69 + t % 3, 2, 10) }
        if (response == EscapeAction.TitrationClear) { p.drawLine(47, 79, 73, 79, 11); p.setPixel(52 + t % 15, 72, 15) }
        if (response == EscapeAction.TitrationOverflow) {
            p.fillRect(39, 84, 42, 5, 3)
            for (let i = 0; i < 4; i++) p.fillCircle(84 + i * 7 + t, 82 + (i % 2) * 5, 3, 3)
        }
        // Mechanical counter makes 6/7/9/10 a visible fixture, not hidden state.
        rounded(p, 95, 39, 29, 35, 14); p.fillRect(100, 45, 19, 15, 1); p.print("" + drops, drops == 10 ? 104 : 107, 48, 10, image.font5)
        for (let i = 0; i < 4; i++) p.fillCircle(101 + i * 6, 67, 2, i == control % 4 ? 10 : 6)
        if (!fitted) p.print("EMPTY", 93, 78, 3, image.font5)
    }

    // 14. Four physical loadings are preserved, including the two different ways to make 5 == 5.
    // A level result releases the measured dropper onto the source tray.
    function balance(p: Image, control: number, response: number, t: number, ok: boolean, sourceState: number) {
        let weight = [7,5,3,5][control % 4]
        shadow(p, 72, 101, 58)
        // Brass laboratory balance with a central knife edge and dial.
        p.fillRect(68, 42, 9, 45, 14); p.fillRect(54, 86, 38, 8, 6); p.fillCircle(72, 43, 10, 5); p.fillCircle(72, 43, 6, 1); p.fillCircle(72, 43, 2, 10)
        let tilt = response == EscapeAction.ScaleLeft ? 8 : response == EscapeAction.ScaleRight ? -8 : response == EscapeAction.ScaleLevel ? 0 : weight > 5 ? 8 : weight < 5 ? -8 : 0
        p.drawLine(24, 45 + tilt, 120, 45 - tilt, 14); p.drawLine(25, 42 + tilt, 119, 42 - tilt, 15)
        p.fillCircle(72, 44, 5, 6)
        p.drawLine(31, 46 + tilt, 37, 72 + tilt, 6); p.drawLine(113, 46 - tilt, 107, 72 - tilt, 6)
        oval(p, 37, 77 + tilt, 22, 6, 5); oval(p, 107, 77 - tilt, 22, 6, 5)
        // Left fixtures use visibly different weight stacks even when totals repeat.
        if (control % 4 == 0) { p.fillRect(27, 63 + tilt, 20, 11, 4); p.fillRect(31, 57 + tilt, 12, 7, 14) }
        else if (control % 4 == 1) { p.fillRect(29, 62 + tilt, 16, 12, 14); p.fillCircle(37, 59 + tilt, 5, 6) }
        else if (control % 4 == 2) { p.fillRect(31, 66 + tilt, 12, 8, 6); p.fillCircle(37, 63 + tilt, 4, 9) }
        else { p.fillRect(28, 67 + tilt, 18, 7, 9); p.fillRect(33, 58 + tilt, 8, 10, 14) }
        p.fillRect(99, 62 - tilt, 16, 12, 14); p.fillCircle(107, 59 - tilt, 5, 6)
        p.print("" + weight, 33, 78 + tilt, 1, image.font5); p.print("5", 104, 78 - tilt, 1, image.font5)
        if (response >= 0) p.fillCircle(72, 29, 5, ok ? 10 : 3)
        // Output tray: the measured dropper exists only after a successful level result.
        p.fillRect(96, 88, 35, 9, 1); p.drawRect(99, 84, 29, 10, 6)
        if (sourceState == 0 && ok) {
            p.fillRect(110, 70, 6, 18, 15); p.fillRect(108, 68, 10, 5, 3); p.fillCircle(113, 90, 4, 10); p.setPixel(113, 94, 8)
        } else { p.drawLine(103, 91, 123, 86, 6) }
    }

    // 15. Four actual wire colors route through a mechanical sorter.  Valid colors seat; green ejects.
    // Successful installation releases the coil connector used by the sample station.
    function wires(p: Image, control: number, response: number, t: number, ok: boolean, sourceState: number) {
        shadow(p, 72, 101, 60)
        rounded(p, 14, 20, 116, 70, 14); p.fillRect(20, 26, 104, 57, 1); p.drawLine(22, 29, 121, 29, 6)
        let colors = [7,13,3,15]
        for (let i = 0; i < 4; i++) {
            let y = 38 + i * 11, c = colors[i], selected = i == control % 4
            p.fillCircle(29, y, 6, c); p.fillCircle(29, y, 2, selected ? 15 : 1)
            let end = 97
            if (response == EscapeAction.WireEject && selected) end = 55 + t * 5
            p.drawLine(35, y, end, y + (i % 2 == 0 ? 3 : -3), c)
            p.drawLine(35, y + 1, end, y + 1 + (i % 2 == 0 ? 3 : -3), selected ? 15 : c)
            if (!(response == EscapeAction.WireEject && selected)) p.fillCircle(101, y + (i % 2 == 0 ? 3 : -3), 4, c)
        }
        // Terminal comb and selected-channel lock lamp.
        p.fillRect(105, 33, 12, 43, 6); p.fillRect(108, 36, 6, 37, 14)
        for (let i = 0; i < 4; i++) p.fillCircle(111, 39 + i * 10, 3, i == control % 4 && response == EscapeAction.WireInstall ? 10 : 1)
        if (response == EscapeAction.WireEject) { p.drawLine(54 + t * 4, 32 + control % 4 * 11, 63 + t * 5, 24 + control % 4 * 8, 3); p.fillCircle(120, 82, 4, 3) }
        if (response == EscapeAction.WireInstall) p.fillCircle(120, 82, 4, 10)
        // Coil-connector source cradle.
        p.fillRect(17, 86, 42, 10, 1); p.drawRect(20, 83, 36, 11, 6)
        if (sourceState == 0 && ok) {
            p.fillRect(23, 85, 5, 6, 4); p.fillRect(49, 85, 5, 6, 4)
            for (let x = 29; x <= 47; x += 4) p.drawCircle(x, 88, 4, 10)
            p.drawLine(27, 88, 51, 88, 15)
        } else p.drawLine(25, 91, 51, 85, 6)
    }

    // 16. The pruning jig presents either a three-point or four-point leaf.  Clipping the valid leaf
    // opens a small propagation drawer containing the repair patch for the vessel.
    function plant(p: Image, control: number, response: number, t: number, ok: boolean, sourceState: number) {
        shadow(p, 71, 101, 55)
        // Ceramic planter and trellis.
        oval(p, 67, 87, 30, 9, 14); p.fillRect(38, 69, 59, 18, 2); oval(p, 67, 69, 29, 8, 6); p.drawLine(67, 70, 67, 24, 7)
        p.drawLine(49, 26, 49, 68, 6); p.drawLine(85, 26, 85, 68, 6); p.drawLine(49, 29, 85, 29, 6); p.drawLine(49, 47, 85, 47, 6)
        let points = control == 0 ? 3 : 4
        // Central target leaf is deliberately larger so the point count can be read physically.
        let lx = 84, ly = 43
        p.drawLine(67, 49, lx - 7, ly + 2, 7)
        if (!(response == EscapeAction.LeafClip && ok)) {
            if (points == 3) { p.drawLine(lx,ly-9,lx-9,ly+5,8); p.drawLine(lx,ly-9,lx+9,ly+5,8); for (let yy = ly-6; yy <= ly+4; yy += 2) { let hw = Math.floor((yy-(ly-9))*9/14); p.fillRect(lx-hw, yy, hw*2+1, 2, 8) }; p.fillRect(lx-7,ly+2,14,5,7) }
            else { p.fillRect(lx-7,ly-7,15,15,8); p.fillRect(lx-10,ly-3,21,7,7); p.fillRect(lx-3,ly-10,7,21,8); p.fillCircle(lx,ly,5,7) }
            p.drawLine(lx-7,ly+2,lx+7,ly+2,9)
        } else {
            p.drawLine(75, 45, 91 + t * 2, 35 - t, 7); p.fillCircle(91 + t * 2, 35 - t, 3, 8)
        }
        // Surrounding foliage stays organic and asymmetric.
        let leavesX = [52,78,55,76,57,74]
        let leavesY = [36,31,53,57,62,65]
        for (let i = 0; i < 6; i++) { p.drawLine(67, leavesY[i]+3, leavesX[i], leavesY[i], 7); oval(p, leavesX[i], leavesY[i], 8, 4, i % 2 ? 8 : 7); p.setPixel(leavesX[i]-2, leavesY[i]-1, 9) }
        // Pruning shears and point selector plaque.
        p.drawLine(109, 21, 98, 45, 15); p.drawLine(114, 23, 101, 46, 15); p.fillCircle(110, 19, 6, 3); p.fillCircle(99, 45, 6, 3); p.fillRect(103, 29, 5, 10, 5)
        rounded(p, 13, 20, 28, 17, 14); p.print(points == 3 ? "3 PT" : "4 PT", 16, 25, 1, image.font5)
        // Propagation drawer / patch source.
        p.fillRect(100, 78, 31, 17, 1); p.drawRect(102, 79, 27, 14, 6); p.fillRect(106, 81, 19, 3, 14)
        if (sourceState == 0 && ok) {
            p.fillRect(106, 84, 18, 8, 11); p.drawRect(106, 84, 18, 8, 15); p.drawLine(108, 86, 122, 90, 3); p.drawLine(108, 90, 122, 86, 3)
        } else p.drawLine(106, 90, 124, 84, 6)
        if (response == EscapeAction.LeafKeep) p.fillCircle(116, 72, 4, 3)
        else if (response == EscapeAction.LeafClip) p.fillCircle(116, 72, 4, 10)
    }

    // 17. The vessel's crack and removable repair plate are explicit.  Heat is a separate burner control;
    // only a repaired and hot vessel reveals the hidden mark through its inspection window.
    function heatVessel(p: Image, control: number, response: number, t: number, ok: boolean, fitted: boolean) {
        shadow(p, 72, 102, 58)
        // Burner base: the five fixtures preserve OUT / LOW / OUT / ON / HIGH exactly.
        p.fillRect(19, 87, 106, 8, 1); p.fillRect(27, 80, 90, 8, 14); p.drawLine(30, 82, 114, 82, 15)
        let flame = [0,1,0,2,3][control % 5]
        if (flame > 0) {
            let fh = flame == 1 ? 7 : flame == 2 ? 12 : 17
            for (let i = 0; i < 4; i++) { let x = 49 + i * 15; let wobble = (i+t)%3; p.fillCircle(x,80-fh+5-wobble,5, flame == 3 ? 3 : 4); p.fillRect(x-4,80-fh+5-wobble,9,fh-4+wobble, flame == 3 ? 3 : 4); p.fillCircle(x,77,3,10); p.fillRect(x-2,77,5,4,10) }
        }
        // Rounded copper/brass vessel with glass inspection port.
        oval(p, 72, 76, 39, 17, 14); p.fillRect(33, 45, 78, 31, 14); p.drawLine(39, 49, 104, 49, 15); p.drawLine(38, 73, 106, 73, 6)
        oval(p, 72, 45, 39, 15, 5); oval(p, 72, 47, 32, 10, 1)
        p.fillRect(57, 22, 30, 20, 14); oval(p, 72, 22, 15, 5, 6); p.fillRect(68, 13, 8, 10, 6); p.fillCircle(72, 11, 5, 10)
        // Inspection window.
        p.fillCircle(72, 61, 13, 1); p.fillCircle(72, 61, 10, response == EscapeAction.VesselReveal || response < 0 && ok ? 10 : 6); p.drawCircle(72, 61, 12, 15)
        if (response == EscapeAction.VesselReveal || response < 0 && ok) { p.fillCircle(72, 61, 5, 4); p.drawLine(68,61,72,55,15); p.drawLine(72,55,77,63,15); p.drawLine(77,63,68,61,15) }
        else if (response == EscapeAction.VesselBlank) p.drawLine(66, 61, 78, 61, 9)
        // Crack on right wall, covered only when the patch is actually fitted.
        if (fitted) {
            p.fillRect(101, 54, 18, 14, 11); p.drawRect(101, 54, 18, 14, 15); p.drawLine(104, 57, 116, 65, 3); p.drawLine(104, 65, 116, 57, 3)
            bolt(p, 104, 56); bolt(p, 116, 66)
        } else {
            p.drawLine(105, 53, 112, 60, 1); p.drawLine(112, 60, 107, 67, 1); p.drawLine(107, 67, 118, 72, 1)
            p.drawLine(106, 53, 113, 60, 3); p.drawLine(113, 60, 108, 67, 3); p.drawLine(108, 67, 119, 72, 3)
        }
        if (response == EscapeAction.VesselLeak) for (let i = 0; i < 4; i++) p.fillCircle(117 + Math.min(9,t*2), 65 + i * 6, 3, 11)
        if ((response == EscapeAction.VesselReveal || response < 0 && ok) && flame > 0) for (let i = 0; i < 3; i++) p.fillCircle(59 + i * 12, 35 - ((t + i * 2) % 6), 3, 11)
        // Five-position burner selector.
        for (let i = 0; i < 5; i++) p.fillCircle(33 + i * 16, 91, 3, i == control % 5 ? 10 : 6)
    }

    // 18. Pedal receiver: the selected fixture is the real RPM (39/40/79/80), not a generic speed knob.
    // A clear 80-RPM lock releases the Signal Module used by the interference mixer.
    function pedalRadio(p: Image, control: number, response: number, t: number, ok: boolean, idle: number, parked: boolean, sourceState: number) {
        let rpm = [39,40,79,80][control % 4]
        shadow(p, 71, 101, 59)
        // Bicycle-like pedal generator and chain drive.
        p.fillRect(12, 86, 57, 8, 1); p.fillRect(16, 83, 49, 6, 14); bolt(p, 19, 87); bolt(p, 61, 87)
        let spin = parked && ok ? idle : response >= 0 ? t * (rpm >= 79 ? 2 : 1) : idle % 4
        p.fillCircle(34, 58, 24, 1); p.fillCircle(34, 58, 21, 14); p.drawCircle(34, 58, 19, 6)
        for (let i = 0; i < 6; i++) {
            let q = (i + spin) % 6
            let ex = q == 0 ? 34 : q == 1 ? 49 : q == 2 ? 49 : q == 3 ? 34 : q == 4 ? 19 : 19
            let ey = q == 0 ? 40 : q == 1 ? 48 : q == 2 ? 68 : q == 3 ? 76 : q == 4 ? 68 : 48
            p.drawLine(34, 58, ex, ey, 6)
        }
        p.fillCircle(34, 58, 6, 10)
        let pedalSide = spin % 2 == 0 ? -1 : 1
        p.drawLine(34, 58, 34 + pedalSide * 18, 68, 5); p.fillRect(32 + pedalSide * 18, 66, 10, 4, 14)
        p.drawLine(53, 51, 68, 45, 6); p.drawLine(53, 67, 68, 71, 6)
        p.fillCircle(69, 58, 13, 1); p.fillCircle(69, 58, 10, 5); p.fillCircle(69, 58, 4, 10)
        p.drawLine(56, 49, 68, 45, 4); p.drawLine(56, 68, 68, 71, 4)

        // Receiver cabinet: analogue RPM gauge above a signal scope.
        rounded(p, 76, 17, 57, 68, 14); p.fillRect(80, 21, 49, 60, 2)
        p.fillRect(84, 25, 40, 22, 1); p.drawRect(84, 25, 40, 22, 6)
        p.print("RPM", 87, 28, 15, image.font5); p.print("" + rpm, 103, 36, rpm >= 80 ? 10 : rpm >= 40 ? 9 : 3, image.font5)
        // Four detents remain physically distinct even where threshold outcomes are adjacent.
        for (let i = 0; i < 4; i++) p.fillCircle(88 + i * 11, 50, 3, i == control % 4 ? 10 : 6)
        p.drawLine(88, 54, 121, 54, 6)
        // Signal scope: dead = flat, static = broken noise, clear = coherent stepped wave.
        p.fillRect(84, 58, 40, 17, 1); p.drawRect(84, 58, 40, 17, 6)
        if (response == EscapeAction.ReceiverDead || response < 0 && !parked) {
            p.drawLine(88, 67, 120, 67, 6)
            if (response == EscapeAction.ReceiverDead) p.fillCircle(121, 67, 2, 3)
        } else if (response == EscapeAction.ReceiverStatic) {
            for (let i = 0; i < 8; i++) { let x = 87 + i * 4; p.drawLine(x, 67, x + 3, 61 + ((i + t) % 4) * 3, i % 2 ? 3 : 14) }
        } else {
            for (let i = 0; i < 8; i++) { let x = 87 + i * 4; let y = 66 + ((i + t) % 4 == 0 ? -5 : (i + t) % 4 == 2 ? 5 : 0); p.drawLine(x, 66, x + 3, y, 10) }
            p.fillCircle(121, 61, 2, 10)
        }
        p.drawLine(69, 58, 78, 58, 4); p.setPixel(81, 58, 15)

        // Signal-module output cradle. sourceState alone is not proof of production;
        // the module appears only during/after a genuine ReceiverClear success.
        p.fillRect(85, 83, 43, 13, 1); p.drawRect(88, 81, 37, 12, 6)
        if (sourceState == 0 && ok) {
            p.fillRect(96, 83, 21, 8, 6); p.drawRect(96, 83, 21, 8, 15)
            p.fillCircle(102, 87, 2, 10); p.drawLine(113, 83, 117, 79, 15); p.setPixel(112 + t % 3, 88, 8)
        } else p.drawLine(94, 90, 120, 84, 6)
    }

    // 19. Interference mixer: Scratch, Beep, Hum, All Three and Quiet are five actual signal states.
    // Without the installed Signal Module all three interference sources remain physically active.
    function horns(p: Image, control: number, response: number, t: number, ok: boolean, fitted: boolean) {
        shadow(p, 72, 101, 59)
        rounded(p, 13, 18, 118, 73, 14); p.fillRect(18, 23, 108, 62, 2)
        // Installed signal module matches cargo 8; empty bay is impossible to mistake for QUIET.
        p.fillRect(21, 27, 29, 20, 1); p.drawRect(21, 27, 29, 20, 6)
        if (fitted) {
            p.fillRect(25, 31, 21, 12, 6); p.drawRect(25, 31, 21, 12, 15); p.fillCircle(31, 37, 3, 10)
            p.drawLine(41, 32, 47, 26, 15); p.setPixel(40, 39, 8)
        } else {
            p.drawLine(25, 31, 45, 43, 6); p.drawLine(45, 31, 25, 43, 6); p.print("EMPTY", 22, 49, 3, image.font5)
        }

        let forceAll = !fitted
        let scratch = forceAll || control == 0 || control == 3
        let beep = forceAll || control == 1 || control == 3
        let hum = forceAll || control == 2 || control == 3
        // Scratch channel: tiny record + stylus.
        p.fillCircle(66, 36, 11, 1); p.fillCircle(66, 36, 9, scratch ? 5 : 6); p.drawCircle(66, 36, 6, 14); p.fillCircle(66, 36, 2, 15)
        p.drawLine(74, 27, 70, 36, scratch ? 3 : 6); p.fillCircle(75, 26, 3, 14)
        // Beep channel: annunciator horn.
        p.fillRect(86, 28, 21, 16, 1); p.fillRect(89, 30, 15, 12, beep ? 10 : 6); p.fillRect(92, 32, 9, 8, 1); p.fillCircle(96, 36, 3, beep ? 10 : 6)
        // Hum channel: transformer coil.
        p.fillRect(111, 27, 10, 20, 6); for (let y = 30; y <= 43; y += 4) p.drawLine(108, y, 124, y, hum ? 13 : 6)
        p.fillRect(113, 30, 6, 14, 1)

        // Mixer bus and five-position selector.
        p.drawLine(58, 52, 119, 52, 14); p.drawLine(58, 54, 119, 54, 6)
        for (let i = 0; i < 5; i++) p.fillCircle(34 + i * 19, 75, 4, i == control % 5 ? 10 : 6)
        p.fillCircle(34 + (control % 5) * 19, 75, 2, 15)
        p.print(control == 4 ? "QUIET" : control == 3 ? "ALL" : control == 0 ? "SCR" : control == 1 ? "BEEP" : "HUM", 54, 82, 15, image.font5)

        // Output monitor: distortion stays visibly noisy; clear state collapses to a clean carrier.
        p.fillRect(56, 58, 66, 12, 1); p.drawRect(56, 58, 66, 12, 6)
        if (response == EscapeAction.NoiseClear) {
            p.drawLine(60, 64, 118, 64, 10); for (let i = 0; i < 5; i++) p.setPixel(64 + i * 12, 62 + (i+t)%3, 15)
        } else if (response == EscapeAction.NoiseDistort || scratch || beep || hum) {
            for (let i = 0; i < 9; i++) { let x = 60 + i * 6; let y = 64 + ((i * 3 + t) % 7) - 3; p.drawLine(x, 64, x + 5, y, response >= 0 ? 3 : 9) }
        } else p.drawLine(60, 64, 118, 64, 9)
    }

    // 20. Message printer: five selector detents expose NO SIGNAL / RADIO / CABLE / BOTH / NO SIGNAL.
    // A valid feed produces the physical Message Strip carried to the pneumatic tube.
    function printer(p: Image, control: number, response: number, t: number, ok: boolean, sourceState: number) {
        shadow(p, 72, 101, 58)
        rounded(p, 18, 25, 108, 63, 14); p.fillRect(23, 30, 98, 53, 2)
        // Two actual input jacks and a five-detent rotary selector.
        p.fillRect(28, 35, 26, 24, 1); p.drawRect(28, 35, 26, 24, 6)
        p.fillCircle(36, 46, 5, control == 1 || control == 3 ? 10 : 6); p.fillCircle(47, 46, 5, control == 2 || control == 3 ? 11 : 6)
        p.print("R", 34, 43, 15, image.font5); p.print("C", 45, 43, 15, image.font5)
        for (let i = 0; i < 5; i++) p.fillCircle(31 + i * 6, 64, 2, i == control % 5 ? 10 : 6)
        // Print head and paper path.
        p.fillRect(62, 34, 50, 21, 1); p.fillRect(66, 38, 42, 13, 12); p.drawLine(69, 41, 103, 41, 15)
        let head = response == EscapeAction.PrinterFeed ? 68 + (t * 5) % 34 : response == EscapeAction.PrinterJam ? 86 + (t % 2) * 3 : 72
        p.fillRect(head, 35, 7, 19, 6); p.fillRect(head + 2, 39, 3, 11, response == EscapeAction.PrinterJam ? 3 : 10)
        let paper = response == EscapeAction.PrinterFeed ? 7 + t * 4 : response == EscapeAction.PrinterJam ? 12 : 5
        p.fillRect(67, 55, 39, Math.min(31,paper), 15); p.drawRect(67, 55, 39, Math.min(31,paper), 6)
        if (paper > 10) { p.drawLine(72, 62, 99, 62, 1); p.drawLine(72, 68, 95, 68, 1); p.drawLine(72, 74, 101, 74, 1) }
        if (response == EscapeAction.PrinterJam) { p.drawLine(68, 58, 104, 77, 3); p.fillCircle(110, 61, 4, 3) }
        else if (response == EscapeAction.PrinterFeed) p.fillCircle(114, 61, 4, 10)
        // Message-strip source slot. It does not exist until a successful feed.
        p.fillRect(20, 86, 43, 10, 1); p.drawRect(23, 83, 37, 11, 6)
        if (sourceState == 0 && ok) {
            p.fillRect(29, 84, 25, 8, 15); p.drawRect(29, 84, 25, 8, 6); p.drawLine(33, 87, 50, 87, 1); p.drawLine(33, 90, 47, 90, 1)
        } else p.drawLine(28, 91, 55, 85, 6)
    }

    // 21. Pneumatic route selector: Drain, Route A and Route B are separate tubes.
    // The printed Message Strip must be visibly installed before either launch route can work.
    function tubes(p: Image, control: number, response: number, t: number, ok: boolean, fitted: boolean) {
        shadow(p, 72, 101, 59)
        // Three real route pipes: drain drops down, A rises, B runs low.
        p.fillRect(16, 87, 112, 8, 1); p.fillRect(20, 84, 104, 5, 14)
        p.fillRect(25, 22, 8, 60, 9); p.fillRect(28, 22, 3, 60, 15)
        p.drawLine(31, 26, 96, 26, 9); p.drawLine(31, 29, 96, 29, 15)
        p.drawLine(31, 64, 96, 64, 9); p.drawLine(31, 67, 96, 67, 15)
        p.drawLine(96, 26, 117, 43, 9); p.drawLine(96, 29, 114, 44, 15)
        p.drawLine(96, 64, 117, 49, 9); p.drawLine(96, 67, 114, 50, 15)
        p.fillRect(113, 42, 8, 39, 9); p.fillRect(116, 45, 3, 33, 15)
        // Message strip insertion gate.
        p.fillRect(45, 39, 48, 18, 1); p.drawRect(45, 39, 48, 18, 6)
        if (fitted) {
            p.fillRect(54, 42, 30, 12, 15); p.drawRect(54, 42, 30, 12, 6); p.drawLine(58, 46, 80, 46, 1); p.drawLine(58, 50, 76, 50, 1)
        } else { p.drawLine(53, 43, 85, 53, 6); p.print("STRIP", 57, 44, 6, image.font5) }
        // Route selector plate.
        for (let i = 0; i < 3; i++) p.fillCircle(43 + i * 27, 78, 5, i == control % 3 ? 10 : 6)
        p.print(control % 3 == 0 ? "DRAIN" : control % 3 == 1 ? "A" : "B", 90, 77, 15, image.font5)

        if (response == EscapeAction.TubeLaunch) {
            let routeY = control % 3 == 1 ? 27 : 65
            let cx = 34 + t * 11
            p.fillCircle(Math.min(113,cx), routeY, 6, control % 3 == 1 ? 10 : 11); p.drawCircle(Math.min(113,cx), routeY, 5, 15)
            p.fillRect(48, routeY - 1, Math.min(62,t*9), 2, control % 3 == 1 ? 10 : 11)
        } else if (response == EscapeAction.TubeDrain) {
            let cy = 33 + t * 8
            p.fillCircle(29, Math.min(81,cy), 6, 3); p.drawCircle(29, Math.min(81,cy), 5, 15)
            if (t > 4) { p.fillCircle(23, 82, 3, 11); p.fillCircle(36, 87, 2, 11) }
        } else {
            let sy = control % 3 == 1 ? 27 : control % 3 == 2 ? 65 : 52
            p.fillCircle(35, sy, 4, fitted ? 10 : 6)
        }
    }

    // 22. Two-stage pressure rig. Part 0 stabilizes at 48..50; part 1 releases only at 20
    // after that learner-owned pressureReady state was earned. Both stages keep their true fixtures visible.
    function pressure(p: Image, control: number, response: number, t: number, ok: boolean, part: number) {
        let value = part == 0 ? [47,48,50,51][control % 4] : [20,30,20,30][control % 4]
        shadow(p, 72, 101, 59)
        rounded(p, 13, 18, 118, 73, 14); p.fillRect(18, 23, 108, 62, 2)
        // Large gauge with numeric readout and four physical regulator detents.
        p.fillCircle(48, 52, 27, 1); p.fillCircle(48, 52, 24, 15); p.fillCircle(48, 52, 20, 12); p.drawCircle(48, 52, 22, 6)
        for (let i = 0; i < 5; i++) p.fillRect(34 + i * 7, 31 + (i%2)*2, 2, 5, 6)
        let needle = value <= 20 ? -14 : value >= 50 ? 12 : value >= 48 ? 7 : -5
        p.drawLine(48, 52, 48 + needle, 39, response == EscapeAction.SealLeak || response == EscapeAction.SealVent ? 3 : 10)
        p.fillCircle(48, 52, 4, 6); p.print("" + value, 40, 62, 1, image.font5)
        p.print(part == 0 ? "STABLE" : "RELEASE", 24, 78, part == 0 ? 10 : 11, image.font5)

        // Pressure cylinder / seal stack on the right.
        p.fillRect(82, 28, 34, 48, 1); p.fillRect(87, 24, 24, 56, 14); p.drawRect(87, 24, 24, 56, 6)
        p.fillRect(91, 30, 16, 39, 12); p.fillRect(94, 34, 10, 31, 9)
        let retract = response == EscapeAction.SealRetract ? t * 4 : 0
        p.fillRect(84, 42 - retract, 30, 11, 5); p.fillRect(88, 45 - retract, 22, 5, response == EscapeAction.SealStable || response == EscapeAction.SealRetract ? 10 : 6)
        bolt(p, 89, 26); bolt(p, 109, 77)
        // Four detents are preserved, including the duplicate 20/30 values in release stage.
        for (let i = 0; i < 4; i++) p.fillCircle(82 + i * 12, 87, 4, i == control % 4 ? 10 : 6)
        if (response == EscapeAction.SealStable) {
            p.fillCircle(119, 34, 5, 10); p.drawLine(115, 36, 122, 29, 15)
        } else if (response == EscapeAction.SealLeak) {
            for (let i = 0; i < 4; i++) p.fillCircle(114 + t * 2, 40 + i * 8, 3, 11)
            p.fillCircle(121, 34, 5, 3)
        } else if (response == EscapeAction.SealRetract) {
            p.fillRect(116, 39, 10 + t * 2, 22, 10); p.fillCircle(121, 34, 5, 10)
        } else if (response == EscapeAction.SealVent) {
            for (let i = 0; i < 5; i++) p.drawLine(115, 48 + i * 4, 126 + t, 43 + i * 5, 11)
            p.fillCircle(121, 34, 5, 3)
        }
    }

    // 23. Pitch bridge: part 0 shows the selected +/-10 or +/-25 actuator against the actual accumulated pitch;
    // part 1 judges that same pitch as Down / Level / Up. No canned response replaces the real pitch geometry.
    function plank(p: Image, control: number, response: number, t: number, ok: boolean, pitch: number, part: number) {
        let tilt = Math.max(-16, Math.min(16, Math.idiv(pitch, 2)))
        let feedback = part == 1
        shadow(p, 72, 101, 61)
        // Suspension towers and cables establish a real bridge rather than a single line.
        p.fillRect(15, 27, 7, 65, 6); p.fillRect(122, 27, 7, 65, 6); p.fillRect(17, 28, 3, 58, 14); p.fillRect(124, 28, 3, 58, 14)
        p.fillRect(11, 89, 18, 7, 1); p.fillRect(115, 89, 18, 7, 1)
        p.drawLine(20, 31, 72, 19, 9); p.drawLine(72, 19, 126, 31, 9); p.fillCircle(72, 19, 5, 14)
        // Deck obeys actual pitch. Positive pitch raises left / lowers right exactly as before.
        p.drawLine(21, 65 + tilt, 122, 65 - tilt, 5); p.drawLine(21, 70 + tilt, 122, 70 - tilt, 14)
        for (let x = 28; x <= 112; x += 14) {
            let local = Math.idiv((x - 21) * (-2 * tilt), 101) + tilt
            p.drawLine(x, 66 + local, x + 9, 66 + local, 15)
            p.drawLine(x, 33, x, 63 + local, 6)
        }
        // Central plumb reference makes zero visibly objective.
        p.drawLine(72, 21, 72, 82, 9); p.fillCircle(72, 83, 6, 10); p.fillCircle(72, 83, 2, 15)
        p.drawLine(61, 54, 83, 54, 6); p.setPixel(72, 52, 15)
        // Part 0: four actuator choices, with actual signed magnitude printed.
        if (!feedback) {
            let changes = [10,25,-10,-25]
            let delta = changes[control % 4]
            p.fillRect(34, 86, 76, 11, 1); p.drawRect(36, 84, 72, 11, 6)
            for (let i = 0; i < 4; i++) p.fillCircle(43 + i * 18, 89, 3, i == control % 4 ? 10 : 6)
            p.print(delta > 0 ? "+" + delta : "" + delta, 86, 86, delta > 0 ? 10 : 11, image.font5)
            // Directional hydraulic actuator sits under the deck.
            let ax = delta > 0 ? 42 : 101
            p.fillRect(ax - 5, 72, 10, 16, 6); p.fillRect(ax - 2, 68, 4, 16, delta > 0 ? 10 : 11)
        } else {
            // Part 1: feedback follows actual pitch and response, not selected fixture.
            let state = pitch == 0 ? 0 : pitch < 0 ? -1 : 1
            p.fillRect(34, 86, 76, 11, 1); p.drawRect(36, 84, 72, 11, 6)
            p.print(state == 0 ? "LEVEL" : state < 0 ? "DOWN" : "UP", 56, 86, state == 0 ? 10 : 3, image.font5)
            if (response == EscapeAction.PitchLevel) p.fillCircle(105, 88, 4, 10)
            else if (response == EscapeAction.PitchDown || response == EscapeAction.PitchUp) p.fillCircle(105, 88, 4, 3)
        }
        // Moving inspection trolley follows a successful level result; otherwise it rests on the low side.
        let bx = response == EscapeAction.PitchLevel && feedback ? 72 : pitch > 0 ? 103 : pitch < 0 ? 40 : 72
        let by = 57 + Math.idiv((bx - 21) * (-2 * tilt), 101) + tilt
        if (response >= 0 && feedback && response != EscapeAction.PitchLevel) bx += (t % 2) * (pitch < 0 ? -2 : 2)
        p.fillCircle(bx, by, 7, feedback && response == EscapeAction.PitchLevel ? 10 : 5); p.fillCircle(bx - 2, by - 2, 2, 15)
    }

    // 24. Remote sensor console: four fixtures are SENSOR 1 / SENSOR 2 / SENSOR 3 / NO SENSOR.
    // A successful numbered reading releases the physical Sensor Card for the shutter bank.
    function sensors(p: Image, control: number, response: number, t: number, ok: boolean, sourceState: number) {
        shadow(p, 72, 101, 59)
        rounded(p, 15, 18, 114, 72, 14); p.fillRect(20, 23, 104, 62, 2)
        // Three remote mast channels with individual lamp housings and cable runs.
        p.fillRect(22, 28, 8, 50, 6); p.fillRect(25, 31, 3, 43, 14)
        for (let i = 0; i < 3; i++) {
            let y = 34 + i * 20
            p.drawLine(30, y, 96, y, 8); p.drawLine(31, y + 2, 96, y + 2, 1)
            for (let x = 39; x <= 88; x += 13) p.fillRect(x, y - 2, 2, 5, 6)
            p.fillRect(96, y - 9, 24, 18, 1); p.fillRect(99, y - 6, 18, 12, 12); p.drawRect(99, y - 6, 18, 12, 6)
            let selected = control < 3 && i == control
            let lit = response >= EscapeAction.SensorLamp1 && response <= EscapeAction.SensorLamp3 && i == response - EscapeAction.SensorLamp1
            p.fillCircle(108, y, 5, lit ? 10 : selected && response >= 0 ? 3 : selected ? 9 : 6)
            p.fillCircle(108, y, 2, lit ? 15 : 1); p.print("" + (i + 1), 101, y - 3, 15, image.font5)
            if (lit) {
                let beamEnd = Math.min(95, 40 + t * 8)
                p.drawLine(35, y, beamEnd, y, 11); p.setPixel(Math.max(36, beamEnd - 4), y - 1, 15)
            }
        }
        // Four-position sensor selector: the fourth detent is deliberately disconnected/dark.
        p.fillRect(23, 82, 69, 13, 1); p.drawRect(25, 80, 65, 13, 6)
        for (let i = 0; i < 4; i++) p.fillCircle(34 + i * 15, 86, 4, i == control % 4 ? (i == 3 ? 3 : 10) : 6)
        p.print(control % 4 == 3 ? "NONE" : "S" + (control % 4 + 1), 94, 83, control % 4 == 3 ? 3 : 10, image.font5)
        if (response == EscapeAction.SensorDark) {
            p.fillRect(96, 76, 24, 7, 3); p.drawLine(99, 79, 116, 79, 1)
        }
        // Output dock mirrors the Sensor Card contacts but never fabricates the cargo item before success.
        p.fillRect(15, 96, 39, 6, 1); p.drawRect(18, 92, 33, 8, 6)
        if (sourceState == 0 && ok) { p.fillRect(23, 94, 23, 4, 14); p.fillRect(27, 95, 15, 2, 10) }
        else p.drawLine(23, 98, 46, 93, 6)
    }

    // 25. Shutter bank: five controls include WINDOW A, WINDOW B, RED HAZARD, inert control and WINDOW A again.
    // The Sensor Card is a real prerequisite and is shown in a dedicated reader socket.
    function shutters(p: Image, control: number, response: number, t: number, ok: boolean, fitted: boolean) {
        shadow(p, 72, 101, 60)
        rounded(p, 10, 13, 124, 81, 14); p.fillRect(15, 18, 114, 71, 1)
        // Sensor-card reader.
        p.fillRect(15, 20, 27, 20, 2); p.drawRect(15, 20, 27, 20, 6)
        if (fitted) { p.fillRect(19, 23, 19, 14, 14); p.drawRect(19, 23, 19, 14, 15); p.fillCircle(28, 29, 4, 8); p.fillRect(22, 35, 12, 2, 10) }
        else { p.drawRect(20, 24, 17, 12, 6); p.drawLine(22, 34, 35, 25, 6) }
        p.fillCircle(45, 29, 4, fitted ? 10 : 3)
        // Three architectural shutter bays.
        for (let i = 0; i < 3; i++) {
            let x = 48 + i * 27
            let chosen = (control % 5 == 0 || control % 5 == 4) ? i == 0 : control % 5 == 1 ? i == 1 : false
            let opening = response == EscapeAction.ShutterOpen && ok && chosen ? Math.min(30,t * 5) : 0
            p.fillRect(x, 24, 23, 54, 12); p.drawRect(x, 24, 23, 54, 6)
            p.fillRect(x + 3, 27, 17, 46, 8)
            for (let y = 29 - opening; y <= 69 - opening; y += 7) p.fillRect(x + 4, y, 15, 3, response == EscapeAction.ShutterWarn ? 3 : 6)
            p.fillRect(x + 8, 75, 7, 5, 5)
            if (opening > 8) { p.fillRect(x + 3, 68, 17, Math.min(9,opening-7), 15); p.drawLine(x + 5, 69, x + 18, 59, 11) }
        }
        // Five controls, including the deliberately dangerous red control and inert detent.
        p.fillRect(18, 82, 104, 13, 2); p.drawRect(18, 82, 104, 13, 6)
        for (let i = 0; i < 5; i++) p.fillCircle(28 + i * 21, 88, 4, i == control % 5 ? (i == 2 ? 3 : i == 3 ? 6 : 10) : 5)
        if (response == EscapeAction.ShutterWarn) {
            p.fillCircle(116, 20, 7, 3); p.fillCircle(116, 20, 3, 15); p.drawLine(108, 47, 124, 47, 3); p.drawLine(116, 39, 116, 55, 3)
        } else if (response == EscapeAction.ShutterClosed) {
            p.fillRect(105, 18, 18, 6, 3); p.drawLine(108, 21, 120, 21, 15)
        }
    }

    // 26. Star-wire alignment: five fixtures encode front/middle/back mismatch or both all-match variants.
    // Successful ignition releases the Pattern Plate used by the rock comparison station.
    function constellation(p: Image, control: number, response: number, t: number, ok: boolean, sourceState: number) {
        shadow(p, 72, 101, 56)
        rounded(p, 15, 12, 114, 82, 14); p.fillRect(20, 17, 104, 72, 1)
        p.fillRect(24, 21, 96, 58, 12); p.drawRect(24, 21, 96, 58, 6)
        let miss = control % 5
        for (let i = 0; i < 3; i++) {
            let r = 27 - i * 8
            let mismatch = miss == i
            let active = !mismatch
            let phase = response == EscapeAction.StarIgnite && ok ? t + i * 2 : i * 2
            p.drawCircle(72, 50, r, mismatch ? 3 : (i == 0 ? 8 : i == 1 ? 13 : 10))
            for (let n = 0; n < 4; n++) {
                let q = (n + phase) % 4
                let x = q == 0 ? 72 : q == 1 ? 72 + r - 2 : q == 2 ? 72 : 72 - r + 2
                let y = q == 0 ? 50 - r + 2 : q == 1 ? 50 : q == 2 ? 50 + r - 2 : 50
                p.fillCircle(x, y, response == EscapeAction.StarIgnite && active ? 3 : 2, active ? 15 : 3)
            }
            if (mismatch) p.drawLine(68 - i * 3, 50 - r + 3, 76 + i * 3, 50 - r + 9, 3)
        }
        p.fillCircle(72, 50, 7, response == EscapeAction.StarFizzle ? 3 : 15); p.fillCircle(72, 50, 3, 10)
        if (response == EscapeAction.StarIgnite) {
            for (let i = 0; i < 6; i++) p.drawLine(72, 50, 39 + i * 13, 20 + (i % 3) * 29, i % 2 ? 10 : 11)
        } else if (response == EscapeAction.StarFizzle) {
            p.drawLine(62, 42, 82, 58, 3); p.drawLine(82, 42, 62, 58, 3)
        }
        // Five detents preserve the duplicate all-match configurations 3 and 4.
        p.fillRect(34, 82, 76, 11, 2); for (let i = 0; i < 5; i++) p.fillCircle(42 + i * 15, 87, 3, i == control % 5 ? 10 : 6)
        // Pattern Plate output dock.
        p.fillRect(12, 94, 41, 7, 1); p.drawRect(17, 90, 31, 9, 6)
        if (sourceState == 0 && ok) { p.fillRect(22, 92, 21, 5, 6); p.fillCircle(28, 94, 2, 8); p.fillCircle(38, 94, 2, 3) }
    }

    // 27. Rock path compares two inset stones. The Pattern Plate is a real prerequisite.
    // Fixtures preserve neither/color/pattern/both/color-only alternatives exactly.
    function rockPath(p: Image, control: number, response: number, t: number, ok: boolean, fitted: boolean) {
        shadow(p, 71, 102, 61)
        p.fillRect(7, 31, 130, 58, 12); p.drawLine(8, 37, 136, 50, 14); p.drawLine(10, 76, 132, 62, 14)
        // Pattern-plate reader at the top of the path.
        p.fillRect(45, 6, 54, 22, 1); p.drawRect(45, 6, 54, 22, 6)
        if (fitted) { p.fillRect(50, 10, 44, 14, 6); p.fillCircle(61, 17, 4, 8); p.fillCircle(84, 17, 4, 3); p.drawLine(68, 17, 77, 17, 10) }
        else { p.drawRect(52, 11, 40, 12, 6); p.drawLine(55, 21, 89, 12, 6) }
        let sameColor = control == 1 || control == 3 || control == 4
        let samePattern = control == 2 || control == 3
        // Five stepping stones physically expose color and mark comparison.
        for (let i = 0; i < 5; i++) {
            let x = 15 + i * 24
            let baseY = 67 - (i % 2) * 18
            let y = baseY + (response == EscapeAction.RockCollapse && i > 2 ? Math.min(20,t * 4) : 0)
            let pathGood = response == EscapeAction.RockBeam && ok
            let c = pathGood ? (i % 2 == 0 ? 8 : 10) : i == control % 5 ? 10 : (i % 2 == 0 ? 6 : 14)
            p.fillCircle(x, y, 14, c); p.drawCircle(x, y, 13, 1)
            let mark = (control + i) % 3
            if (mark == 0) p.fillRect(x - 6, y - 5, 9, 3, 15)
            else if (mark == 1) { p.drawLine(x - 6, y - 5, x + 5, y + 5, 15); p.drawLine(x + 5, y - 5, x - 6, y + 5, 15) }
            else p.fillCircle(x, y, 4, 15)
            p.setPixel(x + 7, y + 5, 5)
        }
        // Exact comparison pair: first is fixed blue/dot; second changes color and mark by fixture.
        p.fillRect(42, 91, 61, 18, 1)
        p.fillCircle(57, 100, 7, 8); p.fillCircle(87, 100, 7, sameColor ? 8 : 3)
        p.fillCircle(57, 100, 2, 15)
        if (samePattern) p.fillCircle(87, 100, 2, 15); else p.drawLine(82, 100, 92, 100, 15)
        if (response == EscapeAction.RockBeam && ok) {
            for (let i = 0; i < 4; i++) p.drawLine(24 + i * 24, 66 - (i % 2) * 18, 39 + i * 24, 48 - ((i + 1) % 2) * 18, 11)
            p.setPixel(31 + t * 11, 48, 15)
        }
    }

    // 28. Synchronizer: five readiness fixtures expose missing power/pressure/signal, alarm, or all-ready.
    // Locking all three buses releases the physical Interlock Key.
    function interlocks(p: Image, control: number, response: number, t: number, ok: boolean, idle: number, parked: boolean, sourceState: number) {
        shadow(p, 72, 101, 58)
        rounded(p, 12, 15, 120, 78, 14); p.fillRect(17, 20, 110, 67, 2)
        // Three named readiness buses feed the gear train.
        let names = ["PWR","PRS","SIG"]
        for (let i = 0; i < 3; i++) {
            let y = 28 + i * 18
            let missing = control % 5 == i
            let ready = !missing && control % 5 != 3
            p.fillRect(22, y - 6, 28, 12, 1); p.drawRect(22, y - 6, 28, 12, 6); p.print(names[i], 26, y - 3, ready ? 10 : 3, image.font5)
            p.fillCircle(54, y, 4, ready ? 10 : 3); p.drawLine(58, y, 74, y, ready ? 10 : 6)
        }
        // Interlocking gear train only synchronizes in the true all-ready fixture.
        for (let i = 0; i < 3; i++) {
            let x = 82 + i * 18
            let turn = parked && ok ? idle + i : response >= 0 ? (ok ? t + i : i * 2 + (i == control % 3 ? t : 0)) : i * 2
            gear(p, x, 49, 11, response == EscapeAction.SyncReject ? 3 : i == 1 ? 13 : 10, turn)
        }
        // Alarm fixture remains independently visible even though all three buses can otherwise look present.
        p.fillRect(78, 72, 42, 11, 1); p.drawRect(78, 72, 42, 11, 6)
        p.fillCircle(87, 77, 4, control % 5 == 3 ? 3 : 6); p.print(control % 5 == 3 ? "ALARM" : control % 5 == 4 ? "READY" : "CHECK", 94, 74, control % 5 == 4 ? 10 : control % 5 == 3 ? 3 : 15, image.font5)
        if (response == EscapeAction.SyncLock) {
            p.drawLine(60, 27, 60 + t * 8, 77, 11); p.fillCircle(123, 48, 5, 10)
        } else if (response == EscapeAction.SyncReject) {
            p.drawLine(72, 23, 125, 84, 3); p.drawLine(125, 23, 72, 84, 3); p.fillCircle(123, 48, 5, 3)
        }
        // Interlock-key output dock.
        p.fillRect(13, 92, 42, 8, 1); p.drawRect(17, 88, 34, 10, 6)
        if (sourceState == 0 && ok) { p.fillCircle(27, 93, 5, 10); p.fillCircle(27, 93, 2, 1); p.fillRect(31, 91, 15, 4, 10) }
    }

    // A compact machine-side socket is shown only for a transfer destination.
    // It makes the received state legible without duplicating the cargo sprite.
    function fixtureStatus(p: Image, fitted: boolean, sourceState: number, requiresPart: boolean) {
        if (fitted) { p.fillRect(119, 83, 13, 8, 14); p.fillRect(121, 85, 9, 4, 10); p.setPixel(123, 86, 15) }
        else if (sourceState >= 0 || requiresPart) { p.drawRect(119, 83, 13, 8, 6); p.fillRect(122, 86, 7, 2, 1) }
    }

    // These are tiny local motions, not a translation or blink applied to a
    // whole card. They keep later stations alive while preserving their puzzle
    // states. A fresh response has its own larger, readable animation above.
    function ambientDetails(p: Image, station: number, control: number, response: number, ok: boolean, idle: number, parked: boolean) {
        if (response >= 0 && !parked) return
        if (station == 4) p.setPixel(40 + (control % 2) * 41, 67 - (idle % 3), 15) // hold-face glint
        else if (station == 5) p.drawLine(18 + idle * 3, 34, 25 + idle * 3, 34, 6) // gap-air ripple
        else if (station == 6) p.setPixel(55, 30 + idle % 18, 15) // lantern glass reflection
        else if (station == 7) p.setPixel(25 + (idle % 4) * 30, 40, 15) // portrait eye catchlight
        else if (station == 8) p.fillCircle(34 + (idle * 9) % 71, 31 + (idle % 3) * 13, 1, 15) // drifting mural pigment
        else if (station == 9) p.setPixel(35 + (control % 3) * 32, 40 + idle % 8, 15) // socket rim glint
        else if (station == 10) p.setPixel(101 + idle % 5, 30, 15) // lens sweep
        else if (station == 11) p.fillCircle(39 + (idle % 3) * 31, 66 - idle % 9, 1, 15) // bath bubble
        else if (station == 12) p.setPixel(35 + (idle * 7) % 66, 69 - idle % 4, 10) // loose filing
        else if (station == 13) p.fillCircle(78, 34 + idle % 12, 1, 10) // hanging drop
        else if (station == 14) p.setPixel(34 + control % 3 * 3, 67 - idle % 3, 15) // weight edge
        else if (station == 15) p.setPixel(109, 38 + idle % 28, 15) // terminal reflection
        else if (station == 16) p.setPixel(55 + (idle % 4) * 8, 31 + (idle % 5) * 6, 15) // leaf edge
        else if (station == 17 && parked && ok) p.fillCircle(61 + idle % 17, 35 - idle % 6, 1, 11) // warm vessel steam
        else if (station == 19) p.setPixel(47 + (idle % 3) * 25, 31, 15) // horn-metal shine
        else if (station == 20) p.setPixel(44 + idle % 29, 56, 15) // printer scanner light
        else if (station == 21) p.setPixel(35 + idle % 55, control % 2 == 0 ? 21 : 66, 15) // tube-line glint
        else if (station == 22) p.setPixel(43 + idle % 17, 34, 15) // gauge tick
        else if (station == 23) p.setPixel(70 + idle % 5, 20, 15) // plumb-bob highlight
        else if (station == 24 && parked && ok) p.setPixel(55 + idle % 43, 39 + (control % 3) * 19, 15) // lit sensor beam
        else if (station == 25 && parked && ok) p.setPixel(30 + idle % 80, 54, 15) // light through open shutter
        else if (station == 26) p.fillCircle(45 + (idle * 7) % 51, 34 + idle % 29, 1, 15) // star twinkle
        else if (station == 27 && parked && ok) p.fillCircle(28 + idle % 76, 47, 1, 11) // rock-path beam sparkle
        else if (station == 29) p.setPixel(35 + idle % 42, 30, 15) // exit-door brass gleam
    }

    // 29. Final lever / exit door: three fixtures represent one unplugged core light, alarm on, or quiet/full-ready.
    // The Interlock Key is visibly required before the lever can honestly pull the door open.
    function exitDoor(p: Image, control: number, response: number, t: number, ok: boolean, fitted: boolean) {
        shadow(p, 72, 102, 61)
        // Monumental vault door with three core-light channels.
        p.fillRect(12, 9, 88, 87, 1); p.fillRect(17, 14, 78, 82, 14); p.fillRect(22, 19, 68, 73, 12); p.fillRect(27, 24, 58, 63, 2)
        p.drawRect(27, 24, 58, 63, 6); p.drawLine(31, 29, 81, 29, 15)
        for (let y = 36; y < 82; y += 14) { p.drawLine(31, y, 81, y, 14); bolt(p, 32, y); bolt(p, 80, y) }
        // Three core lights are the actual final meter. Fixture 0 removes one; fixture 1 alarms; fixture 2 is quiet.
        let lights = control % 3 == 0 || !fitted ? 2 : 3
        for (let i = 0; i < 3; i++) {
            let on = i < lights
            p.fillCircle(40 + i * 17, 52, 6, on ? 10 : 6); p.fillCircle(40 + i * 17, 52, 2, on ? 15 : 1)
            p.drawLine(40 + i * 17, 59, 40 + i * 17, 68, on ? 10 : 6)
        }
        // Interlock-key cylinder and lever tower.
        p.fillRect(103, 25, 28, 64, 14); p.drawRect(103, 25, 28, 64, 6)
        p.fillRect(107, 31, 20, 17, 1); p.drawRect(107, 31, 20, 17, 6)
        if (fitted) { p.fillCircle(114, 39, 6, 10); p.fillCircle(114, 39, 2, 1); p.fillRect(118, 37, 8, 4, 10) }
        else { p.drawCircle(114, 39, 6, 6); p.drawLine(108, 44, 122, 34, 6) }
        p.fillCircle(117, 59, 8, 5); p.fillCircle(117, 59, 4, fitted ? 10 : 6)
        let pull = response == EscapeAction.LeverPull && ok ? Math.min(20,t * 3) : 0
        p.drawLine(117, 63, 117 + pull, 82, response == EscapeAction.LeverReject ? 3 : fitted ? 10 : 6); p.fillCircle(117 + pull, 84, 6, response == EscapeAction.LeverReject ? 3 : 10)
        if (control % 3 == 1) { p.fillCircle(121, 18, 7, 3); p.fillCircle(121, 18, 3, 15); p.print("ALARM", 96, 8, 3, image.font5) }
        else p.print(control % 3 == 0 ? "2/3" : "3/3", 105, 8, control % 3 == 0 ? 6 : 10, image.font5)
        if (response == EscapeAction.LeverPull && ok) {
            // Door retracts left while bright exit rays appear through the opened jamb.
            let open = Math.min(52,t * 7)
            p.fillRect(27, 24, open, 63, 1); p.fillRect(28, 26, Math.max(0,open-2), 59, 12)
            for (let i = 0; i < 5; i++) p.drawLine(87, 49, 140, 19 + i * 17, 11)
            p.fillRect(18, 93, 116, 6, 10)
        } else if (response == EscapeAction.LeverReject) {
            p.drawLine(104, 91, 130, 91, 3); p.drawLine(106, 94, 128, 94, 3); p.fillCircle(95, 18 + (t % 2) * 3, 4, 3)
        } else p.fillRect(15, 94, 119, 5, 6)
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

    function roomFloor(room: number): number {
        if (room == 0) return 9      // pale workshop limestone
        if (room == 1) return 15     // luminous gallery ceramic
        if (room == 2) return 9      // warm garden stone
        if (room == 3) return 14     // bridge steel-blue deck
        return 12                    // last-door slate
    }

    function roomSeam(room: number): number {
        if (room == 0) return 5
        if (room == 1) return 11
        if (room == 2) return 7
        if (room == 3) return 8
        return 14
    }

    function roomWall(room: number): number {
        if (room == 0) return 5
        if (room == 1) return 13
        if (room == 2) return 6
        if (room == 3) return 8
        return 2
    }

    function roomAccent(room: number): number {
        if (room == 0) return 4
        if (room == 1) return 11
        if (room == 2) return 7
        if (room == 3) return 10
        return 10
    }

    function panel(p: Image, x: number, y: number, w: number, h: number, fill: number, edge: number, highlight: number) {
        p.fillRect(x + 2, y + 2, w, h, 1)
        p.fillRect(x, y, w, h, edge)
        p.fillRect(x + 2, y + 2, w - 4, h - 4, fill)
        p.drawLine(x + 3, y + 3, x + w - 4, y + 3, highlight)
        p.drawLine(x + 3, y + 3, x + 3, y + h - 4, highlight)
        p.drawLine(x + 3, y + h - 4, x + w - 4, y + h - 4, 6)
    }

    function roomDetails(p: Image, room: number) {
        let accent = roomAccent(room)
        if (room == 0) {
            // Workshop: brass service rail and iron mounting plates stay in the wall band.
            for (let x = 54; x < 590; x += 88) {
                p.fillRect(x, 54, 38, 5, 2)
                p.drawLine(x + 3, 54, x + 34, 54, 10)
                p.fillCircle(x + 5, 57, 2, 6); p.fillCircle(x + 33, 57, 2, 6)
            }
        } else if (room == 1) {
            // Gallery: shallow glazed insets and little colored light catches.
            for (let x = 52; x < 590; x += 90) {
                p.fillRect(x, 53, 44, 7, 12)
                p.drawLine(x + 2, 54, x + 41, 54, 15)
                p.fillRect(x + 7, 56, 7, 2, x % 180 == 52 ? 11 : 13)
                p.fillRect(x + 28, 56, 7, 2, x % 180 == 52 ? 13 : 11)
            }
        } else if (room == 2) {
            // Garden: stone wall with restrained vine sprigs, never crossing the walking floor.
            for (let x = 48; x < 590; x += 82) {
                p.drawLine(x, 59, x + 12, 52, 7)
                p.drawLine(x + 12, 52, x + 25, 59, 7)
                p.fillCircle(x + 5, 56, 2, 7); p.fillCircle(x + 20, 55, 2, 7)
            }
        } else if (room == 3) {
            // Bridge: riveted structural rail.
            p.fillRect(42, 53, 556, 8, 1)
            p.drawLine(42, 54, 598, 54, 11)
            for (let x = 52; x < 598; x += 36) p.fillCircle(x, 57, 2, 6)
        } else {
            // Last Door: monumental dark lintel with sparse gold circuit marks.
            p.fillRect(42, 52, 556, 9, 1)
            p.drawLine(42, 53, 598, 53, 10)
            for (let x = 58; x < 590; x += 74) {
                p.drawLine(x, 56, x + 18, 56, accent)
                p.fillCircle(x + 22, 56, 2, accent)
            }
        }
    }

    function floor(p: Image, room: number) {
        p.fill(12)
        let wall = roomWall(room)
        let floorColor = roomFloor(room)
        let seam = roomSeam(room)
        let accent = roomAccent(room)
        // Layered perimeter: dark exterior, material wall, bright inner lip, then the walking plane.
        p.fillRect(14, 47, 612, 390, 1)
        p.fillRect(18, 50, 604, 384, wall)
        p.fillRect(24, 56, 592, 372, 2)
        p.fillRect(30, 63, 580, 359, 6)
        p.fillRect(34, 67, 572, 349, floorColor)
        // Large offset slabs read as horizontal floor rather than a wall grid.
        for (let y = 68; y < 416; y += 38) {
            p.drawLine(34, y, 605, y, 15)
            p.drawLine(34, y + 1, 605, y + 1, seam)
            for (let x = 34 + (Math.idiv(y, 38) % 2) * 38; x < 606; x += 76) {
                p.drawLine(x, y + 2, x, Math.min(y + 37, 415), seam)
                if (room == 3) p.setPixel(x + 4, y + 8, 11)
                else if (room == 2) p.setPixel(x + 8, y + 20, 7)
                else if (room == 4) p.drawLine(x + 10, y + 7, x + 19, y + 7, 14)
            }
        }
        // Inner wall lip and baseboard shadows give the floor a recessed physical edge.
        p.fillRect(34, 63, 572, 4, accent)
        p.drawLine(38, 67, 602, 67, 15)
        p.fillRect(30, 68, 4, 348, 1)
        p.fillRect(606, 68, 4, 348, 1)
        p.fillRect(34, 416, 572, 7, 1)
        p.drawLine(38, 417, 602, 417, seam)
        roomDetails(p, room)
        // Side doorway frame. It remains decoration only; collision authority stays in floor.ts.
        if (room > 0) {
            p.fillRect(11, 210, 29, 65, 1)
            p.fillRect(15, 216, 25, 53, wall)
            p.fillRect(20, 220, 20, 45, floorColor)
            p.drawLine(21, 242, 31, 232, accent)
            p.drawLine(21, 242, 31, 252, accent)
            p.fillRect(13, 214, 4, 57, 6)
        } else {
            // Reset lever at the entrance reads as wall hardware, not a puzzle station.
            p.fillRect(15, 224, 18, 35, 1)
            p.fillRect(18, 227, 12, 29, 6)
            p.drawLine(23, 248, 28, 232, 4)
            p.fillCircle(28, 232, 4, 3)
            p.setPixel(27, 230, 15)
        }
    }

    function connection(p: Image, a: number, b: number, done: boolean, idleFrame: number) {
        let ax = escapeFlow.x(a), ay = escapeFlow.y(a)
        let bx = escapeFlow.x(b), by = escapeFlow.y(b)
        let color = done ? 8 : 6
        // Floor-hugging conduit: shadow, casing, lit inner line, then occasional clamps.
        p.drawLine(ax, ay + 40, bx + 5, ay + 40, 12)
        p.drawLine(ax, ay + 36, bx, ay + 36, 1)
        p.drawLine(ax, ay + 37, bx, ay + 37, color)
        p.drawLine(bx, ay + 36, bx, by, 1)
        p.drawLine(bx + 1, ay + 37, bx + 1, by, color)
        let minX = Math.min(ax, bx), maxX = Math.max(ax, bx)
        for (let x = minX + 18; x < maxX; x += 34) p.fillRect(x, ay + 34, 2, 7, 6)
        if (done) {
            let t = (Math.abs(idleFrame) % 8) / 8
            p.fillCircle(Math.round(ax + (bx - ax) * t), ay + 37, 2, 10)
            p.setPixel(Math.round(ax + (bx - ax) * t), ay + 36, 15)
        }
    }

    function door(p: Image, room: number, solved: number[]) {
        let open = escapeFlow.roomComplete(room, solved)
        let accent = roomAccent(room)
        // Thick jamb, recessed track and lit threshold make this read as architecture.
        p.fillRect(600, 204, 34, 77, 1)
        p.fillRect(604, 208, 28, 69, 6)
        p.fillRect(608, 211, 20, 64, open ? 1 : 2)
        p.drawLine(606, 209, 630, 209, 15)
        p.fillRect(598, 278, 35, 4, 12)
        if (open) {
            p.fillRect(596, 217, 33, 52, 1)
            p.fillRect(600, 220, 29, 46, 12)
            p.drawLine(602, 222, 626, 222, accent)
            for (let i = 0; i < 3; i++) {
                p.drawLine(606 + i * 7, 236, 612 + i * 7, 242, accent)
                p.drawLine(606 + i * 7, 248, 612 + i * 7, 242, accent)
            }
            p.fillRect(600, 264, 29, 3, 10)
        } else {
            p.fillRect(611, 217, 4, 50, 5)
            p.fillRect(620, 217, 4, 50, 2)
            p.drawLine(612, 218, 612, 264, 10)
            p.fillCircle(619, 244, 4, 10)
            p.setPixel(618, 242, 15)
            // Each finished chain retracts its own real door catch.
            let catches = room == 0 ? [5] : room == 1 ? [6,12] : room == 2 ? [16,21,17] : room == 3 ? [25,29] : [31,33,34]
            for (let i = 0; i < catches.length; i++) {
                let y = 242 - (catches.length - 1) * 10 + i * 20
                let released = solved[catches[i]] == 1
                p.fillRect(597, y - 4, 22, 9, 1)
                p.fillRect(released ? 613 : 600, y - 2, released ? 5 : 18, 5, released ? 7 : 6)
                p.fillCircle(625, y, 3, released ? 7 : 3)
                if (released) p.setPixel(625, y - 1, 15)
            }
        }
    }

    function settledControl(beat: number, controls: number[], settledControls: number[], solved: number[]): number {
        if (solved[beat] && settledControls[beat] != undefined) return settledControls[beat]
        return controls[beat] || 0
    }

    function sourceState(station: number, itemStates: number[]): number {
        let item = escapeCargo.sourceItem(station)
        return item < 0 ? -1 : itemStates[item] == undefined ? 0 : itemStates[item]
    }

    function scaleImage(target: Image, source: Image, x: number, y: number, scale: number) {
        for (let py = 0; py < source.height; py++) for (let px = 0; px < source.width; px++) {
            let color = source.getPixel(px, py)
            if (color) target.fillRect(x + px * scale, y + py * scale, scale, scale, color)
        }
    }

    export function world(room: number, solved: number[], introduced: number[], focusBeat: number, activeBeat: number, controls: number[], response: number, reactionFrame: number, pitch: number, firstClear: number, reactionBeat: number, reactionControl: number, idleFrame: number, settledControls: number[] = [], itemStates: number[] = []): Image {
        let p = image.create(640, 480)
        floor(p, room)
        escapeFloor.drawSurfaces(p, room)
        let focus = escapeFlow.stationForBeat(focusBeat)
        let active = activeBeat < 0 ? -1 : escapeFlow.stationForBeat(activeBeat)
        let reacting = reactionBeat < 0 || reactionFrame < 0 ? -1 : escapeFlow.stationForBeat(reactionBeat)
        for (let l = 0; l < linksA.length; l++) if (Math.idiv(linksA[l], 6) == room) {
            let output = escapeCargo.sourceItem(linksA[l])
            if (output < 0 || escapeCargo.targetStation(output) != linksB[l]) connection(p, linksA[l], linksB[l], stationDone(linksA[l], solved), idleFrame)
        }
        door(p, room, solved)
        // Back-to-front placement keeps overlapping physical silhouettes legible.
        for (let row = 0; row < 2; row++) for (let local = 0; local < 6; local++) {
            let s = room * 6 + local
            let x = escapeFlow.x(s), y = escapeFlow.y(s)
            if ((y < 250 ? 0 : 1) != row) continue
            let b = s == reacting ? reactionBeat : s == active ? activeBeat : solved[escapeFlow.lastBeats[s]] ? escapeFlow.lastBeats[s] : escapeFlow.firstBeats[s]
            let done = stationDone(s, solved)
            let available = escapeFlow.available(s, solved, introduced, focusBeat)
            oval(p, x + 4, y + 43, 53, 11, 6)
            let portraitMask = solved[7] + 2 * solved[8] + 4 * solved[9] + 8 * solved[10]
            let objectControl = s == reacting ? reactionControl : settledControl(b, controls, settledControls, solved)
            let requiredItem = escapeCargo.requiredForBeat(b)
            let fitted = requiredItem >= 0 && itemStates[requiredItem] == 2
            let object = escapeObjects.prop(s, visibleControl(b, objectControl, solved), s == reacting ? response : -1, s == reacting ? reactionFrame : -1, solved[b] == 1, s == 7 ? b - 7 : b - escapeFlow.firstBeats[s], pitch, portraitMask, idleFrame, fitted, sourceState(s, itemStates), requiredItem >= 0)
            if (!available) {
                for (let py = 0; py < object.height; py++) for (let px = 0; px < object.width; px++) {
                    let c = object.getPixel(px, py)
                    if (c) object.setPixel(px, py, darkMap[c])
                }
            }
            p.drawTransparentImage(object, x - 72, y - 56)
            if (s == focus) {
                // Gold chevron floats above only the next station; no false floor target is introduced.
                p.fillRect(x - 3, y - 59, 7, 3, 10)
                p.drawLine(x - 10, y - 55, x, y - 46, 10)
                p.drawLine(x + 10, y - 55, x, y - 46, 10)
                p.setPixel(x, y - 58, 15)
            }
            // Only the current object receives an interaction plaque; the room is not a label grid.
            if (s == active || s == focus) {
                let name = shortNames[s]
                let left = Math.max(38, Math.min(600 - name.length * 6, x - name.length * 3))
                let edge = s == active ? 11 : 10
                p.fillRect(left - 5, y + 52, name.length * 6 + 10, 14, 1)
                p.fillRect(left - 3, y + 54, name.length * 6 + 6, 10, 12)
                p.drawLine(left - 2, y + 54, left + name.length * 6 + 2, y + 54, edge)
                words(p, name, left, y + 56, 15, 1)
            }
        }
        // Surface tiles were composed below the apparatus. Only the operating
        // pads and output trays are drawn in this foreground pass.
        escapeFloor.drawPads(p, room, focus, active)
        // HUD sits outside the walkable room and uses the same beveled material language as the machines.
        p.fillRect(0, 0, 640, 42, 1)
        p.fillRect(0, 3, 640, 36, 12)
        p.drawLine(0, 39, 639, 39, roomAccent(room))
        words(p, roomTitles[room], 18, 8, 15, 2)
        panel(p, 532, 9, 88, 22, 1, 6, roomAccent(room))
        words(p, "ROOM " + ["A", "B", "C", "D", "E"][room], 549, 16, 10, 1)
        p.fillRect(0, 439, 640, 41, 1)
        p.fillRect(0, 443, 640, 37, 12)
        p.drawLine(0, 443, 639, 443, roomAccent(room))
        if (activeBeat >= 0) {
            let s = escapeFlow.stationForBeat(activeBeat)
            let part = escapeFlow.lastBeats[s] > escapeFlow.firstBeats[s] ? "  PART " + (activeBeat - escapeFlow.firstBeats[s] + 1) + "/" + (escapeFlow.lastBeats[s] - escapeFlow.firstBeats[s] + 1) : ""
            words(p, escapeLab.readout(activeBeat) + part, 14, 447, 15, 2)
            words(p, escapeFlow.lastBeats[s] > escapeFlow.firstBeats[s] ? "ARROWS WALK   A OPERATE   HOLD B: TUNE / SELECT PART" : "ARROWS WALK   A OPERATE   HOLD B: TUNE", 14, 469, 10, 1)
        } else {
            let target = focus < 0 ? "Walk to the open doorway" : "Next: " + shortNames[focus]
            words(p, target, 14, 447, 15, 2)
            words(p, "ARROWS WALK   A INTERACT   GOLD LIGHT GUIDES YOU", 14, 469, 10, 1)
        }
        return p
    }

    // Held B opens this transient machine view. It deliberately contains no
    // mode toggle: the engine returns to the room as soon as B is released.
    export function operating(station: number, beat: number, fixture: number, solved: number[], settledControls: number[], itemStates: number[], response: number, reactionFrame: number, pitch: number, idleFrame: number): Image {
        let p = image.create(640, 480)
        let room = Math.idiv(station, 6)
        let accent = roomAccent(room)
        p.fill(12)
        // Large recessed workbench frame; the actual 144x112 prop remains the single machine illustration.
        p.fillRect(12, 10, 616, 460, 1)
        p.fillRect(17, 15, 606, 450, 2)
        p.fillRect(22, 20, 596, 440, 12)
        p.drawLine(24, 21, 616, 21, accent)
        p.fillRect(24, 24, 592, 42, 14)
        p.drawLine(24, 65, 615, 65, 6)
        words(p, "OPERATING", 36, 29, 10, 1)
        words(p, shortNames[station], 36, 44, 15, 2)
        panel(p, 430, 30, 168, 25, 3, 1, 4)
        words(p, "RELEASE B TO WALK", 445, 39, 15, 1)

        let settled = solved[beat] && settledControls[beat] != undefined ? settledControls[beat] : fixture
        let control = reactionFrame >= 0 ? fixture : settled
        let requiredItem = escapeCargo.requiredForBeat(beat)
        let fitted = requiredItem >= 0 && itemStates[requiredItem] == 2
        let portraitMask = solved[7] + 2 * solved[8] + 4 * solved[9] + 8 * solved[10]
        let object = escapeObjects.prop(station, visibleControl(beat, control, solved), reactionFrame >= 0 ? response : -1, reactionFrame, solved[beat] == 1, station == 7 ? beat - 7 : beat - escapeFlow.firstBeats[station], pitch, portraitMask, idleFrame, fitted, sourceState(station, itemStates), requiredItem >= 0)

        // Machine stage: floor shadow plus a crisp 3x copy of the exact room prop.
        p.fillRect(36, 91, 432, 318, 2)
        p.fillRect(41, 96, 422, 308, 1)
        p.fillRect(45, 100, 414, 300, 12)
        oval(p, 252, 390, 170, 12, 1)
        scaleImage(p, object, 35, 75, 3)
        p.drawLine(45, 399, 458, 399, accent)
        words(p, "SELECTED: " + (escapeLab.readout(beat) || ("SETTING " + (fixture + 1))), 44, 76, 15, 1)

        // Physical input console: selected, settled and fixture state occupy distinct recessed bays.
        panel(p, 482, 91, 122, 310, 14, 1, accent)
        words(p, "INPUT", 498, 107, 10, 1)
        p.fillRect(494, 128, 98, 72, 12)
        p.drawRect(494, 128, 98, 72, 6)
        words(p, "SELECTED", 504, 141, 10, 1)
        words(p, "#" + (fixture + 1), 504, 160, 15, 2)
        if (solved[beat]) {
            p.fillRect(494, 210, 98, 57, 12)
            p.drawRect(494, 210, 98, 57, 6)
            words(p, "SETTLED", 504, 222, 10, 1)
            words(p, "#" + (settled + 1), 504, 240, 7, 2)
        }
        p.fillRect(494, 278, 98, 109, 12)
        p.drawRect(494, 278, 98, 109, 6)
        words(p, "FIXTURE", 504, 290, 10, 1)
        if (requiredItem >= 0) {
            words(p, fitted ? "FITTED" : "NEEDS PART", 500, 309, fitted ? 7 : 3, 1)
            words(p, escapeCargo.names[requiredItem], 500, 326, 15, 1)
            let item = escapeCargo.drawItem(requiredItem, idleFrame)
            scaleImage(p, item, 515, 340, 2)
        } else {
            words(p, "BUILT IN", 504, 312, 7, 1)
            p.fillCircle(544, 350, 15, 6)
            p.fillCircle(544, 350, 10, accent)
            p.fillCircle(544, 350, 4, 15)
        }

        p.fillRect(30, 416, 580, 39, 6)
        p.drawLine(31, 417, 608, 417, 15)
        words(p, "LEFT / RIGHT CHANGE INPUT     UP / DOWN SELECT PART     A OPERATE", 43, 428, 15, 1)
        words(p, "RELEASE B TO WALK", 231, 444, 10, 1)
        return p
    }

    export function explorer(direction: number, step: number): Image {
        let p = image.create(32, 40)
        // Feet anchor remains at the original lower edge. Only limbs and tiny equipment shift with stride.
        oval(p, 16, 36, 11, 3, 6)
        let stride = step % 3 == 0 ? 0 : step % 3 == 1 ? 2 : -2
        p.fillRect(8, 28 + stride, 6, 8, 12)
        p.fillRect(19, 28 - stride, 6, 8, 12)
        p.fillRect(8, 35 + stride, 8, 3, 1)
        p.fillRect(19, 35 - stride, 8, 3, 1)
        p.setPixel(9, 35 + stride, 15); p.setPixel(20, 35 - stride, 15)
        // Teal field jacket, lighter chest panel, dark belt and compact backpack.
        p.fillRect(7, 16, 20, 15, 8)
        p.fillRect(9, 17, 16, 5, 11)
        p.fillRect(9, 23, 16, 2, 14)
        p.fillRect(5, 20 - stride, 4, 10, 5)
        p.fillRect(27, 20 + stride, 4, 10, 5)
        p.fillRect(4, 23 - stride, 3, 6, 12)
        p.fillRect(25, 18, 3, 11, 2)
        // Warm face under a dark explorer cap. Facing changes only facial/profile pixels.
        p.fillRect(8, 4, 18, 14, 4)
        p.fillRect(10, 8, 14, 11, 5)
        p.fillRect(7, 2, 21, 5, 2)
        p.fillRect(8, 5, 5, 6, 2)
        p.drawLine(9, 6, 25, 6, 14)
        if (direction == 3) {
            p.fillRect(10, 8, 15, 12, 2)
            p.fillRect(13, 9, 9, 3, 14)
        } else if (direction == 1) {
            p.fillRect(9, 12, 3, 3, 1); p.fillRect(6, 16, 5, 3, 4); p.setPixel(10, 11, 15)
        } else if (direction == 2) {
            p.fillRect(22, 12, 3, 3, 1); p.fillRect(24, 16, 5, 3, 4); p.setPixel(23, 11, 15)
        } else {
            p.fillRect(12, 12, 3, 3, 1); p.fillRect(21, 12, 3, 3, 1)
            p.fillRect(15, 18, 6, 2, 4); p.setPixel(13, 11, 15); p.setPixel(22, 11, 15)
        }
        return p
    }

    export function ending(firstClear: number, secondClear: number, phase: number): Image {
        let p = image.create(640, 480)
        // Exterior night slate with a warm path spilling out of the final doorway.
        p.fill(12)
        for (let y = 0; y < 305; y += 34) {
            p.drawLine(0, y, 639, y, y % 68 == 0 ? 14 : 2)
            for (let x = (Math.idiv(y, 34) % 2) * 46; x < 640; x += 92) p.drawLine(x, y, x, Math.min(304, y + 33), 2)
        }
        p.fillRect(0, 304, 640, 176, 2)
        p.fillRect(0, 316, 640, 164, 7)
        for (let x = 0; x < 640; x += 64) {
            p.drawLine(x, 316, x + 31, 304, 9)
            p.drawLine(x + 31, 304, x + 63, 316, 9)
        }
        // Monumental layered doorway and luminous interior.
        p.fillRect(213, 67, 214, 245, 1)
        p.fillRect(221, 75, 198, 237, 6)
        p.fillRect(231, 85, 178, 227, 2)
        p.fillRect(242, 96, 156, 216, 15)
        p.fillRect(255, 107, 130, 205, 10)
        p.fillRect(278, 120, 84, 192, 9)
        p.drawLine(244, 98, 396, 98, 10)
        p.drawLine(255, 108, 385, 108, 15)
        for (let i = 0; i < 5; i++) {
            let x = 92 + i * 114
            oval(p, x, 326, 72, 13, 8)
            p.fillCircle(x - 1, 306, 4 + (Math.abs(phase) + i) % 3, 10)
            p.setPixel(x - 1, 304, 15)
        }
        // Rays remain behind the explorer and pulse locally instead of flashing the screen.
        for (let i = 0; i < 7; i++) p.drawLine(320, 296, 206 + i * 38, 330 + (i % 2) * 13, i % 2 == 0 ? 10 : 15)
        p.drawTransparentImage(explorer(0, Math.abs(phase) % 3), 304, 269)
        if (secondClear) {
            words(p, "YOU DID IT!", 253, 29, 15, 2)
            words(p, "Every room works because of your code.", 94, 362, 15, 2)
            words(p, "Two complete escapes. Congratulations!", 98, 395, 10, 2)
        } else {
            words(p, "YOU FOUND THE WAY OUT!", 194, 29, 15, 2)
            words(p, "Your rules brought every room to life.", 94, 362, 15, 2)
            words(p, "B: play the whole adventure once more", 98, 395, 10, 2)
        }
        panel(p, 168, 430, 304, 30, 12, 1, 10)
        words(p, "Your completion is saved.", 184, 441, 15, 2)
        return p
    }

}

namespace userconfig {
    export const ARCADE_SCREEN_WIDTH = 640
    export const ARCADE_SCREEN_HEIGHT = 480
}

//% color=#4767ac icon="\uf11b" block="Escape Room" weight=90
namespace escapeLab {
    const saveKey = "logic-escape-room:v3"
    const priorKey = "logic-escape-room:v2"
    const legacyKey = "logic-escape-room:v1"
    const saveVersion = 3
    let handlers: (() => void)[] = []
    let solved: number[] = []
    let introduced: number[] = []
    let controls: number[] = []
    let settledControls: number[] = []
    let itemStates: number[] = []
    let room = 0
    let firstClear = 0
    let secondClear = 0
    let ending = 0
    let pitch = -20
    let pressureReady = false
    let player: Sprite = null
    let explorer: Sprite = null
    let cargoSprites: Sprite[] = []
    let tossItem = -1
    let tossFrames = 0
    let tossX = 0
    let tossY = 0
    let producingItem = -1
    let focused = false
    let station = -1
    let beat = -1
    let fixture = 0
    let response = -1
    let credible = true
    let phase = 0
    let inAttempt = false
    let resetArmed = false
    let explorerFacing = 0
    let reactionFrame = -1
    let reactionBeat = -1
    let reactionControl = 0
    let scurryFrames = 0
    let flame: Sprite = null
    let flameFrames: Image[] = []
    let busy = false
    let bPressedAt = -1
    let operating = false

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
        settledControls = []
        itemStates = []
        for (let i = 0; i < 36; i++) { solved.push(0); introduced.push(0); controls.push(0); settledControls.push(0) }
        for (let i = 0; i < escapeCargo.count; i++) itemStates.push(0)
    }

    function safeInteger(value: number, fallback: number, low: number, high: number): number {
        // Settings storage is outside this game. Accept only finite whole
        // values, then keep it within a deliberately broad game-safe range.
        if (value != Math.round(value) || value <= -1000000 || value >= 1000000) return fallback
        return Math.max(low, Math.min(high, value))
    }

    function load() {
        let data = settings.readNumberArray(saveKey)
        let version = 3
        if (!data || data.length != 164 || data[0] != saveVersion) {
            data = settings.readNumberArray(priorKey)
            version = 2
        }
        if (!data || (version == 2 && (data.length != 115 || data[0] != 2))) {
            data = settings.readNumberArray(legacyKey)
            version = 1
        }
        if (!data || (version == 1 && (data.length != 43 || data[0] != 1))) {
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
            introduced.push(version == 1 ? 0 : data[43 + i] == 1 ? 1 : 0)
            controls.push(version == 1 ? 0 : safeInteger(data[79 + i], 0, 0, 4))
        }
        // Old successes count only when their new physical source also exists.
        if (version == 1) {
            const source = [-1,0,1,2,3,4,14,15,15,15,15,7,11,-1,13,-1,19,18,-1,-1,-1,20,-1,22,23,24,-1,26,27,28,-1,30,-1,32,31,34]
            for (let pass = 0; pass < 36; pass++) {
                for (let b = 0; b < 36; b++) if (source[b] >= 0 && !solved[source[b]]) solved[b] = 0
                if (!solved[7] || !solved[8] || !solved[9] || !solved[10]) solved[11] = 0
                if (!solved[31] || !solved[33] || !solved[1] || !solved[27] || !solved[25] || !solved[30]) solved[34] = 0
            }
            if (!solved[35]) ending = 0
            for (let r = 0; r < room; r++) if (!escapeFlow.roomComplete(r, solved)) { room = r; break }
        }
        itemStates = []
        settledControls = []
        let carried = -1
        for (let i = 0; i < escapeCargo.count; i++) {
            let state = version == 3 ? safeInteger(data[115 + i], 0, 0, 2) : escapeCargo.ready(i, solved) ? 2 : 0
            if (!escapeCargo.ready(i, solved)) state = 0
            if (state == 1) { if (carried >= 0) state = 0; else carried = i }
            itemStates.push(state)
        }
        for (let i = 0; i < 36; i++) settledControls.push(version == 3 ? safeInteger(data[128 + i], 0, 0, 4) : solved[i] ? controls[i] : 0)
        if (version != 3) save()
    }

    function save() {
        let data = [saveVersion, room, firstClear, secondClear, ending, pitch, pressureReady ? 1 : 0]
        for (let i = 0; i < 36; i++) data.push(solved[i])
        for (let i = 0; i < 36; i++) data.push(introduced[i])
        for (let i = 0; i < 36; i++) data.push(controls[i])
        for (let i = 0; i < escapeCargo.count; i++) data.push(itemStates[i])
        for (let i = 0; i < 36; i++) data.push(settledControls[i])
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

    function nearPad(availableOnly: boolean): number {
        let best = -1
        let distance = 10000
        for (let local = 0; local < 6; local++) {
            let candidate = room * 6 + local
            if (availableOnly && !escapeFlow.available(candidate, solved, introduced, escapeFlow.focusBeat(room, solved, introduced)) && !(escapeCargo.targetItem(candidate) >= 0 && itemStates[escapeCargo.targetItem(candidate)] >= 1)) continue
            let dx = player.x - escapeFloor.standX(candidate)
            let dy = player.y - escapeFloor.standY(candidate)
            let d = dx * dx + dy * dy
            if (d < distance) { distance = d; best = candidate }
        }
        return distance < 1156 ? best : -1
    }

    function nearSourceTray(): number {
        for (let i = 0; i < escapeCargo.count; i++) {
            if (Math.idiv(escapeCargo.sourceStation(i), 6) != room || itemStates[i] != 0 || !escapeCargo.ready(i, solved)) continue
            let source = escapeCargo.sourceStation(i)
            let dx = player.x - escapeFloor.trayX(source)
            let dy = player.y - escapeFloor.trayY(source)
            if (dx * dx + dy * dy < 900) return i
        }
        return -1
    }

    function carriedItem(): number {
        for (let i = 0; i < escapeCargo.count; i++) if (itemStates[i] == 1) return i
        return -1
    }

    function updateCargoSprites() {
        for (let i = 0; i < escapeCargo.count; i++) {
            let sprite = cargoSprites[i]
            if (!sprite) continue
            sprite.setImage(escapeCargo.drawItem(i, phase))
            if (operating || ending > 0) sprite.setFlag(SpriteFlag.Invisible, true)
            else if (itemStates[i] == 0 && producingItem == i && reactionFrame >= 0) {
                let t = escapeCargo.productionProgress(reactionFrame)
                if (t < 0 || Math.idiv(escapeCargo.sourceStation(i), 6) != room) sprite.setFlag(SpriteFlag.Invisible, true)
                else {
                    sprite.setPosition(escapeCargo.productionX(i, reactionFrame), escapeCargo.productionY(i, reactionFrame))
                    sprite.setFlag(SpriteFlag.Invisible, false)
                }
            } else if (tossItem == i && tossFrames > 0) {
                sprite.setPosition(escapeCargo.returnX(i, tossX, tossFrames), escapeCargo.returnY(i, tossY, tossFrames))
                sprite.setFlag(SpriteFlag.Invisible, false)
            } else if (!escapeCargo.ready(i, solved) && itemStates[i] != 2) sprite.setFlag(SpriteFlag.Invisible, true)
            else if (itemStates[i] == 0) {
                let source = escapeCargo.sourceStation(i)
                sprite.setPosition(escapeFloor.trayX(source), escapeFloor.trayY(source))
                sprite.setFlag(SpriteFlag.Invisible, Math.idiv(source, 6) != room)
            } else if (itemStates[i] == 1) {
                sprite.setPosition(player.x + 11, player.y - 21)
                sprite.setFlag(SpriteFlag.Invisible, false)
            } else {
                let target = escapeCargo.targetStation(i)
                sprite.setPosition(escapeFlow.x(target), escapeFlow.y(target) - 6)
                sprite.setFlag(SpriteFlag.Invisible, Math.idiv(target, 6) != room)
            }
        }
    }

    function tossHome(id: number) {
        tossItem = id
        tossFrames = escapeCargo.returnFrames
        tossX = player.x
        tossY = player.y - 20
        itemStates[id] = 0
        save()
    }

    function nearestStation(): number {
        return nearPad(true)
    }

    function enterStation(s: number) {
        if (station == s) return
        station = s
        let itinerary = escapeFlow.focusBeat(room, solved, introduced)
        beat = itinerary >= firstBeats[s] && itinerary <= lastBeats[s] ? itinerary : firstBeats[s]
        if (beat == firstBeats[s]) for (let i = firstBeats[s]; i <= lastBeats[s]; i++) if (!solved[i]) { beat = i; break }
        fixture = controls[beat]
        credible = true
        focused = true
        draw()
    }

    function prerequisitesMet(b: number): boolean {
        if (!escapeCargo.installedForBeat(b, itemStates)) return false
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
        focused = false
        station = -1
        beat = -1
        fixture = 0
        credible = true
        draw()
    }

    function updateNearbyStation() {
        if (ending > 0 || busy || operating) return
        let s = nearestStation()
        if (s == station) return
        if (s < 0) leaveStation()
        else enterStation(s)
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
        if (b == 1) return itemStates[0] == 2 ? ["CRANK RESTING", "TURN CRANK"][f] : "CRANK SOCKET EMPTY"
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
        if (b == 21) return itemStates[6] == 2 ? ["FLAME OUT", "FLAME LOW", "FLAME OUT", "FLAME ON", "FLAME HIGH"][f] : "PATCH SLOT EMPTY"
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
        if (fact == EscapeFact.CrankFitted) return beat == 1 && itemStates[0] == 2
        if (fact == EscapeFact.PowerAvailable) return solved[1] == 1
        if (fact == EscapeFact.WaterFlowing) return beat == 3 && fixture == 1 && itemStates[1] == 2 && solved[2] == 1
        if (fact == EscapeFact.YellowOn) return itemStates[4] == 2 && (fixture == 1 || fixture >= 3) && solved[7] == 1 && solved[8] == 1 && solved[9] == 1 && solved[10] == 1
        if (fact == EscapeFact.BlueOn) return itemStates[4] == 2 && (fixture == 2 || fixture >= 3) && solved[7] == 1 && solved[8] == 1 && solved[9] == 1 && solved[10] == 1
        if (fact == EscapeFact.RedOn) return fixture == 4
        if (fact == EscapeFact.Metallic) return beat == 16 && fixture > 0
        if (fact == EscapeFact.MagnetOn) return beat == 16 && itemStates[5] == 2 && solved[19] == 1 && (fixture == 0 || fixture == 2)
        if (fact == EscapeFact.VesselRepaired) return beat == 21 && itemStates[6] == 2
        if (fact == EscapeFact.VesselHot) return beat == 21 && (fixture == 1 || fixture >= 3)
        if (fact == EscapeFact.ScratchOn) return beat == 23 && (fixture == 0 || fixture == 3 || itemStates[8] != 2)
        if (fact == EscapeFact.BeepOn) return beat == 23 && (fixture == 1 || fixture == 3 || itemStates[8] != 2)
        if (fact == EscapeFact.HumOn) return beat == 23 && (fixture == 2 || fixture == 3 || itemStates[8] != 2)
        if (fact == EscapeFact.RadioClear) return beat == 24 && (fixture == 1 || fixture == 3) && solved[22] == 1 && solved[23] == 1
        if (fact == EscapeFact.CableConnected) return beat == 24 && (fixture == 2 || fixture == 3) && solved[23] == 1
        if (fact == EscapeFact.RouteA) return beat == 25 && fixture == 1 && itemStates[9] == 2 && solved[24] == 1
        if (fact == EscapeFact.RouteB) return beat == 25 && fixture == 2 && itemStates[9] == 2 && solved[24] == 1
        if (fact == EscapeFact.PressureReady) return pressureReady
        if (fact == EscapeFact.WindowA) return beat == 31 && itemStates[10] == 2 && solved[30] == 1 && (fixture == 0 || fixture == 4)
        if (fact == EscapeFact.WindowB) return beat == 31 && itemStates[10] == 2 && solved[30] == 1 && fixture == 1
        if (fact == EscapeFact.DangerousControl) return beat == 31 && fixture == 2
        if (fact == EscapeFact.FrontMatch) return beat == 32 && fixture != 0
        if (fact == EscapeFact.MiddleMatch) return beat == 32 && fixture != 1
        if (fact == EscapeFact.BackMatch) return beat == 32 && fixture != 2
        if (fact == EscapeFact.SameColor) return beat == 33 && itemStates[11] == 2 && solved[32] == 1 && (fixture == 1 || fixture >= 3)
        if (fact == EscapeFact.SamePattern) return beat == 33 && itemStates[11] == 2 && solved[32] == 1 && (fixture == 2 || fixture == 3)
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
        if (m == EscapeMeter.ShoeSide) return fixture == 0 || itemStates[3] != 2 ? 2 : 1
        if (m == EscapeMeter.StoneColor) return [1,2,3][fixture]
        if (m == EscapeMeter.SocketColor) return [2,2,3][fixture]
        if (m == EscapeMeter.Zoom) return fixture == 0 || itemStates[2] != 2 ? 2 : 3
        if (m == EscapeMeter.Temperature) return [19,20,40,41][fixture]
        if (m == EscapeMeter.Drops) return itemStates[7] != 2 ? 6 : [6,7,9,10][fixture]
        if (m == EscapeMeter.LeftWeight) return [7,5,3,5][fixture]
        if (m == EscapeMeter.RightWeight) return 5
        if (m == EscapeMeter.WireColor) return fixture
        if (m == EscapeMeter.LeafPoints) return fixture == 0 ? 3 : 4
        if (m == EscapeMeter.RPM) return [39,40,79,80][fixture]
        if (m == EscapeMeter.PressureTenths) return beat == 26 ? [47,48,50,51][fixture] : [20,30,20,30][fixture]
        if (m == EscapeMeter.PitchChange) return [10,25,-10,-25][fixture]
        if (m == EscapeMeter.PitchAngle) return pitch
        if (m == EscapeMeter.SensorNumber) return [1,2,3,0][fixture]
        if (m == EscapeMeter.CoreLights) return Math.max(0, (solved[32] ? 1 : 0) + (solved[33] ? 1 : 0) + (solved[34] ? 1 : 0) - (itemStates[12] != 2 || beat == 35 && fixture == 0 ? 1 : 0))
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
    function visualItemStates(): number[] {
        // Once a newly produced object leaves the machine, hide the machine's
        // source copy without changing the persistent cargo state. The cargo
        // sprite then becomes the same physical object traveling to its tray.
        if (operating || producingItem < 0 || reactionFrame < 3) return itemStates
        let states: number[] = []
        for (let i = 0; i < itemStates.length; i++) states.push(itemStates[i])
        states[producingItem] = 1
        return states
    }

    function draw() {
        if (ending > 0) scene.setBackgroundImage(escapeArt.ending(firstClear, secondClear, phase))
        else if (operating && focused) scene.setBackgroundImage(escapeArt.operating(station, beat, reactionBeat == beat && reactionFrame >= 0 ? reactionControl : fixture, solved, settledControls, itemStates, reactionBeat == beat ? response : -1, reactionBeat == beat ? reactionFrame : -1, pitch, phase))
        else scene.setBackgroundImage(escapeArt.world(room, solved, introduced, escapeFlow.focusBeat(room, solved, introduced), focused ? beat : -1, controls, response, reactionFrame, pitch, firstClear, reactionBeat, reactionControl, phase, settledControls, visualItemStates()))
    }

    function updateExplorer() {
        if (ending > 0) return
        let moving = Math.abs(player.vx) + Math.abs(player.vy) > 1
        if (Math.abs(player.vx) > Math.abs(player.vy) && Math.abs(player.vx) > 1) explorerFacing = player.vx < 0 ? 1 : 2
        else if (Math.abs(player.vy) > 1) explorerFacing = player.vy < 0 ? 3 : 0
        explorer.setPosition(player.x, player.y - 16)
        explorer.setImage(escapeArt.explorer(explorerFacing, moving ? phase % 3 + 1 : 0))
        explorer.setFlag(SpriteFlag.Invisible, operating)
    }

    function followMovingSprites() {
        if (ending > 0) return
        explorer.setPosition(player.x, player.y - 16)
        let carried = carriedItem()
        if (carried >= 0 && !operating) cargoSprites[carried].setPosition(player.x + 11, player.y - 21)
        if (scurryFrames > 0 && !operating) flame.setPosition(player.x + 6, player.y - 31)
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
        reactionBeat = beat
        reactionControl = fixture
        credible = matchesInput(beat, action)
        reactionFrame = 0
        producingItem = -1
        if (action == EscapeAction.FireFlare && credible) {
            scurryFrames = 12
            flame.setFlag(SpriteFlag.Invisible, false)
        }
        if (action == EscapeAction.SealStable) pressureReady = credible
        if (action == EscapeAction.SealLeak) pressureReady = false
        if (beat == 27) pressureReady = false
        let readyBefore: number[] = []
        for (let i = 0; i < escapeCargo.count; i++) readyBefore.push(escapeCargo.ready(i, solved) ? 1 : 0)
        let success = credible && prerequisitesMet(beat) && progressAction(beat, action)
        if (success) {
            solved[beat] = 1
            settledControls[beat] = fixture
            // Animate only a real not-ready -> ready transition. This avoids
            // re-producing an item when a solved station is operated again and
            // also handles the filter cassette, which becomes ready when the
            // last of four portrait beats succeeds (not necessarily beat 10).
            for (let i = 0; i < escapeCargo.count; i++) if (readyBefore[i] == 0 && escapeCargo.ready(i, solved) && itemStates[i] == 0) producingItem = i
            if (action == EscapeAction.LeverPull) {
                if (firstClear == 0) { firstClear = 1; ending = 1 }
                else { secondClear = 1; ending = 2 }
                leaveStation()
                explorer.setFlag(SpriteFlag.Invisible, true)
                controller.moveSprite(player, 0, 0)
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
        if (credible) { solved[28] = 1; settledControls[28] = fixture }
        response = EscapeAction.PitchUp
        reactionBeat = beat
        reactionControl = fixture
        reactionFrame = 0
        producingItem = -1
        save()
        draw()
    }

    controller.A.onEvent(ControllerButtonEvent.Pressed, function () {
        if (ending > 0) return
        if (busy || reactionFrame >= 0 || tossFrames > 0) return
        if (resetArmed) {
            cancelReset()
            return
        }
        let carried = carriedItem()
        if (carried < 0) {
            if (!operating) {
                let trayItem = nearSourceTray()
                if (trayItem >= 0) {
                    itemStates[trayItem] = 1
                    save()
                    updateCargoSprites()
                    draw()
                    return
                }
            }
        } else {
            let pad = nearPad(false)
            if (pad == escapeCargo.targetStation(carried)) {
                itemStates[carried] = 2
                save()
            } else tossHome(carried)
            updateCargoSprites()
            draw()
            return
        }
        if (player.x >= 588 && player.y >= 205 && player.y <= 275 && room < 4) {
            if (escapeFlow.roomComplete(room, solved)) { leaveStation(); room++; escapeFloor.install(room); player.setPosition(52, 264); save(); draw() }
            else player.sayText("The exit still needs its catches", 900, false)
            return
        }
        if (player.x <= 52 && player.y >= 205 && player.y <= 275 && room > 0) { leaveStation(); room--; escapeFloor.install(room); player.setPosition(600, 240); save(); draw(); return }
        updateNearbyStation()
        if (!focused) return
        busy = true
        let operatedBeat = beat
        let handler = handlers[operatedBeat]
        if (handler) { inAttempt = true; handler(); inAttempt = false }
        busy = false
        draw()
    })

    controller.B.onEvent(ControllerButtonEvent.Pressed, function () {
        if (ending > 0) {
            fresh()
            save()
            control.reset()
            return
        }
        updateNearbyStation()
        bPressedAt = control.millis()
        if (focused) {
            operating = true
            controller.moveSprite(player, 0, 0)
            player.vx = 0
            player.vy = 0
            explorer.setFlag(SpriteFlag.Invisible, true)
            flame.setFlag(SpriteFlag.Invisible, true)
            updateCargoSprites()
            draw()
        }
    })

    controller.B.onEvent(ControllerButtonEvent.Released, function () {
        if (ending > 0 || bPressedAt < 0) return
        bPressedAt = -1
        if (operating) {
            operating = false
            controller.moveSprite(player, 150, 150)
            explorer.setFlag(SpriteFlag.Invisible, false)
            if (scurryFrames > 0) flame.setFlag(SpriteFlag.Invisible, false)
            updateCargoSprites()
            draw()
            return
        }
        if (focused) return
        if (room == 0 && player.x <= 52) {
            if (resetArmed) clearThisGame()
            else {
                resetArmed = true
                player.sayText("Press B again to reset. A cancels.", 1500, false)
            }
        }
    })

    controller.left.onEvent(ControllerButtonEvent.Pressed, function () {
        if (operating) {
            if (reactionFrame >= 0) return
            fixture = (fixture + fixtureCount(beat) - 1) % fixtureCount(beat)
            controls[beat] = fixture
            save()
            draw()
            return
        }
        cancelReset()
    })
    controller.right.onEvent(ControllerButtonEvent.Pressed, function () {
        if (operating) {
            if (reactionFrame >= 0) return
            fixture = (fixture + 1) % fixtureCount(beat)
            controls[beat] = fixture
            save()
            draw()
            return
        }
        cancelReset()
    })
    controller.up.onEvent(ControllerButtonEvent.Pressed, function () {
        if (operating && reactionFrame >= 0) return
        if (operating && beat > firstBeats[station]) { beat--; fixture = controls[beat]; draw(); return }
        cancelReset()
    })
    controller.down.onEvent(ControllerButtonEvent.Pressed, function () {
        if (operating && reactionFrame >= 0) return
        if (operating && beat < lastBeats[station]) { beat++; fixture = controls[beat]; draw(); return }
        cancelReset()
    })

    load()
    escapeArt.installPalette()
    escapeFloor.install(room)
    let feet = image.create(12, 10)
    feet.fill(1)
    player = sprites.create(feet, SpriteKind.Player)
    player.setFlag(SpriteFlag.Invisible, true)
    player.setPosition(320, 250)
    controller.moveSprite(player, 150, 150)
    player.setStayInScreen(true)
    explorer = sprites.create(escapeArt.explorer(0, 0), SpriteKind.Projectile)
    explorer.setFlag(SpriteFlag.Ghost, true)
    explorer.setPosition(player.x, player.y - 16)
    for (let i = 0; i < escapeCargo.count; i++) {
        let cargo = sprites.create(escapeCargo.drawItem(i, 0), SpriteKind.Projectile)
        cargo.setFlag(SpriteFlag.Ghost, true)
        cargo.setFlag(SpriteFlag.Invisible, true)
        cargoSprites.push(cargo)
    }
    for (let i = 0; i < 3; i++) {
        let flameImage = image.create(10, 14)
        // A tiny local scurry flame: asymmetric outer tongue, bright inner
        // core and one short-lived ember. It stays 10x14 as contracted.
        flameImage.setPixel(4 + (i == 1 ? -1 : 1), 0, 5)
        flameImage.setPixel(5 - (i == 2 ? 1 : 0), 2, 4)
        flameImage.fillRect(3, 4, 5, 7, 4)
        flameImage.fillRect(2 + (i == 0 ? 1 : 0), 7, 7, 4, 4)
        flameImage.fillRect(4, 7 + (i == 2 ? 1 : 0), 3, 6, 5)
        flameImage.setPixel(5, 6, 10)
        flameImage.setPixel(i == 1 ? 1 : 8, 3 + i, i == 2 ? 10 : 5)
        flameImage.setPixel(i == 0 ? 8 : 1, 10 - i, 4)
        flameFrames.push(flameImage)
    }
    flame = sprites.create(flameFrames[0], SpriteKind.Projectile)
    flame.setFlag(SpriteFlag.Ghost, true)
    flame.setFlag(SpriteFlag.Invisible, true)
    if (ending > 0) { explorer.setFlag(SpriteFlag.Invisible, true); controller.moveSprite(player, 0, 0) }
    game.onUpdate(function () { followMovingSprites() })
    game.onUpdateInterval(120, function () {
        phase++
        if (reactionFrame >= 0) {
            reactionFrame++
            if (reactionFrame > 12) { reactionFrame = -1; response = -1; reactionBeat = -1; producingItem = -1 }
        }
        if (scurryFrames > 0) {
            flame.setImage(flameFrames[phase % 3])
            flame.setPosition(player.x + 6, player.y - 31)
            scurryFrames--
            if (scurryFrames == 0) flame.setFlag(SpriteFlag.Invisible, true)
        }
        if (tossFrames > 0) { tossFrames--; if (tossFrames == 0) tossItem = -1 }
        updateNearbyStation()
        updateExplorer()
        updateCargoSprites()
        draw()
    })
    updateCargoSprites()
    draw()
}
```
