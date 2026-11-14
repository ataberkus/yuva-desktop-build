# yuva-desktop-build

CI for the Yuva desktop apps. The source is the private `ataberkus/yuva-prealpha`; these workflows check it out with
a read-only deploy key.

- `poll.yml` — every 10 minutes, dispatches a publishing build for each app whose files changed on `main` since its
  last `desktop-v*` / `desktop-mac-v*` tag.
- `desktop-release.yml` — Windows installer → `https://yuva.chat/desktop/latest.yml`.
- `desktop-mac.yml` — macOS DMG → `https://yuva.chat/desktop/latest-mac.yml`.
- `ios.yml` — iOS app (`mobile/`) → simulator launch check, then TestFlight (App Store Connect API key secrets, see
  the top of the file). Manual only: `gh workflow run ios.yml -R ataberkus/yuva-desktop-build -f ref=main`.

Manual build of any ref (artifact only unless `publish`):

```
gh workflow run desktop-mac.yml -R ataberkus/yuva-desktop-build -f ref=<branch|sha>
```

Run logs and artifacts are public.
