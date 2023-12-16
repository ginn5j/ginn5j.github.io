---
title: "Recovering the 2005 KublaCon GeekSpeak Redux"
date: 2011-07-04T13:11:18-04:00
excerpt: "Here is the tale (originally posted at BoardGameGeek.com) of the audio I recovered from the live GeekSpeak hosted by Scott Alden (aka Aldie) and Derk Solko at the 2005 KublaCon gaming convention."
type: post
permalink: /blog/2011/07/04/recovering-the-2005-kublacon-geekspeak-redux/
---
_This is an article I wrote and posted on the BoardGameGeek web site several years ago after recovering the audio for Scott Alden (Aldie) from a session recorded at the 2005 KublaCon gaming convention. I'm re-posting this to my blog to have all of my on-line writing in a central location. I also thought some of my geeky, non-gamer friends would enjoy the tale..._

## Finding Apple Lossless Audio -or- Salvaging BoardgameSpeak from the Trash

I wrote this article to record what transpired between Friday (3 Jun 2005) and Sunday (5 Jun) leading up to the recovery of the digital audio recorded during a live GeekSpeak that took place on Saturday (28 May 2005) at KublaCon. I will go into considerable depth about how I arrived at the solution, including an explanation of the audio format Aldie uses to record GeekSpeak and the program I wrote to extract the essential information from the audio file. Due to the technical nature of the subject, the discussion may get heavy at times. Whenever I start down that path, I'll warn you so you can skip ahead to the next section if you so desire.

### --- My Background ---

As you've probably guessed, I'm a software development professional. I've written software for platforms ranging from IBM mainframes to various Unix platforms to the Macintosh and Windows using Assembly, BASIC, Pascal, Scheme, FORTRAN, C, C++, Forte and Java to name a few. 🙂 This has been going on since the early '80s. I have an undergraduate degree in Computer Science from Indiana University. I've always enjoyed tough technical challenges like this and don't see them nearly often enough these days. I'm what's known as a 'technical architect' at work. During the day, I advise, consult and review solution delivery projects. I stay abreast of current technology trends and help junior technologists learn the ropes. As often as possible, I get involved in writing some software. It's my belief that an architect has more impact when he/she demonstrates more than a moderate understanding of the technology he/she is advising and consulting on with project teams. At night I'm a geek like all of you! My geek interests tend toward music and books in addition to board games.

### --- The Problem ---

Aldie posted the call for help on Wednesday (1 Jun) afternoon. For whatever reason, I completely missed the thread until late Friday afternoon at work. I took a break from working on a document to browse over to the 'Geek and noticed the request. I read through the thread. There were more than 60 replies at this point. I got the feeling there was a lot of frustration because not a lot of progress had been made in the 48 hours since Aldie called on the community for assistance. I didn't realize it until later when I was analyzing the file but Sterling (sbabcock) was on the right track by working on the suggestion by Andreas Resch (Gonzaga) to look at the header information for the file. At that point in time, I thought, "Wow! Cool problem!" between "It doesn't look very promising" and "Man, that'll be a lot of work."

I finished up at work and headed home. We didn't have anything going on Friday evening and the kids were running around outside since it was so nice. I took a look at the thread again and decided, "What the heck, let's take a run at this and see where it leads." I pulled down the file and proceeded to do what everyone else had done --- try to open it with every imaginable audio tool known to mankind. Here's a laundry list of what I tried:

  * AACMachine
  * ALAC (the ALAC decoder)
  * Audacity
  * Audio Identifier
  * Audition (formerly CoolEdit)
  * BeSweet
  * dBpowerAmp
  * iTunes
  * MP4Box
  * mpeg4ip
  * QuickTime
  * wbias
  * WinAmp

