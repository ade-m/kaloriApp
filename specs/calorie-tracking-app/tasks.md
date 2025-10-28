# Tasks: Calorie Tracking App Core Features

**Input**: Design documents from `/specs/calorie-tracking-app/`
**Prerequisites**: plan.md, spec.md

**Organization**: Tasks are grouped by user story to enable independent implementation and testing of each story.

## Format: `[ID] [P?] [Story] Description`

- **[P]**: Can run in parallel (different files, no dependencies)
- **[Story]**: Which user story this task belongs to (e.g., US1, US2, US3)

---

## Phase 1: Setup (Shared Infrastructure)

**Purpose**: Project initialization and basic structure.

- [ ] T001 Create Laravel project in `backend/` directory.
- [ ] T002 Configure `.env` file for PostgreSQL database connection.
- [ ] T003 Install Filament, Spatie/laravel-permission, and other required dependencies via Composer.
- [ ] T004 [P] Configure linting and formatting tools (e.g., PHP CS Fixer).

---

## Phase 2: Foundational (Blocking Prerequisites)

**Purpose**: Core infrastructure that MUST be complete before ANY user story can be implemented.

- [ ] T005 Create database migrations for `users`, `foods`, `meals`, `food_items`, and `goals` tables in `backend/database/migrations/`.
- [ ] T006 Run initial database migrations to create all tables.
- [ ] T007 Create Eloquent models for `User`, `Food`, `Meal`, `FoodItem`, and `Goal` in `backend/app/Models/`.
- [ ] T008 Define the relationships (e.g., `belongsTo`, `hasMany`) within the Eloquent models.
- [ ] T009 Set up basic user authentication using Laravel Breeze or similar.

**Checkpoint**: Foundation ready - user story implementation can now begin.

---

## Phase 3: User Story 1 - Log a Meal (Priority: P1) 🎯 MVP

**Goal**: Allow users to log the meals they eat to track calorie intake.
**Independent Test**: A user can add a meal with food items and see it recorded for the current day.

### Implementation for User Story 1

- [ ] T010 [US1] Create `FoodResource` in `backend/app/Filament/Resources/` to manage the food database.
- [ ] T011 [US1] Implement the form in `FoodResource` to add/edit foods with their calorie information.
- [ ] T012 [US1] Create `MealResource` in `backend/app/Filament/Resources/`.
- [ ] T013 [US1] Implement the form in `MealResource` to log a meal, including a repeater field to add multiple `food_items`.
- [ ] T014 [US1] The `food_items` repeater should allow selecting a `Food` and specifying a `quantity`.
- [ ] T015 [US1] Ensure the `user_id` is automatically associated with the logged meal.

**Checkpoint**: User Story 1 is fully functional and testable independently.

---

## Phase 4: User Story 2 - View Daily Summary (Priority: P2)

**Goal**: Provide users with a summary of their total daily calorie intake.
**Independent Test**: A user can view a page that accurately sums the calories from all meals logged for the current day.

### Implementation for User Story 2

- [ ] T016 [US2] Create a custom Filament page or a widget on the dashboard to display the daily summary.
- [ ] T017 [US2] Implement the logic to fetch all meals for the logged-in user for the current day.
- [ ] T018 [US2] Calculate the total calorie intake by summing the calories of all `food_items` across the day's meals.
- [ ] T019 [US2] Display the total calories on the summary page/widget.

**Checkpoint**: User Stories 1 AND 2 both work.

---

## Phase 5: User Story 3 - Set a Personal Calorie Goal (Priority: P3)

**Goal**: Allow users to set a daily calorie goal to track against a target.
**Independent Test**: A user can set a daily goal, and it is displayed on their summary page.

### Implementation for User Story 3

- [ ] T020 [US3] Create `GoalResource` in `backend/app/Filament/Resources/`.
- [ ] T021 [US3] Implement a form in `GoalResource` for users to create or update their daily calorie goal.
- [ ] T022 [US3] Modify the daily summary page/widget to display the user's current calorie goal.
- [ ] T023 [US3] [P] Add a calculation to the summary to show "calories remaining" (Goal - Consumed).

**Checkpoint**: All user stories are now independently functional.

---

## Phase 6: Polish & Cross-Cutting Concerns

- [ ] T024 [P] Write feature tests for the core logic of each user story.
- [ ] T025 [P] Add basic database seeders for `foods` to provide initial data in `backend/database/seeders/`.
- [ ] T026 Review and refine the UI/UX of all Filament resources and pages.