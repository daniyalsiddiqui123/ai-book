## Generating Integration and E2E Tests

The same principle applies to higher-level tests. If you use a Gherkin spec to define user behavior, it can serve as a direct blueprint for an end-to-end (E2E) test using a framework like Cypress or Playwright.

**Gherkin Spec Snippet:**

```gherkin
  Scenario: Failed login with invalid credentials
    Given the user is on the login page
    When the user enters "user@example.com" into the email field
    And the user enters "wrongpassword" into the password field
    And the user clicks the "Log In" button
    Then the user should remain on the login page
    And an error message "Invalid email or password" should be displayed
```

**Prompt to the AI Agent:**

> "Using the Gherkin spec file `features/login.feature`, generate the corresponding Playwright test file `tests/login.spec.ts`."

**AI-Generated Playwright Test:**

```typescript
import { test, expect } from '@playwright/test';

test.describe('User Authentication', () => {
    test('Failed login with invalid credentials', async ({ page }) => {
        // Given the user is on the login page
        await page.goto('/login');

        // When the user enters credentials
        await page.fill('input[name="email"]', 'user@example.com');
        await page.fill('input[name="password"]', 'wrongpassword');

        // And the user clicks the "Log In" button
        await page.click('button:has-text("Log In")');

        // Then the user should remain on the login page
        await expect(page).toHaveURL('/login');

        // And an error message should be displayed
        const errorMessage = page.locator('.error-message');
        await expect(errorMessage).toBeVisible();
        await expect(errorMessage).toHaveText('Invalid email or password');
    });
});
```

The AI effectively translates the human-readable Gherkin steps into concrete browser automation commands. This creates a powerful, living link between your user-facing requirements and your automated test suite. When a product manager signs off on a feature file, they are simultaneously signing off on the E2E test that will validate it.