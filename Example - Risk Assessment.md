
# The Risk Assessment Template

## Feature: Form Authentication

**Application:** The Internet. <br>
**Feature:** User login. <br>
**URL:** `/login`. <br>
**Assessment Type:** Feature-level QA Risk Assessment
**Environment:** QA / Test
**Risk Model:** Probability × Impact
**Overall Risk Level:** Medium–High

## Risk Identification

- **What could go wrong?**
The login functionality could:
    - Accept invalid credentials.
    - Reject valid credentials.
    - Allow access without authentication.
    - Fail to terminate the authentication information through errors, URLs, cookies, or browser storage.
    - Behave incorrectly when credentials are empty, malformed, or contain unexpected character.
    - Produce incorrect behavior after repeated login/logout attempts.

- **Where could failure occure?**
Potential failure points include:
    - Login form validation.
    - Crdential verification.
    - Authentication state/session management.
    - Redirect after successful login.
    - Error handling.
    - Logout functionality.
    - Browser cookies.session data.

- **Who or what could be affected?**

    | Area            | Potentially Affected                           |
    | --------------- | ---------------------------------------------- |
    | Users           | Users attempting to authenticate               |
    | Application     | Authentication and session management          |
    | Security        | Unauthorized access/session exposure           |
    | User experience | Login errors, redirects, confusing feedback    |
    | Business        | Users unable to access protected functionality |


## Risk Impact
- **What happens if this risk occurs?**
The consequences ranfe from minor usability problems to potentially serious security failure. <br>
For Example:
    - A valid user cannot log in  -> loss of functionality.
    - Invalid credentials are accepted --> unauthorized access.
    - Logout does not invalidate the session --> potential unautharized access from a shared/browser enviroment.
    - Incorrect error handling exposes authentication details -> portential information disclosure.

- **Who is affected by the failure?** Primarily:
    1. End Users.
    2. Users sharing devices/browsers.
    3. The application/system owner.
    4. Potentially unauthorized users if authentication controls fail.

- **How could it impact the business, system, or user?**

    | Impact Area   | Example                                        |
    | ------------- | ---------------------------------------------- |
    | Functionality | User cannot access authenticated functionality |
    | Security      | Unauthorized user gains access                 |
    | Data          | Protected information may become accessible    |
    | UX            | User receives confusing or misleading feedback |
    | Reputation    | Security failures reduce trust                 |
    | Operations    | Increased support/incident investigation       |


### Impact:
- User Impact:
- Business impact:
- Technical/system impact:
- Data impact:
- Operational impact:

## Risk Probability
- **How serious would the consequences be?**
    Severity depends heavily on **what the failure allows.**

    | Failure                                          | Severity     | Why                                     |
    | ------------------------------------------------ | ------------ | --------------------------------------- |
    | Incorrect error message                          | Low          | Primarily UX impact                     |
    | Valid credentials rejected                       | Medium       | Blocks legitimate users                 |
    | Incorrect redirect                               | Medium       | Disrupts authentication flow            |
    | Login fails intermittently                       | Medium–High  | Can significantly affect accessibility  |
    | Logout doesn't terminate access                  | High         | Authentication/session security concern |
    | Invalid credentials accepted                     | **Critical** | Potential unauthorized access           |
    | Protected page accessible without authentication | **Critical** | Authentication boundary is bypassed     |

- What would happen if the failure reached production?
- How difficult would recovery be?

## Risk Priority

| Risk                                             | Probability | Impact | Priority | Level       |
| ------------------------------------------------ | ----------: | -----: | -------: | ----------- |
| Invalid credentials accepted                     |           1 |      5 |    **5** | 🔴 High     |
| Protected page accessible without authentication |           1 |      5 |    **5** | 🔴 High     |
| Logout fails to invalidate session               |           3 |      5 |   **15** | 🔴 Critical |
| Valid credentials rejected                       |           3 |      4 |   **12** | 🔴 High     |
| Incorrect authentication redirect                |           3 |      3 |    **9** | 🟠 Medium   |
| Empty credentials accepted                       |           1 |      4 |    **4** | 🟡 Low      |
| Unexpected input breaks login                    |           3 |      3 |    **9** | 🟠 Medium   |
| Poor authentication error messaging              |           3 |      2 |    **6** | 🟡 Low      |

### Highest-priority risks

