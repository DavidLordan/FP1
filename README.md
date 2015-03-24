# Final Project Assignment 1: Exploration (FP1) 
DUE March 25, 2015 Wednesday (2015-03-25)


```
#lang racket

(require net/url)

(define myurl (string->url "http://www.cs.uml.edu/"))
(define myport (get-pure-port myurl))
(display-pure-port myport)
```

### My Library: (rsound)

For the first part our final project I decided to play around with the ‘RSound’ library.  From the description on the library’s site: “This collection provides a means to represent, read, write, play and manipulate sounds.”

The full description can be found here: http://pkg-build.racket-lang.org/doc/rsound/index.html

I decided to experiment with the library’s piano tones.  I did this because it seemed like an easy place to start, as the procedure for creating a sound at a specific pitch is very simple. Calling the ‘piano-tone’ procedure creates note objects, referred to as ‘rsounds’. The piano-tone procedure takes an integer from 0 to 127 to be used as a midi-note number (pitch in this instance).  The rsound objects are then played using the ‘play’ procedure. 

The current strategy for controlling the rhythm of notes being played is to call a sleep procedure to halt the system for a given amount of time, allowing the note to sustain.

For example:
```
(play (piano-tone 48))
(sleep 1)
(play (piano-tone 54))
(sleep 2)
```

The code above plays a piano tone with midi number 48 (C4 on a piano), then pauses for one second while the note sustains. The program then plays midi-note 54 (G4 on a piano) and pauses for two seconds while the note sustains. This pattern can be repeated to play a particular melody of pitches with durations. I have abstracted this pattern away into a few procedures and definitions that are much easier to use. This is described in the following section. I’d also like to mention that from what I understand, the rsound library has a much more sophisticated way to control a sequence of notes rather than calling sleep to control their durations. This is something I intend to spend some time learning and experimenting with, but have not yet done so at this time. 

I began by first defining a series of rsound objects using the piano-tone procedure, giving them their formal musical names. 

Ex:
```
(define e3 (piano-tone 40))
(define f3 (piano-tone 41))
(define f#3 (piano-tone 42))
```

I then created tempo and note-duration definitions. By default, a quarter note (one beat in 4/4 time) is one second (60 bpm). All other note durations are defined similarly. 

Ex:
```
(define tempo 1)

(define trip (/ .333 tempo))
(define eight (/ .5 tempo))
(define quarter (/ 1 tempo))
(define half (/ 2 tempo))
(define whole (/ 4 tempo))
```

The tempo variable allows for the length of time for each note duration to be reduced, making the melody faster as the tempo is increased. 

The playNote procedure then takes note and duration (integer) arguments and plays the given note for the appropriate amount of time. 

Ex:
```
  (define (playNote note length)
  (play note)
  (sleep length))
```

This allows somewhat complex melodies to be generated simply by providing the formal note name and the note duration.

Ex:
```
(playNote d4 trip)
(playNote c5 half)
(playNote g4 quarter)
(playNote f4 trip)
```

My next plan for the project is to store these sequences of notes and durations in lists so that entire melodies can be called by name, rather than built manually note by note. 

* the code that you wrote
* output from your code demonstrating what it produced
* any diagrams or figures explaining your work 
 
The narrative itself should be no longer than 350 words. Yes, you can add more files and link or refer to them. This is github, handling files is awesome and easy!

Ask questions publicly in the Piazza group.

### How to Do and Submit this assignment

1. To start, [**fork** this repository][forking].
1. You might want to [**Clone**][ref-clone] this repository to your computer
  2. (This assignment is just one README.md file, so you can edit it right in github without cloning if you like)
1. Modify the README.md file and [**commit**][ref-commit] changes to complete your solution.
1. [**Push**][ref-push]/sync the changes up to your GitHub (skip this if you didn't clone)
1. [Create a **pull request**][pull-request] on the original repository to turn in the assignment.

<!-- Links -->
[piazza]: https://piazza.com/class/i55is8xqqwhmr?cid=411
[markdown]: https://help.github.com/articles/markdown-basics/
[forking]: https://guides.github.com/activities/forking/
[ref-clone]: http://gitref.org/creating/#clone
[ref-commit]: http://gitref.org/basic/#commit
[ref-push]: http://gitref.org/remotes/#push
[pull-request]: https://help.github.com/articles/creating-a-pull-request
