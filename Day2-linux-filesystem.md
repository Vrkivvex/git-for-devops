# Day 2 – Linux Filesystem

## Root Directory

Linux uses a single filesystem starting from:

/

Everything exists under this root directory.

Example structure:

/
├── home
├── etc
├── var
├── usr
├── bin

## Important Directories

/home → user files  
/etc → configuration files  
/var → logs and variable data  
/usr → installed programs  
/tmp → temporary files  

## Navigation Commands

Check current directory

pwd

List files

ls

Detailed list

ls -l

Change directory

cd foldername

Go back

cd ..

Go to home

cd ~

## File Operations

Create file

touch file.txt

Open editor

nano file.txt

View file

cat file.txt

View long file

less file.txt

## Key Concept

Linux follows the idea:

Everything is a file.