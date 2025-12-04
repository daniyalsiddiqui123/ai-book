## Choosing Your Format

There is no single "best" format for a specification; the choice depends on the nature of the feature being described. The key is that the format must be structured enough for a machine to parse reliably.

### Gherkin: For Behavior-Driven Specs

Gherkin is a simple, plain-language syntax originally developed for Behavior-Driven Development (BDD). Its `Given-When-Then` structure is exceptionally well-suited for describing user interactions and business rules. It forces you to think in terms of preconditions, actions, and outcomes, which is a perfect input format for an AI.

**Example Gherkin Spec for a Login Feature:**

```gherkin
Feature: User Authentication

  Scenario: Successful login with valid credentials
    Given the user is on the login page
    And they have a registered account with email "user@example.com" and password "password123"
    When the user enters "user@example.com" into the email field
    And the user enters "password123" into the password field
    And the user clicks the "Log In" button
    Then the user should be redirected to their dashboard page
    And a welcome message "Welcome back!" should be displayed

  Scenario: Failed login with invalid credentials
    Given the user is on the login page
    When the user enters "user@example.com" into the email field
    And the user enters "wrongpassword" into the password field
    And the user clicks the "Log In" button
    Then the user should remain on the login page
    And an error message "Invalid email or password" should be displayed
```

This format is nearly a direct blueprint for generating end-to-end tests and the underlying logic.

### Markdown: For UI, Content, and APIs

For specifying things that are less about behavior and more about structure—like a UI layout, an API endpoint, or a data model—Markdown is often a better choice. Its system of headers, lists, and code blocks is universally understood and flexible.

**Example Markdown Spec for a User Profile API Endpoint:**

````markdown
# API Endpoint: GET /api/users/{userId}

## 1. Summary

Retrieves the public profile information for a given user.

## 2. Path Parameters

- `userId` (string, required): The unique identifier for the user.

## 3. Success Response (200 OK)

The response body will be a JSON object with the following structure:

```json
{
  "id": "string",
  "username": "string",
  "joinDate": "string (ISO 8601 format)",
  "avatarUrl": "string (URL)"
}
```

## 4. Error Responses

- **404 Not Found:** Returned if the `userId` does not exist.
  ```json
  {
    "error": "User not found"
  }
  ```
- **500 Internal Server Error:** Returned for any unexpected server-side issues.
````

This provides a clear contract that an AI can use to generate the server-side route handler, the database query, and the data serialization logic.