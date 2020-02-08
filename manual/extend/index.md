# Extending the System

The save system is meant to be modular, flexiblie and extendsible at its most on every aspect, such as Storage API, Encryption API, Serialization API, ...
Follow the below instructions for creating or extending the system for implementing your own feature or adding your own requirements to the system.

## Storage

You can extend or create your own storage by extending the [`StorageBase`](xref:Bayat.SaveSystem.Storage.StorageBase) class, for more information take a look at How to Create Custom Storage.

[Learn more](storage.md)

## Encryption

You can extend or create your own encryption by implementing the [`ISaveSystemEncryption`](xref:Bayat.SaveSystem.Security.ISaveSystemEncryption) interface, for more information take a look at How to Create Custom Encryption Algorithm

[Learn more](encryption.md)

## Converter

You can customize the serialization of objects by using the Converters to implement your own process, you can do it by extending the [`ObjectJsonConverter`](xref:Bayat.Json.Converters.ObjectJsonConverter) or [`JsonConverter`](xref:Bayat.Json.JsonConverter).

[Learm more](converter.md)

