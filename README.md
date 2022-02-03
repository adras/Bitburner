# Bitburner - Skynet
## Introduction
This is my attempt at creating skynet for bitburner. The idea was to create a fully automated script which takes over all servers in the game, upgrades them where possible and farms money/hacking xp.

# Setup
To set this up, create the files with the same names as here on github on your "home" computer in Bitburner

## Deploy
Run the main deploy/hacking script. This hacks all servers on the first level (if possible), copies and executes hack.script on these servers. This script can be executed multiple times. E.g. if you didn't have enough hacking xp to hack a server, and have the xp later, just run it again, and the server will be included.
Rerunning the script however terminates the current hacking attempt on all servers.

Execute: `run deploy.script`

## Server-Farms
There's another script, which automatically buys new servers when there's enough money. Such a server will be automatically setup to run the `weaken.script`. Weaken picks a random server, weakens and then grows it. This is supposed to be run after deploy.script

To set this up, pick a server with enough ram, e.g. `foodsnstuff` and run the following commands
Copy the script to the food server: `scp farm.script foodnstuff`
Connect to foodsnstuff: `connect foodsnstuff`
Kill hacking script which was started by deploy: `kill hack.script`
Start the farm script: `run farm.script`
Restart the hack script: `run hack.script -t ??' - Not sure how many threads are possible. Try 2-4 as -t parameter

## TakeOver
`takeOver.script` Is the script which hacks a server. This is automatically run by `deploy.script`. However it requires some configuration. As of creating this, there was no way to figure out if `bruteSSH` and the other tools are already researched. This results in some annoying popups when these tools are executed but not yet researched. Therefore this script is configurable by the `maxPorts` variable. Choose 0 if no tools are researched, 1 if you've got bruteSSH, 2 if you have the FTP tool as well. More is not yet implemented, but it should be easy to add these tools as well.

# Result
The `deploy.script` automatically hacks servers and installs `hack.script`. The `farm.script` automatically buys up to 25 servers (current maximum) and runs `weaken.script` on each server. This weaken script by default picks a random server, weakens and then grows it. Since there's already a hack script installed by deploy on each of these servers, this helps to boost them.
