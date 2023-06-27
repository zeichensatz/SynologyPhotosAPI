# SynologyPhotosAPI
I started to explore the Synology Photos API for my own project. This project is about integration of images from Synology Photos into my website directly by using API calls.
The informations here are by far not complete. It's just a start. Your commits/pull requests will highly be appreciated!

## Searching the Synology Photos app directories
There are some files in the directory `/volume1/@appstore/SynologyPhotos/usr/webapi`, which are an entry point to the Synology Photos API.
* SYNO.Foto.lib. [Here](API/SYNO.Foto.lib) is a formatted/readable version of the json file.
* SYNO.FotoTeam.lib [Here](API/SYNO.FotoTeam.lib) is a formatted/readable version of the json file.
BTW: The libraries for the Synology APIs are available in the directory `/usr/syno/synoman/webapi` of your DS.

## Synology File Station API Guide
The [Synology File Station API Guide](https://global.download.synology.com/download/Document/Software/DeveloperGuide/Package/FileStation/All/enu/Synology_File_Station_API_Guide.pdf) gives some basic informations, how to access the Synology API. Even though the explanations are limited to the use of the FileStation, this is a starting point, to explore the Synology Photos API.<br/>
Note: For exploring the Synology Photos API you should have installed this package of course. Otherwise the API will not be listed.

### Which APIs are available on your Synology?
You may either use the administration port `5001` or the path `/photo` to retrieve information about all available APIs. Just replace `<IP_ADDRESS>` with your Synology's address:

```
https://<IP_ADDRESS>:5001/webapi/query.cgi?api=SYNO.API.Info&version=1&method=query&query=all
```
```
https://<IP_ADDRESS>/photo/webapi/entry.cgi?api=SYNO.API.Info&version=1&method=query&query=all
```

`entry.cgi` and `query.cgi` can be used synonymously. Both will get the same result.

From the response you can see, that the part about the Synology Photos API lists the same APIs as we can find in the above mentioned files [SYNO.Foto.lib](API/SYNO.Foto.lib) and [SYNO.Fototeam.lib](API/SYNO.FotoTeam.lib):

```
...
"SYNO.Foto.BackgroundTask.File":{"maxVersion":1,"minVersion":1,"path":"entry.cgi","requestFormat":"JSON"},
"SYNO.Foto.BackgroundTask.Info":{"maxVersion":1,"minVersion":1,"path":"entry.cgi","requestFormat":"JSON"},
"SYNO.Foto.Browse.Album":{"maxVersion":1,"minVersion":1,"path":"entry.cgi","requestFormat":"JSON"},
"SYNO.Foto.Browse.Category":{"maxVersion":1,"minVersion":1,"path":"entry.cgi","requestFormat":"JSON"},
...
```

### Authentication
#### Login:
For many API calls you need to be authenticated first. You can achieve this by the SYNO.API.Auth as follows.<br/>
Just replace `<IP_ADDRESS>`, `<USER>` and `<PASSWORD>` with your data:

```
https://<IP_ADDRESS>/photo/webapi/auth.cgi?api=SYNO.API.Auth&version=3&method=login&account=<USER>&passwd=<PASSWORD>
```
Using the POST method with curl would work like follows:
```
curl -X POST --data 'api=SYNO.API.Auth&version=3&method=login&account=<USER>&passwd=<PASSWORD>' https://<IP_ADDRESS>/photo/webapi/auth.cgi
```
You will get the following response:
```json
{
   "data":{
      "did":"3ezTHmf9ekMNjM-nF8J3qI5VzsMXlJBjRcNHotIwzKTc3ju2YGB7y9IIvOPxHTSuvvZmVOxM7u7f57w7ndtmog",
      "sid":"k76NZ-C7inEyhENeX7Jfu7yB28Wk_wbWEszF2ZtHSB8dcW68WQYQbTvF0Oqo21zoQuitKmoFop-kSvJQGHG1oU"
   },
   "success":true
}
```
#### Logout:
In the browser it works as following:
```
https://<IP_ADDRESS>/photo/webapi/auth.cgi?api=SYNO.API.Auth&version=3&method=logout
```
With curl:
```
curl 'http://<IP_ADDRESS>/photo/webapi/auth.cgi?api=SYNO.API.Auth&version=3&method=logout'
```
Response should be:
```json
{
   "success":true
}
```

About authenticaton also see [DSM Login Web API Guide](https://global.download.synology.com/download/Document/Software/DeveloperGuide/Os/DSM/All/enu/DSM_Login_Web_API_Guide_enu.pdf).

### Synology Photos API
#### Structure

##### Difference between SYNO.Foto.* and SYNO.FotoTeam.*
`SYNO.Foto.*` offers access to all folders in the `Personal Space` in the `Photos` tab and to all `Albums` in the `Albums` tab.<br/>
`SYNO.FotoTeam.*` offers access to all folders in the `Shared Space`.

There are less APIs in SYNO.FotoTeam available. The APIs with similar names should be quite the same refering to their methods and responses.

##### Level of authentication for APIs
There are three levels of authentication for the APIs, see the `authLevel` in the files [SYNO.Foto.lib](API/SYNO.Foto.lib) and [SYNO.Fototeam.lib](API/SYNO.FotoTeam.lib).
`authLevel` can get the values 0, 1, 2.

| Value | Description |
| --- | --- | 
| 0 | No authentication needed. For display of general informations. | 
| 1 | Authentication needed | 
| 2 | No authentication needed. If authenticated accessible area might be different. | 

##### List of SYNO.Foto.* APIs

| API name | Description |
| --- | --- | 
| SYNO.Foto.BackgroundTask.File | | 
| SYNO.Foto.BackgroundTask.Info | | 
| SYNO.Foto.Browse.Album | Handle albums. Normal and condition(al) albums are listed. | 
| SYNO.Foto.Browse.Category | | 
| SYNO.Foto.Browse.ConditionAlbum | Handle only condition(al) albums. | 
| SYNO.Foto.Browse.Diff | | 
| SYNO.Foto.Browse.Folder | Handle only folders in the `Personal Space`. | 
| SYNO.Foto.Browse.GeneralTag | | 
| SYNO.Foto.Browse.Geocoding | | 
| SYNO.Foto.Browse.Item | Handle an item in the `Personal Space`. Example methods include `add_tag`, `copy`, `delete`, `get`, `get_exif`, `get_tag`, `list`, `move`, `rename`, `set` | 
| SYNO.Foto.Browse.NormalAlbum | Handle only normal albums. | 
| SYNO.Foto.Browse.Person | | 
| SYNO.Foto.Browse.RecentlyAdded | | 
| SYNO.Foto.Browse.Timeline | | 
| SYNO.Foto.Browse.Unit | | 
| SYNO.Foto.Download | Retrieve/download the original file. | 
| SYNO.Foto.Favorite | | 
| SYNO.Foto.Index | | 
| SYNO.Foto.Migration | | 
| SYNO.Foto.PublicSharing | Get all text strings for user interface (UI). | 
| SYNO.Foto.Search.Filter | List all available search filters. | 
| SYNO.Foto.Search.Search | Search album and items. | 
| SYNO.Foto.Setting.Admin | | 
| SYNO.Foto.Setting.Guest | Get settings for guests. | 
| SYNO.Foto.Setting.MobileCompatibility | | 
| SYNO.Foto.Setting.TeamSpace | | 
| SYNO.Foto.Setting.User | | 
| SYNO.Foto.Setting.Wizard | | 
| SYNO.Foto.Sharing.Misc | | 
| SYNO.Foto.Sharing.Passphrase | | 
| SYNO.Foto.Streaming | | 
| SYNO.Foto.Thumbnail | Get thumbnail(s). | 
| SYNO.Foto.Upload.Item | | 
| SYNO.Foto.UserInfo | | 

##### List of SYNO.FotoTeam.* APIs

| API name | Description |
| --- | --- | 
| SYNO.FotoTeam.BackgroundTask.File | | 
| SYNO.FotoTeam.Browse.Diff | | 
| SYNO.FotoTeam.Browse.Folder | Handle only folders in the `Shared Space`. | 
| SYNO.FotoTeam.Browse.GeneralTag | | 
| SYNO.FotoTeam.Browse.Geocoding | | 
| SYNO.FotoTeam.Browse.Item | Handle an item in the `Shared Space`. Example methods include `add_tag`, `copy`, `delete`, `get`, `get_exif`, `get_tag`, `list`, `move`, `rename`, `set` | 
| SYNO.FotoTeam.Browse.Person | | 
| SYNO.FotoTeam.Browse.RecentlyAdded | | 
| SYNO.FotoTeam.Browse.Timeline | | 
| SYNO.FotoTeam.Browse.Unit | | 
| SYNO.FotoTeam.Download | Retrieve/download the original file | 
| SYNO.FotoTeam.Favorite | | 
| SYNO.FotoTeam.Index | | 
| SYNO.FotoTeam.Search.Filter | List all available search filters. | 
| SYNO.FotoTeam.Search.Search | Search album and items. | 
| SYNO.FotoTeam.Sharing.Passphrase | | 
| SYNO.FotoTeam.Streaming | | 
| SYNO.FotoTeam.Thumbnail | Get thumbnail(s). | 
| SYNO.FotoTeam.Upload.Item | | 

In the directories [API/SYNO.Foto/](API/SYNO.Foto/) and [API/SYNO.FotoTeam/](API/SYNO.FotoTeam/) the descriptions for the APIs will be listed for every method. The files name pattern is `<name of API>.<name of method>.md`, i.e. `SYNO.Foto.Browse.Album.list.md` (API: SYNO.Foto.Browse.Album, method: list).

I only checked a few APIs, which I want to use for my application and I didn't check any available parameter for request and response.

Please let me know, if you want to participate in this documentation. I will add you to the contributors then.


## Access to public Shared Folders
### list content of directory `/photo`
The following call gets all folders in the directory `/volume1/photo` from the DS. If you are logged in, you will get a list of all folders, to which you are granted access. If you are not logged in, you will get a lists of all public shared folders.
```
https://<IP_ADDRESS>/photo/webapi/entry.cgi?api=SYNO.FotoTeam.Browse.Folder&version=1&method=list_parents
```
Response might look like following:
```json
{
   "data":{
      "list":[
         {
            "id":1,
            "name":"/",
            "owner_user_id":0,
            "parent":1,
            "passphrase":"Bo00JIHnO",
            "shared":true,
            "sort_by":"default",
            "sort_direction":"default"
         },
         {
            "id":153,
            "name":"/Mongolia",
            "owner_user_id":0,
            "parent":1,
            "passphrase":"CFGTXzTL1",
            "shared":true,
            "sort_by":"default",
            "sort_direction":"default"
         },
      ]
   },
   "success":true
}
```
### List subdirectories of a folder
To get a list of subfolders from a specific folder you have to use the method `list` instead of `list_parents` and add the `id` of a folder:
```
https://<IP_ADDRESS>/photo/webapi/entry.cgi?api=SYNO.FotoTeam.Browse.Folder&version=1&method=list&offset=0&limit=100&id=153
```
Response:
```json
{
   "data":{
      "list":[
         {
            "id":608,
            "name":"/Mongolia/20170730",
            "owner_user_id":0,
            "parent":153,
            "passphrase":"2C9P3NUtC",
            "shared":true,
            "sort_by":"default",
            "sort_direction":"default"
         },
...
         {
            "id":776,
            "name":"/Mongolia/20170805",
            "owner_user_id":0,
            "parent":153,
            "passphrase":"RTxSv1YXb",
            "shared":true,
            "sort_by":"default",
            "sort_direction":"default"
         },
      ]
   },
   "success":true
}
```
### List items in a folder
Now you can list all items in this folder as following:
```
https://<IP_ADDRESS>/photo/webapi/entry.cgi?api=SYNO.FotoTeam.Browse.Item&version=1&method=list&offset=0&limit=100&folder_id=608&additional=["thumbnail"]
```
Parameter `additional=["thumbnail"]` is added to get the value `cache_key` for every item. `cache_key` is needed for getting a specific item later.

Response:
```json
{
   "data":{
      "list":[
         {
            "additional":{
               "thumbnail":{
                  "cache_key":"40808_1633659236",
                  "m":"ready",
                  "preview":"broken",
                  "sm":"ready",
                  "unit_id":40808,
                  "xl":"ready"
               }
            },
            "filename":"IMG_20170730_205341_1.JPG",
            "filesize":1470363,
            "folder_id":608,
            "id":40808,
            "indexed_time":1633631344618,
            "owner_user_id":0,
            "time":1501448021,
            "type":"photo"
         },
...
         {
            "additional":{
               "thumbnail":{
                  "cache_key":"40798_1633659232",
                  "m":"ready",
                  "preview":"broken",
                  "sm":"ready",
                  "unit_id":40798,
                  "xl":"ready"
               }
            },
            "filename":"IMG_20170730_074551.JPG",
            "filesize":1867614,
            "folder_id":608,
            "id":40798,
            "indexed_time":1633631344380,
            "owner_user_id":0,
            "time":1501400751,
            "type":"photo"
         }
      ]
   },
   "success":true
}
```

### Get item
Following call will get the image into your browser:
```
https://<IP_ADDRESS>/photo/mo/sharing/webapi/entry.cgi?api=SYNO.FotoTeam.Thumbnail&method=get&version=1&id=40808&cache_key=40808_1633659236&type=unit&size=sm
```

## Access to Shared Albums
To access shared albums was a problem, I'm quite struggling with.
I want to access the thumbnails of photos in a shared album for loading them into my own web application.

```
https://<IP_ADDRESS>/photo/mo/sharing/EkPUCJLDI
```
This displays a shared album without having to be logged in (as long there's not a password set for this shared album).

These are the steps, how to get access on each file in a shared album:

### Getting a sharing_id
The only way to get a valid cookie I know at the moment, is by using curl to call the link for the shared album. `-c cookie` stores the cookie data into the file `cookie`.
```
curl -c cookie https://<IP_ADDRESS>/photo/mo/sharing/EkPUCJLDI
```
There should be another way via the AUTH.API.

### List items in a shared album
Now we can list the items of this album with the following curl command:
```
curl -b cookie -H "x-syno-sharing: EkPUCJLDI" -d 'additional=["thumbnail","resolution","orientation","video_convert","video_meta","provider_user_id"]&offset=0&limit=4&sort_by="takentime"&sort_direction="asc"&passphrase="EkPUCJLDI"&api=SYNO.Foto.Browse.Item&method=list&version=1' https://<IP_ADDRESS>/photo/mo/sharing/webapi/entry.cgi
```
or directly in the browser:
```
https://<IP_ADDRESS>/photo/mo/sharing/webapi/entry.cgi?additional=["thumbnail","resolution","orientation","video_convert","video_meta","provider_user_id"]&offset=0&limit=4&sort_by="takentime"&sort_direction="asc"&passphrase="EkPUCJLDI"&api=SYNO.Foto.Browse.Item&method=list&version=1
```

With `-b cookie` the content of the file `cookie` will be sent. 
Besides of the cookie, we also need to add the `x-syno-sharing: EkPUCJLDI` to the header.

Of course the cookie could be given to the header this way too:
```
curl -H "cookie: sharing_sid=Kr5KTYIJn11M0c-h0UN3366oIaE5l-BX" -H "x-syno-sharing: EkPUCJLDI" -d 'additional=["thumbnail","resolution","orientation","video_convert","video_meta","provider_user_id"]&offset=0&limit=4&sort_by="takentime"&sort_direction="asc"&passphrase="EkPUCJLDI"&api=SYNO.Foto.Browse.Item&method=list&version=1' https://<IP_ADDRESS>/photo/mo/sharing/webapi/entry.cgi
```

The response might look as follows:
```json
{
   "data":{
      "list":[
         {
            "additional":{
               "orientation":6,
               "orientation_original":6,
               "provider_user_id":2,
               "resolution":{
                  "height":4032,
                  "width":3024
               },
               "thumbnail":{
                  "cache_key":"25758_1633653387",
                  "m":"ready",
                  "preview":"broken",
                  "sm":"ready",
                  "unit_id":25758,
                  "xl":"ready"
               }
            },
            "filename":"IMG_20210911_190642.JPG",
            "filesize":3098406,
            "folder_id":1438,
            "id":25758,
            "indexed_time":1633630824030,
            "live_type":"photo",
            "owner_user_id":0,
            "time":1631387203,
            "type":"live"
         },
         {
            "additional":{
               "orientation":1,
               "orientation_original":1,
               "provider_user_id":2,
               "resolution":{
                  "height":3024,
                  "width":4032
               },
               "thumbnail":{
                  "cache_key":"25752_1633653385",
                  "m":"ready",
                  "preview":"broken",
                  "sm":"ready",
                  "unit_id":25752,
                  "xl":"ready"
               }
            },
            "filename":"IMG_20210912_144022.JPG",
            "filesize":3006194,
            "folder_id":1437,
            "id":25752,
            "indexed_time":1633630823784,
            "live_type":"photo",
            "owner_user_id":0,
            "time":1631457623,
            "type":"live"
         },
         {
            "additional":{
               "orientation":1,
               "orientation_original":1,
               "provider_user_id":2,
               "resolution":{
                  "height":1536,
                  "width":2048
               },
               "thumbnail":{
                  "cache_key":"25757_1633653387",
                  "m":"ready",
                  "preview":"broken",
                  "sm":"ready",
                  "unit_id":25757,
                  "xl":"ready"
               }
            },
            "filename":"IMG_20210911_182919.jpg",
            "filesize":188232,
            "folder_id":1438,
            "id":25757,
            "indexed_time":1633630823000,
            "owner_user_id":0,
            "time":1631815585,
            "type":"photo"
         }
      ]
   },
   "success":true
}
```
### Get thumbnail for each item
Now you can get the thumbnail of each image:
```
curl -k -b cookie 'https://<IP_ADDRESS>/photo/mo/sharing/webapi/entry.cgi?id=25752&cache_key="25752_1633653385"&type="unit"&size="sm"&passphrase="EkPUCJLDI"&api="SYNO.Foto.Thumbnail"&method="get"&version=1&_sharing_id="EkPUCJLDI"'
```
As you see, the cookie is still needed.
The parameter `passphrase="EkPUCJLDI"` is not needed.

### The problem:
Getting a thumbnail this way with curl on the html server for the website doesn't help. The thumbnail can't be used as a reference to the image in html because the cookie we get on the webserver with curl limits it's use to the server and not to the browser of someone calling the website.
Therefore another solution has to be found.

#### Javascript Solution

When fetching photo data from the  API, each photo object includes an `additional` object which contains a `thumbnail` object. This `thumbnail` object includes a `cache_key` field. The `cache_key` is a unique identifier for the photo's thumbnail image.

When generating a URL to access the thumbnail image, you can include the `cache_key` as a parameter along with the `sid` in the URL. This allows you to bypass the session-based restrictions that would normally prevent the thumbnail image from being accessed outside of the original session in which it was requested.

Here's an example of how to fetch photo data and generate a thumbnail URL:

```javascript
async function fetchPhotos(sid) {
  const photosResponse = await fetch(
    `https://${ip}/photo/webapi/entry.cgi?api=SYNO.Foto.Browse.Item&version=1&method=list&type=photo&offset=0&limit=5000&_sid=${sid}&additional=["thumbnail"]`
  )
  const photosData = await photosResponse.json()
  return photosData.data.list[0] //just return the first photo as an example
}
```
That will return an object that looks like this:

```JSON
{
  id: 7713,
  filename: 'IMG_20230625_095440.jpg',
  filesize: 7231588,
  time: 1687686880,
  indexed_time: 1687683302513,
  owner_user_id: 1,
  folder_id: 242,
  type: 'photo',
  additional: {
    thumbnail: {
      m: 'ready',
      xl: 'ready',
      preview: 'broken',
      sm: 'ready',
      cache_key: '7713_1687701308',
      unit_id: 7713
    }
  }
}
```

The `cache_key` can then used as a parameter to access the web url of the photo


```javascript
function getThumbnailUrl(ip, sid, photo) {
  const {
    id,
    additional: {
      thumbnail: { cache_key }
    }
  } = photo
  return `https://${ip}/webapi/entry.cgi?api=SYNO.Foto.Thumbnail&version=1&method=get&mode=download&id=${id}&type=unit&size=xl&cache_key=${cache_key}&_sid=${sid}`
}
```

Note that the `cache_key` is specific to each photo and its corresponding thumbnail image. It cannot be used to access other photos or their thumbnails.


It seems that this approach allows you to circumvent the issue of needing a cookie by using the `cache_key` and `sid` for authentication. By including them as params, you're able to access the thumbnails directly, even in a new, cookie-less session/incognito window. 

---

### How to get size (height/width) of photos and thumbnails
With help of the Synology Photos API one can only get informations about the size of the original photo, not about the size of the thumbnails. You can only get general information about the thumbnails: availability and a general size. Sizes can have the values `sm`, `m` and `xl`.
As far as I checked the thumbnail sizes, they are calculated as follows:

| size | width | height | calculation
| --- | --- | --- | --- |
| original | 2448 | 3264 | --- |
| sm | <b>240</b> | 320 | 3264/2448*<b>240</b>=319,99999999 |
| m | <b>320</b> | 427 | 3264/2448*<b>320</b>=426,66666666 |
| xl | <b>1280</b> | 1707 | 3264/2448*<b>1280</b>=1706,6666666 |

Values for this file:
```
https://<IP_ADDRESS>/photo/mo/sharing/webapi/entry.cgi?api=SYNO.FotoTeam.Thumbnail&method=get&version=1&id=40808&cache_key=40808_1633659236&type=unit&size=<THUMBNAIL-SIZE>
```
The file in original resolution can be retrieved as following:
```
https://<IP_ADDRESS>/photo/webapi/entry.cgi?cache_key="40808_1633659236"&unit_id=[40808]&api="SYNO.FotoTeam.Download"&method="download"&version=1
```

| size | width | height | calculation
| --- | --- | --- | --- |
| original | 6000 | 4000 | --- |
| sm | 360 | <b>240</b> | 6000/4000*<b>240</b>=360 |
| m | 480 | <b>320</b> | 6000/4000*<b>320</b>=480 |
| xl | 1920 | <b>1280</b> | 6000/4000*<b>1280</b>=1920 |

Values for this file (this file is in the personal space. One has to be logged in before as explained above. Or when logged in from SynologyPhotos one needs to add the valid SynoToken!):
```
https://<IP_ADDRESS>/photo/mo/sharing/webapi/entry.cgi?api=SYNO.Foto.Thumbnail&method=get&version=1&id=80719&cache_key=80719_1633863542&type=unit&size=<THUMBNAIL-SIZE>&SynoToken=pSAYNF9UTBZQA
```
The file in original resolution can be retrieved (this file is in the personal space. One has to be logged in before as explained above. Or when logged in from SynologyPhotos one needs to add the valid SynoToken!) as following:
```
https://<IP_ADDRESS>/photo/webapi/entry.cgi?cache_key="80719_1633863542"&unit_id=[80719]&api=SYNO.Foto.Download&method=download&version=1&SynoToken=pSAYNF9UTBZQA
```

The thumbnails are calculated on the lower value of both sides for every size. The value for each size is:
| size | value |
| --- | --- |
| sm | 240 |
| m | 320 |
| xl | 1280 |

I didn't systematically check yet, what will happen, if the original size is smaller than a thumbnail minimum size. Most probably the thumbnail will not be generated in this case.

So size calculation can be done as following:
* get srcHeight (from additional.resolution.height) and srcWidth (from additional.resolution.width) of original file
* if srcHeight > scrWidth then 
  * xSM/xM/xXL = 240/320/1280
  * srcWidth DIV srcHeight * 240/320/1280 = ySM/yM/yXL
* else
  * ySM/yM/yXL = 240/320/1280
  * csrcHeight DIV srcWidth * 240/320/1280 = xSM/xM/xXL
