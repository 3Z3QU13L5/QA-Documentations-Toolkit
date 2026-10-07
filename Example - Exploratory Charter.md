# Exploratory Testing Charter Template

**Application:** The Internet <br>
**Feature:** User Login / Form Authentication <br>
**Feature URL:** `/login` <br>
**Session ID:** ETC-LOGIN-001 <br>
**Session Duration:** 60 minutes <br>
**Test Level:** Functional / Integration / Security-oriented <br>
**Environment:** Public practice application <br>
**Status:** Planned <br>
**Tester:** Tester <br>
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

**What did we observe?**
Normal authentication and invalid-credential feedback behaved as expected. Direct access to /secure without authentication redirected to the login page. However, during one simulated navigation sequence, the browser displayed previously loaded protected-page content after logout when the Back button was used. Refreshing that page redirected to login.

**What actions were performed during exploration?**
I established the normal login and logout behavior using the provided valid credentials. I then explored invalid and empty credentials, direct navigation to /secure, page refreshes, browser history, and repeated login/logout sequences. During the session, I also investigated whether the application behaved consistently when revisiting a protected page after logout.

**What new questions emerged?**
Does the post-logout behavior expose cached protected content, or does it indicate that the server continues to accept an invalidated session? Does the behavior differ across browsers or cache configurations? What are the application's explicit requirements for browser-history behavior after logout?

### Observations

|Time    |Action / Investigation  |Observation  |Evidence   |
|--------|------------------------|-------------|-----------|
|10:00   |Open /login and establish the baseline |Login form loaded with username and password fields |SS-001 |
|10:05   |Submit valid credentials |Authentication succeeded; redirected to /secure; success message displayed |SS-002  |
|10:10   |Refresh the protected page |Remained authenticated; protected page loaded normally |SS-003    |
|10:15   |Log out and directly navigate to /secure |Access was denied; redirected to /login |SS-004 |
|10:20   |Submit incorrect username and password |Login rejected; appropriate error message displayed |SS-005   |
|10:25   |Submit empty credentials, then retry with valid credentials |Empty submission rejected; subsequent valid login succeeded |SS-006  |
|10:32   |Log out, then use the browser Back button |Previously displayed protected-page content appeared in browser history |VID-001   |
|10:38   |Refresh the page reached through Back navigation |Redirected to /login; protected content no longer displayed |VID-002    |
|10:43    |Repeat login → logout → Back sequence three times |Previously loaded protected content appeared in two of three simulated attempts |VID-003  |
|10:50    |Repeat failed login → successful login → logout |Authentication state and error recovery behaved as expected |SS-007 |
|10:55 |Review findings and capture reproduction notes |Recorded one suspected defect and one unresolved technical question |NOTES-001   |

> Evidence references represent example files in a hypothetical test-evidence repository.

### Questions Raised

- Does the protected response include appropriate cache-control headers? 
- Is the behavior reproducible in Firefox, Edge, or a private browsing session? 
- Does the application explicitly require protected content to be inaccessible through browser history after logout?

## 7. Findings

**What did we discover?**
The login form rejected invalid and empty credentials, valid credentials granted access to the protected page, and direct navigation to /secure after logout redirected to login. An unexpected browser-history behavior was observed: previously loaded protected content could reappear after logout without a new server request being established during the session.

**Why does each finding matter?**
The expected authentication behaviors provide evidence that the principal login and logout flows work under the conditions tested. The browser-history observation matters because sensitive information could remain visible on a shared device after a user logs out, even if server-side access is correctly revoked.

**What evidence supports the finding?**
Screenshots document successful and unsuccessful authentication. Video recordings capture the post-logout navigation sequence, and reproduction notes record the conditions under which the unexpected behavior appeared.

|ID     |Finding    |Impact / Significance  |Evidence   |Classification |
| ----- | --------- | --------------------- | --------- | ------------- |
|FND-001 |Valid credentials grant access to /secure |Confirms expected behavior of the primary authentication flow |SS-002, SS-003  |Expected behavior  |
|FND-002 |Invalid and empty credentials are rejected |Confirms basic negative-input handling |SS-005, SS-006    |Expected behavior  |
|FND-003 |Direct access to /secure after logout redirects to login |Provides evidence that direct protected-page access is restricted after logout |SS-004  |Expected behavior  |
|FND-004    |Browser Back navigation can redisplay previously loaded protected content after logout |Potential exposure of sensitive content on a shared device |VID-001, VID-003   |Suspected defect / security concern    |
|FND-005    |Refreshing the redisplayed page redirects to login |Suggests the observed content may originate from browser history or cache rather than an active authenticated session  |VID-002    |Technical investigation opportunity    |

