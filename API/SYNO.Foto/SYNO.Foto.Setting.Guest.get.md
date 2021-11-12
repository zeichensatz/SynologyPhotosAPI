# SYNO.Foto.Setting.Guest
## method: get
Authlevel: 2<br/>
No authentication needed.
### Description:
Get settings for guests.
### Request:

| Parameter | Description | Value | Default Value |
| --- | --- | --- | --- |
| NONE | | | |

### Example:
```
https://<IP_ADDRESS>/photo/webapi/entry.cgi?api=SYNO.Foto.Setting.Guest&version=1&method=get
```

### Response:
`<data>` object definitions:

| Parameter | Type | Description |
| --- | --- | --- |
| --- | --- | --- |

### Example:
```
{
   "data":{
      "alias":"photo",
      "default_thumbnail_size":"sm",
      "display_photo_info_to_guest":true,
      "enable_home_service":true,
      "enable_team_space":true
   },
   "success":true
}
```
