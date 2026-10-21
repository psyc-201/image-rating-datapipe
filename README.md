# Animal typicality experiment (jsPsych + DataPipe + GitHub Pages)

Participants see 12 animals and use a slider to rate how typical each one is.
It uses the same pieces as the jsPsych Tutorial Sheets 0–2, plus two new steps:

- **GitHub Pages** puts the experiment online, so participants can open it with a link.
- **DataPipe** saves each participant's data as a `.csv` file in your UCSD Google Drive.

All of the experiment code is in **`index.html`**. Lines marked `NEW` are the
only things the tutorials did not cover.

## 1. Make your own copy

1. On this page, click **Use this template** → **Create a new repository**.
   Owner: your account. Leave it **Public**. Click **Create repository**.
2. Click **Code** → **Open with GitHub Desktop** → **Clone**.

## 2. Try it on your laptop

Double-click **`index.html`**. It opens in your browser. At the end you will
see your data on the screen, just like in the tutorials.

## 3. Put it online

1. On your repository's GitHub page: **Settings** → **Pages**.
2. Source: **Deploy from a branch**. Branch: **main**, folder **/ (root)**.
   Click **Save**.
3. After a minute or two, reload. Your link appears at the top:
   `https://YOUR-USERNAME.github.io/YOUR-REPO-NAME/`

Every time you push from GitHub Desktop, the website updates within a few minutes.

## 4. Save data with DataPipe

Use your **UCSD email** for all of these steps.

1. Go to <https://pipe.jspsych.org> and **Sign up** with your `@ucsd.edu` email.
2. **Account Settings** → **Storage Providers** → **Connect** next to **Google Drive**.
   - Sign in with your `@ucsd.edu` address. You go to the UCSD login page:
     log in and approve Duo, the same as for Canvas.
   - If Google offers a personal Gmail account instead, click
     **Use another account** and type your `@ucsd.edu` address.
   - Click **Allow**. DataPipe can only see the files it creates.
3. Click **New Experiment** → **Google Drive** → give it a title → **Create**.
4. Copy the **experiment ID** (12 letters and numbers) from the dashboard.
5. In `index.html`, paste it in place of `PASTE_YOUR_ID_HERE`. Keep the quotes.
   Save, then **Commit** and **Push** in GitHub Desktop.
6. On the DataPipe dashboard, turn on **Accept new data**.
7. Do the experiment once at your `github.io` link. A new `.csv` file should
   appear in your Google Drive, under `My Drive/DataPipe`.

From now on, every run saves a file, including your own tests. Delete test
files before you collect real data.

## 5. Analyze the data

Double-click **`image-rating-datapipe.Rproj`** to open RStudio, open
**`analysis/analyze-ratings.qmd`**, and click **Render**.

It uses the practice files in `data/example/`. For real data, download your
files from Google Drive into a folder called `data/raw/`, and change
`"example"` to `"raw"` in the document. (`data/raw/` is never uploaded to
GitHub. Participant data should not go in a public repository.)

## Stuck?

- **Blank page:** Open the console (Chrome: View → Developer → JavaScript
  Console). The red error usually names the line, often a missing comma or quote.
- **No file in Google Drive:** Check that **Accept new data** is on and that
  the ID in `index.html` matches your dashboard.
- **Google says the app is blocked:** Tell your TA. Don't switch to a personal Gmail.
- **Website shows an old version:** Wait a few minutes and reload. Check that
  you pushed.

## Images

The animal images are the public-domain (CC0) images from THINGSplus:
Stoinski, Perkuhn & Hebart (2023), *Behavior Research Methods*,
<https://osf.io/jum2f/>. THINGSplus also published typicality norms for these
animals, in case you want to compare your results to theirs.
