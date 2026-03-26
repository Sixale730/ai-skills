# Bloc State Management

Use Bloc/Cubit for explicit event-to-state transitions, complex business logic, and predictable flows.

## Core: Event -> State -> Bloc

```dart
sealed class CounterEvent {}
final class CounterIncremented extends CounterEvent {}

class CounterBloc extends Bloc<CounterEvent, int> {
  CounterBloc() : super(0) {
    on<CounterIncremented>((event, emit) => emit(state + 1));
  }
}
```

## Widgets: BlocBuilder, BlocListener, BlocConsumer
## Testing: blocTest<Bloc, State>()
## Best Practices: Immutable states, small focused blocs, one feature = one bloc
