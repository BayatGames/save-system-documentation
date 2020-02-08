# Installation

Follow the below instructions before importing the package:

- The save system requires **.NET 4.x** or higher, so before importing the package make sure to set **Api Compatiblity Level** or **Scripting Runtime Version** to **.NET 4.x** in [**Player Settings**](https://docs.unity3d.com/Manual/class-PlayerSettings.html).

Now, import the package and when the import process is done, the save system is ready to use, by the way there are a few more tips to help you to get most out of it:

- Download and import the demos to try out the save system features, [**Download now**](../packages/demos.unitypackage)

- Modify the default settings through the **Window > Bayat > Save System > Default Settings** window.

- Create a new **Save System Manager** for the scene that you want to use the save system in it whether by right clicking on the hierarchy and using **Bayat > Save System > Save System Manager** or by creating a new object manually and adding **Save System Manager**, **Auto Save Manager** and ***Scene Reference Resolver** to it.

- Use **Collect Scene Dependencies*** on the **Scene Reference Resolver** component or through the **Window > Bayat > Core > Scene Reference Resolver** window to fetch new available scene objects and components and add them to the reference database.

- Use **Collect Project Dependencies*** on the **Asset Reference Resolver** asset or through the **Window > Bayat > Core > Asset Reference Resolver** window to fetch new available assets and add them to the reference database.

- Use the **Window > Bayat > Core > Reference Checker** window to check whether an object is referenced by either Asset Reference Resolver or Scene Reference Resolver.

- Generate a new custom object converter using the **Window > Bayat > Json > Create Object Converter** window.

If you ran into any issues or had any questions, email us at support@bayat.io.