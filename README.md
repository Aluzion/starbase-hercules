# starbase-hercules

[![StarBase Hercules](/assets/hercules-front.small.png)](/assets/hercules-front.png)


## Features

* Endo-gernomic™ seats and dashboard.
* Maximum speed (no cargo).
* Modular cargo system.
* Cartesian coordinate targeting system with 180/180 view.
* Mining Laser and Ore Collector duty cycle.
* Armored Charodium blast cage.
* Warp Drive Core.
* Moon landing gear.
* Rear Cargo Lock Beams.
* Internal Radiators.
* ISAN Navigation.
* 30 Waypoint System.

## Quick Start Guide

1. There are no flight controls within reach. Most default key bindings are used. For advanced use see [Recommended Key Bindings](#recommended-key-bindings).
1. Once seated enable *-1* low, or *+1* high multiplier scaling with `C4`. See [Flight Controls](#flight-controls).
1. When in flight turn *On* Cruise Control and Power Management with `R2`. See [Power Management](#power-management).
1. Turn *On* the Range Finder with `C6`. See [Targeting System](#targeting-system).
1. Fire Weapons with `L1` or turn *On* the Mining Lasers with `L2`.

## Control Panel

| | [L]eft | [C]enter | [R]ight |
| :-: | :- | :- | :- |
| | [![Controls Left Side](/assets/hercules-control-left.thumb.png)](/assets/hercules-control-left.png) | [![Controls Main](/assets/hercules-control-main.thumb.png)](/assets/hercules-control-main.png) | [![Controls Right Side](/assets/hercules-control-right.thumb.png)](assets/hercules-control-right.png) |
| 1 | Weapons Fire (`Fire: [SPACE]`) | Forward Thrust (`FcuForward: [SHIFT]`) | Material Scanners (`Scanner: [L-ALT]`) |
| 2 | Mining Lasers (`MiningLaserOn: [SPACE]`) | Forward Thrust Multiplier (`FcuForwardMultiplier`)| Cruise Control (`Cruise: [Z]`) |
| 3 | Transponder (`Transponder`) | Backward, Pitch, Yaw and Roll Thrust Multiplier (`FcuGeneralMultiplier`)| Rear Cargo Lock Beams (`CLock`) |
| 4 | Waypoints. See [30 Waypoints System](https://github.com/Archaegeo/Starbase/tree/main/ISAN-Waypoint%20System). | Thrust Multiplier Selection. `-1`: low, `+1`: high.  See [Flight Controls](#flight-controls). | Fuel display with averaged consumption/s, remaining units for 2x top and 2x right chambers. |
| 5 | | Target Range (`Trng`). See [Targeting System](#targeting-system). | Fuel display with estimated time remaining, remaining units for 2x bottom and 2x left chambers. |
| 6 | | On/Off Targeting Range Finder. (`RangeFinder: [KEYPAD-0]`). | Gas display with estimated time reminaing, averaged consuption/s, and remaining gas units. |
| 7 | | Center Targeting Range Finder (`TReset: [KEYPAD-5]`) | |


## Flight Controls

The ship uses dual flight-controllers (`FcuForwardMultiplier` and `FcuGeneralMultiplier`) with a separate variable for each. This allows separate control of the forward thrust and the remaining trim controls for `FcuBackward`, `FcuRotationalPitch`, `FcuRotationalYaw` and `FcuRotationalRoll`. All of the flight controls are mounted underneath the pilot's seat to reduce clutter the increase visibility. The multipliers can be changed quickly on the main control panel (`C4`), or with custom key bindings for more granular control.

> **Note**: The default multiplier uses a `FcuForwardMultiplier` of `70%`. This provides the optimal power and performance ratios with the default cargo module. The optimal ratios very depending on the mass of the cargo.

See [Control Panel](#control-panel), [Recommended Key Bindings](#recommended-key-bindings)

## Power Management 

Power is managed automatically. 
* High-idle mode is enabled as soon as the ship spawns and the fuel chambers up warmed up and set to 50%. This mode is disabled when the batteries are full (above 95%) for 2 consecutive minutes and can be re-enabled manually by toggling `Cruise` either on or off.
* When `Cruise` is activated `FcuForward` scaling is enabled. When the battery power drop below 50% `FcuForward` is gradually reduced in order to avoid depleting the batteries. When using the cargo lock-beam (`Clock`) to tow heavy modules then special attention must be given to the stored power level to ensure the cargo lock-beam is maintained while in flight.

> **Note:** The power management script will only reduce the `FcuForward` control when `Cruise` is *On* and `StoredBatteryPower` < 50%. 

## Targeting System

All weapon and tools utilize a 3D Polar to Cartesian target coordinate system. Each tool/weapon has a dedicated yolol script to reduce targeting latency and fencing to prevent activation while pointed towards the ship.

See [Control Panel](#control-panel)

Key bindings are required in order to "point" the targeting system. When the range finder (`Trng`) is disabled all of the weapons/tools point straight ahead. When the range finder is enabled all of the weapons/tools will point towards the target. If the range finder has no target in range, the `TARGETRANGE+` and `TARGETRANGE-` can be used to increase or decrease the target range manually.

When a tool/weapon is obstructed by the ship and unable to safely point in the direction of the target it will remain stationary and the tool/weapon is disabled in order to prevent firing when triggered. Special fields are modified on the weapons/tools to disable them in order to speed up weapon readiness once a safe LOS is re-established.

> **Note**: Advanced YOLOL Chips are used without trigonomic functions (SIN, COS, TAN). Polynomial approximations are substituted and the polar plane is translated in order to improve accuracy at desired angles. Not all angles have the same accuracy.

## Modular Cargo System

> **CAUTION**: Improper use of the cargo docking routine may cause loss of the cargo and/or damage to the ship. All Endo's should commit the following module to static memory.

![Modular Cargo System](/assets/hercules-back.png)

> **Still in development**


| [![Cargo LOS](/assets/hercules-cargo.thumb.png)](/assets/hercules-cargo.png) | [![Cargo LOS](/assets/hercules-cargo-1.thumb.png)](/assets/hercules-cargo-1.png) | [![Cargo LOS](/assets/hercules-cargo-2.thumb.png)](/assets/hercules-cargo-2.png) | [![Cargo LOS](/assets/hercules-weld-beams.thumb.png)](/assets/hercules-weld-beams.png) |
| :-: | :-: | :-: | :-: |
| Figure 1 | Figure 2 | Figure 3 | Figure 4 |

The cargo docking system will automatically "dock" a compatible cargo module up to 100m away ([Figure 1](/assets/hercules-cargo.png)). The heavier a cargo module is, the longer it takes to dock/undock. Once a cargo module is docked it has the option to connect to the ships cable and pipe network, or it can run a separate independant network.

When the docking routine is enabled the rear facing tractor beam will use a straight LOS to "lock" on to a cargo module up to 100m away ([Figure 3](/assets/hercules-cargo-2.png)). The ship should be oriented to point towards the cargo module using the flight controls in the rear seat ([Figure 2](/assets/hercules-cargo-1.png)).

Once the cargo is docked, it can be towed by either using the cargo lock-beams, or welded to the ship on both sides ([Figure 4](/assets/hercules-weld-beams.png)). The cargo lock-beams (`CLock`) can be used to manually release the cargo while in flight, but with heavy cargo modules this may consume more power than the ship is able to generate, unless the cargo module is able to assist with its own power generation. 

> **Note**: The ship strength rating will be greatly reduced while towing an unwelded cargo module with only the cargo lock-beams. This introduces different forces on the ship and the cargo module.

The rear seat of the ship includes a full set of flight controls and multiplier scaling to allow ship movement and orientation prior to docking. 

| | [![Control Rear](/assets/hercules-control-rear.thumb.png)](/assets/hercules-control-rear.png) |
| :-: | :- |
| R1 | The force being applied to push/pull the cargo (`CForce`). |
| R2 | The torque being applied to the pitch/yaw/roll the cargo (`CTorque`). |
| R3 | Turn `On`/`Off` the docking routine (`CRun`). See below for more information. |
| R4 | The rangefinder distance to the cargo in meters (`CRangeT`). |
| R5 | The projected position to dock the cargo (`CTo`). |
| R6 | Turn `On`/`Off` the Cargo Lock Beams (`Clock`).  |
| R7 | The `Pitch` angle in degrees (-180 to 180). This is only updated during the Torque phase (#3) of the docking routine. |
| R8 | The `Pitch` angle sign, `-1` for negative angles, `+1` for positive angles. |
| R9 | The `Pitch` multiplier. `On` for 180 degrees, `Off` for 90 degrees. |
| R10 | The `Yaw` angle in degrees (-180 to 180). This is only updated during the Torque phase (#3) of the docking routine. |
| R11 | The `Yaw` angle sign, `-1` for negative angles, `+1` for positive angles. |
| R12 | The `Yaw` multiplier. `On` for 180 degrees, `Off` for 90 degrees. |
| R13 | The `Roll` angle in degrees (-180 to 180). This is only updated during the Torque phase (#3) of the docking routine. |
| R14 | The `Roll` angle sign, `-1` for negative angles, `+1` for positive angles. |
| R15 | The `Roll` multiplier. `On` for 180 degrees, `Off` for 90 degrees. |


> **Note**: To undock a cargo module the docking routine can be used to initially push the cargo to a safe distance before using the thrusters to move away.

### Docking Routine

The docking routine is a series of automated steps that are run in series to dock/undock the cargo. The routine can be stopped at any time by turning `Off` the button (`CRun`). The routine will always start at the beginning of the following steps when manually restarted.

The color of the button (`CRun`) indicates which step the routine is on:

| Step | Color | Description |
| :-: | :- | :- |
| 0 | Black | Off. Click `CRun` to start routine. |
| 1 | Solid Red | Initializing, attempt to grab cargo with beam. |
| 2 | Blinking Red | Force cargo to get rough cargo size and push it to a minimum safe distance (`CTo`). Wide cargo (width > length) may not be pushed far enough out and may collide with the ship's thrusters when torqued. The routine can be turned off and on again in order to gain additional distance before being torqued. |
| 3 | Solid Orange | Torque cargo and adjust pitch, yaw and roll. Adjustments can be made to these 3 angles only at this time. |
| 4 | Blinking Orange | Get precise cargo size and calculate position to (`CTo`). This distance varies for different length cargo modules. |
| 5 | Blinking Blue | Force cargo and pull to dock. Force and torque applied to the cargo is weaker the closer it gets to mitigate damage. Once this step is active the cargo should have the proper pitch, yaw and roll to be pulled directly to dock. If the orientation is not straight stop and restart the docking routine. |
| 6 | Blinking Green | Enable Cargo Lock Beams (`CLock`). Disabling the routine does not disable the Cargo Lock Beams. |
| 7 | Solid Green | Cargo Lock Beams (`CLock`) successfully locked. Turn Off. |

> **Note**: "Force" is the pushing/pulling and "Torque" is the rotation of the pitch, yaw and roll. In each step of the routine the cargo is either forced or torqued, but never both at the same time. In some cases the routine may backtrack to earlier steps when an unexpected force or torque is detected. 

## YOLOL Script Reference

Horizontal scaling of yolol compute for abstraction and performance.

### Right Rack

| Row | 1 | 2 | 3 | 4 |
| :-: | - | - | - | - |
| RA | [Turret TRT Top Right (Top)](/yolol/ra1.yolol) | [Turret TRR Top Right (Right)](/yolol/ra2.yolol) | [Turret TRB Top Right (Bottom)](/yolol/ra3.yolol) | [Turret TRL Top Right (Left)](/yolol/ra4.yolol) |
| RB | [Turret BRT Bottom Right (Top)](/yolol/rb1.yolol) | [Turret BRR Bottom Right (Right)](/yolol/rb2.yolol) | [Turret BRB Bottom Right (Bottom)](/yolol/rb3.yolol) | [Turret BRL Bottom Right (Left)](/yolol/rb4.yolol) |
| RC | [Turret FL Front (Left)](/yolol/rc1.yolol) | [Turret FR Front (Right)](/yolol/rc2.yolol) | [Targeting](/yolol/rc3.yolol) | **MC** [Targeting](/yolol/rc4.yolol) |
| RD | [Mining Laser Duty Cycle](/yolol/rd1.yolol) | [Ore Collector Duty Cycle](/yolol/rd2.yolol) | [Fcu Multiplier Scaling](/yolol/rd3.yolol) | - |
| RE | [NTP](/yolol/re1.yolol) | [Clock](/yolol/re2.yolol) | [Power Management](/yolol/re3.yolol) | - |
| RF | [Fuel Display](/yolol/rf1.yolol) | [Gas Display](/yolol/rf2.yolol) | [Material Scanner(s)](/yolol/rf3.yolol) | - |

### Left Rack

| Row | 1 | 2 | 3 | 4 |
| :-: | - | - | - | - |
| RG | [Turret TLT Top Left (Top)](/yolol/rg1.yolol) | [Turret TLB Top Left (Right)](/yolol/rg2.yolol) | [Turret TLB Top Left (Bottom)](/yolol/rg3.yolol) | [Turret TLL Top Left (Left)](/yolol/rg4.yolol) |
| RH | [Turret BLT Bottom Left (Top)](/yolol/rh1.yolol) | [Turret BLR Bottom Left (Right)](/yolol/rh2.yolol) | [Turret BLB Bottom Left (Bottom)](/yolol/rh3.yolol) | [Turret BLB Bottom Left (Left)](/yolol/rh4.yolol) |
| RI | [ISAN](/yolol/ri1.yolol). See [Repository](https://github.com/Collective-SB/ISAN) | - | **MC** [Waypoint System](/yolol/ri3.yolol). See [Repository](https://github.com/Archaegeo/Starbase/tree/main/ISAN-Waypoint%20System) | **MC** [Waypoint System](/yolol/ri4.yolol) |
| RJ | [Waypoint System](/yolol/rj1.yolol) | [Waypoint System](/yolol/rj2.yolol) | [Waypoint System](/yolol/rj3.yolol) | [Waypoint System](/yolol/rj4.yolol) |
| RK | **MC** [Waypoints 1-10](/yolol/rk1.yolol) | **MC** [Waypoints 11-20](/yolol/rk2.yolol) | **MC** [Waypoints 21-30](/yolol/rk3.yolol) | - |

### Rear Rack

[Cargo Docking Routine](/yolol/cargo.yolol) is located directly above the rear cargo seat.

## Recommended Key Bindings

| Function | Key | Control Panel |
| :- | :- | :- |
| `CRUISE` | `Z` | `R2` |
| `FCUBACKWARD+` | `BACKSPACE` |
| `FCUFORWARD+` | `SHIFT` |
| `FCUFORWARD-` | `CTRL` |
| `FCUFORWARDMULTIPLIER+` | `INSERT` |
| `FCUFORWARDMULTIPLIER-` | `DELETE` |
| `FCUGENERALMULTIPLIER+` | `HOME` |
| `FCUGENERALMULTIPLIER-` | `END` |
| `FCURIGHTLEFT+` | `RIGHT` |
| `FCURIGHTLEFT-` | `LEFT` |
| `FCUROTATIONALPITCH+` | `S` |
| `FCUROTATIONALPITCH-` | `W` |
| `FCUROTATIONALROLL+` | `D` |
| `FCUROTATIONALROLL-` | `A` |
| `FCUROTATIONALYAW+` | `E` |
| `FCUROTATIONALYAW-` | `Q` |
| `FCUUPDOWN+` | `UP` |
| `FCUUPDOWN-` | `DOWN` |
| `FIRE` | `SPACE` | `L1` |
| `MININGLASERON` | `SPACE` | `L2` |
| `ORECOLLECTORON` | `X` | `R...` |
| `RANGEFINGER` | `KP_INSERT` | `C6` |
| `SCANNER` | `ALT` | `R1` |
| `TARGETPITCH+` | `KP_UP` |
| `TARGETPITCH-` | `KP_DOWN` |
| `TARGETROTATION+` | `KP_RIGHT` |
| `TARGETROTATION-` | `KP_LEFT` |
| `TARGETRANGE+` | `PRIOR` |
| `TARGETRANGE-` | `NEXT` |
| `TRESET` | `KP_BEGIN` | `C7` |

## Design Notes

* High visibility.
* High strength and low weight prioritized over form and cosmetics.
* Accessibile cable and pipe networks to ease repairs.
* Compact design with minimal internal space to reduce weight.
* Avoid yolol buffers and proxies for responsive controls.
* Never produce automated or unexpected movement in flight control. 

## Limitations and Warranty

* As-Is Where Is

### Get Support, Provide Feedback

* [Browse the issues](https://github.com/Aluzion/starbase-hercules/issues) to read existing discussions. 
* [Post a new issue](https://github.com/Aluzion/starbase-hercules/issues/new) to post a bug, ask a question or  provide feedback. :)
