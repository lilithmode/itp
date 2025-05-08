# please, i'm begging you prototype documentation
## play the game [here!](https://lilithmode.itch.io/piby-prototype) (password is: iloveminerva)
### contact me if this doesn't work <3

## Ok. Let's start talking about how this all happened. I'm just gonna write down the important stuff.

#This game uses:
## - Ren'Py (Visual Novel Engine)
## - Python (inside Ren'Py for logic)
## - Sprites and audio for visuals and feedback
## - A coin flip mechanic that affects the story 

# Coin Flip?
### The coin flip is used to decide outcomes at certain story points. It uses Ren'Py's `python:` block with the `random` module. Classic elseif statements coming into play here.

`renpy
init python:
    import random

label coin_flip:
    $ result = random.choice(["heads", "tails"])
    if result == "heads":
        "It's heads."
        jump heads_path
    else:
        "It's tails."
        jump tails_path`
		

# Basic Audio Implementation (easy)
### just uses the basic renpy tags for music, sound, and more
#### i.e: play music "audio/_music/pious.mp3"

# Advanced Audio Implementation (help me)
### Easily the hardest thing that had to be figured out alongside Wen.
#### ended up using the id object to manually put in the voice lines that DIDN'T work,
#### i.e: id setup_minervas_ac231527

# Sprite implementation
### ended up having to make a styles sheet that worked in my favor for positioning the sprites correctly... want to improve upon this framework.

`transform hop:
    pause .15
    yoffset 0
    easein .175 yoffset -10
    easeout .175 yoffset 0
    easein .175 yoffset -4
    easeout .175 yoffset 0
    yoffset 0

transform upclose:
    xpos 0.25 yalign 0.5

transform small_sprite:
    xzoom 0.5
    yzoom 0.5

## mostly for side images
image side bug = "images/sprites/side_bug_neutral.png"
image side bug huh = "images/sprites/side_bug_huh.png"
image side bug nervous = "images/sprites/side_bug_nervous.png"
image side bug wtf = "images/sprites/side_bug_wtf.png"
`

# QUESTIONNAIRE.
#### i wanted to cry. i had to read so many forums for this one.

`screen questionnaire_screen():

    tag menu 

	frame:
        style_prefix "pref"
		xalign 0.5
        yalign 0.5
        xsize 700
        ysize 500
        background Frame("#00ffc088", 10, 10)  
        padding (10, 10)

        viewport:
            scrollbars "vertical"
            mousewheel True
            draggable True
            yfill True
            xfill True

            vbox:
                spacing 20
                text "Social Rehabilitation Reflection Tool" size 30

                text "1. How did you feel about the experience?" size 20
                vbox:
                    textbutton "It was surreal." action SetDict(questionnaire_answers, "q1", "surreal")
                    textbutton "It made me uncomfortable." action SetDict(questionnaire_answers, "q1", "uncomfortable")
                    textbutton "I didn’t really get it." action SetDict(questionnaire_answers, "q1", "confused")

                text "2. What broke the immersion of the program?" size 20
                vbox:
                    textbutton "The Glitches." action SetDict(questionnaire_answers, "q2", "glitches")
                    textbutton "Behavior of the Minervas." action SetDict(questionnaire_answers, "q2", "behaviors")
                    textbutton "My Behavior." action SetDict(questionnaire_answers, "q2", "selfhate")

                text "3. Did the conversations prove useful to self-actualization?" size 20
                vbox:
                    textbutton "Absolutely." action SetDict(questionnaire_answers, "q3", "yes")
                    textbutton "Not sure yet." action SetDict(questionnaire_answers, "q3", "maybe")
                    textbutton "Probably not." action SetDict(questionnaire_answers, "q3", "no")

                text "4. Do you feel encouraged to retry this simulation?" size 20
                vbox:
                    textbutton "Absolutely." action SetDict(questionnaire_answers, "q4", "yes")
                    textbutton "Not sure yet." action SetDict(questionnaire_answers, "q4", "maybe")
                    textbutton "Probably not." action SetDict(questionnaire_answers, "q4", "no")

                text "5. Is this enough, yet, Bug?" size 20
                vbox:
                    textbutton "No." action SetDict(questionnaire_answers, "q5", "no")
                    textbutton "No." action SetDict(questionnaire_answers, "q5", "no")
                    textbutton "No." action SetDict(questionnaire_answers, "q5", "no")

                if all(questionnaire_answers.values()):
                    textbutton "Submit" action Return()
                else:
                    text "Please answer all questions to continue." size 15 color "#999"`

# Text Implmentation
#### Wen and I tag teamed this so hard. involves a lot of interesting pause effects for text, and how that sound is implemented when the protag types to the minervas in the terminal.
`    # This function is optional. Only include it if you want automatic pauses between punctuation
    def typography(what):
        replacements = [
                ('. ','. {w=.2}'), # Moderate pause after periods
                ('? ','? {w=.25}'), # Long pause after question marks
                ('! ','! {w=.25}'), # Long pause after exclamation marks
                (', ',', {w=.15}'), # Short pause after commas
        ]
        for item in replacements:
            what = what.replace(item[0],item[1])
        return what
    config.say_menu_text_filter = typography # This ensures the text block has the same ID value, even after all the replacements are made

# wen testing soundfonts implementation for terminal (bug)
    def typing_sounds(event, interact=False, **kwargs):
        if event == "show":
            what = renpy.store._last_say_what
            if what:
                words = what.split()
                for i in range(len(words)):
                    randosound = renpy.random.randint(1, 5)
                    renpy.sound.queue(f"audio/_sfx_typing_dirty/Bfxr_type_{randosound}.mp3", channel="sound", loop=False)
        elif event == "end" or event == "slow_done": # This stops the text sounds if there is a pause in the dialog or the text has finished displaying
            renpy.sound.stop(channel="sound")`
			
#### overall, i think this was a pretty fun job to do with everyone involved and I'm looking forward to see how we can polish this!