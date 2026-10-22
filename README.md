# Design — Mobile

## Template copy

This repo is one of the name-substituted Flutter template copies in
`bookchaowalit-mobile`. The canonical Flutter template is
[`bookchaowalit-mobile/education-coursenotes-mobile`](https://github.com/bookchaowalit-mobile/education-coursenotes-mobile);
fixes land there first and are copied here (this repo owns its copy, no shared
package). Consolidation or archiving is pending owner decision D5 (BD-033), see
`repository-catalog/portfolio/MOBILE-CONSOLIDATION-2026-10.md` in solo-empire.

Turn a hex colour into a tint/shade palette and check WCAG contrast.

Part of [Chaowalit Greepoke](https://bookchaowalit.com)'s 101 Portfolio Projects.

## Features

- Parses #RGB and #RRGGBB hex colours
- Generates a 9-step tint/shade scale
- WCAG 2.x contrast ratio against white and black with AA/AAA ratings

Data lives in memory for the current session only; there is no account,
backend, analytics or network access.

## Tech Stack

- **Framework:** Flutter (CI pinned to 3.47.5) + Material 3
- **Language:** Dart
- **State:** `StatefulWidget` / `setState`; the core logic is pure Dart in
  `lib/logic/` and unit-tested without widgets

## Develop and verify

```bash
flutter pub get
dart format --output=none --set-exit-if-changed lib test
flutter analyze
flutter test
flutter run
```

CI (`.github/workflows/build.yml`) pins Flutter in the workflow `env`,
resolves dependencies with `flutter pub get --enforce-lockfile`, runs the same
format/analyze/test checks (all fail closed) plus the shared
`platform-ci-workflows` `security.yml` scan, and builds a debug APK on pushes
to `main`.

## Build

```bash
# Android
flutter build apk --debug
```

Release builds (`flutter build apk --release` / `appbundle`) fail on purpose
until signing is configured; they never fall back to the debug key. To sign,
create an upload keystore outside the repo and add the ignored
`android/key.properties`:

```properties
storePassword=...
keyPassword=...
keyAlias=upload
storeFile=/absolute/path/to/upload-keystore.jks
```

Never commit `key.properties` or keystores (both are git-ignored).

## Related

- **Frontend:** [bookchaowalit-website/design-frontend](https://github.com/bookchaowalit-website/design-frontend)
- **Portfolio:** [bookchaowalit.com](https://bookchaowalit.com)

## License

MIT
