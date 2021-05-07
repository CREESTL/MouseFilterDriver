## Quick Overview

This is a very simple filter driver. And here are the steps to run it.

(**Please note that all mentioned below was done using VirtualBox and Windows10 installed on it in order to prevent main OS crash!**)

### What you will need:
- OSRLoader (Download it [here](https://www.osronline.com/article.cfm%5Earticle=157.htm))
- DbgView (Download it [here](https://docs.microsoft.com/en-us/sysinternals/downloads/debugview))
- Visual Studio 2019 (Download it [here](https://visualstudio.microsoft.com/ru/vs/))
- Do all steps from [here](https://docs.microsoft.com/en-us/windows-hardware/drivers/download-the-wdk) to install WDK
- Two hands

### What to do next:
- Reboot windows to the mode where it does not check if drivers were signed (Google on it) - otherwise your driver will not start!
- Open VS2019
- Create new project. VS will allow you to choose the type of the project. If you've installed WDK correctly - there will be "KMDF.Empty" type (**NOT** "KMDF.USB"). Choose it and continue with other steps to create a project
- In 'Sorce Files' copy `main.c` from this repo
- Go to *Project settings -> C/C++ -> Code creation* and disable `Spectre` library
- Also in *Project settings -> C/C++ -> General* set `Warning Level` to `1`
- Set `Debug` and `x64` in VS and build solution (it will create a folder in your project containing `.inf`, `.sys` and `.cat` files)
- Run DbgView **as administrator**. In `Capture` set `Capture Kernel`
- Run OSRLoader
- In OSRLoader  search for `.sys` file created previously
- `Register Service`
- `Run Service`

There you go! Now in your DbgView you can see message `Random coordinates: ... , ...` (when your've moving the mouse)

That means that the driver is working correctly!

