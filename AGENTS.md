# AGENTS.md - hardware/mainline/common-ext

This repository holds AI-assisted copies of components from
`hardware/mainline/common`, kept in a separate repository outside the
LineageOS organization because of that organization's rules restricting AI
tool usage, so this kind of development can keep happening. See `README.md`
for the full rationale.

## Hard rule: `docs/` is a symlink to the sibling `common` repository

`docs/` here is `-> ../common/docs`, i.e. it resolves inside a *different
git repository* checked out as a sibling directory. Editing anything under
`docs/` edits `hardware/mainline/common`, not this repository — do not do
that from here. Any convention specific to this repository (like the two
below) belongs directly in this file, or in a new top-level file, never
under `docs/`.

With that said, `docs/CODE_STYLE.md`, `COMMIT_CONVENTIONS.md`,
`WORKFLOW.md`, `NAMING_CONVENTIONS.md`, `INITIAL_IMPLEMENTATION_GUIDELINES.md`,
and `REVIEW.md` all apply here exactly as written, with the two adjustments
below.

## Naming convention (on top of `docs/NAMING_CONVENTIONS.md`)

Every build module that would otherwise collide with the same module name in
`hardware/mainline/common` gets an `ext`/`_ext` marker worked into its name
(usually right before a trailing `_defaults`/`impl`/variant suffix if it has
one, otherwise appended at the end) — e.g. `libfooimpl` → `libfooextimpl`,
`foo.bar` → `foo.bar_ext`. Everything else about a component (including
every other naming rule in `docs/NAMING_CONVENTIONS.md`) stays exactly the
same as in `common`, so cherry-picks between the two repositories stay
mechanical. See `README.md` for the full examples; when unsure, check how an
existing sibling component here was already renamed rather than inventing a
new pattern.

## Commit subject prefix (overrides the example in `docs/COMMIT_CONVENTIONS.md`)

Use `mainline/common-ext: <path>: <imperative summary>` (not
`mainline/common:`). Everything else in `docs/COMMIT_CONVENTIONS.md` —
body, `Assisted-by` trailers, `Change-Id` — applies unchanged.

## Review

This repository isn't hosted on LineageOS Gerrit (see `git remote -v`;
review here happens on gitea/GitHub instead), so `Code-Review`/`Verified`
votes don't literally apply. Still hold every commit to the same bar
described in `docs/REVIEW.md`: components here may eventually be
cherry-picked into `hardware/mainline/common` (adjusting the naming
convention above in whichever direction), and should already be able to
pass review there when that happens.

## Components

`interfaces/<domain>/<name>/` mirrors the same components as in `common`
(currently `sensors/mainline`, `vibrator/mainline`,
`graphics/allocator/fb`, `graphics/composer/drmfb`, `audio/effect/legacy`,
`audio/mainline`), plus their `libraries/` dependencies (`libhwdb`,
`smbios-parser`). Each has its own `AGENTS.md` with module-specific
guidance — read that file first when working inside such a directory.
