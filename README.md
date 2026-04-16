# Movie Explorer — Cross-Platform Project

A cross-platform mobile application built with .NET MAUI that enables users to browse, search, and manage their favourite movies in a seamless and responsive interface. The application is designed to run natively on both Android and iOS from a single shared codebase, demonstrating modern mobile development practices.

The project combines clean UI design with practical features such as authentication, persistent storage, theming, and real-time updates, making it a complete end-to-end mobile application.

---

## Project Overview

Movie Explorer is designed to simulate a real-world mobile application where users can:

Create and manage accounts securely
Browse a dynamically loaded movie catalogue
Search and filter content efficiently
Save and manage personal favourites
Track activity through a history log
Customise the app experience through settings

The application emphasises usability, responsiveness, and maintainability, with a structured architecture separating UI, models, and services.

## Pages Overview

| Page | File | Description |
|---|---|---|
| Login | `LoginPage` | User login with username and password validation |
| Sign Up | `SignupPage` | Create a new account with password confirmation |
| Home | `MainPage` | Browse, search, and sort the full movie list |
| Movie Details | `MovieDetailPage` | View details for a selected movie and add to favourites |
| Favourites | `FavouritesPage` | View and remove saved favourite movies |
| History | `HistoryPage` | View a timestamped log of viewed and favourited movies |
| Settings | `SettingsPage` | Toggle dark mode, clock visibility, view history, and log out |

---

## Features

- **User Authentication** — Users can register and log in using a username and password.
    Passwords must meet a minimum length requirement of 8 characters.
    Credentials are stored locally using a custom UserStore.
    Session persistence is handled using the Preferences API.
    Automatic redirection ensures unauthenticated users cannot access protected pages.

- **Movie Browsing** — Movie data is retrieved from a remote JSON source.
Data is cached locally after the first successful fetch.
Offline functionality is supported after initial load.
Movie entries include title, genre, year, director, rating, and emoji representation.
- **Search** — Real-time filtering of the movie list.
Supports searching by title or genre.
Case-insensitive matching for improved usability.
Updates dynamically as the user types.
- **Sorting** — Toggle between ascending (A–Z) and descending (Z–A) order.
Sorting is applied instantly to the displayed movie list.
Designed for intuitive user interaction via a single button.
- **Favourites** — Movies can be added to favourites from the detail page.
Favourites are stored persistently on the device.
Users can remove individual items or clear all favourites.
Accessible quickly via the navigation bar.
- **History** — Logs key user actions such as viewing or favouriting movies.
Each entry includes a timestamp.
Provides a chronological overview of user activity.
Users can clear history at any time
- **Dark / Light Mode** — Supports both light and dark modes.
Themes are applied globally across all pages.
Changes take effect immediately without restarting the app.
Preferences are saved and restored on launch.
- **Live Clock** — Displays a real-time digital clock in HH:mm:ss format.
Updates every second.
Can be toggled on or off via Settings.
- **Fade-In Animations** — Smooth fade-in transitions on page load.
Uses FadeTo with CubicInOut easing for a polished experience.
Enhances perceived performance and UI fluidity.
- **Bottom Navigation Bar** — Persistent bottom navigation bar across all main pages.
Quick access to Home, Favourites, and Settings.
Active page button is disabled to improve UX clarity.
- **Persistent Settings** — User preferences are stored in a JSON file locally.
Includes theme selection, clock visibility, and other options.
Loaded automatically on app startup.

---

## Getting Started

### Prerequisites

- [.NET 8 SDK](https://dotnet.microsoft.com/download)
- [Visual Studio 2022](https://visualstudio.microsoft.com/) with the **.NET MAUI** workload installed
- Android Emulator or physical Android/iOS device

### Installation

1. Clone the repository:
```bash
git clone https://github.com/DanielNelga/Movie-Explorer-CrossPlatform-Project.git
cd Movie-Explorer-CrossPlatform-Project
```

2. Open the solution in Visual Studio 2022.

3. Select your target platform (Android / iOS) and run the project.

> **Note:** On first launch, the app will download the movie data from GitHub. An internet connection is required for the first load. After that, movies are served from local cache.

---

## File Structure

```
📦 CrossPlatformProject
 ┣ 📄 App.xaml / App.xaml.cs           # App entry point, theme management
 ┣ 📄 AppShell.xaml / AppShell.xaml.cs # Shell navigation and route registration
 ┣ 📄 MauiProgram.cs                   # App builder and service registration
 ┣ 📄 MainPage.xaml / .cs              # Home page — movie list, search, sort
 ┣ 📄 MovieDetailPage.xaml / .cs       # Movie detail view, add to favourites
 ┣ 📄 FavouritesPage.xaml / .cs        # Favourites list and remove functionality
 ┣ 📄 HistoryPage.xaml / .cs           # Browsing/favouriting history log
 ┣ 📄 SettingsPage.xaml / .cs          # Dark mode, clock, logout, clear favourites
 ┣ 📄 LoginPage.xaml / .cs             # Login with credential validation
 ┣ 📄 SignupPage.xaml / .cs            # Account creation with password rules
 ┣ 📄 Movie.cs                         # Movie model with JSON property mapping
 ┣ 📄 SettingsList.cs                  # Settings model (DarkMode, ShowClock, etc.)
 ┣ 📄 ManageSettings.cs                # Save/load settings to/from JSON file
 ┗ 📁 Services
    ┣ 📄 AuthService.cs                # Authentication service
    ┣ 📄 UserStore.cs                  # User account creation and login validation
    ┣ 📄 FavouritesStore.cs            # Persistent favourites storage
    ┗ 📄 HistoryStore.cs               # Persistent history log storage
```

---

## Theme & Styling

The app uses two custom colour themes applied dynamically at runtime:

| Token | Light Mode | Dark Mode |
|---|---|---|
| `BgColor` | `#E6D3A3` (Champagne) | `#0F172A` (Navy) |
| `SubTextColor` | `#0F172A` (Navy) | `#E6D3A3` (Champagne) |
| `ButtonBg` | `#0F172A` (Navy) | `#E6D3A3` (Champagne) |
| `ButtonText` | Navy | Black |

Themes are toggled via the `ApplyTheme(bool dark)` method in `App.xaml.cs` and persisted between sessions.

---

## Movie Data

Movies are loaded from a remote JSON file:

```
https://raw.githubusercontent.com/DonH-ITS/jsonfiles/refs/heads/main/moviesemoji.json
```

Each movie object contains: `title`, `genre` (list), `year`, `director`, `rating`, and `emoji`. On first load the file is downloaded and cached locally. Subsequent launches read from cache, enabling offline use.

---

## Authentication

- Users register with a username and a password of at least 8 characters.
- Passwords must match the confirmation field on sign-up.
- Credentials are validated locally via `UserStore`.
- The logged-in user is stored using `Preferences`. On app start, if no session is found, the user is redirected to the Login page.
- Logging out clears the stored session and navigates back to Login.

---

## Technologies Used

- **.NET MAUI** — Cross-platform UI framework
- **C#** — Application logic
- **XAML** — UI layout and styling
- **System.Text.Json** — JSON serialisation/deserialisation
- **Shell Navigation** — Route-based navigation between pages
- **Preferences API** — Session/login persistence
- **FileSystem API** — Local JSON caching for movies and settings

---

## Developer

| Name | Student ID |
|---|---|
| Daniel Nelga | G00464658@atu.ie |

---

##  License

This project was built for educational purposes as part of a college module at ATU (Atlantic Technological University).
