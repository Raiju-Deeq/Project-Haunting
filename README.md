# Project Haunting

## Unreal Engine Project Files
The project files for our game.
Developed with Unreal Engine 5.3.2

---

# Table Of Contents
1. [**About Us**](#about-us)
2. **Project Haunting TDD**  
3. **Project Haunting GDD**
4. **Supported Platforms**
5. **Future Plans**  


## About Us
We are second year university students who have been working on creating our own launch ready video game.
This repo will contain the unreal engine project files as well as the completed build.
Will update this section closer to completion of the game.

## Project Haunting Updated TDD

**Technical Design Document (TDD) for *Project Haunting of Hollow Manor***  
*Version 0.3 | Last Updated: April 5, 2025*  
**Technical Focus**: Procedural Generation, Artificial Intelligence & Shaders  
**Design Focus**: Gameplay & Level Design  

---

## **Table of Contents**
1. **Title Page**  
2. **Features**  
3. **Game Engine Justification**  
4. **Technical Details**  
   - 4.1 Procedural Room Generation  
   - 4.2 Enemy AI System + Crafting & Tools  
   - 4.3 Technical Architecture  
1. **AI & Logic Implementation**  
2. **Programming & Procedural Systems**  
3. **Audio & Visuals**  
4. **Accessibility & Localization**  
5. **Risk Mitigation**  
6. **Quality Assurance**  
7. **Hardware Requirements**  
8. **Project Management**  
9. **Asset Pipeline**  
10. **Appendix**
11. **References**

---

### **1. Title Page**  
- **Target Audience**: Teens/Young Adults (ESRB Rating: Teen)  
- **Engine**: Unreal Engine 5.3.2  
- **GitHub**: [Project Haunting Repository](https://github.com/Raiju-Deeq/Project-Haunting)  
- **Jira**: [SCRUM Board](https://alexa03.atlassian.net/jira/software/projects/SCRUM/boards/1)  
- **Team Roles**:  
  - *Scrum Master*: Dahna Aldrighetti  
  - *Product Owner*: Mohamed Deeq Mohamed  
  - *Tech Developers*: Mohamed Deeq Mohamed & Benjamin 

---

### **2. Features**  
| Feature                    | Implementation Method           | Tools/Technologies Used           |     |
| -------------------------- | ------------------------------- | --------------------------------- | --- |
| Procedural Room Generation | Modular Rooms + DataTables      | Unreal Engine Blueprint           |     |
| Enemy AI                   | Behavior Trees + EQS Perception | AIPerceptionComponent             |     |
| Crafting System            | Data-driven recipes             | DataAssets, GameplayAbilitySystem |     |

---

### **3. Game Engine Justification**  
**Unreal Engine 5.3.2 Advantages**:  
- **Nanite/Lumen**: Enables dynamic horror lighting (e.g., flickering shadows) and high-detail environments without performance loss  
- **Modular Gameplay Plugins**: Isolate AI and procedural systems for scalable development
- **Unity Comparison**: Lacks native support for Lumen’s real-time global illumination and Nanite’s geometry streaming

---

### **4. Technical Details**  
#### **4.1 Procedural Room Generation**  
- **Controlled PCG Workflow**: Modular rooms prebuilt with layout assets etc. Then fed into procedural generator to spawn them. (See Appendix z for details)
  - **Fallback System**: Manual level overrides if generation fails QA checks as rooms are modular and prebuild. Designer can place rooms manually.

```cpp  
// DataTable Entry for Room Compatibility  
USTRUCT(BlueprintType)  
struct FRoomData : public FTableRowBase {  
    GENERATED_BODY()  
    UPROPERTY(EditAnywhere)  
    FName RoomID;  
    UPROPERTY(EditAnywhere)  
    TArray CompatibleRooms;  // e.g., Library cannot adjoin Kitchen  
};  
```

#### **4.2 Enemy AI System**  
- **Behavior Tree Structure**:  
  ```mermaid  
  graph TD  
    A[Patrol] --> B{Detect Player?}  
    B -->|Yes| C[Chase]  
    B -->|No| A  
    C --> D{Line of Sight?}  
    D -->|Yes| C  
    D -->|No| E[Investigate] --> A  
  ```
- **Perception Parameters**:  
  - *Sight*: 180° FOV, 5m range.  
  - *Hearing*: Noise detection for footsteps/object interactions


**Crafting & Tools**

| Tool           | Recipe                | Effect                                                                   |     |
| -------------- | --------------------- | ------------------------------------------------------------------------ | --- |
| Flashlight     | Battery + Metal Scrap | Brightens area and also allows the player to stun the enemy temporarily. |     |
| Grappling Hook | Rope + Rusty Gear     | Accesses vertical platforms                                              |     |

#### **4.3 Technical Architecture
**Modular Design Philosophy**
We will implement a modular plugin based architecture that separates functionality into discrete, decoupled systems. (See Appendix x for details)

**File Structure**
Alongside the modular design, we'll implement a clear folder structure following Unreal Engine best practices
(See Appendix y for details)

---

### **5. AI & Logic Implementation**  
- **Debugging Tools**:  
  - Visualize perception radii with `DebugDraw` 
  - NavMesh pathing visualization via console command `Show NavMesh`.  
- **Edge Cases**:  
  - *Lost Player*: AI uses EQS to search last known location for 30s before resuming patrol

---

### **6. Programming & Procedural Systems**  
- **Room Assembly Algorithm**: Basic procedural generator that I previously used in an older project. Will remake it.
- **Performance Optimization**:  
  - Stream levels via `World Partition` to manage memory. Research needed

---

### **7. Audio & Visuals**  
- **Logic Pro X/FMOD Studio Integration**:  
  - Dynamic audio layers intensify when enemy is within 3m (e.g., heartbeat SFX)
- **Post-Processing**:  
  - Vignette effect applied via material parameter collection when enemy is nearby
  - Post-Process shader will be used

---

### **8. Accessibility & Localization**  
- **Input Remapping**: Supports Xbox/PS controllers via `EnhancedInputSystem` (See Figure W for more details)
- **Localization**:  
  - Multiple languages managed through Unreal’s `Localization Dashboard` 
  - Example:  
    ```cpp  
    // Localized Interaction Prompt  
    UPROPERTY(EditDefaultsOnly, Category="UI")  
    FText InteractionPrompt;  // Uses FText for automatic translation  
    ```

---

### **9. Risk Mitigation**  
| Risk                      | Mitigation Strategy                               |     |
| ------------------------- | ------------------------------------------------- | --- |
| Procedural generation lag |                                                   |     |
| AI pathfinding failures   | Manual `NavModifier` zones + bi-weekly EQS audits |     |
| Crafting exploits         | Unit tests validate recipe inputs nightly         |     |

---

### **10. Quality Assurance**  
- **Automated Testing**: **Research needed**
  ```bash  
  # Gauntlet test for enemy detection  
  RunUnreal.exe HollowManor -Test=EnemyPerception  
  ```
- **Playtesting Phases**:  
  1. **Pre-Alpha (May 15)**: Core movement/combat.  
  2. **Beta (June 1)**: Full procedural generation.  

---

### **11. Hardware Requirements**  
| Component | Minimum | Recommended |     |
| --------- | ------- | ----------- | --- |
| GPU       | Unknown | Unknown     |     |
| RAM       | Unknown | Unknown     |     |
| Storage   | Unknown | Unknown     |     |

---

### **12. Project Management**  
- **Tech Team SCRUM Workflow**:  
  - **Sprint 1 (Apr 7-20)**: Prototype procedural room generation & Enemy AI.  
  - **Sprint 4 (May 5-12)**: QA polish for Closed Beta.  
- **GitHub Strategy**:  
  ```  
  main           // Main development
  ├── feature/ai-pathfinding // Branches used for bugs
  └── release/v0.4 // Branches used for experimental & test 
  //Merge back to main when testing is over
  ```

---

### **13. Asset Pipeline**  
- **Naming Conventions**:  
We'll use a prefix-based naming system for all assets:
- **BP_**: Blueprints e.g. `BP_Flashlight` 
- **M_**: Materials e.g. `M_WallMaterial`
- **SM_**: Static Meshes e.g. `SM_Table`
- **SK_**: Skeletal Meshes e.g. `SK_Hero`
- **T_**: Textures e.g. `T_Wallpaper`
- **P_**: Particle Systems e.g. `P_Fire`
- **WBP_**: Widget Blueprints e.g. `WBP_HealthBar`
- **DA_**: Data Assets e.g. `DA_`


---

### 14. Appendix

Figure x 
### Modular Design Philosophy
Following the modern best practices for Unreal Engine projects, we will implement a modular architecture that separates functionality into discrete, decoupled systems. This approach offers several benefits:

- Easier maintenance and updates to specific features without affecting others
- Clear boundaries between systems to minimize unintended side effects
- Ability to enable/disable features during development and testing
- Better collaboration between team members working on different features

### Plugin-Based Architecture
We will utilize Unreal Engine's Game Features and Modular Gameplay plugins to implement key game systems. This architecture allows us to:

- Develop features in isolation with clear boundaries
- Add or remove content without modifying the core game
- Enable better testing and iteration of individual features
- Scale the project more efficiently as it grows

```
// Example Game Feature Plugin Structure
/Plugins/GameFeatures/
    /GrapplingSystem/
        /Content/
            /Animations/
            /Blueprints/
        /Source/
        GrapplingSystem.uplugin
    /PuzzleSystem/
        /Content/
            /Blueprints/
            /Materials/
        /Source/
        PuzzleSystem.uplugin
```

### Component-Based Design
Rather than relying on deep inheritance hierarchies, we'll implement a component-based approach for gameplay objects:

- **Character Components**: Movement abilities, health system, inventory
- **Interaction Components**: Grappling, object manipulation, stealth mechanics
- **AI Components**: Enemy behaviors, pathing, player detection
- **Environmental Components**: Interactive elements, puzzles, triggers

This pattern allows us to mix and match behaviors across different actor types while maintaining clean, focused code in each component.

### Data-Driven Systems
To separate game data from implementation code, we'll implement:

- **DataTables**: For enemy properties, puzzle configurations, collectible items
- **Data Assets**: For more complex game objects with nested properties
- **Data Registries**: For global data access and management
- **ScriptableObjects**: For designer-friendly content creation


Figure y
### File Structure 
```
/Content/Individual team member folder (e.g. Mo)
    /HollowManor/       // Project-specific content
        /Characters/
        /Environments/
        /Core/           // Essential game systems
        /Interactables/
        /FX/
        /UI/
        /Audio/
        /Maps/
    /MaterialLibrary/    // Shared materials and textures
    /Plugins/            // Project plugins
```


Figure Z
### Modular Room System
```
/Content/Mansion/
    /Modules/
        /Hallways/
        /Rooms/
            /Library/
            /ClockworkRoom/
            /DiningRoom/
    /Assemblies/
        /WestWing/
        /EastWing/
        /MainHall/
```

Figure W
![Image from Control Scheme 1](https://app.milanote.com/media/p/images/1U1LBm1cKnEkdU/O95/image.png?w=800)

![Image from Control Scheme 1](https://app.milanote.com/media/p/images/1U1LC91cKnEkdV/UH8/image.png?w=800)

---

### **15. References**  
 Unreal Engine Modular Gameplay Documentation
 Game Features and Modular Gameplay in Unreal Engine https://dev.epicgames.com/documentation/en-us/unreal-engine/game-features-and-modular-gameplay-in-unreal-engine
Techniques and Strategies for Data-driven design in Game ... https://web.eecs.umich.edu/~soar/Classes/494/talks/Schumaker.pdf
Modular Game Features in UE5: Plug 'n Play, the Unreal Way https://www.unrealengine.com/en-US/blog/modular-game-features-in-ue5-plug-n-play-the-unreal-way
9 Types of Game Design Documents: Insights from Alexey Savchenko https://kreonit.com/idea-generation-and-game-design/9-essential-types-of-game-design-documents-insights-from-alexey-savchenko/
Architecture - Game engine and data driven design https://gamedev.stackexchange.com/questions/17331/game-engine-and-data-driven-design
Component · Decoupling Patterns - Game Programming Patterns https://gameprogrammingpatterns.com/component.html
10 Tips for a Successful Unreal Project from Day One - YouTube https://www.youtube.com/watch?v=1gL7NSgQZys
Siitoo/Technical-Design-Document - GitHub https://github.com/Siitoo/Technical-Design-Document
Unreal Engine 5 Game Features Plugin - YouTube https://www.youtube.com/watch?v=IYbMDWZHqzg
Component-Based Design: Complete Implementation Guide - UXPin https://www.uxpin.com/studio/blog/component-based-design-complete-implementation-guide/
Why You Should Embrace the Component Design Pattern in Game ... https://unrealstack.com/why-you-should-embrace-the-component-design-pattern-in-game-development/
Good and best practices in UE... [Architecture] - Unreal Engine Forums https://forums.unrealengine.com/t/good-and-best-practices-in-ue-architecture/1642211
Unreal Engine Plugin Overview — Charon 2024.4.1 documentation https://gamedevware.github.io/charon/unreal_engine/overview.html
Data Registries in Unreal Engine - Epic Games Developers https://dev.epicgames.com/documentation/en-us/unreal-engine/data-registries-in-unreal-engine
Data Driven Gameplay Elements in Unreal Engine https://dev.epicgames.com/documentation/en-us/unreal-engine/data-driven-gameplay-elements-in-unreal-engine
Mastering Pipeline Game Development: Insights from WildSphere ... https://www.bravezebra.com/blog/mastering-pipeline-game-development-insights-from-wildsphere-ind

---


## Project Haunting GDD



## Supported Platforms



## Future Plans
