# SYNO.Foto.Browse.Item
## method: list
Authlevel: 1<br/>
This means, you have to be authenticated first.
### Description:
List all items in all folders in `Personal Space`.
### Request:

| Parameter | Description | Value | Default Value |
| --- | --- | --- | --- |
| offset | Required. Specify how many shared folders are skipped before beginning to return listed shared folders. | Integer | 0 |
| limit | Required. Number of shared folders requested. 0 lists all shared folders. | Integer | 0 |
| folder_id | Optional. ID of folder | Integer | |
| sort_by | Optional.<br/>Only working, when `folder_id` is given.<br/>Specify which file information to sort on. <br>Options include: <br/><b>filename:</b> file name. <br/><b>filesize:</b> file size. | filename, filesize | filename |
| sort_direction | Optional.<br/>Only working, when `folder_id` is given.<br/>Specify to sort ascending or to sort descending.<br/>Options include: <br/><b>asc:</b> sort ascending. <br/><b>desc:</b> sort descending. | asc or desc | desc |
| type | Type of data<br/><b>photo:</b> Photo<br/><b>video:</b> Video<br/><b>live:</b> iPhone live photos | String |
| passphrase | Passphrase for a shared album, i.e. `xXHXZxIov`. Only items of this album will be listed. | String | |
| additional | Get additional informations about an item.<br/><b>thumbnail:</b> Available thumbnail sizes. Values can be `sm`, `m`, `xl`.<br/><b>resolution:</b> returns `height` and `width` of original photo<br/><b>orientation:</b> Orientation of file. Value seems to be integer.<br/><b>video_convert:</b> ???<br/><b>video_meta:</b> ???<br/><b>provider_user_id:</b> ???<br><b>exif:</b> Returns keys as `aperture`, `camera`, `exposure_time"`, `focal_length`, `iso`, `lens`.</br><b>tag:</b> Returns keys `id` and `name` for every tag.</br><b>description:</b> Returns exif description.</br><b>gps:</b> Coordinates returned as values `latitude` and `longitude`.</br><b>geocoding_id:</b> Geocoding id for internal database ???</br><b>address:</b> Address calculated from gps coordinates.</br><b>person:</b> Returns person object.<br/>Example: `&additional["thumbnail","resolution"]` | String ||

### Example:
```
https://<IP_ADDRESS>/photo/webapi/entry.cgi?api=SYNO.Foto.Browse.Item&version=1&method=list&offset=0&limit=100&folder_id=1989&additional=["thumbnail","resolution","orientation","video_convert","video_meta","provider_user_id","exif","tag","description","gps","geocoding_id","address","person"]
```

### Response:
`<data>` object definitions:

| Parameter | Type | Description |
| --- | --- | --- |
| filename | String | Name of file |
| filesize | Integer | Size of file |
| folder_id | Integer | ID of folder |
| id | Integer | ID of file |
| indexed_time | Linux timestamp in second | Timestamp of indexing the file |
| live_type | String | i.e.: photo (in case of iPhone live photos) |
| owner_user_id | Integer | UID of owner |
| time | Linux timestamp in second | Timestamp of file creation |
| type | String | Type of data<br/><b>photo:</b> Photo<br/><b>video:</b> Video<br/><b>live:</b> iPhone live photos |

`<additional>` object definitions:
| Parameter | Type | Description |
| --- | --- | --- |
| orientation | Integer | ??? |
| orientation_original | Integer | ??? |
| resolution | object with keys `height` and `width` as Integer | Height and width of original photo |
| thumbnail | object with keys `cache_key`, `preview`, `sm`, `m`, `xl` | Returns available thumbnail data of photo |
| video_convert | | ??? | 
| video_meta | | ??? | 
| provider_user_id | | ??? | 
| exif | Returns keys as `aperture`, `camera`, `exposure_time"`, `focal_length`, `iso`, `lens`. | Exif data | 
| tag | Returns object(s) with keys `id` and `name` | | 
| description | String | Exif description | 
| gps | Returns object with keys `latitude` and `longitude`. | GPS coordinates | 
| geocoding_id | Integer | For internal database ??? | 
| address | Returns object with keys `city`, `city_id`, `country`, `country_id`, `county`, `county_id`, `district`, `district_id`, `landmark`, `landmark_id`, `route`, `route_id`, `state`, `state_id`, `town`, `town_id`, `village`, `village_id | Address calculated from gps coordinates. | 
| person | Returns person object(s) | Information about tagged person(s). | 

### Example:
```
{
   "data":{
      "list":[
         {
            "additional":{
               "orientation":1,
               "orientation_original":1,
               "resolution":{
                  "height":4000,
                  "width":6000
               },
               "thumbnail":{
                  "cache_key":"80716_1633859830",
                  "m":"ready",
                  "preview":"broken",
                  "sm":"ready",
                  "unit_id":80716,
                  "xl":"ready"
               }
            },
            "filename":"IMG_20210723_201314.JPG",
            "filesize":13078975,
            "folder_id":1989,
            "id":80716,
            "indexed_time":1633867030761,
            "owner_user_id":2,
            "time":1627071194,
            "type":"photo"
         },
         {
            "additional":{
               "orientation":1,
               "orientation_original":1,
               "resolution":{
                  "height":4000,
                  "width":6000
               },
               "thumbnail":{
                  "cache_key":"80715_1633859830",
                  "m":"ready",
                  "preview":"broken",
                  "sm":"ready",
                  "unit_id":80715,
                  "xl":"ready"
               }
            },
            "filename":"IMG_20210723_201307.JPG",
            "filesize":14224627,
            "folder_id":1989,
            "id":80715,
            "indexed_time":1633867030229,
            "owner_user_id":2,
            "time":1627071187,
            "type":"photo"
         },
...
         {
            "filename":"IMG_20210918_154606.MOV",
            "filesize":40551327,
            "folder_id":1990,
            "id":80759,
            "indexed_time":1633870760297,
            "owner_user_id":2,
            "time":1631979966,
            "type":"video"
         },
...
         {
            "additional":{
               "orientation":1,
               "orientation_original":1,
               "resolution":{
                  "height":4000,
                  "width":6000
               },
               "thumbnail":{
                  "cache_key":"80714_1633859830",
                  "m":"ready",
                  "preview":"broken",
                  "sm":"ready",
                  "unit_id":80714,
                  "xl":"ready"
               }
            },
            "filename":"IMG_20210723_193530.JPG",
            "filesize":12873598,
            "folder_id":1989,
            "id":80714,
            "indexed_time":1633867029955,
            "owner_user_id":2,
            "time":1627068930,
            "type":"photo"
         }
      ]
   },
   "success":true
}
```
