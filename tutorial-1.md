# Tutorial #1 Basics

## The mod structure

Mods when they have all their folders in will look like this.
```
Mod/
    - backgrounds/
    - components/
    - crosshairs/
    - FancyInput/
    - flags/
    - ground/
    - instruments/
    - languages/
    - lib/
    - music/
    - palettes/
    - scripts/
    - settings/
    - sounds/
    - src/
        - client/
        - server/
        - shared/
    - thumbs/
    - worldtypes/
    - manifest.succ
```
Does that mean you need to have all of these folders?
Of course you don't that would be ridiculus if you did.

## Manifest.succ

The Manifest.succ file will look something like this.
```
ID: exampleID
Name: exampleName
Author: exampleAuthor
Version: 0.0.0
Priority: 0
```
This file is where you will put your mod name, id, and who made it, and what version it is and what load priority it is (the load priority might be true).
So you should make a new folder call it whatever you want, like CoolMod, or FirstMod, and then create a manifest.succ file.
and in that file you should type.
```
ID:
Name:
Author:
Version:
Priority:
```
Once you do that you should fill it out.

## Components
This next part is going to be about components.
So you should make a new folder call it whatever you want, like CoolMod, or FirstMod, and then create a manifest.succ file.