The only application that would even open the file was Audacity. It thought the file was an MP3 and gave me the same result as Aldie --- a second and a half of garbled noise. Hmmm, so much for the possibility of a quick resolution. That's OK, I didn't really believe that path would lead anywhere productive. Still, it needed to be explored. By then, it was late because I had spent a lot of time googling to find other audio utilities I'd not used before. It must've been at least 10 or 11pm before I moved on to looking at the file itself.

There were suggestions in the thread that the header (or the lack of one) was the problem. I popped a CD into my computer and opened up iTunes. I recorded one of the tracks into the Apple Lossless Audio format and opened both of the files in a hex editor. For those that don't make a living writing software, a file in its most basic form is nothing more than a collection of numbers and a hex editor is an application that shows you all the numbers that make up a file.

### --- Interlude ... You BIT me?!? A HEX on you if I see you BYTE anybody else! ---

This next part will get a little heavy but here are a couple more definitions if you don't know a lot about computers and want to follow along. First, the most basic piece of information on a computer is a bit. A bit is a number that only has two possible values, 0 or 1 --- off or on --- and that's because when you get down to the most fundamental concepts used by computers, they only understand 0 and 1 --- off and on. When you put 8 bits together, you have something known as a byte. A byte can represent any number between 0 and 255. Representing numbers as a series of 0s and 1s is great for computers but it's very difficult for us humans to deal with on a daily basis. However, representing this sort of thing with the way we usually count (by 10) doesn't work well either. With binary numbers (i.e. counting with 0s and 1s only), I'm essentially using powers of 2 to count and this doesn't translate gracefully into our system of counting by 10. Instead, we count by 16 (yes, a power of 2! 2 to the 4th specifically) and although this isn't as easy as counting by 10, it is better than counting by 2. But to count in hexadecimal (i.e. by 16) I need additional symbols to represent the additional numbers. Normally, when I get to the number ten in decimal, I need 2 symbols to represent the number, a 1 and a 0 --- 10. In hex, I want to use only 1 symbol to represent numbers until I get to 16. So for numbers between 10 and 15, I use the first few letters of the alphabet -- A to F. When I want to write ten in hex, I write A instead. Eleven is B, twelve is C and so on to fifteen which is F. Sixteen is written as 10. This is difficult to grasp at first but what it means is I can represent a byte that is made up of eight bits (or eight symbols) with only two symbols in hex! Some examples:

    Decimal     Binary   Hexadecimal
          0   00000000            00
          1   00000001            01
         10   00001010            0A
         16   00010000            10
         63   00111111            3F
        255   11111111            FF

That's a crash course in bits, bytes and hexadecimal. Now back to the show and what I saw when I opened the files.

### --- An Inkling and a Little Success ---

When I was looking at the files in the hex editor, it was obvious there was a significant difference between the two files. The track I'd recorded had what appeared to be a lot of information at the beginning of the file that the GeekSpeak file did not have. None of it made any sense at this point but there were a few short snippets of text that suggested meaning and that could be used for more googling. "Hey, I thought you were looking at a bunch of numbers! How could you tell there was text in the file," you ask? Let me show you:

    00 00 00 20 66 75 79 70 4D 34 41 20 00 00 00 00 ; ... ftypM4A ....
    4D 34 41 20 6D 70 34 32 69 73 6F 6D 00 00 00 00 ; M4A mp42isom....
    00 00 31 9F 6D 6F 6F 76 00 00 00 6C 6D 76 68 64 ; ..1Ÿmoov...lmvhd
    00 00 00 00 BE C6 84 32 BE C6 84 52 00 00 02 58 ; ....¾Æ„2¾Æ„R...x

