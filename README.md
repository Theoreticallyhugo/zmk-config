## Flashing
 1. download firmware from actions
 1. plug in one half of keyboard and double click lil white button
 1. mount and pull .uf2 file on it
 1. repeat for other half

## ZMK version pinning
ZMK is pinned to a fixed commit instead of tracking `main`, so builds are
reproducible and don't silently change firmware between flashes. It's pinned
in two places, which must be updated together:
 - `config/west.yml` (`revision:`)
 - `.github/workflows/build.yml` (`build-user-config.yml@<sha>`)

When to bump: only when you deliberately want to pull in new upstream ZMK
changes (bugfix, feature, new board support) — not automatically. To bump,
grab the latest commit SHA from https://github.com/zmkfirmware/zmk/commits/main,
update both files to that SHA, then build and test before relying on it. If
something breaks after a bump, reverting both files to the previous SHA gets
you back to a known-good state.
