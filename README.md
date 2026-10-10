# Lab 4 — Vibe Coding: Galaga Game Enhancements

## 1. Project Overview

This project enhances the **Galaga** arcade-lite game developed using Python and Pygame. The game features Bézier-curve motion, wave-based enemy spawning, formation swaying, diving attack patterns, player shooting, lives, scoring, and projectile collisions.

The objective of this lab was to use an LLM (Gemini / Antigravity) as a pair-programming partner to diagnose and repair an intentional trajectory bug and implement three new gameplay features across iterative Git commits.

---

## 2. Student Details

- **Student Name:** ROOPESH
- **SRN:** PES1UG24AM393
- **Serial Number:** 31
- **Section:** 5-G
- **Assigned Repository:** `https://github.com/SETAPESU26/31_galaga`
- **GitHub Repository:** [https://github.com/roopeshp057-a11y/galaga-game](https://github.com/roopeshp057-a11y/galaga-game)

---

## 3. Implemented Features

### Task 1 — Fix Entry & Dive Bézier Curve Path Bug
- **Analysis:** Cubic Bézier curves follow the standard equation:
  $$B(t) = (1-t)^3 P_0 + 3(1-t)^2 t P_1 + 3(1-t) t^2 P_2 + t^3 P_3$$
- **Bug Identified:** In the original `bezier()` function, the third weighted term was written as `3 * u * t * p2` instead of `3 * u * t * t * p2`, missing the squared exponent on parameter $t$. This caused enemies to noticeably overshoot and bulge awkwardly mid-flight during entry.
- **Fix Applied:** Squared parameter $t$ in the third term (`3 * u * t * t * p2[0]` and `3 * u * t * t * p2[1]`). Enemies now follow smooth, continuous curved trajectories into formation.
- **Commit:** `Fix cubic Bézier curve calculation bug in bezier() (Task 1)`

### Task 2 — Custom Enemy Tinting (`enemy_tint`)
- **Objective:** Provide visual distinction for different enemy types (`"boss"`, `"red"`, `"blue"`).
- **Implementation:** Implemented `enemy_tint(kind)` returning vibrant arcade neon palettes:
  - **Boss:** Neon Emerald `(60, 240, 160)`
  - **Red:** Vibrant Arcade Crimson `(255, 75, 95)`
  - **Blue:** Electric Azure Cyan `(75, 175, 255)`
- **Commit:** `Implement enemy_tint() for custom enemy coloration (Task 2)`

### Task 3 — Wave Start Banner Announcement (`on_wave_start`)
- **Objective:** Trigger wave announcements and stage transitions when a wave begins.
- **Implementation:** Added an animated stage announcement banner (`STAGE {wave} - GET READY`) rendered centered on screen for 2.0 seconds at the beginning of each wave.
- **Commit:** `Implement on_wave_start() with wave banner display (Task 3)`

### Task 4 — Player Shield Charges & Visual HUD (`shield_charges`)
- **Objective:** Grant hit-absorbing energy shields at wave start and render an active shield indicator.
- **Implementation:** Granted `1 + (wave - 1) // 3` hit absorption charges per wave. Rendered a glowing cyan energy shield circle around the player ship when active, and added a real-time `Shield` counter to the game HUD.
- **Commit:** `Implement shield_charges() with visual shield indicator (Task 4)`

---

## 4. Technologies Used

- **Programming Language:** Python 3.13
- **Game Library:** Pygame 2.6.1
- **Development Environment:** Visual Studio Code / Antigravity IDE
- **Version Control:** Git and GitHub
- **LLM Assistance:** Google Antigravity (Gemini)

---

## 5. Repository Structure

```text
galaga-game/
├── game.py                        # Complete, fixed and enhanced Galaga game
├── README.md                      # Project documentation and lab report
├── before_edit.mp4                # 10s gameplay recording BEFORE fixes (showing bug)
├── FINAL.mp4                      # 10s gameplay recording AFTER fixes (showing all features)
├── Galaga_Repair_Enhancements.pdf # Comprehensive submission PDF report
├── Lab-4/                         # Lab-4 packaged deliverables
│   ├── game.py
│   ├── README.md
│   ├── before_edit.mp4
│   ├── FINAL.mp4
│   ├── Galaga_Repair_Enhancements.pdf
│   ├── CHAT_HISTORY.md
│   └── CHAT_HISTORY.html
└── .gitignore
```

---

## 6. Running the Game

### Setup
```bash
pip install pygame
```

### Run
```bash
python game.py
```

### Controls

| Key | Action |
|---|---|
| Left Arrow / Right Arrow | Move ship left / right |
| Spacebar | Fire projectiles |
| R | Restart / Reset game |

---

## 7. Testing and Verification

- [x] Enemies enter along smooth Bézier curves without bulging or overshooting.
- [x] Enemies settle into a swaying formation and periodically dive while firing.
- [x] Boss and basic enemies display distinct custom colors.
- [x] Wave banner appears centered for 2 seconds at the start of each wave.
- [x] Player shield absorbs hits before ships are destroyed, showing cyan shield circle.
- [x] Pressing `R` resets the game state properly.

---

## 8. Gameplay Demonstrations

- **Before modifications:** [before_edit.mp4](./before_edit.mp4) (10 seconds showing Bézier trajectory overshoot)
- **After modifications:** [FINAL.mp4](./FINAL.mp4) (10 seconds demonstrating fixed curves, enemy tints, wave banner, and shield)

---

## 9. LLM Chat History & Report

The complete conversation documenting the AI-assisted pair-programming process is available in the PDF report:

📄 **[View Complete Report (PDF)](./Galaga_Repair_Enhancements.pdf)**
