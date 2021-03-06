## API Description

- All APIs are directly send to the backend of Private Cloud Music. For example, `api.php` on your server. and all APIs are using **POST** method. 

- Use `do` parameter to specify what data is requested. and use other additional parameter accroding to your `do` parameter.

- Always return a **json** to process. Contains a http `status` code node, a `message` node. and the most important `result` node.

- `result` node only avaliable if the request is legal. Contains the data content `type` and the main `data` content.

------------------------------------------------------------------

## API Spec

### Get folder list API:

* POST:
	+ 'do' = "getfolders"

* RETURN:
	+ json with the following struct.

``` json
{
	"status": 200,
	"message": "OK",
	"result":{
		"type": "folderList",
		"data": [
			"Folder1", "Folder2", "Folder3"
		]
	}
}
```

### Get file list of given folder name.

* POST:
	+ 'do' = "getplaylist"
	+ 'folder' = folder name

* RETURN:
	json with the following struct. (if folder exist)
	
``` json
{
	"status": 200,
	"message": "OK",
	"result":{
		"type": "fileList",
		"data": [
			{
				"fileName": "FileName.mp3",
				"fileSize": 123123123,
				"modifiedTime": "1313065072"
			},
			{
				"fileName": "FileName2.wav",
				"fileSize": 123123123,
				"modifiedTime": "1313065072"
			}
		]
	}
}
```

### If anything wrong.

* RETURN:
	+ json with HTTP status code and error message.

``` json
{
	"status": 400,
	"message": "illegal request!",
}
```

------------------------------------------------------------------

## Example

We assume your Private Cloud Music backend can be access at url `http://foo.bar/baz/api.php` and we use `wget` for the following example.

### Get folder list API:

``` bash
	wget --post-data "do=getfolders" http://foo.bar/baz/api.php
```

This will get the folder list since we **post** a `do` parameter to the backend and the value is `getfolders`.

### Get file list of given folder name.

``` bash
	wget --post-data "do=getplaylist&folder=Folder1" http://foo.bar/baz/api.php
```

If `Folder1` exist, this will get the audio file list inside the folder named `Folder1`. Since `do` parameter value is `getplaylist`. If that folder doesn't exist, will get an error contains the http status code and the error message.