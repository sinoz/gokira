# GoKira

GoKira is your go-to cache library for OldSchool RuneScape, written in Go.

## Install

```
go get -u -v github.com/sinoz/gokira
```

## Supported Revisions

GoKira has been tested on the following revisions of OldSchool RuneScape:

- 149
- 177
- 178
- 187

## How To Use

Loading the cache is as easy as:

```
cache, err := gokira.LoadCache("cache/", 21)
```

If you are interested in the raw file data of the underlying file bundle, you can also do:

```
bundle, err := gokira.LoadFileBundle("cache/", 21)
if err != nil {
    log.Fatal(err)
}

cache, err := gokira.NewCache(bundle)
if err != nil {
    log.Fatal(err)
}
```

Developers who aren't very familiar with the cache might only want to use this library for streaming purposes in their server application. The game client expects to receive a collection of pages that together make up a categorized folder. To fetch such a folder (or the release manifest / update keys):

```
if archiveId == 255 && folderId == 255 {
    m, err := cache.getReleaseManifest()
    if err != nil {
        return nil, err
    }

    return m.Encode(), nil
}

return cache.getFolderPages(archiveId, folderId), nil
```

To learn more on how to use this library for your OldSchool RuneScape application, check out the examples directory.

## Extras

#### Supported Cryptographic/Compression Utilities

- XTEA (deciphering, enciphering)
- RSA (decrypting, encrypting)
- DJB2 (One-way hashing)
- GZIP (Decompression)
- BZIP2 (Decompression)

## FAQ

#### Why the name?

I was watching the anime Death Note and couldn't really think of anything else. I needed something so here we go. If you have any suggestions, feel free to make an issue or comment on an existing issue.

#### Does this also support applying cache modifications?

No. The focus of this library is to give developers a cache library to build (server) applications with. Additionally, the Go standard library currently, at the time of this writing, does not support Bzip2 encoding. Although Gzip can be used, perhaps one day.

#### Will this library also support RuneScape 3?

No.

## Giving Credits

- Sini for some of the namings
- Authors of OpenRS for illustrating the cache encoding format in their work
