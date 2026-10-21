# Image rating experiment (jsPsych + DataPipe + GitHub Pages)

A minimal online experiment you can copy and make your own. Participants see
six images, one at a time, and rate how much they like each one from 1 to 7.

When you are done you will have:

- An experiment running at a public web address (hosted free by GitHub Pages)
- Data from each participant saved automatically to your Google Drive (by DataPipe)
- A Quarto document that reads in everyone's data and plots the ratings

## How the pieces fit together

```
  your laptop                GitHub                 participant            DataPipe            Google Drive
 ─────────────   push    ──────────────   visits   ─────────────   sends   ──────────   saves   ─────────────
  index.html    ───────►  GitHub Pages   ───────►   their web      ──────►  pipe.       ──────►  one .csv file
  stimuli/                hosts the                 browser runs   data     jspsych.org          per participant
                          experiment                the experiment
```

This picks up where the jsPsych Tutorial Sheets 0–2 leave off: same jsPsych
pieces (a timeline, plugins, timeline variables, `data` and `on_finish`), plus
the two things the tutorials do not cover: putting the experiment online and
saving the data.

- **jsPsych** is a JavaScript library for building experiments. All of our
  experiment code is in one file: `index.html`.
- **GitHub Pages** turns your repository into a website, so participants can
  open the experiment with a link.
- **DataPipe** receives each participant's data and saves it to your storage.
  We need it because GitHub Pages can *show* a web page but cannot *receive* data.

> **Your data never goes into GitHub.** GitHub holds the experiment code; the
> data goes to your Google Drive. Keep it that way: participant data does not
> belong in a public repository.

---

## Part 1. Make your own copy

