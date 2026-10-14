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

- **ID:** BUG-001
- **Title:** Back button allow accessto protected-page content
- **Date:** September 28, 2026
- **Report:** in ETC-LOGIN-001
- **Envieoment:** Chrome — Desktop
- **Build/Version:** --

## Context

- **What functionality is affected?** User authentication, logout, protected-page access, browser navigation, and session-related behavior. <br>
- **What were you trying to accomplish?** The exploratory session was investigating whether authentication state was correctly maintained when transitioning between authenticated and unauthenticated states, particularly after logout. <br>
- **Why does this behavior matter?** A user may expect logout to prevent further access to information from the authenticated session. If protected information remains visible through browser history, another person using the same device could potentially view information from the previous session.

### Feature/Area
- User authentication

### Context
-  Previously loaded protected-page content can become visible again through the browser Back button after the user logs out

### Expected Result
- After logout, the authenticated session should no longer provide access to protected functionality or protected information. Browser navigation should not expose protected content in a way that violates the application's security requirements.

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

- **What should happen?** After logout, the authenticated session should no longer provide access to protected functionality or protected information. Browser navigation should not allow the user to bypass the application's authentication boundary. <br>
- **What actually happened?** After logout, pressing the browser Back button can display the previously loaded protected page. In the simulated session, the content appeared without first performing another successful login.

    Refreshing the page redirected the user to /login. <br>
- **What is the difference between expected and actual behavior?** The application correctly rejects direct access to /secure after logout, but browser Back navigation can redisplay content that was previously loaded while the user was authenticated.

The observed behavior therefore creates an inconsistency between server/application access control and browser navigation behavior.

### Expected Result

After logout, the authenticated session should no longer provide access to protected functionality or protected information. Browser navigation should not expose protected content in a way that violates the application's security requirements.

### Actual Result

After logout, pressing the browser Back button can display the previously loaded protected-page content. In the simulated exploratory session, this behavior occurred in 2 of 3 attempts. Refreshing the page redirected the user to /login.

The available evidence does not establish whether the browser is restoring cached content or whether a new request to the protected resource is being authorized incorrectly.

## Impact

- **Who or what is affected?**
    Users who access the application from a shared or subsequently reused device may be affected. The affected functionality includes protected-page content displayed during an authenticated session.

- **How does the defect affect the user or system?**
    A logged-out user may still see previously displayed protected information through browser history. This can create confusion about whether logout was successful and may expose information to someone who subsequently uses the same browser.

- **What could happen if it reaches production?**
    Depending on the sensitivity of protected content, information from a previous authenticated session could potentially be viewed by another person using the same device.

    The current evidence does not establish that a new protected request can be successfully made after logout.

**User Impact**  Users who access the application from a shared or subsequently reused device may be affected. <br> 

**Business Impact** Depending on the sensitivity of protected content, information from a previous authenticated session could potentially be viewed by another person using the same device. <br>

## Severity

- **How serious is the defect?**
    <br>
    **Medium — provisional.**

    The defect potentially exposes previously displayed protected information after logout, but the current evidence does not demonstrate an authentication bypass or successful retrieval of new protected data.

- **What happens if it remains unsolved?**
    Previously viewed protected information may remain visible through browser history after logout. The practical impact depends on the sensitivity of the information and the application's intended logout behavior.

- **Can users work around it?**
    Yes, a user can close the browser, avoid using Back, or refresh the page, which causes the application to redirect to login in the simulated scenario.

    However, relying on user behavior is not considered a satisfactory resolution for a session-management concern.

**Severity:** Medium — provisional.
<br>

**Justification**
Severity is provisionally classified as Medium because the issue involves potentially sensitive information exposure but has not been demonstrated to bypass server-side authentication.

Severity should be reassessed after technical investigation confirms the source and scope of the behavior.

## Priority

- **How urgently should this be fixed?**
    <br>
    **High — provisional.**

    The defect should be investigated before treating the logout functionality as fully verified because it concerns the boundary between authenticated and unauthenticated states.

