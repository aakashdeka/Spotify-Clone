# 🎵 Spotify Clone

A fully functional Spotify-inspired web music player built with vanilla HTML, CSS, and JavaScript. Browse mood-based and artist-based playlists, play/pause tracks, seek through songs, and control volume — all in a clean dark UI that mirrors Spotify's iconic look.

![Spotify Clone Preview](img/cover.jpg)

---

## ✨ Features

- 🎨 **Spotify-like dark UI** — dark background, card-based playlist grid, and Spotify green accents
- 📁 **Dynamic playlist loading** — playlists are auto-discovered from the `songs/` directory via server-side directory indexing
- 🎶 **Full audio controls** — play, pause, previous, next, seekbar scrubbing, and real-time timestamps
- 🔊 **Volume control** — slider-based volume control with mute/unmute toggle
- 📱 **Responsive design** — collapsible left sidebar with hamburger menu on mobile/tablet (`≤1200px`)
- 🗂️ **Library sidebar** — click any song in the queue list to play it instantly
- 🃏 **Playlist cards** — each playlist shows its cover art, title, and description loaded from `info.json`

---

## 📂 Project Structure

```
Spotify clone/
├── index.html              # Main HTML entry point
├── favicon.ico
│
├── css/
│   ├── style.css           # Main component styles + responsive breakpoints
│   └── utility.css         # Utility classes (flex, bg, padding, etc.) + scrollbar styling
│
├── js/
│   └── script.js           # All app logic — fetching, playback, UI events
│
├── img/                    # All SVG icons and the default cover image
│   ├── logo.svg
│   ├── play.svg / pause.svg
│   ├── nextsong.svg / prevsong.svg
│   ├── volume.svg / mute.svg
│   ├── hamburger.svg / close.svg
│   ├── home.svg / search.svg / music.svg / playlist.svg
│   └── cover.jpg
│
└── songs/                  # Music library — one sub-folder per playlist
    ├── htaccess.txt        # Enables Apache directory listing (required for auto-discovery)
    ├── ncs/
    │   ├── cover.jpg       # Playlist cover art
    │   ├── info.json       # { "title": "...", "description": "..." }
    │   └── *.mp3
    ├── Diljit/
    ├── karan aujla/
    ├── cs/
    ├── Angry_(mood)/
    ├── Bright_(mood)/
    ├── Chill_(mood)/
    ├── Dark_(mood)/
    ├── Funky_(mood)/
    ├── Love_(mood)/
    └── Uplifting_(mood)/
```

---

## 🚀 Getting Started

### Prerequisites

This project requires a web server that supports **directory listing** (for the playlist auto-discovery to work). A simple Python or Node.js local server is sufficient.

> ⚠️ Opening `index.html` directly in a browser (`file://` protocol) will **not** work — the `fetch()` calls require an HTTP server.

### Option 1 — Python (Recommended, no install needed)

```bash
cd "Spotify clone"
python -m http.server 8000
```

Then open [http://localhost:8000](http://localhost:8000) in your browser.

### Option 2 — Node.js (`http-server`)

```bash
npm install -g http-server
cd "Spotify clone"
http-server -p 8000
```

### Option 3 — Live Server (VS Code Extension)

Install the **Live Server** extension in VS Code, right-click `index.html`, and select **Open with Live Server**.

> **Apache/Nginx users:** The `songs/htaccess.txt` file should be renamed to `.htaccess` and placed inside the `songs/` directory. It enables `Options +Indexes` so the JS can read folder contents.

---

## ➕ Adding a New Playlist

1. Create a new sub-folder inside `songs/`, e.g. `songs/MyPlaylist/`
2. Add your `.mp3` files to the folder
3. Add a `cover.jpg` (playlist thumbnail)
4. Add an `info.json` file:
   ```json
   {
     "title": "My Playlist",
     "description": "A short description"
   }
   ```
5. Refresh the page — the new playlist card will appear automatically.

---

## 🛠️ Technology Stack

| Technology | Role |
|---|---|
| HTML5 | Page structure & semantic markup |
| CSS3 | Styling, layout (Flexbox), responsive design |
| Vanilla JavaScript (ES6+) | Audio playback, DOM manipulation, fetch API |
| Google Fonts (Roboto) | Typography |
| SVG Icons | UI icons (play, pause, nav, etc.) |

---

## 📱 Responsive Behaviour

| Breakpoint | Behaviour |
|---|---|
| `> 1200px` | Full two-column layout — sidebar always visible |
| `≤ 1200px` | Sidebar slides off-screen; hamburger icon shows to open it |
| `≤ 500px` | Cards go full-width; header and buttons compress for small phones |

---

## ⚙️ How It Works

1. **On load**, `main()` calls `getSongs("songs/ncs")` to load the default playlist, then `displayAlbums()` to render all playlist cards.
2. **`displayAlbums()`** fetches the `/songs/` directory listing, finds all sub-folders, reads each folder's `info.json`, and renders a card for it.
3. **`getSongs(folder)`** fetches the folder's directory listing, parses all `.mp3` links, and populates the sidebar song list.
4. **`playMusic(track)`** sets the `<audio>` element `src`, plays the track, and updates the song info display.
5. **Seekbar** uses a CSS `left %` on an absolutely-positioned circle element that updates on every `timeupdate` event.

---

## 📄 License

This project is built for **educational purposes** as a front-end development exercise. All music files are owned by their respective artists and labels.  
The Spotify brand, logo, and design language are trademarks of **Spotify AB** — this clone is not affiliated with or endorsed by Spotify.
