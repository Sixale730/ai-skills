# GoRouter Navigation

## Basic Setup

```dart
final goRouter = GoRouter(
  initialLocation: '/',
  redirect: (context, state) { /* auth check */ },
  routes: [
    GoRoute(path: '/', builder: (_, __) => const HomeScreen()),
    GoRoute(path: '/details/:id', builder: (_, state) => DetailsScreen(id: state.pathParameters['id']!)),
  ],
);
```

## Navigation: context.go(), context.push(), context.pop()
## Shell Routes for persistent bottom nav
## Query Parameters via state.uri.queryParameters
