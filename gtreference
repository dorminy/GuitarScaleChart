#!/usr/bin/env python3

import sys
from tkinter import *
from collections import OrderedDict

# This program creates a guitar scale gui from grid elements, and fills them in color-coded appropriately.
# https://github.com/crawsome/GuitarScaleChart
# 2017 Colin Burke, et al contributors from Github :-)

# Get Note name from a 0-11 INT
def getnotename(tonename):
    notedict = ['E ', 'F ', 'F#', 'G ', 'Ab','A ', 'Bb', 'B ', 'C ', 'Db', 'D ', 'Eb']
    return notedict[tonename % 12]

# Contains int offsets, based on note string, added for convenience, which is simply offset relative to C.
def getoffset_tonename(tonename):
    scaleref = {
        'E ': 0, 'F ': 1, 'F#': 2, 'G ': 3, 'Ab': 4, 'A ': 5, 'Bb': 6, 'B ': 7, 'C ': 8, 'Db': 9, 'D ': 10, 'Eb': 11}
    return scaleref[tonename]

# Return array that is rotated circular
def rotate(l, n):
    return l[-n:] + l[:-n]

fretsizes = [5,5,5,5,5,4,4,4,4,3,3,3,3,2,2,2,2,2,2,2,2,2,2,2,2]

scales = OrderedDict([
    ('Major', [0, 2, 2, 1, 2, 2, 2, 1]),
    ('Natural minor', [0, 2, 1, 2, 2, 1, 2, 2]),
    ('Harmonic minor', [0, 2, 1, 2, 2, 1, 3, 1]),
    ('Melodic minor', [0, 2, 1, 2, 2, 2, 2, 2]),
    ('Dorian mode', [0, 2, 1, 2, 2, 2, 1, 2]),
    ('Phrygian mode', [0, 1, 2, 2, 2, 1, 2, 2]),
    ('Lydian mode', [0, 2, 2, 2, 1, 2, 2, 1]),
    ('Mixolydian mode', [0, 2, 2, 1, 2, 2, 1, 2]),
    ('Locrian mode', [0, 1, 2, 2, 1, 2, 2, 2]),
    ('Ahava raba mode', [0, 1, 3, 1, 2, 1, 2, 2]),
    ('Minor pentatonic', [0, 3, 2, 2, 3, 2]),
    ('Pentatonic', [0, 2, 2, 3, 2, 3]),
    ('Blues', [0, 3, 2, 1, 1, 3]),
    ('5 chord', [0, 7]),
    ('Major chord', [0, 4, 3]),
    ('Minor chord', [0, 3, 4]),
    ('Diminished chord', [0, 3, 3]),
    ('Augmented chord', [0, 4, 4]),
    ('Sus2 chord', [0, 2, 5]),
    ('Sus4 chord', [0, 5, 2]),
    ('Maj7 chord', [0, 4, 3, 4]),
    ('min7 chord', [0, 3, 4, 3]),
    ('7 chord', [0, 4, 3, 3]),
    ('7#9 chord',[0, 4, 3, 3, 4]),
    ('min7b5 chord', [0, 3, 3, 4]),
    ('dim7 chord', [0, 3, 3, 3]),
    ('9 chord', [0, 4, 3, 3, 4]),
    ('Maj9 chord', [0, 4, 3, 4, 3]),
    ('m9 chord', [0, 3, 4, 3, 4]),
    ('11 chord', [0, 4, 3, 3, 4, 3]),
    ('Maj11 chord', [0, 4, 3, 4, 3, 3]),
    ('min11 chord', [0, 3, 4, 3, 4, 3]),
])

# returns a scale of 16 notes, from the key tonic + 24
def makescale(keyroot, keyopt):
    keywheel = []
    keywheel.extend(scales[keyopt])
    filler = 0
    # fill array with 16 notes relevant to key and option.
    ourscale = []
    lenvar = len(keywheel)  # of notes we use (2 octaves of key notes)
    for inte in range(lenvar):
        filler += keywheel[inte % len(keywheel)]
        ourscale.append(int(filler + getoffset_tonename(keyroot)))
    return ourscale

