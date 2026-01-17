# Acceptance Criteria Patterns

Comprehensive patterns for writing testable, specific acceptance criteria.

## Given-When-Then Format

The Given-When-Then format (Gherkin syntax) creates clear, testable scenarios.

### Basic Pattern

```
Given [precondition/context]
When [action/trigger]
Then [expected outcome]
```

### With Multiple Conditions

```
Given [precondition 1]
And [precondition 2]
When [action]
Then [outcome 1]
And [outcome 2]
```

### Examples by Category

#### Authentication

```
Given a user with valid credentials
When they enter their email and password and click "Sign In"
Then they are redirected to the dashboard
And their session is created with 24-hour expiration

Given a user with invalid password
When they attempt to sign in 5 times
Then their account is locked for 30 minutes
And they receive a "Too many attempts" error message
And a notification email is sent to their address

Given an authenticated user
When they click "Sign Out"
Then their session is invalidated
And they are redirected to the login page
And cached sensitive data is cleared from the browser
```

#### Data Validation

```
Given a user on the registration form
When they enter an email without @ symbol
Then the email field displays "Invalid email format"
And the Submit button remains disabled

Given a user creating a new project
When they enter a name longer than 100 characters
Then only the first 100 characters are accepted
And a character counter shows "100/100"

Given a user uploading a file
When the file size exceeds 10MB
Then the upload is rejected before transfer begins
And the message "File must be under 10MB" is displayed
```

#### Search and Filtering

```
Given a user on the product listing page
When they enter "blue shoes" in the search box
And press Enter
Then results show only products matching "blue" AND "shoes"
And results load within 2 seconds
And the result count is displayed above the list

Given search results are displayed
When the user clicks "Price: Low to High"
Then results are reordered by ascending price
And the sort indicator shows the active sort
And the URL updates to include sort parameter
```

#### Error Handling

```
Given a user submitting a form
When the server returns a 500 error
Then the form displays "Something went wrong. Please try again."
And the form data is preserved
And a "Retry" button is shown
And the error is logged with request ID

Given a user viewing a product page
When the product data fails to load
Then a skeleton loader is shown for 3 seconds
Then an error state is displayed with "Reload" option
And the header and navigation remain functional
```

#### Permissions

```
Given a user with "viewer" role
When they access the Settings page
Then they see settings in read-only mode
And edit buttons are hidden
And attempting direct URL to edit shows "Permission denied"

Given a user with "admin" role
When they view any user's profile
Then they see the "Edit User" and "Delete User" buttons
And they can modify user roles
And changes are logged in the audit trail
```

## Numeric and Performance Criteria

### Response Time

```
The search results API must:
- Return results within 200ms for 95th percentile
- Return results within 500ms for 99th percentile
- Support at least 100 concurrent searches
```

### Capacity

```
The file upload feature must:
- Accept files up to 50MB
- Support simultaneous uploads (max 3 per user)
- Process at least 1000 uploads per hour per server
```

### Availability

```
The authentication service must:
- Maintain 99.9% uptime monthly
- Failover to backup within 30 seconds
- Preserve active sessions during failover
```

## Edge Case Patterns

### Empty States

```
Given a new user with no data
When they view the dashboard
Then they see a welcome message with getting started steps
And sample data or demo mode option is offered

Given a search with no results
When results page loads
Then "No results found" message displays
And suggestions for broader search are shown
And recent searches are displayed if available
```

### Boundary Conditions

```
Given a shopping cart
When user adds the 100th item (maximum limit)
Then the item is added successfully
And "Cart full" message appears
And "Add to cart" buttons are disabled

Given a text field with 0 characters
When user clicks Submit
Then "This field is required" error shows
And field border turns red
And focus moves to the empty field
```

### Concurrent Operations

```
Given two users editing the same document
When User A saves their changes
Then User B sees a notification about conflicting changes
And User B can choose to merge, overwrite, or discard
And version history preserves both change sets

Given a user clicking "Submit" twice rapidly
Then only one submission is processed
And second click shows "Processing..." disabled state
And no duplicate records are created
```

### Timeout Scenarios

```
Given a long-running report generation
When processing exceeds 30 seconds
Then a progress indicator shows estimated time remaining
And user can choose to continue waiting or cancel
And if cancelled, partial results are available

Given an idle user session
When no activity for 15 minutes
Then a "Session expiring" warning appears at 14 minutes
And session extends if user interacts
And user is logged out at 15 minutes with data preserved
```

## Anti-Patterns to Avoid

### Too Vague

❌ Bad:
```
The system should handle errors gracefully
```

✅ Good:
```
Given any API returns a 4xx or 5xx error
When the error occurs during a user action
Then a user-friendly message is displayed (not technical details)
And the error is logged with request ID, timestamp, and stack trace
And the user can retry the action or navigate away
```

### Untestable

❌ Bad:
```
The interface should be intuitive
```

✅ Good:
```
Given a new user who has never used the application
When they attempt to create their first project
Then they can complete the task in under 3 clicks
And without consulting help documentation
And the success rate in usability testing exceeds 90%
```

### Ambiguous

❌ Bad:
```
Data should be saved automatically
```

✅ Good:
```
Given a user editing a document
When they make any change
Then the change is saved within 2 seconds
And a "Saved" indicator appears
And if offline, changes are queued and synced when online
And conflicting offline changes prompt user resolution
```

### Missing Context

❌ Bad:
```
Users can delete items
```

✅ Good:
```
Given a user with "owner" role viewing their item
When they click "Delete"
Then a confirmation modal appears with item name
And deletion requires typing "DELETE" to confirm
And deleted items move to trash for 30-day recovery
And users without owner role see no delete option
```

## Checklist for Acceptance Criteria

Before finalizing, verify each criterion:

- [ ] Is it specific enough to implement without questions?
- [ ] Is it testable with a pass/fail outcome?
- [ ] Does it include the preconditions (Given)?
- [ ] Does it specify the trigger (When)?
- [ ] Does it define the expected outcome (Then)?
- [ ] Are edge cases and error conditions covered?
- [ ] Are numeric thresholds explicit where applicable?
- [ ] Is the persona/role specified when relevant?
