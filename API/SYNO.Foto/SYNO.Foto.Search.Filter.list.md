# SYNO.Foto.Search.Filter
## method: list
Authlevel: 1<br/>
This means, you have to be authenticated first.
### Description:
List all available search filters.
### Request:

| Parameter | Description | Value | Default Value |
| --- | --- | --- | --- |
| NONE | --- | --- | --- |

### Example:
```
https://<IP_ADDRESS>/photo/webapi/entry.cgi?api=SYNO.Foto.Search.Filter&method=list&version=1&offset=0&limit=100
```

### Response:
`<data>` object definitions:

| Parameter | Type | Description |
| --- | --- | --- |
| see example | | |

### Example:
```json
{
   "data":{
      "aperture":[
         {
            "id":25,
            "name":"F1.8"
         },
...
         {
            "id":9,
            "name":"F11"
         }
      ],
      "camera":[
         {
            "id":14,
            "name":"NIKON D5500"
         },
         {
            "id":13,
            "name":"iPhone 11"
         },
         {
            "id":15,
            "name":"iPhone XR"
         }
      ],
      "exposure_time_group":[
         {
            "end":{
               "den":3000,
               "num":1
            },
            "start":{
               "den":1,
               "num":0
            }
         },
...
         {
            "end":{
               "den":8,
               "num":1
            },
            "start":{
               "den":60,
               "num":1
            }
         }
      ],
      "flash":[
         0,
         16,
         24
      ],
      "focal_length_group":[
         {
            "end":22,
            "start":0
         },
...
         {
            "end":300,
            "start":135
         }
      ],
      "folder_filter":[
         {
            "id":1989,
            "name":"/myfolder1",
            "owner_user_id":2,
            "parent":74,
            "passphrase":"",
            "shared":false,
            "sort_by":"default",
            "sort_direction":"default"
         },
         {
            "id":1990,
            "name":"/myfolder2",
            "owner_user_id":2,
            "parent":74,
            "passphrase":"",
            "shared":false,
            "sort_by":"default",
            "sort_direction":"default"
         }
      ],
      "general_tag":[
         {
            "id":1273,
            "name":"2021"
         },
         {
            "id":1275,
            "name":"Iceland"
         },
      ],
      "geocoding":[
         {
            "children":[
               {
                  "children":[
                     
                  ],
                  "id":227,
                  "level":4,
                  "name":"Eastern Region"
               }
            ],
            "id":225,
            "level":1,
            "name":"Iceland"
         },
...
         {
            "children":[
               {
                  "children":[
                     {
                        "children":[
                           
                        ],
                        "id":173,
                        "level":6,
                        "name":"Località Carbonarie"
                     }
                  ],
                  "id":168,
                  "level":3,
                  "name":"UTI del Canal del Ferro - Val Canale"
               }
            ],
            "id":37,
            "level":1,
            "name":"Italy"
         }
      ],
      "iso":[
         {
            "id":52,
            "name":"16"
         },
...
         {
            "id":2,
            "name":"400"
         }
      ],
      "item_type":[
         {
            "id":0,
            "name":"photo"
         },
         {
            "id":1,
            "name":"video"
         }
      ],
      "lens":[
         {
            "id":7,
            "name":"Nikon AF-S DX Nikkor 18-140mm f/3.5-5.6G ED VR"
         },
...
         {
            "id":10,
            "name":"iPhone XR front camera 2.87mm f/2.2"
         }
      ],
      "person":[
         {
            "cover":7,
            "id":1,
            "item_count":7,
            "name":"Mister X",
            "show":true
         }
      ],
      "time":[
         {
            "end_time":1633046399,
            "month":9,
            "start_time":1630454400,
            "year":2021
         },
...
         {
            "end_time":1617235199,
            "month":3,
            "start_time":1614556800,
            "year":2021
         }
      ]
   },
   "success":true
}
```
