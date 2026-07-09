# Interface quality-of-life checklist

Paraphrased from Anthony Hobday's ["Notes on software quality"](https://anthonyhobday.com/blog/20260410).
Go through every item that applies to the interface under audit; record each miss
as a papercut finding.

## Pointer & keyboard forgiveness

- [ ] **Generous mouse paths** — nested menus stay open while the mouse travels
      diagonally toward a submenu, even if it briefly leaves the menu's bounds.
- [ ] **Coyote time for shortcuts** — multi-key shortcuts aren't cancelled the
      instant the wrong key is released first.
- [ ] **No traps under the cursor** — when a click opens new UI at the mouse
      position, nothing risky sits where a second accidental click would land.
- [ ] **Correct mobile keyboard** — each field opens the right keyboard type
      (numeric, email, etc.).

## Motion & transitions

- [ ] **End-of-list feedback** — scrollable lists stretch/bounce (or otherwise
      signal) when the user hits the end.
- [ ] **Animated expand/collapse** — everything that expands or collapses does so
      with a fast, smooth animation rather than snapping.
- [ ] **Animation origin** — expansion starts from the element that triggered it,
      so it reads as growing away from that element.
- [ ] **Animated movement** — elements that move between positions animate rather
      than teleport.
- [ ] **Peripheral change cues** — motion draws attention when something appears
      or changes at the edge of the user's vision.
- [ ] **Asymmetric popup timing** — menus and popups appear ~instantly but fade
      away slightly slower.
- [ ] **Tooltip warm-up** — tooltips open on a delay, but once one is showing,
      moving to a neighboring element shows its tooltip instantly.

## Spatial stability

- [ ] **Optical alignment** — visually unbalanced elements are nudged so they
      *look* aligned, not just mathematically aligned.
- [ ] **Stable edit mode** — switching text to an editable state keeps the text in
      exactly the same place.
- [ ] **No reactive layout shift** — interacting with or near an element never
      moves it, unless moving it is the point.
- [ ] **Subjective scroll position** — adding/removing list items keeps the items
      the user is looking at visually in place.
- [ ] **Consistent context menus** — menu actions appear in the same position
      relative to the cursor every time.
- [ ] **Object permanence** — elements shared between views persist through the
      transition, even if they move or resize.
- [ ] **Snap points** — movable elements with natural resting positions (e.g.
      horizontal card stacks) snap into them.

## Data & feedback

- [ ] **Never lose input** — text or choices the user entered survive leaving the
      screen, unless they explicitly discard them.
- [ ] **Live preview** — changes show in real time; if the affected thing isn't
      visible, a preview shows the effect as options change.
