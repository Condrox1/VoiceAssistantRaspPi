# Voice-Activated Assistant for Raspberry Pi

This is a simple voice-activated assistant built for Raspberry Pi using Python and the OpenAI API. It listens for a wake word, processes your voice input, and responds using OpenAI's GPT model. It also reads out the responses using a text-to-speech engine.

## Features

- **Wake Word Detection**: Listens for the phrase "Hey Assistant."
- **Voice Commands**: Recognizes your voice, processes the text with OpenAI, and responds.
- **Text-to-Speech**: The assistant speaks its response back to you.
- **Easy to Customize**: Modify the wake word, responses, and more.

## Requirements

### Hardware:
- Raspberry Pi (3B+ or newer)
- USB Microphone
- Speakers

### Software:
- Python 3
- OpenAI API Key (Get it [here](https://beta.openai.com/signup))

### Python Libraries:
Install the required libraries using `pip`:

```bash
pip install openai speechrecognition pyttsx3 numpy python-dotenv pyaudio
```

## Setup

1. **Clone the Repo**:
   ```bash
   git clone https://github.com/Condrox1/VoiceAssistantRaspPi.git
   cd VoiceAssistantRaspPi
   ```

2. **Set Up OpenAI API Key**:
   Create a `.env` file in the project folder and add your OpenAI API key:
   ```bash
   OPENAI_API_KEY=your-openai-api-key
   ```

3. **Run the Assistant**:
   Run the Python script:
   ```bash
   python main.py
   ```

## How It Works

- The assistant listens for "Hey Assistant."
- After detecting the wake word, it listens for your command.
- Your command is sent to OpenAI's GPT model for processing.
- The assistant speaks the response using text-to-speech.

### Example: Wake Word Detection
```python
def listen_for_wake_word(source):
    print("Listening for 'Hey Assistant'...")
    while True:
        audio = r.listen(source)
        try:
            text = r.recognize_google(audio)
            if "hey assistant" in text.lower():
                print("Wake word detected.")
                engine.say("Yes?")
                engine.runAndWait()
                listen_and_respond(source)
                break
        except sr.UnknownValueError:
            pass
```

## Customization

- **Change Wake Word**: Modify `"hey assistant"` in the code.
- **Add Custom Responses**: Update the response logic in the `listen_and_respond` function.
- **Switch Voices**: Change the voice settings in `pyttsx3` to pick a different TTS voice.

## License

This project is licensed under the MIT License.

---
