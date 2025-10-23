# Gemini-Powered Fireworks Generator 🎆

A stunning, interactive fireworks display that runs entirely in your browser. This project combines the HTML Canvas for physics-based animation with the Google Gemini API to provide ✨ **AI-powered poetic narration and text-to-speech (TTS)** ✨ for the show.

# LIVE: https://riponalmamun.github.io/Fireworks-Generator/

## Features

* **Interactive Display:** Click or tap anywhere on the screen to launch your own firework.
* **Generative Show:** An automatic launcher creates a continuous, beautiful display.
* **Simple Physics:** Rockets accelerate against gravity and particles explode outwards, all with realistic(ish) trails and friction.
* **✨ AI Narration:** Click the "Narrate Show" button to have the Gemini API generate a unique, poetic description of the fireworks.
* **✨ AI Voice:** The generated narration is immediately converted to speech using the Gemini TTS API and played in your browser.
* **Zero Dependencies:** It's all in a single HTML file, using a CDN for Tailwind CSS.

---

## Technologies Used

* **Frontend:** HTML5 (Canvas), JavaScript (ES6+), Tailwind CSS (via CDN)
* **AI & APIs:**
    * **Google Gemini API (`gemini-2.5-flash-preview-09-2025`):** For text generation.
    * **Google Gemini API (`gemini-2.5-flash-preview-tts`):** For Text-to-Speech.
    * **Web Audio API:** For decoding and playing the generated audio.

---

## Setup and Configuration

Because this project uses the Gemini API, you need to provide your own API key to run it locally.

### 1. Get Your Gemini API Key

1.  Go to **[Google AI Studio](https://aistudio.google.com/app/apikey)**.
2.  Sign in and create a new API key.
3.  Copy the key to your clipboard.

### 2. Configure the Project

1.  Clone this repository or download the `fireworks.html` file.
2.  Open the `fireworks.html` file in your favorite code editor.
3.  Find the `API_KEY` constant (around line 170):

    ```javascript
    // --- Gemini API Configuration ---
    const API_KEY = ""; // Leave empty, will be handled by the environment
    ```

4.  Paste your API key inside the quotes:

    ```javascript
    // --- Gemini API Configuration ---
    const API_KEY = "YOUR_API_KEY_GOES_HERE";
    ```

### 3. Run It Locally

You **cannot** just open the `fireworks.html` file directly in your browser using a `file:///` path. Browser security policies will block the API requests.

You must serve the file from a **local web server**. The easiest way is using Python or Node.js.

**Using Python (Recommended):**
1.  Open your terminal or command prompt.
2.  Navigate to the project's directory: `cd path/to/your/project`
3.  Run this command:
    ```bash
    # For Python 3
    python -m http.server
    ```
4.  Open your browser and go to `http://localhost:8000`.

**Using Node.js (if you have `serve`):**
1.  Open your terminal.
2.  Navigate to the project's directory.
3.  Run this command:
    ```bash
    npx serve
    ```
4.  Open your browser and go to the local address it provides (e.g., `http://localhost:3000`).

---

## How It Works: The AI Pipeline

When you click the "✨ Narrate Show" button, a two-step process begins:

1.  **Text Generation:** An API call is made to the Gemini text model (`gemini-2.5-flash-preview-09-2025`). It's given a system prompt to act as a "poetic fireworks show narrator" and asked to describe the scene.
2.  **Text-to-Speech (TTS):** The text response from Step 1 is immediately sent to the Gemini TTS model (`gemini-2.5-flash-preview-tts`).
3.  **Audio Handling:** The API returns Base64-encoded PCM (raw) audio data. The JavaScript in the browser:
    * Decodes the Base64 data into an `ArrayBuffer`.
    * Converts the raw PCM data into a valid `.wav` file (by adding the necessary WAV header in memory).
    * Creates a `Blob` from the WAV data and plays it using the Web Audio API.

### 🔒 A Note on Security

The current method of placing the `API_KEY` directly in the frontend JavaScript is **only for local development and demonstration**.

**DO NOT** deploy this file to a public website (like GitHub Pages) with your API key inside it. Your key will be stolen and abused. For a real-world application, you must proxy your API calls through a secure backend (e.g., a Node.js/Express, Python/Flask, or serverless function) that holds the API key securely.

---

## Future Ideas

* **Secure Backend:** Create a simple serverless function (e.g., on Vercel or Netlify) to proxy the API calls and protect the key.
* **AI-Driven Fireworks:** Pass a description of the current fireworks (e.g., `{"count": 5, "colors": ["red", "blue"]}`) to the Gemini model and have it control the *next* launch (e.g., "Now, a big green explosion!").
* **Voice Selection:** Allow the user to choose from different TTS voices.

## License

This project is distributed under the MIT License. See the `LICENSE` file for more information.
