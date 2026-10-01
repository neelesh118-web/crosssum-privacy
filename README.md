# CrossSum — Privacy Policy (the public page)

This repository exists for exactly one reason: **the public URL Google Play's listing asks for.**

It serves one page — <https://neelesh118-web.github.io/crosssum-privacy/> — which is the privacy policy
for **CrossSum — Math Crossword Puzzle** (`app.crosssum.game`).

## It is generated, not written here

The policy is **data in the app's own repository**, in `lib/store/disclosure.dart`, where
`test/store/disclosure_test.dart` holds it against the build: the ad SDK in `pubspec.yaml`, the
advertising-id permission the manifest declares, and the controls the game's own Privacy screen offers.
That is the point of publishing it this way — the page Google's reviewers open cannot drift from the
policy the app actually ships, because both are the same string.

**Do not edit `index.html`.** Regenerate it from the app's repository:

```
dart run tool/publish_policy.dart
cd privacy-site
git add index.html && git commit -m "Re-publish the privacy policy" && git push
```

## How the live page is checked

Three things hold this page to the app's own policy, so that "published" keeps meaning "the same
text":

- `test/store/disclosure_test.dart` compares `index.html` against today's rendering whenever this
directory is checked out beside the app's repository (`flutter test test/store/disclosure_test.dart`);
- `dart run tool/upload_check.dart` in the app's repository **fetches this address** and compares what is
  being served against what the app renders today — and refuses an upload while the two differ;
- the release runbook (`docs/07-RELEASE.md`, step 3) must still name this address, which a test asserts.

## What is served

One static page: no script, no tracker, no web font, no analytics, no cookies. A page whose subject is
privacy should make no network requests beyond itself, and this one makes none.

## Contact

Questions about the policy: the contact address at the bottom of the page itself.
