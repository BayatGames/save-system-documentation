# Firebase Realtime Database

The Firebase Realtime Database implementation.

- [Download **Firebase Realtime Database Integration**](../../../../packages/firebase-realtime-database.unitypackage)
- [Get Started with Realtime Database for Unity](https://firebase.google.com/docs/database/unity/start)
- [Realtime Database (Documentation page)](https://firebase.google.com/docs/database)
- [Realtime Database (Product page)](https://firebase.google.com/products/database)

## Syntax

```
firebase-database://encoding=<String>;usebase64=<Boolean>;storage=<String>;reference=<String>;reference-url=<String>
```

## Parameters

| Name          | Type   | Description                                       | Alias                           |
|---------------|--------|---------------------------------------------------|---------------------------------|
| encoding      | string | The text encoding                                 | text-encoding, encoding-name    |
| usebase64     | bool   | Whether to use base64 encoding for storage or not | use-base64                      |
| database      | string | The Firebase Realtime Database URL                | database-url, database-instance |
| reference     | string | The Firebase Realtime Database reference path     | database-reference              |
| reference-url | string | The Firebase Realtime Database reference URL      | database-reference-url          |