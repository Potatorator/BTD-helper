# BTD Auto Helper - Mobile (Android)

The phone version of the PC helper for Roblox **Build Tower Defense**. It runs *on the phone*, over the
game: it taps **Retry** after a defeat and checks the **Spawner Shop** for Legendary / Mythic (and
optionally Secret) spawners, buying them when they're in stock.

> Android 11 or newer. iPhone is not possible (iOS doesn't let one app see or tap inside another).

## 1. Build the app (once)

**Option A - Android Studio (easiest)**
1. Install Android Studio (free) from developer.android.com/studio.
2. *File > Open* this folder. Wait for "Gradle sync" to finish (first time downloads ~1 GB).
3. *Build > Build App Bundle(s) / APK(s) > Build APK(s)*.
4. Click **locate** - the file is `app/build/outputs/apk/debug/app-debug.apk`.

**Option B - GitHub (no installs)**
Put this folder in a GitHub repository; the included workflow builds the APK automatically.
Download it from the repository's **Actions** tab > latest run > *BTD-Auto-Helper-APK*.

## 2. Install and set up on the phone
1. Copy the APK to the phone and open it. Allow "install unknown apps" when asked.
2. Open **BTD Auto Helper** and tap **Open Accessibility settings**.
3. Find **BTD Auto Helper** (Samsung: *Installed apps*) and turn it on.
   - If Android says the setting is **restricted** (Android 13+ for apps not from the Play Store):
     go to *Settings > Apps > BTD Auto Helper*, tap **⋮** (top right) > **Allow restricted settings**,
     then turn it on again.
4. Open Roblox. A round blue button appears on the left edge - tap it for the control panel,
   drag it to move it.

## 3. Use it
- **Start** - the panel hides itself; the button's ring shows the status
  (green = running, orange = checking the shop, blue = waiting for Roblox, grey = stopped).
- **Check shop** - runs a shop check right now.
- **Calibrate** - only if taps miss (other phone / layout): tap SPAWNERS, then the shop's X,
  then the middle of the card list, when asked.
- Switches, rarity chips and the interval are saved instantly.
- Keep Roblox on screen. Don't touch the screen while it's tapping.

## Feature list (PC -> mobile)
| PC version | Mobile version |
|---|---|
| Auto-click Retry (blue button + "Retry" text check, never other buttons) | Same detection; never taps Revive, Close or Skip Wave |
| Click timed in 60 FPS frames, verify, slower fallback, switch to slow after 2 misses | Tap held 3 frames (50 ms), verify, 120 ms fallback, same switch-over |
| Shop check every N min / on start / "Check shop now" | Same |
| Opens shop via SPAWNERS, closes via X (auto-found) / saved point | Same (mobile positions measured from your screenshots) |
| Quick scan (bottom rows) / full scan (every page) | Same - quick scan reads up from the bottom until the Epic row (Ice Cave's row) |
| Rarity from the label: Legendary, Mythic (gradient), Secret | Same + reads the grey Secret label |
| Buy only steady buttons (2 frames agree), max 10 per check, 5 tries per card | Same. Mobile Buy buttons are orange - both orange and green are recognised |
| Buy automatically off = beep + log only | Sound + vibration + log only |
| Robux popup safety: close it, stop buying | Same (closes it with Back) |
| Switch back to my window | **Hide controls while tapping** - phone equivalent: the helper's button can never catch a tap |
| Debug pictures | Saved to `Android/data/com.btdhelper/files/debug_shots` |
| Calibrate (hover + F8) | Calibrate by tapping the 3 points |
| Status, counters, countdown, coloured activity log | Same, in the floating panel and in the app |
| "Roblox not found / minimized" | "Waiting for Roblox" when Roblox isn't on screen |
| crash_log.txt | `Android/data/com.btdhelper/files/crash_log.txt` |

## What was tested before delivery
- Detection on all 7 of your mobile screenshots at 3 resolutions (incl. 2340x1080):
  Retry found on the Defeat screen (match 0.87-0.91), never on gameplay (Skip Wave);
  every card's rarity read correctly; X and scrollbar found.
- The real automation engine run against a simulated phone built from the screenshots:
  Retry, missed-tap fallback, quick scan (bought Mythic + Card Kingdom + Ice Cave, skipped Secret),
  full scan with Secret enabled, auto-buy off, Robux-popup safety, waiting for Roblox, Stop.
- The control panel, rendered at phone size (landscape over the game and portrait in the app).
- The whole app compiles (checked against stand-ins for the Android classes).

**Not tested here (needs your phone):** Android's real screenshots and taps, the floating button,
and how Roblox reacts to taps/swipes (e.g. scroll speed). If something is off, turn on
*Debug pictures*, run once, and send the pictures + the activity log.
