# SYNO.Foto.Search.Search
## method: count_item
Authlevel: 1<br/>
This means, you have to be authenticated first.
### Description:
Counts items for a keyword.
### Request:

| Parameter | Description | Value | Default Value |
| --- | --- | --- | --- |
| keyword | Optional: Keyword for search. | String | |

### Example:
```
https://<IP_ADDRESS>/photo/webapi/entry.cgi?api=SYNO.Foto.Search.Search&method=count_item&version=1&keyword=%22Iceland%22
```

### Response:
`<data>` object definitions:

| Parameter | Type | Description |
| --- | --- | --- |
| count | Integer | Number of files |

```json
{
   "data":{
      "count":36
   },
   "success":true
}
```
