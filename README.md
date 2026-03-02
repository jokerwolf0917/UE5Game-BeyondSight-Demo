# UE5 Portfolio Project: Blind Protagonist & Guide Dog System

**👉 [Click Here to Watch the Technical & Gameplay Demo on YouTube](https://youtu.be/8wcCgXnQruQ)**
## 📖 Project Overview
This project is a third-person narrative game prototype developed in **Unreal Engine 5**. It features a unique non-photorealistic rendering style to simulate the experience of a blind protagonist and implements a robust dual-character control system (Human & Guide Dog).

The project focuses on modular architecture, clean Blueprint logic, and technical art implementation.

---

## 🎨 1. Tech Art: "Blind Vision" Post-Process Shader
To simulate the protagonist's echolocation and limited vision, I developed a custom Post-Process Material using HLSL logic within the Material Editor.

**Key Technical Features:**
* **Sobel Edge Detection:** Utilizes `SceneTexture:CustomDepth` to draw outlines around objects, simulating the "mental map" of the blind character.
* **Spherical Masking:** Implements a distance-based visibility system where objects fade into existence only when near the player or making sound.
* **Material Functions:** Complex logic (like the Sobel kernel) is encapsulated into reusable Material Functions (`MF_Sobel_Depth`) for maintainability.

### Visual Result
![Blind Vision Shader Effect](/image/demo.png)

### Shader Logic Graph
![Shader Graph Logic](/image/M_BlindVision_PPA.png)

> 🔗 **Interactive Graph:** [View Shader Logic on BlueprintUE](https://blueprintue.com/blueprint/urwz84vf/)

---

## 🎮 2. System Architecture: Dual Character Controller
A core mechanic of the game is the ability to switch control between the Blind Protagonist and the Guide Dog. I refactored the legacy logic into a clean, event-driven architecture hosted within the `BP_PlayerController`.

**Key Technical Features:**
* **Decoupled Logic:** Input handling and Pawn possession logic are separated from the character Blueprints, allowing for modularity.
* **Enhanced Input Integration:** Utilized `Add Mapping Context` to dynamically swap input schemes when switching characters.
* **Lifecycle Management:** Proper initialization in `BeginPlay` ensures secure reference handling and prevents race conditions during startup.

### Controller Logic (Initialization & Switching)
![Player Controller Architecture](/image/BP_PlayerController.png)

> 🔗 **Interactive Graph:** [View Controller Logic on BlueprintUE](https://blueprintue.com/blueprint/v499qxtb/)

---

## 🐕 3. Gameplay Mechanics: Guide Dog QTE System
The Guide Dog character features a "Temptation System" where it can be distracted by environmental stimuli (e.g., food smells). The player must perform a Quick Time Event (QTE) to refocus the dog.

**Key Technical Features:**
* **Context-Aware Interaction:** The input system (`E` Key) uses a "Gatekeeper" Branch logic to intelligently determine context:
    * **If Tempted:** Triggers the Resistance QTE mechanics.
    * **If Normal:** Scans for surrounding interactive items using `GetOverlappingActors`.
* **State Machine Logic:** The QTE loop is managed via a clean `Event Tick` flow that handles progress calculation, win/loss states, and UI updates.

### Core QTE Loop & State Management
![QTE State Machine Logic](/image/BP_GuideDogCharacter1.png)

### Context-Aware Input System
![Input Flow Logic](/image/BP_GuideDogCharacter2.png)

> 🔗 **Interactive Graph:** [View Guide Dog Logic on BlueprintUE](https://blueprintue.com/blueprint/edno9fvb/)

---

## 🔗 4. Interaction System & Interfaces
To ensure scalability, all interactive objects (Doors, Story Items, NPCs) implement a **Blueprint Interface (`BPI_StoryInteraction`)**.

* **Decoupling:** The character does not need to Cast to specific object classes. It simply sends an Interface Message, and the object responds accordingly.
* **Story Triggers:** A dedicated `BP_StoryTrigger` handles narrative events, managing UI prompts and index-based dialogue progression.

### Generic Story Trigger Logic
![Story Trigger Logic](/image/BP_StoryTrigger.png)

> 🔗 **Interactive Graph:** [View Trigger Logic on BlueprintUE](https://blueprintue.com/blueprint/4zxtyby3/)

---

## 🛠 Tools & Technologies
* **Engine:** Unreal Engine 5.4
* **Language:** Blueprints (Visual Scripting), HLSL (Custom Nodes in Materials)
* **Version Control:** Git
* **IDE:** Rider / Visual Studio

---

### 📬 Contact
* **Name:** Alyx Wang
* **Email:** jokerwolf0917@gmail.com
