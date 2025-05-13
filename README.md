# CloudSyncPuzzleQuest-DesignPlan

# Cloud Sync Puzzle Quest - App Design & AI Plan

## Thesis Context

This project outlines the design specification and AI-assisted implementation plan for "Cloud Sync Puzzle Quest". This mobile game serves as a practical demonstration for the thesis titled: **"Developing a mobile game with cloud integration for user data synchronization."** The primary focus of the application's technical design is the robust implementation of cloud-based data persistence and real-time synchronization.

## Project Summary

Cloud Sync Puzzle Quest is a casual mobile puzzle game (e.g., spatial logic puzzles) available for iOS and Android. While offering engaging gameplay through level progression and collectible rewards, its core technical purpose is to showcase a reliable and seamless cloud synchronization system. The app ensures that player progress—including completed levels, scores, stars earned, unlocked collectibles, and settings—is consistently saved to the cloud and synchronized across all devices linked to their account in near real-time.

## Chosen Tech Stack

The proposed technology stack for implementing this application is:

* **Platform:** Mobile (iOS & Android)
* **Framework:** Unity (using c# language)
* **State Management:** Bloc / Unity_bloc
* **Backend & Sync:** Firebase
    * **Authentication:** Firebase Authentication (for user identity)
    * **Database:** Firebase Firestore (for real-time data storage and synchronization)
* **AI Code Assistance:** GitHub Copilot / Cursor (planned for accelerating development)
* **Prototyping (Optional):** Figma / AI Wireframing Tools (e.g., Uizard, Visily)

## Key Features

* Core puzzle gameplay loop (specific mechanics TBD, e.g., spatial logic)
* Level progression system with unlock conditions and star ratings (1-3 stars)
* Simple collectible system tied to achievements or level completion
* **Real-time Cloud Synchronization:** Automatic background sync of all relevant user data (level progress, collectibles, settings, scores) using Firebase Firestore.
* **Multi-Device Persistence:** Seamless continuation of gameplay across different user devices.
* User Account Management via Firebase Authentication.

## Deliverables (Task 2)

This repository contains the following documents detailing the app design and plan:

* **[Concept Brief](./Concept_Brief.md)**: Detailed description of the app idea, target audience, and goals.
* **[Architecture Plan](./Architecture_Plan.md)**: Includes:
    * Screen Map and Navigation Flow (Diagram/Description)
    * Data Structure Definitions (Models and Fields)
* **[Complexity Estimation](./Complexity_Estimation.md)**: Table outlining estimated complexity, AI-promptability, tech needed, and potential blockers for core MVP features.
* **[AI Code Generation Prompts](./AI_Prompts.md)**: Specific prompts designed for AI code assistants (Copilot/Cursor) for key implementation tasks.
* **(Optional) [Figma Prototype](./figma/)**: [Link to Figma File Here - if applicable] or screenshots located in the `/figma` directory.

## Cloud Sync Strategy Overview

The synchronization strategy is central to this project and leverages Firebase Firestore's real-time capabilities:

* **Data Storage:** User-specific data (`UserData`, including nested `levelProgress` and `unlockedCollectibles` maps) will be stored in a Firestore document keyed by the authenticated `userId`. Static game data (like `Collectible` definitions) may reside in a separate collection or be bundled.
* **Real-time Updates:** The app will utilize Firestore real-time listeners (`.snapshots()`) to subscribe to changes in the user's data document. This ensures the UI automatically reflects the most current state pushed from the cloud or other devices.
* **Saving Progress:** Updates to user progress (e.g., after completing a level) will be written to Firestore. These writes will update specific fields, including arrays/maps for collectibles/level progress, and crucially update a `lastSyncTimestamp` field on the main user document.
* **Conflict Resolution (MVP):** The initial approach for handling potential data conflicts (e.g., simultaneous writes) will likely be a simple 'last write wins' strategy, implicitly handled by using the `lastSyncTimestamp` or Firestore's default behavior. More complex strategies are outside the MVP scope but acknowledged.
* **Offline Handling (Basic):** Basic offline support will rely on Firestore's built-in caching. For the MVP, operations performed offline might be queued and automatically synced upon reconnection. A robust offline strategy (e.g., manual caching, conflict resolution upon reconnect) is a potential future enhancement beyond the core thesis demonstration.

---
