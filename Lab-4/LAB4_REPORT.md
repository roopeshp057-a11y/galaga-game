# Lab 4: Vibe Coding - Galaga Repair Lab Report

**Student Details:**
- **Name:** ROOPESH
- **SRN:** PES1UG24AM393
- **Serial Number:** 31
- **Assigned Repository:** `https://github.com/SETAPESU26/31_galaga`
- **Personal Repository:** `https://github.com/roopeshp057-a11y/galaga-game`

---

## 1. Task Breakdown & Solutions

### Task 1: Fix the Entry/Dive Bézier Path Bug
- **Bug Identified:** In the cubic Bézier function `bezier(p0, p1, p2, p3, t)`, the 3rd term ($3(1-t)t^2 P_2$) was missing the squared exponent on `t` (`3 * u * t * p2` instead of `3 * u * t * t * p2`). This caused enemies to bulge and overshoot awkwardly during entry.
- **Fix Applied:**
  ```python
  def bezier(p0, p1, p2, p3, t):
      u = 1 - t
      x = u ** 3 * p0[0] + 3 * u * u * t * p1[0] + 3 * u * t * t * p2[0] + t ** 3 * p3[0]
      y = u ** 3 * p0[1] + 3 * u * u * t * p1[1] + 3 * u * t * t * p2[1] + t ** 3 * p3[1]
      return pygame.Vector2(x, y)
  ```
- **Commit:** `Fix cubic Bézier curve calculation bug in bezier() (Task 1)`

---

### Task 2: Implement `enemy_tint(kind)`
- **Objective:** Provide visual distinction for different enemy kinds (`"boss"`, `"red"`, `"blue"`).
- **Implementation:**
  ```python
  def enemy_tint(kind):
      """Return an (r, g, b) colour override for an enemy kind, or None for the default."""
      tints = {
          "boss": (60, 240, 160),    # Vibrant emerald neon
          "red": (255, 75, 95),      # Bright arcade crimson
          "blue": (75, 175, 255),    # Electric azure cyan
      }
      return tints.get(kind)
  ```
- **Commit:** `Implement enemy_tint() for custom enemy coloration (Task 2)`

---

### Task 3: Implement `on_wave_start(wave)`
- **Objective:** Trigger wave announcements and stage transitions when a wave begins.
- **Implementation:**
  ```python
  WAVE_BANNER = {"text": "", "timer": 0.0}

  def on_wave_start(wave):
      """Called at the start of every wave; add banners, speed-ups, or palette swaps here."""
      WAVE_BANNER["text"] = f"STAGE {wave} - GET READY"
      WAVE_BANNER["timer"] = 2.0
  ```
- **Commit:** `Implement on_wave_start() with wave banner display (Task 3)`

---

### Task 4: Implement `shield_charges(wave)`
- **Objective:** Grant absorbing shield charges at wave start and render an energy shield indicator.
- **Implementation:**
  ```python
  def shield_charges(wave):
      """Return how many hits the player's shield can absorb this wave, or None to disable the shield."""
      return 1 + (wave - 1) // 3
  ```
  - Added cyan glowing shield circle around player ship when `self.shield > 0`.
  - Added shield charge indicator to the HUD: `Score ... Lives ... Shield ... Wave ...`
- **Commit:** `Implement shield_charges() with visual shield indicator (Task 4)`

---

## 2. Deliverables Checklist
- [x] **Video Before Fix:** `video_before_fix.mp4` (10 seconds showing Bézier overshoot bug)
- [x] **Video After Fix:** `video_after_fix.mp4` (10 seconds showing smooth curves, tints, stage banner, shield)
- [x] **Updated Code:** `game.py` with all 4 tasks implemented
- [x] **Separate Commits:** 4 individual git commits pushed to `https://github.com/roopeshp057-a11y/galaga-game`
- [x] **Chat History:** Exported chat session
