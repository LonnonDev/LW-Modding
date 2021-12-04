# C# Localization Tutorial
## How to do Localization
To do localization you must create a folder in your mod directory called `languages`.
Then create your language folder called `English` for example.
This folder is where all your language succs will be.
to create a language succ it must follow this format `<Language>_<type>.succ`.
For example an english language succ would be `English_components.succ` and would look like this.
```succ
<modname>.<component>: "<name>"
```
You don't have to put everything in this one file you can split them up.
For small mods you'll probably put everything in this one file.
And that is how you do localization.
