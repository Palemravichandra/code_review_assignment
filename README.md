# code_review_assignment

## Code Quality Improvements

**1. Avoid Hardcoded Paths**

**Issue:**

Hardcoded paths for the geckodriver executable are used.

**Recommendation:**

Use configuration files or environment variables to manage file paths. This makes the code more portable and easier to maintain.
```python

import os
geckodriver_path = os.getenv('GECKODRIVER_PATH', 'default/path/to/geckodriver')
driver = webdriver.Firefox(executable_path=geckodriver_path)
```


**2. Proper Exception Handling**

**Issue:**

Raising generic exceptions without detailed messages.

**Recommendation:**
Use assertions or specific exception types with meaningful messages to improve error handling.

**Example:**
```python
assert self.driver.current_url == "https://www.happyfox.com/home", "Not on the home page"
```

**3. Use WebDriverWait Instead of time.sleep**

**Issue:**
time.sleep is used for waiting, which is inefficient and can lead to flaky tests.

**Recommendation:**
Use WebDriverWait to wait for specific conditions, making the tests more reliable and efficient.

**Example:**
```python
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC

wait = WebDriverWait(driver, 10)
element = wait.until(EC.element_to_be_clickable((By.ID, 'some_id')))
```
**4. Logging**

**Issue:**
Print statements are used for logging.

**Recommendation:**
Use the logging module for better logging practices. This provides more control over log levels and output formats.
**Example:**
```python
import logging

logging.basicConfig(level=logging.INFO)
logger = logging.getLogger(__name__)

logger.info(f"Row {i} Text: {rowText}")
```
**5. Correct Element Locator Usage**

**Issue:**
Improper usage of element locators, such as placing By.XPATH incorrectly.

**Recommendation:**
Ensure element locators are used correctly within find_element and find_elements methods.

**Example:**
```python
self.rowLocator = (By.XPATH, "//table[@id='dataTable']/tbody/tr")
rows = self.driver.find_elements(*self.rowLocator)
```
**6. Class Naming Conventions**
**Issue:**
Class names should follow proper naming conventions for better readability and consistency.

**Recommendation:**
Use CamelCase for class names.

**Example:**
```python
class TestCase101:
    # Class code

class PagesForAutomationAssignment:
    # Class code
```
**7. Modularization and Reusability**
**Issue:**
Methods and code blocks can be further modularized for reusability.

**Recommendation:**
Break down large methods into smaller, reusable methods. This makes the code easier to maintain and extend.

**Example:**
```python
class LoginPage(BasePage):

    def enter_username(self, username):
        self.driver.find_element(By.ID, "username").send_keys(username)

    def enter_password(self, password):
        self.driver.find_element(By.ID, "password").send_keys(password)

    def click_login(self):
        self.driver.find_element(By.ID, "loginButton").click()

    def login(self, username, password):
        self.enter_username(username)
        self.enter_password(password)
        self.click_login()
```

## Conclusion

Implementing these improvements will significantly enhance the quality of the test automation code, making it more robust, readable, and maintainable. Always aim to follow best practices and continuously refactor code to adapt to new requirements and improvements.
