# QA-Automation-portfolio-python

A comprehensive QA automation repository combining **API testing, performance testing, and UI testing** using **Python**, **Pytest**, **Locust**, and **Selenium WebDriver**.
This portfolio demonstrates end-to-end automation practices essential for real-world software testing workflows.

## Project Highlights
- Automated API functional tests with reusable request actions.
- Integrated load and performance testing using Locust.
- Selenium-Python UI tests built on the Page Object Model (POM).
- Allure reports and HTML reports for detailed test analytics.
- Supports local and LambdaTest cloud executions.

## Tech Stack
- **Language:** Python 3.8+
- **Frameworks:** Pytest, Locust, Selenium
- **Reporting Tools:** Allure, HTMLTestRunner
- **Cloud Grid:** LambdaTest
- **Environment Management:** Virtualenv

## Repository Structure
```
QA-Automation-portfolio-python/
│
├── actions/                      # Actions for API endpoints
│   ├── base_actions.py
│   └── post_actions.py
│
├── configs/                      
│   └── config.py                 # Environment and URL configurations
│
├── e2e_tests/
│   └── post_crud_tests.py        # Functional API CRUD tests
│
├── perf_tests/
│   └── post_perf_run.py          # Locust performance test file
│
├── selenium-ui/
│   ├── tests/                    # Selenium test cases
│   ├── pages/                    # Page Object Model classes
│   ├── data/config.yaml          # Test configuration (browser, environment)
│   └── results/                  # Selenium HTML reports
│
├── locust_headless.conf          # Performance test headless config
├── requirements.txt              # Python dependencies
├── setup.cfg                     # Pytest configuration
└── README.md                     # Documentation
```

## Setup Instructions
### 1. Install Prerequisites
- Install Python (≥ 3.8) from the [official website](https://www.python.org/downloads/).
- Ensure pip is available:
```
python -m ensurepip --upgrade
```
- (Optional) Use a virtual environment:
```
python -m venv venv
source venv/bin/activate      # Linux/macOS
.\venv\Scripts\activate       # Windows
```

### 2. Install Dependencies
```
pip install -r requirements.txt
```

## API & Performance Testing
### 1. Run Functional Tests
```
pytest
```
Generate and view HTML results:
```
pytest --html=results/report.html
```
To view Allure Reports:
```
allure serve results/
```

### 2. Run Performance Tests
**GUI Mode:**
```
locust -f perf_tests/post_perf_run.py
```
Visit: http://localhost:8089  
Enter:
- Users to simulate: 1  
- Spawn rate: 1  
- Host: https://jsonplaceholder.typicode.com  

**Headless Mode:**
```
locust --config=locust_headless.conf
```
CSV results are generated in `perf_result_*.csv`.

## Selenium UI Testing
### 1. Install Browser Drivers
Use `webdriver_manager` to automatically manage drivers:
```
pip install webdriver-manager
```

### 2. Run Selenium Tests
```
pytest selenium-ui/tests/ -v --html=selenium-ui/results/report.html
```

### 3. Configure Browsers
Edit browser and environment preferences in:
```
selenium-ui/data/config.yaml
```

## Sample Selenium Test
```
from selenium import webdriver
from selenium.webdriver.common.by import By
from webdriver_manager.chrome import ChromeDriverManager

def test_duckduckgo_search():
    driver = webdriver.Chrome(ChromeDriverManager().install())
    driver.get("https://duckduckgo.com/")
    search = driver.find_element(By.NAME, "q")
    search.send_keys("Python QA automation")
    search.submit()
    assert "Python" in driver.title
    driver.quit()
```

## Cloud Execution (LambdaTest)
Set environment variables:

**Linux/macOS:**
```
export LT_USERNAME="YOUR_USERNAME"
export LT_ACCESS_KEY="YOUR_ACCESS_KEY"
```

**Windows:**
```
set LT_USERNAME="YOUR_USERNAME"
set LT_ACCESS_KEY="YOUR_ACCESS_KEY"
```

Run tests remotely using LambdaTest capabilities:
```
webdriver.Remote(
  command_executor="https://{username}:{access_key}@hub.lambdatest.com/wd/hub",
  desired_capabilities=capabilities
)
```

## Additional Resources
- [Selenium Python Official Docs](https://selenium-python.readthedocs.io/)
- [Pytest Documentation](https://docs.pytest.org/en/stable/)
- [Locust Performance Testing](https://locust.io/)
- [LambdaTest Documentation](https://www.lambdatest.com/support/docs/)
```
