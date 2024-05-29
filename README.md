# code_review_assignment

## code quality improvements

***1. Avoid Hardcoded Paths***

***Issue:***

Hardcoded paths for the geckodriver executable are used.

***Recommendation:***

Use configuration files or environment variables to manage file paths. This makes the code more portable and easier to maintain.
~python

import os

geckodriver_path = os.getenv('GECKODRIVER_PATH', 'default/path/to/geckodriver')
driver = webdriver.Firefox(executable_path=geckodriver_path)
python
