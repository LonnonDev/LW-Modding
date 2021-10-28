# LW - LS Modding
## Contents
1. [Structure](#structure)
2. [Files](#files)
    - [/manifest.succ](#modmanifestsucc)
    - [/components/\<component>.succ](#modcomponentscomponentsucc)
    - [/scripts/\<script>.lsx](#modscriptsscriptlsx)
    - [/ignore](#modignore)

## Structure
[Back To Top](#Contents)

When makign a mod you would want files to store that additions you want to make to the game.  
The usual structure looks like:
```
Logic World/GameData
    - <mod>/
        - components/
            - <component>.succ
        - languages/
            - English/
                <translation-strings>.succ
            - <Other>/
        - scripts/
            - <script>.lsx
        - manifest.succ
        - ignore #optional
```

## Files
### `<mod>/manifest.succ`
[Back To Top](#Contents)

This is information about your mod. It is what will be shown in the mod list in-game, and the ID is prefixed to components in the item menu so it's best to keep it short. It doesn't have to be unique, so if you want to make multiple mods it will keep your things together (think of it as a namespace).
```succ
ID: exampleID
Name: exampleName
Author: exampleAuthor
Version: 0.0.0
Priority: 1
```

![Loaded Mods Menu](https://user-images.githubusercontent.com/7610940/138955141-7165ec2f-a975-42ad-919c-c91c15ebc615.png)

### `<mod>/components/<component>.succ`
[Back To Top](#Contents)

This is what defines your component as a placeable item in-game. See the examples in `Logic World/GameData/MHG/Components` or https://docs.logicworld.net/articles/component-reference.html

Components will appear in the item menu like this:  
```xml
<Manifest ID>.<Name in component succ>
```
Using the example manifest above, and this example `succ`:
```succ
exampleComponent:
    column: "Logic"
    prefab:
        blocks:
            - Standard
        inputs:
            -
                position: (0, 0.5, -0.5)
                rotation: (-90, 0, 0)
        outputs:
            -
                position: (0, 0.5, 0.5)
                rotation: (90, 0, 0)
    logicScript: exampleID.exampleComponent
    placingRules:
        gridPlacingDimensions: (2, 1)
...
```

The item would appear in-game as `exampleID.exampleComponent`:

![exampleID.exampleComponent](https://user-images.githubusercontent.com/7610940/138955557-42657956-80c9-4778-9743-2ffcd2a55edf.png)

### `<mod>/scripts/<script>.lsx`
[Back To Top](#Contents)

These are the files that contains all the logic of your components. 

Here is an example (`NOT gate`):
```
any
    out[0] != in[0]
end
```
[`.lsx` reference](Reference/LSX-Guide.md)

### `<mod>/ignore`
[Back To Top](#Contents)

If this file is present, the mod will not be loaded in to the game.  
This allows you to still play on servers or worlds that dont have the mod.