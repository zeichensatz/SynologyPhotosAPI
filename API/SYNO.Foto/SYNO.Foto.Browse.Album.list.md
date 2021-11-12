# SYNO.Foto.Browse.Album
## method: list
Authlevel: 1<br/>
This means, you have to be authenticated first.
### Description:
List all albums.
### Request:

| Parameter | Description | Value | Default Value |
| --- | --- | --- | --- |
| offset | Required. Specify how many shared folders are skipped before beginning to return listed shared folders. | Integer | 0 |
| limit | Required. Number of shared folders requested. 0 lists all shared folders. | Integer | 0 |
| sort_by | Optional. Specify which file information to sort on. <br>Options include: <br/><b>name:</b> file name. <br/><b>size:</b> file size. <br/><b>user:</b> file owner. <br/><b>group:</b> file group. <br/><b>mtime:</b> last modified time. <br/><b>atime:</b> last access time. <br/><b>ctime:</b> last change time. <br/><b>crtime:</b> create time. <br/><b>posix:</b> POSIX permission. <br/><b>type:</b> file extension. | name, size, user, group, mtime, atime, ctime, crtime, posix or type | name |
| sort_direction | Optional. Specify to sort ascending or to sort descending. <br/>Options include: <br/><b>asc:</b> sort ascending. <br/><b>desc:</b> sort descending. | asc or desc | asc |

### Example:
```
https://<IP_ADDRESS>/photo/webapi/entry.cgi?api=SYNO.Foto.Browse.Album&version=1&method=list&offset=0&limit=100
```

### Response:
`<data>` object definitions:

| Parameter | Type | Description |
| --- | --- | --- |
| cant_migrate_condition | `cant_migrate_condition` object |   |
| condition | `<condition>` object  | Arguments for conditional album |
| create_time | Linux timestamp in second |   |
| end_time | Linux timestamp in second |   |
| freeze_album |   |   |
| id | Integer | id of album |
| item_count | Integer | Total number items in album. |
| owner_user_id | Integer | UID of album owner. |
| passphrase |  |  |
| shared |  |   |
| sort_by |   |   |
| sort_direction |   |   |
| start_time |   |   |
| temporary_shared |   |   |
| type |   |   |
| version |   |   |

`<condition>` object definition:

| Parameter | Type | Description |
| --- | --- | --- |
| folder_filter | Integer |   |
| user_id | Integer |   |

### Example:
```
{
   "data":{
      "list":[
         {
            "cant_migrate_condition":{
               
            },
            "condition":{
               
            },
            "create_time":1633947628,
            "end_time":1631815585,
            "freeze_album":false,
            "id":8,
            "item_count":3,
            "name":"My Album Name",
            "owner_user_id":2,
            "passphrase":"",
            "shared":false,
            "sort_by":"default",
            "sort_direction":"default",
            "start_time":1631387203,
            "temporary_shared":false,
            "type":"normal",
            "version":442042
         },
         {
            "condition":{
               "folder_filter":[
                  1423
               ],
               "user_id":0
            },
            "create_time":1633865347,
            "id":7,
            "item_count":257,
            "name":"My Conditional Album Name",
            "owner_user_id":2,
            "passphrase":"",
            "shared":false,
            "sort_by":"default",
            "sort_direction":"default",
            "type":"condition",
            "version":602595
         }
      ]
   },
   "success":true
}
```
