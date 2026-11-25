# Our Travel Journal – GitHub Pages setup

A static scrapbook site. Everything (pages, photos, music) lives in your GitHub repo. No server needed.

## How it works
- **Visitors/friends**: just open the link. They see the journal, hear the music, and comment on photos.
- **You (owner)**: tap 🔑 Admin, paste a GitHub token, and then you can add pages, photos, captions, and music. Changes are saved straight into the repo (`data.json`, `photos/`, `music/`) and go live in about a minute.
- **Comments**: use giscus, which stores comments in your repo's GitHub Discussions. Friends sign in with GitHub to comment.

## Step 1 – Create the repo
1. Go to github.com → **New repository**. Name it e.g. `travel-journal`. Make it **Public** (needed for free GitHub Pages and giscus).
2. Tick "Add a README" so the `main` branch exists.
3. Click **Add file → Upload files**, drag in `index.html` and `data.json`, and commit.

## Step 2 – Turn on GitHub Pages
Repo → **Settings → Pages** → Source: **Deploy from a branch** → Branch: `main`, folder `/ (root)` → Save.
After a minute your site is at `https://YOUR-USERNAME.github.io/travel-journal/`.

## Step 3 – Create your owner token
1. GitHub → profile picture → **Settings → Developer settings → Personal access tokens → Fine-grained tokens → Generate new token**.
2. Repository access: **Only select repositories** → pick `travel-journal`.
3. Permissions → Repository permissions → **Contents: Read and write**.
4. Generate and copy the token (starts with `github_pat_`).
5. Open your site → tap **🔑 Admin** → paste → Save.

The token is kept only in your browser. Never share it. Friends never need it.

## Step 4 – Add content
Once logged in as admin you will see **+ Add page**, **🎵 Music**, and **🗑 Page**.
- Tap any empty frame to upload a photo. Edit captions and page titles directly.
- Tap **🎵 Music** on a page (or on the cover) to upload an .mp3 for that page. Music switches when you flip pages; the 🔊 button mutes it.
- Browsers block autoplay until a tap, so music starts after the first tap on → or "Open journal".

## Step 5 – Turn on comments (giscus)
1. Repo → **Settings → General → Features** → tick **Discussions**.
2. Install the giscus app: https://github.com/apps/giscus → select your repo.
3. Go to https://giscus.app, enter `YOUR-USERNAME/travel-journal`, pick a Discussion category (create one called "Comments", type *Announcement*), and set Mapping to "Specific term".
4. giscus.app shows `data-repo-id` and `data-category-id`. Copy them.
5. In `index.html`, find the `CONFIG` block near the top of the script and fill in:
   ```js
   giscus:{repo:'YOUR-USERNAME/travel-journal',repoId:'R_xxxx',category:'Comments',categoryId:'DIC_xxxx'}
   ```
6. Commit the change. Now tapping any photo opens it large with a comment box beneath it.

## Notes
- Photos are resized to ~1400px before upload to keep the repo small. Keep music files under ~20 MB (GitHub's hard limit is 100 MB per file, and repos should stay under ~1 GB).
- After you save, GitHub Pages takes about 1 minute to publish. You see your own changes instantly in your browser.
- Want it private? Use a private repo with GitHub Pro/Team Pages, but giscus comments then won't work for outsiders.
- Custom domain: set `owner` and `repo` manually in `CONFIG` since they're auto-detected only from `*.github.io` URLs.
