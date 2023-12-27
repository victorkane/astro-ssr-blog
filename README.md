# Astro SSR Blog

## Ref

- [YT Traversy Media 2023-12-18 Astro Quick Start Course | Build an SSR Blog](https://youtu.be/XoIHKO6AkoM?si=SASPBUTBb5rlnGLx)
- [GH Final Code Astro Blog](https://github.com/bradtraversy/astro-blog)
- [Demo](https://astro-blog-flame.vercel.app/)
- [Course Page](https://www.traversymedia.com/astro-quick-start)
- [Become a Traversy Media Member](https://www.traversymedia.com/offers/2NFSzqDt/checkout)

## Notes

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

### 29:06 - Layout & Slots

### 36:45 - Component Props

### 39:31 - Using Constants

### 42:52 - Navbar & Footer Components

### 46:51 - Custom 404 Page

### 51:18 - Collections & Markdown

### 55:27 - Collection Schema

### 58:17 - Querying Collections

### 01:07:02 - Format & Sort By Date

### 01:12:36 - Article Card Component

### 01:15:52 - Homepage Articles

### 01:25:08 - Most Recent Article

### 01:31:11 - Slug & getStaticPaths

### 01:37:12 - SSR Config & Single Article

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
