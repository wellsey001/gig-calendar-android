<p align="center"><img src="logo.png" alt="" width="120"></p>

# Earshot

See when the artists you listen to on Spotify are playing near you, or anywhere in the country, in one clean calendar.

**Open the app:** https://wellsey001.github.io/gig-calendar/

<p align="center">
  <img src="screenshots/month.png" alt="Month view with gigs shown as ticket stubs on each day" width="800">
</p>

## What it does

- **Reads your Spotify library.** It looks at the artists you follow, your most-played artists and the artists on your liked songs, then ranks them by how much you listen to them.
- **Finds their gigs.** It checks Ticketmaster for upcoming shows by those artists in your chosen country.
- **Shows what’s near you.** Gigs within your chosen distance of home are “in earshot” and highlighted in yellow. Gigs further afield are shown in purple.
- **Keeps track of the gigs you’re going to.** Mark a gig as “I’m going” and it appears in **My gigs** with a countdown and a reminder to book a hotel.
- **Fits into your own calendar.** Export gigs to Google Calendar, Apple Calendar or Outlook as an `.ics` file.
- **Works on Android.** Install it as an app with its own icon, a bottom tab bar and swipe-up gig details.

## Screenshots

| Month view | List view | My gigs |
|:---:|:---:|:---:|
| <img src="screenshots/month.png" alt="Month view" width="260"> | <img src="screenshots/list.png" alt="List of upcoming gigs with photos and distances" width="260"> | <img src="screenshots/my-gigs.png" alt="My gigs with countdowns and hotel status" width="260"> |

| Gig details | On Android |
|:---:|:---:|
| <img src="screenshots/details.png" alt="Gig details panel with photo, directions and ticket buttons" width="260"> | <img src="screenshots/android.png" alt="The app on an Android phone with the bottom tab bar" width="260"> |

## Getting started

