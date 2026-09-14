# Games-first Experience and Implementation

**Date:** 2026-09-12

## TL;DR

The initial release supports games only, with the actions and constraints defined
in the PRD. This document extracts existing interaction and implementation choices;
it does not claim they are implemented or settle the remaining design gaps.
The broader dashboard and data model are retained explicitly as context, not a
requirement to build multi-category infrastructure now.

## Design

### Home and navigation

**Initial release:** the home experience centers on the single active game, not a four-category dashboard. The occupied/empty slot behavior below still applies; the exact games-focused layout remains a design decision.

**Broader multi-category concept (not initial scope):**

The root of the app. Four slots, one per category. Each slot has two states:

- **Occupied** — holds the active item. Surfaces cover art, title, secondary metadata, and category identity.
- **Empty** — the category has no active item. Entering an empty slot opens the add-item flow for that category.

Category identity is always legible — the user can tell which slot is which without entering it. Entering an occupied slot opens the item's detail view. **No other affordances at root.**

The broader dashboard above is preserved, not a new games-first layout proposal.
`DESIGN.md` also assumes four rows and category navigation. Those assumptions do
not apply to the games-only scope; adapting its visual guidance is still open.
This extraction does not replace that design system or decide a new layout.

### Adding games

1. The user types into a games search input.
2. Debounced search autocompletes from IGDB, the existing games provider choice.
3. Selecting a result saves its title, cover art, and metadata.
4. When no match exists, a custom entry needs only a title and has no cover art.

The original flow describes saving results and custom entries locally. Firestore
is also specified for persistence below; the relationship between local storage,
offline behavior, and remote persistence remains unresolved.

### State transitions and review interaction

The PRD owns the allowed actions, capacity limits, and review requirements.
The existing implementation details are:

- Starting an item records `startedAt`.
- Completing opens the rating-and-description review flow, records `completedAt`,
  and frees the active slot.
- Returning to backlog clears `startedAt`, creates no log entry, and has no penalty.
- Dropping asks for confirmation, with the existing copy example:
  “You started this on Feb 3. Drop it?” It records `droppedAt` without a review.
- The dropped log is tucked away rather than prominently displayed. Completed
  history is chronological and shows dates, ratings, and reflections.

Optional voice transcription remains a product requirement. The previous Web
Speech API proposal is no longer the implementation target for the native Android
app; its native implementation and fallback behavior remain undecided.

### Platform and persistence

The app targets native Android with Jetpack Compose and an adaptive UI. Layouts
respond to the available app window, from phone-sized windows to large screens
and resizable desktop-style Android windows. Desktop is an Android windowing
experience, not a separate Windows, macOS, or Linux app or a multiplatform target.
Offline support, installability, and Google sign-in remain product requirements.

Firestore persistence and Firebase Auth with Google sign-in remain the existing
backend choices. The prior PWA deployment proposal at `analogue.charlies.bot`
through Firebase App Hosting is no longer the app delivery plan. Native app
distribution has not been decided. These are design choices, not evidence of an
already implemented system.

`DESIGN.md` retains web-specific guidance. Its visual intent can inform the native
app, but browser implementation details are not requirements for Jetpack Compose.

### Conceptual data model

This conceptual model preserves the broader multi-category design. Initially, only games and game-relevant metadata are in scope. The other category values and metadata fields do not require multi-category infrastructure in the first release. Statuses, dates, reviews, backlog ordering, and constraints still apply to games.

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

## Open questions

- What games-focused home layout and navigation replace the four-row/category assumptions in `DESIGN.md`, and how is its visual guidance adapted to Compose?
- What happens when returning the active game to an already full backlog? The five-item cap must remain intact.
- How do local saves, Firestore persistence, and offline changes work together?
- How will IGDB requests and credentials be handled? See the preserved API research questions.
- What native voice-transcription implementation and fallback behavior are needed?

## Links

- [Product requirements](../PRD.md) — product behavior, constraints, and release scope.
- [Media API candidates](../research/media-apis.md) — inherited notes requiring verification.
- [Visual design system](../../DESIGN.md) — existing visual guidance; multi-category layout needs adaptation.
