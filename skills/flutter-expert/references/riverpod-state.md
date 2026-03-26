# Riverpod State Management

## Provider Types

```dart
import 'package:flutter_riverpod/flutter_riverpod.dart';

final counterProvider = StateProvider<int>((ref) => 0);
final usersProvider = FutureProvider<List<User>>((ref) async {
  final api = ref.read(apiProvider);
  return api.getUsers();
});
final messagesProvider = StreamProvider<List<Message>>((ref) {
  return ref.read(chatServiceProvider).messagesStream;
});
```

## Notifier Pattern (Riverpod 2.0)

```dart
@riverpod
class TodoList extends _$TodoList {
  @override
  List<Todo> build() => [];

  void add(Todo todo) { state = [...state, todo]; }
  void toggle(String id) {
    state = [
      for (final todo in state)
        if (todo.id == id) todo.copyWith(completed: !todo.completed) else todo,
    ];
  }
  void remove(String id) { state = state.where((t) => t.id != id).toList(); }
}
```

## Usage in Widgets

```dart
class TodoScreen extends ConsumerWidget {
  const TodoScreen({super.key});
  @override
  Widget build(BuildContext context, WidgetRef ref) {
    final todos = ref.watch(todoListProvider);
    return ListView.builder(
      itemCount: todos.length,
      itemBuilder: (context, index) {
        final todo = todos[index];
        return ListTile(
          title: Text(todo.title),
          leading: Checkbox(
            value: todo.completed,
            onChanged: (_) => ref.read(todoListProvider.notifier).toggle(todo.id),
          ),
        );
      },
    );
  }
}
```

## Quick Reference

| Provider | Use Case |
|----------|----------|
| `Provider` | Computed/derived values |
| `StateProvider` | Simple mutable state |
| `FutureProvider` | Async operations (one-time) |
| `StreamProvider` | Real-time data streams |
| `NotifierProvider` | Complex state with methods |
| `AsyncNotifierProvider` | Async state with methods |
