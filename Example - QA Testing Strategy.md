
# Example — QA Testing Strategy

## Feature: Form Authentication

**Application:** The Internet. <br>
**Feature:** User login. <br>
**URL:** `/login`. <br>
**Objective:** Validate that users can authenticate successfully with valid credentials and are appropriately prevented from accessing the secure area with invalid credentials.

## Feature Overview
- **What is being changed or introduced?** A login feature that allows users to authenticate and access a secure area.
- **Who will use or be affected by it?**  Any user who needs authenticated access to the application.
- **Why is the feature being implemented?** To restrict access to authenticated users and provide a controlled login flow.

> **QA Interpretation**: "Does the login button work?"

## Risks
- **What could go wrong?**
    - Valid users cannot log in.
    - Invalid credentials are accepted.
    - Error message are incorrect or unclear.
    - User can access the secure area without authentication.
    - Logout doesn't properly terminate the session.
- **Who/what would be affected if it failed?** Users attempting to authenticate and any functionality protected by authentication.
- **How could the failure impact the business or users?** Users could be blocked from legitimate functionality, or unauthorized users could potentially access protected functionality.

### Risk Level

**High** - Authentication failures can have significant security and usability consequences.

## Test Scope
- **What needs to be tested?**
    - Valid login
    - Invalid username
    - Invalid password
    - Invalid username + password
    - Empty credentials
    - Login error messages
    - Successful redirect/access
    - Logout
    - Access to the secure page after logout

- **What is explicitly out of scope?**
    - Password recovery
    - Account registration
    - MFA
    - Password creation/change
    - Email verification

- **Whew could the change have side effects?**
    - Secure pages
    - Session handling
    - Logout
    - Navigation
    - Authentication state

## Test Levels
- **What level of testing is needed?**
    - Functional testing
    - Negative testing
    - Exploratory testing
    - Integration/system-level validation
- **Where should each level be performed?** Primarily through the web UI, while using browser DevTools where useful to inspect requests, cookies, and session behavior.
- **Why is each level necessary for this feature?** Because successful authentication isn't enough—we need to verify both expected behavior and protection against invalid states.

## Dependecies & Assumptions
- **What does this feature depend on?**
    - Authentication endpoint
    - Valid test credentials
    - Session/cookie mechanism
    - Secure page
- **Who/whats could prevent it from working correctly?**
    - Authentication service failure
    - Incorrect credentials
    - Session/cookie problems
    - Browser/network issues
- **What assumptions are we making?**
    - The supplied credentials represent a valid test account.
    - The secure page should only be accessible after successful authentication.

## Enviroments
- **Where will the feature be tested?** The Internet's web application using a supported desktop browser.
- **What enviroment/configuration is required?**
    - Supported browser
    - Internet connection
    - Valid test credentials

- **How will we know the enviroment is ready?**
    - Login page loads successfully.
    - Test credentials are available.
    - Secure page is accessible after authentication.

## Test Data
- **What data is needed?**
At minimum:
    - Valid username
    - Valid password
    - Invalid username
    - Invalid password
    - Empty username/password

- **Who/what provides or creates it?** The application provides the documented test credentials; invalid combinations are created by QA.
- **How should the data look or behave to cover the important scenarios?** Valid credentials should authenticate successfully; invalid or incomplete credentials should be rejected.

## Regression Impact
- **What existing functionality could be affected?**
    - Authentication
    - Secure page access
    - Logout
    - Navigation
    - Session management

- **Where are the dependencies or integration points?** The login mechanism, authentication endpoint, browser session/cookies, and secure page.
- **How much regression testing is needed?** Targeted regression, focused on authentication and protected navigation rather than unrelated application features.

## Entry Criteria
- **What must be ready before testing start?**
    - Login page available
    - Valid test credentials available
    - Test environment accessible

- **Who needs to provide or approve it?** The application/development team must provide a functional environment and valid credentials.
- **How do we verify that we're ready?** Open the login page and confirm that the basic authentication flow can be initiated.

## Exit Criteria
- **What must ve succesfully tested before realease?**
    - Valid authentication works.
    - Invalid credentials are rejected.
    - Secure content requires authentication.
    - Logout works correctly.
    - Critical authentication defects are resolved

- **What defects or risks are acceptanble?** No unresolved critical/high-risk authentication or access-control defects.
- **Who needs to approve or accept the remaining risk?** The appropriate product/engineering stakeholder should explicitly accept any remaining significant risk.

