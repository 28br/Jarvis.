# Jarvis.
Jarvis AI app.
import speech_recognition as sr
import pyttsx3

# Initialize the speech recognizer and engine
recognizer = sr.Recognizer()
engine = pyttsx3.init()

# Function to speak out the given text
def speak(text):
    engine.say(text)
    engine.runAndWait()

# Function to recognize speech
def recognize_speech():
    with sr.Microphone() as source:
        print("Listening...")
        recognizer.adjust_for_ambient_noise(source)
        audio = recognizer.listen(source)

    try:
        print("Recognizing...")
        query = recognizer.recognize_google(audio)
        print(f"User said: {query}")
        return query.lower()
    except Exception as e:
        print("Sorry, I couldn't understand. Please try again.")
        return ""

# Main function to execute the AI
def main():
    speak("Hello! How can I assist you today?")
    while True:
        query = recognize_speech()
        
        if "hello" in query:
            speak("Hello! How can I assist you today?")
        elif "bye" in query:
            speak("Goodbye!")
            break
        elif "what is your name" in query:
            speak("I am an AI assistant.")
        else:
            speak("Sorry, I didn't get that.")

if __name__ == "__main__":
    main()
