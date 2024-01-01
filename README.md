# Assistant
This is a basic chat assistant similar to Google assistant.This is building on python language.This project is use different library of python language.
import pyttsx3
import datetime
import speech_recognition as sr
import wikipedia
import webbrowser


engine=pyttsx3.init('sapi5')
voices=engine.getProperty('voices')
print(voices[1].id)
engine.setProperty('voice',voices[1].id)

def jarvisvoice(audio):
    engine.say(audio)
    engine.runAndWait()  

def wish():
    hour=int(datetime.datetime.now().hour)  
    print("---->",hour)  
    if hour>=0 and hour<12:
        jarvisvoice("Good Morning")
    elif hour>=12 and hour<18:
        jarvisvoice("Good Afternoon !")  
    else:
        jarvisvoice("Good Evening !") 



def takecommand():
    r=sr.Recognizer() 
    with sr.Microphone() as source:
        print("Listening....") 
        r.pause_threshold=1
        audio=r.listen(source)    
    try:
        print("Recognizing.....")
        query=r.recognize(audio)
        print("Query : "+ query)
    except Exception as e:
        print(e)
        print("sorry... say that again please")
        return "None"
    return query

jarvisvoice("Hello")
jarvisvoice("I am Alexa")
wish()
jarvisvoice("Welcome to home assistant Alexa")



status=True
while status:
    query=takecommand().lower()
    if "what is" in query or "who is "in query:
        jarvisvoice("searching in wikipedia")
        query=query.replace("wikipedia","")
        result=wikipedia.summary(query,sentences=2)
        print(result)
        jarvisvoice("Accoring to wikipedia...")
        jarvisvoice(result)
    elif "open google" in query:
        webbrowser.open("google.com")
    elif "open youtube" in query:
        webbrowser.open("youtube.com")
    elif "open gmail" in query:
        webbrowser.open("gmail.com")        
