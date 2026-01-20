# Common Specification Problems

Frequent issues found in specifications and how to fix them.

## Problem Categories

### 1. Vague Requirements

**Symptoms:**
- Words like "should", "may", "might", "could"
- Subjective terms: "user-friendly", "fast", "easy"
- No specific numbers or thresholds
- Ambiguous pronouns ("it", "they", "the system")

**Examples and Fixes:**

| Problem | Fix |
|---------|-----|
| "The page should load quickly" | "The page fully renders within 2 seconds on 3G connection" |
| "Users should have a good experience" | "Users can complete checkout in 5 steps or fewer" |
| "The system may send notifications" | "The system sends email notification within 1 minute of event" |
| "It should handle errors" | "The upload form displays specific error messages for: file too large (>10MB), wrong format (not PNG/JPG), and upload failure" |

### 2. Incomplete Scope

**Symptoms:**
- No "Out of Scope" section
- Missing edge cases
- No error handling requirements
- Unclear boundaries with related features

**Common Missing Elements:**

**User States:**
- New users (empty state)
- Power users (high volume)
- Returning users (existing data)
- Users with accessibility needs

**System States:**
- Offline mode
- Slow network
- Server errors
- Maintenance mode

**Data States:**
- Empty/null values
- Maximum limits reached
- Invalid/corrupted data
- Concurrent modifications

### 3. Untestable Criteria

**Symptoms:**
- No pass/fail determination possible
- Requires subjective judgment
- Missing preconditions
- Missing expected outcomes

**Transform Untestable to Testable:**

| Untestable | Testable |
|------------|----------|
| "Intuitive navigation" | "New users find the Settings page within 30 seconds in usability testing" |
| "Secure authentication" | "Passwords are hashed with bcrypt (cost factor 12), sessions expire after 24 hours, failed logins are rate-limited to 5 per minute" |
| "Responsive design" | "Layout adapts correctly at breakpoints: 320px, 768px, 1024px, 1440px" |
| "Graceful degradation" | "If JavaScript is disabled: forms still submit, content is readable, navigation works" |

### 4. Missing Assumptions

**Symptoms:**
- Spec assumes knowledge not stated
- Technical constraints not mentioned
- Business rules implied but not documented

**Common Unstated Assumptions:**

**Technical:**
- Browser support requirements
- Device compatibility
- Network conditions
- API availability
- Data format expectations

**Business:**
- User authentication required
- Billing or subscription state
- Regional availability
- Feature flag dependencies
- Role-based access

**Fix:** Add explicit "Assumptions" section:
```markdown
## Assumptions
- Users are authenticated before accessing this feature
- API response times are under 500ms
- Users have JavaScript enabled
- Feature is available to Pro tier and above
```

### 5. Scope Creep Indicators

**Symptoms:**
- "While we're at it" additions
- Requirements unrelated to stated problem
- Gold-plating (unnecessary enhancements)
- Conflicting priorities

**Red Flags:**
- "It would be nice if..."
- "We should also..."
- "This is a good opportunity to..."
- "Users might want..."

**Fix:** Strict scope boundaries:
```markdown
## In Scope
- User can upload profile photo
- Photo is cropped to square
- Photo is resized to 200x200

## Out of Scope (Future Consideration)
- Photo filters
- Multiple profile photos
- GIF support
- Social media import
```

### 6. Missing Non-Functional Requirements

**Symptoms:**
- Only functional requirements listed
- No performance targets
- No security requirements
- No accessibility requirements

**Essential Non-Functional Categories:**

**Performance:**
```markdown
- Page load: < 3 seconds on 3G
- API response: < 200ms p95
- Database queries: < 100ms
```

**Security:**
```markdown
- All data encrypted in transit (TLS 1.3)
- PII encrypted at rest (AES-256)
- Session tokens rotate every 24 hours
```

**Accessibility:**
```markdown
- WCAG 2.1 AA compliance
- Keyboard navigable
- Screen reader compatible
```

**Reliability:**
```markdown
- 99.9% uptime target
- Automatic failover within 30 seconds
- Data backup every 6 hours
```

### 7. Inconsistent Terminology

**Symptoms:**
- Same concept called different names
- Acronyms used without definition
- Technical jargon mixed with business terms

**Examples:**
- "User" vs "Customer" vs "Account" (which is it?)
- "Delete" vs "Remove" vs "Archive" (different meanings?)
- "Project" vs "Workspace" vs "Team" (relationships unclear)

**Fix:** Add glossary:
```markdown
## Glossary
- **User**: An individual with login credentials
- **Account**: A billing entity (may contain multiple users)
- **Workspace**: A collaborative space within an account
- **Delete**: Permanent removal (cannot be undone)
- **Archive**: Soft removal (can be restored)
```

### 8. Missing User Context

**Symptoms:**
- No personas defined
- Unclear who performs actions
- Mixed user types without distinction
- No user journey

**Fix:** Define personas and their needs:
```markdown
## Personas

### Admin User
- Full access to all settings
- Can manage other users
- Responsible for billing
- Uses feature: Weekly

### Regular User
- Limited to own content
- Cannot access admin features
- Primary daily user
- Uses feature: Daily

### Guest User
- Read-only access
- No account required
- Cannot save preferences
- Uses feature: Occasionally
```

### 9. Poor Acceptance Criteria

**Symptoms:**
- Missing criteria entirely
- Copy of requirements (not testable scenarios)
- Too broad (one criterion covers too much)
- Missing error cases

**Transform Poor to Good:**

| Poor | Good |
|------|------|
| "User can upload files" | "Given a user on the upload page, when they select a PNG file under 5MB and click Upload, then the file appears in their library within 5 seconds with a success message" |
| "Search works" | "Given search results exist, when user types 3+ characters, then matching results appear within 500ms, limited to 10 items, sorted by relevance" |
| "Errors are handled" | "Given server returns 500, when user submits form, then 'Unable to save. Please try again.' appears, form data is preserved, and Retry button is shown" |

### 10. Dependency Blindness

**Symptoms:**
- No dependencies listed
- Circular dependencies not identified
- External service dependencies assumed
- Team dependencies not considered

**Fix:** Explicit dependency mapping:
```markdown
## Dependencies

### Technical
- Authentication service (existing)
- Email service (new integration required)
- CDN for image hosting (existing)

### Team
- Design: Mockups needed by [date]
- Backend: API endpoint required
- Security: Review before launch

### External
- Stripe API for payments
- SendGrid for emails
- AWS S3 for storage

### Blockers
- Cannot proceed until auth service supports SSO
- Waiting on legal approval for data handling
```

## Self-Review Checklist

Before submitting a specification, verify:

### Clarity
- [ ] No vague words (should, may, might, could)
- [ ] All terms defined consistently
- [ ] Specific numbers where applicable
- [ ] Clear subject in each requirement

### Completeness
- [ ] Happy path covered
- [ ] Error cases covered
- [ ] Edge cases covered
- [ ] Out of scope explicitly listed

### Testability
- [ ] Each acceptance criterion has pass/fail outcome
- [ ] Preconditions stated (Given)
- [ ] Actions specified (When)
- [ ] Expected outcomes defined (Then)

### Context
- [ ] Personas identified
- [ ] Assumptions documented
- [ ] Dependencies listed
- [ ] Glossary for specialized terms

### Technical
- [ ] Performance requirements included
- [ ] Security requirements included
- [ ] Accessibility requirements included
- [ ] Integration points identified
