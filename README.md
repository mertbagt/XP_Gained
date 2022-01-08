# XP Gained

This is a MUSHclient plugin for the specific [MUD](https://en.wikipedia.org/wiki/MUD), SWmud

This plugin was a request by a fellow player to track xp gains over a one hour period.   It calculates and displays in a side window the ammount of xp gained from the most recent event that awarded xp (see Prompts below).  Also, when the timer is turned on (see Alias Commands), it will track the aggregate xp earned for the duration of the one hour timer.

## SWmud

[SWmud homepage](http://www.swmud.org/)

telnet://swmud.org:6666

## MUSHclient

[MUSHclient homepage](http://www.gammon.com.au/mushclient/mushclient.htm)

## Install

Find where your MUSHclient is installed.  Place XP_Gained.xml in your plugins folder at:

../Mushclient/worlds/plugins

Then log in to SWmud so that when you select File from the top menu options, the option Plugins appears:

![Plugin option location](https://github.com/mertbagt/XP_Gained/blob/main/Images/xpHour01.JPG)

click Add:

![Plugin menu](https://github.com/mertbagt/XP_Gained/blob/main/Images/xpHour02.JPG)

and select the file from your folder directory.

## Setup Part 1 - Files and Settings

XP_Gained works by sending info to a secondary window within MUSHclient.  The 'New World' we're setting up below will define this secondary window and allow the code to interact with it.

We set this up by first selecting File, New World:

![File menu -> New World](https://github.com/mertbagt/XP_Gained/blob/main/Images/xpHour1.JPG)

and then entering the following settings:

* World Name: xpHour

MUD address and port:
* TCP/IP add: 0.0.0.0
* Port: 4000

![World Settings](https://github.com/mertbagt/XP_Gained/blob/main/Images/xpHour2.JPG)

and hit OK.  

A prompt should pop up asking to 'Save changes to Untitled?' -> go ahead and click Yes

![Save Prompt](https://github.com/mertbagt/XP_Gained/blob/main/Images/xpHour3.JPG)

Shouldn't be strictly necessary but lines 185 and 270 put the focus back on the main window.  If your main world file is something other than SWmud.MCL, then find and replace your file name for SWmud.MCL on those lines with the name you're using.

example, change this:
```
local SWmudOpened = world.Open ("worlds\\\\SWmud.MCL") -- puts focus back on main window
```
to
```
local SWmudOpened = world.Open ("worlds\\\\YourFileName.MCL") -- puts focus back on main window
```
where you use your actual file name in place of YourFileName

## Setup Part 2 - Prompts

The way this plugin keeps track of your xp changes, is by reading your xp from your prompt and keeping track of when that value changes.

```
--=== Guide Entry on prompt (Player Command) ===--
Command: prompt
Syntax: <prompt [options]>
        <prompt no color [on/off]>
Usable by: Anyone

Sets the format of your prompt.

The options are: 

  Number  |  Info
----------|-----------
    1     |  hit points 
    2     |  hit points/max hit points 
    3     |  social points 
    4     |  social points/max social points 
    5     |  experience points 
    6     |  credits
    7     |  alignment 
    8     |  jedi alignment 
    9     |  alignment/jedi alignment
    10    |  bmode status 
    11    |  drugged status 
    12    |  wimpy hps 
    13    |  current ammo remaining (wielded weapon) 
    14    |  current ammo/max ammo (wielded weapon) 
    15    |  hidden status 
    16    |  status tags** 
    17    |  unread mail flag 
    18    |  shield hit points 
    19    |  vehicle armor
    20    |  vehicle armor/vehicle max armor

Example: prompt 2 5 9.
Example: prompt 2 18 5. (numbers can be in any order).

Typing <prompt clear> returns prompt back to default.
Typing <prompt no color [on/off]> toggles colour in prompt.
```
![Color Chart](https://github.com/mertbagt/XP_Gained/blob/main/Images/xpHour4.JPG)

The plugin is set up by default for either of two prompt configurations in XP_Gained.xml:

### Configuration 1

![Config 1](https://github.com/mertbagt/XP_Gained/blob/main/Images/prompt01.png)

```
prompt: 2 7 5 6 10 11 14 16

line 69: match="^\d+/\d+ (\-\d+|\d+) (\d+) \d+ .* &gt;"
```

### Configuration 2

![Config 1](https://github.com/mertbagt/XP_Gained/blob/main/Images/prompt02.png)

```
prompt 2 11 9 5 10

line 111: match="^\d+/\d+ .* (\-\d+|\d+)/(\-\d+|\d+) (\d+) .* &gt;"
```
If your prompt is different, you need to translate it into regex:

[Regex Syntax](https://www.gammon.com.au/scripts/doc.php?general=regexp)

and then replace either line 69 or 111 with:

match="&lt;your regex here&gt;"

## Alias Commands

xphelp - lists out plugin commands in the mud client.

xpstart - Starts a one hour timer.  This also resets the aggregated xp totals from any prior uses of the timer and begins collecting a new aggregation.

xpstop - Halts the timer.

## Graphical Examples

### Initial Screen

![Initial Screen](https://github.com/mertbagt/XP_Gained/blob/main/Images/initial.JPG)

This is an example of the initial screen on start up.  I have my window set to the side and normally have other side windows above and below, but obviously rearrange your windows to personal taste.

---

![Start Timer](https://github.com/mertbagt/XP_Gained/blob/main/Images/start.JPG)

After entering 'xpstart', the timer starts.  

'You have gained xp' updates when there's a new prompt.  So bear in mind it's possible to gain xp from more than one source between fresh prompts.

'Accumulated xp' is total xp gained from when the timer starts to either: 

1) this moment if the timer is still running

![In Action](https://github.com/mertbagt/XP_Gained/blob/main/Images/mediares.JPG)

or

2) the moment the timer stopped.



---