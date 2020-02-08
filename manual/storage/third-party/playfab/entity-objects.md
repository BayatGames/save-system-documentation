# PlayFab Entity Objects

The PlayFab entity objects implementation.

- [Download **PlayFab Integration**](../../../../packages/playfab.unitypackage)
- [Player Data](https://docs.microsoft.com/en-us/gaming/playfab/features/data/playerdata/)
- [Entity Programming Model](https://docs.microsoft.com/en-us/gaming/playfab/features/data/entities/index)
- [Entities quickstart](https://docs.microsoft.com/en-us/gaming/playfab/features/data/entities/quickstart)

## Syntax

```
playfab-entity://entity-id=<String>;entity-type=<String>;encoding=<String>;usebase64=<Boolean>
```

## Parameters

| Name        | Type   | Description                                       | Alias                        |
|-------------|--------|---------------------------------------------------|------------------------------|
| encoding    | string | The text encoding                                 | text-encoding, encoding-name |
| usebase64   | bool   | Whether to use base64 encoding for storage or not | use-base64                   |
| entity-id   | string | The PlayFab entity ID                             | entityid                     |
| entity-type | string | The PlayFab entity type                           |                              |