# HRZZ Mobile

## 1. Hero Section

HRZZ Mobile is split into two operational views: administrator and practitioner. Administrators manage practitioners, reports, knowledge-center content, and statistics. Practitioners work inside their own dashboard to submit reports, study, take quizzes, and review progress.

## 2. Product / Workflow Overview

The app separates management workflows from practitioner workflows so each role gets a focused UI and its own navigation path.

- Admin flow covers practitioner management, reports, statistics, and knowledge-center operations.
- Practitioner flow covers report creation, learning content, quizzes, and personal progress tracking.
- The dashboard layer is role-aware and routes users to the correct main shell after authentication.
- Charts and summary views are used for operational reporting, not decorative analytics.
- Arabic and English localization is part of the shared app shell.

## 3. Engineering Highlights

- Feature organization is split into `admin`, `practical`, and `common`, which keeps shared code separate from role-specific screens.
- Riverpod providers are kept close to each feature, with `FutureProvider`, `StateNotifierProvider`, and `StateProvider` used where they fit the workflow.
- The project includes `riverpod_generator` in the toolchain, which supports a scalable provider pattern as the app grows.
- AutoRoute manages a single navigation graph with separate initial routes for onboarding, login, admin shell, and practitioner shell.
- Statistics, reports, and knowledge-center flows each keep their own providers and services instead of sharing one large controller.
- Localized transitions and RTL-aware routing keep the UI behavior aligned with the selected language.

## 4. Screenshots / Demo Placeholder

- Product walkthrough: ADD_VIDEO_OR_GIF_LINK
- App screenshots: ADD_SCREENSHOT_LINKS

## 5. Engineering Stack

- Flutter (Dart)
- Flutter Riverpod
- riverpod_generator
- AutoRoute
- Dio
- fl_chart
- persistent_bottom_nav_bar_v2
- SharedPreferences

## 6. Architecture Overview

1. `main.dart` and `HrzzApp` mount the router, translations, theme, and locale-aware material shell.
2. `AppRouter` decides the initial flow from `RoutingPrefs` and applies role-specific route groups.
3. Feature providers keep dashboard, statistics, reports, quizzes, and knowledge-center logic separate.
4. Shared services handle network access and backend interaction while screens stay presentation-focused.
5. Common widgets and theme helpers keep the admin and practitioner shells visually aligned.

## 7. Simplified Folder Structure

```text
lib/
  app/
    core/
    features/
      admin/
      common/
      practical/
  generated/
  router/
  hrzz_app.dart
  main.dart
```

## 8. System Architecture Diagram (ASCII)

```text
Presentation Layer
      |
      v
Riverpod Providers
      |
      v
Feature Services / Controllers
      |
      v
Core API Layer
      |
      v
HRZZ Backend
```

## 9. My Responsibilities / Scope

- Delivered the admin and practitioner workflow split.
- Structured provider state for dashboards, reports, quizzes, and statistics.
- Kept routing aligned with role-based entry and shell navigation.
- Maintained the shared knowledge-center and reporting patterns across features.
- Reused shared components so the two role experiences stay consistent.

## 10. Repository Notes

- This repository is maintained as a portfolio showcase.
- The README stays focused on implementation shape and operational workflow coverage.
