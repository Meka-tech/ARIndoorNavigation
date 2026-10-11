# Augmented Reality Indoor Navigation via LiDAR Mapping and Target Tracking

[![Conference](https://img.shields.io/badge/IEEE%20NIGERCON-2026%20Accepted-blue.svg)](https://attend.ieee.org/nigercon-2026/)
[![Engine](https://img.shields.io/badge/Engine-Unity-green.svg)]()
[![License](https://img.shields.io/badge/License-MIT-lightgrey.svg)](LICENSE)

Companion software and interface assets for the research paper:

> **"Augmented Reality Indoor Navigation: A Smartphone-Based Approach via LiDAR Mapping and Target Tracking"**
> *Accepted at the 2026 IEEE Nigeria International Conference on Digital Transformation (NIGERCON), 5-6 November 2026, University of Lagos*
> **Authors:** Favour Mokwenye, Bonaventure Ekengwu, Eugene Chinedu Ebere, Samuel Nnaemeka Onyeji
> **Affiliation:** Department of Electronic and Computer Engineering, University of Nigeria, Nsukka

This project builds on [FireDragonGameStudio/ARIndoorNavigation](https://github.com/FireDragonGameStudio/ARIndoorNavigation) (MIT, Copyright (c) 2018 Markus Altenhofer). See [Acknowledgements](#7-acknowledgements).

---
<img height="400" alt="S4" src="https://github.com/user-attachments/assets/d393d04b-adb8-4ce9-a22a-0c5b24f05db8" />

## 1. System Overview

Printed maps and fixed signage are often inadequate for finding your way inside large buildings. This project is a smartphone AR navigation system that works without powered Bluetooth Low Energy (BLE) beacons or Wi-Fi positioning infrastructure:

* **Offline mapping:** the building is scanned once with an iPhone 13 Pro LiDAR sensor using Polycam, exported as `.obj` / `.fbx`, and brought into Unity, where the NavMesh is baked.
* **Image-target anchoring:** the user's position is set by scanning an unpowered Vuforia image target, then carried forward by the phone's own motion tracking. LiDAR is used for offline mapping only, not for real-time localization.
* **Route guidance:** Unity's NavMesh computes the shortest walkable path around obstacles in the scanned mesh. The AR overlay shows the path, a directional arrow, a destination pin and room information.

---

## 2. Research Team and Roles

### Favour Mokwenye: First Author, Researcher, Interface Designer and Usability Lead
* **Interface design:** designed the mobile AR wayfinding interface, including directional arrows, destination pins and room information overlays.
* **Navigation flows:** structured the user flows for destination selection and turn-by-turn guidance.
* **Usability evaluation:** formulated the two-stage evaluation (user acceptance testing, then a usability study with n = 10), and analysed System Usability Scale (SUS) scores and task completion times.
* **Manuscript:** led the literature review, research framing, analysis and primary drafting of the paper.

### Samuel Nnaemeka Onyeji: Researcher, Unity 3D Systems Specialist and Developer
* **Engine architecture:** configured the core Unity AR scene logic, camera feeds and runtime state management.
* **Pathfinding:** baked the NavMesh from the exported LiDAR mesh and built the navigation controller for shortest walkable path computation.
* **Build pipeline:** managed the Android SDK/NDK build pipeline and device deployment.

### Eugene Chinedu Ebere: Researcher, Computer Vision and Object Tracking
* **Vuforia integration:** configured the Vuforia SDK in Unity and the image target recognition pipeline.
* **Target database:** managed the Vuforia Target Manager database, including target properties and multi-target settings.
* **Target placement:** handled placement and calibration of physical targets in the building.

### Engr. Dr. Bonaventure O. Ekengwu: Project Supervisor and Co-author
* **Supervision:** supervised the project at the Department of Electronic and Computer Engineering, University of Nigeria, Nsukka.
* **Review:** provided manuscript review and guidance for conference submission.

---

## 3. Repository Structure

```text
├── Assets/            # Unity project assets, scripts and scenes
├── Packages/          # Unity package manifest
├── ProjectSettings/   # Unity project settings
├── UserSettings/      # Unity editor user settings
├── UX-Assets/         # Interface design assets, exported as PNG (Favour Mokwenye)
├── .gitignore
├── .vsconfig
└── LICENSE
```

---

## 4. Tools and Devices

* **Engine:** Unity with AR Foundation (Google ARCore, Apple ARKit, AR Tracked Image Manager)
* **Tracking:** Vuforia Engine SDK
* **Offline capture:** iPhone 13 Pro LiDAR with Polycam, exported as `.obj` / `.fbx`
* **Navigation:** Unity NavMesh
* **Build toolchain:** Android SDK and NDK
* **Test device:** Samsung Galaxy A21 (no LiDAR), used for navigation during evaluation
* **Language:** C#
* **Version control:** Git and GitHub

---

## 5. Evaluation Summary

The system was evaluated in a faculty building at the University of Nigeria, Nsukka. A three-participant user acceptance test was followed by a usability study with ten participants across three navigation legs.

| Measure | Result |
| --- | --- |
| Mean SUS score | 85.0 (SD = 6.87) |
| Mean task completion time | 46.3 s (SD = 5.36) |
| Leg 1 / Leg 2 / Leg 3 (mean) | 19.2 s / 12.5 s / 14.6 s |

* **Usability:** a mean SUS score of 85.0 falls in the "excellent" band under the interpretation of Bangor et al.
* **Initial acquisition:** Leg 1 took longer than Leg 2, consistent with the time needed to acquire the first image target.
* **Dynamic conditions:** every participant completed the obstacle and dynamic-environment scenarios without major incident.

---

## 6. Limitations

* Occasional drift was observed between the walked path and the path drawn in the AR interface, mostly in the first round of user acceptance testing. This was observed during testing and was **not measured quantitatively**.
* The evaluation covers ten participants in a single building, so it is a pilot-scale result and does not establish how the system behaves in other environments.
* No comparison was made against non-digital alternatives such as printed signage or a standard map application.
* Multi-floor routing and multi-language support are future work.

---

## 7. Acknowledgements

This repository is a fork of [FireDragonGameStudio/ARIndoorNavigation](https://github.com/FireDragonGameStudio/ARIndoorNavigation), released under the MIT License, Copyright (c) 2018 Markus Altenhofer. The original licence and copyright notice are retained in [LICENSE](LICENSE). Our work extends that project for the system described in the paper above.

---

## 8. Getting Started

1. Clone the repository and open it in Unity. The editor version is in `ProjectSettings/ProjectVersion.txt`.
2. Add your own Vuforia licence key in the Vuforia configuration. Do not commit licence keys.
3. Import your Vuforia target database and place the matching printed targets in the building.
4. Build to an Android device.
