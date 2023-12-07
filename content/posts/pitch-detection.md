---
title: Pitch Detection
date: 2023-12-05T17:58:32-05:00
draft: false
---
# so you want to pitch detect.

I'm really happy you're into the arts and trust tech enough to look for a software solution, but unless you want to just detect the pitch of a melody (one note at any moment) this is pretty hard to do in the general case.

Background: my brother was complaining about the amount of time it took to write sheet music in notating software for his compositions, and my initial reaction was "that's part of the deal", the idea being that if you're making a composition, you should at least spend the amount of time with it that you'd take to notate it, to give it the kind of care and thought that will make it sound deliberate. My brother usually just comes up with things on the fly after many repetitions of experimenting on the keyboard and will record them and use up all of our iCloud storage, which is very exciting but not great for our picture taking capacity.

So I was thinking about it a little bit more, because it is true that some people can just come up with beautiful pieces after a few minutes of thinking. I didn't really fully believe this until I read the first chapter of *Godel, Escher, Bach*, which was, sure enough, about Bach composing fugues on the spot. So clearly there is a use case for real-time score creation. And I mean, I'm a fan of the youtube video "BMO sings please never fall in love again", which was created via a neural net trained on BMO's voice and that can recreate any melody in that voice! And so I felt confident enough in technology to tell my brother that yeah, there is probably a tech solution to this that might involve a neural net, and I'd look into creating something for him.

Well, I tried to on around Nov 29. Here's how it went.

# naiveté

At first I was just like "neural networks do be too annoying. What if I just take a Fourier transform! I didn't take unified signals for nothing". But there were two issues with this thought. One was I didn't really pay attention in class to the discrete version of this so I didn't have full intuition on how to code this up. But second, I realized what I was looking for actually had to be a *sliding* FT, which I had implicitly required but for some reason in my head I forgot frequencies in FTs weren't calculated per-instant, and that they needed time to accurately detect frequency. Heisenberg inequality style.  Quite obviously the FT of the entire thing would be useless to me.

So then I found ways to convert mp3 files into .wav files so that python could read them into numpy, and then I took a sliding dft using the python library, and simply tried to graph it. I got actual nonsense. it was just noise all the way through. So then I limited the graph to frequencies a piano could reasonably play, and then I got some signal way in the lower section of the graph, where I presume my brother was playing! But it was still too tiny to make out, so I restricted the time axis to a few seconds at the beginning of when he plays (different from the beginning of the recording) and adjusted the stft settings to value note precision over knowledge of when exactly he played it (i.e. lengthen the sliding time). And then I was left with the below graph.

So I was like, cool! I'll figure out what note he's playing, and then I'll graph that horizontal line as well. So it turns out he's playing a c5, and then an f5. I don't graph the entire horizontal line because it would block out the actual heatmap:

The MOST ANNOYING THING about this graph is that the frequencies most represented at each time ARE NOT THE NOTE THAT IS BEING PLAYED.

# annoyance

And so I searched online about what harmonic qualities pianos have, and got some answers about guitars. It turns out that a viable option is recording a note, figuring out the frequency plot, and then using that as a baseline from which you can figure out what all of the other notes are supposed to look like. Mathematica has an article on this, linked here.

But importantly, this is NOT a solution if you're trying to find all of the notes in a chord. Because it's nontrivial to figure out which notes are added together if your harmonic spectrum is all over the place. Or it might have been simple in a better world, but when I searched up solutions for chord detection, people were trying to use neural nets, a sure signal that this problem is just not solvable by normal algorithms yet. People were even writing research papers [todo: link] about ways that they were training them/applying loss. And of course, there were plenty of people just shaking their heads at newcomers to this game and telling them that it was just a very hard problem.

And THEN I was like, okay. My only hope now is using MIDI output, if our piano has that ability. And then I watched [this] youtube video from a guy who turns MIDI output into a score, and it is STILL painstaking detail-oriented work, although maybe not as much as writing every note on the staff. I wonder if my brother would think it's an upgrade. I don't know if the software the guy in the video is using is proprietary, but if it is I guess I'll deal with that problem if I have the luxury of using MIDI.

# that's all folks

Let's do this another time :)

---

aside: as i created the file for this post, i realized how little posts i actually have on here so far. it's a very stark contrast compared to the other vaults!

