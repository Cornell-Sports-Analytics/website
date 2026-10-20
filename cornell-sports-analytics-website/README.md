# Cornell Sports Analytics website

Source for [cornellsportsanalytics.com](https://cornellsportsanalytics.com). It is a plain static site built by GitHub Pages (Jekyll). There is no server and no database, so there is nothing to keep running.

Everything below can be done in the GitHub web interface. You do not need to install anything.

## Add a past project

1. Open the `projects` folder in this repository.
2. Click **Add file > Upload files**.
3. Drag in a folder named for the year (for example `2027`) that contains the PDF. If the year folder already exists, open it first and drag in just the PDF.
4. Click **Commit changes**.

After about a minute the PDF appears on the Past projects page under its year. The page sorts itself, so nothing else needs editing.

Name PDFs with lowercase words and dashes, for example `nba-draft-model.pdf`. With no extra details, the page shows the file name as the title.

To show a proper title, authors, and a one-sentence summary, add an entry to `_data/projects.yml`. The example at the top of that file shows the format. The key must match the PDF's file name exactly.

## Update photos

- Landing page photos: save pictures in `assets/images/team/`. They appear on the home page automatically, in file name order, and the first one is shown largest. Use descriptive file names such as `spring-2027-case-competition.jpg`, because the name is used as the photo's description for screen readers.
- Until photos are added, the home page shows plain placeholder tiles.
- Keep each photo under about 1 MB so the page loads quickly.

## Update the executive board

Edit `_data/eboard.yml`. Copy a block to add someone, delete a block to remove someone. Save member photos in `assets/images/eboard/` and put the file name in the `photo` field. Update this file every spring when the new board is elected.

## Change the contact details

Edit `_config.yml`. Set `contact_email` and the social links. Lines left empty are hidden.

## Handoff checklist for outgoing officers

The site only survives if these things are passed on each year.

- **Domain.** cornellsportsanalytics.com is registered at Porkbun. Add a shared club email as a contact on the Porkbun account, turn on auto-renew, and make sure the payment card on file will not expire. Hand the Porkbun login to the incoming president.
- **GitHub.** This repository belongs to the Cornell-Sports-Analytics organization, not to a person. Make sure at least two current officers are organization owners, and remove graduated members.
- **Recovery codes.** Store the two-factor recovery codes for Porkbun and GitHub somewhere officers can reach, such as a shared password manager.
- **This README.** If something here is out of date, fix it.

## One-time setup (already done if the site is live)

### 1. Publish from GitHub

In the repository go to **Settings > Pages**. Under **Build and deployment**, choose **Deploy from a branch**, then branch `main` and folder `/ (root)`.

Under **Custom domain**, enter `cornellsportsanalytics.com` and save. The `CNAME` file in this repository already holds the domain, so do not delete it.

### 2. Point the domain at GitHub (Porkbun)

In Porkbun, open **Domain Management**, then **DNS** for cornellsportsanalytics.com. New domains come with default parking records whose value is `pixie.porkbun.com`. Delete those first, because they conflict with the records below.

Then add these records:

| Type | Host | Answer |
| --- | --- | --- |
| A | (leave blank) | 185.199.108.153 |
| A | (leave blank) | 185.199.109.153 |
| A | (leave blank) | 185.199.110.153 |
| A | (leave blank) | 185.199.111.153 |
| CNAME | www | cornell-sports-analytics.github.io |

Optionally add four AAAA records on the blank host for IPv6: `2606:50c0:8000::153`, `2606:50c0:8001::153`, `2606:50c0:8002::153`, and `2606:50c0:8003::153`.

DNS changes can take up to 24 hours. When GitHub's Pages settings show the DNS check as passed, tick **Enforce HTTPS**.

### 3. Verify the domain (recommended)

In the Cornell-Sports-Analytics organization settings, open **Pages** and add the domain under verified domains. GitHub shows a TXT record to add in Porkbun. Verifying stops anyone else from claiming the domain on GitHub Pages.

## Preview on your own computer (optional)

You need Ruby and Bundler installed.

```
bundle install
bundle exec jekyll serve
```

Then open http://localhost:4000.

## How the site is organized

| Path | What it holds |
| --- | --- |
| `index.html` | Landing page |
| `about.html` | About us and executive board |
| `projects.html` | Past projects page (builds itself from `projects/`) |
| `contact.html` | Contact us |
| `projects/<year>/` | Project PDFs |
| `_data/` | Editable lists: navigation, executive board, project details |
| `assets/` | Styles, photos, icon |
| `_layouts/`, `_includes/` | Shared page frame, header, and footer |
| `_config.yml` | Site settings and contact details |
