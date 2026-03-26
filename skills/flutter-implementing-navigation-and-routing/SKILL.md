---
name: "flutter-implementing-navigation-and-routing"
description: "Handles routing, navigation, and deep linking in a Flutter application. Use when moving between screens or setting up URL-based navigation."
---
# Implementing Navigation and Routing in Flutter

Use `Navigator` (imperative) for simple apps, `Router`/`go_router` (declarative) for deep linking and web. Pass data via constructors. Return data via `Navigator.pop(context, result)`. Use nested `Navigator` for sub-flows with `GlobalKey<NavigatorState>`. Avoid named routes.