Testing should concentrate first on:

1. Authentication bypass
2. Invalid credentials being accepted
3. Session/logout security
4. Valid credentials being rejected
5. Authentication state and redirects

This is important: **Probability alone shouldn't determine testing prioirity**. A low-probability authentication bypass can deserve more attention than a highly probable cosmetic defect because the impact is dramatically different.

## Mitigation
- **How can we reduce the probability of failure?**
Use target functional, negative, state-based, and exploratory testing.

    | Risk                         | Mitigation                                                       |
    | ---------------------------- | ---------------------------------------------------------------- |
    | Invalid credentials accepted | Test invalid username/password combinations                      |
    | Authentication bypass        | Attempt direct access to protected pages without authentication  |
    | Logout failure               | Authenticate → logout → attempt to access protected page         |
    | Valid credentials rejected   | Test known valid credentials under normal conditions             |
    | Redirect failure             | Verify successful and unsuccessful navigation paths              |
    | Empty credentials            | Test empty username/password independently and together          |
    | Unexpected input             | Test malformed, boundary, and unusual input                      |
    | Session problems             | Inspect authentication state/cookies and test browser navigation |


- **What testing can detect or prevent the failure?**
    **High Priorioty**:
    - Positive testing.
    - Negative testing.
    - Boundary.edge testing.
    - State-transition testing.
    - Session testing.
    - Authentication bypass attempts.
    - Exploratory testing.
    - Browser DevTools inspection.

- What additionals controls are required?

## Residual Risk
- **What risk after testing and mitigation?**
    Potential residual risks include:
    - Server-side authentication implementation details that cannot be fully observed from the UI.
    - Infrastructure/security configuration outside the feature's testing scope.
    - Browser-specific behavior not covered during testing.
    - Concurrency/session behavior not tested under load.
    - Vulnerabilities requiring specialized security testing.


- **Why is the remaining risk acceptable or unacceptable?** <br>
    **For a simple demostration application:** likely acceptable after functional and basic security-oriented testing passes.

    **For a production authentication system:** this assessment alone would **not** be sufficient.

    Additional security testing would be appropriate, including areas such as:
        - Session management.
        - Authentication controls.
        - Authorization.
        - Brute-force protection.
        - Rate limiting.
        - Credential handling.
        - Secure cookie configuration.
        - CSRF protections.
        - Transport security.
        - Security headers.

- **Who should accept the remaining risk?**
    Normally the appropriate product/engineering authority or designated risk owner—not QA alone.


## Risk-Based Test Focus

**Priority 1 - Authentication Boundary**
Test:
    - Valid credentials.
    - Invalid username.
    - Invalid password.
    - Both invalid
    - Empty credentials.
    - Direct access to protected page
    - Access after logout.

**Reason**: Failure can compromise the authentication boundary. <br>

**Priority 2 - Authentication State**
Test:
    - Login -> authentication page.
    - Login -> refresh.
    - Login -> navigate.
    - Logout -> protected page.
    - Logout -> browser back.
    - Session expiration if applicable.

**Reason:** Authentication isn't just a button click; it is a **state transition system.** <br>

**Priority 3 - Input Handling**
Test:
    - Empty username.
    - Empty password.
    - Both empty.
    - Incorrect formats.
    - Unexpected characters.
    - Very long values.
    - Leading/trailing spaces where applicable.

**Reason:** Input validation can create both functional and security problems. <br>

**Priority 4 - User Experience**
Test:
    - Error messages.
    - Error placement.
    - Failed-login recovery.
    - Redirect behavior.
    - Form state after failure.
    - Keyboard interaction

**Reason:** Important, but lower business/security impact than authentication boundary failure.

## Risk Assessment Summary

### Overall Risk Level

**Medium-High**

The feature has a relatively small functional surface area but contains a **high-risk security boundary.** The most significant risks are unauthorized access, authentication bypass, and incorrect session termination.

### Main Concerns

- Authentication must reject invalid credentials.
- Protected functionality must not be accessible without authentication.
- Logout must correctly terminate the authenticated state.
- Valid users must be able to authenticate reliably.
- Input and error handling should not expose sensitive information.
- Authentication state should remain consistent across navigation and refresh.

### Recommended QA Action

**Go - only after high/critical risks have been adequately tested and no unresolved authentication/security defects remain.**
