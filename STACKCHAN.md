# StackChan integration branch

`personal` in this fork is not a generic board branch and is not sent
upstream. It carries the device-core changes needed by
[xupeng/StackChan](https://github.com/xupeng/StackChan), whose `personal`
branch pins a full commit SHA from here through `firmware/repos.json`.

Because the two repositories are coupled, a change here has to be pushed
first and the pinned SHA in StackChan updated in the same round:

1. commit here on `personal`
2. `git push origin personal`
3. update `firmware/repos.json` in StackChan to the new SHA
4. rebuild, then flash

Branch content, in order:

- StackChan board integration imported from the patch that used to live in
  the StackChan tree (binding flow, asset loading, `TryReadRegs`,
  overridable `StartWifiConfigMode`)
- interrupting a spoken reply, dropping audio tasks of an aborted reply
  through a playback generation, honouring the abort reason on TTS stop
- runtime sleep/shutdown delays on `PowerSaveTimer`
- keeping OTA server timestamps in UTC
- head tap stopping both speech and a running Agent dance

## Keeping up with upstream

The branch is rebased onto newer upstream release tags instead of merged,
so the commits above stay a short linear stack. After a rebase, push with
`--force-with-lease` and update the SHA pinned by StackChan.

Tag stable points as `personal-YYYY-MM-DD`.
