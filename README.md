# Ranked

A phone web app for quitting bad habits, with a competitive ladder inspired by Valorant's rank system.

## How it plays

- **Daily match**: each day, mark every habit **Clean** or **Relapsed**, then **Lock in**. All clean = Victory, any relapse = Defeat.
- **Rank rating (RR)**: Victory is +20 RR, plus streak and multi-habit bonuses. Defeat is −20 RR (−30 at most), softened a little for habits you still held. Missions add +3 RR each, up to 4 a day.
- **Placements**: the first 5 matches count double and your rank stays hidden until they're done.
- **Ladder**: Iron → Bronze → Silver → Gold → Platinum → Diamond → Ascendant → Immortal (3 divisions each, 100 RR per division) → Radiant at 2400 RR. If you lose at 0 RR in a division, you drop a division.
- **Career**: RR graph, 16-week calendar heatmap, clean rate per habit, and match history.
- **Collection**: 24 badges (First Blood, Ace, Flawless, Clutch…). You can wear any unlocked badge as your title. This tab also shows the full ladder.
- **Settings**: add, edit or archive habits and missions, see how ranking works, and export or import a backup.

- **Apple Health**: missions can have a Health target, for example Exercise minutes ≥ 10 for "10-minute walk", Workouts ≥ 1, Mindful minutes, Water, Steps, or "in bed by 23:00". A sync ticks off every mission that hit its target. Settings → Apple Health has the setup guide.

You can check in or edit any of the last 7 days. RR is recalculated from your full history each time, so edits always stay consistent.

## Running it

It's a static site with no build step, hosted with GitHub Pages at **https://sevinli1225-spec.github.io/ranked/**. Open that on your phone:

- **iPhone**: in Safari, tap Share → Add to Home Screen.
- **Android**: in Chrome, open the menu → Install app.

To try it locally, run `python3 -m http.server` in this folder and open http://localhost:8000.

Data is saved in the browser's `localStorage` on that device only. Use **Export backup** in Settings now and then.

## Apple Health sync

Websites can't read Apple Health, so Ranked uses an iPhone Shortcut named **Ranked Health** as the bridge. The step-by-step guide is under Settings → Apple Health → Set up the shortcut. The shortcut reads today's Health samples and produces one line of text:

```
ranked-health:date=2026-10-08&steps=9120&exercise=34&workouts=1&mindful=6&water=2250&bedtime=22:40
```

- **Home Screen app**: tap **Sync Apple Health**. The shortcut runs and copies the line, then you switch back and tap **Paste**. iOS keeps Home Screen web apps' storage separate from Safari, which is why this uses the clipboard.
- **Safari**: the shortcut can open `https://sevinli1225-spec.github.io/ranked/#ranked-health:…` and the data is imported automatically.
- A daily Shortcuts automation, e.g. at 9:30 PM, can run the shortcut for you. You then paste in Ranked later.

Every field is optional, and number formats like `8,432` or `9:45 PM` are handled. Syncing only ever ticks missions on, never off, and only for the last 7 days.
