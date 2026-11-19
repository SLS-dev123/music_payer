# SLS_player

A simple music player for Android, written in Python with [Kivy](https://kivy.org) and packaged as an APK with [Buildozer](https://github.com/kivy/buildozer).

## Features

- Plays MP3, OGG, WAV, FLAC and M4A files (support for less common formats depends on your phone)
- Automatically scans the `Music` and `Download` folders on your device
- Play, pause, stop, next and previous
- Seek bar with elapsed and total time
- Volume slider
- Shuffle and repeat
- Tap any song in the list to play it
- Moves to the next track automatically when a song ends

## Project structure

```
SLS_player/
├── main.py                      # The app (UI + playback logic)
├── buildozer.spec               # Android build configuration
├── README.md
└── .github/workflows/build.yml  # GitHub Actions workflow that builds the APK
```

## Build the APK

### Option 1: GitHub Actions (no Linux needed)

1. Create a free GitHub repository and upload all the files, keeping the `.github` folder.
2. Open the **Actions** tab and run **Build Android APK**. The first build takes about 15 to 25 minutes.
3. When it finishes, download the `SLS_player-apk` artifact and unzip it to get the `.apk` file.

### Option 2: Build locally (Linux or WSL)

```bash
pip install buildozer
buildozer android debug
```

The APK is created in the `bin/` folder. The first build downloads the Android SDK and NDK, so it needs a good internet connection and several GB of free space.

## Install on your phone

1. Copy the `.apk` file to your phone.
2. Open it and allow installs from unknown sources if Android asks.
3. On first launch, grant the audio/storage permission so the app can find your music.

## Run on a computer (for testing)

```bash
pip install kivy
python main.py
```

On desktop, the app scans your `~/Music` folder.

## Configuration

Edit `buildozer.spec` to change:

| Setting | What it does |
|---|---|
| `title` | App name shown on the phone |
| `package.name` / `package.domain` | Android package ID (`org.example.slsplayer` by default). Change `org.example` to your own domain before publishing |
| `version` | App version |
| `android.permissions` | Permissions the app requests |
| `android.archs` | CPU architectures to build for |

## Troubleshooting

- **"No music found":** Make sure your songs are in the `Music` or `Download` folder, and that you granted the permission. Tap **Scan for music** to rescan.
- **A song won't play:** The format may not be supported on your phone. Try MP3 or OGG.
- **Music stops when I close the app:** Background playback isn't implemented yet. It would need an Android foreground service.
- **Build fails:** Read the end of the build log. Running `buildozer android clean` and building again fixes many problems.

## Known limitations

- No background playback or lock-screen controls
- Only scans the `Music` and `Download` folders (no custom folder picker)
- No album art or tag (title/artist) display; tracks are shown by file name

## License

Add a license of your choice here.
