# Day 3 – Permissions, Processes, Searching

## File Permissions

Example permission:

-rwxr-xr--

Breakdown

Owner → first 3 characters  
Group → next 3 characters  
Others → last 3 characters  

Permission symbols

r → read  
w → write  
x → execute  

## Change Permissions

chmod 777 file.txt

Everyone can read, write, execute.

Better example

chmod 644 file.txt

Owner → read + write  
Others → read

## Change Owner

sudo chown user file.txt

## Processes

List running processes

ps
ps aux

Real time monitor

top

Better monitor

htop

Kill process

kill PID

## Searching with grep

Search text

grep word file.txt

Example

grep docker notes.txt

## Pipes

Send output from one command to another

ps aux | grep firefox

List only txt files

ls | grep txt

## Finding Files

Search file

find . -name file.txt

Search extension

find . -name "*.txt"

## Logs

Show last lines

tail log.txt

Show last 10 lines

tail -n 10 log.txt

Watch logs live

tail -f log.txt