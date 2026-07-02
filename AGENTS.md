# 🏗 Project Workflow & Architecture Guide (High Signal Facts)

### 🚀 Setup & Development Cycle
*   **Initial Setup:** Always run `bundle install` first to ensure all Jekyll dependencies and gems are installed before running the server.
*   **Local Dev Server:** Use `bundle exec jekyll serve --host localhost` when developing, ensuring execution is performed from the root of the blog structure where the build process initiates.
*   **Production Testing:** To simulate a production environment accurately, explicitly set the environment variable: `JEKYLL_ENV=production bundle exec jekyll serve --host localhost`.

### 🧱 Architectural Quirks & Conventions
*   **Theming Dependency:** The site relies on a specific remote theme version. Manual updates or attempts to use conflicting themes must account for this dependency lock.
*   **Multilingual Data Structure:** Localization and UI text are managed using YAML files found under `docs/_data/`. Changes to available languages require updating structures in these specific data files (e.g., `docs/_data/ui-text.yml`).

### ⚠️ Developer Gotchas
*   **Testing Environment:** The codebase is a static site built by Jekyll/Liquid. "Running tests" means validating the build process; confirm successful compilation using the commands above, not unit testing source code libraries for business logic (which are minimal).

### ✍️ Content Creation Guidelines
*   **AI Content Assistance:** When generating or editing blog posts, consider that this is a static Jekyll site. AI assistance should focus on content creation and refinement. AI assistance should NOT generate huge tool calls. A blog post should ideally not surpass 5000 characters.
*   **Blog Post Generation:** When tasked with writing a new blog post, first read several existing posts in `docs/_posts/` to understand and emulate the established writing style and format.
*   **Post ID and permalink:** A new blog post must have an ID and permalink in its front matter. The ID must follow an incremental numbering sequence based on the last published post's ID (e.g., if the last post's ID is 37, the next one should be 38). The ID does not contain text; it is a number. The permalink is of the format /archives/ID. The last blog post is the last file under `docs/_posts/` and its front matter contains the post's ID and permalink.
*   **Post slug:** New blog post slugs should follow the pattern of previous blog posts, i.e., with a date prefix and then a short title with hyphens. The format of the slug is thus YYYY-MM-DD-hyphenated-title. If the date is not given by the user's context, then use today's date.
*   **Post assets:** Assets like PDFs or images, should be copied into a sub-folder under the `assets` folder. The sub-folder is typically named after the slug of the post that references it.
*   **Presentation posts:** If the blog post is about a Devstaff presentation, follow the ideal example of the 2025-02-13-developer-academia.md blog post, otherwise follow the ideal example of the 2023-06-11-devoxx-greece-elasticsearch-presentation.md blog post for presentations. The front matter should have a similar format as the example blog post, including a new ID and permalink, and the post should similarly write a few words about the venue, the title of the presentation, its abstract, reference a downloadable link of the slides .pdf asset, embed a Youtube public recording, and the agenda.