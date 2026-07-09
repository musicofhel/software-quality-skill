# Interface papercut checklist

Walk every applicable item; record each miss as a papercut finding. Items marked
**[H]** paraphrase Anthony Hobday's original quality-of-life list
([source](https://anthonyhobday.com/blog/20260410)); the rest extend it.

## Pointer & keyboard forgiveness

- [ ] **[H]** Generous mouse paths — nested menus tolerate the diagonal shortcut
      to a submenu without closing.
- [ ] **[H]** Coyote time for shortcuts — releasing the wrong key first doesn't
      instantly cancel a multi-key chord.
- [ ] **[H]** No traps under the cursor — UI that opens at the mouse position
      never puts a destructive action where a double-click would land.
- [ ] **[H]** Correct mobile keyboard per field (numeric, email, URL).
- [ ] Click targets ≥ 44px on touch; small icons get padded hit areas.
- [ ] Hover-revealed controls are also reachable by keyboard and touch.
- [ ] Drag operations can be cancelled (Escape) and have a forgiving drop tolerance.
- [ ] Text is selectable wherever a user might want to copy it (IDs, errors, paths).

## Focus & keyboard

- [ ] Focus ring visible on every interactive element — never `outline: none`
      without a replacement.
- [ ] Tab order matches visual order.
- [ ] Modals trap focus while open and return it to the trigger on close.
- [ ] Escape closes the topmost layer only (menu → modal → page, one per press).
- [ ] Enter submits the obvious single-field form; Cmd/Ctrl+Enter submits textareas.
- [ ] First field of a form is autofocused — unless the page is content-first,
      where stealing focus is the papercut.
- [ ] Keyboard shortcuts don't fire while typing in an input.

## Motion & transitions

- [ ] **[H]** End-of-list feedback — scroll views stretch/bounce or otherwise
      signal the end.
- [ ] **[H]** Expand/collapse animates fast and smooth rather than snapping.
- [ ] **[H]** Animations originate from the triggering element.
- [ ] **[H]** Elements that move between positions animate rather than teleport.
- [ ] **[H]** Motion cues changes at the edge of vision.
- [ ] **[H]** Popups appear ~instantly, fade away slightly slower.
- [ ] **[H]** Tooltips warm up — first one delayed, neighbors then instant.
- [ ] All motion shares duration/easing tokens; nothing animates longer than
      ~300ms for common actions.
- [ ] `prefers-reduced-motion` is honored.
- [ ] Nothing animates on a loop in the user's peripheral vision while they work.

## Spatial stability

- [ ] **[H]** Optical alignment — icons, triangles, and mixed-size text nudged to
      *look* aligned, not just measure aligned.
- [ ] **[H]** Entering edit mode keeps text in exactly the same place.
- [ ] **[H]** Interacting with or near an element never moves it (unless moving
      is the point).
- [ ] **[H]** List insert/remove preserves the user's visual scroll position.
- [ ] **[H]** Context-menu actions sit in the same spot relative to the cursor
      every time.
- [ ] **[H]** Object permanence — shared elements persist through view
      transitions, even while moving or resizing.
- [ ] **[H]** Movable elements with natural resting positions snap into them.
- [ ] No layout shift on load — images and async content reserve their space.
- [ ] Scroll position restores on back-navigation.
- [ ] Long text truncates with a tooltip or expansion — never silently.

## Forms & input

- [ ] Validate on blur; revalidate on input — never scold mid-typing, never wait
      for submit to reveal every problem at once.
- [ ] Inputs are forgiving: trim whitespace, accept paste artifacts, take phone
      numbers and cards with or without separators.
- [ ] Error messages sit next to the field they describe, and the first invalid
      field gets focus on failed submit.
- [ ] Labels are real labels (clicking them focuses the field); placeholder text
      is never the only label.
- [ ] Submit disables (or dedupes) during flight and shows progress.
- [ ] Destructive actions get undo where possible; confirmation dialogs only
      where undo is impossible — and then the confirm button names the action
      ("Delete project", never "OK").

## Data, feedback & state

- [ ] **[H]** User input survives leaving the screen unless explicitly discarded.
- [ ] **[H]** Changes preview live; effects on off-screen things get a preview.
- [ ] Every async action confirms success or failure — nothing ends in silence.
- [ ] Loading uses skeletons for content, spinners only for actions; anything
      past ~10s gets a cancel and an estimate.
- [ ] Stale data is marked as stale, or refreshes itself.
- [ ] Timestamps show relative *and* absolute ("2h ago · Jul 8, 14:32"), in the
      user's timezone.
- [ ] Numbers are formatted for the locale; tabular numbers align in columns.
- [ ] Copy-to-clipboard confirms it copied.
- [ ] Empty states explain what belongs there and offer the primary action.
- [ ] Notifications/toasts don't cover the thing they're about, and persist long
      enough to read (or until dismissed, if they contain an action).

## Words

- [ ] One concept, one name — everywhere (UI, errors, docs).
- [ ] Errors say what happened, why, and what to do next; never blame the user;
      never ship a code as the whole message.
- [ ] Buttons are verbs describing the outcome ("Save changes"), not "Submit"/"OK".
- [ ] Sentence case or title case — picked once, applied everywhere.
- [ ] No developer vocabulary leaks: "null", "undefined", "NaN", raw enum values,
      or `snake_case_keys` visible to users.
