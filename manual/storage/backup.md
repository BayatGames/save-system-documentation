# Backup

The backup feature allows you to take a copy of your existing storage item to restore it at anytime later, it'll be created based on the current date and time, so it'll be unique to the current time and also it adds a new entry to the backups list of storage item meta data, so this feature **requires Meta Data API** to be enabled.

## Creating a new Backup

```csharp
StorageBackup backup = await SaveSystemAPI.CreateBackupAsync("my-identifier");
```

## Restoring a Backup

```csharp
// Just using the latest backup as an example
StorageBackup latestBackup = await SaveSystemAPI.GetLatestBackup("my-identifier");

await SaveSystemAPI.RestoreBackup("my-identifier", latestBackup);
```

## Restoring the latest Backup

```csharp
await SaveSystemAPI.RestoreLatestBackupAsync("my-identifier");
```

## Retrieving a list of all Backups

```csharp
List<StorageBackup> backups = await SaveSystemAPI.GetBackups("my-identifier");
```

## Delete a Backup

```csharp
// Just using the latest backup as an example
StorageBackup latestBackup = await SaveSystemAPI.GetLatestBackup("my-identifier");

await SaveSystemAPI.DeleteBackup("my-identifier", latestBackup);
```

## Deleting all Backups

```csharp
await SaveSystemAPI.DeleteBackups("my-identifier");
```

## Related

- [SaveSystemAPI](xref:Bayat.SaveSystem.SaveSystemAPI)