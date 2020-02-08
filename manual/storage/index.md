# Storages

There are different types of storages for different situations and use cases, Save System supports both Local and Online storage types, so you can easily manage your data across different platforms with different storage types using an Unified API.

## Built-in Storages

The package includes built-in storages for most common use cases that enables you to get a boost in your productivity:

- File
- Unity PlayerPrefs
- Firebase (both Realtime Database and Cloud Storage)
- PlayFab (both new Entity objects and UserData API)

## Custom Storage

You can easily create your own custom storage by extending the [`StorageBase`](xref:Bayat.SaveSystem.Storage.StorageBase) class and implementing the methods.

[Learn more](../extend/storage.md)

## Backup

Storage API allows you to backup your data by duplicating it in most cases (it depends on the storage implementation), then it uses the Meta Data API to add the backup to the list of the backups in the item meta data, so when you use [`SaveSystemAPI.GetBackups`](xref:Bayat.SaveSystem.SaveSystemAPI.GetBackupsAsync(System.String)) or [`SaveSystemAPI.RestoreLatestBackup`](xref:Bayat.SaveSystem.SaveSystemAPI.RestoreLatestBackupAsync(System.String)) it detects the backups through there.

So it means by disabling the Meta Data API, you wouldn't be able to use Backups. (by the way it depends on the storage implementation, but in most cases it wouldn't work)

## Meta Data

The Meta Data API allows you to store additional meta information about the storage item, such as Last Access Time, Last Modification Time, Is Encrypted and ...
So, it would allow you to add your own custom data to it, or use the existing information.

## Catalog

The Catalog storage item allows the storage to keep a list of items in the storage so you wouldn't have to use Query methods to loop through files or keys in a database to find out which files or entries are saved using Save System, also it just saves the identifier in the list, not the full path or modified identifier, so it would let you get most out of the identifier value by converting it to whatever you want. 

Also, it lets you to keep a list of active saved items in the storage too, for like displaying saved slots.

## Connection String

The connection string allows to create a new storage instance using an URL-like syntax string.

```
<Storage Protocol>://<Parameter Name>=<Paramter Value>; <Parameterss ...>
```

The storage protocol is actually the storage identifier, such as `disk` or `playerprefs` or any other storages available.

So for example if you want to initialize the [`LocalDiskStorage`](xref:Bayat.SaveSystem.Storage.LocalDiskStorage), you can do it like this:

```
disk://path={0}
```

Also, you can use pre-defined variables inside the connection string which are identified using numbers, the below shows the list of available pre-defined variable numbers you can use:

- {0} = [Application.persistentDataPath](https://docs.unity3d.com/ScriptReference/Application-persistentDataPath.html)
- {1} = [Application.dataPath](https://docs.unity3d.com/ScriptReference/Application-dataPath.html)
- {2} = [Application.streamingAssetsPath](https://docs.unity3d.com/ScriptReference/Application-streamingAssetsPath.html)
- {3} = [Application.temporaryCachePath](https://docs.unity3d.com/ScriptReference/Application-temporaryCachePath.html)
- {4} = [Application.absoluteURL](https://docs.unity3d.com/ScriptReference/Application-absoluteURL.html)
- {5} = [Application.buildGUID](https://docs.unity3d.com/ScriptReference/Application-buildGUID.html)
- {6} = [Application.companyName](https://docs.unity3d.com/ScriptReference/Application-companyName.html)
- {7} = [Application.productName](https://docs.unity3d.com/ScriptReference/Application-productName.html)
- {8} = [Application.identifier](https://docs.unity3d.com/ScriptReference/Application-identifier.html)
- {9} = [Application.version](https://docs.unity3d.com/ScriptReference/Application-version.html)
- {10} = [Application.unityVersion](https://docs.unity3d.com/ScriptReference/Application-unityVersion.html)

You can find more information about built-in storages connection string:

- [File](built-in/file.md)
- [PlayerPrefs](built-in/playerprefs.md)

Or third-party integrations:

- [Firebase Realtime Database](third-party/firebase/database.md)
- [Firebase Cloud Storage](third-party/firebase/storage.md)
- [PlayFab UserData](third-party/playfab/userdata.md)
- [PlayFab Entity Objects](third-party/playfab/entity-objects.md)