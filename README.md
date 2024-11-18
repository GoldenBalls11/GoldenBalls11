def listen():
    r = sr.Recognizer()
    with sr.Microphone() as source:
        print("Listening...")
        audio = r.listen(source)
        try:
            print("Recognizing...")
            query = r.recognize_google(audio, language='en-us')
            print(f"User said: {query}\n")
            return query
        except Exception as e:
            print("Sorry, I didn't catch that. Could you please repeat?")
            return "None"

def greet():
    hour = datetime.datetime.now().hour
    if 0 <= hour < 12:
        speak("Good morning, sir!")
    elif 12 <= hour < 18:
        speak("Good afternoon, sir!")
    else:
        speak("Good evening, sir!")
    speak("I am Jarvis, your AI assistant. How may I help you today?")

def process_command(command):
    if 'wikipedia' in command.lower():
        speak('Searching Wikipedia...')
        query = command.replace("wikipedia", "")
        results = wikipedia.summary(query, sentences=2)
        speak("According to Wikipedia")
        print(results)
        speak(results)
    elif 'open youtube' in command.lower():
        webbrowser.open("https://www.youtube.com")
        speak("Opening YouTube")
    elif 'open google' in command.lower():
        webbrowser.open("https://www.google.com")
        speak("Opening Google")
    elif 'time' in command.lower():
        strTime = datetime.datetime.now().strftime("%H:%M:%S")
        speak(f"Sir, the time is {strTime}")
    elif 'exit' in command.lower():
        speak("Goodbye, sir. Have a great day!")
        return False
