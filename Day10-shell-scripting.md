# Day 10 – Shell Scripting (Detailed)

## What is Shell Scripting

Shell scripting is used to automate tasks in Linux.

Instead of running commands manually, we write them in a script file.

Example use cases:

- automate backups
- deploy applications
- manage Docker containers
- schedule tasks

---

## Creating a Script

Create file:

touch script.sh

Open file:

nano script.sh

---

## Shebang

#!/bin/bash

This tells the system to use bash shell to execute the script.

---

## Make Script Executable

chmod +x script.sh

Run script:

./script.sh

---

## Basic Commands in Script

echo → print text  
pwd → show current directory  
date → show date and time  
whoami → current user  

Example:

echo "Hello"
pwd
date

---

## Variables

Define variable:

NAME="Vishesh"

Use variable:

echo $NAME

Important:

- No spaces around =
- Use $ to access value

---

## User Input

read NAME

Example:

echo "Enter your name:"
read NAME
echo "Hello $NAME"

---

## Conditions

Used for decision making.

Syntax:

if [ condition ]
then
  command
else
  command
fi

Example:

if [ $AGE -ge 18 ]
then
  echo "Adult"
else
  echo "Minor"
fi

Operators:

-ge → greater or equal  
-gt → greater  
-lt → less  
-eq → equal  

---

## Loops

Used to repeat tasks.

Example:

for i in 1 2 3
do
  echo $i
done

---

## Real DevOps Example

Stopping multiple containers:

for i in container1 container2
do
  docker stop $i
done

---

## Key Learning

Shell scripting helps automate repetitive tasks and is widely used in DevOps for:

- deployment scripts
- monitoring scripts
- automation pipelines