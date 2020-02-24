# Auto Save

The auto save feature allows you to save and load data without using the programatic interface.

## Auto Save Component

Tha auto save component allows you to control the serialization behaviour of a GameObject, such as serializing components or children, excluding specific children or components.

![Auto Save](../images/auto-save-component.png)

- **Serialize Children**: Enables serialization of the GameObject children.
- **Serialize Components**: Enables serialization of the GameObject components.
- **Serialize Excluded Children**: Inverts the serialization of the GameObject children using the **Excluded Children** list that means instead of excluding them, it will only serialize the children that are included in the list.
- **Serialize Excluded Components**: Inverts the serialization of the GameObject components using the **Excluded Components** list that means instead of excluding them, it will only serialize the components that are included in the list.
- **Excluded Children**: The list of excluded children, if the **Serialize Excluded Children** option is not set, it prevents the children in this list from being serialized, otherwise it'll only serialize the children included in this list.
- **Excluded Components**: The list of excluded components, if the **Serialize Excluded Components** option is not set, it prevents the components in this list from being serialized, otherwise it'll only serialize the components included in this list.

## Auto Save Manager

The Auto Save Manager component holds a list of all the Auto Save components available in the scene, so you can save the GameObjects with Auto Save copmponent easily by calling the Save method on Auto Save Manager or use save event to do it at specific time, such as OnApplicationQuit, OnApplicationPause, OnDisable or OnDestroy and then load it back by calling Load manually or using an event like Start, Awake or OnEnable.

![Auto Save Manager](../images/auto-save-manager-component.png)

- **Identifier**: The storage item identifier to store the data into, it can be a file name or a key.
- **Settings Preset**: The settings preset to use.
- **Auto Saves**: The auto saves available in the scene.
- **Save Event**: The event to save the data.
- **Load Event**: The event to load the data.

Learn more about these events at [**Order of Execution for Event Functions**](https://docs.unity3d.com/Manual/ExecutionOrder.html) article.