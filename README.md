# Alfered
#Virtual Assistant
import pyttsx3  
import datetime
import wikipedia
import webbrowser
import pyjokes
import os
import datetime
import psutil
import pyautogui
import pywhatkit
import smtplib
import speech_recognition as sr
import time as ti
import webbrowser as we
from email.message import EmailMessage
from newsapi import NewsApiClient



user = "Yash"


engine = pyttsx3.init('sapi5')
voices = engine.getProperty('voices')
engine.setProperty('voice', voices[0].id)



def speak(audio):
    engine.say(audio)
    engine.runAndWait()

def wishMe():
    hour = int(datetime.datetime.now().hour) #Module.object.function()
    if hour >= 0 and hour < 12:
        
        speak("Good morning Yash!")
    elif hour >= 12 and hour < 18:
        speak("Good Afternoon Yash!")
    else:
        speak("Good Evening Yash!")

    

def takeCommand():
    r = sr.Recognizer() #Predefined
    with sr.Microphone() as source:
        print("Listening...")
        r.pause_threshold = 1
        audio = r.listen(source)

    try:
        print("Recognizing...")
        query = r.recognize_google(audio, language='en-in')
        print(f"User Said : {query} \n")
    except Exception as e:    
        print(e)
        print("Sorry! Please Say that again!")
        return "None"
    return query

def sendEmail():
    senderemail = "jarvisai330@gmail.com"
    password = "ifdblayqkfmnkluv"
    email_list = {
        "anurag": "anuragmishra7576@gmail.com",
        "yash":"yashmane516@gmail.com",  
    }
    try:
        email = EmailMessage()
        speak("To whom you want to send the mail?")
        name = takeCommand().lower()
        email['To'] = email_list[name]
        speak("What is the subject of the mail?")
        email["Subject"] = takeCommand()
        email['From'] = senderemail
        speak("What should i Say?")
        email.set_content(takeCommand())
        s = smtplib.SMTP("smtp.gmail.com", 587)
        s.starttls()
        s.login(senderemail, password)
        s.send_message(email)
        s.close()
        speak("Email has sent")
    except Exception as e:
        print(e)
        speak("Unable to send the Email")

def sendWhatMsg():
    user_name = {
        'anurag': '+91 7385326428' 
    }
    try:
        speak("To whom you want to send the message?")
        name = takeCommand().lower()
        speak("What is the message")
        we.open("https://web.whatsapp.com/send?phone=" + 
                user_name[name]+'&text='+takeCommand().lower())
        ti.sleep(15)
        pyautogui.press('enter')
        speak("Message sent")
    except Exception as e:
        print(e)
        speak("Unable to send the Message")


if __name__ == "__main__":   
    wishMe()
    while True:
        query = takeCommand().lower()
        print(query)
        if 'alfred' in query:
            speak("how may i assist you!")
            #break
            query = takeCommand().lower()
            print(query)

            if 'bye' in query:
                speak("Thank you Yash, Bye Bye!")
                break
#############
            
            if ("time" in query):
                speak("Current time is " +
                    datetime.datetime.now().strftime("%I:%M"))
               

            elif ('date' in query):
                speak("Current date is " + str(datetime.datetime.now().day)
                    + " " + str(datetime.datetime.now().month)
                    + " " + str(datetime.datetime.now().year))
               

            elif ('email' in query):
                sendEmail()

            elif ('message' in query):
                print("Sending...")
                sendWhatMsg()

            elif ("search" in query):
                speak("what you want to search?")
                we.open("https://www.google.com/search?q="+takeCommand())

            elif ("youtube" in query):
                speak("What you want to search on Youtube?")
                pywhatkit.playonyt(takeCommand())


            elif ("joke" in query):
                speak(pyjokes.get_joke())


            elif ("screenshot" in query):
                pyautogui.screenshot(str(ti.time()) + ".png").show()

            elif "cpu" in query:
                speak(f"Cpu is at {str(psutil.cpu_percent())}")

            elif "offline" in query:
                hour = datetime.datetime.now().hour
                if (hour >= 21) and (hour < 6):
                    speak(f"Good Night {user}! Have a nice Sleep")
                else:
                    speak(f"By {user}")
                quit()

##############
            if 'wikipedia' in query:
                speak('Searching, please wait!')
                query = query.replace("search","")
                results = wikipedia.summary(query, sentences=2)
                speak("I found this on web,")
                speak(results)

            elif 'open facebook' in query:
                speak("Opening facebook!")
                webbrowser.open("facebook.com")

            elif 'open google' in query:
                speak("Opening google!")
                webbrowser.open("google.com")

            elif 'check whatsapp' in query:
                speak("Checking your whats app messages!")
                webbrowser.open("web.whatsapp.com")


    ########################################################
            elif 'play music' in query:
                music_dir = 'D:\\music'
                songs = os.listdir(music_dir)
                print(songs)
                speak("Which Song do you want to listen!")
                query = takeCommand().lower()
                if 'ajeeb' in query:
                    speak("playing ajib dasta hai ye for you sir!")
                    os.startfile(os.path.join(music_dir, songs[1]))
                elif 'abhi' in query:
                    speak("playing abhi na jao chhod kar for you sir!")
                    os.startfile(os.path.join(music_dir, songs[0]))
                elif 'chaudhvin' in query:
                    speak("playing chaudhvin ka chand for you sir!")
                    os.startfile(os.path.join(music_dir, songs[2]))
                elif 'diwana' in query:
                    speak("playing diwana hua badal for you sir!")
                    os.startfile(os.path.join(music_dir, songs[3]))
                elif 'gulbadan' in query:
                    speak("playing ye gulbadan for you sir!")
                    os.startfile(os.path.join(music_dir, songs[4]))
                elif 'ehsan' in query:
                    speak("playing ehsan tera hoga for you sir!")
                    os.startfile(os.path.join(music_dir, songs[5]))
                elif 'wada' in query:
                    speak("playing jo wada kiya for you sir!")
                    os.startfile(os.path.join(music_dir, songs[6]))
                elif 'khoya' in query:
                    speak("playing khoya khoya chand for you sir!")
                    os.startfile(os.path.join(music_dir, songs[7]))
                elif 'tarif' in query:
                    speak("playing taarif karoon kya uski for you sir!")
                    os.startfile(os.path.join(music_dir, songs[8]))
                elif 'tumse' in query:
                    speak("playing tumse accha kon hey for you sir!")
                    os.startfile(os.path.join(music_dir, songs[2]))

    ###################################################################
            elif 'the time' in query:
                strTime  = datetime.datetime.now().strftime("%H:%M:%S")
                speak(F"Sir, The time is {strTime}")

            elif 'open.net' in query:
                codePath = "C:\\Program Files (x86)\\Microsoft Visual Studio 10.0\\Common7\\IDE\\devenv.exe"
                speak("Opening dot net, have a wonderful coding experience sir!")
                os.startfile(codePath)
                
            elif 'open code' in query:
                codePath = "C:\\Users\\sagar\\AppData\\Local\\Programs\\Microsoft VS Code\\Code.exe"
                speak("Opening code, have a wonderful coding experience sir!")
                os.startfile(codePath)
