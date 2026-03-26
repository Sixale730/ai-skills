# Project Structure

Feature-based structure: lib/features/{feature}/data|domain|presentation|providers/
Shared: lib/shared/widgets|services|models/
Routing: lib/routes/app_router.dart
Core: lib/core/constants|theme|utils|errors/

| Layer | Responsibility |
|-------|----------------|
| data/ | API calls, local storage, DTOs |
| domain/ | Business logic, entities, use cases |
| presentation/ | UI screens, widgets |
| providers/ | State management providers |
