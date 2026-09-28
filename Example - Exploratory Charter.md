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

**What could go wrong?**
Invalid credentials might ve accepted, protected content might become accessible without authentication, logout might fail to terminate access, or unusual input might cause unexpected application behavior.

**What weaknesses or assumptions should we challenge?**
That login always establishes the correct session, logout always terminates it, pretected pages always enforce authentication, and browser navigation cannot expose protected functionality.

**Which risks deserve special attention?**
Authentication bypass, incorrect session termination, unauthorized protected-page access, incosistent authentication state, and unexpected failures during credential validation.

### Focus Areas

|Risk	|Exploration Focus	|Priority   |
|-------|-------------------|-----------|
|Authentication bypass	|Direct URL access and unexpected navigation	|Critical   |
|Incorrect session termination	|ogout followed by navigation or refresh	|Critical   |
|Invalid credentials accepted	|Unusual credential combinations	|High   |
|Inconsistent authentication state	|Repeated login/logout and browser navigation	|High   |
|Unexpected input handling	|Long values, whitespace, special characters	|Medium |
|Incorrect error feedback	|Failed login and recovery sequences	|Medium |

### Heuristics

- **Error handling:** Introduce invalid input and observe recovery.
- **Boundary conditions:** Explore unusual credential lengths and character combinations.
- **State transitions:** Investigate movement between logged-in and logged-out states.
- **Consistency:** Repeat equivalent actions in different sequences.
- **Recovery behavior:** Investigate whether the application returns to a valid state after unexpected actions.
- **Security:** Challenge access restrictions and session termination.
s
## 4. Test Environment

**Where will exploration take place?**
On the public *The Internet* practivce application, using its Form Authentication feature.

**What configuration or environment is required?**
Confirm that the login page loads, the supplied test credentials work, and the secure page and logout functionality are accessible.

**What tools or data are needed?**
A desktop browser, browser DevTools, the application's documented test credentials, and a place to record session notes and evidence.

### Environment

- **Application:** The Internet
- **Login page:** `/login`
- **Protected page:** `secure`
- **Browser / Device:** Chrome or another selected browser.
- **Test Data:**
    - **Valide username:** `tomsmith`
    - **Valid password:** `SuperSecretPassword!`
    - **Invalid Credentials:** Tester-generated values
- **Supporting Tools:** Browser DevTools, screenshots, session notes.
- **Session:** Fresh browser session recommended.

## 5. Exploration Approach

**How will we explore the system?**
Use time-boxed, risk-based exploratory testing. Begin with the normal login and logout flow to establish a baseline, then investigate authentication boundaries through unexpected inputs, navigation sequences, session-state changes, and browser behavior.

**What paths or behaviors will we investigate?**
Investigate successful and failed authentication, direct access to the secure page, login/logout transitions, browser Back/Forward/Refresh, repeated submissions, session behavior, and transitions between authenticated and unauthenticated states.

**What variations should we try?**
Vary credential validity, input content, input length, whitespace, character combinations, action order, repeated actions, navigation method, and authentication state. Compare equivalent behaviors performed through different sequences to identify inconsistencies.

### Approach

|Path	|Investigation   |
|-------|----------------|
|Unauthenticated → Login → Secure	|Establish normal authentication behavior    |
|Unauthenticated → Secure	|Challenge protected-page access |
|Login failure → Login success	|Investigate recovery from failed authentication |
|Login success → Refresh	|Investigate session persistence |
|Login success → Logout → Secure	|Investigate session termination |
|Login success → Logout → Back/Forward	|Challenge browser navigation behavior   |
|Login → Navigate → Logout	|Investigate authentication state transitions    |
|Invalid input → Retry → Valid input	|Investigate error recovery  |
|Repeated Login / Logout	|Investigate state consistency   |

### Variations

|Dimension	|Variations  |
|-----------|------------|
|Credentials	|Valid, invalid, partially valid, empty  |
|Input	|Normal, whitespace, unexpected characters, unusually long   |
|Action order	|Login → logout, logout → login, failed → successful |
|Navigation	|Direct URL, links, Back, Forward, Refresh   |
|Session state	|Authenticated, unauthenticated, recently logged out |
|Submission	|Single, repeated, rapid |
|Browser behavior	|Normal navigation, cached/history navigation    |

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
