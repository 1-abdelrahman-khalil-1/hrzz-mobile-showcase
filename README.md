# Hrzz Mobile

A professional, role-based Flutter mobile health and hospital management application tailored for practitioners and supervisors, featuring dual-language (Arabic/English) support and Arabic-first Right-to-Left (RTL) optimization.

---

## What Is This Project?

**Hrzz Mobile** is designed to streamline communication and incident management within a healthcare/hospital environment. It divides operational workflows into two main role views:

*   **Practitioners**: Field users who require a focused mobile tool to report incidents, read medical articles, track personal progress, study via the knowledge center, and take educational quizzes.
*   **Supervisors (Admins)**: Administrative users who oversee practitioner accounts, monitor statistical dashboards, review incident reports, and decide on operational actions.

The application solves the problem of disconnected workflows between health practitioners and administrators by providing a unified, role-aware interface that handles data orchestration, reporting lifecycles, and continuing education.

---
---
## SuperVisor


https://github.com/user-attachments/assets/a57ecc84-1cb3-4d4e-8e58-b01c81b0c404


## Doctor


https://github.com/user-attachments/assets/d1526b64-7a65-4373-9ef8-24b8c35c06cd


---
## Features

### Shared Features (Common)
*   **Bilingual Authentication**: OTP (One-Time Password) validation using phone number and employee credentials.
*   **Dynamic Localization**: Dual-language support (Arabic & English) managed via compile-time safe translations, defaulting to an Arabic-first RTL layout.
*   **Knowledge Center & Articles**: Access to searchable medical directories, disease databases, and liking/sharing mechanisms.
*   **Interactive Chat**: Live conversational messaging with support or administrators.
*   **User Preferences**: Manage profile information, app language, and view legal agreements (Privacy Policy, Terms of Service).

### Practitioner Features (Practical)
*   **Incident Report Wizard**: A multi-step structured reporting workflow with automatic duplicate checking, validation, and offline draft saving.
*   **Quizzes & Continuing Education**: Multiple-choice testing interface with progress tracking, score calculations, and leaderboard points.
*   **Personalized Analytics**: Visual charts demonstrating report submission trends and quiz scores.

### Supervisor Features (Admin)
*   **Practitioner Management**: Detailed profile views, activation toggles, and practitioner assignment tracking.
*   **Incident Report Queue**: High-level incident listing, filtering by status (pending, open, closed), and dedicated detail inspection.
*   **Administrative Decisions**: One-click actions to accept, request completion, reject, or cancel incoming incident reports.
*   **Supervisor Dashboard**: Geolocation mapping of incident reports, statistical graphs, and role-wide data charts.

---

## My Contributions

As the Lead Developer of this project, I designed and implemented the entire core system architecture and features:
*   **Role-Based View Segregation**: Structured the application shell to split into separate `admin` and `practical` feature modules, ensuring a complete separation of presentation concern and secure navigation roots.
*   **Arabic-First RTL Optimization**: Configured custom transition animations and reversed design layouts to display correctly in native Arabic RTL directionality.
*   **Automated Scaffolding & Theme Utilities**: Created developer scripts (`make_screen.dart`, `generate_styles.dart`) to speed up modular feature creation and compile-time safe styling generation.
*   **Unified State and Error Handling**: Designed the `GeneralState` and `InternetErrorHandlerMixin` patterns to centralize network and error states across the app.

---

## Tech Stack

### Frontend
| Technology | Purpose |
| :--- | :--- |
| **Flutter / Dart SDK `^3.5.0`** | Cross-platform mobile framework |
| **Riverpod `^2.6.1`** | State management, caching, and dependency injection |
| **AutoRoute `^10.2.0`** | Declarative nested routing and language-aware transitions |
| **Slang Flutter `^4.9.0`** | Type-safe localization and translation compiler |
| **fl_chart `^0.68.0`** | Interactive statistical graphs and chart layouts |

### Database & Storage
| Technology | Purpose |
| :--- | :--- |
| **SharedPreferences `^2.3.0`** | Local key-value store for user credentials, app state, and user preferences |

