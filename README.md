
### Windows Setup Guide

The following tools are required:
* Windows 10
-# (Not technically necessary, but Linux hasn't been tested yet.)
* [Java version 25](https://download.oracle.com/java/25/latest/jdk-25_windows-x64_bin.exe)
-# (though, versions 8 and up should all work)
* [Python 3](https://www.python.org/downloads/latest/python3.9/)
-# (any version of Python 3.x should work) 
* [Tailscale](https://tailscale.com/download)
* [Apache version 2.2 (no link yet)](https://google.com)

0. Download Java, Python, and Apache if you haven't already.

1. Download this repository.

2. Extract `near-exclave.zip`.

3. Move the resulting folder into your Documents directory.

4. Install and set up [Tailscale](https://tailscale.com/download) if you don't already have it.
* Once Tailscale is set up, go to the `Machines` tab and edit the machine you want to use. Rename it to something like "neartest". You'll need to remember your machine's name for a later step.
* Go to the `DNS` tab and use the random name generator to get a better name for your Tailnet. You'll need to remember your Tailnet's name for a later step.

4.5. Close off your Tailnet to everyone but yourself.
* This step is not technically necessary, but is *heavily* recommended for security's sake. With a version of Apache this old, you'll be pwn'ed by modern bots if your connection is open to the web.
-# (This guide will be updated once I can test a more recent version of Apache. Until then, it isn't recommended to open your server up to the wider web.)
* Go to the `Access controls` tab. Edit the Tailnet you will use. Change the Source to only your own email, and the Destination to `autogroup:self`. Click `Save grant`.

5. Authenticate your server with your Tailnet.
* Go to the `Settings` tab. Go to `Keys` (you'll need to scroll down in the left area), then `Generate auth key...`, then check the "Use this key to authenticate more than one device" box, and then finally `Generate key`. Jot the key down somewhere (it won't show the full key to you again), then put the key in `C:\Users\[yourusernamehere]\near-exclave\DuskFiles\DuskCheerpj\wwwClient\client.html`, where there will be a space for it.

6. Edit the "prefs" file (`C:\Users\[yourusernamehere]\near-exclave\DuskFiles\DuskCheerpj\conf\prefs`); change `"dusk.comet-richter.ts.net"` to `"[yourmachine].[yourTailnet].ts.net"`.
-# If it prompts you to pick an app to open it, simply pick the text editor of your choice, such as Notepad, Notepad++, or Vim.

7. Start the server.
* Start the Duskserver running:
```
cd C:\Users\[yourusernamehere]\Documents\near-exclave\DuskFiles\DuskCheerpj
java -jar Duskserver.jar
```
* Put the client on an http server:
```
cd C:\Users\[yourusernamehere]\Documents\near-exclave\DuskFiles\DuskCheerpj\wwwClient
python3 http.server -m 8000
```
* Funnel the client to the internet and serve the Dusk server port to your Tailnet (run this as administrator): 
```
tailscale funnel --bg 8000 
tailscale serve --tcp=2222 tcp://localhost:7474
```

8. Go to your new website and click "client.html" to start the game. Connect to server using your Tailnet IPv4 address and port 2222.





* The raw, uncompiled server source code should be located in `C:\Users\[yourusernamehere]\Documents\near-exclave\DuskFiles\DuskServerSource`.
* The raw, uncompiled client source code should be located in `C:\Users\[yourusernamehere]\Documents\near-exclave\DuskFiles\ClientSourceCJ`.

Compile Server Files:
```
cd C:\Users\[yourusernamehere]\Documents\near-exclave\DuskFiles\DuskServerSource
javac *.java
```
Compile Client Files:
```
cd C:\Users\[yourusernamehere]\Documents\near-exclave\DuskFiles\ClientSourceCJ
javac -cp C:\Users\[yourusernamehere]\Documents\near-exclave\DuskFiles\DuskComet-Richter\wwwClient\lib\flatlaf-3.4.1.jar:. *.java
```
Run Server:
```
cd C:\Users\[yourusernamehere]\Documents\near-exclave\DuskFiles
java -cp DuskServerSource DuskServer
```
Run Client (currently not working):
```
java -cp C:\Users\[yourusernamehere]\Documents\near-exclave\DuskFiles\DuskComet-Richter\wwwClient\lib\flatlaf-3.4.1.jar:. Dusk
```



## Contribution

Near: Exclave isn't really *meant* to go back into DuskRPG, and it will definetly break things if it's pulled into DuskRPG! But if I run into anything that happens to need fixing that also applies to DuskRPG as a whole, I'll be sure to submit any fixes I find as branch PRs in main DuskRPG.

# DuskRPG

The lovely individuals contributing to DuskRPG deserve so many good things. Their work has singlehandedly kinda saved me a *lot* of work and made this project possible at all in the first place, actually.
May you wonderful, wonderful people never ever get a shoe pebble again in your lives.
If this project should be taken down for whatever reason, please let me know and I'll get on it right away! You can shoot me an email at `nylonswordsman@gmail.com`.
