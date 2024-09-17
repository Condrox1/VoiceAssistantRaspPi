# Voice-Activated Assistant for Raspberry Pi

Welcome to the **Voice-Activated Assistant for Raspberry Pi**! This project is a voice-activated AI assistant powered by Python, utilizing OpenAI's GPT-3.5 Turbo model for conversational abilities. It listens for a wake word and responds to your queries or commands, making it an excellent starting point for creating smart assistants or IoT control systems on a Raspberry Pi.

## Features

- **Wake Word Activation**: The assistant listens for the phrase "Hey Assistant" to activate.
- **OpenAI GPT-3.5 Turbo Integration**: Sends user input to OpenAI for smart and dynamic responses.
- **Text-to-Speech (TTS)**: The assistant speaks responses back to you, creating a hands-free experience.
- **Voice Recognition**: Uses Google’s speech recognition engine to convert speech into text.
- **Customizable Responses**: Set up personalized responses for your assistant.
- **Raspberry Pi Friendly**: Runs seamlessly on Raspberry Pi with support for microphone and speaker.

## Prerequisites

To run this project, you need:

- **Python 3.6+**
- **Raspberry Pi** (preferably 3B+ or later)
- **USB Microphone** for voice input
- **Speakers** for audio output
- **Internet Connection** for the OpenAI API
- **OpenAI API Key** (get yours [here](https://beta.openai.com/signup))

### Required Python Libraries:

Install these using `pip`:

```bash
pip install openai speechrecognition pyttsx3 numpy python-dotenv
```

Additionally, you may need **PyAudio** for microphone input:

```bash
pip install pyaudio
```

## Installation

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/your-repo/voice-assistant-raspberrypi.git
   cd voice-assistant-raspberrypi
   ```

2. **Set Up Environment Variables**:
   Create a `.env` file in the project directory and add your OpenAI API key:
   ```bash
   OPENAI_API_KEY=your-openai-api-key
   ```

3. **Run the Assistant**:
   ```bash
   python assistant.py
   ```

## How It Works

This assistant uses **speech recognition** to listen for the wake word "Hey Assistant." Once activated, it records your next command, processes it through OpenAI's GPT-3.5 Turbo, and replies using a **text-to-speech engine**.

### Code Walkthrough

- **Environment Setup**: 
   - The OpenAI API key is loaded from a `.env` file.
   - The `openai` library is used to interact with GPT-3.5 Turbo.
   - **SpeechRecognition** is used to capture audio from the microphone, and **pyttsx3** handles text-to-speech output.

- **Wake Word Detection**:
   The assistant listens continuously for the wake word ("Hey Assistant"). If detected, it provides a friendly response using a randomized reply from `wake_word_responses`.

- **Processing User Input**:
   Once activated, the assistant captures the next user input, sends it to the OpenAI API for processing, and reads out the response.

- **Fallback**:
   If no valid input is detected, the assistant returns to listening mode, ready for the next wake word.

### Example Code Snippets

1. **Wake Word Detection**:
   ```python
   def listen_for_wake_word(source):
       print("Listening for 'Hey Assistant'...")
       while True:
           audio = r.listen(source)
           try:
               text = r.recognize_google(audio)
               if "hey assistant" in text.lower():
                   print("Wake word detected.")
                   engine.say(np.random.choice(wake_word_responses))
                   engine.runAndWait()
                   listen_and_respond(source)
                   break
           except sr.UnknownValueError:
               pass
   ```

2. **Using OpenAI API**:
   ```python
   response = openai.ChatCompletion.create(
       model="gpt-3.5-turbo", 
       messages=[{"role": "user", "content": f"{text}"}]
   )
   response_text = response.choices[0].message.content
   print(f"OpenAI response: {response_text}")
   ```

3. **Text-to-Speech**:
   ```python
   engine.say(response_text)
   engine.runAndWait()
   ```

## Customization

- **Wake Word and Responses**: Modify the wake word and add new custom responses by editing the `wake_word_responses` list in the code.
- **Voice Settings**: Change the voice by adjusting the TTS engine properties:
   ```python
   voice = engine.getProperty('voices')[1]  # Change to different index for other voices
   engine.setProperty('voice', voice.id)
   ```

- **Additional Commands**: You can extend the functionality by adding more command handlers in the `listen_and_respond` function.

## Troubleshooting

- **Speech Recognition Not Working**:
   Ensure that your microphone is properly set up and recognized by your Raspberry Pi. You can use `arecord` to test the microphone.
   
- **API Errors**:
   Check if the OpenAI API key is valid and properly loaded from the `.env` file.

- **PyAudio Issues**:
   If you encounter installation issues with `pyaudio`, use the following command to install the required dependencies:
   ```bash
   sudo apt-get install portaudio19-dev
   ```

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for more details.

---

Enjoy building your personalized voice-activated assistant with Raspberry Pi and OpenAI! Feel free to extend it to match your needs or integrate it with your smart home setup!
