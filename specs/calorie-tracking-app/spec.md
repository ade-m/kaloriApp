# Feature Specification: Calorie Tracking App Core Features

**Feature Branch**: `feat/calorie-tracking-app`  
**Created**: 2025-10-28  
**Status**: Draft  
**Input**: User description: "saya ingin membangun aplikasi track kalori dengan menggunakan laravel, filament, postgresSQL dan spatie"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Log a Meal (Priority: P1)

As a user, I want to log the meals I eat throughout the day so that I can track my calorie intake.

**Why this priority**: This is the absolute core functionality of the application. Without it, no other feature has value.

**Independent Test**: A user can successfully add a meal with at least one food item and see it recorded for the current day.

**Acceptance Scenarios**:

1. **Given** I am logged into my account, **When** I navigate to the "Log Meal" page and enter "Breakfast" with "Oatmeal" (150 calories), **Then** the meal is saved and my daily calorie total increases by 150.
2. **Given** I am logging a meal, **When** I do not enter a food item, **Then** I see an error message and the meal is not saved.

---

### User Story 2 - View Daily Summary (Priority: P2)

As a user, I want to see a summary of my total calorie intake for the day so that I can understand my progress.

**Why this priority**: This provides the essential feedback loop for the user, making the act of logging meals useful.

**Independent Test**: A user can view a page that accurately sums the calories from all meals logged for the current day.

**Acceptance Scenarios**:

1. **Given** I have logged "Breakfast" (300 calories) and "Lunch" (500 calories) for today, **When** I view my daily summary, **Then** I see a total calorie intake of 800.
2. **Given** I have not logged any meals for today, **When** I view my daily summary, **Then** I see a total calorie intake of 0.

---

### User Story 3 - Set a Personal Calorie Goal (Priority: P3)

As a user, I want to set a daily calorie goal so that I can track my intake against a specific target.

**Why this priority**: This introduces personalization and gives the user a clear target to aim for, increasing engagement.

**Independent Test**: A user can set a daily calorie goal, and this goal is displayed on their daily summary page.

**Acceptance Scenarios**:

1. **Given** I am on my profile page, **When** I set my daily calorie goal to 2000, **Then** my daily summary page shows a target of 2000 calories.
2. **Given** I have a daily goal of 2000 calories and have consumed 800 calories, **When** I view my summary, **Then** I see that I have 1200 calories remaining.

---

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST allow users to register and log in.
- **FR-002**: System MUST allow users to log meals with multiple food items and quantities.
- **FR-003**: System MUST calculate and display the total calorie intake for the current day.
- **FR-004**: Users MUST be able to set and update their daily calorie goal.
- **FR-005**: System MUST persist all user data (meals, goals, foods) in the PostgreSQL database.

### Key Entities

- **User**: Represents an individual using the app. Attributes: name, email, password.
- **Meal**: Represents a specific eating occasion (e.g., Breakfast). Attributes: name, consumed_at. Belongs to a User.
- **Food**: Represents an item in the food database. Attributes: name, calories, protein, carbs, fat.
- **FoodItem**: A pivot entity linking a Meal to a Food, with a specific quantity.
- **Goal**: Represents a user's daily calorie target. Attributes: target_calories, date. Belongs to a User.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: A user can log a meal with three food items in under 60 seconds.
- **SC-002**: The daily summary page must load in under 2 seconds.
- **SC-003**: 95% of users successfully log their first meal without assistance.