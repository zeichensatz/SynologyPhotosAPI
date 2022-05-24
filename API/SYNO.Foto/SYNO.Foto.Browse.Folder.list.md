# SYNO.Foto.Browse.Folder
## method: list
Authlevel: 1<br/>
This means, you have to be authenticated first.
### Description:
List all folders in `Personal Space`.
### Request:

| Parameter | Description | Value | Default Value |
| --- | --- | --- | --- |
| offset | Required. Specify how many shared folders are skipped before beginning to return listed shared folders. | Integer |  |
| limit | Required. Number of shared folders requested. Value has to be higher than 0 otherwise nothing will displayed. | Integer |  |
| id | ID of parent directory | Integer |  |
| sort_by | Optional. Specify which file information to sort on. <br>Options include: <br/><b>name:</b> file name. <br/><b>size:</b> file size. <br/><b>user:</b> file owner. <br/><b>group:</b> file group. <br/><b>mtime:</b> last modified time. <br/><b>atime:</b> last access time. <br/><b>ctime:</b> last change time. <br/><b>crtime:</b> create time. <br/><b>posix:</b> POSIX permission. <br/><b>type:</b> file extension. | name, size, user, group, mtime, atime, ctime, crtime, posix or type | name |
| sort_direction | Optional. Specify to sort ascending or to sort descending. <br/>Options include: <br/><b>asc:</b> sort ascending. <br/><b>desc:</b> sort descending. | asc or desc | asc |

### Example:
```
https://<IP_ADDRESS>/photo/webapi/entry.cgi?api=SYNO.Foto.Browse.Folder&version=1&method=list&offset=0&limit=100
```

### Response:
`<data>` object definitions:

| Parameter | Type | Description |
| --- | --- | --- |
| id | Integer | ID of folder |
| name | String | Folder name |
| owner_user_id | Integer | UID of album owner |
| parent | Integer | ID of parent directory |
| passphrase |  | Passphrase |
| shared | Boolean |   |
| sort_by |   |   |
| sort_direction |   |   |

### Example:
```json
{
   "data":{
      "list":[
         {
            "id":1989,
            "name":"/20210723",
            "owner_user_id":2,
            "parent":74,
            "passphrase":"",
            "shared":false,
            "sort_by":"default",
            "sort_direction":"default"
         },
         {
            "id":1990,
            "name":"/20210918",
            "owner_user_id":2,
            "parent":74,
            "passphrase":"",
            "shared":false,
            "sort_by":"default",
            "sort_direction":"default"
         }
      ]
   },
   "success":true
}
```
