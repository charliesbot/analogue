# Analogue — Design Doc

_A PWA for completing things, not collecting them._

## Context

There are countless apps for tracking media consumption — Letterboxd, Goodreads, Backloggd, Last.fm. They all share the same problem: they optimize for _discovery and collection_, not _completion and presence_. For someone with ADHD, this is poison. The dopamine hit comes from adding the next thing, not finishing the current one.

Analogue flips that. It's a tool built around _constraints_. You commit to what you're experiencing right now, and the app holds you to it. No social feed, no recommendations. Just: what are you doing, and are you done yet? And when you're done — reflect on it before moving on.

## Philosophy

- **One active item per category.** You're playing one game, reading one book, listening to one album, watching one movie. That's it.
- **Tiny backlog, not a wishlist.** Max 5 items queued per category. Want to add a 6th? Remove one first. This forces prioritization over accumulation.
- **Commit or let go.** An active item is either _in progress_, _completed_ (with a review), or _dropped_. No percentages, no chapters, no "on hold". You finish it or you consciously walk away.
- **Completion = reflection.** When you finish something, you rate it and write about it. Optional voice transcription for when thoughts flow better spoken. This is the moment of presence — you don't just check a box, you sit with what you experienced.
- **No attention-seeking.** No notifications, no streaks, no gamification. The app is quiet. You come to it when you're ready.
- **Fewer decisions, not more.** The content is the app. The categories are the navigation. If a control isn't load-bearing, it doesn't exist. Every surface the user lands on should ask of them: _one thing_ (or nothing at all). Cognitive overhead is the enemy of presence.
- **Self-growth as a side effect.** The constraints push you to try new things. The reviews capture what you thought. Over a year, this becomes a journal of your taste evolving — what you loved, what you dropped, what surprised you.

## Categories (v1)

1. **Games** — one active game at a time
2. **Music** — one active album at a time (full album listening, not singles/playlists)
3. **Books** — one active book at a time
4. **Movies** — one active movie at a time. Being present means you actually watched it — not half-watching while on your phone.

**Later (v2):** TV Shows (seasons as the unit of completion)

## Core Concepts

### Dashboard

The root of the app. Four slots, one per category. Each slot has two states:

- **Occupied** — holds the active item. Surfaces cover art, title, secondary metadata, and category identity.
- **Empty** — the category has no active item. Entering an empty slot opens the add-item flow for that category.

Category identity is always legible — the user can tell which slot is which without entering it. Entering an occupied slot opens the item's detail view. **No other affordances at root.**

### Active Slot

Each category has exactly **one active slot**. When you put something in it, a start date is recorded. Three possible outcomes:

1. **Complete it** — triggers the review flow (rating + description), records completion date, frees the slot.
2. **Move back to backlog** — you're not ready for this yet, but you still want it. Clears startedAt, moves it back to the queue. No penalty, no log entry.
3. **Drop it** — a deliberate action with confirmation (_"You started this on Feb 3. Drop it?"_). The item moves to a quiet "dropped" log. No review required.

### Completion Review

When marking something complete, the app asks for:

- **Rating** — 1-5 stars. Simple enough to not overthink, granular enough to reveal patterns over time.
- **Description** — free-text reflection. What did you think? What stuck with you?
- **Voice transcription** — optional. Use the Web Speech API to let users speak their review instead of typing. Lower friction, more natural for capturing in-the-moment thoughts.

The review is the heart of the app. It's what turns "I finished a game" into "I reflected on an experience."

### Backlog

Each category has a backlog capped at **5 items**. Items include title + cover art (fetched via API). To add a 6th, you must remove one. The backlog is a queue, not a collection.

To start something from the backlog, you move it to the active slot (which must be empty — you finished or dropped the current one first).

### Dropped Log

A quiet, tucked-away list of things you started but didn't finish, with start and drop dates. Not prominently displayed — you'd have to look for it. But over time it reveals patterns: do you always drop books after two weeks? Do you never drop games? Useful for year-end self-reflection.

### Completed / History

A chronological list of everything you've finished, with start/completion dates, ratings, and your reviews. This is your journal of experiences. At year-end, this becomes a powerful personal retrospective.

### What the app does NOT have

- Social features
- Recommendations or discovery
- Import from other services
- Notifications or reminders
- Stats or streaks
- Gamification of any kind

## Media APIs

Cover art and metadata are fetched from external APIs when adding items:

| Category | API                             | Notes                                                       |
| -------- | ------------------------------- | ----------------------------------------------------------- |
| Games    | IGDB (via Twitch)               | Cover art, platform info                                    |
| Books    | Google Books API                | Free, no key required for basic queries                     |
| Movies   | TMDB                            | Free tier, cover art + year                                 |
| Music    | MusicBrainz + Cover Art Archive | Free, no auth. Or consider Spotify API for better cover art |

**Adding an item flow:**

1. User types in a text input scoped to the current category.
2. As they type, the app autocompletes from the relevant API (debounced search).
3. User picks a result → title, cover art, and metadata are saved locally.
4. If there's no match (indie game, obscure album, self-published book), the user can create a **custom entry** — just a title, no cover art. Custom entries are saved to the local DB like any other item.

## Platform

- **PWA.** Installable, works on phone and desktop. Deployed to `analogue.charlies.bot` via Firebase App Hosting.

## Data Model

```
Category: games | music | books | movies

Item {
  id: string
  title: string
  category: Category
  status: "active" | "backlog" | "completed" | "dropped"
  coverUrl: string | null       // from API
  metadata: {                   // from API, category-specific
    author?: string             // books
    artist?: string             // music
    developer?: string          // games
    director?: string           // movies
    year?: number
    platform?: string           // games
  }
  startedAt: Date | null        // set when moved to active
  completedAt: Date | null      // set when marked complete
  droppedAt: Date | null        // set when dropped
  review: {                     // set on completion
    rating: number              // 1-5 stars
    description: string
  } | null
  createdAt: Date               // when first added
  position: number              // order in backlog
}
```

Constraints enforced at the app level:

- Max 1 item with status "active" per category
- Max 5 items with status "backlog" per category
- Completing requires a review (rating + description)
- Dropping records droppedAt but no review

## Open Questions

1. **Rating scale:** 1-5 stars. Decided — enough signal for year-end self-reflection without overthinking.
2. **Music: what counts as "complete"?** Honor system. The point is the _intention_ to sit with an album. One full listen-through is the spirit of it.
3. **TV shows (v2).** Season as the unit of commitment makes sense — it's a contained arc.
4. **Year-in-review.** A generated retrospective of everything you completed and dropped, with your reviews. Powerful v2 feature — not for v1.

## v1 Scope

- PWA shell with offline support and installability
- 4 categories, each with: 1 active slot, 5-item backlog, completed list, dropped log
- Search + add items via external APIs (with cover art)
- Move to active, mark complete (with review), drop
- Voice transcription option for reviews
- Firestore + Firebase Auth (Google sign-in)
- Home screen showing current active items at a glance
- Completed history per category with reviews
