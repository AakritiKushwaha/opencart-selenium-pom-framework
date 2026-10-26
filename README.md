# OpenCart Selenium Automation

Java-based UI automation for the OpenCart demo application, built with Selenium WebDriver, TestNG, and the Page Object Model. The framework supports multiple browser and environment configurations, Excel-driven test data, and ExtentReports/Allure reporting.

## Prerequisites

- JDK 17
- Apache Maven 3.8 or later
- Chrome, Firefox, Edge, or Safari (Safari requires macOS)
- Network access to the configured OpenCart application

Selenium Manager/WebDriverManager handles driver setup for the supported browsers. Confirm Maven is using Java 17 with `mvn -version`.

## Run Tests

Run the default regression suite from the project root:

```bash
mvn clean test
```

The default suite is `src/test/resources/testrunner/testng_regression.xml`. It covers login, account-page, and product-search tests. To select another environment, pass one of `qa`, `stage`, `dev`, `uat`, or `prod`:

```bash
mvn clean test -Denv=qa
```

When `env` is omitted, the framework uses the QA configuration. Browser, URL, headless mode, and incognito mode are set in the selected properties file under `src/test/resources/config/`. The browser options support Chrome and Firefox; the driver factory also recognizes Edge and Safari.

The `RegisterTest` class is available in the test source, but it is not currently included in the default regression suite. The `testng_sanity.xml` file is currently empty; populate it with a valid TestNG suite before selecting it.

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

Generated reports, screenshots, and test output are local run artifacts; review `.gitignore` before committing them.

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

## Before Publishing

The environment properties currently include hard-coded application login credentials. Replace them with non-sensitive test credentials or load credentials from a local, untracked configuration or environment variables before pushing this repository. If those values are real or have been shared, rotate them. Do not commit account passwords or other secrets.
