# 🎤 Voice-Activated Personal Assistant

A powerful, extensible desktop voice assistant that responds to your commands just like Siri or Alexa. Built with Python, Claude AI, and modern speech recognition technology.

<div align="center">

![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)
![License](https://img.shields.io/badge/License-MIT-green.svg)
![Platform](https://img.shields.io/badge/Platform-macOS%20%7C%20Linux%20%7C%20Windows-blue.svg)

**[Features](#features)** • **[Quick Start](#quick-start)** • **[Usage](#usage)** • **[Configuration](#configuration)** • **[Extensions](#extensions)**

</div>

---

## ✨ Features

### Core Capabilities
- 🎙️ **Continuous Voice Listening** - Always ready to respond to your wake word
- 🧠 **AI-Powered** - Uses Claude AI for intelligent, context-aware responses
- 🌍 **Multi-Task Support** - Weather, news, reminders, timers, and more
- 🔊 **Natural Speech** - Text-to-speech with adjustable speaking speed
- 💬 **Conversation Memory** - Maintains context across multiple interactions
- 🎯 **Wake Word Detection** - Say "Assistant" to activate (customizable)

### Built-in Tasks
| Task | Command | Example |
|------|---------|---------|
| **Weather** | "What's the weather?" | Fetches current weather with temperature, humidity, wind |
| **News** | "Tell me the news" | Gets top headlines from NewsAPI |
| **Time** | "What time is it?" | Announces current time |
| **Date** | "What's today's date?" | Announces current date |
| **Reminders** | "Remind me in 10 minutes" | Sets voice-activated reminders |
| **Jokes** | "Tell me a joke" | Generates funny jokes |
| **Calculations** | "What is 25 times 4?" | Performs math calculations |
| **Smart Home** | "Turn on the light" | Controls IoT devices (extensible) |
| **Music** | "Play my playlist" | Controls Spotify (extensible) |

### Advanced Features
- 📝 Multi-turn conversation with context awareness
- 🔐 Secure API key management
- 🎨 Modern PyQt6 GUI with real-time status
- 🧩 Fully extensible architecture
- 💾 Persistent reminders and configuration
- 🌐 Cross-platform (macOS, Linux, Windows)

---

## 🚀 Quick Start

### 1. **Clone or Download**
```bash
cd voice-assistant
```

### 2. **Run Setup Wizard** (Recommended)
```bash
python setup.py
```
This will guide you through:
- Python version verification
- System dependency installation
- API key configuration
- Microphone testing

### 3. **Manual Setup** (Alternative)
```bash
# Install Python dependencies
pip install -r requirements.txt

# Create .env file with API keys
cp .env.example .env
# Edit .env with your actual API keys

# Run the assistant
python voice_assistant.py
```

### 4. **Start Using**
- The GUI window appears and starts listening
- Say **"Assistant"** to activate
- Give your command
- The assistant responds and speaks the answer

---

## 💬 Usage

### Voice Commands

#### Basic Commands
```
"What's the weather?"
"Tell me the news"
"What time is it?"
"What's today's date?"
```

#### Reminders & Timers
```
"Remind me to call mom in 30 minutes"
"Set a timer for 5 minutes"
"Wake me up at 7 AM"
```

#### Smart Home (Extensible)
```
"Turn on the lights"
"Set temperature to 72 degrees"
"Lock the front door"
"Dim the lights to 50%"
```

#### Music & Entertainment (Extensible)
```
"Play my favorite playlist"
"Skip to the next song"
"Play Bohemian Rhapsody"
"Pause the music"
```

#### Conversational
```
"Tell me a joke"
"How are you?"
"What can you do?"
"How's my day looking?"
```

#### Complex Commands
The AI intelligently parses complex requests:
```
"What's the weather in Paris and tell me if I need an umbrella?"
"Set a reminder for my meeting at 3 PM and turn off the lights"
"Give me a weather summary for next week and the top 5 news stories"
```

### Using the GUI

**Status Indicators:**
- 🔴 **Ready** (Green) - Listening for wake word
- 🔴 **Listening...** (Red) - Processing voice input
- 🟢 **Processing** - Handling your command

**Buttons:**
- **🎙️ Test Command** - Test without saying the wake word
- **⏹️ Stop** - Stop the assistant

**Display Areas:**
- **Transcript** - Shows what you said
- **Response** - Shows the assistant's reply

---

## 🔧 Configuration

### API Keys

Create a `.env` file (copy from `.env.example`):

```bash
# Required
ANTHROPIC_API_KEY=sk-ant-xxxxx

# Optional but recommended
WEATHER_API_KEY=your_openweather_key
NEWS_API_KEY=your_newsapi_key

# For extensions
SPOTIFY_CLIENT_ID=your_spotify_id
GOOGLE_CALENDAR_API_KEY=your_calendar_key
```

**Where to get keys:**
- **Anthropic**: https://console.anthropic.com/
- **OpenWeather**: https://openweathermap.org/api (free tier available)
- **NewsAPI**: https://newsapi.org/ (free tier available)
- **Spotify**: https://developer.spotify.com/
- **Google Calendar**: https://console.cloud.google.com/

### Customization

**Change Wake Word:**
Edit `voice_assistant.py` line 119:
```python
self.wake_word = "assistant"  # Change to "alexa", "hey siri", etc.
```

**Adjust Speech Speed:**
Edit line 131:
```python
self.tts_engine.setProperty('rate', 150)  # 50-300 words per minute
```

**Modify Noise Detection:**
Edit line 138:
```python
self.recognizer.adjust_for_ambient_noise(source, duration=1)  # Increase for noisy environments
```

---

## 🧩 Extensions & Integrations

The assistant is fully extensible. See `extensions_example.py` for templates to add:

### Available Extensions (Examples Provided)

1. **Calendar Integration** (Google Calendar)
   ```python
   from extensions_example import CalendarIntegration
   calendar = CalendarIntegration()
   calendar.get_upcoming_events()
   ```

2. **Music Control** (Spotify)
   ```python
   from extensions_example import SpotifyIntegration
   spotify = SpotifyIntegration()
   spotify.play_track("Song Name")
   ```

3. **Smart Home** (IoT Devices)
   ```python
   from extensions_example import SmartHomeIntegration
   smart_home = SmartHomeIntegration()
   smart_home.toggle_light()
   ```

4. **Email Integration**
   ```python
   from extensions_example import EmailIntegration
   email = EmailIntegration("your@email.com", "password")
   email.send_email("recipient@email.com", "Subject", "Body")
   ```

5. **Advanced Command Parser**
   ```python
   from extensions_example import AdvancedCommandParser
   parser = AdvancedCommandParser()
   parser.parse_smart_reminder("remind me about meeting in 30 mins")
   ```

### Creating Custom Commands

Add to `TaskExecutor.execute_task()`:

```python
elif 'your_keyword' in command_lower:
    return self.your_custom_function(command)
```

Or use the `CustomCommandRegistry`:

```python
from advanced_features import CustomCommandRegistry

registry = CustomCommandRegistry()
registry.register(['your_trigger'], your_handler_function)
result = registry.execute(user_input)
```

---

## 📊 Architecture

```
┌─────────────────────────────────────────┐
│   Voice Assistant Application           │
├─────────────────────────────────────────┤
│                                         │
│  ┌─────────────────────────────────┐   │
│  │  Voice Processing Layer         │   │
│  │  • Speech Recognition (Google)  │   │
│  │  • Wake Word Detection          │   │
│  │  • Text-to-Speech (pyttsx3)     │   │
│  └─────────────────────────────────┘   │
│              ↓                          │
│  ┌─────────────────────────────────┐   │
│  │  Task Execution Engine          │   │
│  │  • Claude AI Integration        │   │
│  │  • Weather/News APIs            │   │
│  │  • Reminders & Timers           │   │
│  │  • Custom Commands              │   │
│  └─────────────────────────────────┘   │
│              ↓                          │
│  ┌─────────────────────────────────┐   │
│  │  User Interface (PyQt6)         │   │
│  │  • Real-time Status             │   │
│  │  • Command Transcript           │   │
│  │  • Response Display             │   │
│  └─────────────────────────────────┘   │
│                                         │
└─────────────────────────────────────────┘
```

---

## 🐛 Troubleshooting

### Common Issues

**"Microphone Not Found"**
```bash
python -m speech_recognition
```
Check system audio settings and microphone permissions.

**Speech Recognition Errors**
- Ensure internet connection (Google Speech Recognition API)
- Speak clearly and at normal pace
- Check microphone volume

**Text-to-Speech Issues**

macOS:
```bash
brew install espeak
```

Linux:
```bash
sudo apt-get install espeak python3-dev
```

**API Errors**
- Verify `.env` file exists in project directory
- Check API key validity on provider websites
- Ensure internet connection

**Wake Word Not Detected**
- Speak clearly with proper pronunciation
- Adjust `adjust_for_ambient_noise` duration
- Check microphone sensitivity

---

## 📋 Project Files

```
voice-assistant/
├── voice_assistant.py          # Main application
├── advanced_features.py        # Advanced features & managers
├── extensions_example.py       # Integration examples
├── setup.py                    # Interactive setup wizard
├── requirements.txt            # Python dependencies
├── .env.example                # API key template
├── SETUP_GUIDE.md              # Detailed setup instructions
└── README.md                   # This file
```

---

## 🔐 Privacy & Security

- ✅ Speech recognized by Google Speech Recognition API
- ✅ Commands processed by Anthropic's Claude API
- ✅ Weather/News from public APIs
- ✅ **No local storage of voice recordings**
- ✅ API keys stored in local `.env` file
- ✅ **Never commit `.env` to version control**

---

## 🚀 Future Enhancements

- [ ] Local speech recognition (offline mode)
- [ ] Wake word customization UI
- [ ] Multiple user profiles
- [ ] Voice biometric authentication
- [ ] Mobile companion app
- [ ] Multi-language support
- [ ] System tray integration
- [ ] Keyboard hotkey activation (Cmd+Space)
- [ ] Advanced natural language understanding
- [ ] IoT device auto-discovery
- [ ] Machine learning for personalization
- [ ] Cloud sync for reminders/config

---

## 📝 Code Examples

### Basic Usage

```python
from voice_assistant import VoiceAssistantApp
import sys
from PyQt6.QtWidgets import QApplication

app = QApplication(sys.argv)
assistant = VoiceAssistantApp()
assistant.show()
sys.exit(app.exec())
```

### Custom Task

```python
from voice_assistant import TaskExecutor

executor = TaskExecutor()
response = executor.execute_task("What's the weather in London?")
print(response)
```

### Custom Command

```python
from advanced_features import CustomCommandRegistry

registry = CustomCommandRegistry()

def my_handler(text):
    return "You said: " + text

registry.register(['my command'], my_handler)
result = registry.execute("my command do something")
```

---

## 💡 Tips & Tricks

1. **Natural Phrasing** - Speak as you would to a human
2. **Context Awareness** - The assistant remembers previous commands in the conversation
3. **Combine Commands** - Ask for multiple things in one sentence
4. **Customize Wake Word** - Make it memorable and easy to pronounce
5. **Use Hotkey** - Add to system startup for always-on assistant
6. **Extend Features** - Check `extensions_example.py` for templates

---

## 🤝 Contributing

This project is open for extensions and improvements:
1. Add new integrations to `extensions_example.py`
2. Improve command parsing in `advanced_features.py`
3. Add new task handlers to `TaskExecutor`
4. Enhance GUI with PyQt6

---

## 📄 License

This project is provided as-is for personal and educational use.

---

## 🙋 Support

**Having issues?**
1. Check the [Troubleshooting](#-troubleshooting) section
2. Review `SETUP_GUIDE.md` for detailed instructions
3. Verify all API keys are correctly set
4. Check internet connection
5. Review error messages in the UI

---

## 🎉 Getting Started Now!

```bash
# 1. Run setup wizard
python setup.py

# 2. Start the assistant
python voice_assistant.py

# 3. Say "Assistant" and start commanding!
```

**Happy voice commanding!** 🎤✨

---

