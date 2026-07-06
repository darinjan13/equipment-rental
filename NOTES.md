# NOTES

## 1. Explain one fix — Double-booking bug

The `dates_overlap` function checked only whether the new booking's start date fell inside the existing booking's range (`start_b <= start_a <= end_b`). This missed cases where the new booking started before the existing one but still overlapped (e.g., Jan 5–20 when an existing booking runs Jan 10–15). The fix uses the standard interval overlap check (`start_a <= end_b and start_b <= end_a`), which correctly catches all overlapping scenarios regardless of which range starts first.

## 2. Double-booking failure example

The original code wrongly allowed booking the Canon DSLR Camera from `2026-01-08` to `2026-01-12`, which overlaps the existing `2026-01-10` to `2026-01-15` booking. The fix now correctly blocks this.

## 3. AI use

I used OpenCode with the Superpowers plugin to help analyze the codebase, identify root causes, implement fixes, and verify them. I checked its output by:

- Reviewing each fix against the business rules in `app.py`
- Running end-to-end API tests to confirm correct behavior (overlap blocked, maintenance rejected, same-day pricing correct, non-overlapping allowed)
- Verifying no regressions in existing functionality
