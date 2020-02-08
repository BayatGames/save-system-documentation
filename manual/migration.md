# Migration

If you're a returning user from whether Easy Save or Save Game Pro and want to migrate your existing game / app to Save System, keep reading to learn how to migrate your data.

First, for migrating the data, the data should be loaded to its C# object representation, so you should know the data type of your saved data in order to migrate it to new system, then the data is saved using the new system and you're ready to use it from further on.

- [Download **Easy Save 2 Migration**](../packages/easy-save-2-migration.unitypackage)
- [Download **Easy Save 3 Migration**](../packages/easy-save-3-migration.unitypackage)
- [Download **Save Game Pro Migration**](../packages/save-game-pro-migration.unitypackage)

## Migrating from Easy Save

### Easy Save 2

```csharp
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

using Bayat.SaveSystem.Migration;

public class SaveGameTest : MonoBehaviour
{

    public string identifier = "test.txt";

    async void Start()
    {

        // Migrate the data if it is not already migrated
        if (!await EasySave2Migration.IsMigrated(identifier))
        {

            // The data type here is a string, but you should change it based on your stored data using the prevoius system
            await EasySave2Migration.Migrate<string>(identifier);
        }
    }

}
```

### Easy Save 3

```csharp
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

using Bayat.SaveSystem.Migration;

public class SaveGameTest : MonoBehaviour
{

    public string identifier = "test.txt";

    async void Start()
    {

        // Migrate the data if it is not already migrated
        if (!await EasySave3Migration.IsMigrated(identifier))
        {
            
            // The data type here is a string, but you should change it based on your stored data using the prevoius system
            await EasySave3Migration.Migrate<string>(identifier);
        }
    }

}
```

## Migrating from Save Game Pro

```csharp
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

using Bayat.SaveSystem.Migration;

using BayatGames.SaveGamePro;

public class SaveGameTest : MonoBehaviour
{

    public string identifier = "test.txt";

    async void Start()
    {
        
        // Migrate the data if it is not already migrated
        if (!await SaveGameProMigration.IsMigrated(identifier))
        {
            
            // The data type here is a string, but you should change it based on your stored data using the prevoius system
            await SaveGameProMigration.Migrate<string>(identifier);
        }
    }

}
```