You need R, RStudio, GitHub Desktop, and a GitHub account. If you do not have
them yet, do [getting-started-with-r](https://github.com/psyc-201/getting-started-with-r) first.

1. On this repository's GitHub page, click the green **Use this template**
   button, then **Create a new repository**.
2. Owner: **your own account**. Give it a name (e.g., `my-rating-experiment`),
   leave it **Public**, and click **Create repository**.
3. Click **Code** → **Open with GitHub Desktop**, choose where to put the
   folder (e.g., `Documents/GitHub`), and click **Clone**.

## Part 2. Try the experiment on your laptop

Find the folder and **double-click `index.html`**. It opens in your web browser.
Click through it.

At the end, your data appear on screen as a table. That is because the
experiment starts in **testing mode** (`SAVE_DATA = false`), which saves
nothing.

Now open `index.html` in a text editor to read the code. **RStudio works
fine**: File → Open File. You can also use [VS Code](https://code.visualstudio.com/).
Read it top to bottom; the comments explain each step.

Try one change: edit the welcome message, save the file, and **reload** the
page in your browser. Your change is there.

## Part 3. Put it online with GitHub Pages

1. On *your* repository's GitHub page, go to **Settings** → **Pages** (left
   sidebar).
2. Under **Build and deployment**, set **Source** to **Deploy from a branch**,
   choose the branch **main** and the folder **/ (root)**, and click **Save**.
3. Wait a minute or two, then reload the page. A link appears at the top:
   `https://YOUR-USERNAME.github.io/YOUR-REPO-NAME/`

Open the link. It is the same experiment, now on the internet. Every time you
push a change from GitHub Desktop, the website updates within a minute or two.

## Part 4. Save data with DataPipe

### 4a. Create the DataPipe experiment

Use your **UCSD email** for everything in this part. Your data then live in
your UCSD Google Drive, behind UCSD login.

1. Go to <https://pipe.jspsych.org> and click **Sign up**. Make an account
   with your `@ucsd.edu` email address and a new password. (This is a
   DataPipe password, not your UCSD password.)
2. **Connect your UCSD Google Drive.** Click **Account Settings** →
   **Storage Providers**, then **Connect** next to **Google Drive**.
   - Google's sign-in page opens. Type your `@ucsd.edu` address and click
     **Next**.
   - You are sent to the **UCSD single sign-on page**. Log in with your UCSD
     username and password, and approve the Duo prompt, the same way you log
     in to Canvas.
   - **Check the account.** If Google is already signed in to a personal
     Gmail, it may offer that one. Click **Use another account** and type
     your `@ucsd.edu` address instead.
   - Google asks whether to let DataPipe *see, edit, create, and delete only
     the specific Google Drive files you use with this app*. Click
     **Continue** / **Allow**. DataPipe can only touch the files it creates;
     it cannot see anything else in your Drive.
   - You land back on DataPipe. A green **Connected** label means it worked.
3. Click **New Experiment**, choose **Google Drive**, give it a title, and
   click **Create**. DataPipe makes a folder for it in your UCSD Drive, under
   `My Drive/DataPipe`.
4. Your dashboard now shows an **experiment ID**: 12 letters and numbers.
   Copy it.

### 4b. Connect your experiment to DataPipe

Open `index.html` and change the two lines at the top:

```js
const DATAPIPE_ID = "PASTE_YOUR_ID_HERE";   // ← paste your ID between the quotes
const SAVE_DATA = false;                    // ← change to true
```

Save. In GitHub Desktop, commit (e.g., `Connect to DataPipe`) and click
**Push origin**.

Your experiment ID is not a password. It is fine for it to be in a public
repository.

### 4c. Turn on data collection and test it

1. On your DataPipe dashboard, switch on **Accept new data**. Until you do
   this, DataPipe refuses all data and the experiment ends with
   *"Your data could not be saved."*
2. Wait a minute for GitHub Pages to update, then do the experiment once
   yourself at your `github.io` link.
3. Look in your Google Drive folder. There should be one new `.csv` file named
   after a random participant ID (e.g., `k3j9x0pq2a.csv`).

If you see the file, everything works. Delete your test file before you
collect real data.

## Part 5. Analyze the data

1. Double-click **`image-rating-datapipe.Rproj`** to open the project in RStudio.
2. Open **`analysis/analyze-ratings.qmd`** and click **Render**.

It runs on the practice files in `data/example/`. To analyze real data,
download the `.csv` files from your Google Drive folder into a new folder,
`data/raw/`, and change `"example"` to `"raw"` in the document.

`data/raw/` is listed in `.gitignore`, so GitHub Desktop will not offer to
commit it. Real data stays on your laptop.

---

## Making it your own

All of these are in `index.html`:

| To change... | Edit... |
|---|---|
| The images | Put your images in `stimuli/`, then update both lists: `preload` and `test_stimuli` |
| The question | The `prompt` in `rating_trial` |
| The scale (e.g., 1–5) | The `choices` in `rating_trial`, and the instructions text |
| Image size | `stimulus_height` in `rating_trial` |

The [jsPsych plugin list](https://www.jspsych.org/latest/plugins/list-of-plugins/)
shows the other kinds of screens you can use (sliders, text boxes, surveys,
keyboard responses...). Each plugin's page has an example you can copy.

## Before you collect real data

- **IRB approval and consent.** A real study needs an approved protocol and a
  consent form in place of the welcome screen.
- **Set a session limit** on your DataPipe dashboard, so a shared link cannot
  bring in more participants than you planned.
- **Delete your test files** from the Google Drive folder.
- **Turn off Accept new data** when you finish collecting.

## What is in this repository

```
image-rating-datapipe/
├── index.html                     the whole experiment
├── stimuli/                       the six images participants rate
├── data/
│   └── example/                   3 practice data files (random clicks)
├── analysis/
│   └── analyze-ratings.qmd        read all data files, average, plot
└── image-rating-datapipe.Rproj    open this to start work in RStudio
```

## Stuck?

- **The page is blank.** Open the browser's console (Chrome: View → Developer →
  JavaScript Console) and read the red error. It usually names a line number in
  `index.html`, often a missing comma or quotation mark near your last edit.
- **An image does not appear.** Check that the file name in the `images` list
  matches the file in `stimuli/` exactly. Capital letters count:
  `Dog.png` and `dog.png` are different files on GitHub Pages.
- **My github.io link shows the old version.** Wait two minutes and reload. Check
  that you pushed (GitHub Desktop says *No local changes* and has no
  **Push origin** button).
- **Google says "Access blocked" or "This app is blocked" when I connect
  Drive.** UCSD's Google settings are refusing DataPipe for your account. Do
  not switch to a personal Gmail; tell your TA or Bria.
- **My files went to the wrong Google account.** In DataPipe, go to
  **Account Settings** → **Storage Providers**, click **Disconnect**, then
  **Connect** again and pick your `@ucsd.edu` account. Then create a new
  DataPipe experiment, and paste its new ID into `index.html`.
- **"Your data could not be saved."** Check that **Accept new data** is on, that
  `DATAPIPE_ID` matches your dashboard exactly, and that you have not hit your
  session limit.
- **There is a `.partial.json` file in my Drive.** Someone left partway through.
  DataPipe saves their trials so far. The analysis only reads `.csv` files, so
  these are skipped.

DataPipe's own documentation: <https://pipe.jspsych.org/docs>.
