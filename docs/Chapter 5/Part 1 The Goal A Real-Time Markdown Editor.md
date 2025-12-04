Theory is essential, but there is no substitute for practice. In this chapter, we will walk through a complete, end-to-end project using the AI/Spec-Driven methodology. We will put the principles into action and use the tools we configured in the previous chapter to build a simple but non-trivial web application.

## The Goal: A Real-Time Markdown Editor

Our project will be a web-based Markdown editor. It's the "Hello, World" of modern web apps. The requirements are simple:

1.  The user sees two panels side-by-side.
2.  On the left, there is a text area where they can type Markdown.
3.  On the right, a preview panel instantly displays the rendered HTML from the Markdown input.
4.  The application should be a standalone HTML file with embedded CSS and JavaScript, requiring no server or build step.

This project is ideal because it's easy to understand, but it involves UI, user interaction, and a core logic component (the Markdown-to-HTML conversion), making it a perfect test case for our workflow.

Let's begin. We will follow the four key steps of the AI/Spec-Driven process.

## Step 1: Writing the Specification

We start by creating a new file named `markdown_editor.spec.md`. As discussed in Chapter 3, Markdown is a great format for describing UI and application structure. We will be as specific as possible to give our AI translator the best possible prompt.

Here is the content of our specification file:

```markdown
# Specification: Real-Time Markdown Editor

## 1. Project Overview

This project is a single-page, real-time Markdown editor. It will be delivered as a single `index.html` file with vanilla JavaScript and CSS, containing no external dependencies.

## 2. UI Layout

- The page should have a main title `<h1>` with the text "Real-Time Markdown Editor".
- The layout will be a two-column container.
- The left column contains a `<textarea>` element for user input.
- The right column contains a `<div>` element that will serve as the preview pane.
- The two columns should be separated by a subtle border.
- Both the `textarea` and the preview `div` should take up the full height of the viewport minus the header.

## 3. Core Functionality

- When the user types into the `textarea` on the left, the content should be converted from Markdown to HTML.
- The resulting HTML must be rendered in the preview `div` on the right in real-time (i.e., on every key press).
- The application must use a reputable, open-source JavaScript library for Markdown conversion. The library should be fetched from a CDN and included in a `<script>` tag. The library "Marked.js" is a suitable choice.

## 4. Styling (CSS)

- The overall theme should be clean and modern (e.g., dark mode).
- The `body` should have a dark background color (e.g., `#1e1e1e`) and light text (e.g., `#d4d4d4`).
- The `textarea` should be styled to match the dark theme, with no border and a slightly lighter background than the body. It should use a monospaced font.
- The preview `div` should have styling for standard HTML elements (headings, lists, code blocks) that makes them legible and aesthetically pleasing on a dark background.
  - `<h1>`, `<h2>`: Bold, with a bottom border.
  - `<code>`: A slightly different background color, rounded corners, and a monospaced font.
  - `<blockquote>`: An indented block with a left border.

## 5. Initial State

- When the page loads, the `textarea` should contain some default placeholder Markdown text to demonstrate the functionality to the user. This text should include a heading, a list, and a code block.

````

This spec is clear, detailed, and machine-readable. It covers layout, functionality, styling, and initial state, leaving very little to chance.

## Step 2: Generating the Artifacts (Code)

Now we turn to our AI partner. For this step, we'll use a CLI agent, as it's perfect for file-based generation tasks. We open our terminal and issue a prompt.

**Our Prompt to the AI CLI Agent:**

```
Using the file `markdown_editor.spec.md` as the single source of truth, create the `index.html` file that fully implements all requirements in the specification. Ensure all CSS and JavaScript are included directly within the HTML file.
```

The AI agent will now perform the following actions:

1.  **Parse the Spec:** It reads and understands all five sections of our `.spec.md` file.
2.  **Structure the HTML:** It creates the basic HTML5 document structure, including the `<h1>` title and the two-column layout.
3.  **Implement the Core Logic:** It identifies the need for a Markdown library, finds the CDN link for "Marked.js," and includes it. It then writes the JavaScript code to add an event listener to the `textarea` that calls the library and updates the preview `div`'s `innerHTML` on every input event.
4.  **Apply Styling:** It writes the CSS for the dark mode theme, the column layout, and the specific styling for the `textarea` and rendered HTML elements, as requested.
5.  **Set Initial State:** It adds the placeholder Markdown content to the `textarea` as the initial value.
6.  **Assemble the File:** It combines the HTML structure, the CSS styles (in a `<style>` block), and the JavaScript logic (in a `<script>` block) into a single `index.html` file.

