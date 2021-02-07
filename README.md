# team-quadtec.github.io
'''SMILES,OUR TEAM HAS DEVELOPED A CHATBOT USING PYTHON WHICH RESPONDS TO THE USERs WISH. U CAN CHECK IT OUT HERE'''
import pyttsx3
import speech_recognition as sr
import datetime 
import wikipedia
import webbrowser
import os 
import smtplib


engine = pyttsx3.init('sapi5')
voices = engine.getProperty('voices')
#print(voices[1].id)
engine.setProperty('voices',voices[1].id)

def speak(audio):
    engine.say(audio)
    engine.runAndWait()


def wishMe():
    hour = int(datetime.datetime.now().hour)
    if hour>= 0 and hour<12:
        speak("Good Morning!")
  
    elif hour>= 12 and hour<18:
        speak("Good Afternoon!")   
  
    else:
        speak("Good Evening!")

    speak("Pysis,at your service ,sir mam, to make your day perfect. What can i do for you?")

def takeCommand():
    #it takes microphone input from the user and returns string output
    r = sr.Recognizer()
    with sr.Microphone() as source:
        print('listening...')
        r.pause_threshold = 1
        audio =r.listen(source)
    try:
        print('recognising...')
        query = r.recognize_google(audio,language='en-in')
        print(f'user said:{query}\n')
    except Exception as e:
        #print(e)

        print('say that again please')
        return "None"
    return query

if __name__ == "__main__":
    wishMe()
    while True:
         query = takeCommand().lower()


         #logic for executing task based on query 
         if "wikipedia" in query:
             speak('searching wikipedia...')
             query = query.replace('wikipedia',"")
             results = wikipedia.summary(query,sentences =2)
             speak("according to wikipedia")
             speak(results)

         elif "open youtube" in query:
             webbrowser.open("youtube.com")
         elif "open google"  in query:
             webbrowser.open("google.com")
         elif "open spec portal" in query:
             webbrowser.open("specnith.com")
         elif "play music" in query:
             music_dir = 'C:\\Users\\anjali\\Downloads\\xyz'
             songs = os.listdir(music_dir)
             print(songs)
             os.startfile(os.path.join(music_dir,songs[0]))
         elif "the time" in query:
             strTime = datetime.datetime.now().strftime("%H:%M:%S")
             speak(f"Sir,the time is {strTime}")
         elif "open code" in query:
             codePath ="C:\\Users\\anjali\\Desktop\\kartik"
             os.startfile(codePath)
