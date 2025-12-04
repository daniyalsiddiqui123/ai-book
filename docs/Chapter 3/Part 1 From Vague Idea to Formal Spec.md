If the specification is the single source of truth, then the ability to write a good specification becomes the most crucial skill in the AI/Spec-Driven Development paradigm. A great spec enables the AI to generate flawless code with minimal intervention. A poor spec will lead to a frustrating cycle of flawed output, manual corrections, and wasted time.

So, what makes a spec "AI-readable"? It's a combination of choosing the right format, adopting a clear and structured writing style, and providing the appropriate level of detail—a practice that can be thought of as "prompt engineering for requirements."

## From Vague Idea to Formal Spec

Every feature begins as a vague idea. "Users should be able to connect their calendar." This is a goal, not a specification. The first step is to break this goal down into concrete, testable behaviors. This is a collaborative process, often involving a product manager, a developer, and an AI assistant.

The conversation might look like this:

*   **Product Manager:** "We need a calendar integration feature."
*   **Developer:** "Okay. Which calendar providers should we support initially? Google Calendar, Outlook, Apple Calendar?"
*   **Product Manager:** "Let's start with just Google Calendar to keep it simple."
*   **Developer (prompting an AI assistant):** "AI, can you outline the standard OAuth 2.0 flow for Google Calendar API access? What scopes will we need to read calendar events?"
*   **AI Assistant:** "Certainly. The standard flow involves redirecting the user to a Google consent screen. You will need the `https://www.googleapis.com/auth/calendar.readonly` scope. The steps are: 1. Redirect user to Google's OAuth server. 2. User grants permission. 3. Google redirects back to your app with an authorization code. 4. Your app exchanges the code for an access token. 5. You can now use the access token to call the Calendar API."
*   **Developer:** "Great. Let's codify that. The spec needs a section for 'Authentication' and another for 'Displaying Events'."

This dialogue transforms a fuzzy concept into a structured outline. The goal is to leave as little room for ambiguity as possible *before* any code is generated.