The agent will then write this file to our directory.

*(Note: In a real-world scenario, you would run this command. For the purpose of this book, we will show the expected output in the next section.)*

## Step 3: The Developer's Review (Architect-in-the-Loop)

The AI has produced a candidate implementation. Our role now is to act as the architect and reviewer. We open the generated `index.html` file to inspect it. We also open it in a web browser to visually verify the result.

Here is what the AI might generate:
*(Abridged for brevity, but a real file would be complete)*

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Real-Time Markdown Editor</title>
    <!-- 1. Include Marked.js from CDN -->
    <script src="https://cdn.jsdelivr.net/npm/marked/marked.min.js"></script>
    <style>
        /* 4. Styling (CSS) */
        body {
            background-color: #1e1e1e;
            color: #d4d4d4;
            font-family: sans-serif;
            margin: 0;
            display: flex;
            flex-direction: column;
            height: 100vh;
        }
        h1 { text-align: center; border-bottom: 1px solid #444; padding-bottom: 10px; }
        .container { display: flex; flex: 1; }
        .column { flex: 1; padding: 15px; overflow-y: auto; }
        .column:first-child { border-right: 1px solid #444; }
        textarea {
            width: 100%;
            height: 100%;
            background-color: #252526;
            color: #d4d4d4;
            border: none;
            font-family: monospace;
            font-size: 16px;
            resize: none;
        }
        /* ... more CSS for preview elements ... */
    </style>
</head>
<body>
    <h1>Real-Time Markdown Editor</h1>
    <div class="container">
        <div class="column">
            <!-- 5. Initial State -->
            <textarea id="markdown-input"># Welcome!

This is a real-time Markdown editor.

- Type Markdown on the left.
- See the result on the right.

`Enjoy!`</textarea>
        </div>
        <div class="column" id="preview"></div>
    </div>

    <script>
        // 3. Core Functionality
        const markdownInput = document.getElementById('markdown-input');
        const preview = document.getElementById('preview');

        function renderMarkdown() {
            preview.innerHTML = marked.parse(markdownInput.value);
        }

        markdownInput.addEventListener('input', renderMarkdown);

        // Initial render on page load
        renderMarkdown();
    </script>
</body>
</html>
```

**Our Review Checklist:**
```
*   [x] Does it have the `<h1>` title? **Yes.**
*   [x] Is it a two-column layout? **Yes.**
*   [x] Does it update in real-time? **Yes, the `input` event listener ensures this.**
*   [x] Does it use Marked.js from a CDN? **Yes.**
*   [x] Is the styling a dark theme as described? **Yes.**
*   [x] Does it have the placeholder text? **Yes.**

The generated code looks clean, correct, and directly follows the specification. We open the file in Chrome, and it works perfectly.

## Step 4: Iteration and Refinement (If Necessary)

Imagine we open the app and notice one small issue: when we create a link in Markdown, clicking it does nothing. This is because standard links will navigate on the same page. For a better user experience, external links should open in a new tab.

This requirement was missing from our original spec! This is a classic example of where the developer's expertise comes in. We have two options:

1.  **Manual Fix:** We could use our IDE Copilot to quickly modify the JavaScript. We'd ask it to "modify the marked.js options to make all links open in a new tab." It would likely suggest a change to use `marked.use({ renderer: { link: (href, title, text) => `<a target="_blank" href="${href}" title="${title}">${text}</a>` } });`.
2.  **The "Spec-First" Fix (Preferred):** The more disciplined approach is to first update the specification. We add a new line to `markdown_editor.spec.md` under section 3:
    *   "All generated links in the preview panel must open in a new browser tab (`target='_blank'`)."

We then re-run the same AI command from Step 2. The AI will parse the updated spec, notice the new requirement, and regenerate the `index.html` file with the correct JavaScript modification.

This "Spec-First" approach keeps our specification as the true source of truth and ensures our project remains perfectly documented and reproducible.

With that final change, our project is complete. We went from a detailed idea (the spec) to a fully functional, styled, and correct web application in a fraction of the time it would have taken to write manually. We spent our brainpower on defining the requirements and reviewing the output, not on the toil of HTML boilerplate and CSS positioning. This is the power of AI/Spec-Driven Development in action.