## Prompt Engineering for Specifications

Writing a good spec is a form of prompt engineering. You are providing a detailed, structured prompt to the AI code generator. The principles are the same:

*   **Be Specific and Unambiguous:** Avoid fuzzy words. Instead of "the page should load quickly," write "the page must achieve a Google Lighthouse performance score of 90 or higher." Instead of "show the user's name," write "display the user's `firstName` and `lastName` properties in a `<h1>` tag."
*   **Provide Context:** Don't assume the AI knows about your existing codebase. If a spec requires interacting with another component, reference it explicitly. "When the user clicks the 'Save' button, call the `dataManager.saveUser(userData)` function."
*   **Define the "Don'ts":** Explicitly state what should *not* happen. "The password field must not display the characters as they are typed." "An unauthenticated user must not be able to access the `/admin` route."
*   **Use Examples:** Just like with Gherkin, providing concrete examples of inputs and expected outputs is one of the most effective ways to clarify your intent.