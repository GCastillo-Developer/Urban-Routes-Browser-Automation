Urban-Routes-Browser-Automation
Overview

This Python project automates the testing of a web page using a structured and modular approach. The project uses a Page Object Model (POM) to organize web elements and interactions, making tests maintainable and scalable.

The automation scripts include setup and teardown procedures, reusable helper functions, and structured test data management.

Project Structure:
project_root/
│
├── main.py               # Main test script with setup, teardown, and feature tests
├── page_object_model.py  # Defines page objects and web element interactions
├── helper.py             # Reusable helper functions (e.g., waits, clicks, validations)
├── data.py               # Test data storage (inputs, expected values, URLs)
├── requirements.txt      # Python dependencies
└── README.md             # Project documentation

-------------------------------------------------------------------------------------------------------------------------------------------------

Main Test Suite (main.py)
The main.py file contains the full automated test suite for the Urban Routes web application.
It uses Selenium WebDriver along with the Page Object Model to execute end‑to‑end scenarios that simulate real user behavior.

This module is organized into a single test class, TestUrbanRoutes, where each method represents a distinct feature test.

### ----Class Setup ----

Class Setup — setup_class()
Before any tests run, the suite:

• Initializes Chrome WebDriver with performance logging enabled
(required for retrieving the SMS confirmation code).
• Checks whether the Urban Routes server is reachable using
helpers.is_url_reachable().
• Prints connection status to help diagnose environment issues.

This ensures the test environment is stable before executing feature tests.

### ----Test Scenarios----
Each test follows a consistent pattern:
• Navigate to the Urban Routes URL
• Initialize a UrbanRoutesPage object
• Enter required locations
• Perform the feature-specific interaction
• Assert the expected result

Below is a breakdown of each test.

### ----Set Route Test -- test_set_route()----
Validates that the user can correctly enter:
• From address
• To address

The test asserts that the values displayed in the UI match the expected inputs.

### ----Select Supportive Plan — test_select_plan()----
Simulates:
• Entering route locations
• Calling a taxi
• Selecting the Supportive plan

The test verifies that the correct plan is highlighted as active.

### ----Fill Phone Number & Confirm — test_fill_phone_number()----
This test covers the full phone verification flow:
• Opens the phone number input
• Enters the user’s phone number
• Requests an SMS code
• Retrieves the code using helpers.retrieve_phone_code()
• Enters the code and confirms
• Asserts that the phone number is correctly saved

This is one of the most advanced flows in the suite.

### ----Add Credit Card — test_fill_card()----
Simulates adding a payment method:
• Opens the payment method menu
• Selects Add Card
• Enters card number and security code
•  Confirms the addition
• Verifies that the payment method is now set to Card

### ----Comment for Driver — test_comment_for_driver()----
Tests the ability to:
• Open the comment field
• Enter a custom message
• Retrieve the entered text

The test ensures the comment is stored correctly.

### ----Order Blanket & Handkerchiefs — test_order_blanket_and_handkerchiefs()----
Validates the toggle switch for additional comfort items.

The test asserts that the toggle is successfully activated.

### ----Order 2 Ice Creams — test_order_2_ice_creams()----
Simulates increasing the ice cream quantity and verifies that:
• The displayed count equals 2

### ----Car Search Modal Appears — test_car_search_model_appears()----
This is the full end‑to‑end ordering flow:
• Enter route
• Select plan
• Enter phone number
• Retrieve and confirm SMS code
• Leave a comment
• Click Order
• Assert that the car search modal appears

This test confirms that the user can successfully order a taxi.

### ----Class Teardown — teardown_class()----
After all tests complete:
• The WebDriver instance is closed using quit()
• Ensures no browser processes remain open

------------------------------------------------------------------------------------------------------------------------------------------------

Page Object Model (pages.py)

This section contains automated UI tests for the Urban Routes web application using Python, Selenium WebDriver, and the Page Object Model (POM) design pattern. The codebase automates and validates full end-to-end user workflows, from configuring routes to completing taxi bookings.

