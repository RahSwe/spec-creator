---
type: bug-report
title: Search Results Pagination Resets on Back Navigation
created: 2024-01-12
status: confirmed
severity: medium
affected_users: all
---

# Bug Report: Search Results Pagination Resets on Back Navigation

## Environment

- **Application Version:** 2.4.1
- **Operating System:** macOS 14.2, Windows 11, Ubuntu 22.04 (confirmed on all)
- **Browser:** Chrome 120, Firefox 121, Safari 17 (confirmed on all)
- **User Role:** All authenticated users
- **Feature Area:** Search functionality

## Steps to Reproduce

1. Navigate to the search page at `/search`
2. Enter search query "project management" and press Enter
3. Wait for results to load (147 results displayed)
4. Click "Next" to navigate to page 2 of results
5. Click "Next" again to navigate to page 3 of results
6. Click on any search result to view the detail page
7. Click browser back button to return to search results

## Expected Behavior

- User returns to page 3 of search results
- The same results are displayed
- Scroll position is preserved or near the previously viewed result
- Search query "project management" remains in the search box

## Actual Behavior

- User returns to page 1 of search results
- Scroll position resets to top
- Search query is preserved (partial: this works correctly)
- User must click "Next" multiple times to return to their previous position
- For long result sets, this creates significant friction

## Impact Analysis

- **User Impact:** Users lose their place in search results, causing frustration and repeated navigation
- **Frequency:** Occurs 100% of the time on back navigation
- **Workaround:** Open search results in new tab (not discoverable)
- **Affected Users:** All users who paginate through search results

## Severity Justification

**Medium** - Feature is usable but creates significant friction for power users who frequently search and paginate. No data loss occurs.

## Technical Notes

### Root Cause (Suspected)

Pagination state is stored only in component state, not in URL or browser history. When navigating away and back, the component remounts with default state (page 1).

### Suggested Fix

Store pagination in URL query parameter:
- Current: `/search?q=project%20management`
- Fixed: `/search?q=project%20management&page=3`

This allows browser history to preserve pagination state automatically.

### Related Code

- Search page component: `src/pages/Search.tsx`
- Pagination component: `src/components/Pagination.tsx`
- Search results hook: `src/hooks/useSearchResults.ts`

## Additional Context

### Screenshot

[Before back navigation - Page 3]
```
Search: "project management"
Page 3 of 15 | Showing 21-30 of 147 results
```

[After back navigation - Reset to Page 1]
```
Search: "project management"
Page 1 of 15 | Showing 1-10 of 147 results
```

### Related Issues

- #1234 - Search filters also reset on back navigation (same root cause)
- #1156 - Sort order resets on back navigation (same root cause)

### User Complaints

- Support ticket #5678: "I keep losing my place in search results"
- Forum post: "Why does search pagination not work with back button?"

## Acceptance Criteria for Fix

- [ ] Given a user on page 3 of search results, when they click a result and press back, then they return to page 3
- [ ] Given the URL `/search?q=test&page=3`, when loaded directly, then page 3 of results displays
- [ ] Given a user changes the page parameter in URL manually, when page loads, then the specified page displays
- [ ] Given an invalid page number in URL (e.g., page=999), when loaded, then the last available page displays with appropriate message
- [ ] Given pagination is updated, when user shares URL, then recipient sees the same page
