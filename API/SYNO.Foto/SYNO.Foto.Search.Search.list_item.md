# SYNO.Foto.Search.Search
## method: list_item
Authlevel: 1<br/>
This means, you have to be authenticated first.
### Description:
List items for a keyword.
### Request:

| Parameter | Description | Value | Default Value |
| --- | --- | --- | --- |
| offset | Required. Specify how many items are skipped before beginning to return | Integer | 0 |
| limit | Required. Number of items requested. 0 lists all items. | Integer | 0 |
| keyword | Keyword to search for | String | |
| timeline_group_unit | Parameter to group results, one of "day", ... ??? | String | day |
| additional | ??? | List of String | ["thumbnail","resolution","orientation","video_convert","video_meta","address"] |
| start_time | start timestamp to limit results | Integer |  |
| end_time | end timestamp to limit results | Integer |  |

### Example:
```
https://<IP_ADDRESS>/photo/webapi/entry.cgi?api=SYNO.Foto.Search.Search&method=list_item&version=1&offset=0&limit=10&keyword=%22Iceland%22
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

```json
{
   "data":{
      "list":[
         {
            "filename":"IMG_20210812_113728.JPG",
            "filesize":13316487,
            "folder_id":1443,
            "id":26257,
            "indexed_time":1633630843266,
            "owner_user_id":0,
            "time":1628768248,
            "type":"photo"
         },
         {
            "filename":"IMG_20210812_113645.JPG",
            "filesize":15124884,
            "folder_id":204,
            "id":25769,
            "indexed_time":1633630825038,
            "owner_user_id":0,
            "time":1628768205,
            "type":"photo"
         },
         {
            "filename":"IMG_20210812_113645.JPG",
            "filesize":15124884,
            "folder_id":1443,
            "id":26256,
            "indexed_time":1633630843226,
            "owner_user_id":0,
            "time":1628768205,
            "type":"photo"
         },
         {
            "filename":"IMG_20210812_112411.JPG",
            "filesize":2412111,
            "folder_id":204,
            "id":25768,
            "indexed_time":1633630824977,
            "live_type":"photo",
            "owner_user_id":0,
            "time":1628767451,
            "type":"live"
         },
         {
            "filename":"IMG_20210812_112411.JPG",
            "filesize":2412111,
            "folder_id":1443,
            "id":26255,
            "indexed_time":1633630843182,
            "live_type":"photo",
            "owner_user_id":0,
            "time":1628767451,
            "type":"live"
         },
         {
            "filename":"IMG_20210812_112228.JPG",
            "filesize":1709221,
            "folder_id":1443,
            "id":26254,
            "indexed_time":1633630843051,
            "live_type":"photo",
            "owner_user_id":0,
            "time":1628767348,
            "type":"live"
         },
         {
            "filename":"IMG_20210812_111556.JPG",
            "filesize":15704537,
            "folder_id":1443,
            "id":26253,
            "indexed_time":1633630843026,
            "owner_user_id":0,
            "time":1628766956,
            "type":"photo"
         },
         {
            "filename":"IMG_20210812_092204.JPG",
            "filesize":3612383,
            "folder_id":204,
            "id":25767,
            "indexed_time":1633630824932,
            "live_type":"photo",
            "owner_user_id":0,
            "time":1628760124,
            "type":"live"
         },
         {
            "filename":"IMG_20210812_092204.JPG",
            "filesize":3612383,
            "folder_id":1443,
            "id":26252,
            "indexed_time":1633630842957,
            "live_type":"photo",
            "owner_user_id":0,
            "time":1628760124,
            "type":"live"
         },
         {
            "filename":"IMG_20210812_092019.JPG",
            "filesize":14822064,
            "folder_id":1443,
            "id":26251,
            "indexed_time":1633630842927,
            "owner_user_id":0,
            "time":1628760019,
            "type":"photo"
         }
      ]
   },
   "success":true
}
```
