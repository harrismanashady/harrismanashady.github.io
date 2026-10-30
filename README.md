# Are.Es Cam

A camera web app for iPhone that shoots photos and video with the look of a RED digital cinema camera. The camera feed is processed through RED's published color science (REDWideGamutRGB and Log3G10) and an IPP2-style output stage, so footage gets dense, rich color, soft highlight roll-off and deep but detailed shadows. It installs to the Home Screen and runs full screen like a regular app, with no App Store and no Mac needed.

## What it does

- **Live graded viewfinder.** The look is applied to the camera feed in real time on the GPU (WebGL 2).
- **Photo and Video modes.** Video records the graded image (look, grain and vignette included) with sound, at up to 1920 pixels on the long side and 30 fps, as MP4 on iPhone. A REC timecode runs while recording; frame, camera flip and settings lock during a take. Clips stop at 3 minutes because recordings are held in memory until they finish.
- **Self-timer.** The timer button in the viewfinder cycles Off, 3 s and 10 s. Tap the shutter and a countdown runs on screen before the photo is taken or the recording starts; tap the shutter again to cancel. Stopping a recording is always immediate.
- **Remote shutter.** A Bluetooth keyboard or camera remote works the shutter with Enter or Space. On two-button camera remotes, use the button that sends Enter (often the one marked Android). The iPhone's volume buttons, and remote buttons that act as volume up, can't be used: iOS keeps volume keys to itself and doesn't pass them to web pages or Home Screen web apps, only to App Store apps.
- **Tap to focus.** Tap the viewfinder to focus on that spot; exposure and ISO stay as they are. iPhone Safari lets a web page set the lens's focus distance but not a focus point, so the app drives the lens itself, the way contrast-detect autofocus works: it moves smoothly from where focus already is, watches the sharpness at the tapped spot, and eases onto the sharpest point, so a change of subject looks like a focus pull rather than a jump. Focus transition (Slow, Medium, Fast) in Settings sets how fast it moves. An AF LOCK badge shows the lock; tap it to return to automatic. Where a camera doesn't allow focus control, focus stays automatic.
- **Pinch to zoom, 0.5× to 15×.** Zoom eases smoothly and works while recording. Each lens is cropped digitally up to the next one (Ultra Wide, Main, Telephoto); when zoom crosses over, the last frame is held while the other lens starts and is then cross-faded into it at the same field of view, so the switch doesn't jump. The .5, 1, 2 and 3 buttons glide to those zooms. Lenses are opened directly by device, so iOS doesn't switch lenses on its own. Lens specs are those of the iPhone 14 Pro / Pro Max.
- **HDR.** An HDR button in the viewfinder (Off, HDR, HDR+) and in Settings. iPhone Safari doesn't let web apps shoot several exposures or save HDR files, so this is HDR tone mapping of each frame: large-scale brightness is pulled toward mid grey, so bright skies come down and shadows open up, while local detail stays. The brightness estimate blends two blur sizes and switches to the smaller one near strong edges, which avoids halos. It applies to photos and video and is saved with each shot for re-grading.
- **AI skin tone.** An on-device AI model (MediaPipe's multiclass selfie segmenter) finds people and separates face and body skin from hair, clothes and background. Detected skin keeps a natural rendering, slightly brighter and with less grain, in every look, even Noir and One Colour; an AI · SKIN tag shows when someone is detected. It runs on the phone, works offline after the first load, and can be switched off in Settings. The model and runtime are about 27 MB, downloaded once.
- **Iris (simulated).** iPhone lenses have fixed apertures (f/2.2, f/1.78, f/2.8 on the 14 Pro), and web pages can't read the depth data Portrait mode uses. The Iris control shows the lens's real f-number, and f/1.4–f/8 simulate shallow depth of field: a lens-style blur that grows with distance from the spot you tapped, and racks smoothly to a new spot: the old subject softens as the new one sharpens. It's applied to photos and video, and saved with each shot for re-grading.
- **Auto-rotate.** The motion sensor detects whether you're holding the phone in portrait or landscape, even with Portrait Orientation Lock on, so photos and videos are saved the right way up, like the iPhone camera. Buttons turn to face you, and a video keeps the orientation it started with. iPhone asks once for Motion & Orientation access, on the first tap. It can be switched off in Settings.
- **Looks:** Cine (the default cinema look), Golden, Teal & Amber, Neon & Glow, Instant, Bleach, Noir, Dark Black (low-key, with inky crushed blacks) and One Colour.
- **Instant.** The look of instant film prints: soft contrast, milky blacks with a cool cyan tint, bright creamy highlights, pastel colors with greens leaning teal and skin a touch pink, a gentle diffusion around bright areas, and the corner falloff of a small flash lens. Photos come out as an instant print, drawn after real Instax-style film: a matte white card a shade darker toward its edges with a faint grain, thin borders at the sides and top, and the wide strip at the bottom with its slightly darker band and seam over the developer pod, in the proportions of real prints. Tap the Instant chip again (or the FRAME value) to choose Mini (the default), Square, Wide, or Off. The viewfinder shows the card, and the strip moves to whichever side will be the bottom of the photo as you turn the phone. Videos keep the normal frame and no border. The print format is saved with each photo, so re-grading can change it.
- **Instant effects.** Under the print formats, Instant has the lens effects of instant cameras with digital effects: Normal, Vignette (deep dark corners), Soft Focus (a dreamy soft glow over a sharp picture), Blur (sharp in the middle, soft toward the edges), Fisheye (a bulging circle with black corners), Color Shift (red and blue drift apart), Light Leak (warm light streaking in from an edge), Mirror (the top half reflected below), Double Exposure and Half-Frame. Double Exposure and Half-Frame take two shots: the first press keeps a frame (a 1 OF 2 badge shows; tap it to discard), the second makes the photo, with both exposures blended or stacked as two halves. Effects follow the way you hold the phone, show in the viewfinder, are saved with each photo for re-grading (two-shot photos keep their first frame too), and apply to video, except the two-shot ones, which are for photos only.
- **Neon & Glow.** A night-city look: magentas, cyans and violets pushed hard, greens turned teal, blue skies turned indigo, and deep violet-black shadows. Bright lights glow: signs, lamps and neon tubes get a soft halo in their own color, spread at three sizes like the bloom of a diffusion filter. Only light well above white glows, so dark areas stay clean; in daylight, bright highlights get a gentle halation. It applies to the viewfinder, photos and video.
- **One Colour.** Keeps one colour and turns everything else black and white, in photos and video. Pick Red, Orange, Yellow, Green, Cyan, Blue, Purple or Pink, and a Range (Narrow, Medium, Wide) for how close a hue has to be to count. Greys and near-neutral colours always go black and white. Tap the One Colour chip again to change the colour; the choice is saved with each shot for re-grading.
- **Image pipeline controls** like a cinema camera's menu: Contrast (Low, Med-Low, Medium, Med-High, High) and Highlight roll-off (Hard, Medium, Soft, Very Soft).
- **RAW-style re-grading.** Every shot keeps its ungraded frame, so you can reopen it from the roll and change ISO, white balance, look, contrast and roll-off afterwards, the way REDCODE RAW clips stay adjustable in post.
- **Your own LUTs.** Import any 3D `.cube` LUT and say what it was made for: RED Log3G10 / REDWideGamutRGB (LUTs for RED footage), Apple Log, or normal Rec.709 video. Are.Es Cam converts the camera feed into that format before the LUT.
- **Camera controls:** ISO (exposure, base 800), white balance in Kelvin, frame crops (17:9, 2.39:1, 1.85:1, 16:9, full), false-color exposure view, film grain and lens vignette.
- **Roll.** Photos and videos are named like cinema clips (`A001_C0001_20261026.jpg`), stay on the phone, and save to Photos through the share sheet. Tap a shot to view it, then swipe left or right (or use the arrow buttons) to move through the roll; after deleting one, the next one along shows. Tap Select to pick several (or Select all), then Save to Photos to share them in one go, or Delete to remove them from the app after a confirmation.
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
- Neon & Glow (and, more gently, Instant) adds a glow before the LUT: a quarter-size copy of the frame keeps only light above white (highlights are restored pixel by pixel first, so thin neon tubes keep their brightness), and its mipmaps are added back at three sizes.
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
| `vendor/mediapipe-0.10.35/` | MediaPipe Tasks Vision 0.10.35 (JavaScript bundle and WebAssembly runtime) |
| `vendor/models/selfie_multiclass_256x256.tflite` | MediaPipe multiclass selfie segmentation model |

MediaPipe and its selfie segmentation model are by Google and are used under the Apache License 2.0.

Are.Es Cam is not affiliated with RED Digital Cinema, Nikon or Apple. RED, REDCODE, IPP2, REDWideGamutRGB and Log3G10 are trademarks of their owners.
