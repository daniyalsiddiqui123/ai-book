## Providing Domain-Specific Context

An AI's biggest weakness is its lack of specific context about your project. It has general knowledge of Python, but it doesn't know about your company's internal `AuthService` library or the specific data schema of your `users` table.

Providing this context is a key part of the developer's role as "architect-in-the-loop."

**Techniques for Context Provision:**

*   **Context Files:** Before starting a session with an AI agent, create a temporary context file. Copy and paste the relevant pieces of information into it: the database schema for the tables you're working with, the function signatures of the services you'll be calling, and the TypeScript interfaces for your core data models. You then instruct the AI: "Use the information in `context.md` as background knowledge when fulfilling my request."
*   **Vector Databases and RAG (Retrieval-Augmented Generation):** For larger projects, a more sophisticated approach is to use a vector database. You can "embed" your entire codebase, your technical documentation, and even your API guides into a searchable vector store. When you prompt the AI, it first searches this database for relevant information and includes it automatically as context. This is the core idea behind Retrieval-Augmented Generation (RAG) and is a feature of many advanced AI CLI tools and platforms.
*   **Fine-Tuning (The Heavy Hammer):** For very large organizations, it's possible to "fine-tune" a base AI model on your specific codebase. This creates a new, private model that has your internal patterns and APIs "baked in." This is a costly and complex process but can provide a significant boost in the quality and relevance of the AI's generated output.