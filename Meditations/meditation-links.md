# Meditation Links

**Last Updated:** November 9, 2026
**Status:** Live
**Feature Area:** Meditation

## Overview

This page lists every built-in meditation in the Stay Positive Android app and the YouTube video it plays.

All built-in meditations are YouTube videos. The app stores each one as a YouTube video ID and builds the full link as `https://www.youtube.com/watch?v=<youtubeId>`.

A machine-readable copy of this list is in [`meditation-links.json`](meditation-links.json).

---

## Built-in Meditations

| Collection | Title | ID | YouTube Link |
|---|---|---|---|
| Relieve Stress | Relaxation | `relaxation` | https://www.youtube.com/watch?v=cyxv_X-JmxE |
| Relieve Stress | Relaxation II | `relaxation_ii` | https://www.youtube.com/watch?v=GTdEJwVOxg0 |
| Relieve Stress | Work Stress | `work_stress` | https://www.youtube.com/watch?v=X4WjbW6amQw |
| Find Focus | Communication | `communication` | https://www.youtube.com/watch?v=rJHBW8-56zU |
| Find Focus | Focus | `focus` | https://www.youtube.com/watch?v=zSkFFW--Ma0 |
| Find Focus | Productivity | `productivity` | https://www.youtube.com/watch?v=tI16SNCtMrQ |
| Sleep Well | Rainfall | `rainfall` | https://www.youtube.com/watch?v=eTeD8DAta4c |
| Guided | Pineal Gland Awakening | `pineal_gland_awakening` | https://www.youtube.com/watch?v=QgsJfSaiJ4Y |
| Learn to Meditate | Foundations I | `foundations_i` | https://www.youtube.com/watch?v=VUjiXcfKBn8 |
| Learn to Meditate | Foundations II | `foundations_ii` | https://www.youtube.com/watch?v=uqtIqCKjkuc |
| Learn to Meditate | Foundations III | `foundations_iii` | https://www.youtube.com/watch?v=cesbu-AbcuU |
| Learn to Meditate | Foundations IV | `foundations_iv` | https://www.youtube.com/watch?v=LTsbayyhKfA |

**Total:** 12 meditations

---

## Where This Lives in the App

The same list is defined in three places in the Android app:

* `Reset/MeditationCatalog.kt` — used as the Reset routine fallback when a user has no favorites
* `Meditation/MeditationActivity.kt` — `getUrlFromSessionId()`
* `Meditation/MeditationsMainActivity.kt` — `getUrlFromSessionId()`

When a meditation is added, removed, or its video changes, all three must be updated, along with this page and `meditation-links.json`.

The meditation ID is saved to Firestore, so an ID must never be renamed once it has shipped.

---

## Not Included

* **My Meditations (Premium):** YouTube links that Premium users add themselves. These are stored per user in Firebase, not in the app code.
* **Reset Visualization placeholder audio:** a temporary sample audio file, not a meditation.
