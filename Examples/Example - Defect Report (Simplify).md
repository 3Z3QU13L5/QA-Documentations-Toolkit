# Defect Report Template

**Defect ID:** BUG-001 <br>
**Application:** The Internet <br>
**Feature:** User Login / Form Authentication <br>
**Environment:** Chrome — Desktop <br>
**Status:** Open <br>
**Severity:** Medium — Provisional <br>
**Priority:** High — Provisional <br>
**Related Risk:** Incorrect session termination / protected-content exposure

## Description

- **What is the defect?** Previously loaded protected-page content can reappear after logout when the user presses the browser Back button.
- **Where does it occur?** During browser navigation from the login page back to the previously visited /secure page after logout.
- **What functionality is affected?** Logout, protected-page navigation, authentication state, and browser history behavior.

**Severity:** Medium
<br>

## Reproduction

- **What steps cause the defect?** Log in with valid credentials, open the protected page, log out, and press the browser Back button.
- **What data or conditions are required?** A desktop Chrome browser session, valid test credentials, a successfully loaded protected page, and browser history containing that page.
- **What evidence proves the defect exists?** Simulated video evidence shows previously loaded protected content reappearing after logout. The behavior occurred in 2 of 3 simulated attempts. Technical confirmation of the cause is still pending.

### Preconditions (Given)
1. The user is using Chrome on a desktop browser.
2. The login page at https://the-internet.herokuapp.com/login is accessible.
3. Valid test credentials are available: username tomsmith, password SuperSecretPassword!.
4. The user can authenticate successfully and access /secure.
5. The protected page has been loaded and remains in browser history.

### Steps to Reproduce (When)
1. Open /login and enter the valid credentials.
2. Submit the form and verify that the application redirects to /secure.
3. Click Logout and verify that the application returns to /login.
4. Press the browser Back button.
5. Observe whether the previously loaded protected-page content reappears.
6. Refresh the page and observe whether the application redirects to /login.

### Expected Result vs Actual Result (Then)

**Expected Result**
<br> 
After logout, the authenticated session should no longer provide access to protected functionality or protected information. Browser navigation should not expose protected content in a way that violates the application's security requirements.

**Actual Result**
<br>
After logout, pressing the browser Back button can display the previously loaded protected-page content. In the simulated exploratory session, this behavior occurred in 2 of 3 attempts. Refreshing the page redirected the user to /login.

The available evidence does not establish whether the browser is restoring cached content or whether a new request to the protected resource is being authorized incorrectly.

### Evidence

**VID-001 — Video**: Previously loaded protected content appears after logout and browser Back navigation.
**VID-002 — Video**: Refreshing the redisplayed page redirects to /login.
**VID-003 — Video**: Repeated reproduction attempts; the behavior occurred in 2 of 3 simulated attempts.
**SS-004 — Screenshot**: Direct access to /secure after logout is denied.
**ETC-LOGIN-001 — Exploratory Testing Charter**: Documents the discovery and investigation notes.

**Additional evidence required:** Browser Network/DevTools records, protected-page response headers, cache behavior, and session state before and after logout.

**Current assessment:** Open — technical investigation required. The root cause has not been confirmed.