### Tooling & Generators
| Tool | Usage |
| :--- | :--- |
| **Build Runner `^2.4.15`** | Orchestrates code generation for routing and state providers |
| **AutoRoute Generator `^10.0.1`** | Generates type-safe route representations |
| **Riverpod Generator `^2.6.5`** | Generates reactive state providers |
| **Slang Build Runner `^4.9.0`** | Automatically compiles JSON translations into Dart files |

---

## Architecture

Hrzz Mobile is built following a **Feature-First Clean Architecture** style, enforcing strict separation between business logic, network communication, and presentation.

```text
                               +-----------------------------+
                               |     Presentation Layer      |
                               | (Screens, Widgets, Shimmers) |
                               +--------------+--------------+
                                              | Watches
                                              v
                               +-----------------------------+
                               |   Riverpod Provider Layer   |
                               |  (Controllers, Notifiers)   |
                               +--------------+--------------+
                                              | Calls
                                              v
                               +-----------------------------+
                               |      Data/Service Layer     |
                               |   (DioClient, Mappers,      |
                               |    Models, Preferences)     |
                               +--------------+--------------+
                                              | Request
                                              v
                               +-----------------------------+
                               |         Backend API         |
                               +-----------------------------+
```

### Folder Organization
Each feature folder follows a standardized domain separation:
*   `data/models/`: Plain Dart classes, serialization factories (`fromJson`, `toJson`), and custom localized mappers.
*   `data/service/`: Repository classes consuming the networking clients.
*   `data/enums/`: Domain-specific enums with localized labels and color helpers.
*   `presentation/controller/`: Riverpod providers managing UI-related states.
*   `presentation/screens/`: Layout screens registered as auto-route pages (`@RoutePage`).
*   `presentation/widgets/`: Highly reusable, feature-specific UI elements.

### Architecture Highlights
*   **Dependency Injection**: Riverpod acts as the compile-time safe dependency injector, managing singletons for database helpers, API clients, and application services.
*   **Routing**: The application maintains a single navigation graph configured via `AutoRoute`. Transition animations are RTL-aware, shifting layouts from right-to-left for Arabic, and left-to-right for English.
*   **Networking**: Managed by a custom `DioClient` wrapper. It auto-injects auth tokens, language headers, and user-agent details.
*   **Error Handling**: All network calls pass through a centralized validation zone that translates HTTP errors and exceptions (such as `NoInternetConnection`, `UnAuthorized`, or `InternalServerError`) into uniform user-facing screens and notifications.

---

## Project Structure

The codebase is organized as follows:

