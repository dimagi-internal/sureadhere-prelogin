# SureAdhere site: edit, preview, and publish (no code required)

This guide is for non-technical teammates. You can make a change to the
SureAdhere marketing site, see it in a private preview, and publish it to the
live site **without writing code or using the command line**.

There are two ways to do it:

- **The easy way (recommended): just ask Claude.** You describe the change in
  plain language; Claude does all the GitHub work and hands you a preview link
  and a merge button. You never open github.com. Start here.
- **The manual way (fallback):** do the steps yourself in the GitHub website.
  Use this only if Claude isn't available. It's further down under
  "Manual fallback."

---

## The easy way: ask Claude (recommended)

This is the standard way to edit the site. Open a Claude session on the
`sureadhere/marketing` repo and just talk to it.

1. **Describe your change** in plain language, for example:
   > "On the homepage, change the headline to 'adherence matters' and remove
   > the word 'most'."
2. **Claude makes the change and prepares it.** It edits the file, saves it on
   a safe branch, and opens a proposed change (a "pull request") for you. You
   don't touch GitHub.
3. **Claude sends you a preview link.** Within a minute or so, Claude posts a
   private preview link (it ends in `.workers.dev`). Click it and confirm the
   change looks right.
4. **Claude shows you a publish button.** You'll see a choice like
   **"Publish this change?"** with **Merge now** / **Not yet**. Click
   **Merge now** when you're happy.
5. **It goes live.** Claude publishes the change; the live site updates within a
   minute or two. If you still see the old version, do a hard refresh
   (**Cmd+Shift+R** on Mac, **Ctrl+Shift+R** on Windows).

That's it. If the preview doesn't look right, just tell Claude what to fix and
it will update the same change and send a new preview.

> **What you need:** access to a Claude session pointed at the
> `sureadhere/marketing` repo. Ask your engineering contact to set this up if
> you don't have it.

---

## Manual fallback: do it yourself on GitHub

Use this only if you can't use Claude. It does the same three things by hand:
**edit → preview → publish**, entirely in your web browser.

> Throughout this section, *"the repo"* means the project's files on GitHub at
> **https://github.com/sureadhere/marketing**. A *"PR" (pull request)* is just a
> proposed set of changes that you review before they go live.

**What you need:** a **GitHub account** with access to the repo, and (optional
but recommended) a **Cloudflare dashboard** login to see the preview. Ask your
engineering contact for both.

### Step 1 — Edit a page

1. Go to **https://github.com/sureadhere/marketing**.
2. Open the file you want to change. The site's pages live in folders, for
   example:
   - Homepage: `index.html`
   - Clinical Trials page: `clinical-trials/index.html`
   - Behavioral Health page: `behavioral-health/index.html`
   - (Each section has its own folder with an `index.html` inside.)
3. Click the **pencil icon** (✏️ "Edit this file") in the top-right of the file
   view.

   > 📸 *Screenshot: the pencil/Edit icon on a file page.*

4. Make your text change directly in the editor. For simple wording changes,
   find the text and type over it. (For anything involving layout, images, or
   new pages, ask your engineering contact or start an AI-assisted session
   instead of editing by hand.)
5. When done, scroll down to the **"Commit changes"** box (or click the green
   **Commit changes...** button, top-right).
6. In the dialog:
   - Write a short description of what you changed (e.g. "Update homepage
     stat to 99%").
   - Choose **"Create a new branch for this commit and start a pull request."**
     Give the branch a simple name (e.g. `update-homepage-stat`).
   - Click **Propose changes**, then **Create pull request** on the next
     screen.

   > 📸 *Screenshot: the "Commit changes" dialog with "Create a new branch"
   > selected.*

You've now created a **pull request (PR)** — a proposed change that is *not yet
live*. Next you'll preview it.

---

### Step 2 — Preview your change

You have two ways to preview, depending on what's set up. Use whichever is
available to you.

#### Option A (recommended): Cloudflare preview

When the repo is connected to **Cloudflare Workers Builds**, every pull request
automatically gets its own private preview link.

1. Log in at **https://dash.cloudflare.com**.
2. Go to **Workers & Pages**, then open the **`marketing`** project.
3. Click the **Builds** (or **Deployments**) tab.
4. Find the build that matches your pull request. Click it.
5. Open the **preview URL** it shows (it ends in `.workers.dev`).

   > 📸 *Screenshot: the Builds tab with a preview build and its preview URL.*

This preview shows your change exactly as it will look live, without affecting
the real site.

#### Option B: ask for a preview link in the PR

If you don't have Cloudflare access, post a comment on your pull request asking
your engineering contact (or the AI assistant watching the PR) to share the
preview link. The same Cloudflare preview can be opened by anyone with access.

> **Tip:** If a preview looks out of date, refresh the page. If it still looks
> wrong, do a "hard refresh": **Ctrl+Shift+R** (Windows) or **Cmd+Shift+R**
> (Mac). Browsers cache styling, so this forces the newest version to load.

---

### Step 3 — Publish (make it live)

When the preview looks right:

1. Go back to your pull request on GitHub.
2. Make sure any automatic checks at the bottom show green checkmarks. If
   something is red, ask your engineering contact before continuing.
3. Click the green **Merge pull request** button, then **Confirm merge**.

   > 📸 *Screenshot: the green "Merge pull request" button.*

4. (Optional) Click **Delete branch** afterward to keep things tidy. This does
   not affect the live site.

Merging publishes your change. The live site updates automatically within a
couple of minutes.

---

### After publishing: confirm it's live

1. Wait 1–2 minutes for the site to rebuild.
2. Open the live site and check your change.
3. If you still see the old version, do a **hard refresh**
   (**Ctrl+Shift+R** / **Cmd+Shift+R**) or open the page in a private/incognito
   window. Styling and images are cached by your browser and by the network, so
   a fresh load is sometimes needed.

---

## Quick glossary

| Term | Plain meaning |
| --- | --- |
| Repo / repository | The folder of all the site's files on GitHub. |
| Branch | A safe copy of the files where your change lives until it's published. |
| Commit | A saved change with a short description. |
| Pull request (PR) | A proposed change you review before it goes live. |
| Merge | The button that publishes a pull request to the live site. |
| Preview / build | A private copy of the site showing your change before it's live. |
| Hard refresh | Reloading a page while ignoring the cached (old) version. |

---

## When to ask for help instead of editing yourself

Do these with your engineering contact or an AI-assisted session, not by hand:

- Adding, removing, or renaming a whole page.
- Changing the top navigation menu or the footer (these must stay identical on
  every page).
- Adding or swapping images.
- Editing either privacy policy (English or Chinese) — these are legal
  documents and must be cleared with Dimagi legal first.

For everything else, the three steps above are all you need.
