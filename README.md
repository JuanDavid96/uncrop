# Uncrop

A phone app that lets Instagram show your whole photo or video. It adds the thinnest possible strip so nothing gets cut, and by default an on-device AI paints that strip with what the rest of the scene would look like. You can also choose a plain strip (white or black, matching Instagram's light or dark mode). The picture itself is never cropped, stretched or blurred. It runs entirely on the phone: no uploads, no account, works offline once installed.

## AI fill

- Uses LaMa, an open-source image fill-in model (Apache-2.0), run on the phone with ONNX Runtime Web. Model file: huggingface.co/Carve/LaMa-ONNX. LaMa was trained on the Places2 dataset (CC-BY 4.0); credit: Suvorov et al., "Resolution-robust Large Mask Inpainting with Fourier Convolutions" (2021).
- The first time you use it, the app asks before downloading the model (about 200 MB). Use Wi-Fi. It's kept on the phone and works offline afterwards.
- Takes roughly 10–60 seconds per photo, depending on the phone. Newer phones use the graphics chip and are much faster.
- Videos: the AI paints the edges at several moments through the video (about every 2 seconds, up to 12 times) and the app blends smoothly between them while recording.
- If the AI can't run on a phone (for example, not enough memory), the app automatically uses a plain strip and says so.
- AI fill only works in the installed app. The preview inside the Claude app can't download the model.

Available in English, Spanish, Portuguese, French, German and Italian. It follows the phone's language automatically; tap the language button at the top to switch.

## What's in this folder

| File | What it does |
|---|---|
| `index.html` | The whole app (screen, conversion, saving) |
| `manifest.webmanifest` | Lets phones install it with its name and icon |
| `sw.js` | Makes it open instantly and work offline |
| `icons/` | Home screen icons |

## 1. Put it online (free, about 5 minutes)

Phones can only install the app from an `https://` address. Pick one:

**Netlify (easiest)**
1. Go to app.netlify.com/drop and create a free account.
2. Unzip this folder and drag the whole `uncrop-app` folder onto the page.
3. You get an address like `https://something.netlify.app`. You can rename it under Site settings.

**GitHub Pages**
1. Create a new public repository and upload the contents of this folder.
2. Settings → Pages → Branch: `main`, folder `/ (root)` → Save.
3. Your app is at `https://<your-username>.github.io/<repo-name>/`.

## 2. Install it on your phone

**iPhone (Safari):** open the address → Share button → Add to Home Screen → Add.
**Android (Chrome):** open the address → tap Install in the app, or ⋮ menu → Install app.

## 3. Use it

1. Tap **Choose photos or videos** and pick one or several.
2. Leave the strip color on **Automatic** (white in light mode, black in dark mode) or pick White or Black.
3. Tap **Convert**, then **Save to Photos**. On iPhone choose *Save Image* / *Save Video* in the share sheet.
4. In Instagram, tap the ⤢ button in the bottom-left corner of the photo so it shows in full.

## Quality notes

- **Photos:** at *Original* size the photo is copied pixel for pixel. If it already fits Instagram, you get the untouched original back. iPhones can't process images above about 16 megapixels in the browser, so very large photos (e.g. 48 MP) are scaled to that limit, which is still several times what Instagram keeps.
- **Videos:** adding a strip requires writing a new video, encoded as MP4 at 16–60 Mbps. Conversion runs in real time (a 30-second clip takes about 30 seconds). Keep the app open with the screen on.
- Instagram resizes posts to about 1080 px wide and recompresses everything. Uploading a high-quality file is what keeps that step from making things worse.

## Updating the app

After changing any file, open `sw.js` and raise the version number in `uncrop-v11` by one, then upload again. Installed copies update the next time they're opened.

## Putting it in the App Store / Google Play (optional)

Once it's online, pwabuilder.com can package the same app for Google Play (and a starter Xcode project for the App Store) from its address. Store accounts cost $25 once (Google) and $99/year (Apple).
