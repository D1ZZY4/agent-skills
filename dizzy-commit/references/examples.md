# Worked Examples

## Good, default mode

```
feat(api): add GET /users/:id/profile

Mobile client needs profile data without the full user payload
to reduce LTE bandwidth on cold-launch screens.

Closes #128
```

## Good, strict mode

Two unrelated dark-mode fixes, split into two commits. See `strict-mode.md` for the author
and banned-word rules applied here.

```
fix(button): dark mode contrast on danger variant

Add `dark:text-[#f07060]` and `dark:border-[#d44a30]` to danger variant.

Aligns with `--status-unstable-text` and `--status-unstable-border` dark
variants already defined in `globals.css`.
```

```
fix(info-tab): status tokens for stable/bug colors

- `text-[var(--color-stable)]` -> `text-[var(--status-stable-text)]`
- `bg-[var(--color-unstable)]` -> `bg-[var(--status-unstable-border)]`

Fixes dark mode contrast. The raw color vars have no dark override.
```

## Bad: bundled, plan-flavored, banned words

```
refactor: Phase 3, security fixes, bug fixes, and accessibility improvements

Security:
- Remove spam-protection note from FeedbackForm
- Add URL scheme guards for download_link/donate_link

Bug fixes:
- Wire filterPillVariants into BrandFilter
- Replace rounded-* with wobble.* in RomFormModal, FeedbackTab, RomGrid
...
```

17 unrelated changes in one commit, no scope, contains "Phase 3." Split into one focused
commit per concern instead, each with its own scope.

## Bad: subject and body run together, changelog-dump body (real failure mode)

```
docs(repo): sync references after LICENSE rename and NFC doc integration Update LICENSE.md to LICENSE in 8 README files following the a270f09 rename - Register nfc-oos-post-port.md in port-rom AGENTS.md, REFERENCE.md, and README.md file maps - Delete integrated prompt/info-1.md and prompt/info-2.md
```

Broken in three ways: no blank line between subject and body, so it reads as one run-on
sentence; the body lists individual files instead of the actual change; and it never checked
whether `prompt/` was gitignored before including content sourced from it.

Fixed version, using the `-F` file method from `commit-execution.md` to guarantee real
separation:

```
docs(repo): sync references after LICENSE rename

Update LICENSE.md references to LICENSE across READMEs and register
the new NFC port doc in the port-rom file maps, following a270f09.

Drops the now-redundant prompt/info-1.md and info-2.md content that
was already merged elsewhere.
```
