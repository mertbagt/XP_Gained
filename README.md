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

Then add the plugin in MUSHclient with File, Plugin, Add and select the file

<insert pic>

XP_Gained works by sending info to a secondary window within MUSHclient.  We set this up by selecting File, New World

and then entering the following settings:

###World Name: xpHour

###TCP/IP add: 0.0.0.0

###Port: 4000

and hit save

sec 4 Prompts

prompt desc

## Alias Commands

xpstart - Starts a one hour timer.  This also resets the aggregated xp totals from any prior uses of the timer and begins collecting a new aggregation.

xpstop - Halts the timer.

Sec 6 todos:

   add help aliases
   
   add graphical examples