# Error States & Edge Cases

Comprehensive guide to designing error handling, identifying edge case scenarios, and creating recovery flows that maintain user trust and task completion.

---

## Error State Classification

Not all errors are equal. Classify errors to determine appropriate handling strategies.

### Error Taxonomy

| Error Type | Description | User Impact | Example |
|-----------|------------|------------|--------|
| **Validation error** | User input doesn't meet requirements | Low — immediate feedback, easy fix | Invalid email format, password too short |
| **System error** | Backend failure, timeout, or crash | High — user cannot proceed | 500 server error, database timeout |
| **Permission error** | User lacks authorization for action | Medium — blocked but can find alternative | Trying to edit without write access |
| **Not found error** | Requested resource doesn't exist | Medium — user disoriented | 404 page, deleted item, broken link |
| **Connectivity error** | Network failure or offline state | High — all actions blocked | No internet, API unreachable |
| **Rate limit error** | Too many requests in short period | Medium — temporary block | API throttling, login attempt limits |
| **Data conflict error** | Concurrent edits or stale data | Medium — potential data loss | Two users editing same item simultaneously |
| **Business logic error** | Action violates business rules | Medium — user confused about why | Insufficient funds, expired subscription, exceeded quota |
| **Destructive action error** | User about to do something irreversible | Critical — potential data loss | Deleting account, removing team member, purging data |

### Error Severity Matrix

| Severity | Criteria | Design Response | Recovery Expectation |
|----------|---------|----------------|---------------------|
| **Critical** | User loses data or cannot complete core task | Full-screen error with clear recovery; auto-save if possible | Must provide specific next steps |
| **Major** | User is significantly blocked or frustrated | Inline error with detailed explanation and action | Provide alternative path or workaround |
| **Minor** | User is slightly inconvenienced | Subtle inline feedback with fix guidance | Self-correctable within seconds |
| **Info** | Not an error but unusual state | Informational message or banner | No recovery needed |

---

## Error Message Design

### Anatomy of a Good Error Message

Every error message should answer three questions:

1. **What happened?** — Describe the problem in plain language
2. **Why did it happen?** — Provide context (if helpful and not too technical)
3. **What can the user do?** — Give a specific action to recover

### Error Message Patterns

| Pattern | Structure | Example |
|---------|----------|--------|
| **Statement + Action** | "[Problem]. [What to do]." | "Your session has expired. Please log in again." |
| **Reason + Fix** | "[Why it failed] because [reason]. [Fix]." | "We couldn't save your changes because the file is too large. Try reducing the image size to under 5MB." |
| **Apologetic + Action** | "Sorry, [problem]. [What to do]." | "Sorry, we couldn't process your payment. Please check your card details and try again." |
| **Specific + Alternative** | "[Problem]. You can [option A] or [option B]." | "This feature requires a Pro plan. You can upgrade now or try the free alternative." |

### Error Message Anti-Patterns

| Bad Practice | Why It's Bad | Better Approach |
|-------------|-------------|----------------|
| "An error occurred" | No information; user doesn't know what to do | Describe the specific problem |
| "Error Code: 0x8004005" | Technical jargon; meaningless to users | Translate to plain language |
| "Invalid input" | Doesn't say what's wrong or how to fix it | "Email must include @ symbol" |
| "Something went wrong" | Vague; doesn't help with recovery | "We couldn't load your projects. Please refresh the page." |
| Blaming the user: "You entered wrong data" | Feels hostile; erodes trust | "The phone number format should be (555) 123-4567" |
| Long technical explanation | Users don't read walls of text | One sentence problem + one sentence fix |
| No action provided | User is stuck with no next step | Always include a button or link for recovery |

### Error Message Tone Guide

| Tone | When to Use | Example |
|------|-----------|--------|
| **Neutral / matter-of-fact** | Validation errors, expected issues | "Password must be at least 8 characters." |
| **Empathetic** | System failures that block the user | "We know this is frustrating. Our team is working to fix the issue." |
| **Reassuring** | Data-related errors where users fear loss | "Don't worry — your work was auto-saved 2 minutes ago." |
| **Encouraging** | User gives up or reaches dead end | "Almost there! Just one more step to complete setup." |
| **Avoid: Humorous** | Critical errors, data loss, payment issues | Humor trivializes serious problems |

---

## Error State UI Patterns

### Inline Validation

Real-time feedback as user fills out forms.

| Timing | Behavior | Best For |
|--------|---------|----------|
| **On blur** (leave field) | Validate after user finishes typing | Most form fields |
| **On submit** | Validate all fields at once | Simple forms with few fields |
| **On keypress** (debounced) | Validate while typing (with delay) | Availability checks (username, email) |
| **On focus + format hint** | Show expected format before user types | Complex formats (phone, date, card number) |

**Inline validation design rules:**
- Show error messages directly below the relevant field
- Use red border/outline on the field (with accessible color + icon for color-blind users)
- Preserve user input — never clear what they typed
- Show success state (✅) for corrected fields to build confidence
- Scroll to first error if errors are off-screen

