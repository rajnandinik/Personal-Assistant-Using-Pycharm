# Personal-Assistant-Using-Pycharm
#Creating Your own Personal Assistant using Python libraries.
import speech_recognition as sr
import pyttsx3
import pywhatkit
import datetime
import wikipedia
listener = sr.Recognizer()
engine = pyttsx3.init()
voices = engine.getProperty('voices')
engine.setProperty('voice', voices[1].id)
engine.say('I am your alexa')
engine.say('what can I do for you')
engine.runAndWait()
voices = engine.getProperty('voices')
engine.setProperty('voice', voices[1].id)
def talk(text):
    engine.say(text)
    engine.runAndWait()
def take_command():
    try:
        with sr.Microphone() as source:
            print('listening.....')
            voice = listener.listen(source)
            command = listener.recognize_google(voice)
            command = command.lower()
            if 'alexa' in command:
                command = command.replace('alexa', '')
                print(command)

    except:
        pass
    return command

def run_alexa():
    command = take_command()
    print(command)
    if 'play' in command:
        song = command.replace('play', '')
        talk('playing' + song)
        pywhatkit.playonyt(song)
    elif 'time' in command:
        time = datetime.datetime.now().strftime('%I:%M %p')
        talk('Current time is ' + time)
    elif 'who is' in command:
        person = command.replace('who is', '')
        info = wikipedia.summary(person, 1)
        print(info)
        talk(info)
    elif 'search' in command:
        thing = command.replace('search', '')
        talk('searching' + thing)
        pywhatkit.search(thing)
    elif 'talk' in command:
        talk('hey! I am your alexa what can I do for you')
    elif 'do you love me' in command:
        talk('I am in a relationship with wifi')
    else:
        talk('please say the command again.')
while True:
    run_alexa()


