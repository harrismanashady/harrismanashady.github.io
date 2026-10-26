# Are.Es Cam

A camera web app for iPhone that shoots photos and video with the look of a RED digital cinema camera. The camera feed is processed through RED's published color science (REDWideGamutRGB and Log3G10) and an IPP2-style output stage, so footage gets dense, rich color, soft highlight roll-off and deep but detailed shadows. It installs to the Home Screen and runs full screen like a regular app, with no App Store and no Mac needed.

## What it does

- **Live graded viewfinder.** The look is applied to the camera feed in real time on the GPU (WebGL 2).
- **Photo and Video modes.** Video records the graded image (look, grain and vignette included) with sound, at up to 1920 pixels on the long side and 30 fps, as MP4 on iPhone. A REC timecode runs while recording; frame, camera flip and settings lock during a take. Clips stop at 3 minutes because recordings are held in memory until they finish.
- **Looks:** Cine (the default cinema look), Golden, Teal & Amber, Bleach and Noir.
- **Image pipeline controls** like a cinema camera's menu: Contrast (Low, Med-Low, Medium, Med-High, High) and Highlight roll-off (Hard, Medium, Soft, Very Soft).
- **RAW-style re-grading.** Every shot keeps its ungraded frame, so you can reopen it from the roll and change ISO, white balance, look, contrast and roll-off afterwards, the way REDCODE RAW clips stay adjustable in post.
- **Your own LUTs.** Import any 3D `.cube` LUT and say what it was made for: RED Log3G10 / REDWideGamutRGB (LUTs for RED footage), Apple Log, or normal Rec.709 video. Are.Es Cam converts the camera feed into that format before the LUT.
- **Camera controls:** ISO (exposure, base 800), white balance in Kelvin, frame crops (17:9, 2.39:1, 1.85:1, 16:9, full), false-color exposure view, film grain and lens vignette.
- **Roll.** Photos and videos are named like cinema clips (`A001_C0001_20261026.jpg`), stay on the phone, and save to Photos through the share sheet.
- **Grade existing photos** from your library with any look.
- Works offline after the first visit.

## Install on iPhone

1. Host this folder on any HTTPS web host (GitHub Pages works: Settings → Pages → deploy from the branch, root folder).
2. Open the URL in **Safari** on the iPhone.
3. Tap **Share → Add to Home Screen**.
4. Open Are.Es Cam from the Home Screen and allow camera access.

Requires iOS 15 or later (for WebGL 2). Live view and video need the app to be opened from its web address; they don't work inside an embedded preview that blocks camera access.

## How the color pipeline works

```
camera frame (sRGB) → linear → highlight range restored → ISO and white balance
  → REDWideGamutRGB → Log3G10 → 3D LUT (look + output tone map) → display sRGB → vignette, grain
```

- **REDWideGamutRGB** uses RED's published primaries (D65 white). **Log3G10** uses RED's published curve: 18% grey encodes to 1/3, and 10 stops above grey encodes to 1.0.
- Built-in looks are baked into 65³ LUTs at runtime from `grade()` in `index.html`. They take Log3G10 / REDWideGamutRGB input, the same as a LUT made for RED footage, so built-in and imported LUTs go through the same path.
- The output tone curve and highlight roll-off are Are.Es Cam's own approximation of a cinema output transform. RED's IPP2 transforms themselves are not published as formulas.
- The camera feed is already processed by iOS, so the conversion into Log3G10 approximates real camera-original footage: highlights the iPhone clipped can't be recovered.

## Files

| File | Purpose |
| --- | --- |
| `index.html` | The whole app: UI, color science, WebGL renderer, storage |
| `manifest.webmanifest` | Home Screen name, icon and full-screen mode |
| `sw.js` | Offline cache |
| `icons/` | App icons |

Are.Es Cam is not affiliated with RED Digital Cinema, Nikon or Apple. RED, REDCODE, IPP2, REDWideGamutRGB and Log3G10 are trademarks of their owners.
