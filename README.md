# FTC Team 26744 — Lion Robotics Black
**Clear Lake, Iowa** | Season: INTO THE DEEP 2024–25

> Programmer: Arman Nikoueiha (Freshman) — first year in FTC

---

## Overview

This was the inaugural season for Team 26744, a brand new team spun up from the Lion Robotics program. As the team's programmer in my **freshman year**, I was responsible for all software on a robot built from scratch — from basic teleop controls to a tuned Roadrunner autonomous achieving a consistent **5-specimen autonomous routine**.

The season was a genuine learning experience: we started with On Bot Java, hit real limitations, made the call to migrate to Android Studio and Roadrunner mid-season, tuned the system from scratch, and iterated steadily until the software had been pushed to the ceiling of what the robot's mechanical design could support.

---

## Robot Overview

The robot was designed around a **pivot arm + linear slide** system for scoring specimens on the high chamber and collecting samples from the submersible. A key mid-season upgrade was adding a **rotating wrist** to the claw, which allowed specimen orientation correction without turning the entire robot — critical for fast cycling.

**Subsystems:**
- Mecanum drivetrain — field-centric driving and strafing
- Pivot arm with single-stage linear slide extender
- 3D-printed claw with rotating wrist
- Secondary arm for extended reach into the submersible

---

## Software Highlights

### Migrating from On Bot Java to Android Studio + Roadrunner
At the start of the season we used **On Bot Java**, an FTC-specific browser-based editor. We quickly ran into its core limitations — no version control and no support for external libraries like Roadrunner or ftclib.

After attending a **programming and autonomous workshop hosted by Team 21311** (Lion Robotics Gold), we made the switch to Android Studio and Roadrunner. This gave us:
- Git-based version control
- Access to Roadrunner's spline path generation and odometry-based self-correction
- A tunable, consistent autonomous that eventually hit **5 specimens per match**

---

### Roadrunner Tuning
Roadrunner requires careful per-robot calibration. The key tuning steps we worked through:

- Calibrated **inches per tick** on dead wheel odometry pods to accurately map encoder ticks to real-world distance
- Tuned **PIDF values** for the reactionary path follower
- Adjusted **kV, kA, and kS** feed-forward constants for the motion profiles
- Iteratively tested and refined autonomous path timing through repeated competition and practice cycles

The tuning paid off — we ultimately achieved a reliable 5-specimen autonomous routine.

---

### Heading Lock (PIDF Drivetrain Stabilization)
A persistent problem mid-season was heading drift caused by uneven weight distribution when the pivot arm extended. Our initial fix was a 3-pound steel counterweight — functional but inelegant.

We replaced this with a proper software solution: a **PIDF heading lock** that actively corrects heading error while strafing. This could be toggled on/off via a controller button, giving the driver control while keeping the robot pointed in the right direction during precision maneuvers.

---

### Teleop Macros (One-Button Preset Positions)
To reduce driver cognitive load during fast-paced matches, we implemented a **macro system** — preset arm/slide/wrist positions that could be reached with a single button press. The four key macros were:

| Macro | Function |
|---|---|
| Starting position | Compact driving configuration |
| Submersible grab | Arm/slide extended for sample collection |
| Wall specimen grab | Pivot and wrist configured for human player zone |
| Specimen place | Arm raised, wrist corrected for high chamber |

This let the driver focus on field navigation rather than manually positioning each joint.

---

### Distance Sensor Wall Approach
Retrieving specimens from the wall required high positional precision. We integrated a distance sensor that fed real-time readings to the drivetrain, implementing a velocity ramp-down as the robot approached the wall. This significantly improved specimen pickup consistency without requiring perfect driver input.

---

### Absolute Encoder for Pivot Accuracy
An early reliability problem was the pivot slides drifting from their target positions. The root cause: the motor encoder was measuring gearbox rotation rather than actual axle position, introducing error that accumulated over a match.

The fix was switching to a **REV absolute encoder** mounted directly on the pivot axle. Unlike relative motor encoders, absolute encoders measure true angular position — so the robot always knows exactly where the pivot is, regardless of slip or startup position. This fixed our positioning issues and was a key step toward a consistent autonomous.

---

### Odometry Upgrade: Pinpoint IMU Computer
Our first autonomous used the Control Hub's built-in IMU for heading. We quickly discovered it was highly susceptible to **ESD (ElectroStatic Discharge)** — the IMU would reset from static buildup on the competition field, immediately breaking our path following.

We upgraded to a **GoBilda Pinpoint odometry computer**, which integrates our two dead wheel pods for position and is far more ESD-resistant. The improvement was immediate and made our autonomous dramatically more reliable match-to-match.

---

### 5-Specimen No-Preload Autonomous
A strategic programming decision late in the season: rather than using a specimen preload, we built an autonomous that picks up 5 specimens entirely from the field. This freed our alliance partner to use both of their preloads while we still scored 5 specimens — a net advantage for the alliance.

---

## Software at the Ceiling of Mechanical Potential

By the end of the season, the software had been optimized to the ceiling of what the robot's hardware could support. Every major software problem had been diagnosed and solved — ESD-resistant odometry, absolute encoder pivot positioning, PIDF heading stabilization, distance-sensor-assisted wall approach, and a fully tuned 5-specimen autonomous. The code was reliable and consistent.

The limiting factor was mechanical. The pivot arm used a gear-driven system that introduced **backlash** — lost motion from gaps between gear teeth — which caused wobble under load and made precise high-chamber placements inconsistent. There is no software fix for backlash; it is a fundamental property of gear-driven mechanisms. No amount of tuning could fully compensate for the mechanical play.

This gap between software capability and mechanical limitation was one of the most important lessons of the season. It informed our future plans directly: a planned redesign around a **capstan drive** (a rope-and-drum system) that eliminates backlash entirely through friction rather than gear mesh. The software was ready. The robot needed to catch up.

---

## What I Learned

This was my first year programming a competition robot. The biggest lessons:

- **Tooling matters** — switching from On Bot Java to Android Studio + Roadrunner mid-season was the right call even though it cost time
- **Hardware and software are coupled** — many of our "software problems" (heading drift, position inaccuracy) were actually hardware problems with software workarounds. The real fixes came from hardware changes (absolute encoder, Pinpoint)
- **Software can be optimized past its hardware** — by the end of the season the code was as good as it could be given the mechanical constraints. Understanding where that ceiling is, and why, is a skill in itself
- **Iteration is everything** — our autonomous improved through disciplined testing and a willingness to change approach when something wasn't working

---

## Stack
- **Language:** Java
- **IDE:** Android Studio
- **Autonomous:** Roadrunner (spline paths + odometry PIDF)
- **Odometry:** GoBilda Pinpoint Computer + 2x dead wheels
- **Notable Sensors:** REV absolute encoder (pivot), distance sensor (wall approach)

---

*Team 26744 — Lion Robotics Black | Clear Lake, Iowa | Inaugural Season 2024–25*
