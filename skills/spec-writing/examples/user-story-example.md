---
type: user-story
title: Quick Add Task from Dashboard
created: 2024-01-14
status: approved
sprint: 2024-Q1-S3
story_points: 5
---

# User Story: Quick Add Task from Dashboard

## Story

**As a** project team member,
**I want** to quickly add a task from the dashboard without navigating to a project,
**So that** I can capture ideas immediately without losing context of my current view.

## Background

Currently, adding a task requires: Dashboard → Project → Task List → New Task (4 clicks, page navigation). Users report losing their train of thought during this flow, especially when quickly capturing multiple ideas.

## Acceptance Criteria

### Primary Flow

**Scenario 1: Quick add with keyboard shortcut**
- Given I am on the dashboard
- And I press Cmd+K (Mac) or Ctrl+K (Windows)
- When the quick add modal appears
- Then focus is in the task title field
- And I can type immediately without clicking

**Scenario 2: Quick add with button**
- Given I am on the dashboard
- When I click the "+" button in the top navigation
- Then the quick add modal appears
- And focus is in the task title field

**Scenario 3: Minimal task creation**
- Given the quick add modal is open
- When I type "Review design specs" and press Enter
- Then the task is created in my default project
- And a toast notification confirms "Task created in [Project Name]"
- And the modal closes
- And I remain on the dashboard

**Scenario 4: Task with project selection**
- Given the quick add modal is open
- When I type "Review design specs"
- And I click the project dropdown
- Then I see my 5 most recent projects
- And a search field to find other projects
- When I select "Website Redesign"
- And press Enter
- Then the task is created in "Website Redesign"

### Additional Options

**Scenario 5: Setting due date**
- Given the quick add modal is open
- When I type "Review specs"
- And I click the calendar icon
- Then a date picker appears
- When I select tomorrow's date
- And press Enter
- Then the task is created with tomorrow's due date

**Scenario 6: Natural language due date**
- Given the quick add modal is open
- When I type "Review specs tomorrow"
- Then "tomorrow" is highlighted and parsed as due date
- When I press Enter
- Then the task is created with tomorrow's due date
- And the title is "Review specs" (without "tomorrow")

**Scenario 7: Assigning to self**
- Given the quick add modal is open
- When I type "Review specs"
- And I click "Assign to me"
- And press Enter
- Then the task is created assigned to me

### Error Handling

**Scenario 8: Empty title prevention**
- Given the quick add modal is open
- When I press Enter without typing a title
- Then the modal shakes briefly
- And the title field shows "Task title is required"
- And the modal remains open

**Scenario 9: No default project**
- Given I have no default project set
- And the quick add modal is open
- When I type a task title and press Enter
- Then the project dropdown highlights with "Select a project"
- And the task is not created until project is selected

**Scenario 10: Network error**
- Given the quick add modal is open
- And I have typed a valid task
- When I press Enter
- And the network request fails
- Then I see "Couldn't create task. Please try again."
- And a Retry button appears
- And my typed content is preserved

### Accessibility

**Scenario 11: Screen reader navigation**
- Given I am using a screen reader
- When the quick add modal opens
- Then the modal is announced as "Quick add task dialog"
- And focus is announced as "Task title, required, edit text"

**Scenario 12: Keyboard navigation**
- Given the quick add modal is open
- When I press Tab
- Then focus moves through: Title → Project → Due Date → Assign → Create button
- When I press Escape
- Then the modal closes without creating a task

### Dismissal

**Scenario 13: Cancel via Escape**
- Given the quick add modal is open
- And I have typed "Draft task"
- When I press Escape
- Then a confirmation appears "Discard this task?"
- When I click "Discard"
- Then the modal closes
- And no task is created

**Scenario 14: Cancel empty modal**
- Given the quick add modal is open
- And the title field is empty
- When I press Escape
- Then the modal closes immediately (no confirmation needed)

## UI/UX Notes

- Modal should be compact (400px max width)
- Modal appears centered, 100px from top
- Background dims but dashboard remains visible
- Animation: fade in 150ms
- Keyboard shortcut hint shown on "+" button hover

## Out of Scope

- Adding subtasks from quick add
- Bulk task creation
- Task templates
- File attachments
- Task description (just title for "quick" add)

## Dependencies

- Default project setting (exists in user preferences)
- Toast notification system (exists)
- Date parsing library (evaluate: chrono-node)

## Notes

- Analytics: Track quick add usage vs. standard add flow
- Consider: Recent tasks dropdown after creation for "undo"
