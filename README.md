# david_zara
import pyttsx3
import datetime
import speech_recognition as sr
import wikipedia
import webbrowser
import os
import smtplib

engine=pyttsx3.init('sapi5')
voices=engine.getProperty('voices')
engine.setProperty('voices',voices[1].id)


def speak(audio):
    engine.say(audio)
    engine.runAndWait()

def wishme():
    hour=int(datetime.datetime.now().hour)
    if hour>0 and hour<12:
        speak("Good Morning!")
    elif hour>12 and hour<18:
        speak("Good Afternoon!")
    else:
        speak("Good Evening!")
    speak("I am  David . Plz tell how may i help you ?")

def take():
    r = sr.Recognizer()
    with sr.Microphone() as source:
        print("Listening...")
        r.pause_threshold = 1
        r.adjust_for_ambient_noise(source)
        audio = r.listen(source)

    try:
        print("Recognizing...")
        query = r.recognize_google(audio, language='en-in')
        print(f"User said: {query}\n")

    except Exception as e:
        # print(e)
        print("Say that again please...")
        return "None"
    return query

def sendEmail(to, content):
    server = smtplib.SMTP('smtp.gmail.com', 587)
    server.ehlo()
    server.starttls()
    server.login('youremail@gmail.com', 'your-password')
    server.sendmail('youremail@gmail.com', to, content)
    server.close()

if __name__ == '__main__' :
    wishme()
    while True:

        query=take().lower()
        if "wikipedia" in query:
            print("Searching on Wikipedia...")
            query=query.replace("wikipedia","")
            result=wikipedia.summary(query,sentences=2)
            result=wikipedia.summary(query,sentences=2)
            speak("According to Wikipedia")
            print(result)
            speak(result)
        elif "abuse" in query:
            speak("You Bloody Shit")    
        elif "open youtube" in query:
            webbrowser.open("youtube.com")
        elif "open stackoverflow" in query:
            webbrowser.open("stackqverflow.com")
        elif "open google" in query:
            webbrowser.open("google.com")
        elif  "time" in query:
            strTime=datetime.datetime.now().strftime("%H:%M:%S")
            print(strTime)
            speak(f"Sir , the time is {strTime}")
        elif 'open stackoverflow' in query:
            webbrowser.open("stackoverflow.com")       
        elif "play music" in query:
            music_dir="D:\\naman\\music"
            songs=os.listdir(music_dir)
            print(songs)
        elif 'the time' in query:
            strTime = datetime.datetime.now().strftime("%H:%M:%S")    
            speak(f"Sir, the time is {strTime}")
        elif "email to naman" in query:
            try:
                speak("what should i say!")
                content=take()
                to="Enter the Email of the Person to which you want to Send Email"
                sendEmail(to,content)
                speak("Email has been sent!")
            except Exception as e:
                print(e)
                speak("sorry sir i am not able to send the email")
        elif "quit" in query:
            exit()    
# Requirments for this project:
# 1.python-3.8.3
# 2.pip install wikipedia for wikipedia
# 3.pip install SpeechRecognition for  SpeechRecognition
# 4.pip install pipwin and pipwin install pyaudio for support in SpeechRecognition module
# 5.pip install pyttsx3 for voices
# 6.pip install pywin32 for error of sapi5
# 7.pip install googlesearch-python for search purpose
