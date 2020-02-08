# Storage

A storage implementation provides methods for accessing and applying operations on the storage through a Unified API.

There are a few built-in storage implementations such as:

- File
- PlayerPrefs

Which are good inspirations for implementing your own storage on top of them.

Also, the Storage API uses the async syntax so you can implement Online / Cloud storages too easily.

So here we have the PlayerPrefs storage implementation:

```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using System.IO;
using System.Text;
using System.Threading.Tasks;
using UnityEngine;

namespace Bayat.SaveSystem.Storage
{

    /// <summary>
    /// PlayerPrefs storage implementation.
    /// </summary>
    public class PlayerPrefsStorage : StorageBase
    {

        protected bool useBase64 = true;

        public PlayerPrefsStorage(string encodingName, bool useBase64) : base(encodingName)
        {
            this.useBase64 = useBase64;
        }

        public override Task<IStorageStream> GetWriteStream(string identifier)
        {
            PlayerPrefsStorageStream storageStream = new PlayerPrefsStorageStream(identifier, new MemoryStream());
            return Task.FromResult<IStorageStream>(storageStream);
        }

        protected override Task CommitWriteStreamInternal(IStorageStream stream)
        {
            PlayerPrefsStorageStream memoryStream = (PlayerPrefsStorageStream)stream;
            string data = null;
            if (useBase64)
            {
                data = Convert.ToBase64String(((MemoryStream)memoryStream.UnderlyingStream).ToArray());
            }
            else
            {
                this.TextEncoding.GetString(((MemoryStream)memoryStream.UnderlyingStream).ToArray());
            }
            PlayerPrefs.SetString(memoryStream.Identifier, data);
            return Task.CompletedTask;
        }

        public override Task<IStorageStream> GetReadStream(string identifier)
        {
            MemoryStream memoryStream = null;
            if (useBase64)
            {
                memoryStream = new MemoryStream(Convert.FromBase64String(PlayerPrefs.GetString(identifier)));
            }
            else
            {
                memoryStream = new MemoryStream(this.TextEncoding.GetBytes(PlayerPrefs.GetString(identifier)));
            }
            PlayerPrefsStorageStream storageStream = new PlayerPrefsStorageStream(identifier, memoryStream);
            return Task.FromResult<IStorageStream>(storageStream);
        }

        protected override Task WriteAllTextInternal(string identifier, string data)
        {
            PlayerPrefs.SetString(identifier, data);
            return Task.CompletedTask;
        }

        public override Task<string> ReadAllText(string identifier)
        {
            return Task.FromResult(PlayerPrefs.GetString(identifier));
        }

        protected override Task WriteAllBytesInternal(string identifier, byte[] data)
        {
            PlayerPrefs.SetString(identifier, Convert.ToBase64String(data));
            return Task.CompletedTask;
        }

        public override Task<byte[]> ReadAllBytes(string identifier)
        {
            return Task.FromResult(Convert.FromBase64String(PlayerPrefs.GetString(identifier)));
        }

        public override async Task<StorageClearOperationResult> Clear()
        {
            bool result = true;
            List<string> catalog = await LoadCatalog();
            foreach (string identifier in catalog)
            {
                result &= (await Delete(identifier)).Succeed;
            }
            return new StorageClearOperationResult(result, catalog.ToArray());
        }

        protected override Task<StorageDeleteOperationResult> DeleteInternal(string identifier)
        {
            bool result = false;
            if (PlayerPrefs.HasKey(identifier))
            {
                PlayerPrefs.DeleteKey(identifier);
                result = true;
            }
            return Task.FromResult(new StorageDeleteOperationResult(result));
        }

        public override Task<bool> Exists(string identifier)
        {
            return Task.FromResult(PlayerPrefs.HasKey(identifier));
        }

        protected override async Task<StorageMoveOperationResult> MoveInternal(string oldIdentifier, string newIdentifier, bool replace)
        {
            bool result = false;
            if (PlayerPrefs.HasKey(oldIdentifier))
            {
                if (replace || !PlayerPrefs.HasKey(newIdentifier))
                {
                    PlayerPrefs.SetString(newIdentifier, PlayerPrefs.GetString(oldIdentifier));
                    await Delete(oldIdentifier);
                    result = true;
                }
            }
            return new StorageMoveOperationResult(result, newIdentifier);
        }

        protected override Task<StorageCopyOperationResult> CopyInternal(string fromIdentifier, string toIdentifier, bool replace)
        {
            bool result = false;
            if (PlayerPrefs.HasKey(fromIdentifier))
            {
                if (replace || !PlayerPrefs.HasKey(toIdentifier))
                {
                    PlayerPrefs.SetString(toIdentifier, PlayerPrefs.GetString(fromIdentifier));
                    result = true;
                }
            }
            return Task.FromResult(new StorageCopyOperationResult(result, toIdentifier));
        }

        public override async Task<string[]> List(string identifier, StorageListOptions options)
        {
            List<string> items = await LoadCatalog();
            if (options.MaxResults.HasValue)
            {
                items.Capacity = options.MaxResults.GetValueOrDefault();
            }
            return items.FindAll(item => item.Contains(identifier)).ToArray();
        }

        public override async Task<string[]> ListAll()
        {
            return (await LoadCatalog()).ToArray();
        }

    }

    /// <summary>
    /// The PlayerPrefs storage stream wrapper.
    /// </summary>
    public class PlayerPrefsStorageStream : StorageStream
    {

        public PlayerPrefsStorageStream(string identifier, Stream stream) : base(identifier, stream)
        {
        }

    }

}
```

Now this requires a connection string factory in order to initialize it through a connection string, instead of instantiating the class directly, so lets do it by implementing the [`IConnectionFactory`](xref:Bayat.SaveSystem.Storage.IConnectionFactory) interface:

```csharp
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

namespace Bayat.SaveSystem.Storage
{

    /// <summary>
    /// The built-in connection factory.
    /// </summary>
    public class BuiltInConnectionFactory : IConnectionFactory
    {

        public IStorage CreateStorage(StorageConnectionString connectionString)
        {
            if (connectionString.Prefix == "disk")
            {
                //connectionString.GetRequired("path", true, out string path, "base-path", "folder", "directory", "dir");
                string path = connectionString.Get("path", Application.persistentDataPath, "base-path", "folder", "directory", "dir");

                return new LocalDiskStorage(path);
            }

            if (connectionString.Prefix == "playerprefs")
            {
                string encodingName = connectionString.Get("encoding", StorageBase.DefaultTextEncodingName, "text-encoding", "encoding-name");
                bool useBase64 = connectionString.GetBoolean("usebase64", true, "use-base64");

                return new PlayerPrefsStorage(encodingName, useBase64);
            }

            return null;
        }

    }

}
```

The [`CreateStorage`](xref:Bayat.SaveSystem.Storage.IConnectionFactory.CreateStorage(Bayat.SaveSystem.Storage.StorageConnectionString)) method is called automatically by the main connection string factory.

Now when we use `playerprefs://`, it will initialize the PlayerPrefs storage.