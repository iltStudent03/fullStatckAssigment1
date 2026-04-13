# Playwright E2E Testing Example

This repository is a starter template for end-to-end (E2E) testing using Playwright with JavaScript.
It is designed as a practical example to help you quickly run browser automation tests for a web application.

## Project Description

Playwright is a modern browser automation framework from Microsoft that supports:

- Chromium, Firefox, and WebKit
- Parallel test execution
- Built-in retries and trace viewer
- HTML reports and screenshots/videos on failure

This example README assumes you want a clean setup for writing UI tests such as login checks, navigation flows, and validation of page content.

## Prerequisites

Before starting, make sure you have:

- Node.js 18 or later
- npm 9 or later (or pnpm/yarn)
- Git

Check versions:

```bash
node -v
npm -v
```

## Installation

### 1. Clone the repository

```bash
git clone <your-repository-url>
cd FullStatckTraining
```

### 2. Initialize Playwright (if not already initialized)

```bash
npm init playwright@latest
```

Recommended answers during setup:

- Language: JavaScript
- Tests folder: tests
- Add GitHub Actions: Yes (optional)
- Install Playwright browsers: Yes

### 3. Install dependencies

If package files already exist:

```bash
npm install
```

### 4. Install browser binaries

```bash
npx playwright install
```

## Suggested Project Structure

```text
FullStatckTraining/
  tests/
    example.spec.js
  playwright.config.js
  package.json
  README.md
```

## Usage

### Run all tests

```bash
npx playwright test
```

### Run tests in headed mode

```bash
npx playwright test --headed
```

### Run tests in UI mode

```bash
npx playwright test --ui
```

### Run a single test file

```bash
npx playwright test tests/example.spec.js
```

### Run tests in a specific browser

```bash
npx playwright test --project=chromium
```

### Open the latest HTML report

```bash
npx playwright show-report
```

## Example Test

Create a file at tests/example.spec.js:

```javascript
const { test, expect } = require("@playwright/test");

test("homepage has expected title", async ({ page }) => {
  await page.goto("https://playwright.dev/");
  await expect(page).toHaveTitle(/Playwright/);
});

test("get started link is visible", async ({ page }) => {
  await page.goto("https://playwright.dev/");
  await expect(page.getByRole("link", { name: "Get started" })).toBeVisible();
});
```

Run it:

```bash
npx playwright test tests/example.spec.js
```

## Useful npm Scripts (optional)

Add these to package.json for convenience:

```json
{
  "scripts": {
    "test:e2e": "playwright test",
    "test:e2e:headed": "playwright test --headed",
    "test:e2e:ui": "playwright test --ui",
    "report": "playwright show-report"
  }
}
```

Then use:

```bash
npm run test:e2e
npm run test:e2e:ui
```

## Configuration Notes

You can customize behavior in playwright.config.js, such as:

- baseURL for your app
- test retries in CI
- timeout settings
- screenshot/video/trace capture policy
- browser projects to run

Example snippet:

```javascript
// playwright.config.js
const { defineConfig, devices } = require("@playwright/test");

module.exports = defineConfig({
  testDir: "./tests",
  retries: process.env.CI ? 2 : 0,
  use: {
    baseURL: "http://localhost:3000",
    screenshot: "only-on-failure",
    video: "retain-on-failure",
    trace: "on-first-retry",
  },
  projects: [
    { name: "chromium", use: { ...devices["Desktop Chrome"] } },
    { name: "firefox", use: { ...devices["Desktop Firefox"] } },
    { name: "webkit", use: { ...devices["Desktop Safari"] } },
  ],
});
```

## CI Example

For CI pipelines (GitHub Actions, Azure DevOps, etc.), common flow:

1. Install dependencies
2. Install Playwright browsers
3. Run tests
4. Publish test reports/artifacts

Minimal command set:

```bash
npm ci
npx playwright install --with-deps
npx playwright test
```

## Troubleshooting

- Browser not found:
  - Run npx playwright install
- Tests are flaky:
  - Prefer locator assertions and explicit waits via expect
  - Enable trace on retry and inspect failures
- App is not reachable:
  - Verify baseURL and local server start command

## Learning Resources

- Playwright docs: https://playwright.dev/docs/intro
- Playwright test API: https://playwright.dev/docs/api/class-test
- Best practices: https://playwright.dev/docs/best-practices

## Lesson 1 Update

- Added feature-branch workflow example changes on Feature-lesson1.
- Added a dedicated Playwright installation guide in PLAYWRIGHT_INSTALLATION.md.
