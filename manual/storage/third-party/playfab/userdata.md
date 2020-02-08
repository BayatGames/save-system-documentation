# PlayFab UserData

The PlayFab UserData implementation.

- [Download **PlayFab Integration**](../../../../packages/playfab.unitypackage)
- [Player Data](https://docs.microsoft.com/en-us/gaming/playfab/features/data/playerdata/)
- [Player data quickstart (UserData)](https://docs.microsoft.com/en-us/gaming/playfab/features/data/playerdata/quickstart)

## Syntax

```
playfab-userdata://encoding=<String>;usebase64=<Boolean>
```

## Parameters

| Name        | Type   | Description                                       | Alias                        |
|-------------|--------|---------------------------------------------------|------------------------------|
| encoding    | string | The text encoding                                 | text-encoding, encoding-name |
| usebase64   | bool   | Whether to use base64 encoding for storage or not | use-base64                   |
| entity-id   | string | The PlayFab entity ID                             | entityid                     |
| entity-type | string | The PlayFab entity type                           |                              |