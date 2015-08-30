---
layout: post
title: Introducing Surgeon
comments: true
tags:
- Android
- Python
---

## Prologue
For the last few months, well thinking again maybe two years now, I have been working on a new Android project with other partners. I learned a lot from the beginning of this particular project until now, and I can see my improvements that I have been learning all the way down throw the code.

One of the new routines I impose myself it is to divide the values in smaller/themed ones. What I mean with this is, for example, divide the ‘strings.xml’ file in to others like ’strings_settings.xml’ or ‘strings_menu.xml’.

What I want to achieve with that? You may ask. Well, be more organized, avoid wasting time searching in a huge strings file to change one single coma are two good reasons to begin.

The problem? Simple, when you want to translate your app for the first time you have too many files. But the thing get a lot wort from this point. Imagine you add a new string in each string file, it is too hard to keep tracking on every single file.

This is why I developed Surgeon. Ok also I wanted to take a shot in Python, so finally I have found my excuse.

## What is Surgeon?
**For the Android developers that love to split the strings files, will have to suffer when they have to add translations.** It is hard to know if there is a new string searching in each file for each translation and mobile network.

Surgeon it is a simple script that **finds all the string files, merges them and compares each translation to find the differences**. Finally generates a new file with the missing translations in each language.

## How do I use it?
- Edit the *config.py* file and put the name and the path of your project and/or other extra configurations.
- And run the script with:

		python surgeon.py
		
Easy isn't it?

## Customize
- Define where is your project with *PROJECT_PATH*
- Search in a specific module defining *MODULE_NAME* constant
- For a particular flavour
- You can define if your strings files has a particular prefix or suffix
- And last but no least, the result file
- What more? DIY and PR :)
	
## Don't be shy
Pull requests are more than welcome. I am not an expert in Python so lets put this newbie surgeon to the top of the wall of fame.

## Download
**Surgeon** is  hosted with GitHub. Head to the <a href="https://github.com/MiguelCatalan/Surgeon">GitHub repository</a> for downloads, bug reports, and features requests.

**Thanks!**