You need a Spotify account, and the person who runs this copy of the app has to add you as a user first (see [Sharing with friends](#sharing-with-friends)).

1. Open the app link above.
2. Choose **Settings**, enter your postcode and choose **Set**. Outside the UK, use **Use my current location** instead, or type coordinates such as `48.85, 2.35`.
3. Choose your country and how far counts as “in earshot”. The default is 50 miles.
4. Choose **Save settings**, then **Connect Spotify** and sign in.
5. The scan starts as soon as you’re back. It takes about a minute for 150 artists.

To scan again later, for example to pick up newly announced gigs, choose **Scan again**.

## Using the app

### Month view

Each gig is a ticket stub on its date. Yellow gigs are in earshot and purple ones are further afield. Use the arrows to move between months. If a month is empty, a link takes you to the next month that has a gig.

### List view

All upcoming gigs in date order, grouped by month, each with a photo, the venue and how far away it is.

### Filters

- **Whole country** or **In earshot** switches between all gigs and only the ones within your distance.
- The filter box narrows the list by artist, venue or city.

### Gig details

Tap any gig to see the date, time, venue, distance and ticket status. From there you can:

- choose **I’m going** to add it to My gigs
- choose **Find tickets** to open the gig on Ticketmaster
- choose **Get directions** to open the venue in Google Maps
- choose **Add to calendar** to download that one gig as a calendar file

### My gigs

Every gig you’ve marked as going, with:

- **A countdown** showing how many days are left.
- **A hotel tracker** with three settings: Not booked, Booked or Not needed. Gigs near home start as Not needed, and the line at the top tells you how many still need a hotel.
- **Been there**, a section at the bottom where past gigs move to.

Your picks are kept when you scan again.

### Exporting to your calendar

Choose **Export to calendar** to download `earshot-gigs.ics` with every upcoming gig in the current view. On the My gigs tab, it exports only the gigs you’re going to. Open the file on your phone or computer to add the gigs to your calendar.

## Installing on Android

**Option 1: from Chrome.** Open the app link in Chrome, open the menu (⋮) and choose **Install app**.

**Option 2: from an APK.** If you’ve been sent the Earshot APK:

1. Tap the file. Android asks to allow installs from that app (Files, WhatsApp and so on).
2. Choose **Settings**, turn on **Allow from this source**, then go back.
3. Choose **Install**. If Play Protect warns about an unknown app, choose **More details**, then **Install anyway**. This is normal for apps that don’t come from the Play Store.

The app loads the live website, so it updates itself. You never need to reinstall it for new features.

## Sharing with friends

Spotify only lets this app sign in up to five people, including the owner. To add a friend:

1. Go to the [Spotify developer dashboard](https://developer.spotify.com/dashboard) and open the app.
2. Under **User Management**, add your friend’s name and the email address of their Spotify account.
3. Send them the app link or the APK.

## Switching Spotify accounts on one device

1. Open **Settings** and choose **Disconnect Spotify**. This also clears the scan results.
2. Choose **Connect Spotify**, then **Not you?** on Spotify’s page, and sign in with the other account.

Your picked gigs and settings stay on the device, so update the postcode in Settings if needed.

## Running your own copy

### 1. Get the two keys

- **Spotify Client ID:** create an app in the [Spotify developer dashboard](https://developer.spotify.com/dashboard) and tick **Web API**. Spotify requires the app owner to have Premium.
- **Ticketmaster key:** sign up at [developer.ticketmaster.com](https://developer.ticketmaster.com/) and copy your **Consumer Key**. It’s free and allows 5,000 checks a day.

### 2. Build the keys in (optional)

Open `index.html`, search for `PRESET` and fill in both keys:

```js
const PRESET = { clientId: 'your-spotify-client-id', tmKey: 'your-ticketmaster-key' };
```

With the keys built in, people using your copy only have to add a postcode and sign in. Leave them blank if you want each person to enter their own in Settings.

### 3. Publish it on GitHub Pages

1. Upload the files to a **public** repository.
2. Go to **Settings**, then **Pages**, choose the `main` branch and `/ (root)`, and save.
3. Your app will be at `https://YOUR-GITHUB-NAME.github.io/REPOSITORY-NAME/`.

### 4. Tell Spotify where the app lives

In your Spotify app’s settings, add the app’s address to **Redirect URIs**, including the slash at the end. **Settings** in the app shows the exact address to copy.

### Running it on your own computer

Spotify can’t sign you in from a file opened directly, so serve it instead. In the folder with the files, run:

```
python3 -m http.server 8000 --bind 127.0.0.1
```

On Windows, use `py` instead of `python3`. Then open `http://127.0.0.1:8000/` and add that address to your Spotify app’s Redirect URIs. Spotify doesn’t accept `localhost`, so use `127.0.0.1`.

## Files

| File | What it is |
|---|---|
| `index.html` | The whole app |
| `manifest.json` | App name, colours and icons for installing on Android |
| `sw.js` | Lets the app open without a signal. It always checks for a newer version first. |
| `icon-192.png`, `icon-512.png`, `icon-maskable-512.png` | App icons |
| `logo.svg`, `logo.png` | The Earshot logo |

## Privacy

Everything stays in your browser: your settings, scan results and picked gigs. There’s no server and no account apart from Spotify. The app asks Spotify for read-only access to the artists you follow, your top artists and your liked songs. It can’t change anything in your Spotify account.

The Spotify Client ID and Ticketmaster key in `index.html` are visible to anyone who views the page’s code. That’s expected: the Client ID isn’t a secret, and only people added in User Management can sign in. The worst anyone could do with the Ticketmaster key is use up its free daily allowance. Never put your Spotify **Client Secret** in the file; the app doesn’t need it.

## Limitations

- Gigs come from Ticketmaster only, so shows sold only through other sites, such as Dice or See Tickets, won’t appear.
- Spotify’s Development Mode limits the app to five users and requires the owner to have Premium.
- Artists are matched by name, so an artist who shares a name with another act can occasionally pick up the wrong gigs.

## Troubleshooting

| Problem | Fix |
|---|---|
| “Spotify can’t sign you in from a preview window or a file” | Open the app from its web address or `http://127.0.0.1:8000/`, not by double-clicking the file. |
| Spotify says **Invalid redirect URI** | Add the app’s exact address, including the slash at the end, to Redirect URIs in the Spotify dashboard. |
| Spotify refuses a friend’s sign-in | Add their Spotify email under **User Management**. |
| “Ticketmaster rejected the API key” | Check the key in Settings, or in `PRESET` in `index.html`. |
| Gigs show letter tiles instead of photos | Choose **Scan again**. Gigs saved before photos were added don’t have them. |
| Changes don’t show after updating GitHub | Wait for the green tick in the **Actions** tab, then press Ctrl+Shift+R. |
| The Android app shows a browser bar at the top | The `assetlinks.json` file isn’t being found. See the PWABuilder instructions for the `YOUR-GITHUB-NAME.github.io` repository. |
