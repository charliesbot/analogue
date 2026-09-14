# Analogue — Product Requirements

_An app for completing things, not collecting them._

## Context

There are countless apps for tracking media consumption — Letterboxd, Goodreads, Backloggd, Last.fm. They all share the same problem: they optimize for _discovery and collection_, not _completion and presence_. For someone with ADHD, this is poison. The dopamine hit comes from adding the next thing, not finishing the current one.

Analogue flips that. It's a tool built around _constraints_. You commit to what you're experiencing right now, and the app holds you to it. No social feed, no recommendations. Just: what are you doing, and are you done yet? And when you're done — reflect on it before moving on.

## Initial Focus

**The initial release focuses exclusively on video games.** The broader goal remains intentional media consumption, but the first experience is built around choosing, playing, completing, and reflecting on games.

The actions and constraints are unchanged: one active game, a backlog of at most five games, completion with a rating and reflection, return to backlog, dropping, and completed/dropped history. This narrows the supported media, not the existing feature requirements.

Multi-category concepts below are preserved as the broader product vision, not initial-release requirements. Books, music, movies, category navigation, and their integrations are outside the initial scope. Future ideas are possibilities, not committed releases.

## Philosophy

- **One active item per category.** You're playing one game, reading one book, listening to one album, watching one movie. That's it.
- **Tiny backlog, not a wishlist.** Max 5 items queued per category. Want to add a 6th? Remove one first. This forces prioritization over accumulation.
- **Commit or let go.** An active item is either _in progress_, _completed_ (with a review), or _dropped_. No percentages, no chapters, no "on hold". You finish it or you consciously walk away.
- **Completion = reflection.** When you finish something, you rate it and write about it. Optional voice transcription for when thoughts flow better spoken. This is the moment of presence — you don't just check a box, you sit with what you experienced.
- **No attention-seeking.** No notifications, no streaks, no gamification. The app is quiet. You come to it when you're ready.
- **Fewer decisions, not more.** The content is the app. In the broader multi-category vision, the categories are the navigation; the games-only release needs no category navigation. If a control isn't load-bearing, it doesn't exist. Every surface the user lands on should ask of them: _one thing_ (or nothing at all). Cognitive overhead is the enemy of presence.
- **Self-growth as a side effect.** The constraints push you to try new things. The reviews capture what you thought. Over a year, this becomes a journal of your taste evolving — what you loved, what you dropped, what surprised you.

## Categories — Broader Product Vision

Only games are included in the initial release. The remaining categories preserve the intended expansion possibilities.

1. **Games** — one active game at a time
2. **Music** — one active album at a time (full album listening, not singles/playlists)
3. **Books** — one active book at a time
4. **Movies** — one active movie at a time. Being present means you actually watched it — not half-watching while on your phone.

## Core Concepts

### Home

The initial home experience shows the current active game at a glance and offers
a way to add a game when the slot is empty. The broader product vision supports
seeing active items across categories; its layout is not an initial requirement.

### Active Slot

Each category has exactly **one active slot**. When you put something in it, a start date is recorded. Three possible outcomes:

1. **Complete it** — triggers the review flow (rating + description), records completion date, frees the slot.
2. **Move back to backlog** — you're not ready for this yet, but you still want it. Clears the start date and moves it back to the queue. No penalty, no log entry.
3. **Drop it** — a deliberate action with confirmation. The item moves to a quiet "dropped" log. No review required.

### Completion Review

When marking something complete, the app asks for:

- **Rating** — 1-5 stars. Simple enough to not overthink, granular enough to reveal patterns over time.
- **Description** — free-text reflection. What did you think? What stuck with you?
- **Voice transcription** — optional. Let users speak their review instead of typing. Lower friction, more natural for capturing in-the-moment thoughts.

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

## Search and Custom Entries

Users can search for games and add a result with its title, cover art, and metadata.
When no match is found, they can create a custom entry with just a title and no
cover art. The same capability belongs to the broader product vision for other
media, including obscure albums and self-published books, but only games are in
initial scope.

## Platform

A native Android app built with Jetpack Compose, with an adaptive UI for phone,
large-screen, and resizable desktop-style Android windows. Desktop means the
Android app adapting to its available window, not a separate Windows, macOS, or
Linux app. Installability, offline support, and Google sign-in remain requirements.

## Open Questions

1. **Rating scale:** 1-5 stars. Decided — enough signal for year-end self-reflection without overthinking.
2. **Music: what counts as "complete"?** Honor system. The point is the _intention_ to sit with an album. One full listen-through is the spirit of it.
3. **Year-in-review.** A generated retrospective of everything you completed and dropped, with your reviews. Possible later feature — not for the initial release.

## Initial Release Scope — Video Games

- Native Android app using Jetpack Compose, with offline support and installability
- Adaptive Android UI across phone, large-screen, and desktop-style window sizes
- Games only: 1 active slot, 5-item backlog, completed list, dropped log
- Search + add games (with cover art), with custom entries when no match is found
- Move to active, mark complete (with review), return to backlog, drop
- Voice transcription option for reviews
- Google sign-in
- Home screen showing the current active game at a glance
- Completed game history with reviews

The broader expansion retains the same active slot, backlog, completed list, dropped log, and reviews for each additional category, with a home screen showing active items across categories. It is not required for this release.

## Supporting Documents

- [Games-first design](design/games-first.md) describes interaction and implementation details, retained broader design context, and unresolved design questions.
- [Media API candidates](research/media-apis.md) preserves existing provider notes; these are not newly verified research findings.
