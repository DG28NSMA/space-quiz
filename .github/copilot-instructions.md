# Copilot instructions

## Running and checking the quiz

- Open `index.html` directly in a browser. The quiz has no build step, dependencies, or configured test/lint runner.
- Manual smoke test: answer a mix of right and wrong choices, complete all 10 questions, verify the score and result, try Play again, and toggle both themes.

## Architecture

- The app is a single-file page: `index.html` contains the markup, CSS, question data, and browser-side behavior. There is no server or module system.
- The `questions` array is the source of truth for prompts, answer choices, correct answer indexes, icons, and feedback facts. `correct` is a zero-based index into `answers`.
- `renderQuestion()` rebuilds `#quizContent` for each step and attaches that step's answer and continue handlers. `showResult()` replaces it with the result view; `restart()` resets quiz state and renders question one.
- Score and quiz progress live outside `#quizContent`; progress counts a question only after it has been answered.

## Project conventions

- Keep quiz content in the `questions` array and preserve its shape; answer choices are generated from that data.
- Keep presentation and interaction self-contained in `index.html`; do not add a framework or external assets for ordinary quiz changes.
- Theme colors come from CSS custom properties in `:root` and `:root[data-theme="dark"]`. `setTheme()` updates the root attribute and stores the preference when browser storage is available; retain system-preference fallback and both palettes.
- Preserve native buttons and visible focus styles, the progress bar's ARIA value, live feedback/result announcements, and the reduced-motion media query when changing interactions or animations.
