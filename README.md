                          CWirc X-Chat morse plugin
                          -------------------------
                                   2.0.0
                                   -----

                                   F8EJF
                Pierre-Philippe Coupard <pcoupard@skynet.be>
                                 20/05/2006



  CWirc is a plugin for the X-Chat IRC client to transmit raw morse code over
the internet using IRC servers as reflectors. The transmitted morse code can be
received in near real-time by other X-Chat clients with the CWirc plugin. CWirc
tries to emulate a standard amateur radio rig : it sends and receives morse
over virtual channels, and it can listen to multiple senders transmitting on
the same channel. Morse code is keyed locally using a straight or iambic key
connected to a serial port, or using the mouse buttons, and the sound is played
through the soundcard, or through an external sounder.

  Note that CWirc doesn't do any morse decoding : it simply transmits and
receives morse code timing events. A standard IRC user on the same IRC channel
you're transmitting morse on will only see coded lines when morse code is
transmitted. Only other CWirc users can receive what you send.



1 - Installing CWirc

  - Edit the Makefile to set the target OS (LINUX, FREEBSD or NETBSD) and the
    installation paths for the CWirc binaries.

  - Build the program by typing "make"

  - Install the plugin and its frontend program by typing "make install" as root



2 - Using CWirc

    CWirc is composed of two parts : a X-Chat plugin stub that intercept and
  sends morse frames as IRC text, and a frontend application that interacts
  with the user through a graphical interface. The frontend application is
  meant to be loaded by the plugin only, and cannot be used as a standalone
  program.

    To use CWirc, it is necessary that X-Chat loads the plugin part first.
  Normally, the CWirc plugin is installed in the X-Chat plugins directory as
  "cwirc.so" and is automatically loaded by X-Chat at startup. You can verify
  it's loaded properly by going in the "Windows" --> "Plugins and Scripts" menu
  in X-Chat and checking that CWirc appears in the list.
  
    When the "cwirc.so" file is loaded, it adds a new command to X-Chat, called
  "/CW" (you can do "/HELP CW" to verify this), and it also adds a "CWirc"
  button in the userlist buttons (if you don't see it, try enabling "Userlist
  button enabled" in the "Preferences -> User list" menu. The "/CW" command or
  the "CWirc" button enable and disable the plugin. Note that CWirc should
  have no incidence whatsoever on your normal IRC chatting on any channel, but
  it will always silently filter out incoming morse frames, whether it is
  enabled or not, so you can chat normally on a morse-dedicated IRC channel
  even with the plugin disabled.

    When enabling the plugin, the frontend application is called and the CWirc
  control panel appears outside of X-Chat. In the control panel, there are six
  tabs: the main tab for regular use, as well as the keyer settings,
  simulation, personal information, I/O configuration and "about" tabs.


  2.1 - The main tab

    2.1.1 - The S-meter / sidetone mode toggle

        This is an emulated classic needle signal meter. When signal strength
      simulation (see below) is used, it shows the strength of the incoming
      signal. When no simulation is used, it is simply decorative and move
      from S0 to S9+30 no matter what signal is sent or received.

        When the S-meter is clicked, CWirc switches to sidetone mode. When it's
      clicked again, CWirc goes back to normal mode. In sidetone mode, you can
      key without actually sending anything. This is useful when adjusting a
      key, or to train keying morse code, without bothering anybody on the
      channel.


    2.1.2 - The Channel setting

        CWirc has a concept of "CW channel", as opposed to IRC channel. They are
      not the same. Think of it as the frequency you'd dial on your radio rig.
      You can only send or receive morse on one CW channel. CWirc ignores morse
      sent to other CW channels. There are 4000 CW channels available (0->3999),
      therefore on any given IRC channel, there can be up to 4000 distinct QSOs
      going on.

        The top "PR x" selector selects one of 5 preset channels. The bottom
      channel setting sets the CW channel for that preset channel. You can
      therefore program up to 5 favorite CW channels : for example, you could
      set channel 1 at 1000 for the CQ channel, channel 2 at 1100 for the
      channel you usually QSY to, channel 3 at 912 to listen to the news
      channel ...


    2.1.3 - The RX pitch setting

        This setting changes the sound pitch of received morse beeps, allowing
      you to play your correspondant's signal at a frequency you're confortable
      with, or helping you discriminate between different operators
      transmitting on the same channel, if you "have an ear" for a particular
      audio frequency.

      NOTE: this setting does nothing if CWirc plays sounder clicks instead of
            beeps, or if the CW output is an external sounder only (see below).


    2.1.4 - The TX pitch setting

        This setting changes the sound pitch of your own signal played back to
      you locally. You can adjust it in sidetone mode (see above) to avoid
      sending garbage on the channel.

      NOTE: this setting does nothing if CWirc plays sounder clicks instead of
            beeps, or if the CW output is an external sounder only (see below).


    2.1.5 - The Squelch setting

        If you use QRN simulation (see below), fake radio static is played
      continuously and it quickly gets very tiring. Like on a real radio, to
      cut off the background noise when it's not useful (when you're not
      actually transmitting or receiving anything), set the squelch high enough
      to stop the background noise, and low enough to re-enable the sound when
      a signal comes.

        Note that if you use signal strength and/or sporadic-E simulation (see
      below), using the squelch can make you miss weak signals.


    2.1.6 - The AF gain setting

        This changes the volume of beeps or sounder clicks played throught the
      sound card. Note that your computer's actual mixer device isn't used to
      set the volume : CWirc simply generates lower amplitude sound signals
      internally.


    2.1.7 - The Key setting

        This setting tells CWirc to read mouse clicks on the mouse keying zone,
      or a real morse key connected to a serial port (see below), as a straight
      key, or as paddles using the internal automatic keyer. The icon displayed
      in the mouse keying zone changes to a straight key or an iambic key
      accordingly.


    2.1.8 - The Iambic keyer speed setting

        If you set "Key" to "iambic", you can set the automatic keyer's speed
      in words per minutes. The keyer will function in that speed according to
      the settings in the "Keyer settings" tab (see below).


    2.1.9 - The mouse keying zone

        If you enabled the mouse as CW input (see below), you can key morse code
      with the mouse by leaving the pointer in the morse key icon and using the
      buttons as key or paddles. If you set "Key" to "iambic", the left and
      right mouse buttons act as paddles. If you set "Key" to "straight", either
      mouse button emulates the key.


    2.1.10 - The automatic morse decoder

        At the bottom of the control panel, there is a line with morse
      characters decoded from the morse signal currently received.

        The morse decoder that generates those characters simulates a real
      automatic decoder connected to the audio output of a real radio rig.
      Therefore, it will work only if only one person is transmitting at a
      time. If several people send morse together on the same CW channel, like
      in a pile-up, or if you transmit over someone else's signal, the decoder
      will get confused and generate garbage. If you really need to decode a
      particular sender in a pile-up with the decoder, you could use the IRC
      command "/IGNORE" to silence all the other senders.

        If you use signal strength and/or sporadic-E simulation, the decoder
      will not work if the incoming signal is too weak or fluctuating, or will
      not decode properly. Similarly, if a strong signal and a weak signal are
      received at the same time, only the strong signal will be decoded. If
      more than one strong signal arrive at the same time, the decoder will get
      confused.

        Also, the decoder needs to "hear" a little signal before synchronizing
      correctly with a sender, or with you. Therefore, the first character(s)
      will be garbled as the decoder guesses the timing of the morse code.
      It will resync similarly if the sender suddenly changes his/her keying
      speed dramatically, or if you yourself don't send at a speed close to
      that of your correspondant. Finally, although the decoder makes
      allowances for slightly incorrect morse timings and drifting keying
      speed, it still needs to receive somewhat clean morse code to work well.
      You're better off using your ears to copy a bad sender, or a sender using
      a very atypical dit weighing.

        The decoder is also useful in sidetone mode (see above) to train keying
      clean morse with proper timing.

      NOTE: If you conduct a QSO in a code that's not modern morse code or DOT
            code, like in genuine American morse code, the decoder will
            produce garbage.


    2.1.11 - The automatic morse decoder's speed indicator / reset button

        The received morse speed indicator at the right of the decoded text, in
      words per minute, is an measure of your correspondant's keying speed.
      It is measured from the raw received or sent signal, therefore it can be
      quite approximative. If the decoder gets confused with two superimposed
      signals, or a signal with fluctuating strength, the speed indicator
      becomes wild and means nothing. If the morse code doesn't use a dit
      weighing of 50%, the speed indicator will also be skewed.

        This indicator also doubles as a morse decoder reset button. Pressing
      it will erase the current decoded characters buffer and will reset the
      automatic decoder.


    2.1.12 - The automatic morse decoder's language selector

        At the right of the morse decoder speed indicator, you can select which
      language or code set you would like the decoder to use to decode incoming
      signals. At the moment, English (international), French, Russian,
      Japanese (katakana) morse code, and historic DOT code (which isn't morse)
      are supported.

        In order to view decoded characters in a language other than English,
      (english morse or DOT) you need to have a real Unicode/ISO-10646 font set
      installed on your system. If you are interested in using a non-English
      morse code set, chances are your machine is already setup correctly.
      Otherwise, a good start if you want to configure your fonts correctly
      under X is to read the "XFree86 Font De-uglification HOWTO" document
      available at :

      http://www.tldp.org/HOWTO/FDU/index.html

        If you find the decoder distracting, or if you can't resist looking at
      it when training to copy, simply select "No decoder" to disable it
      entirely.


  2.2 - The Keyer settings tab

      This tab lets you adjust the iambic keyer to your liking. Keyer features
    and settings are a very personal issue : iambic keyers from different
    manufacturers (or home-made keyers), and sometimes different models from
    the same manufacturer, have slightly different responses to an operator's
    input, and most people tend to prefer the features displayed by whichever
    keyer they first learned iambic keying with. The CWirc keyer can be
    adjusted to match almost any existing iambic keyer.


    2.2.1 - The iambic mode selector

        Set the iambic mode you would like the CWirc keyer to use. The iambic
      mode (A or B) only changes the behaviour of the keyer when both paddles
      are released after having been squeezed together (i.e. iambic keying) :
      in mode-A, when both paddles are released in the middle of an element
      being sent (dit or dah), the element is completed, then the keyer stops.
      In mode-B, the element is completed, then the keyer automatically sends
      an extra opposing element, then stops.

        If your Cs consistently come out as Ks, you're probably using mode-A
      when you really want mode-B. Conversely, if your Ks consistently come out
      as Cs, you probably want to use mode-A.


    2.2.2 - The dit memory and dah memory

        If you enable the dit memory, when the keyer sees the dit paddle being
      hit, however briefly, during the sending of a dah, it "remembers" it and
      sends the dit at the next possible occasion. Similarly, the dah memory
      enables the automatic insertion of a dah by touching the dah paddle while
      a dit is being sent out.

        Typically, dit/dah memory is used to make Ns and As by tapping the
      two paddles quickly one after the other (but not squeezing, that would
      make the keyer go into iambic mode). It's also very useful to make
      letters such as Y, Q, L or F by sending a stream of dahs or dits, and
      inserting a dit or a dah by tapping the opposing paddle at the right
      moment.


    2.2.3 - The mid-element mode-B mode

        Most mode-B keyers automatically insert an opposing element when
      releasing both paddles anytime during the element currently being sent,
      in iambic mode. Some mode-B keyers however seem to make a distinction
      between the case where both paddles are released before the middle of the
      element currently being sent, and the case where they're released after.
      In the former case, those keyers don't send an opposing element, while
      they do in the latter. Those keyers seem to be a minority though.

        If your As consistently come out as Rs and your Us as Fs, but your
      keying is otherwise fine in mode-B, you might want to try this option.


    2.2.4 - The auto character spacing

        When this option is enabled, the keyer forces you to wait the correct
      time between letters. Try using this if you consistently run letters
      together.


    2.2.5 - The auto word spacing

        In addition to the auto character spacing, you can use this option to
      force the keyer to make you wait the correct time between words and help
      you format your transmission perfectly. Try using this if you consistently
      fail to leave enough time between words. Be aware however that this option
      requires an otherwise good keying to be used efficiently, as it will force
      you to wait a full inter-word pause each time you hesistate on a letter.


    2.2.6 - The "invert paddles" option

        If you're left handed, or if you're used to key using the left paddle
      as dah paddle and the right paddle as dit paddle, enable this option.


    2.2.7 - The dit weight setting

        Back when radios often showed a certain lag between the moment a key
      was depressed and the moment it would start transmitting, it was often
      useful to artificially increase the length of the elements sent by the
      keyer, so that they would end up being sent on the air with the proper
      timing by the radio. Today, most transceivers don't need this trick to
      send properly formatted CW, but some operators have kept their
      non-standard dit weight because it sounds better, or to "personalize"
      their signal. The CWirc keyer allows you to change the dit weight as
      well, although it's completely useless to do CW over the net.

        The value corresponding to the standard morse code timing is 50%.

      NOTE: don't overdo it : if you set the dit weight too far off 50%, most
            people won't be comfortable copying you, and some might even not
            copy you at all.


  2.3 - The Simulation tab

      This tab lets you set CWirc to experience an approximation of what a real
    radio sounds like, to train copying signals that are less than perfect and
    a little less "artificial" and computer-generated than with the basic
    settings.


    2.3.1 - the QRN simulation box

        Check "simulate QRN" to add noise and static to incoming signals. Use
      the "QRN level" slider to set the level of noise you want. The level
      of QRN you've chosen registers on the S-meter in the main tab.


    2.3.2 - The Propagation simulation box

        Check "simulate signal strength for signals with grid squares" to make
      CWirc generate a fake signal strength for incoming signals that have been
      sent with a grid square location as part of the signal.

        For this to work, you have to have your own grid square set in the
      Personal info tab (see below) : the way CWirc knows what signal strength
      to give to an incoming signal is by calculating the distance between you
      and the person who emits the signal, hence it must know your location as
      well as the sender's. It's up to the sender to disclose his/her own grid
      square : if he/she doesn't want to disclose it, his/her signal will be
      given a default signal strength that you can set with the bottom slider
      marked "default signal strength for signals without grid squares".

        In addition to the basic signal strength simulation, you can add
      sporadic-E simulation by checking "simulate sporadic-E for weak signals".
      Real sporadic-E is a type of ionospheric E-layer reflection caused by
      small patches of unusually dense ionization in the atmosphere that makes
      many long distance contacts possible on VHF. Such reflected signals tends
      to come and go quickly as the patches of ionization move up in the
      atmosphere, making those long contacts challenging to establish and
      maintain. With sporadic-E simulation enabled, CWirc makes the strength of
      all weak signals it receives (approximately under S3) fluctuate as if
      they came from a sporadic-E reflection.


  2.4 - The Personal info tab

    2.4.1 - The Callsign setting

        If you are a ham, you can set your callsign for other users to see in
      your morse messages, or when they query your information with the
      /CTCP CWIRC command (see below).


    2.4.2 - The Grid square setting

        Set the grid square corresponding to your present physical location here
      if you want to be able to use signal strength and sporadic-E simulation.
      If you don't know your grid square location, you can find it on the
      following webpage, with the grid map, or if you know your latitude and
      longitude :

      http://www4.plala.or.jp/nomrax/GL/index.html

        CWirc accepts grid squares in the basic 4-character format ("AB12"), or
      the more accurate 6-character ("AB12CD") format.


    2.4.3 - The "send callsign with CW" button

        If you select this, CWirc will send your callsign along with your CW
      signal, and other CWirc users will be able to see it when they receive
      your signal. If you choose to broadcast your callsign, it will be sent
      in scrambled form in the IRC message, so only other CWirc users will be
      able to see it.

        This is useful if you want to keep your normal anonymous IRC nick for
      casual IRC chatting, but you want to go by your ham callsign with other
      CWirc users at the same time.

    
    2.4.4 - The "send grid square with CW" button

        If you select this, your grid square location will be sent along with
      your CW signal, allowing remote CWirc users to use signal strength
      simulation options with your signal. If you choose to broadcast your
      grid square, it will be sent in scrambled form in the IRC message. If you
      you want to stay vague about where you are, enter your grid square in
      4-character format (they define an area that measures approximately
      70 miles x 100 miles in the continental US).

    
    2.4.5 - The CTCP settings

        CWirc can reply to a custom CTCP query (CTCP CWIRC) to report what
      version you are using, what channel you are currently on, what your
      callsign is or what your grid square location is.

        If you don't want to disclose any of these details, un-check the "reply
      to CTCP CWIRC queries" setting. If you check it, it'll give anybody who
      types "/CTCP <your nick> CWIRC" the version of your CWirc client.

        Additionally, you can also check "send callsign in CTCP reply", "send
      grid square in CTCP reply, or "send current channel in CTCP reply" to
      give those details along with the CWirc version.


  2.5 - The I/O configuration tab

      This tab allows you to set the parameters for the CW input and output
    devices, and the buffering policy. The settings in the I/O configuration
    tab are only effective after your click on the "Change/Save" button. If a
    parameter is erroneous, an error popup window will inform you of the reason.


    2.5.1 - The CW input setting

        To key morse code, you can use the mouse by clicking on the mouse keying
      zone (see above), a real morse key connected to a serial port (see below)
      or both. If you choose "real key" or "both", the "Serial device" setting
      needs to be set.


    2.5.2 - The CW output setting

        To play morse code, CWirc can use a soundcard, an external sounder or CW
      oscillator connected to a serial port (see below), or both. If you choose
      "soundcard" or "both", the "Sound device" setting needs to be set. If you
      choose "sounder", the "Serial device" setting needs to be set.

      NOTE: if you use both a real morse key and a sounder, they will share the
            same serial port.

      NOTE: if you use a sounder, you shouldn't use signal strength simulation
            as well. The reason is that weak signals, below a certain threshold,
            will simply not be played on the sounder.

      NOTE: the "sounder" option (external sounder as sole CW output) isn't
            available under FreeBSD or NetBSD, as these OSes don't provide a
            proper /dev/rtc implementation, therefore CWirc always needs the
            soundcard to pace itself.


    2.5.3 - The CW sound setting

        If "CW output" is set to "soundcard" or "both", you can choose to play
      incoming and outgoing morse code as regular beeps, or as sounder clicks.
      Most "modern" hams should choose beeps here. Sounder clicks are really
      a feature for those who are interested in historical landline telegraphy,
      who want to experience the sound of yesteryear's telegraphy as heard in
      railway telegraph stations, or want to try out the original American
      morse code (which is different from the international morse code
      everybody knows today).

        Note that the sounder clicks played by CWirc come from an actual Vail
      sounder, and the timings of the sounder's arm going up and down are
      accurately reproduced.

    
    2.5.4 - The Key debounce setting

        When using a real morse key connected to a serial port, its contact(s)
      will read at regular interval to determine its/their states. If you get
      spurrious dits or dahs while keying, it's possible that your key
      contact(s) "bounce" when they make or break the electrical contact.
      Contact "bouncing" is a common electrical phenomenon that occurs with
      nearly all electrical switches. To alleviate the problem, increase the
      value of "Key debounce" until the problem disappears.

      NOTE: the lower the "Key debounce" value, the better, especially if you're
            a fast keyer. If you feel your key is sluggish and/or misses
            elements when you key fast, try lowering the value.


    2.5.5 - The Recv buffering setting

        This tells CWirc how long (in milliseconds) it should pre-buffer
      incoming morse from the IRC server. On IRC servers that are reasonably
      responsive, 1000 ms (1 s) is usually enough. If you're connected to an
      IRC server with a lot of lag, try increasing the buffering value. If
      you're connected to a local IRC server, of if you receive morse from an
      operator in a DCC CHAT connection (see below), you can lower the value.

        The more you increase the buffering value, the less your CWirc client
      will be subject to buffer underruns, but the more the receive latency will
      increase.


    2.5.6 - Sound device

        If "CW output" is set to "soundcard" or "both", this tells CWirc which
      sound device to use to access the soundcard. Usually it's "/dev/dsp" under
      Linux, "/dev/dsp0.0" under FreeBSD, or "/dev/audio0" under NetBSD, if you
      only have one soundcard.

      NOTE: if you want to use the aRts daemon with CWirc, you can with
            the artsdsp wrapper and some tinkering, at the expense of sound
            latency:

            - In the KDE sound system preferences, enable the sound system if
              not already enabled of course, enable "Run with the highest
              possible priority (realtime priority)" and set the sound buffer
              slider to the lowest possible level.

            - As root, rename the "cwirc_frontend" binary (usually installed in
              /usr/bin or /usr/local/bin) to "cwirc_frontend.REAL"

            - As root, edit a new shell script called "cwirc_frontend" where
              the real frontend binary was, with the following lines in it:

                #!/bin/sh
                artsdsp cwirc_frontend.REAL $*

              and make it executable by invoking

                chmod +x cwirc_frontend

            - Restart CWirc and ensure the sound device is set to "/dev/dsp".
              The sound should then be redirected to the aRts sound daemon.


    2.5.7 - Serial device

        If "CW input" is set to "real key" or "both", or "CW output" is set to
      "sounder" or "both", this tells CWirc which serial device the real morse
      key and/or the sounder are connected to. Use /dev/ttyS0 for COM1,
      /dev/ttyS1 for COM2 ... under Linux, or /dev/cuaa0 for COM1, /dev/cuaa1
      for COM2 ... under FreeBSD, or /dev/tty00 for COM1, /dev/tty01 for
      COM2 ... under NetBSD.


  2.6 - Conducting QSOs in an IRC channel

      When CWirc is configured to your liking, try connecting to an IRC server
    and joining a channel bearing morse traffic. Don't forget to set the channel
    to the same as used by other parties in the channel (typically 1000 is the
    general CQ channel).

      The morse you send will be emitted on the IRC channel as encoded lines
    every 2 seconds. Similarly, your CWirc client will receive incoming morse
    sent in encoded lines. Note that morse received on channels other than the
    one you are currently ignored will be silently ignored.

    IMPORTANT: CWirc uses a protocol that looks very much like high-speed
               garbage to non-CWirc users. Please be considerate and do NOT use
               CWirc on general IRC channels (i.e. not dedicated to morse
               traffic) unless you know the chatters and you ask them first.


  2.7 - Conducting QSOs outside of the IRC channel

      It is possible that you want to discuss things outside of the IRC channel,
    so not everybody who happens to be tuned to your CW channel can hear what
    you say. It's possible to /QUERY the other person and send him/her morse in
    private, as you would to send normal IRC private messages. You still need
    to be on the same CW channel though.

      You can also DCC CHAT with the other party : in that case, the connection
    between the other party and you is direct, bypassing the IRC server, which
    has the big advantage of reducing the lag between the 2 CWirc clients, and
    ensuring you won't get kicked out of the IRC channel for flooding.


  2.8 - IRC channel locking

      Normally, CWirc receives and sends morse from whatever channel you have
    currently in focus. If you just do morse, that's usually good enough.
    However, it's possible that you might want to send/receive morse to/from one
    IRC channel while doing something else in another. Typically, the situation
    is when you're sitting on a channel waiting for a CQ and you want to chat
    with friends on another IRC channel in the meantime.

      You can instruct CWirc to not follow the channel currently in focus. To
    that, put the IRC channel you want to use in morse in focus and issue the
    "/CWLOCK" command : CWirc then tells you that it's locked on that IRC
    channel. You're then free to do whatever you want on other channels and
    CWirc will stay on the channel you locked it on. If you want to lock CWirc
    onto another channel, simply put the new channel in focus and use the
    "/CWLOCK" command again. If you want to revert to the default mode of
    following the channel in focus, issue the "/CWUNLOCK" command.

      Note that you can lock and unlock CWirc on private chat and DCC CHAT
    windows as well.


  2.9 - Notes on using simulation

      If you use signal strength simulation, and especially if you add
    sporadic-E simulation on top of it, it is entirely possible to not hear an
    incoming signal despite the fact that CWirc reports receiving it, if it is
    too weak (typically the remote sender is too far away physically) or if it
    is too attenuated by the sporadic-E simulation.

      Also, while it is possible, it's a bad idea to use signal strength or
    sporadic-E simulation with a sounder : if the signal is too weak, the sound
    of the sounder will simply be cut-off, because it's a device that is either
    on or off.

      Finally, while possible too, note that using sounder clicks with QRN,
    signal strength or sporadic-E simulation makes no sense : sounders were
    used for land-line telegraphy, and therefore never generated QRN or weak
    signal.



3 - Connecting a real morse key

    Keying morse with a mouse is okay when nothing else is available, but it's
  not ideal. If you have a real morse key, you can use it to key morse in CWirc
  by connecting it to your computer with a simple serial cable :


  3.1 - Using a straight key

    Assuming your serial port uses a DB9 connector, the wiring is :

      DB9 pin number                                Key

                                                   =====
      6 (DSR line) --------------------+-------------|

      4 (DTR line) --------------------+-------------O

    
    Once the key is connected, configure CWirc by setting "CW input" to "real
    key" or "both" and "Key" to "straight".


  3.2 - Using an iambic key

    Assuming your serial port uses a DB9 connector, the wiring is :

      DB9 pin number                                Key

      8 (CTS line) --------------------+--------O--===== Right paddle

      4 (DTR line) --------------------+--------|        Common

      6 (DSR line) --------------------+--------O--===== Left paddle


    Once the key is connected, configure CWirc by setting "CW input" to "real
    key" or "both" and "Key" to "iambic", then configure "Iambic keyer" to your
    liking.



4 - Connecting an external sounder

    A sounder, a CW oscillator, a lamp, or even the PTT of your radio rig can
  be controlled by CWirc through the RTS line on a serial port. That line can
  be made to change state following the received and sent morse code, in
  conjunction with, or in lieu of the soundcard. This is useful for various
  kinds of users :

  - People whose soundcard can't be opened by more than one process at a time,
    and who want to listen to something while doing CW at the same time

  - People who want to experience the original land telegraphy sound (i.e. the
    sounder), that wasn't beeps but clicking noises

  - Hams who want to retransmit an internet CW QSO on the air

  - Users with hearing problems who need a visual indication of dits and dahs

    Of course, ready-made devices that can be driven by a RS232 RTS line aren't
  usually available in retail stores, so you'll probably have to dust off your
  soldering iron. The easiest is probably to make a simple RTS-controlled relay
  box, with an optocoupler to protect your serial port, then use the relay to
  inject power in a commercially available training CW oscillator, a buzzer, a
  light bulb or a sounder coil.

    Assuming your serial port uses a DB9 connector, the wiring to connect your
  custom-made sounder (or whatever other device) is :

    DB9 pin number

    7 (RTS line) --------------------+-------- Sounder output

    5 (GND line) --------------------+-------- Sounder ground


    Once the key is connected, configure CWirc by setting "CW output" to
  "sounder" or "both".

    With a sounder device, if several operators send morse on the same CW
  channel, it's not possible to discriminate between them by the received
  tones, since the only information available with a single data line is the
  presence or absence of signal.

  NOTE: if you set "CW output" to "sounder" (available under Linux only), CWirc
        will not be able to use the soundcard to pace itself. As a result, it
        will try to use your computer's real-time clock instead, through the
        /dev/rtc interface. There are however several things you need to do to
        allow a user program like CWirc to use /dev/rtc :

        - Enable "Enhanced Real Time Clock Support" in the Linux kernel, either
          as a module or compiled in

        - Set permissions to open the /dev/rtc device file read-only as a normal
          user

        - Allow CWirc to ask /dev/rtc to generate 1024 interrupts per second by
          typing the following command in a console, as root :

            echo 1024 > /proc/sys/dev/rtc/max-user-freq

          (The easiest it to put that line in a bootup script, so it's always
          set up correctly each time you restart the machine.)

        If you use the soundcard output as well as the sounder, there is no
        need to do any of the above, as CWirc will automatically use the
        soundcard to synchronize itself whenever possible.



5 - CWirc extensions

    As of version 1.7.0, CWirc supports external extension programs. A simple
  interface allows a program specially designed or modified to work with CWirc
  to receive audio synchronously as you hear it, and key as you'd key.

    If you have extension programs installed, an extra tab will appear in CWirc
  so that you can start it. Note that only one extension can be running at
  any given time.



6 - Note on CWirc and CWCom interfacings

    The interfacing of external devices to a serial port used by CWirc is
  strictly identical to the one used by CWCom for Windows, by MRX Software
  (http://www.mrx.com.au/d_cwcom.htm). Consequently, if you already use CWCom
  in Windows with a key and/or a sounder connected to a serial port, you won't
  need to modify anything to your hardware setup to use CWirc in Unix.



7 - Solving the scratchy sound problem

    On some machines with low-end or integrated sound devices (typically SiS,
  i8x0 or VIA sound devices), CWirc may start to sound very nasty when the
  system gets loaded, even only a little. If you experience sound cuts and
  "scratchy" noises, try to set the CWirc frontend executable (usually
  /usr/bin/cwirc_frontend or /usr/local/bin/cwirc_frontend) suid root, by
  issuing the following commands as root:

    chown root <CWirc frontend install path>/cwirc_frontend
    chmod u+s <CWirc frontend install path>/cwirc_frontend

  then restarting CWirc. This should clear, or at least improve the bad sound
  problem.

    When CWirc is run suid root, it asks the system to give its I/O routine a
  better execution priority than most processes in the system, thereby reducing
  or suppressing sound buffer underruns that are the cause of "scratchy"
  noises. CWirc can only instruct the system to give it this better treatment
  if it has root permissions, hence the need to set the CWirc frontend
  executable file suid root.

    CWirc is normally installed as a regular, non-suid binary by default,
  because although the program drops its root privileges as soon as it has
  changed its own system priority, almost immediately at the beginning of the
  program, and therefore should be quite safe, suid programs are usually viewed
  as a security risk, and most users will be able to run CWirc fine without the
  better priority anyway. This is the reason why it is left to you to set the
  suid attribute on the CWirc frontend executable manually if you need it.

    If the problem seems to persist, you may want to check that CWirc
  effectively did manage to reprioritize its I/O routine with the root
  privilege. To do this, invoke:

    ps x | grep cwirc_frontend

  while CWirc is running, and check that one of the two "cwirc_frontend"
  processes has "<" marked next to it, meaning that it's a high-priority
  task.
  


8 - FAQ

  Q: When setting "CW output" to "sounder", when I try to enable the plugin, it
     says "Error : cannot open /dev/rtc." but I'm sure my kernel has real-time
     clock support, rtc support is setup properly and I have proper permissions
     to access /dev/rtc.

  A: Programs that use /dev/rtc, like VMware or mplayer, have exclusive control
     over the real-time clock and need to be stopped first before using CWirc.
     Try to do "lsof /dev/rtc" to check what process is currently using
     /dev/rtc.

  Q: When setting "CW output" to "sounder", when I try to enable the plugin, it
     says "cannot set /dev/rtc to generate 1024 interrupts per second."

  A: By default, the Linux kernel won't let non-root programs instruct the
     real-time clock to generate more than 64 interrupts per second. CWirc
     needs 1024, so it's necessary that you tell the kernel to lift that safety
     restriction. For details, see the section above on using a sounder. If you
     can't change the kernel setting, because you don't have root access to the
     box for example, you'll have to use the soundcard as well.

  Q: When I try to enable CWirc, X-Chat tells me "CWirc : error : cannot
     execute "cwirc_frontend" ".

  A: cwirc_frontend is the executable for the CWirc frontend. It needs to be
     in your search PATH for the plugin to be able to start it.

  Q: When I key, after a short while, the IRC server kicks me out

  A: A lot of data is transmitted to the IRC server as fast as possible when you
     key. Most IRC servers let you get away with one line sent every 2 seconds,
     but some servers may interpret that as flooding and kick you out. Also, if
     you're a fast keyer, the lines transmitted to the IRC server can get quite
     long and trip the server's flood detection too. Try using a more
     permissive server, keying less fast, or doing private QSOs in DCC CHAT.

  Q: The plugin starts fine but nothing happens when I key with my real key

  A: Make sure the serial device file you've set is the one you connected your
     key to. The plugin can't detect your morse key.

  Q: When someone transmits, the CW flow is chopped every now and then

  A: This is most likely due to lag between the person's machine and the IRC
     server, or between your machine and the IRC server. Try to increase the
     receive buffering, or try to connect to a more responsive, less busy
     server, or initiate a DCC CHAT with the other party to communicate
     directly without the IRC server.

  Q: I've increased the buffering and the sounds still cuts, or the sound cuts
     when I run many things on my system

  A: See the "Solving the scratchy sound problem" section above

  Q: A friend has CWirc installed, I can see some coded frames coming from him
     and he can see some of mine, and none of us can hear anything, or only
     partially.

  A: The frame format changed at version 0.3.0, at version 0.8.0 and again at
     version 1.7.0. Frames generated by previous versions of CWirc will be
     dismissed as normal text. Please upgrade to the latest version.

  Q: I've joined my favorite channel on my favorite IRC server, I've sent
     CQ to see if I could get a contact with other CWirc users, and I've been
     kicked off the channel / banned / insulted as a result. What's going on ?

  A: When the CWirc plugin is loaded, it filters out incoming and outgoing CW
     frames and simply displays "sending" or "receiving" (or nothing at all) to
     spare you of having to watch encoded garbage. However, non-CWirc users
     will see the garbage and will quickly interpret it as a very unfunny trick
     from you, and classify you as a nuisance. Please ask if there are any
     CWirc users on the channel in plain text first, then either /QUERY other
     users in private, DCC CHAT to them, or create another IRC channel, so
     regular IRC users aren't bothered.

  Q: Why isn't the "sounder" option available under FreeBSD or NetBSD, in the
     "CW output" setting ?

  A: Normally, CWirc uses the soundcard to pace itself, i.e. it takes advantage
     of the fact that it takes a very precise amount of time to play a chunk of
     audio. With the "sounder" option, the soundcard isn't used at all.
     Therefore, CWirc has to use another precise timing source. Under Linux,
     it's possible to use the /dev/rtc interface for this. Under FreeBSD or
     NetBSD, there is no such interface natively, and the rtc kernel module
     available as Linux emulation isn't complete and lacks some of the
     functions used by CWirc. As a result, the "sounder" option is simply
     disabled under these OSes.

  Q: What is this DOT thing in the decoder language selection ?

  A: DOT code isn't a language but an old telegraph code directly derived from
     a flag code. Most notably, it was used by the U.S. military during the
     American Civil War. DOT code is not morse code, and isn't in use anymore
     apart during living history events and reenactments. If you're interested
     in historical landline telegraphy and would like to setup a station to
     simulate a telegraph station of that period, you can use the sounder clicks
     simulator and switch the decoder to DOT code to help you copy this old
     code.

  Q: I key morse, but apparently nobody hears me

  A: Check that you're not in sidetone mode. In sidetone mode, CWirc works
     exactly like in normal mode, only it never transmits anything



9 - Contributions

    If you feel like improving the plugin, please send me your changes, I'll
  glady incorporate them. Also, if you run have an IRC server and would like to
  dedicate a channel to morse users, please let me know so I can post the
  address of your server for others to use. I personally use irc.freenode.net,
  which is a nice permissive IRC server.



10 - Credits

    Many thanks to the following people :

  - Patrick Maille <patrick@arcturusnetworks.com> for doing a lot of testing on
    different Linux flavors, and for his suggestions.

  - Juha Nygard <juha.nygard1@netikka.fi> for providing FreeBSD specific help
    and a shell account on his FreeBSD box.

  - Bill Meahan <wmeahan@wa8tzg.org> for providing NetBSD patches, testing and
    debugging help.

  - Ted Wagner <trwagner1@yahoo.com> & David T. Bock <bock@marketcommander.com>
    for their help to add DOT code in the automatic decoder.

  - Mac WA4CAW, for his time, help, and documentation, to figure out the iambic
    keyer timings.

  - Ted WA0EIR, for his help and obscure-bug-finding abilities.

  - Joop Stakenborg PG4I <pa3aba@debian.org> for maintaining the Debian package
    and for the bugfixes.



11 - Legalese

    This software is released under the terms of the General Public License. See
  the "COPYING" file for details.

  Oh, and yes, I forgot :

  DISCLAIMER :

    I am not responsible for any damage caused by this software, whether it's on
  your computer, your morse key, or if it wipes out your hard-drive, or if it
  sets off a nuclear bomb, etc ...
# cwirc-hexchat
This is a fork of the cwirc Xchat2 plugin for Hexchat.