On the left are the first 64 bytes from the audio track I recorded displayed in hexadecimal. On the right are the same 64 bytes but they are displayed with the characters you'd see if you opened the file with a text editor. Except for the 00 or null bytes that is. They are shown as periods on the right but would either show up as spaces in a text editor or possibly not at all. You can see that there are some things that probably have some meaning --- ftyp, moov, mvhd. In looking at the Geekspeak file, the ftyp tag was present but moov and mvhd weren't (there are a lot of others that came after these first 4 lines that I'm not showing at the moment). The GeekSpeak file looked like this:

    00 00 00 20 66 75 79 70 4D 34 41 20 00 00 00 00 ; ... ftypM4A ....
    4D 34 41 20 6D 70 34 32 69 73 6F 6D 00 00 00 00 ; M4A mp42isom....
    07 C9 C3 D0 6D 64 61 74 00 00 00 00 00 13 08 09 ; .ÉÃÐmdat........
    2D F9 20 00 B0 01 A5 FF 00 92 CB FE 00 A9 AF FE ; -ù .°.¥ÿ.’Ëþ.©¯þ

Instead of moov and mvhd, I found mdat. The track I recorded had that too but it was much later in the file. Time to do some googling. If you google for 'moov' or 'mvhd,' you won't end up where I did. For some reason, I googled on a tag that occurred later in header information. When you google on 'stsz,' the first hit will take you to Apple's developer website and more specifically to the documentation that explains the meaning of this tag. If you want to explore how Apple defines the data that belongs at the beginning of their media files, start with the 'moov' tag ([QuickTime File Format Reference](https://developer.apple.com/library/mac/#documentation/QuickTime/QTFF/QTFFPreface/qtffPreface.html)).

Some might consider it fate, others would say it was just dumb luck, a shot in the dark. Perhaps I was channeling some long forgotten Irish ancestor or maybe I was in some Zen-like state. Regardless, I was at the place on the web that had a key piece of the puzzle I needed to salvage the GeekSpeak. So what is so special about the 'stsz' tag? Well, before I answer that, let's talk about audio files a little.

### --- Interlude ... Anatomy of Digital Audio ---

You can think of digital audio sort of like the film on a movie reel. The film is a sequential set of image stills that when played in the proper sequence and at the correct speed provides a playback of the visual action that occurred at the time of recording. Digital audio works the same way. It is a series of audio snapshots (or frames) that when played in the right order and at the correct speed, we hear the sound that was previously recorded. In order to play a recording properly, you need to be able to determine where one frame ends and the next begins. With a physical media like film, it's relatively easy since each frame is the same size and you can visually tell one from the next. With digital audio, it's a little more difficult. Either you need a pattern (e.g. a unique series of numbers) that marks the beginning and end of a frame and make sure that the pattern cannot show up somewhere in between or you need to know where the audio data starts and you need to know how big each frame is. Can you guess where this is going?

### --- An Inkling and a Little Success, continued ---

In the case of the Apple Lossless Audio format, the audio data are all those numbers that come after the 'mdat' tag in the file and there is no pattern defined to mark the beginning or end of the frames. That means I need to know how big each frame is and that's where the 'stsz' tag comes into play. The 'stsz' tag defines how many frames are in the audio track and it also contains an ordered list of numbers that tells me how big each frame is. When I say ordered list, I mean that the first number in the list tells me how big the first frame is, the second tells me how big the second is and so on right through the end of the list. This is great, right?!? I mean, all I have to do is copy the header information from the track I recorded and add it to the beginning of the GeekSpeak file. Then, I can create a new 'stsz' tag with the number of frames and their sizes and we're golden! Hmmm, not quite. Except for the frame that begins right after the 'mdat' tag, I have no idea where any of the other frames start so I can't determine how many are in the file or how big they are. Rats! As it turns out though, I haven't run out of luck yet.

I took a look at the GeekSpeak file right after the 'mdat' tag. It looked like:

    07 C9 C3 D0 6D 64 61 74 00 00 00 00 00 13 08 09 ; .ÉÃÐmdat........
    2D F9 20 00 B0 01 A5 FF 00 92 CB FE 00 A9 AF FE ; -ù .°.¥ÿ.’Ëþ.©¯þ

The first 4 bytes (07 C9 C3 D0) represent the length of the 'mdat' section in bytes. That number in decimal is 130,663,376. The file size was 127MB so that number looks about right (a megabyte is approximately 1 million bytes --- it's actually a little more than that --- the power of 2 strikes again!). The next 4 bytes is the tag and you can see it represented in text on the right side. After that, it's all audio data for the next 130 million bytes. The whole recovery operation hinged on what I did next. If what I tried next hadn't worked the way it did, I'm almost positive the audio would not have been recoverable. So, I'm looking at those next few numbers and as you can see, there are 5 zero bytes in a row. I thought to myself, "What if the software Aldie uses starts every frame with those 5 zero bytes?" I saved the position of that first zero byte in Excel. Then, I searched for the next place in the file that had the same pattern and I saved that in Excel. I did a couple more and then I took the difference between each of the values to find out what the size would be for each frame if I used that technique to search for the frames. The values looked reasonable so I located the first 11 places that pattern occurred so I could generate 10 frames. Here's what I found (all values are in decimal):

    Position  Difference from next position
         658         4086
        4744         4765
        9509         4277
       13786         4486
       18272         4322
       22594         4305
       26899         4851
       31750         4410
       36160         3705
       39865         3900

As you can see, the hypothetical frame size clusters nicely around the value 4000. I think this is a good sign and I copy the header from the file I recorded and create an 'stsz' section with these values. This wasn't everything I did because I'd also been looking around at the documention on Apple's developer site and had discovered that the 'stsz' tag was an element of a larger tag known as the Sample Table or 'stbl' for short. This tag has several elements that define additional information about the audio in the file. The other important tag at this point was the 'stco' tag or the Chunk Offset tag. It's a little more complicated than this but basically, this tag stores the position of where the audio data starts. In my list of frames above, that would be 658. After I added the new header and the frame information, this was no longer the correct position but you get the general idea.

At this point, I opened the file in QuickTime and hit Play. It didn't really sound like anything reasonable. In fact it was one of those times when I played the file and wished I hadn't. The noise that erupted from the speakers physically hurt. Still, I was sure I was heading in the right direction. I did a little more reading and adjusted values in a couple of other tags that defined the duration of the track. I didn't really understand how to calculate these values yet but I knew that the track I recorded was several minutes long and with only 10 frames of audio defined, the values needed had to be much smaller. This seemed to help. Even so, this wasn't enough to be sure that this technique would work. The GeekSpeak file was much too large to extract the frame information by hand. It would require a program to find all the information but I really wanted to have a short sample of audio from the GeekSpeak file that sounded reasonably like it should.

To reach that goal, I needed more frames. So, before I even started to think about the possibility of a program, I went back through the audio data and searched for the pattern until I had recorded enough positions to calculate 100 frame sizes. I went through the same process of adjusting the header information with the additional frame information. I was working from a copy of the GeekSpeak file and cut off all the data after the end of what I believed to be the end of the 100th frame. I played this file and thought I could faintly hear what sounded like someone talking but there was also a lot of white noise. In the BoardGameGeek thread, it was mentioned that the GeekSpeak was recorded in mono and I knew the file I had recorded was in stereo but I didn't have any control over those parameters in iTunes. I continued to dig through the information on Apple's site and eventually came across a tag ('smhd') that controlled the stereo balance for the file. The first value I tried (+1) pushed the balance to the right and all I heard was noise. I went back and used -1 to push it to the left. When I did this, I could plainly hear someone saying something about "push the bolt ... rather than ..." Needless to say, I was extremely excited and was confident that most, if not all, of the audio could be recovered!! It was also 3 in the morning and I'd been up since about 5:30. I made my first post to the thread and told everyone that I had recovered about 3 seconds of audio and could tell it was people talking. I sent the file to Aldie and went to bed. I was excited but I was also beat!

### --- Grokking the Header ---

I got up about 8 and checked to see if there'd been any activity. Nothing yet. Since I'd had a few hours of sleep, I started thinking about what it would take to write a program that would search the entire file and find all the frames and their sizes. This was really the only option. I estimated from the size of the file that there would have to be between 30 and 40 thousand frames. No way I'm doing that by hand! Even if you could wade through 1000 frames a day, that would be a solid month of work to recover the audio. So, I created a new file and was just starting to write a little code when I received a reply from Aldie. He was excited that I'd recovered something but when he played the file, it sounded garbled. I was concerned that he wasn't hearing the same thing I was. I knew my header information still needed a lot of work and that bad data was likely causing the file to play differently on different computers and different software. I asked if he had any other files that had been recorded with the same software. I wanted to compare the differences between how iTunes and Audio Hijack recorded tracks. Aldie obliged with a couple of 1 minute tracks. One was a minute of silence and the other was a minute of music. I pulled them down from BGG and starting comparing them to the file I'd recorded and looking up information on Apple's site.

We had family activities on and off throughout the day. When Aldie indicated he had difficulty playing the file, I decided writing the program could wait. It was more important to grok (Robert Heinlein coined this word in his book "Stranger in a Strange Land" --- it means to understand something so well it becomes a part of you) the header and so I worked at figuring out the different elements of the header when I had time during the day. By Saturday evening, I'd spent enough time with the header that I knew which parts needed to be changed and what the right values were or how to calculate them. Here are some of the 'truths' I uncovered during the day:

#### The number of frames per second

I needed to know this so I could calculate accurate durations. Later, when I had all the frame information, I would need to calculate how long the track was to set the correct duration and all I would be able to work from would be the number of frames in the file. I found this value by dividing the number of frames in each of the sample tracks Aldie created by their time in seconds. Both tracks yielded the same answer --- 10.766657 --- so I was sure this was correct.

#### Media units per second

This value is in a couple of different places in the header. The value translated to 44100 and is a standard value for audio recording.

#### Duration

This threw me for a little while but I finally 'got it' after I translated the previous value. The duration of the track in media units is stored here. The formula to calculate this value is (Number of Samples / 10.766657) * 44100. I had to set this value in 3 different tags --- 'mvhd', 'tkhd' and 'mdhd'.

#### Length

The first 4 bytes of each tag was the length or the size of the tag. Since the 'stsz' tag varied in size depending on the number of frames I defined, I had to adjust the length value for the following 6 tags --- 'moov', 'trak', 'mdia', 'minf', 'stbl' and 'stsz'.

#### Chunk Offset

We talked about this earlier. I had to change the value in the 'stco' tag whenever I made changes to the 'stsz' tag since that moved the starting position of the audio data and this tag stores that information.

#### Mocking up a Header

Using a copy of the header from one of Aldie's files and setting all of the previously mentioned elements to their correct values, I was able to create a 100 frame track that not only played correctly but I was also able to convert it into MP3 format. Until I had a 'good' header, I could not do this. I could only play the file in QuickTime. I sent the updated sample track to Aldie. I felt certain he'd be able to play it this time. It was a little after 8 in the evening and I was finally ready to write the program that would generate the frame information I needed to recover the GeekSpeak.

### --- The Light at the End of the Tunnel ---

I'd been working with the files so much that writing the program didn't take very long at all --- 2 or 3 hours max --- with some intermediate testing. The basic idea was to look for 5 zeros in a row. When I found that pattern, save the file position and continue searching until I reach the end of the file. After I have all the positions, step through each position and subtract it from the next position. Each of those values would be a frame size. If I could generate a file that stored all of this information, I could open it in the hex editor along with the GeekSpeak file and copy the entire file into the spot where the 'stsz' tag would be in the GeekSpeak file. After that, I would just need to set the elements described above to their correct values and I'd be able to play the file.

Here's the program in pseudo-code:

    Open the GeekSpeak file
    Position the file at the beginning of the first frame
    Repeat
       Read the next byte from the file until you've found 5 consecutive zeros
       Record the file position
    Until you've found the last frame
    Close the GeekSpeak file
    Repeat
       Subtract the current file position from the next file position
       Record the value as a frame size
    Until you've stepped through all the positions
    Open the FrameSize file
    Write the number of samples
    Repeat
       Write the current frame size
    Until you've stepped through all the frame sizes
    Close the FrameSize file

That's it! The first time I ran it, I had the search loop set to exit after 1000 samples were found. I went through the same process as before in creating the header --- copy from Aldie's track and paste it to the beginning of the GeekSpeak file, paste in the sample information from the generated file and make all of the necessary adjustments to the other parts of the header. This time I listened to the first minute and a half of audio! I sent the file to Aldie and posted to the thread. Matthew Monin (Octavian) was still up, monitoring the thread and providing encouragement. It was nearly midnight. After determining the number of samples in the GeekSpeak file, I ran the program one more time without the limit and did the final header creation with the complete frame information! It was about 1am in the morning but I fired up the file anyway and started listing to the 'nearly' lost episode of GeekSpeak. After hearing 20 minutes of good audio, I posted to the thread and finished listening to the track. Everything sounded good so I fired a message off to Aldie that the recovery was successful and posted a similar message to the thread.

### --- The Rest is History ---

The next morning, Aldie and I messaged back and forth until he had the file and was successfully listening to it. Later in the day, Aldie and I talked on the phone about the process of recovering the file and as you now know, Aldie and Derk recorded a new intro for the GeekSpeak that day and posted it to BGG later in the evening.

### --- Additional Information and the Source --- 

This post is so long I believe I've run up against a size limit and will post the source code as a reply to this thread.

**_If you've made it this far, I appreciate the time you've taken to read this rather extensive story of the GeekSpeak recovery. I hope you've enjoyed reading this as much as I enjoyed working on the the problem, writing about the process and being able to share it with the BGG community._**

**Regards, Jim**

_The following is the source code of the program I wrote to generate the table of audio frame sizes from the original audio track._

    import java.io.File;
    import java.io.FileInputStream;
    import java.io.FileOutputStream;
    import java.io.IOException;
    
    /*
     * Created on Jun 04, 2005
     */
    
    /**
     * @author Jim Ginn
     *
     * Controlling class to to generate a new sample table for Apple Lossless audio
     * files with no header information.
     *
     * This is a BRUTE FORCE way of doing it. But hey, it worked! :-)
     * I'm sure a knowledgeable perl programmer could do this with just a few lines
     *   of code
     * It's specific to the copy of the file I was using but those details could be
     *   abstracted without much problem to turn it into a general purpose utility
     *   for this sort of thing. Hopefully this sort of problem doesn't occur often
     *   enough to warrant that!
     */
    public class FixSampleTable {
    
       public FixSampleTable() {
          super();
       }
    
       public void process() {
          File audioFile = new File("C:TempGeekSpeakGS_copy_1.m4a");
          File sizeFile = new File("C:TempGeekSpeakGS_size.tmp");
          try {
             if (audioFile.exists()) {
                int curByte;
                long skipVal = 0;
                long position = 0;
                long[][] sizeArray = new long[50000][2];  // I initially set it to
                                                          // 50K but before I let it
                                                          // run through the entire file,
                                                          // I ran it once without saving
                                                          // the info to find out how many
                                                          // frames to expect -- the total
                                                          // count was about 34k so I was ok.
                long zCnt = 0;
                long startPos = 0;
                int totCount = 0;
                long tCnt = 0;
                long size = 0;
    
                System.out.println("Destination: " + audioFile.getAbsolutePath() + " found.");
                FileInputStream aIS = new FileInputStream(audioFile);
                skipVal = aIS.skip(978);   // cheatin' a little here. I knew the byte position
                                           // of the first sample frame.
                if (skipVal == 978) {      // Verifying the input stream landed where I wanted it to
                   position = skipVal;
                   while (position < 130660803) {   // cheatin' again. This is just a little past
                                                    // the beginning of the last sample but before
                                                    // the end. I didn't want the program to get
                                                    // into the empty part of the file
                      curByte = aIS.read();
                      if (curByte < 0) {   // if the byte read is negative, EOF -- better not
                                           // happen, not supposed to get that far
                         System.out.println("end of file found!");
                         break;
                      }
                      if (curByte == 0) {   // found a null byte
                         zCnt++;
                         if (zCnt == 1) {   // first found null since the last reset of the
                                            // count, save the position in the  file
                            startPos = position;
                         }
                         if (zCnt > 4) {    // found 5 nulls in a row, save the file position
                                            // at the start of the sample frame
                            sizeArray[totCount][0] = startPos;
                            totCount++;
                            zCnt = 0;
                         }
                      } else {   // non-null byte, reset the null counter
                         zCnt = 0;
                      }
                      position++;
    
    //                if (totCount < 1000) {   // for testing, drops out after 1000 samples are found
    //                   break;
    //                }
                   }
    
                   System.out.println(totCount);    // I needed this number to figure the duration
                                                    // -- (total frames / 10.7667) = duration in seconds,
                                                    // multiply the result by 44100 to get the duration
                                                    // in what Apple calls movie units
    
                   for (int i = 0; i < totCount - 1; i++) {   // Calculating the size in bytes of each sample
                      size = sizeArray[i + 1][0] - sizeArray[i][0];
                      sizeArray[i][1] = size;
                      System.out.println(size);
                   }
                   sizeArray[totCount - 1][1] = 3549;  // since I aborted the loop before the end of
                                                       // the last frame, I needed to add that value
                                                       // to the array. I'd calculated it in the hex
                                                       // editor already. It goes in totCount-1 position
                                                       // since Java arrays are 0 based
                   System.out.println(sizeArray[totCount - 1][0]);
    
                   aIS.close();
    
                   FileOutputStream sOS = new FileOutputStream(sizeFile, false);   // Writing the number of
                                                                                   // samples and their sizes
                                                                                   // out to a file
                   tCnt = (new Integer(totCount)).longValue();
                   sOS.write(convert(tCnt));   // the calls to convert change the long to
                                               // an array of bytes that are added to the file
                   for (int i = 0; i < totCount; i++) {
                      sOS.write(convert(sizeArray[i][1]));
                   }
                   sOS.close();
    
                }
    
             } else {
                System.out.println("Destination: " + audioFile.getAbsolutePath() + " is not ready.");
                System.out.println("Exiting...");
                System.exit(-1);
             }
    
          } catch (IOException e) {
             System.out.println("Error accessing the file: " + audioFile.getAbsolutePath());
             System.out.print(e.toString());
          }
       }
    
       // I found the following 3 methods because there wasn't a straight forward
       // Java API call to convert a number to an array of bytes
       /**
        * Convert a long into a byte array.
        */
       public static byte[] convert(long n) {
          n = (n ^ 0x8000000000000000L); // flip MSB because "long" is signed
          byte[] key = new byte[8];
          pack8(key, 0, n);
          byte[] key2 = new byte[4];
          for (int i = 0; i < 4; i++) {    // I added this loop because I only needed the last
                                           // 4 bytes in the array. A Java long is 8 bytes but
                                           // I needed 4 byte longs for the file
             key2[i] = key[i + 4];
          }
          return key2;
       }
    
       static final void pack4(byte[] data, int offs, int val) {
          data[offs++] = (byte) (val << 24);
          data[offs++] = (byte) (val << 16);
          data[offs++] = (byte) (val << 8);
          data[offs++] = (byte) val;
       }
    
       static final void pack8(byte[] data, int offs, long val) {
          pack4(data, 0, (int) (val << 32));
          pack4(data, 4, (int) val);
       }
    
       public static void main(String[] args) {
          new FixSampleTable().process();
       }
    }
