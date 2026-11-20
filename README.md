# JARVIS AI — Android phone-only project

This is a starter Android project based on the supplied JARVIS `MainActivity.kt` concept. It keeps the black/gold/red Stark-inspired design direction and adds a working chat UI, Android speech recognition, UK English text-to-speech, local chat history, agent presets, provider selection, and a secure-backend client.

## Important honest limitations

- The centre "J" is an animated placeholder, not a real 3D Iron Man model. A real 3D avatar needs a 3D asset and a rendering integration in a later milestone.
- Voice recognition uses Android's available speech-recognition service. It is not an always-listening wake-word service.
- Real AI requires deploying the backend and configuring an API provider key.
- The app does not autonomously control the phone. Android actions should be added individually with explicit permissions and confirmations.
- Do not put provider API keys in Kotlin, Gradle files, GitHub commits, or the APK.

## Project layout

- `app/` — Android application
- `backend/` — Cloudflare Worker that keeps provider API keys off the phone
- `.github/workflows/build-apk.yml` — cloud APK build workflow

## Build the APK using only an Android phone

1. Open GitHub in your phone browser and create a new repository named `jarvis-ai`.
2. Upload the project files and folders from this ZIP into the repository. Keep the folder structure exactly as shown.
3. Open the repository's **Actions** tab. Enable Actions if GitHub asks.
4. Open **Build JARVIS Android APK** and press **Run workflow**. You can also push a commit to `main` to trigger a build.
5. When the workflow finishes successfully, open its run page and download the `JARVIS-AI-debug` artifact.
6. Extract the artifact ZIP on your phone. Install `app-debug.apk`. Android may ask you to allow installs from the browser or file manager you used.

## Activate real AI securely

The Android app initially runs in demo mode until a backend URL is entered.

1. Create a Cloudflare account and open Workers & Pages.
2. Create a Worker named `jarvis-ai-backend`.
3. Copy the contents of `backend/worker.js` into the Worker editor and deploy it.
4. In Worker settings, add a secret named `GROQ_API_KEY` or `GEMINI_API_KEY`. Add the key only in the Cloudflare secret field. Never send it in chat or commit it to GitHub.
5. Optional Worker variables:
   - `GROQ_MODEL` — defaults to `llama-3.3-70b-versatile`
   - `GEMINI_MODEL` — defaults to `gemini-2.0-flash`
6. Copy the Worker URL and add `/chat` to the end, for example `https://your-worker.workers.dev/chat`.
7. Open JARVIS → Settings, paste the backend URL, save, then select Groq or Gemini.
8. Test with a simple message.

Provider account eligibility, regional availability, quotas, and pricing can change. Check the provider's current terms. If an account requires an adult, ask a parent or guardian to manage the account and keys.

## If you edit Kotlin code

The main app source is:
`app/src/main/java/com/jarvis/ai/MainActivity.kt`

After changing files, commit the changes to GitHub and run the workflow again.

## Security notes

This starter backend is a learning foundation, not a production-hardened public service. Before sharing it widely, add authentication, request rate limits, abuse protection, and stricter CORS/origin controls. Do not expose your Worker endpoint publicly without protections if it uses paid API keys.
