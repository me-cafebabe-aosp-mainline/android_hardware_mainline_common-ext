# The hardware/mainline/common-ext repository

## Introduction

With the new rules to restrict AI tools usage in LineageOS organization,
we're forced to copy the AI-written components from `hardware/mainline/common`
repository to this repository, which stays outside of LineageOS organization,
in order to keep some big development happening.

## The naming conventions for the components imported from the original repository

Every build modules, which would cause conflict with the ones in the original
repository, should have `ext` suffix added to its name.

For example:

- `libfooimpl` -> `libfooextimpl`
- `libfoo_%s` -> `libfoo_ext_%s`
- `foo.bar` -> `foo.bar_ext`
- `foo.bar_defaults` -> `foo.bar_ext_defaults`

Every other naming conventions stays exactly the same,
in order to keep it simple to do cherry-picks between the repositories,
and keep most of things unchanged for the users.