```text
lib/
 ├── app/
 │    ├── core/                  # Core shared configurations & utilities
 │    │    ├── api_helper/        # HTTP client, endpoints, custom exception mappings
 │    │    ├── config/            # Static configuration settings
 │    │    ├── constants/         # Globally shared static constants
 │    │    ├── data/              # Storage wrappers (user, routing, language preferences)
 │    │    ├── enums/             # System-wide shared enumerations
 │    │    ├── extensions/        # Custom extension utilities (DateTime formatting, text styling)
 │    │    ├── mixins/            # Reusable business logic (InternetErrorHandlerMixin)
 │    │    ├── models/            # Core state wrappers (GeneralState)
 │    │    ├── screens_not_related/ # FutureProvider screen helper wrappers
 │    │    ├── services/          # Event bus and authorization status listeners
 │    │    ├── styles/            # CSS-like spacing and margin guidelines
 │    │    ├── themes/            # AppTheme layouts and AppColors palette
 │    │    ├── utils/             # Presentation helpers (Dialogs, BottomSheets, Snackbars)
 │    │    └── widgets/           # Global design system widgets (Buttons, Appbars, Inputs)
 │    └── features/
 │         ├── admin/             # Supervisor/Admin features
 │         │    ├── home/         # Banners, dashboard statistics
 │         │    ├── knowledge_center/ # Knowledge content management
 │         │    ├── main/          # Admin navigation shell & bottom bar
 │         │    ├── practitioners/ # Practitioner accounts management
 │         │    ├── reports/       # Incident review, approval & detail inspections
 │         │    └── statistics/    # Supervisor charts and map displays
 │         ├── common/            # Shared features accessible by all roles
 │         │    ├── app_info/      # App details and feedback messages
 │         │    ├── articles/      # Read & like medical articles
 │         │    ├── auth/          # Phone & employee ID login with OTP verification
 │         │    ├── chat/          # Support conversations
 │         │    ├── disease/       # Disease reference directory
 │         │    ├── disease_types/ # Disease category lists
 │         │    ├── locations/     # District/city/country API lists
 │         │    ├── notifications/ # User notifications
 │         │    ├── onBoarding/    # Initial walkthrough slides
 │         │    └── settings/      # Locale toggles and profile details editing
 │         └── practical/          # Practitioner features
 │              ├── add_report/    # Multi-step incident report wizard
 │              ├── home/          # Banners, statistics, articles feed
 │              ├── knowledge_center/ # Educational search and resource pages
 │              ├── main/          # Practitioner navigation shell & bottom bar
 │              ├── my_reports/    # Personal reports listing and draft saver
 │              ├── quizzes/       # Educational questions, answers, and scoring
 │              └── statistics/    # Personal reporting trends & scores charts
 ├── generated/                   # Generated slang, assets, and style atom files
 ├── router/                      # Routing setup and build_runner outputs
 ├── hrzz_app.dart                # Main MaterialApp.router setup
 └── main.dart                    # Application entry point & bootstrapping
```

---

## Design Decisions

*   **Role-Aware Shell Switching**: The separation of `admin` and `practical` directories ensures that features unique to a role remain isolated. When authentication resolves, the routing preferences dynamically determine the entry page, preventing access leaks between views.
*   **Separation of Concerns via Repository/Service Pattern**: Presentation files never make direct HTTP calls. They execute actions through services, which return strongly-typed models, making testing and backend changes painless.
*   **RTL Row Reversal**: In LTR designs, Row items like `[Icon] [Label]` are coded in that order. Because Flutter adapts layout directionality automatically, ordering items normally in code makes them render backward in Arabic. To maintain correct RTL flow, Row layouts are reversed in code, placing the primary text first and trailing action icons last.
*   **Stateless Widget Extraction**: To optimize rebuild trees, sub-widgets are extracted as separate `StatelessWidget` classes instead of helper methods, establishing clean repaint boundaries.

---

## Key Workflows

### 1. Authentication & Role-Based Routing
```text
[Login Screen] --> Enter Phone & Employee ID --> Send OTP --(API)--> [Otp Screen]
                                                                          |
                                                                      Enter OTP
                                                                          |
                                                                      Verify OTP
                                                                          |
                                                   Save user token, doctor info & role type (isSupervisor)
                                                                          |
                                                                   [Root App Router]
                                                                          |
                                                   +----------------------+----------------------+
                                                   | (isSupervisor = true)                       | (isSupervisor = false)
                                                   v                                             v
                                           [AdminMainRoute]                              [PracticalMainRoute]
                                          (Supervisor Shell)                            (Practitioner Shell)
```

### 2. Practitioner Incident Report Wizard
Practitioners submit reports using a clean, step-by-step reporting setup:
```text
[Type Screen] --> [Subtype Selection] --> [Form Screen] --> [Duplicate Alert (optional)] --> [Review Screen] --> [Success Screen]
```

### 3. Supervisor Incident Management
Supervisors review and take action on reports submitted by practitioners:
```text
[Supervisor Queue] --> Filter by Status --> Inspect Details --> [Accept / Reject / Request Completion / Cancel]
```

---

## Design System

The project incorporates a robust design system, ensuring visual consistency across both practitioner and admin views.

*   **Color Palette**: Defined in `AppColors`, focusing on teal primary (`#0F766E`), blue secondary (`#1080C0`), dark text main (`#12161C`), and functional success/danger/warning accents.
*   **Typography Atoms**: Generated inside `lib/generated/style_atoms.dart` from the definition file `generate_styles.dart`. Typography uses a chained syntax on BuildContext:
    *   `context.bold20Primary` (Bold text, 20px, primary teal color)
    *   `context.regular14TextSub` (Regular text, 14px, secondary gray color)
