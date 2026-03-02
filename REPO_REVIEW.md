# Repository Review and Improvement Suggestions

## Quick strengths
- Single-file apps are easy to host on GitHub Pages and easy to use offline.
- The landing page already provides direct-open and direct-download actions for each app.
- The quiz apps persist progress in `localStorage`, which improves usability for repeat practice.

## High-impact improvements

1. **Reduce duplication by extracting shared quiz logic**
   - The app files currently embed their own HTML/CSS/JS in each page.
   - Introduce a small shared runtime (`assets/quiz-core.js` and `assets/quiz-theme.css`) and keep each app-specific file as question data + metadata.
   - Benefits: faster feature rollout (flagging, search, score logic, keyboard support), fewer bug-fix touchpoints, easier QA.

2. **Add a root `README.md` for contributors and users**
   - Document app purpose, local run instructions, deployment flow, and where question data lives.
   - Include a small “how to add a new MCQ app” checklist.
   - Benefits: easier onboarding, fewer one-off questions, consistent updates.

3. **Introduce basic automated checks**
   - Add lightweight CI with HTML validation and formatting checks (for example, `htmlhint`, `prettier --check`, and optional link check).
   - Benefits: catches structural regressions early and keeps a consistent code style.

4. **Improve accessibility baseline**
   - Add clear focus states for interactive controls, skip-link support, and semantic labeling for question/answer regions.
   - Ensure color contrast and keyboard navigation are validated.
   - Benefits: better usability for keyboard and assistive-tech users; more robust UI quality.

5. **Separate question banks from app shell**
   - Move MCQ content into structured data files (JSON or JS modules) and load into a common renderer.
   - Add a content schema to validate each question object (`id`, `topic`, `stem`, `options`, `answer`, `rationales`).
   - Benefits: safer content updates and easier bulk editing/review.

6. **Add import/export for learner progress**
   - Keep `localStorage` as default but add buttons to export/import progress JSON.
   - Benefits: progress backup, device migration, and easier troubleshooting.

7. **Version and date-stamp medical content updates**
   - Add visible “last reviewed” and “content version” fields for each app.
   - Benefits: clearer trust signals for learners and easier governance for guideline updates.

## Suggested implementation order
1. Add `README.md` and basic CI checks.
2. Extract shared CSS/JS core and migrate one app as a pilot.
3. Move question banks to data files + schema validation.
4. Add accessibility improvements and keyboard test pass.
5. Add progress import/export and content versioning UI.
