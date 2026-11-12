
# The QA Testing Strategy Template

**Application:** The Internet - Two-Factor Login
**Feature:** Two-Factor Login<br>
**URL:** `/two_factor`<br>
**Objective:** Validate that users can authenticate successfully with valid credentials and the two-factor OTP, and are appropriately prevented from accessing the secure area with invalid credentials and the two-factor OTP.

## Feature Overview
The feature tha was introduce to the system is the two-factor OTP on the login process. The intended entity that would be affected by this new feature would be the user, This feature is being implemented with the poupose to increase the security of the login process.

The expected authentication process is as folow:
1. User submits primary credentials.
2. System validates those credentials.
3. System requests or verifies an OTP.
4. User submits the OTP.
5. System grants or denies access.

## Risks
The major risk is allowing access with invalid OTP, either wrong code or empty input, the acceptance of the OTP code beyond the time life expected. If the feature failes the system and the user will be voulnerable. The user or system information and data will be open to loses and miss uses, unauthorize access to protected resources, bypassing the second authentication factor, reusing an expired or previously accepted OTP and incorrect association between an OTP and a user session.

### Risk Level

**High**

## Test Scope

* **In scope:** OTP validation, OTP expiration, empty OTP submission, invalid OTP submission, and access after successful or unsuccessful OTP verification.
* **Out of scope:** Changes to username/password validation, password recovery, account registration, and other unrelated login functionality.

## Test Levels

The tests would be perfomre primarily through the web UI, while using browser DevTools where useful to inspect requests, cookies, and session behavior. The following levels are needed.
   
    - Functional testing
    - Negative testing
    - Exploratory testing
    - Integration/system-level validation

## Dependecies & Assumptions

This feature, the two-factor authentication login, depend on the normal login process and the OTP code recived from the api. The malfuntion of the api could prevent it from working correctly, so we are assuming the promary credentials are available, OTP test values can be obtained, the verificaciont service is available, test accounts have two-factor authentication enable.

## Enviroments

The two-factor authentication will be tested on the browser application. For this test is rwquired to have access to internet, a browser and the application The Internet application. And being able to acces the application the enviroment should be ready to proceed with the test. 

> If available add 
> Browser and version.
> Operating system.
> Application environment.
> Test account configuration.
> Two-factor authentication configuration.
> OTP generation/delivery mechanism.
> Access to browser DevTools.
> Any required test-specific configuration.

## Test Data

The login credentials and OTP code, these data is provide by the browser's applcation "The Internet", and this are:
- Valide User/Password.
- Invalid OTP code.
- Valid OTP code.
- Empty OTP code.
- Expired OTP code.
- Previously used OTP code.
- OTP from another session/user.

## Regression Impact

Within the functionality that could be affected by this feature are the loggin process, access to the secure site/page.

## Entry Criteria

The login page should be available and set with the two-factor authentication, the valid credentials and OTP Code, the test enviroment accessable, test account with two-factor authentication enabled, OTP code generated or retieved, securete area is available. The team should provide the credentials and OTP code. To verify that we are ready to test, enter the site and follow the normal login process.

## Exit Criteria
>criteria measurable.
For realease the valid authentication and the OTP code should works, the invalid credentials and OTP code are rejected, secure content requires authentication, Logout works correctly, critical authentication defects are resolved. No critical or high-risk issues are still present. 

* All planned critical authentication scenarios executed.
* Valid OTP accepted.
* Invalid, empty, and expired OTPs rejected.
* Protected content inaccessible without successful second-factor authentication.
* Logout terminates the authenticated session.
* No unresolved critical or high-risk authentication defects.
* Remaining risks documented and accepted by the authorized owner.