'''jarvis - python code for beginners'''
import pyttsx3
import datetime
import speech_recognition as sr
import wikipedia
import webbrowser
import os

engine = pyttsx3.init("sapi5")
voices = engine.getProperty("voices")
# print(voices[1].id)
engine.setProperty("voices", voices[1].id)


def speak(audio):
    engine.say(audio)
    engine.runAndWait()

def wishme():
    hour = int(datetime.datetime.now().hour)
    if(hour >= 0 and hour<12):
        speak("Good Morning !")
    elif(hour >= 12 and hour<18):
        speak("Good Afternoon !")
    else:
        speak("Good Evening !")
    speak("I am jarvis sir. how can i help you!")

def takeCommand():
    r = sr.Recognizer()
    with sr.Microphone() as source:
        print("Listening...")
        r.pause_threshold = 1
        audio = r.listen(source)

    try:
        print("recognizing...")
        query = r.recognize_google(audio, language="en-in")
        print(f"user said:{query}\n")

    except Exception as e:
        # print(e)
        print("Say that again please...")
        return "None"
    return query

if __name__ == "__main__":
    wishme()
    while True:
        query = takeCommand().lower()

#============logic bulit from here===================#
        if "wikipedia" in query:
            speak("searching wikipedia...")
            query = query.replace("wikipedia", "")
            results = wikipedia.summary(query, sentences=2)
            speak("According to wikipedia")
            print(results)
            speak(results)

        elif "open youtube" in query:
            webbrowser.open("youtube.com")
        elif "open google" in query:
            webbrowser.open("google.com")
        elif "open stackoverflow" in query:
            webbrowser.open("stackoverflow.com")
        elif "play music" in query:
            music_dir = "C:\\Users\\Shweta\\Music\\favorite songs"
            songs = os.listdir(music_dir)
            print(songs)
            os.startfile(os.path.join(music_dir, songs[0]))
        elif "the time" in query:
            strtime = datetime.datetime.now().strftime("%H:%M:%S")
            print(strtime)
            speak(f"sir the time is{strtime}\n")
        elif "thanks jarvis" in query:
            speak("your welcome sir!")
        elif "open code" in query:
            codePath = "C:\\Users\\Shweta\\AppData\\Local\\Programs\\Microsoft VS Code\\Code.exe"
            os.startfile(codePath)

        elif "who are you" in query:
            speak("I am a AI program called jarvis")

        elif "Turn of the music" in query:
            speak("Ok sir!")
            music_dir = "C:\\Users\\Shweta\\Music\\favorite songs"
            songs = os.listdir(music_dir)
            os.close(music_dir,songs[0])
