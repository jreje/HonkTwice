# Honk Twice

A VR matching game for Meta Quest where you identify matching cars by **how they look and how they sound** in order to safely cross the street.

**Team:** Grace, Lucy, Lauren, Julianne
**Course:** COMP 590 (Final Project)

> Demo video: _TODO: add link_

---

## Concept

The player stands at the curb facing a row of cars. Select a car and it lights up and honks, so you can compare its look and sound with the others. Find all of the matching pairs within **3 attempts** to cross the street to the next level. Fail, and you start the level over.

The goal is to convey the attention required to safely cross a busy street. Presence is driven mostly by **spatial audio**: if you close your eyes, you should feel like you're standing next to a road.

## How to Play

- **Look around** by turning your head to scan the row of cars.
- **Select a car** by pointing at it and pressing the trigger. It glows and honks.
- **Pick a second car.**
  - Match: both cars lock with a green glow.
  - Mismatch: both flip back and you lose an attempt.
- **Attempts** are shown by three traffic lights.
- Match every pair before you run out of attempts to win the level.

## Tech Stack

| Item | Version |
| --- | --- |
| Unity | 6000.3.26f1 |
| Render pipeline | Universal Render Pipeline (URP) 17.3.0 |
| XR | OpenXR 1.19.0 + Meta XR All-in-One SDK 209.0.0 |
| Audio | Meta XR Audio (spatializer) |
| Target device | Meta Quest 2 / 3 / 3S / Pro |

## Running the Project

### In the Unity editor
1. Install **Unity 6000.3.26f1** (with **Android Build Support**, including OpenJDK and Android SDK & NDK Tools) via Unity Hub.
2. Clone the repo (see Git setup below) and open the folder in Unity Hub.
3. Open `Assets/Scenes/Level1.unity`.
4. Press Play. With a Quest in Link mode (Windows) the game runs in the headset, or use the **Meta XR Simulator**.

### On a Quest
1. Enable Developer Mode on your headset (Meta Horizon app, Devices, Headset Settings, Developer Mode).
2. In Unity, open **File > Build Profiles**, select **Meta Quest**, and make sure it is the active platform.
3. Connect the Quest via USB and approve the USB debugging prompt.
4. Choose **Build and Run**. The first build can take 15 minutes or more.
5. To relaunch later, find the app under **Unknown Sources** in your Quest library.

## Git Setup

This repo uses **Git LFS** for large assets (models, audio, textures, etc.) and **UnityYAMLMerge** for scenes and prefabs.

```bash
git lfs install
git clone <repo-url>
```

Each person needs to configure the merge tool locally, since it is stored in git config rather than the repo. Add this to your `.git/config` (adjust the path to your Unity install):

```ini
[merge]
    tool = unityyamlmerge

[mergetool "unityyamlmerge"]
    trustExitCode = false
    cmd = '<path to UnityYAMLMerge>' merge -p "$BASE" "$REMOTE" "$LOCAL" "$MERGED"
```
Find your path to UnityYAMLMerge here: https://docs.unity3d.com/6000.2/Documentation/Manual/SmartMerge.html 

## Project Structure

```
Assets/
  Scenes/        Level1.unity (main scene)
  Settings/      URP assets and the Meta Quest build profile
  XR/            OpenXR / XR Management settings
  Plugins/       Android manifest
  Resources/     Meta XR runtime settings
Packages/        manifest.json (Meta XR SDK, OpenXR, URP, etc.)
ProjectSettings/
```

**Bare minimum:** a grid of cards that flip on interaction and play sounds, with a working game loop where matched pairs lock and mismatches reduce attempts.

**Contingency plans**
- Spatial audio doesn't work: fall back to stereo sounds.
- Outer environment too hard: use a simple backdrop.
- Multiple levels too large in scope: ship one level.

## Known Issues / Notes

- _TODO: add as you find them._

## Credits and Outside Resources

- Meta XR SDK, Unity OpenXR, Unity URP
- _TODO: list all third-party assets, sounds, and tutorials with links and licenses._
