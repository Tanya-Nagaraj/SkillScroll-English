# SkillScroll — (English UI with Kannada AI Interaction) Audio-Native Negotiation Agent
SkillScroll is an audio-first mobile web application designed to help rural Karnataka artisans practice and improve their negotiation skills against AI-driven realistic buyer personas.

Features
Reels-Style Feed: Vertical scroll of quest cards.
Audio Native UI: "Hold to Talk" push-to-talk interface.
AI Roleplay: Driven by Gemini Flash with specific local personas (Mandi wholesaler, strict buyer, tourist).
Designed to be deployed on Render.

This repository contains an alternate FastAPI-based version of the SkillScroll application.

## Overview

The application lets a user:

- Choose from negotiation scenarios.
- Start an AI-driven negotiation.
- Speak through the browser microphone.
- Send recorded audio to the FastAPI backend.
- Use Google Gemini to process the spoken response.
- Receive a Kannada reply from the simulated wholesaler.
- See a confidence/score value and short AI feedback.
- Continue the conversation for multiple turns.

The interface is designed as a mobile-first experience and uses browser speech synthesis for spoken Kannada responses.

## Technology Stack

- **Python**
- **FastAPI**
- **Google Gemini API** (`gemini-2.5-flash`)
- **Firebase Admin SDK**
- **HTML / CSS / JavaScript**
- **Web MediaRecorder API** for microphone recording
- **Browser SpeechSynthesis API** for text-to-speech
- **Uvicorn** for serving the FastAPI application

## Project Structure

```text
SkillScroll-English-main/
├── frontend/
│   ├── index.html
│   ├── script.js
│   └── style.css
├── firebase_config.py
├── main.py
└── requirements.txt
```

## How It Works

1. The user selects a negotiation quest.
2. The frontend calls `/start_negotiation`.
3. Gemini generates the wholesaler's opening message.
4. The user records a response using the browser microphone.
5. The audio is sent to `/negotiate`.
6. The FastAPI backend passes the audio to Gemini.
7. Gemini returns:
   - the user's transcript,
   - the simulated wholesaler reply,
   - a score,
   - short feedback.
8. The frontend displays the conversation and reads the reply aloud.
9. After multiple turns, a report card is displayed.

## Included Scenarios

The current frontend contains three scenarios:

- **Mandi Hustle** — negotiate with a buyer offering a substantially lower price.
- **Credit Trap** — negotiate with a buyer asking to purchase on credit.
- **Tourist Bargain** — negotiate with an English-speaking tourist.

## API Endpoints

### `GET /health`

Returns a basic health status.

### `GET /start_negotiation`

Starts a negotiation and generates the simulated wholesaler's opening message.

Example:

```text
/start_negotiation?quest_id=quest-1
```

### `POST /negotiate`

Accepts:

- `quest_id`
- `history`
- recorded `audio`

and returns the user's transcript, simulated agent reply, confidence/score, and feedback.

## Configuration

The application expects a Gemini API key in the environment:

```text
GEMINI_API_KEY=your_api_key
```

Firebase configuration is loaded through `firebase_config.py`.

Do not commit API keys, service-account credentials, or other secrets to GitHub.

## Local Setup

### 1. Clone the repository

```bash
git clone https://github.com/Tanya-Nagaraj/SkillScroll-English.git
cd SkillScroll-English
```

### 2. Create a virtual environment

```bash
python -m venv venv
```

Windows:

```bash
venv\Scripts\activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Configure environment variables

Set your Gemini API key:

```text
GEMINI_API_KEY=your_api_key
```

Configure Firebase according to `firebase_config.py`.

### 5. Run the application

```bash
uvicorn main:app --reload
```

Then open the local address shown by Uvicorn in a browser.

Microphone access must be allowed by the browser for voice interaction.

## Current Development Status

This repository represents an alternate/earlier FastAPI implementation of SkillScroll.

The project is still under development. Planned improvements include replacing prototype speech components with a production Bhashini integration and improving the overall negotiation and evaluation pipeline.

## Important Note

The current implementation should not be presented as a completed production speech platform. Some speech functionality currently relies on browser APIs, and the project is being actively developed.

## Author
**Tanya N**
