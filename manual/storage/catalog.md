# Catalog

The catalog holds a list of saved storage items identifier, this allows you to know what identifiers you've used, how many items you've saved and lets you to iterate through them.

## Loading the Catalog

You can load the catalog using [`IStorage.LoadCatalog`](xref:Bayat.SaveSystem.Storage.IStorage.LoadCatalog) or [`SaveSystemAPI.LoadCatalogAsync`](xref:Bayat.SaveSystem.SaveSystemAPI.LoadCatalogAsync) method:

```csharp
List<string> catalog = await SaveSystemAPI.LoadCatalogAsync();
```

## Modifying the Catalog

```csharp
List<string> catalog = await SaveSystemAPI.LoadCatalogAsync();
catalog.Remove("my-identifier");

// Save the modified catalog
await SaveSystemAPI.SaveCatalogAsync(catalog);
```

## Disabling the Catalog

You can disable the catalog feature by disabling the **Use Catalog** in a Settings preset: 

![Default Settings](../../images/default-settings-preset.png)

![Default Settings Window](../../images/default-settings-window.png)

Or using the Settings window or by setting the **UseCatalog** property of [`SaveSystemSettings`](xref:Bayat.SaveSystem.SaveSystemSettings) class:

```csharp
SaveSystemSettings settings = SaveSystemSettings.DefaultSettings.Clone();
settings.UseCatalog = false;
```

Or disable it from default settings:

```csharp
SaveSystemSettings settings = SaveSystemSettings.DefaultSettings;
settings.UseCatalog = false;
```