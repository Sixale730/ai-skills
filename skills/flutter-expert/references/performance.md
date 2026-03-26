# Performance Optimization

## Profiling: flutter run --profile, flutter analyze, DevTools
## Const widgets prevent rebuilds
## Selective provider watching with .select()
## RepaintBoundary for expensive widgets
## compute() for heavy operations in isolates
## Image optimization: cacheWidth/cacheHeight, cached_network_image

| Check | Solution |
|-------|----------|
| Unnecessary rebuilds | const, select() |
| Large lists | ListView.builder |
| Heavy computation | compute() |
| Jank | RepaintBoundary |
| Memory leaks | Dispose controllers |
