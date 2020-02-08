# Meta Data

The meta data API allows you to store additional information with storage items, this allows for extra functionalities such as holding a list of backups, last modification time, last access time, whether the file is encrypted or no, ...

## Loading the Meta Data

You can load the meta data using [`IStorage.LoadMetaData`](xref:Bayat.SaveSystem.Storage.IStorage.LoadMetaData(System.String)) or [`SaveSystemAPI.LoadMetaDataAsync`](xref:Bayat.SaveSystem.SaveSystemAPI.LoadMetaDataAsync(System.String)) method:

```csharp
StorageMetaData metaData = await SaveSystemAPI.LoadMetaDataAsync("my-identifier");
```

## Modifying the Meta Data

```csharp
StorageMetaData metaData = await SaveSystemAPI.LoadMetaDataAsync("my-identifier");

// Add a new custom meta data
metaData["Corrupted"] = true;

// Or modify existing meta data
metaData["Encrypted"] = false;

// Save the modified meta data
await SaveSystemAPI.SaveMetaDataAsync("my-identifier", metaData);
```

## Disabling the Meta Data

You can disable the meta data feature by disabling the **Use Meta Data** in a Settings preset:

![Default Settings](../../images/default-settings-preset.png)

![Default Settings Window](../../images/default-settings-window.png)

Or using the Settings window or by setting the **UseMetaData** property of [`SaveSystemSettings`](xref:Bayat.SaveSystem.SaveSystemSettings) class:

```csharp
SaveSystemSettings settings = SaveSystemSettings.DefaultSettings.Clone();
settings.UseMetaData = false;
```

Or disable it from default settings:

```csharp
SaveSystemSettings settings = SaveSystemSettings.DefaultSettings;
settings.UseMetaData = false;
```