## 8. Defects

**What behavior is actually incorrect?**
One simulated defect was recorded: previously loaded protected-page content remained visible through browser Back navigation after logout. It is classified as a provisional defect because the expected post-logout cache and history behavior requires confirmation.

**How can the defect be reproduced?**
1. Open /login in a fresh Chrome session.
2. Log in using valid credentials.
3. Verify that /secure is displayed.
4. Click Logout.
5. Verify that the browser returns to /login.
6. Press the browser Back button.
7. Observe whether the previously loaded protected page becomes visible.
8. Refresh the page and observe whether access is denied.


**What impact or risk does each defect introduce?**
A subsequent user of the same browser could potentially see information displayed during the previous user's authenticated session. The observed behavior does not, by itself, demonstrate that the previous session remains active or that new protected information can be retrieved.

### Defects Found

|Defect ID  |Description    |Severity   |Related Risk   |Status |
| --------- | ------------- | --------- | ------------- | ----- |
|BUG-001    |Protected-page content remains visible through browser Back navigation after logout |Medium, provisional |Exposure of previously viewed content after logout   |Open — requires technical confirmation |


## 9. Follow-Up

**What should we investigate next?**
Determine whether the post-logout Back-navigation behavior is caused by browser cache/history, back-forward cache, application behavior, or incomplete session invalidation. Confirm whether the browser is displaying previously cached content or successfully retrieving protected content after logout.

**What requires additional testing?**
Repeat the logout → Back → Refresh sequence under different conditions, including Chrome, Firefox, and Edge; normal and private browsing; and with browser caching disabled. Verify whether new requests to /secure are rejected after logout and whether the behavior is reproducible across multiple sessions.

**What should be added to regression coverage?**
Add regression scenarios covering protected-page access after logout, direct navigation to /secure after logout, browser Back/Forward after logout, page refresh after logout, and verification that protected content cannot be retrieved through a new request once the session has been terminated.

### Follow-Up Actions

|Activity   |Reason / Trigger   |Priority   |Owner  |
| --------- | ----------------- | --------- | ----- |
|Inspect protected-page cache-control headers   |Protected content reappeared after logout  |High   |Developer + QA |
|Verify server-side session invalidation    |Determine whether logout prevents new authenticated requests   |High   |Developer + QA |
|Reproduce in Chrome, Firefox, and Edge |Determine whether behavior is browser-specific |Medium |QA |
|Test private browsing and cache-disabled conditions    |Investigate caching and browser-history differences    |Medium |QA |
|Clarify post-logout content-visibility requirements    |Establish defensible expected behavior for BUG-001 |High   |Product Owner + Security   |
|Add regression scenarios for logout and browser history    |Preserve coverage of the newly discovered behavior |Medium |QA |

### Proposed Follow-Up Session

**Duration:** 45 minutes
**Mission:** Determine the cause and impact of the post-logout protected-content visibility issue.

**Completion criteria:** Document whether the issue is reproducible, whether new protected requests are rejected after logout, which browser conditions affect the behavior, and whether BUG-001 meets the agreed defect criteria.

## 10. Session Summary

### Session Duration

- **Start:** 10:00AM
- **End:** 11:00AM
- **Total:** 60 minutes

### Coverage
- Login with valid, invalild, and empty credentials.
- Authentucation and session-state transitions.
- Direct access to the protected `/secure` page.
- Page refresh while authenticated and after logout.
- Logout behavior.
- Browser "Back"/"Forward" navigation after logout.
- Repeated login/logout sequences.
- Unexpected credential and navigation variations.

### Key Findings

- Valid and invalid authentication flows behaved as expected under the tested conditions.
- Direct access to `/secure` after logout was correctly denied and redirected to the login page.
- Previously loaded protected content could reappear through browser Back navigation after logout in 2 of 3 simulated attempts.

### Overall Assessment

- **Follow-up required:** The observed Back-navigation behavior represents a potential information-exposure issue, but additional investigation is required to determine whether the content is coming from browser cache/history or represents an authentication/session-management failure.

### Recommended Next Action

- Investigate the post-logout Back-navigation behavior using network inspection, different browsers, and cache conditions; then determine whether BUG-001 should be confirmed and add the verified behavior to regression coverage.

> NOTE: THE QUESTION ARE THERE FOR REFERENCE