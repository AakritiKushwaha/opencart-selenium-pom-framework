# OpenCart UI Test Automation

A Java 17 UI automation framework for OpenCart using Selenium WebDriver, TestNG, and the Page Object Model. It demonstrates reusable page objects, parallel test execution, Excel-driven test data, and automated execution reporting.

Test target: [OpenCart demo login](https://naveenautomationlabs.com/opencart/index.php?route=account/login).

## Project Highlights

- Page Object Model separates page interactions from test assertions.
- TestNG runs suite tests in parallel, with up to four test threads; WebDriver instances are stored per thread.
- Apache POI reads product-search and registration data from Excel.
- ExtentReports and Allure listeners capture execution results; failed tests attach screenshots to the Extent report.

## Test Coverage

| Area | Checks |
| --- | --- |
| Login | Page title and URL, forgot-password link, successful login |
| Account | Page title, logout link, account-section headings |
| Product search | Excel-driven searches, product selection, image count, product details |

The registration test class is also implemented and reads Excel data, but it is not included in the default regression suite.

## Prerequisites

- JDK 17
- Apache Maven
- Chrome, Firefox, Edge, or Safari (Safari requires macOS)
- Network access to the configured OpenCart application

WebDriverManager provisions browser drivers. Confirm Maven is using Java 17 with `mvn -version`.

## Run Tests

Run the default regression suite from the project root:

```bash
mvn clean test
```

The default suite is `src/test/resources/testrunner/testng_regression.xml`. It covers login, account, and product-search tests and runs TestNG tests in parallel. To select an environment, pass one of `qa`, `stage`, `dev`, `uat`, or `prod`:

```bash
mvn clean test -Denv=qa
```

When `env` is omitted, the framework uses the QA configuration. Browser, URL, headless mode, and incognito mode are configured in the selected properties file under `src/test/resources/config/`. Chrome and Firefox options include headless and incognito settings; the driver factory also recognizes Edge and Safari.

The `testng_sanity.xml` file is currently empty and is not a runnable suite.

## Test Data

Product search and registration tests read data from `src/test/resources/testdata/OpenCarTestData.xlsx`. The worksheet names are `product` and `register` respectively.

## Reports and Artifacts

- Extent report: `reports/TestExecutionReport.html`
- Failure screenshots: `screenshot/`
- Allure result files: `allure-results/`

To view an Allure report, install the Allure command-line tool and run:

```bash
allure serve allure-results
```

Generated reports, screenshots, and test output are local run artifacts and are ignored by `.gitignore`.

## Project Layout

```text
src/
  main/java/com/qa/opencart/
    constants/       Shared test constants
    factory/         WebDriver and browser options
    listeners/       TestNG listeners and reporting
    pages/           Page Object Model classes
    utils/           Element and Excel utilities
  test/
    java/com/qa/opencart/
      base/          Shared test setup and teardown
      tests/         UI test classes
    resources/
      config/        Environment and browser properties
      testrunner/    TestNG suite definitions
      testdata/      Excel test data
```