### Toast / Snackbar Notifications

| Use For | Duration | Dismissible | Position |
|---------|----------|:----------:|----------|
| Success confirmation | 3–5 seconds | Auto-dismiss | Bottom center or top right |
| Minor error (recoverable) | 5–8 seconds | Manual dismiss | Bottom center or top right |
| Major error (blocking) | Persistent | Manual dismiss only | Top center |
| Undo opportunity | 5–10 seconds | "Undo" button + auto-dismiss | Bottom center |

### Full-Page Error States

Use for critical errors where the entire view cannot load. Include: illustration/icon, clear headline, brief explanation (1–2 lines), primary action button, and secondary link. Examples: 404 pages (search box + home link), server errors ("Refresh" button + status page link), and permission errors ("Request access" button).

### Empty States

Empty states (not errors, but absence of content) need intentional design: first-time use (educational + CTA), no search results (suggest alternatives), filtered to empty (show active filters + clear option), and all-items-processed (positive confirmation + next action).

---

## Edge Case Identification

### Common Edge Case Categories

| Category | Edge Cases to Consider |
|----------|------------------------|
| **Data volume** | Zero items, one item, maximum items, very large dataset |
| **Text content** | Very long text, very short text, special characters, emoji, RTL languages, no text |
| **User state** | Logged out, expired session, multiple tabs, multiple devices |
| **Timing** | Slow network, timeout, simultaneous actions, stale data |
| **Permissions** | Changed mid-session, downgraded plan, removed from team |
| **Device** | Small screen, large screen, landscape, portrait, screen reader, keyboard-only |
| **Browser** | Back button, forward button, refresh, bookmark mid-flow, deep link |
| **Input** | Copy-paste, autofill, password manager, voice input |
| **Interruption** | Phone call during flow, app switch, notification overlay |
| **Account state** | Trial expired, payment failed, account suspended |

### Edge Case Discovery Checklist

For every flow, check: zero data, one item, 10,000 items, browser back/refresh, new tab, network drop, session expiry, concurrent edits, permission changes, copy-paste, screen reader use, and different languages.

---

## Recovery Flow Design

### Recovery Flow Principles

| Principle | Description | Implementation |
|-----------|------------|----------------|
| **Preserve user work** | Never lose what the user has entered or created | Auto-save; preserve form state on error |
| **Offer undo** | Allow users to reverse accidental actions | Undo toast for destructive actions |
| **Provide alternatives** | If path A fails, offer path B | "Can't upload? Try drag-and-drop or paste a URL" |
| **Degrade gracefully** | If a feature breaks, don't break the whole page | Show the rest of the page; isolate broken component |
| **Auto-retry silently** | For transient errors, retry before showing error | Retry API calls 2–3 times before alerting user |
| **Let users skip** | Don't force users through broken optional steps | "Skip for now" option on non-critical steps |

### Destructive Action Protection

| Protection Level | Method | When to Use |
|-----------------|--------|------------|
| **None** | No confirmation | Easily reversible actions (mark as read, move to folder) |
| **Undo** | Action + undo toast (5–10 sec) | Moderate actions (archive, remove from list) |
| **Confirm dialog** | "Are you sure?" with clear consequences | Significant actions (delete project, remove member) |
| **Type to confirm** | User must type item name to confirm | Irreversible high-impact actions (delete account, purge data) |
| **Cool-down period** | Action is scheduled, not immediate; can cancel | Account deletion (30-day grace period) |

**Confirmation dialog best practices:** Use specific headlines ("Delete 'Project Alpha'?" not "Are you sure?"), state consequences clearly, label buttons specifically ("Delete Project" not "OK"), and place destructive actions on the right with cancel on left.

---

## Error Handling Patterns by Flow Type

### Form Submission Errors

| Scenario | Pattern |
|----------|--------|
| Single field invalid | Inline error below field + red border |
| Multiple fields invalid | Scroll to first error + summary at top + inline per field |
| Server rejects submission | Toast or banner with specific reason; preserve all input |
| Network failure during submit | Auto-retry; then show "Couldn't save. [Retry] [Save offline]" |
| Duplicate entry | "This email is already registered. [Log in instead]" |

### Other Flow-Specific Errors

Apply these same principles to authentication flows (preserve session state on re-auth), payment flows (never retry silently; always communicate status), and collaboration flows (show diffs for conflicts; provide clear merge/keep options).

---

## Error Prevention Strategies

| Strategy | Description | Example |
|----------|------------|--------|
| **Constraints** | Limit inputs to valid options | Date picker instead of text field |\n| **Defaults** | Pre-fill with smart defaults | Default country based on IP |
| **Suggestions** | Guide users toward valid input | Autocomplete, format hints |
| **Confirmation** | Verify before irreversible actions | Type-to-confirm for destructive actions |
| **Undo** | Allow reversal instead of preventing | "Sent. [Undo]" within 10 seconds |
| **Auto-save** | Remove the need to manually save | "Saved 2 seconds ago" indicator |
| **Graceful degradation** | Keep working when parts fail | Load cached data when API is slow |
