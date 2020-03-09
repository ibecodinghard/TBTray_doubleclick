TBTray - Native Win32 Thunderbird tray icon (with a persistant tray icon)
=========================================================================

After the x-th reincarnation of the MinimizeToTray add-on for Thunderbird broke
in Thunderbird 68, it seems like it becomes more and more difficult, if not
impossible, to solve the issue at hand - keeping Thunderbird minimized in the
notification area when closing or minimizing it - using Web Extensions.

I know that [BirdTray](https://github.com/gyunaev/birdtray) exists, and it's
even cross-platform. However, it tries to solve way more problems than I have
and uses Qt (no offense, I really like the framework), so it's not quite as
light-weight as I think a background process should be.

So I decided to fork a program a friend of mine wrote - [traktouch](https://github.com/dop3j0e/traktouch),
as it solves a very similar problem. I could have written it from scratch, but
this way I didn't have to write most of the boilerplate code.

Installation
------------

1. Download the [latest TBTray release](https://github.com/sagamusix/TBTray/releases).
2. Extract the archive anywhere you want, `%localappdata%\TBTray` would be a
   good place for instance.
   I would not recommend to put it in the same folder as Thunderbird, although
   it should be possible in theory.
3. Figure out whether you run a 32-bit or 64-bit version of Thunderbird.
   If you are not sure, check whether Thunderbird is installed in
   `Program Files` (64-bit on a 64-bit system, 32-bit on a 32-bit system) or
   `Program Files (x86)` (32-bit on a 64-bit system).
4. Launch the TBTray executable in the folder that **matches your Thunderbird
   bitness**, i.e. if you run a 32-bit Thunderbird, then run `TBTray.exe` in the
   32-bit folder of TBTray.
5. To automatically start TBTray on Windows startup, run `register.cmd` in the
   folder that **matches your Thunderbird bitness**, i.e. if you run a 32-bit
   Thunderbird, then run `register.cmd` in the 32-bit folder of TBTray. 
   If you ever decide to move the executable to a different location, you will
   need to run `register.cmd` again.
6. To completely uninstall, run `unregister.cmd` and delete the extracted files. 

How does it work?
-----------------

TBTray intercepts some window messages sent to Thunderbird, rejecting window
minimize and close events and instead hiding the window and creating a tray icon.

To do this, TBTray checks for the presence of the Thunderbird main window, and if
it finds the window, injects a library into the Thunderbird process to hook into
the message queue. TBTray keeps running in the background, in case you want to
restart Thunderbird at some point.

It doesn't work for me!
-----------------------

The most likely cause is that you have `mail.tabs.drawInTitlebar` set to `true`
(which is the default value) - setting it to `false` should solve that problem.

Note: If you want to get this fixed, consider submitting a pull request - I do
not have the time required to debug and fix a feature I am not using.

Halp, how do I quit Thunderbird?
--------------------------------

Through the File menu, or the context menu of the tray icon.

Is there any sort of configuration?
-----------------------------------

This program does not come with any options, because it is just supposed to fix
exactly the problem I had. Please fork the repository if you want the program to
behave differently. 
