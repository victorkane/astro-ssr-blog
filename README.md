# Astro SSR Blog

## Ref

- [YT Traversy Media 2023-12-18 Astro Quick Start Course | Build an SSR Blog](https://youtu.be/XoIHKO6AkoM?si=SASPBUTBb5rlnGLx)
- [GH Final Code Astro Blog](https://github.com/bradtraversy/astro-blog)
- [Demo](https://astro-blog-flame.vercel.app/)
- [Course Page](https://www.traversymedia.com/astro-quick-start)
- [Become a Traversy Media Member](https://www.traversymedia.com/offers/2NFSzqDt/checkout)

- [ ] Create branch `use/ui-shadcn` using [shadcn for astro](https://ui.shadcn.com/docs/installation/astro) instead of [flowbite](https://flowbite.com/)

## Notes on first run-through

### 7:35 Install and Setup

- Create initial Astro project
- Make sure recommended Astro VS Code extension is enabled for user and/or workspace

```bash
commit d9bc9edc14ba04894d13707af8873c4ddbc2892d (HEAD -> master)
Author: victorkane <victorkane@gmail.com>
Date:   Wed Dec 27 12:21:56 2023 -0300

    Initial commit
```

- Add Tailwind Integration

```bash
victor@victorpc:astro-ssr-blog$ npx astro add tailwind
✔ Resolving packages...
12:33:08
  Astro will run the following command:
  If you skip this step, you can always run it yourself later

 ╭──────────────────────────────────────────────────────────╮
 │ npm install @astrojs/tailwind@^5.0.4 tailwindcss@^3.4.0  │
 ╰──────────────────────────────────────────────────────────╯

✔ Continue? … yes
✔ Installing dependencies...
12:33:36
  Astro will generate a minimal ./tailwind.config.mjs file.

✔ Continue? … yes
12:33:40
  Astro will make the following changes to your config file:

 ╭ astro.config.mjs ─────────────────────────────╮
 │ import { defineConfig } from 'astro/config';  │
 │                                               │
 │ import tailwind from "@astrojs/tailwind";     │
 │                                               │
 │ // https://astro.build/config                 │
 │ export default defineConfig({                 │
 │   integrations: [tailwind()]                  │
 │ });                                           │
 ╰───────────────────────────────────────────────╯

✔ Continue? … yes
12:33:42
   success  Added the following integration to your project:
  - @astrojs/tailwind
victor@victorpc:astro-ssr-blog$
```

- Make Sure tailwindcss VS Code extension is enabled

```bash
victor@victorpc:astro-ssr-blog$ cat .vscode/extensions.json
{
  "recommendations": ["astro-build.astro-vscode", "bradlc.vscode-tailwindcss"],
  "unwantedRecommendations": []
}
```

- Test Tailwind install

### 12:27 - Pages Folder & Routing

- File based routing
- Scaffold home page with fully functioning html mockup

```bash
commit 1788e839d72e074a64f23fae2ecfdd6f542e031b (HEAD -> main, origin/main)
Author: victorkane <victorkane@gmail.com>
Date:   Wed Dec 27 16:59:28 2023 -0300

    fix(home page): successfully removed redundant cdn tailwind depenency

commit 951096f7469eeee3405d09397a583d9f774fe65f
Author: victorkane <victorkane@gmail.com>
Date:   Wed Dec 27 16:53:47 2023 -0300

    build: Scaffold home page with fully functioning html mockup

commit 34f488395b972d6614b44de644d29ede592e80f8
Author: victorkane <victorkane@gmail.com>
Date:   Wed Dec 27 13:11:27 2023 -0300

    chore: scaffold file and folder based routing
```

### 17:26 - Image Component

- `src/` vs `public/` folder for images (see [Astro Docs - Images](https://docs.astro.build/en/guides/images/))
- To avoid problems experienced with Netlify, etc.:
  - article content images: `public/images` (treated as img's as per usual, but leading `/` must figure in path for automatic import (Image's must be imported, and must have width and height attributes (100% for `images`)))
  - article content images are not optimized either, since the import does not occur on the server side (during, for example, SSG) as is the case of log, which is explicitly imported in the component script (server executed "front matter" at top of file); so it is pointless to do what we are doing (using `Image` instead of html `img` element), but we are doing it to be able to show that the alternative does actually exist.
  - site images: logo, etc: `src/images` for importing and using as if they were components, for optimization and other benefits; otherwise they would have to be placed in `public/images` also

### 24:58 - Component Script

- Physical code fence at the top of astro components and pages contains the [Component Script](https://docs.astro.build/en/core-concepts/astro-components/#the-component-script)
- Runs on the server (while executing either SSG or SSR) and not on the client (will not be observable on client side browser)
- Console log not seen in browser but rather in the log running `npm run dev`, for example.
- Concepts explained in video using `src/pages/test.astro` not present in repo

### 29:06 - Layout & Slots

- [Astro Docs. Layouts](https://docs.astro.build/en/core-concepts/layouts/)
- Added support for prettier

```
commit 1d1c3037bb0e6ca536480e35f0dd5651c1acc87f (HEAD -> main)
Author: victorkane <victorkane@gmail.com>
Date:   Thu Dec 28 10:28:03 2023 -0300

    build(editor): add prettier support for astro files

 .prettierignore   | 13 +++++++++++++
 .prettierrc       | 23 +++++++++++++++++++++++
 package-lock.json | 63 +++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
 package.json      |  4 ++++
 4 files changed, 103 insertions(+)
```

- Extracted Main Layout from home page and applied it to home, about and articles listing pages reachable from navbar

```bash
commit b793cb03ea9dc87494bd1f47050293f515c68cb1 (HEAD -> main, origin/main)
Author: victorkane <victorkane@gmail.com>
Date:   Thu Dec 28 10:43:50 2023 -0300

    Extract Main Layout from home page and apply it to home, about and articles listing pages navigable from navbar

 README.md                      |  28 +++++++++-
 src/layouts/MainLayout.astro   | 149 +++++++++++++++++++++++++++++++++++++++++++++++++
 src/pages/about.astro          |   9 ++-
 src/pages/articles/index.astro |   9 ++-
 src/pages/index.astro          |  86 ++--------------------------
 5 files changed, 196 insertions(+), 85 deletions(-)
```

#### 33:35 Migrate content for articles and about page from blog-theme html mockup to Astro pages

```bash
commit fe425c7218fa3179bdaa029673cd7f651141b9a0 (HEAD -> main, origin/main)
Author: victorkane <victorkane@gmail.com>
Date:   Thu Dec 28 16:23:06 2023 -0300

    feat(flesh out pages): Migrate content for articles and about page from blog-theme html mockup to Astro pages

 README.md                      |  17 ++++
 src/pages/about.astro          |  55 ++++++++++++-
 src/pages/articles/index.astro | 212 ++++++++++++++++++++++++++++++++++++++++++++++++-
 3 files changed, 280 insertions(+), 4 deletions(-)
```

### 36:45 - Component Props

- [Astro Docs. Component Props](https://docs.astro.build/en/core-concepts/astro-components/#component-props)

```bash
commit 2ebb0f1cd79ff248ea77e2b6abb1c9a60663e077 (HEAD -> main, origin/main)
Author: victorkane <victorkane@gmail.com>
Date:   Thu Dec 28 16:56:29 2023 -0300

    chore(component props): add component prop for title for main site pages

 README.md                    |   2 +
 src/layouts/MainLayout.astro |  41 ++--
 src/pages/about.astro        |   2 +-
 src/pages/index.astro        | 583 +++++++++++++++++++++++++--------------------------
 4 files changed, 308 insertions(+), 320 deletions(-)
```

### 39:31 - Using Constants

```bash
commit 97954f1dfa8aa7f5bd86e92fd5e97a320e0f019f (HEAD -> main, origin/main)
Author: victorkane <victorkane@gmail.com>
Date:   Fri Dec 29 07:57:39 2023 -0300

    chore: using site-wide configuration constants

 src/constants.ts             | 5 +++++
 src/layouts/MainLayout.astro | 4 +++-
 2 files changed, 8 insertions(+), 1 deletion(-)
```

### 42:52 - Navbar & Footer Components

```bash
commit 8fa1b1b105f5f77af69f19b11b9be601b9d3c2be (HEAD -> main)
Author: victorkane <victorkane@gmail.com>
Date:   Fri Dec 29 08:39:08 2023 -0300

   build(types): (optional) types for some props

src/layouts/MainLayout.astro | 4 ++++
1 file changed, 4 insertions(+)

commit e9301dd12eb3618b78af9ae65625c0f95bfe17a0
Author: victorkane <victorkane@gmail.com>
Date:   Fri Dec 29 08:21:56 2023 -0300

   chore(layout components): abstract out Navbar and Footer components

.vscode/settings.json        |   1 +
src/components/Footer.astro  |  62 +++++++++++++++++++++++++
src/components/Navbar.astro  |  62 +++++++++++++++++++++++++
src/layouts/MainLayout.astro | 128 ++-------------------------------------------------
src/pages/index.astro        |  63 -------------------------
5 files changed, 130 insertions(+), 186 deletions(-)
```

- Generate TypeScript types for all Astro modules (in `src/env.d.ts`). See [astro sync. Astro Docs](https://docs.astro.build/en/reference/cli-reference/#astro-sync)

```bash
victor@victorpc:astro-ssr-blog$ npx astro sync
```

### 46:51 - Custom 404 Page

```bash
commit 7f438ca6a775d473dcd940bd807a3b9fde4a89d9 (HEAD -> main)
Author: victorkane <victorkane@gmail.com>
Date:   Fri Dec 29 09:02:08 2023 -0300

    feat: add custom 404 page

 src/pages/404.astro | 16 ++++++++++++++++
 1 file changed, 16 insertions(+)
```

### 51:18 - Collections & Markdown / 55:27 - Collection Schema / 58:17 - Querying Collections

- File-based content modeling in Astro!
- [ ] Test with CMS [Front Matter](https://frontmatter.codes/)
- Ref [Content Collections. Astro Docs](https://docs.astro.build/en/guides/content-collections/)
- If necessary (red line under `astro:content` in import statement) run `astro sync`:

```bash
victor@victorpc:astro-ssr-blog$ npx astro sync
11:26:02 [types] Added src/env.d.ts type declarations
11:26:02 Types generated 198ms
```

- Scaffold blog listing page

```bash
commit 8c9f42a56453417d453a77168abb3815918b28f2 (HEAD -> main)
Author: victorkane <victorkane@gmail.com>
Date:   Fri Dec 29 11:58:54 2023 -0300

    chore(blog collection): scaffold articles listing page querying actual blog collection

 README.md                                          |  24 +++-
 src/content/blog/best-laptops-for-developers.md    |  40 ++++++
 src/content/blog/cannon-excellence.md              |  52 +++++++
 src/content/blog/cutting-edge-tablets.md           |  52 +++++++
 src/content/blog/elevate-your-mobile-experience.md |  52 +++++++
 src/content/blog/guardian-of-the-digital-realm.md  |  54 +++++++
 src/content/blog/immerse-in-the-virtual-world.md   |  52 +++++++
 src/content/blog/world-of-drones.md                |  52 +++++++
 src/content/config.ts                              |  15 ++
 src/env.d.ts                                       |   1 +
 src/pages/articles/index.astro                     | 217 +++++------------------------
 11 files changed, 422 insertions(+), 189 deletions(-)
```

- query real titles from blog collection for articles on listing page

```bash
commit 60114eb05191baadfe77d0cd813322dbd24c0904 (HEAD -> main, origin/main)
Author: victorkane <victorkane@gmail.com>
Date:   Fri Dec 29 13:20:41 2023 -0300

    chore(blog collection): query real titles from blog collection for articles on listing page

 src/pages/articles/index.astro | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)
```

- query all schema items as well as article slug (front matter only) from blog collection for articles on listing page

```bash
commit 17c7f9a5ada2a71b49c2c28f4e1549986f441521 (HEAD -> main, origin/main)
Author: victorkane <victorkane@gmail.com>
Date:   Fri Dec 29 13:29:49 2023 -0300

    chore(blog collection): query all schema items as well as article slug (front matter only) from blog collection for articles on listing page

 src/pages/articles/index.astro | 8 ++++----
 1 file changed, 4 insertions(+), 4 deletions(-)
```

- query and initially format dynamic tag details for each article on articles listing page

```bash
commit 4d7593dbf9d11e0785f0975f21723d69d5e711a0 (HEAD -> main)
Author: victorkane <victorkane@gmail.com>
Date:   Fri Dec 29 13:48:05 2023 -0300

    chore(blog collection): query and initially format dynamic tag details for each article on articles listing page

 README.md                      | 15 +++++++++++++++
 src/pages/articles/index.astro | 17 +++++++++++------
 2 files changed, 26 insertions(+), 6 deletions(-)
```

### 01:07:02 - Format & Sort By Date

- format date according to locale being used on list articles page

```bash
commit 41d0e0847a7f2703fe0a37055b82d366a793c529 (HEAD -> main, origin/main)
Author: victorkane <victorkane@gmail.com>
Date:   Fri Dec 29 15:37:36 2023 -0300

    chore(list articles page): format date according to locale being used

 src/pages/articles/index.astro | 8 +++++++-
 1 file changed, 7 insertions(+), 1 deletion(-)
```

- abstract locale aware date formatting function into reusable utilities file

```bash
commit 4d89df9b109ab5c7da4b985344154fc235a60b7a (HEAD -> main)
Author: victorkane <victorkane@gmail.com>
Date:   Fri Dec 29 15:45:47 2023 -0300

    chore(utils): abstract locale aware date formatting function into reusable utilities file

 README.md                      | 15 +++++++++++++++
 src/pages/articles/index.astro |  7 +------
 src/utils.ts                   |  7 +++++++
 3 files changed, 23 insertions(+), 6 deletions(-)
```

- sort article publishing dates in descending order on list articles page

```bash
commit 9c4c67659a37b5f6305e0cba67c87476561df8ea (HEAD -> main)
Author: victorkane <victorkane@gmail.com>
Date:   Fri Dec 29 15:57:23 2023 -0300

    feat(article listing page): sort article publishing dates in descending order on list articles page

 src/pages/articles/index.astro | 5 ++++-
 1 file changed, 4 insertions(+), 1 deletion(-)
```

### 01:12:36 - Article Card Component

```bash
commit 5c0e3c7d98915b234489052e452d1e4a49de98c1 (HEAD -> main)
Author: victorkane <victorkane@gmail.com>
Date:   Fri Dec 29 17:12:57 2023 -0300

    chore(components): add Article Card component

 src/components/ArticleCard.astro | 43 +++++++++++++++++++++++++++++++++++++++++++
 src/pages/articles/index.astro   | 38 ++------------------------------------
 2 files changed, 45 insertions(+), 36 deletions(-)
```

### 01:15:52 - Homepage Articles

```bash
commit f7775e7b993c182ee5de44edcabf22b37a4a58ef (HEAD -> main)
Author: victorkane <victorkane@gmail.com>
Date:   Fri Dec 29 18:04:36 2023 -0300

    chore(homepage): render main grid  articles dynamically using ArticleCard component

 src/pages/index.astro | 193 ++++++----------------------------------------------------
 1 file changed, 20 insertions(+), 173 deletions(-)
```

### 01:25:08 - Most Recent Article

```bash
commit 2232209e051443a6246418da5678aeb8798beb60 (HEAD -> main)
Author: victorkane <victorkane@gmail.com>
Date:   Fri Dec 29 19:33:25 2023 -0300

    chore(homepage): render most recent article dynamically using MostRecentArticle component

 src/components/MostRecentArticle.astro | 40 ++++++++++++++++++++++++++++++++++++++++
 src/pages/index.astro                  | 31 ++-----------------------------
 2 files changed, 42 insertions(+), 29 deletions(-)
```

### 01:31:11 - Slug & getStaticPaths

- For single article page
- For static websites, you use `getStaticPaths()`
- In next section we will move over to server side rendering (SSR), which handles things differently
- In this section, we will use the static approach, just to see what that is like
- fix ArticleCard component: prefix link path with proper routing path (`/articles/`)

```bash
commit 281e1aaf31d9ca78dde6aa398dbdbb381f6224f7 (HEAD -> main, origin/main)
Author: victorkane <victorkane@gmail.com>
Date:   Sat Dec 30 09:17:55 2023 -0300

    fix(ArticleCard component): prefix link path with proper routing path

 src/components/ArticleCard.astro | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)
```

### 01:37:12 - SSR Config & Single Article

- In this section we will move over to server side rendering (SSR), which requires special Astro configuration and changing our code for the single article page

### 01:47:30 - Tags Component

### 01:53:18 - Tag Page

### 01:59:34 - Footer Tags

### 02:04:29 - Search Page

### 02:16:15 - API Endpoints

### 02:25:55 - Pagination Component

### 02:34:05 - Disable Prev & Next

### 02:39:36 - Vercel Deployment

## Astro Starter Kit: Minimal (from typical Astro installation)

```sh
npm create astro@latest -- --template minimal
```

[![Open in StackBlitz](https://developer.stackblitz.com/img/open_in_stackblitz.svg)](https://stackblitz.com/github/withastro/astro/tree/latest/examples/minimal)
[![Open with CodeSandbox](https://assets.codesandbox.io/github/button-edit-lime.svg)](https://codesandbox.io/p/sandbox/github/withastro/astro/tree/latest/examples/minimal)
[![Open in GitHub Codespaces](https://github.com/codespaces/badge.svg)](https://codespaces.new/withastro/astro?devcontainer_path=.devcontainer/minimal/devcontainer.json)

> 🧑‍🚀 **Seasoned astronaut?** Delete this file. Have fun!

## 🚀 Project Structure

Inside of your Astro project, you'll see the following folders and files:

```text
/
├── public/
├── src/
│   └── pages/
│       └── index.astro
└── package.json
```

Astro looks for `.astro` or `.md` files in the `src/pages/` directory. Each page is exposed as a route based on its file name.

There's nothing special about `src/components/`, but that's where we like to put any Astro/React/Vue/Svelte/Preact components.

Any static assets, like images, can be placed in the `public/` directory.

## 🧞 Commands

All commands are run from the root of the project, from a terminal:

| Command                   | Action                                           |
| :------------------------ | :----------------------------------------------- |
| `npm install`             | Installs dependencies                            |
| `npm run dev`             | Starts local dev server at `localhost:4321`      |
| `npm run build`           | Build your production site to `./dist/`          |
| `npm run preview`         | Preview your build locally, before deploying     |
| `npm run astro ...`       | Run CLI commands like `astro add`, `astro check` |
| `npm run astro -- --help` | Get help using the Astro CLI                     |

## 👀 Want to learn more?

Feel free to check [our documentation](https://docs.astro.build) or jump into our [Discord server](https://astro.build/chat).
