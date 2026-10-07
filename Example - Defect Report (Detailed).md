# Defect Report Template

**Defect ID:** BUG-001 <br>
**Application:** The Internet <br>
**Feature:** User Login / Form Authentication <br>
**Environment:** Chrome — Desktop <br>
**Test Level:** Functional / Security-oriented <br>
**Discovery Session:** ETC-LOGIN-001 <br>
**Discovery Date:** September 28, 2026 <br>
**Status:** Open <br>
**Severity:** Medium — Provisional <br>
**Priority:** High — Provisional <br>
**Reporter:** QA Engineer <br>
**Related Risk:** Incorrect session termination / protected-content exposure

## Identification

- **What is the defect?** Previously loaded protected-page content can become visible again through the browser Back button after the user logs out. <br>
- **Where does it occur?** The behavior occurs during browser navigation from the login page back to the previously visited `/secure` page after logout. <br>
- **When was it discovered?** The defect was discovered during exploratory session **ETC-LOGIN-001** on September 28, 2026, while investigating authentication state transitions and logout behavior.

### Defect

- ID:
- Title:
- Date:
- Report:
- Envieoment:
- Build/Version:

## Context

- **What functionality is affected?** User authentication, logout, protected-page access, browser navigation, and session-related behavior. <br>
- **What were you trying to accomplish?** The exploratory session was investigating whether authentication state was correctly maintained when transitioning between authenticated and unauthenticated states, particularly after logout. <br>
- **Why does this behavior matter?** A user may expect logout to prevent further access to information from the authenticated session. If protected information remains visible through browser history, another person using the same device could potentially view information from the previous session.

### Feature/Area
- 

### Context
- 

### Expected Result
- 

## Reproduction

- **What steps cause the defect?** <br>
    1. Open the /login page.
    2. Enter valid credentials:
    3. Username: tomsmith
    4. Password: SuperSecretPassword!
    5. Submit the login form.
    6. Verify that the application redirects to /secure.
    7. Click Logout.
    8. Verify that the application returns to /login.
    9. Press the browser Back button.
    10. Observe the previously displayed protected page.

- **What data or conditions are required?** <br>
    * A valid test account.
    * A successful authenticated session.
    * Access to the /secure protected page.
    * Browser history containing the previously loaded protected page.
    * Logout performed before using browser Back.
    * Desktop Chrome browser in the simulated session.

- **Can the defect be reproduced consistently?** <br>
The behavior was reproduced in **2 of 3 simulated attempts.**

The inconsistent reproduction rate means additional investigation is required before determining the exact technical cause.

### Preconditions
1. None

### Steps to Reproduce
|Step	|Action	|Expected	|Actual |
| ----- | ----- | --------- | ----- |
|1	|Open /login	|Login page displayed	|Login page displayed   |
|2	|Enter valid credentials	|Credentials accepted	|Credentials accepted   |
|3	|Submit login	|Redirect to /secure	|Redirect to /secure    |
|4	|Click Logout	|Session terminated and return to login	|Returned to login  |
|5	|Press Back	|Protected content should not remain accessible inappropriately	|Previously loaded protected content displayed  |
|6	|Refresh page	|Authentication required	|Redirected to /login   |

### Test Data 

- Valid Username and Password

### Reproducibility

**Frequency:** Sometimes

## Expected vs Actual

- What should happen?
- What actually happened?
- What is the difference between expected and actual behavior?

### Expected Result

### Actual Result

## Impact

- Who or what is affected?
- How does the defect affect the user or system?
- What could happen if it reaches production?

**User Impact**
<br>

**Business Impact**
<br>

**Technical Impact**
<br>

## Severity

- How serious is the defect?
- What happens if it remains unsolved?
- Can users work around it?

**Severity:** Blocker/Critical/Major/Minor/Trivial
<br>

**Justification**

## Priority

- How urgently should this be fixed?
- Why does it need this level of priority?
- What release or activity could it affect?

**Priority:** --
<br>

**Justification:** --

## Evidence

- What evidence proves the defect exists?
- What information would help developers investigate it?
- Can failure be observed in logs, network requests, database records, or other evidence?

**Screenshot / Video / Console Logs / Network logs / API Response / Database evidence / Device logs / Others**

## Technical Investigation

- What component appears to be responsible?
- What evidence supports this hypothesis?
- What areas should developers investigate?

### Suspected Component
<br>

### Technical Notes
<br>

### Supporting Evidence
<br>

## Resolution / Verification

- What was changed to resolve the defect?
- How was the fix verified?
- What regression testing is required?

**Fix Version / Build:** 
<br>

**Verification Steps:**
1. 
2. 
3. 

### Regression Performed


**Verification Result:** Passed / Failed

## Closure

- Has the defect been successfully resolved?
- Is there any remaining risk?
- Who confirmed the result?

### Status

Open / In Progress / Resolved / Reopened / Closed / Won't Fix

### Remaining Risk
- 
- 

### Closed By
### Closure Date