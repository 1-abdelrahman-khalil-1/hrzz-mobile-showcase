# Hrzz Mobile

A role-based Flutter healthcare application that streamlines incident reporting, practitioner education, and administrative operations.

## Demo

### Supervisor Experience

https://github.com/user-attachments/assets/a57ecc84-1cb3-4d4e-8e58-b01c81b0c404

### Practitioner (Doctor) Experience

https://github.com/user-attachments/assets/d1526b64-7a65-4373-9ef8-24b8c35c06cd

## Overview

Hrzz Mobile is a role-based healthcare application designed for practitioners and supervisors within hospital environments. It streamlines incident reporting, practitioner education, communication, and operational oversight through dedicated experiences tailored to each role.

The application delivers two distinct user experiences within a single codebase, dynamically adapting its interface and functionality based on the authenticated user's role.

## Features

### Authentication & Profiles
- **Bilingual Authentication**: OTP-based login using phone numbers and employee credentials.
- **Dynamic Localization**: Compile-time safe translations with full RTL/LTR layout transitions.
- **Role-Based Access Control**: Secure view segregation between field practitioners and administrative supervisors.

### Practitioner Operations
- **Incident Reporting**: Multi-step wizard with offline draft saving, duplicate detection, and validation.
- **Continuing Education**: Knowledge center, medical articles, and interactive quizzes with progress tracking.
- **Personal Analytics**: Dashboard tracking reporting trends and quiz scores.

### Administrative Oversight
- **Practitioner Management**: Profile monitoring and activation controls.
- **Incident Queue**: Triage, review, and action workflows (Accept, Reject, Request Completion).
- **Supervisor Dashboard**: Geolocation mapping of incidents and role-wide statistical charts.

## Tech Stack

| Category | Technology |
|---|---|
| **Framework** | Flutter, Dart |
| **State Management** | Riverpod |
| **Routing** | AutoRoute |
| **Networking** | Dio |
| **Localization** | Slang |
| **Storage** | SharedPreferences |
| **UI & Charts** | fl_chart |
| **Code Generation** | Build Runner, Riverpod Generator, AutoRoute Generator |

## Architecture

Hrzz Mobile employs a **Feature-First Modular Architecture** using the Repository Pattern, separating presentation, business logic, and network layers.

- **Architectural Style**: Feature-driven modules isolating `admin`, `practical`, and `common` logic.
- **Dependency Injection**: Riverpod manages dependency injection and application state through providers.
- **State Management**: Reactive UI updates using Riverpod's `FutureProvider` for asynchronous data fetching and `StateNotifier` for mutations. A custom `InternetErrorHandlerMixin` centralizes error catching.
- **Networking**: `DioClient` automatically handles token injection, localization headers, and centralizes error validation, redirecting unauthenticated users automatically.
- **Routing**: `AutoRoute` manages the declarative navigation graph with RTL-aware transition animations.

## Project Structure

```text
lib/
 ├── app/
 │    ├── core/               # Shared API helpers, utilities, and global styles
 │    └── features/
 │         ├── admin/         # Supervisor modules (queue, dashboards, user management)
 │         ├── common/        # Shared modules (auth, articles, chat, settings)
 │         └── practical/     # Practitioner modules (incident wizard, quizzes)
 ├── router/                  # AutoRoute configuration
 ├── hrzz_app.dart            # MaterialApp entry point
 └── main.dart                # Bootstrapping
```

## My Contributions

I developed the application's core modules, interface experiences, and integrations (excluding the add incident report feature):
- **Role-Based View Segregation**: Implemented the secure routing shell dividing supervisor and practitioner navigation stack environments.
- **Arabic-First RTL Optimization**: Configured customized transitions and reversed layouts tailored for native RTL readability.
- **Unified Error Handling**: Developed the `GeneralState` and `InternetErrorHandlerMixin` patterns to standardize network state and exception handling across features.


