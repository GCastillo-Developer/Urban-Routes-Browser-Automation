Web Automation Testing Project
Overview

This Python project automates the testing of a web page using a structured and modular approach. The project uses a Page Object Model (POM) to organize web elements and interactions, making tests maintainable and scalable.

The automation scripts include setup and teardown procedures, reusable helper functions, and structured test data management.

Project Structure:
project_root/
│
├── main.py           # Main test script with setup, teardown, and feature tests
├── page_object_model.py  # Defines page objects and web element interactions
├── helper.py         # Reusable helper functions (e.g., waits, clicks, validations)
├── data.py           # Test data storage (inputs, expected values, URLs)
├── requirements.txt  # Python dependencies
└── README.md         # Project documentation

Components:
main.py
• Contains test functions for multiple features of the web page.
• Includes setUp and tearDown methods for initializing and closing the browser.
• Calls methods from page_object_model.py and helper.py for interaction with the web page.

page_object_model.py
• Implements the Page Object Model design pattern
• Defines locators and functions for interacting with page elements.
• Promotes modularity and easier maintenance of tests.

helper.py
• Contains reusable utility functions:
  • Element waits
  • Click, input, and validation helpers
  • Any commonly used interactions across different tests

data.py
• Stores test data:
  • URLs
  • Input values
  • Expected results
• Enables separation of data from test logic for easier updates.

requirements.txt:

• Python dependencies: selenium, pytest.

Features Tested:
• Navigation between pages
• Form submissions
• Button clicks and element interactions
• Validations and assertions on web elements

Notes:
• The project uses Python 3.x and Selenium for browser automation.
• The Page Object Model ensures easy maintenance when the web page changes.
• Helper functions reduce duplicate code and simplify test scripts.
