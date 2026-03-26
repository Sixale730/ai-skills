---
name: "flutter-theming-apps"
description: "Customizes the visual appearance of a Flutter app using the theming system. Use when defining global styles, colors, or typography for an application."
---
# Implementing Flutter Theming and Adaptive Design

Material 3 is default since Flutter 3.16. Use `ColorScheme.fromSeed()` for colors. Use `*ThemeData` suffix classes (e.g., `CardThemeData`). Replace legacy buttons (`FlatButton` -> `TextButton`). Replace `BottomNavigationBar` with `NavigationBar`. Respect platform idioms for scrollbars, text selection, and button order.
