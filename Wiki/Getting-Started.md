## Getting started with modding

If this is your first adventure with modding there can be quite a bit of confusion as you get accustomed to the (sometimes jank) ways things work, this page is here to hopefully help with that a bit.

### What do I need?
First off to begin working with mods you're gonna need to get yourself setup with a C# development environment, you can get away with either targetting **.NET Standard 2.1** or alternatively you can target **.NET Framework 4.8**, mods compiled with either will work correctly, tho some oddities can occur with some dependencies such as HarmonyX.

After you have your C# dev environment setup you'll want to install the latest MelonLoader release (currently 0.6.1) on your ChilloutVR install, there are other mod loaders that will work just fine such as Bepinex, however CVRMG primarily focuses on MelonLoader based modding, as well as most of the existing CVR userbase already use MelonLoader.

### What references do I need?
To work with stuff within CVR you'll need to reference a few of the game's DLLs, as well as a few MelonLoader DLLs, this of course depends on what you want to work with and what kind parts of the Unity Engine you might end up touching, but here's a general list to get you started!

You'll find all these references under the directories listed below

- ChilloutVR/ChilloutVR_Data/Managed
    - Assembly-CSharp.dll - This contains most of the classes and components used by ChilloutVR
    - UnityEngine.dll - Unity Engine Core Components
    - UnityEngine.CoreModule.dll - Unity Engine Core Components
- ChilloutVR/MelonLoader/net35
    - 0Harmony.dll - HarmonyX, this it used to patch and fiddle with C# functions, both Unity side and CVR side
    - MelonLoader.dll - MelonLoader dependency, this is needed for your mod to work with ML at all

