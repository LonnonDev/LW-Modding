# LW - C\# Modding
## Contents
1. [Structure](#structure)
2. [Loader](#loader)
3. [Mods](#mods)

## Structure

There are two folders required. A mod loader, and the mod itself. The full structure looks like this. Individual elements will be explained further later.
```
Logic World/GameData
    - loader/
        - src/
            - server/
                - loader.cs
                - <modname-component>.cs #The file name can be anything
        - manifest.succ
    - <mod>/
        - components/
            - <component>.succ
        - src/
            - server/
                - <non component mod code>.cs   #optional
        - manifest.succ
        - ignore #optional
```

## Loader

The loader's job is to get your component code into the game so your components can reference it to do things. You should plan around using this standard format so everyone can use your mod alongside others in a drag and drop way.

These are the files involved:
```
Logic World/GameData
    - loader/
        - src/
            - server/
                - loader.cs
        - manifest.succ
```

You should not distribute the loader files with your mod, expect them to already be there.

### `manifest.succ`

The loader manifest looks like this:
```
ID: CML
Name: CS Mod Loader
Author: LonnonjamesD
Version: 1.0.0
Priority: 100
```
Note the priority is 100 which is the maximum. The base game is 99, and the minimum is -100. Mods are loaded in descending priority. This way the loader is always loaded first so that everything is there by the time other mods load.

### `loader.cs`
This is the code for the loader. It doesn't do anything special by itself, but it's needed for the mod component code to be loaded and compiled for use.

```cs
using LogicAPI.Server;
using LogicLog;

public class Loader : ServerMod {
    protected override void Initialize() {
        Logger.Info("CSmodLoader initialized");
    }
}
```

## Mods
For each mod you would want files to store that additions you want to make to the game.  
A usual structure looks like:
```
Logic World/GameData
    - loader/
        - src/
            - server/
                - <modname-component>.cs
    - <mod>/
        - components/
            - <component>.succ
        - src/
            - server/
                - <non component mod code>.cs #optional
        - manifest.succ
        - ignore #optional
```

### `<mod>/manifest.succ`

This is information about your mod. It is what will be shown in the mod list in-game, and the ID is prefixed to components in the item menu so it's best to keep it short. It doesn't have to be unique, so if you want to make multiple mods it will keep your things together (think of it as a namespace).
```js
ID: exampleID
Name: exampleName
Author: exampleAuthor
Version: 0.0.0
Priority: 1
```

![Loaded Mods Menu](https://user-images.githubusercontent.com/7610940/138955141-7165ec2f-a975-42ad-919c-c91c15ebc615.png)

### `<mod>/components/<component>.succ`

This is what defines your component as a placeable item in-game. See the examples in `Logic World/GameData/MHG/Components` or https://docs.logicworld.net/articles/component-reference.html

Components will appear in the item menu like this:  
```xml
<Manifest ID>.<Name in component succ>
```

Using the example manifest above, and this example succ:
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
    logicCode: exampleID.exampleComponent
    placingRules:
        gridPlacingDimensions: (2, 1)
...
```

The item would appear in-game as `exampleID.exampleComponent`

![exampleID.exampleComponent](https://user-images.githubusercontent.com/7610940/138955557-42657956-80c9-4778-9743-2ffcd2a55edf.png)

### `loader/src/server/<modname-component>.cs`

This is where your component logic goes. It can contain other code too, and you can have multiple components defined in 1 file. If your file is big and you want to split it, you can put any non-component logic in the mod/src/server/ folder. But anything used in code referenced using logicCode in your succ file **MUST** be in here, the rest will not be loaded by the time the component types are compiled. You'll have to use reflection for anything external (so probably just accept the big file). You should prefix the filename with the same name as the mod folder so it's easier to find and delete when removing the mod

If you want to use the full capabilities of of the component system (inputs, outputs, updating logic each server tick etc.) your component should extend LogicComponent from LogicWorld.Server.Circuitry.

Here is an example 
```cs
using LogicWorld.Server.Circuitry;

namespace exampleID
{
    public class exampleComponent : LogicComponent
    {
        protected override void DoLogicUpdate()
        {
            base.Outputs[0].On = base.Inputs[0].On;
        }
    }
}
```

This example simply sets the single output to the single input each time the server ticks. More info on [LogicComponent](CS-LogicComponent.md) and its features coming soon™

### `<mod>/src/server/<non component mod code>.cs`
##### Reminder: Methods referenced by logicCode statements **MUST** go in `loader/src/server/`

You can put any other code in here. It will be compiled and available in the game, however it won't be loaded until after the `loader/src/server/<component>.cs` file has loaded. So if that references any types/methods defined in code in this folder it won't work. Generally you should try to keep all C# code in the `loader/src/server/<component>.cs` file, but *technically* anything here will get compiled and loaded too.

### `<mod>/ignore`
If this file is present, the mod will not be loaded.