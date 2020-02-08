# File Storage

The local disk file storage implementation.

- [File and Stream I/O](https://docs.microsoft.com/en-us/dotnet/standard/io/)

## Syntax

```
disk://path=<String>
```

## Parameters

| Name | Type   | Description                                                                                          | Alias                             |
|------|--------|------------------------------------------------------------------------------------------------------|-----------------------------------|
| path | string | The base path to apply the storage operations on, the default path is Application.persistentDataPath | folder, dir, directory, base-path |