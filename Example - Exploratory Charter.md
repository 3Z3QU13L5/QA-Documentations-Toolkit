# Exploratory Testing Charter Template

**Application:** The Internet
**Feature:** User Login / Form Authentication
**Feature URL:** `/login`
**Session ID:** ETC-LOGIN-001
**Session Duration:** 60 minutes
**Test Level:** Functional / Integration / Security-oriented
**Environment:** Public practice application
**Status:** Planned
**Tester:** TBD
**Execution Date:** TBD

## 1. Mission

**What are we trying to learn?**
Investigate how the login functionality behaves when user perform unexpected actions, enter unusual credentials, or transition between authenticated and unauthenticated state.

**Why is this area worth exploring?**
Predifined scenarios cover expected behaviors, but unusual action sequences may reveal authentication, session-managemente navigation, and error handling defects that scripted test could overlook. 

**What questions should the session answer?**
- Can unexpected user actions produce an incorrect authentication state?
- Can protected content remain accesible after logout or without authentication?
- Does the application recover correctly from invalid and unusual navigation sequences?

### Charter

Explore the User Login feature to discover unexpected behavior involving authentication state, session termination, protected-page access, and input handling.

**Primary objective:** Identify authentication-related risks that are not adequately explained or covered by existing test scenarios.

### Questions to Answer

- Can unexpected user actions produce an incorrect authentication state?
- Can protected content remain accesible after logout or without authentication?
- Does the application recover correctly from invalid and unusual navigation sequences?

## 2. Scope

**What are we exploring?**
The login form, credential validation, authentication feedback, successful login, secure-page access, browser navigation, and logout. 

**What is outside the session's scope?**
Passworf recovery, user registration, multi-factor authentication, load testing, brute-force testing, and specialized penetration testing.

**Which areas deserve attention during this session?**
At the boundaries between authenticated and unauthenticated states, particularly during login, logout, refresh, briwser navigation, and direct access to protected pages.

### In Scope

- Login with valid and invalid credentials.
- Unexpected credential combinations.
- Repeated form submissions.
- Navigation before and after authentication.
- Direct access to the secure page.
- Browser Back, Forward, and Refresh.
- Logout and subsequent access attempts.
- Authentication cookies and session behavior.
- Error-message consistency.

### Out of Scope

- Password reset and account recovery.
- Account creation and management.
- Multi-factor authentication.
- High-volume or aggressive security testing.
- Backend source-code review.
- Comprehensive accessibility and cross-browser audits.

## 3. Risks / Heuristics

What could go wrong?
What weaknesses or assumptions should we challenge?
Which risks deserve special attention?

### Focus Areas

- 
- 
- 

### Heuristics

- Error handling
- Boundary conditions
- State transitions
- Data integrity
- Usability
- Permissions / access
- Integration behavior
- Recovery behavior
- Performance perception
- Other:


## 4. Test Environment

Where will exploration take place?
What configuration or environment is required?
What tools or data are needed?

### Environment

- Application:
- Version / Build:
- Environment:
- Browser / Device:
- OS:
- Test Data:
- Supporting Tools:

## 5. Exploration Approach

How will we explore the system?
What paths or behaviors will we investigate?
What variations should we try?

### Approach

- 
- 
- 

### Variations

- Different inputs:
- Different users:
- Different states:
- Different devices/browsers:
- Different sequences:
- Unexpected actions:

## 6. Session Notes

What did we observe?
What surprised us?
What behavior requires further investigation?

### Observations

- 
- 
- 

### Questions Raised

- 
- 

## 7. Findings

What did we discover?
Why does each finding matter?
What evidence supports the finding?

| ID     | Finding | Severity | Evidence | Action |
| ------ | ------- | -------- | -------- | ------ |
| EX-001 |         |          |          |        |
| EX-002 |         |          |          |        |
| EX-003 |         |          |          |        |

## 8. Defects

What behavior is actually incorrect?
How can the defect be reproduced?
What evidence should be attached?

### Defects Found

- DEF-:
- DEF-:
- DEF-:


## 9. Follow-Up

What should we investigate next?
What requires additional testing?
What should be added to regression coverage?

### Follow-Up Actions

- 
- 
- 

## 10. Session Summary

### Session Duration

- Start:
- End:
- Total:

### Coverage
- 

### Key Findings

- 
- 
- 

### Overall Assessment

- 

### Recommended Next Action

- 
