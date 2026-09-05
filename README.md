# Double Dragon II: The Revenge (Arcade) — Fixed Attack Controls

**Type:** Improvement / Hack
**Platform:** Arcade (Technōs, `ddragon2`)
**Patched files:** 2 of the 18 ROMs in `ddragon2.zip`
**Format:** BPS
**Hack:** Psicopompo

---

<img width="256" height="240" alt="ddragon2-260905-222916" src="https://github.com/user-attachments/assets/2802be20-d08f-442a-aea6-13f52ff32261" />


## Description

In the original *Double Dragon II* arcade board, the two attack buttons are
directional: one attacks **towards the left of the screen** and the other
**towards the right**, no matter which way your character is facing. In
practice that means one button is your punch and the other is your back
kick — and the two swap over every single time you turn around.

Facing right, button 1 is a back kick and button 3 is a punch. Turn to face
left and it is the other way round.

This was a deliberate design decision in 1988 and it works perfectly well
once it clicks. But it does mean the same button performs two different
moves depending on which way you happen to be facing, which fights the
muscle memory of anyone used to later beat 'em ups.

This hack rebuilds the input handling so that **each button is always the
same move, regardless of which way the character is facing**:

| Button | Move |
| --- | --- |
| Button 1 | Kick |
| Button 2 | Jump (unchanged) |
| Button 3 | Punch |

The change is applied consistently across every attack in the game, not just
the basic punch and kick — see the table below.

Nothing else is touched: graphics, text, enemy behaviour, damage values,
timing and level design are all exactly as in the original.

---

<img width="256" height="240" alt="ddragon2-260905-152417" src="https://github.com/user-attachments/assets/e30adf4e-7de4-42cb-8902-e9f6bbaba617" />

## What changes

| Situation | Button 1 | Button 3 |
| --- | --- | --- |
| On the ground | Kick | Punch |
| Jump + attack (pressed together) | Ground-level kick | Elbow smash |
| In the air (after jumping) | Flying kick | Cyclone kick, at the top of the jump only |
| Holding the knife | Kick | Throw the knife |
| Holding the whip | Spin attack | Normal swing |
| Holding a shovel, bat, oil drum… | Consistent on both sides | Consistent on both sides |
| Picking up a weapon | — | Punch button only |

Two further adjustments were needed to make the above behave sanely:

- **The input buffer window for simultaneous presses was widened from 3 to
  4 frames.** With the original 3-frame window, "jump + attack" was too easy
  to miss once the two attacks stopped being interchangeable.
- **The character no longer flips around in mid-air.** In the original, an
  aerial attack forces the sprite to face the direction the button attacks
  towards. Since the buttons are no longer directional, that forced flip no
  longer made sense and was removed.

Also worth knowing: **the cyclone kick still cannot be performed while
carrying a weapon.** That is original behaviour, not a side effect of this
hack — the stock ROM discards it the same way.

---

## Installation

The arcade game is not a single ROM: it is 18 files inside `ddragon2.zip`.
This hack modifies **two** of them, so there are two patches:

| Patch | Target file | Bytes changed |
| --- | --- | --- |
| `26a9-04.bin.bps` | `26a9-04.bin` (main CPU) | 233 |
| `26ac-0e.63.bps` | `26ac-0e.63` (banked ROM) | 4 |

1. Open `ddragon2.zip` and extract `26a9-04.bin` and `26ac-0e.63`.
2. Apply each `.bps` to its matching file with Flips, beat, or any BPS tool.
3. Put both patched files back into the zip, replacing the originals.
4. Leave the other 16 files untouched.

**Checksums**

```
                original MD5                      patched MD5
26a9-04.bin     b8ce1f29bb973601ff5f95b3073880a0  3f5f52bd363519ca55b94293e7d58a47
26ac-0e.63      a459bd618ba87032fec636ee34e5adac  ba36cb71f1437b947bab2b50f09234f2
```

### Why there is no single patch for the whole zip

A zip file's checksum depends on the compression level and the order of the
files inside it, so the exact same ROM content can produce many different
zips. A patch made against one zip would silently fail against another. The
individual ROM files are stable, so those are what get patched.

---

<img width="240" height="224" alt="170027-2" src="https://github.com/user-attachments/assets/98b743c8-5000-4949-ba91-53f7ec673d12" />

## Compatibility

Tested on **FB Alpha 2012**. It should work on any emulator that runs the
`ddragon2` set, and on real hardware, since only the program ROMs change and
neither their size nor their layout is altered.

Two-player mode works normally: all the modified code is indexed per player,
so both players get the same behaviour.

---

<img width="256" height="240" alt="ddragon2-260905-153013" src="https://github.com/user-attachments/assets/5dbeea28-2072-4a8c-99b7-da6993c7553d" />

## Notes

- Not yet verified: picking up **wooden logs** with the punch button. The
  code is in place and behaves like every other pickup, but the situation
  has not come up in testing yet.
- The grab, knee strike and throw were left alone. They are described in the
  manual as "front attack" and "back attack", which under this hack map to
  fixed buttons like everything else, but they have not been measured
  individually.

---
