# SYNO.FotoTeam.Browse.Item
## method: list_with_filter
<b>Authlevel: 2</b><br/>
This means, you don't have to be authenticated first!
In case, you are not authenticated, you only get shared folders listed.
### Description:
List all items in `Shared Space`, filterd by parameters like start, end date or rating
### Request:

| Parameter | Description | Value | Default Value |
| --- | --- | --- | --- |
| offset | Required. Specify how many shared folders are skipped before beginning to return listed shared folders. | Integer |  |
| limit | Required. Number of shared folders requested. | Integer |  |
| sort_direction | Optional. Specify to sort ascending or to sort descending. <br/>Options include: <br/><b>asc:</b> sort ascending. <br/><b>desc:</b> sort descending. | asc or desc | asc |
|version | Required. Version 1 seems to be sufficient | Integer |
| additional | additional information which will be delivered by the api. <br/> ["thumbnail"]: Every Item will get the proper thumbnail link in Response | String
| time | Filter by Start and Enddate <br/> [{"start_time":1112360182,"end_time":1131803782}]<br>start_time and end_time is formatted as unix timestamp | String | All items 


### Example:
```
https://<IP_ADDRESS>/photo/mo/sharing/webapi/entry.cgi?api=SYNO.FotoTeam.Browse.Item&method=list_with_filter&version=1&rating=[1]&additional=["thumbnail"]&time=[{"start_time":1112360182,"end_time":1131803782}]&offset=0&limit=5&sort_direction=desc
```

### Response:
`<data>` object definitions:

| Parameter | Type | Description |
| --- | --- | --- |
| id | Integer | ID of folder |
| name | String | Name of directory |
| owner_user_id | Integer | UID of album owner. |
| thumbnail | Object  | All meta information for given thumbnail |

### Example:
```YAML
{
    "success": true,
    "data": {
        "list": [
            {
                "id": 95920,
                "filename": "42a5a4fb-8848-4f03-a2fd-05044f038511.jpg",
                "filesize": 206423,
                "time": 1707598022,
                "indexed_time": 1707678397692,
                "owner_user_id": 0,
                "folder_id": 1321,
                "type": "photo",
                "additional": {
                    "thumbnail": {
                        "m": "ready",
                        "xl": "ready",
                        "preview": "broken",
                        "sm": "ready",
                        "cache_key": "95865_1707674847",
                        "unit_id": 95865
                    }
                }
            },
            {
                "id": 20866,
                "filename": "image9.jpg",
                "filesize": 161333,
                "time": 1222854333,
                "indexed_time": 1630595732781,
                "owner_user_id": 0,
                "folder_id": 262,
                "type": "photo",
                "additional": {
                    "thumbnail": {
                        "m": "ready",
                        "xl": "ready",
                        "preview": "broken",
                        "sm": "ready",
                        "cache_key": "20866_1630658197",
                        "unit_id": 20866
                    }
                }
            },
            {
                "id": 20867,
                "filename": "image7.jpg",
                "filesize": 231909,
                "time": 1221928465,
                "indexed_time": 1630595732921,
                "owner_user_id": 0,
                "folder_id": 262,
                "type": "photo",
                "additional": {
                    "thumbnail": {
                        "m": "ready",
                        "xl": "ready",
                        "preview": "broken",
                        "sm": "ready",
                        "cache_key": "20867_1630658197",
                        "unit_id": 20867
                    }
                }
            },
            {
                "id": 20959,
                "filename": "image.jpg",
                "filesize": 208244,
                "time": 1187636770,
                "indexed_time": 1630595744585,
                "owner_user_id": 0,
                "folder_id": 262,
                "type": "photo",
                "additional": {
                    "thumbnail": {
                        "m": "ready",
                        "xl": "ready",
                        "preview": "broken",
                        "sm": "ready",
                        "cache_key": "20959_1630658240",
                        "unit_id": 20959
                    }
                }
            },
            {
                "id": 20962,
                "filename": "image33.jpg",
                "filesize": 174090,
                "time": 1130766938,
                "indexed_time": 1630595744822,
                "owner_user_id": 0,
                "folder_id": 262,
                "type": "photo",
                "additional": {
                    "thumbnail": {
                        "m": "ready",
                        "xl": "ready",
                        "preview": "broken",
                        "sm": "ready",
                        "cache_key": "20962_1630658241",
                        "unit_id": 20962
                    }
                }
            }
        ]
    }
}
```
