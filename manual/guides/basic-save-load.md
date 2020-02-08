# Basic Saving and Loading

Here we will save a few simple data types using the [`SaveSystemAPI`](xref:Bayat.SaveSystem.SaveSystemAPI) class as a demonstration of the API usage.

## Saving a Primitive

```csharp
async void Start() {

    // The location in the storage that we want to save the data, it can be a file, a key, or any kind of identification for the type of storage
    string identifier = "name.json";

    // The simple data we're going to save
    string data = "Bayat - Save System";

    // Save the data associated with the identifier
    await SaveSystemAPI.SaveAsync(identifier, data);

    // Load back the saved data associated with the identifier
    string loadedData = SaveSystemAPI.LoadAsync<string>(identifier);

    Debug.Log(data); // Outputs "Bayat - Save System"
    Debug.Log(loadedData); // Outputs "Bayat - Save System"
}
```

## Saving a Custom Class

```csharp
public class Player {

    public string name;
    public int currentHealth;
    public int score;
    public int highScore;
    public Weapon[] weapons;
    
}

public class Weapon {

    public string name;
    public int damage;

}

public class Gun : Weapon {

    public int currentAmmo;

}
```

```csharp
async void Start() {

    // The location in the storage that we want to save the data, it can be a file, a key, or any kind of identification for the type of storage
    string identifier = "name.json";

    // The simple data we're going to save
    Player data = new Player();
    data.name = "Michael";
    data.currentHealth = 32;
    data.score = 1000;
    data.highScore = 12000;
    data.weapons = new Weapon[] {
        new Weapon() {
            name = "Knife",
            damage = 1
        },
        new Gun() {
            name = "Pistol",
            damage = 10,
            currentAmmo = 100
        }
    };

    // Save the data associated with the identifier
    await SaveSystemAPI.SaveAsync(identifier, data);

    // Load back the saved data associated with the identifier
    Player loadedData = SaveSystemAPI.LoadAsync<Player>(identifier);

    Debug.Log(data.name); // Outputs "Michael"
    Debug.Log(loadedData.name); // Outputs "Michael"
    Debug.Log(loadedData.weapons[1] is Gun); // Outputs "True"
}
```