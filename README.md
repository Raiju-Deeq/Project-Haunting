<!-- HEADER -->
<div align="center">

<img src="project haunting.png" width="600" alt="Haunting Invitation Banner"/>

# Haunting Invitation

### *formerly developed as Project Haunting*

[![Steam](https://img.shields.io/badge/Available_on-Steam-1b2838?style=for-the-badge&logo=steam&logoColor=white)](https://store.steampowered.com)
[![Unreal Engine](https://img.shields.io/badge/Unreal_Engine-5.3.2-313131?style=for-the-badge&logo=unrealengine&logoColor=white)](https://www.unrealengine.com)
[![Published by DMU](https://img.shields.io/badge/Published_by-De_Montfort_University-C8102E?style=for-the-badge)](https://www.dmu.ac.uk)
[![Award](https://img.shields.io/badge/🏆_Best_Group_Project-DMU_End_of_Year_Show-gold?style=for-the-badge)](#awards--recognition)

</div>

---

## 🏆 Awards & Recognition

> **🥇 Best Group Project — De Montfort University End of Year Show**
>
> *Haunting Invitation* was awarded **Best Group Project** at DMU's End of Year Showcase, beating out competing student titles across the entire Games Production cohort.

> **🎮 Launched on Steam**
>
> The game officially launched on **Steam** under the title **Haunting Invitation**, published by De Montfort University — one of a select number of student projects from DMU to reach a commercial storefront.

---

## 🎮 About the Game

**Haunting Invitation** is a first-person survival horror game set inside the decaying rooms of Hollow Manor. Players must explore procedurally generated environments, evade a relentless AI-driven enemy, and craft tools to uncover the manor's dark secrets — all before the invitation expires.

Built as a **group project** by second-year BSc Games Production students at **De Montfort University**, the game shipped from concept to Steam in a single academic year.

| Detail | Info |
|---|---|
| **Engine** | Unreal Engine 5.3.2 |
| **Platform** | PC (Steam) |
| **Genre** | Survival Horror / Puzzle |
| **Publisher** | De Montfort University |
| **ESRB Rating** | Teen |
| **Development Period** | 2024–2025 |

---

## 👥 Team

| Role | Name |
|---|---|
| Product Owner / Tech Developer | Mohamed Deeq Mohamed |
| Scrum Master | Dahna Aldrighetti |
| Tech Developer | Benjamin |

---

## 🔑 Core Features

### 🗺️ Procedural Room Generation
Hollow Manor's layout is never the same twice. Modular, prebuilt rooms are assembled at runtime using a controlled PCG workflow, with a designer-override fallback system ensuring quality-assured layouts every run.

```cpp
// DataTable Entry for Room Compatibility
USTRUCT(BlueprintType)
struct FRoomData : public FTableRowBase {
    GENERATED_BODY()
    UPROPERTY(EditAnywhere)
    FName RoomID;
    UPROPERTY(EditAnywhere)
    TArray<FName> CompatibleRooms;  // e.g., Library cannot adjoin Kitchen
};
```

### 🤖 Enemy AI System
The stalker enemy uses Behavior Trees and Unreal's EQS (Environment Query System) to patrol, detect, chase, and investigate — with a 180° FOV sight cone and dynamic hearing radius that reacts to player noise.

```mermaid
graph TD
  A[Patrol] --> B{Detect Player?}
  B -->|Yes| C[Chase]
  B -->|No| A
  C --> D{Line of Sight?}
  D -->|Yes| C
  D -->|No| E[Investigate] --> A
```

### 🔧 Crafting System
A data-driven crafting system lets players combine scavenged resources into tools that directly counter the manor's threats.

| Tool | Recipe | Effect |
|---|---|---|
| Flashlight | Battery + Metal Scrap | Illuminates dark areas; briefly stuns the enemy |
| Grappling Hook | Rope + Rusty Gear | Accesses elevated platforms and shortcuts |

### 🔊 Dynamic Audio
Integrated with Logic Pro X and FMOD Studio — audio layers intensify as the enemy closes distance, with a procedural heartbeat SFX system that responds to proximity in real-time.

### 🎨 Lumen-Powered Visuals
Leverage UE5's Lumen global illumination and Nanite geometry streaming for dense, high-detail environments with flickering horror lighting — without performance penalties on target hardware.

---

## 🏗️ Technical Architecture

### Modular Plugin System
Systems are decoupled into Game Feature plugins following Unreal's Modular Gameplay pattern, allowing isolated development, testing, and toggling of individual features.

```
/Plugins/GameFeatures/
    /GrapplingSystem/
        /Content/Animations/, /Blueprints/
        GrapplingSystem.uplugin
    /PuzzleSystem/
        /Content/Blueprints/, /Materials/
        PuzzleSystem.uplugin
```

### Asset Naming Conventions

| Prefix | Type | Example |
|---|---|---|
| `BP_` | Blueprints | `BP_Flashlight` |
| `M_` | Materials | `M_WallMaterial` |
| `SM_` | Static Meshes | `SM_Table` |
| `SK_` | Skeletal Meshes | `SK_Hero` |
| `T_` | Textures | `T_Wallpaper` |
| `WBP_` | Widget Blueprints | `WBP_HealthBar` |
| `DA_` | Data Assets | `DA_EnemyStats` |

### Project File Structure

```
/Content/
    /HollowManor/
        /Characters/
        /Environments/
        /Core/           ← Essential game systems
        /Interactables/
        /FX/
        /UI/
        /Audio/
        /Maps/
    /MaterialLibrary/    ← Shared materials & textures
    /Plugins/            ← Project plugins
```

---

## 🎮 Controls

<div align="center">

![Controller Scheme 1](https://app.milanote.com/media/p/images/1U1LBm1cKnEkdU/O95/image.png?w=800)

![Controller Scheme 2](https://app.milanote.com/media/p/images/1U1LC91cKnEkdV/UH8/image.png?w=800)

</div>

Full input remapping is supported for both Xbox and PlayStation controllers via Unreal's `EnhancedInputSystem`.

---

## ♿ Accessibility

- Full controller remapping via `EnhancedInputSystem`
- Multi-language support via Unreal's `Localization Dashboard`
- Subtitle support for all voiced/audio cues
- Adjustable audio mixing for SFX, music, and voice independently

---

## 🚀 Getting Started (Source)

> **Note:** This repo contains the Unreal Engine 5.3.2 source project files. To play the released game, please visit the Steam page.

**Prerequisites:**
- Unreal Engine 5.3.2
- Windows 10/11
- Git LFS enabled (`git lfs install`)

**Clone the repo:**
```bash
git clone https://github.com/Raiju-Deeq/Project-Haunting.git
cd Project-Haunting
```

**Open the project:**
1. Right-click `Project_Haunting.uproject`
2. Select *Generate Visual Studio project files*
3. Open the solution and build
4. Launch via `Project_Haunting.uproject`

---

## 📋 Technical Design Document

<details>
<summary><strong>Click to expand full TDD</strong></summary>

### TDD Overview
- **Version**: 0.5 | **Last Updated**: April 8, 2025
- **Technical Focus**: Procedural Generation, AI & Shaders
- **Design Focus**: Gameplay & Level Design

### AI & Logic Implementation
- Perception radii visualised with `DebugDraw` during development
- NavMesh pathing via console command `Show NavMesh`
- Lost Player Edge Case: AI uses EQS to search last known location for 30s before resuming patrol

### Performance Optimisation
- Level streaming via `World Partition` to manage memory footprint
- `content-visibility` culling for off-screen actors

### Quality Assurance — Playtesting Phases
1. **Pre-Alpha**: Core movement & AI detection
2. **Beta**: Full procedural generation with QA pass
3. **Release Candidate**: Full polish + platform certification

### Risk Mitigation

| Risk | Mitigation |
|---|---|
| Procedural generation lag | Precomputed room graph + async streaming |
| AI pathfinding failures | Manual `NavModifier` zones + bi-weekly EQS audits |
| Crafting exploits | Unit tests validate recipe inputs nightly |

### SCRUM Workflow
- **Sprint 1 (Apr 7–20)**: Prototype procedural room generation & Enemy AI
- **Sprint 4 (May 5–12)**: QA polish for Closed Beta

```
main                        // Stable builds only
├── feature/ai-pathfinding  // Feature branches
├── feature/crafting-system
└── release/v1.0            // Release candidates
```

</details>

---

## 🔗 Links

- 🎮 **[Play on Steam](https://store.steampowered.com)** — *Haunting Invitation*
- 📋 **[SCRUM Board](https://alexa03.atlassian.net/jira/software/projects/SCRUM/boards/1)** — Jira
- 🏫 **[De Montfort University](https://www.dmu.ac.uk/home.aspx)**

---

## 📚 References

- [Game Features & Modular Gameplay — Unreal Engine Docs](https://dev.epicgames.com/documentation/en-us/unreal-engine/game-features-and-modular-gameplay-in-unreal-engine)
- [Data-Driven Gameplay Elements — Unreal Engine Docs](https://dev.epicgames.com/documentation/en-us/unreal-engine/data-driven-gameplay-elements-in-unreal-engine)
- [Data Registries in Unreal Engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/data-registries-in-unreal-engine)
- [Modular Game Features in UE5 — Epic Games Blog](https://www.unrealengine.com/en-US/blog/modular-game-features-in-ue5-plug-n-play-the-unreal-way)
- [Component Pattern — Game Programming Patterns](https://gameprogrammingpatterns.com/component.html)

---

<div align="center">

*Developed by BSc Games Production students at De Montfort University, Leicester, UK.*

**🏆 Best Group Project — DMU End of Year Show**

</div>
