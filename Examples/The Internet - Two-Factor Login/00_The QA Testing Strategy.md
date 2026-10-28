
# The QA Testing Strategy Template

**Application:** The Internet - Two-Factor Login
**Feature:** Two-Factor Login<br>
**URL:** `/two_factor`<br>
**Objective:** Validate that users can authenticate successfully with valid credentials and the two-factor OTP, and are appropriately prevented from accessing the secure area with invalid credentials and the two-factor OTP.

## Feature Overview
The feature tha was introduce to the system is the two-factor OTP on the login process. The intended entity that would be affected by this new feature would be the user, This feature is being implemented with the poupose to increase the security of the login process.

## Risks
The major risk is allowing access with invalid OTP, either wrong code or empty input, the acceptance of the OTP code beyond the time life expected. If the feature failes the system and the user will be voulnerable. The user or system information and data will be open to loses and miss uses.

### Risk Level

**High**

## Test Scope
The two-factor authentication of the login feature usin valid and invalid inputs. 
    - Empty Credentials
    - Valid OTP
    - Invalid OTP
    - Expired OTP
The login feature is out of scope for this session of testing.

## Test Levels

The tests would be perfomre primarily through the web UI, while using browser DevTools where useful to inspect requests, cookies, and session behavior. The following levels are needed.
   
    - Functional testing
    - Negative testing
    - Exploratory testing
    - Integration/system-level validation

## Dependecies & Assumptions
- What does this feature depend on? login process, otp api
- Who/whats could prevent it from working correctly? a malfunction of the api
- What assumptions are we making? The valid OTP is being provided.

> **QA Note:** This section is particularly valuable because it exposes questions we might need to ask the developer/PO before testing.

## Enviroments
- Where will the feature be tested? The browser On the browser application 
- What enviroment/configuration is required? Access to internet, a browser and The Internet application
- How will we know the enviroment is ready? 

## Test Data
- What data is needed? Login credentials and OTP code.
- Who/what provides or creates it? they are provided by the browser's application
- How should the data look or behave to cover the important scenarios? 

## Regression Impact
- What existing functionality could be affected? The loggin process completion, access to the TK site
- Where are the dependencies or integration points? 
- How much regression testing is needed?

## Entry Criteria
- What must be ready before testing start?
- Who needs to provide or approve it?
- How do we verify that we're ready?

## Exit Criteria
- What must ve succesfully tested before realease?
- What defects or risks are acceptanble?
- Who needs to approve or accept the remaining risk?

