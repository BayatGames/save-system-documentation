# Raw Saving and Loading

Here we will save data directly to the storage without serialization and encryption using the [`SaveSystemAPI`](xref:Bayat.SaveSystem.SaveSystemAPI) class as a demonstration of the API usage.

## Read and Write Text

```csharp
async void Start() {

    // The location in the storage that we want to save the data, it can be a file, a key, or any kind of identification for the type of storage
    string identifier = "name.txt";

    // The simple data we're going to save
    string data = "Bayat - Save System";

    // Save the data directly associated with the identifier
    await SaveSystemAPI.WriteAllTextAsync(identifier, data);

    // Load back the saved data associated with the identifier
    string loadedData = SaveSystemAPI.ReadAllTextAsync(identifier);

    Debug.Log(data); // Outputs "Bayat - Save System"
    Debug.Log(loadedData); // Outputs "Bayat - Save System"
}
```

## Read and Write Binary

```csharp
async void Start() {

    // The location in the storage that we want to save the data, it can be a file, a key, or any kind of identification for the type of storage
    string identifier = "name.bin";

    // The simple data we're going to save
    byte[] data = System.Text.Encoding.UTF8.GetBytes("Bayat - Save System");

    // Save the data directly associated with the identifier
    await SaveSystemAPI.WriteAllBytesAsync(identifier, data);

    // Load back the saved data associated with the identifier
    byte[] loadedData = SaveSystemAPI.ReadAllBytesAsync(identifier);

    Debug.Log(System.Text.Encoding.UTF8.GetString(data)); // Outputs "Bayat - Save System"
    Debug.Log(System.Text.Encoding.UTF8.GetString(loadedData)); // Outputs "Bayat - Save System"
}
```