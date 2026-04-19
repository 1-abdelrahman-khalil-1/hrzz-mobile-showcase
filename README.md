# HRZZ Mobile

## Overview

HRZZ Mobile is a professional development and management application designed for an organization with administrators and practitioners. The platform allows administrators to manage practitioners, oversee a knowledge center, and track performance through reports and statistics. Practitioners can use the app to submit reports, access educational content, take quizzes, and monitor their own progress.

## Demo

(Add your demo video here)
[Watch Demo](PUT_YOUR_VIDEO_LINK_HERE)

## Features

- **Dual User Roles:** Separate interfaces and functionalities for Administrators and Practitioners.
- **Administrator Features:**
  - Manage practitioner accounts.
  - Oversee a "Knowledge Center" with educational materials.
  - Generate and view comprehensive reports.
  - Monitor overall statistics and performance, visualized with charts.
- **Practitioner Features:**
  - Submit and track personal reports.
  - Access the Knowledge Center for learning.
  - Participate in quizzes to test their knowledge.
  - View personal statistics and performance data.
- **Authentication:** Secure login for both user roles.
- **Dashboard:** A personalized home screen for each user type.
- Supports both English and Arabic.

## Tech Stack

- **Framework:** Flutter
- **State Management:** Flutter Riverpod (with Riverpod Generator)
- **Routing:** Auto Route
- **API Client:** Dio
- **Charting:** fl_chart
- **UI:** persistent_bottom_nav_bar_v2

## Architecture

The project is built with a feature-driven architecture, separating the application's logic into `admin` and `practical` (practitioner) feature sets. A `common` directory likely holds shared widgets and logic between these roles. The use of Riverpod Generator streamlines state management, and Auto Route handles navigation, creating a robust and maintainable codebase.

## Folder Structure

```
lib/
├── app/
│   ├── core/
│   └── features/
│       ├── admin/
│       │   ├── home/
│       │   ├── knowledge_center/
│       │   ├── main/
│       │   ├── practitioners/
│       │   ├── reports/
│       │   └── statistics/
│       ├── common/
│       └── practical/
│           ├── add_report/
│           ├── home/
│           ├── knowledge_center/
│           ├── main/
│           ├── my_reports/
│           ├── quizzes/
│           └── statistics/
├── generated/
├── router/
├── hrzz_app.dart
└── main.dart
```

## How It Works

The application provides two distinct experiences based on user roles.

- **Administrators** log in to a dashboard where they can manage the platform's content and users. They can add or remove practitioners, upload materials to the knowledge center, and monitor the overall activity and performance through detailed reports and statistical charts.
- **Practitioners** log in to their personal dashboard. They can submit reports, browse the knowledge center for information, take quizzes, and track their own performance and progress over time.

## Dependencies

- `flutter_riverpod` & `riverpod_generator`: For state management.
- `auto_route`: For navigation and routing.
- `dio`: For making HTTP requests to the API.
- `fl_chart`: For displaying charts and graphs.
- `persistent_bottom_nav_bar_v2`: For the main navigation bar.

## Notes

- The application is well-structured, with a clear separation of concerns between different user roles.
- The use of code generation for state management (Riverpod Generator) and routing (Auto Route) helps to reduce boilerplate and improve developer productivity.
- The feature set suggests a focus on continuous professional development and performance tracking.