### ----What the Project Does----
This test automation framework simulates actual user behavior on the Urban Routes web platform to ensure that critical business processes and UI features work exactly as expected. The test suite automatically performs and verifies the following user journey:

1. Address Configuration: Inputs and verifies the pickup (`From`) and destination (`To`) locations.
2. Taxi Plan Selection: Books a taxi specifically using the Supportive Plan tariff layer.
3. Phone Authentication Workflow: Inputs a user's phone number, triggers the validation setup, handles modal pop-ups, inputs the SMS verification token, and confirms the account login.
4. Credit Card Integration: Configures electronic payment profiles by securely filling in credit card numbers and CVV codes, changing focus to activate UI buttons, validating that the "Link" button updates its state correctly, and confirming that the application updates the payment method from cash to card.
5. Special Requirements Fulfillment:
   • Leaves custom textual comments or instructions for the taxi driver.
   • Activates toggles for additional package items (e.g., Blanket and Handkerchiefs).
   • Increments item counters to order extra amenities (e.g., selecting 2 Ice Creams).
6. Order Submission: Submits the complete ride reservation and validates that the asynchronous car search progress modal successfully appears on screen.

### ----Setup & Execution Guide----
Prerequisites
Make sure your environment includes the following components:
• Python 3.8+
• Google Chrome** browser
• ChromeDriver (Must match your current installed version of Google Chrome)

1. Installation
Clone the project repository to your local machine and install Selenium:

bash
git clone https://github.com/GCastillo-Developer/Urban-Routes-Browser-Automation
cd QA-USA-Python_Automation
pip install selenium

-------------------------------------------------------------------------------------------------------------------------------------------------

Helper Module (helper.py)
The helper.py file contains specialized utility functions that support the automation framework by handling tasks that fall outside standard Selenium interactions. These helpers improve reliability, reduce code duplication, and provide capabilities that Selenium alone does not offer.

Phone Confirmation Code Retrieval — retrieve_phone_code(driver)
This function extracts the phone confirmation code sent by the Urban Routes application.
Because the code is not displayed directly on the UI, the function listens to browser performance logs and retrieves the numeric code from the network response.

What it does:
• Monitors Chrome DevTools Protocol (CDP) performance logs.
• Detects API calls containing the phone confirmation number.
• Extracts all digits from the response body.
• Returns the confirmation code as a string.

When to use it:
• Only after the application has requested a phone confirmation code.
• Useful for automated flows requiring login or identity verification.

Why it matters:
• Enables fully automated end‑to‑end tests without manual code entry.
• Avoids brittle UI scraping by reading the actual network response.

• Contains reusable utility functions:
  • Element waits
  • Click, input, and validation helpers
  • Any commonly used interactions across different tests

************************************************************************************************************************************************

URL Reachability Check — is_url_reachable(url)
This function verifies whether the Urban Routes application is accessible before running tests.

What it does:
• Attempts to open the provided URL using a secure SSL context.
• Returns True if the server responds with HTTP 200.
• Returns False if the site is unreachable or returns an unexpected status.

When to use it:
• As a pre‑test check to avoid running tests against a down or unstable environment.
• In CI pipelines to fail fast when the application is offline.

Why it matters:
• Prevents false test failures caused by server downtime.
• Ensures your test suite only runs when the environment is ready.

--------------------------------------------------------------------------------------------------------------------------------------------------

File Constants (data.py)
• Stores test data:
  • URLs
  • File Constants
• Enables separation of data from test logic for easier updates.

-------------------------------------------------------------------------------------------------------------------------------------------------

requirements.txt:

• Python dependencies: selenium, pytest.

Features Tested:
• Selecting the Supportive Plan
• Filling in the Phone Number
• Adding a Credit Card
• Writing a Comment for the Driver
• Ordering a Blanket and Handkerchiefs
• Ordering 2 Ice Creams (Supportive Taxi)
• Ordering a Taxi with the Supportive Tariff

Notes:
• The project uses Python 3.x and Selenium for browser automation.
• The Page Object Model ensures easy maintenance when the web page changes.
• Helper functions reduce duplicate code and simplify test scripts.