# fetches a default scale
ourscale = makescale('E ', 'Major')
# Used for note offsets
e = 0
# high e = (e+4), b = (e-1), g = (e+7), d = (e+2),a = (e+9), low e = (e+4)
# added to each string to offset and identify the notes.
offsetArray = [e, e + 7, e + 3, e + 10, e + 5, e]
# default e Major
fretboard = Tk()
# our callback variables that change when menu options are selected
variable = StringVar(fretboard)
variable.set('E ')
variable2 = StringVar(fretboard)
variable2.set('Major')

# for clearing all our values, used for the "Reset" button.
def resettable():
    bgcolor='white smoke' #notes that aren't in the scale
    for i in range(0, 25):
        for gss in range(0, 6):
            start = offsetArray[gss]            
            if i ==0:
               Col=0
               PadEx=10
               Label(fretboard,borderwidth=2, relief="groove", width=3, text=getnotename(i + start), bg=bgcolor).grid(row=gss + 2, column=Col, padx=0, pady=0)
               Label(fretboard,borderwidth=2, relief="groove", width=1, bg="lemon chiffon").grid(row=gss + 2, column=1, padx=0, pady=0)#draw the nut
            else:
               Col=i+1
               PadEx=0
               Label(fretboard,borderwidth=2, relief="groove", width=fretsizes[i], text=getnotename(i + start), bg=bgcolor).grid(row=gss + 2, column=Col, padx=PadEx, pady=0)

# redraw our whole scale, the action for the "Apply" button
def applyit(val):
    ourtonic = str(variable.get())
    ourkey = str(variable2.get())
    ourscale = makescale(ourtonic, ourkey)
    ournotes = []
    for notes in ourscale:
        ournotes.append(getnotename(notes))
    # draw our whole scale
 #   print(ournotes)
    for i in range(0, 25):
        for gss in range(0, 6):
            start = offsetArray[gss]
            if ourtonic == getnotename(i + start % 12):
              bgcolor='limegreen'  #root notes
            elif getnotename(i + start) in ournotes: 
              bgcolor='medium spring green' #other notes in the scale
            else:
              bgcolor='white smoke' #notes that aren't in the scale
            if i ==0:
               Col=0
               PadEx=10
               Label(fretboard,borderwidth=2, relief="groove", width=3, text=getnotename(i + start), bg=bgcolor).grid(row=gss + 2, column=Col, padx=1, pady=0)
               Label(fretboard,borderwidth=2, relief="groove", width=1, bg="lemon chiffon").grid(row=gss + 2, column=1, padx=1, pady=0)
            else:
               Col=i+1
               PadEx=0
               Label(fretboard,borderwidth=2, relief="groove", width=fretsizes[i], text=getnotename(i + start), bg=bgcolor).grid(row=gss + 2, column=Col, padx=PadEx, pady=0)

if __name__ == "__main__":
    fretboard.geometry('710x220+400+300')
    fretboard.title('Guitar Scale Chart - Colin Burke, 2017')
    fretboard.configure(background='white')
    ourx = 40
    oury = 15
    # For our fret (column) labels on top and bottom
    for i in range(0, 25):
        if i==0:
            PadEx=10
            Col=0
        else:
            PadEx=0
            Col=i+1
        Label(fretboard, text=i, font='Helvetica 10', background='white').grid(row=0, column=Col, padx=PadEx, pady=0)
        Label(fretboard, text=i, font='Helvetica 10', background='white').grid(row=9, column=Col, padx=PadEx, pady=0)

    # draw our whole scale
    applyit("")

    keymenu = OptionMenu(
        fretboard, variable, 'E ', 'F ', 'F#', 'G ', 'Ab', 'A ', 'Bb', 'B ', 'C ', 'Db', 'D ', 'Eb', command=applyit).place(x=ourx * 2, y=oury * 12)

    scalemenu = OptionMenu(fretboard, variable2, *scales.keys(), command=applyit).place(x=ourx * 4, y=oury * 12)

    resetbutton = Button(fretboard, text=' Reset ', command=resettable).place(x=ourx * 10, y=oury * 12)

    fretboard.mainloop()
