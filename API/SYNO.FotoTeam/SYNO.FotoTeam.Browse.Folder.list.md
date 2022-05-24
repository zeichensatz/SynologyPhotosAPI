# SYNO.FotoTeam.Browse.Folder
## method: list
<b>Authlevel: 2</b><br/>
This means, you don't have to be authenticated first!
In case, you are not authenticated, you only get shared folders listed.
### Description:
List folders in `Shared Space`.
### Request:

| Parameter | Description | Value | Default Value |
| --- | --- | --- | --- |
| offset | Required. Specify how many shared folders are skipped before beginning to return listed shared folders. | Integer |  |
| limit | Required. Number of shared folders requested. | Integer |  |
| id | Optional. Specify which folder will be listed. | Integer | 1 |
| sort_direction | Optional. Specify to sort ascending or to sort descending. <br/>Options include: <br/><b>asc:</b> sort ascending. <br/><b>desc:</b> sort descending. | asc or desc | asc |

### Example:
```
https://<IP_ADDRESS>/photo/webapi/entry.cgi?api=SYNO.FotoTeam.Browse.Folder&version=1&method=list&id=1&offset=0&limit=100
```

### Response:
`<data>` object definitions:

| Parameter | Type | Description |
| --- | --- | --- |
| id | Integer | ID of folder |
| name | String | Name of directory |
| owner_user_id | Integer | UID of album owner. |
| parent | Integer | ID of parent directory |
| passphrase | String | Passphrase |
| shared | Boolean |   |
| sort_direction |   | Values can be default, desc, asc. |

### Example:
```json
{
   "data":{
      "list":[
         {
            "id":1,
            "name":"/",
            "owner_user_id":0,
            "parent":1,
            "passphrase":"PASSPHRASE",
            "shared":true,
            "sort_by":"filename",
            "sort_direction":"desc"
         },
...
         {
            "id":1395,
            "name":"/WoK_19990000_Fotos",
            "owner_user_id":0,
            "parent":1,
            "passphrase":"",
            "shared":false,
            "sort_by":"default",
            "sort_direction":"default"
         },
...
      ]
   },
   "success":true
}
```
