## Working with Existing (Legacy) Code

Very few developers have the luxury of starting a new project from scratch. Most of our work involves adding features to or fixing bugs in large, existing codebases. Can you apply AI/Spec-Driven principles to a ten-year-old monolith with no tests?

The answer is yes, but you must be pragmatic and incremental. A "boil the ocean" approach of trying to write specs for the entire legacy system at once will fail. Instead, apply the "campsite rule": leave the codebase cleaner than you found it.

**The "Bubble-Up" Strategy:**

1.  **Isolate the Change:** Identify the specific part of the system your new feature or bug fix will touch. Draw a "bubble" around this small section of the code.
2.  **Write a "Retro-Spec":** Your first step is to write a specification for the *current* behavior of the code inside your bubble. Use AI to help. Feed the legacy code into your AI assistant and ask it: "Generate a Gherkin spec file that describes the behavior of this function. What are its inputs, outputs, and side effects?" This creates a regression test and proves the AI understands the code.
3.  **Generate Characterization Tests:** Use the "retro-spec" to generate a suite of tests that lock the current behavior in place. If the legacy code has no tests, this is a massive first win. You've just created a safety net.
4.  **Modify the Spec:** Now, update the specification to describe the *new*, desired behavior for your feature or fix.
5.  **Regenerate and Validate:** Use the updated spec to regenerate the code *only within your bubble*. Run your new test suite. The tests for the old behavior should now fail, and the tests for the new behavior should pass.

By applying this strategy incrementally, you can slowly and safely introduce the benefits of AI/Spec-Driven Development into a legacy project. Each new feature adds a small, well-specified, and fully-tested module to the codebase, gradually improving its quality over time.