## Refactoring and Maintenance with AI

Code generation isn't a one-time event. AI assistants are powerful partners for the ongoing task of maintaining and improving a codebase.

*   **Refactoring:** You can select a large, complex function and prompt your AI: "Refactor this function. Break it down into smaller, single-responsibility helper functions. Add comments explaining the business logic."
*   **Adding Documentation:** Highlight a block of code and ask, "Generate JSDoc comments for this function, including parameter descriptions and a return value explanation."
*   **Improving Performance:** "This function is slow. Can you identify any performance bottlenecks and suggest a more efficient implementation? For example, could a `Map` be used instead of nested loops?"
*   **Language Translation:** A more advanced use case is migrating between technologies. "Translate this entire Python file, which uses the Flask web framework, into an equivalent TypeScript file using Express.js."

## The Art of Iteration: A Conversation with Your AI

The key to successful code generation is to treat it as an iterative conversation. Your first prompt might not yield the perfect result. The skill lies in providing effective feedback.

Instead of manually fixing the AI's output, provide corrective feedback in your next prompt.

*   **Initial Prompt:** "Create a function that sorts a list of users."
*   **AI Output:** (Generates a simple sort by username).
*   **Developer Feedback:** "That's a good start, but the sorting needs to be more robust. It should be a case-insensitive sort. Also, users with the 'admin' role should always be sorted to the top of the list, regardless of their username."

By providing these delta-based instructions, you guide the AI toward the correct implementation. This feedback loop is often much faster than writing the complex sorting logic yourself. You are the director, and the AI is the actor; you provide the motivation and blocking, and the AI performs the scene.

Mastering this "from spec to skeleton" workflow fundamentally changes the economics of software development. It allows developers to spend less time on the mundane and more time on the architectural and product-level thinking that truly creates value. The next chapter will show how we can apply this same generative power to the other side of the coin: testing.