# Bluey iPhone web app — quick start (no Apple account required)

This is an account-free Safari Home Screen web app, not a signed IPA. It does not require Xcode, an Apple Developer account, Gmail, or an OpenAI API key. It pairs with the Windows host for focus timers, local Qwen chat, local Whisper push-to-talk transcription, iPhone spoken replies and opt-in local Windows screen monitoring.

## A. Publish the PWA from your GitHub fork

1. Make sure these new files are in your `Dytal/bluey-by-riley` repository: `Web/` and `.github/workflows/deploy-bluey-pwa.yml`.
2. In GitHub, open **Settings → Pages**.
3. Under **Build and deployment**, set **Source** to **GitHub Actions**.
4. Open **Actions → Deploy Bluey iPhone web app → Run workflow**. If it isn't listed yet, commit/push the workflow file to `main` first.
5. Wait for the deployment job to finish successfully. The website should then be available at `https://dytal.github.io/bluey-by-riley/`.

## B. Update and start the Windows host

1. Overlay the files in this patch onto your local repository folder, keeping your own `.github/workflows/build-ios-unsigned.yml` file. Do not delete your other project files.
2. In the `Windows` folder, run `run-bluey.bat`.
3. If Bluey's window says `cloudflared` is missing, run `install-cloudflared.bat`, close Bluey fully using the tray icon → **Quit Bluey**, then reopen it.
4. Press **Start iPhone web access**. Wait until the app says the temporary tunnel is ready and displays a replacement QR code.

## C. Install on iPhone XR

1. On the iPhone, open `https://dytal.github.io/bluey-by-riley/` in Safari.
2. Tap **Share → Add to Home Screen → Add**. If offered, keep **Open as Web App** enabled.
3. Return to the Home Screen and launch the new Bluey icon.
4. Inside the installed Bluey app, tap **Scan Windows QR**, allow camera access, and scan the QR currently shown in the Windows host window. Do not scan it with the regular Camera app; the pairing link needs to be saved in the installed app's own storage.
5. Leave Bluey running on Windows. The iPhone and PC need internet access, but they do not have to be on the same Wi-Fi.

## Important limits and privacy

- The PWA supports encrypted pairing, Bluey's face state, focus controls, typed local Qwen chat, local Whisper push-to-talk, iPhone speech synthesis, one-shot Windows screen checks and opt-in 60-second Windows screen monitoring.
- It does not monitor the iPhone's own screen or other iPhone apps, and it does not control the Windows mouse or keyboard. Gemini / Google AI Studio API support is not included (see the eligibility note below).
- Cloudflare Quick Tunnels are temporary testing tunnels. They are public while running, need no Cloudflare account, and use a different URL each time they are restarted. The QR contains the secret that lets a device pair with your PC. Keep it private, do not post it, lock your iPhone with a passcode, use **Forget this PC** on a shared device, and quit Bluey when finished. The PWA stores the pairing in its own browser storage, not the iOS Keychain.
- Since the Quick Tunnel URL changes after restart, press **Start iPhone web access** again and scan the new QR from inside the installed app.
- No Apple account is needed to add this website to the Home Screen. This is a PWA, not an App Store install.


## Local AI, voice and screen monitoring

1. Start LocalAI/llama.cpp with your Qwen model and multimodal projector loaded. The default API URL is `http://127.0.0.1:8080/v1`.
2. In the Windows Bluey host, set the local API URL and optionally the model ID, then press **Test connection**. “OpenAI-compatible” means API request format only; the host rejects remote API URLs so screen images stay on this PC. Enter a local Gemma model ID if your inference server is running Gemma rather than Qwen.
3. Run `Windows/install-bluey-voice.bat` once to install CPU-based local Whisper transcription. The first use downloads the `base.en` model.
4. Pair the PWA. Use **Talk to Bluey** for typed chat or **Start talking** for push-to-talk; tap **Speak reply** to hear the answer with the iPhone's built-in voice.
5. AI screen monitoring is OFF by default. Tap **Turn monitoring on** only when you want Windows screenshots analysed every 60 seconds locally. It stops when toggled off, the phone disconnects, Windows locks, or Bluey closes. **Check once** performs one explicit screenshot check.

Voice messages are processed locally by Whisper and Qwen. Screen screenshots go only to the loopback model endpoint. The PWA can analyse the Windows desktop; it cannot silently capture the iPhone's own screen.

Google Gemini / Google AI Studio API support is not included: Google's current Gemini API Additional Terms require API users to be at least 18 and prohibit API clients likely to be accessed by under-18s; UK API clients must use Paid Services. Do not add a Gemini key or attempt to bypass these terms. A locally hosted Google Gemma model can be selected by its model ID if the local server supports it; Gemma is separate from Gemini. Terms: https://ai.google.dev/gemini-api/terms.

Official Bluey video reference supplied by the project owner: https://www.youtube.com/shorts/IEYzYopNGVQ. The clip could not be loaded from this environment, so no exact video-derived UI claims are made.
