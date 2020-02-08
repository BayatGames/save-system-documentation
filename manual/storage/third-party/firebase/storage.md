# Firebase Cloud Storage

The Firebase Cloud storage implementation.

- [Download **Firebase Cloud Storage Integration**](../../../../packages/firebase-cloud-storage.unitypackage)
- [Get Started with Cloud Storage for Unity](https://firebase.google.com/docs/storage/unity/start)
- [Cloud Storage (Documentation page)](https://firebase.google.com/docs/storage)
- [Cloud Storage (Product page)](https://firebase.google.com/products/storage)

## Syntax

```
firebase-cloud-storage://encoding=<String>;usebase64=<Boolean>;storage=<String>;reference=<String>;reference-url=<String>
```

## Parameters

| Name          | Type   | Description                                       | Alias                         |
|---------------|--------|---------------------------------------------------|-------------------------------|
| encoding      | string | The text encoding                                 | text-encoding, encoding-name  |
| usebase64     | bool   | Whether to use base64 encoding for storage or not | use-base64                    |
| storage       | string | The Firebase cloud storage URL                    | storage-url, storage-instance |
| reference     | string | The Firebase cloud storage reference path         | storage-reference             |
| reference-url | string | The Firebase cloud storage reference URL          | storage-reference-url         |