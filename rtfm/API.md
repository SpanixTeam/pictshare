# API

# upload.php

- URL https://pictshare.net/api/upload.php
- Method: POST file
- Post var name: file
- Answer type: JSON

If the upload was successful answer will look like this

```json
{
    "status":"ok",
    "hash":"y1b6hr.jpg",
    "url":"https://pictshare.net/y1b6hr.jpg"
}
```

If there is an error the server will answer with status:err and a reason

```json
{
    "status":"err",
    "reason":"Unsupported filetype"
}
```

### Examples

1. Uploading a file called test.jpg via curl

```curl -F "file=@test.jpg" https://pictshare.net/api/upload.php```

Answer from the server:
```json
{"status":"ok","hash":"y1b6hr.jpg","url":"https://pictshare.net/y1b6hr.jpg"}
```

# geturl.php

- URL https://pictshare.net/api/geturl.php
- Method: GET
- Var name: url
- Answer type: JSON

Upload content by providing a link to the content. If the link points to a website, the HTML of the page is uploaded as a text bin.

```json
{
    "status":"ok",
    "hash":"y1b6hr.jpg",
    "url":"https://pictshare.net/y1b6hr.jpg",
    "delete_code": "aqxqlv3kqokxd15xpkqp8zjljpqerveu",
    "delete_url":   "https://pictshare.net/delete_aqxqlv3kqokxd15xpkqp8zjljpqerveu/2mr2va.txt"
}
```

If there is an error the server will answer with status:err and a reason

```json
{
    "status":"err",
    "reason":"Unsupported filetype"
}
```

### Examples

1. Uploading the HTML of xkcd.com

```curl -s https://pictshare.net/api/geturl.php?url=https://xkcd.com```

Answer from the server:
```json
{
  "status": "ok",
  "hash": "2mr2va.txt",
  "url": "https://pictshare.net/2mr2va.txt",
  "filetype": "text",
  "delete_code": "aqxqlv3kqokxd15xpkqp8zjljpqerveu",
  "delete_url": "https://pictshare.net/delete_aqxqlv3kqokxd15xpkqp8zjljpqerveu/2mr2va.txt"
}
```

2. Uploading a Video from Imgur

```curl https://pictshare.net/api/geturl.php?url=https://i.imgur.com/qQstLQt.mp4```

Answer from the server:

```json
{
  "status": "ok",
  "hash": "u0ni1m.mp4",
  "url": "https://pictshare.net/u0ni1m.mp4",
  "filetype": "mp4",
  "delete_code": "aqxqlv3kqokxd15xpkqp8zjljpqerveu",
  "delete_url": "https://pictshare.net/delete_aqxqlv3kqokxd15xpkqp8zjljpqerveu/u0ni1m.mp4"
}
```

---

# pasetebin.php
- URL https://pictshare.net/api/pastebin.php
- Method: POST/GET text
- Post var name: api_paste_code
- Answer: Plaintext URL to pasted bin

This API can be used to directly post text. Server responds with the URL to the bin or with an error message

### Example

Creating a new text bin that ready "Hello World"

```curl -F "api_paste_code=Hello World" https://pictshare.net/api/pastebin.php```

Answer from the server:
```https://pictshare.net/vekjy4e5rr.txt```

# info.php
- URL https://pictshare.net/api/info.php
- Method: POST/GET text
- Query var name: hash
- Answer: JSON

This API will get information about any given hash.

## Example

```curl https://pictshare.net/api/info.php?hash=9k3rbw.mp4```

Answer from the server:

```json
{
  "status": "ok",
  "hash": "9k3rbw.mp4",
  "size_bytes": 2513225,
  "size_interpreted": "2.4 MB",
  "type": "video/mp4",
  "type_interpreted": "mp4"
}
```