- **Why does it need this level of priority?**
    Logout is a security-relevant operation. An unresolved discrepancy between logout behavior and browser navigation could affect user trust and potentially expose protected information.

- **What release or activity could it affect?**
    It should be resolved or explicitly accepted before a release containing authentication or session-management changes is considered complete.

**Priority:** High — provisional.
<br>

**Justification:** The priority is higher than the provisional severity because the defect affects an authentication boundary and requires technical clarification before the QA risk can be confidently assessed.

## Evidence

- **What evidence proves the defect exists?**
- **What information would help developers investigate it?**
    The following evidence would help determine the technical cause:

    * Browser Network requests during the Back navigation.
    * Response headers from the /secure page.
    * Cache-Control headers.
    * Browser history and Back-Forward Cache behavior.
    * Session/cookie state before and after logout.
    * Whether the browser makes a new request when the protected page reappears.

- **Can failure be observed in logs, network requests, database records, or other evidence?**
    The browser behavior is directly observable, but the current simulated session did not collect sufficient network or server-side evidence to determine whether the content was retrieved from the server or restored from browser history/cache.

    Network inspection is therefore a required follow-up investigation.

    **Screenshot / Video / Console Logs / Network logs / API Response / Database evidence / Device logs / Others**

## Technical Investigation

- **What component appears to be responsible?**
    The exact responsible component is currently unknown.

    Potential areas include browser caching/history behavior, Back-Forward Cache, HTTP response caching configuration, frontend navigation behavior, or session-management implementation.

- **What evidence supports this hypothesis?**
    The strongest indication is that:

    * Direct access to /secure after logout is denied.
    * Browser Back can redisplay previously loaded protected content.
    * Refreshing the redisplayed page causes a redirect to /login.

    This behavior is consistent with the possibility that the browser is displaying previously loaded content rather than obtaining newly authorized content from the server.

- **What areas should developers investigate?**
    Developers should investigate:

    * Cache-Control and related response headers for protected pages.
    * Browser Back-Forward Cache behavior.
    * Whether logout fully invalidates the server-side session.
    * Whether /secure makes a new network request when restored through Back navigation.
    * Authentication cookie/session state before and after logout.
    * Application behavior when a protected page is restored from browser history.


## Resolution / Verification

- **What was changed to resolve the defect?**

    **Pending.** No fix has yet been implemented in this simulated report.

- **How was the fix verified?**

    **Pending.** After implementation, QA should reproduce the original sequence:
    <br>
    **Login → Secure → Logout → Back → Refresh**

    The verification should confirm that:

    * Previously protected content is not improperly exposed.
    * Direct access to /secure after logout remains denied.
    * Refresh after logout continues to require authentication.
    * Session state is correctly invalidated.
    * The expected behavior is consistent across the supported browser configurations.

- **What regression testing is required?**

    Regression coverage should include:

    * Login with valid credentials.
    * Login with invalid credentials.
    * Direct access to /secure while unauthenticated.
    * Successful logout.
    * Direct /secure access after logout.
    * Browser Back after logout.
    * Browser Forward after logout.
    * Refresh after logout.
    * Re-login after logout.
    * Repeated login/logout sequences.
    * Session/cookie behavior after logout.

## Closure

- **Has the defect been successfully resolved?**
<br>
**No — Open.** The defect remains unresolved pending technical investigation and a verified fix.

- **Is there any remaining risk?**
<br>
Yes.

- **Who confirmed the result?**

    **QA Engineer:** Pending verification <br>
    **Developer:** Pending investigation/fix <br>
    **Product Owner / Security:** Pending risk confirmation where applicable

### Status

**Open**

### Remaining Risk
The remaining risk is potential exposure of previously viewed protected information through browser navigation after logout. The extent of the risk remains uncertain until the technical cause is established.

### Closed By

TBD

### Closure Date

TBD