*   **Custom Widget Kit**:
    *   `CustomAppbar`: Automatically handles RTL back arrows and titles.
    *   `CustomButton` / `CustomButtonOutlined`: Standardized buttons with built-in loading states.
    *   `CustomTextFormField`: Styled inputs with custom validation states.
    *   `CustomCachedNetworkImage`: Binds network images with shimmer loaders and fallback icons.
    *   `CustomPagination`: Handles infinite scroll listing.

---

## API Integration

*   **Networking Client**: Built around `Dio`, the `DioClient` handles automatic header inclusion (User-Agent, Language preference, and Bearer Tokens) and handles JSON parsing.
*   **Centralized Error Interceptor**: Intercepts error responses. It fires an event bus message on `401 Unauthorized` status codes to log out users and automatically redirects to the no-internet view when connection loss is detected.
*   **Pagination Layer**: Powered by `riverpod_infinite_scroll` and `infinite_scroll_pagination`, fetching lists using paginated parameters (page and per-page limits).
*   **Exception Wrapper**: The `HandleErrorsResponse` utility parses error bodies to show helpful toast alerts or screen-level errors.

---

## State Management

State orchestration is managed via **Riverpod**:

*   **Asynchronous Queries (`FutureProvider`)**: Used to fetch read-only data. The screen watches the provider and renders UI using the `ref.watchWhen` extension, automatically handling loading, data, and error bounds:
    ```dart
    ref.watchWhen<List<DiseaseModel>>(
      provider: diseasesFutureProvider,
      loading: () => const DiseaseShimmer(),
      data: (diseases) => DiseaseList(diseases: diseases),
    )
    ```
*   **Centralized Multiple Fetching**: Screens needing multiple async endpoints combine them using `Future.wait` inside a single `FutureProvider` to avoid staggered layout shifts.
*   **Mutations (`StateNotifier`)**: Used to execute server requests. Controllers extend `StateNotifier<GeneralState<T>>` combined with the `InternetErrorHandlerMixin` to automatically catch errors and manage the loading state.
*   **Paginated Feeds (`PagedNotifier`)**: Extends infinite scroll lists to handle data append, retry states, and cache invalidation.

---

## Important Dependencies

*   **flutter_riverpod & riverpod_annotation**: Declares clean, scoped state controllers and handles dependency injection.
*   **auto_route & auto_route_generator**: Orchestrates nested navigation stacks and slide transitions.
*   **dio**: Handles network requests, payload transmission, and header configurations.
*   **slang_flutter & slang_build_runner**: Manages type-safe language localization.
*   **riverpod_infinite_scroll**: Integrates paginated lists with Riverpod notifiers.
*   **fl_chart**: Draws lightweight, interactive statistics and reports.
*   **cached_network_image**: Implements network image caching and performance improvements.

---

## Performance & Best Practices

*   **First-Load Full-Screen Shimmers**: Composite screens require a full-screen shimmer loader on their first fetch, displaying partial loaders only during filtering or sorting updates.
*   **Shimmer Layout Guidelines**: Shimmer indicators are built with `Column` layout components, avoiding viewport elements (`ListView` or `CustomScrollView`) to eliminate intrinsic layout calculation exceptions.
*   **Const Constructors**: Standardized on `const` layout wrappers and components wherever possible to reduce element rebuild costs.
*   **Controller Cleanups**: `TextEditingController`, `ScrollController`, and `TabController` states are disposed within the `dispose()` method of stateful widgets to prevent memory leaks.

---

## Future Improvements

*   **Offline Data Caching**: Implement local persistence using Isar or Hive to allow offline editing and submission of incident reports.
*   **Comprehensive Test Suite**: Introduce unit tests for service classes and widget/goldens tests for shared components.
*   **Dark Mode Support**: Extend `AppTheme` and `AppColors` to automatically support the device's dark mode setting.

