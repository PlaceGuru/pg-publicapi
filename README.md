# Place.Guru public API documentation

**ALL public api calls require the affix** `?key=YOUR_API_KEY`

**POST** and **PUT** requests can either be made with **form data** or **JSON-objects**

# Places

## Get All Places

```
GET /publicapi/places
```

No other parameters


## Get Place

```
GET /publicapi/places/{url}
```

#### URL parameters
- `url` The identifying url of a place

Example request
```
https://place.guru/publicapi/places/azerty4-ab713bc-qwerty2?key=YOUR_API_KEY
```

## Create place

```
POST /publicapi/places
```

#### Arguments

- `name` (required)
  - **Valid values:** Text string of maximum 45 characters
- `geolat` (required)
  - **Valid values:** Latitude between -90 and 90
- `geolng` (required)
  - **Valid values:** Longitude between -180 and 180
- `description` (optional)
  - **Valid values:** Text string of maximum 65554 characters, supports **markdown** format
- `published` (optional)
  - **Valid values:** `true` or `false`
  - **Default:** `false`
  - **Description:** Whether the place shows up in explore or not
- `comments_enabled` (optional)
  - **Valid values:** `true` or `false`
  - **Default:** `true`
  - **Description:** Enable comments or not
- `mails_enabled` (optional)
  - **Valid values:** `true` or `false`
  - **Default:** `true`
  - **Description:** Enable e-mail updates when there is activity in the place (new comments)
- `address` (optional)
  - **Valid values:** Text string of maximum 255 characters
- `phone_number` (optional)
  - **Valid values:** Text string of maximum 255 characters
- `email` (optional)
  - **Valid values:** E-mail address of maximum 255 characters
- `videos` (optional)
  - **Valid values:** Array of urls for embedded videos
    - **Example:** `[ "link_1" , "link_2" ]`
    **TODO:** What kind of URLs will we allow, parse them in backend or not, ..., example links?
- `links` (optional)
  - **Valid values:** Array of link objects
    - **Example:**
    ```
    [
      {
        "type" : "website",
        "url" : "http://my.site.com"
      },
      {
        "type" : "twitter",
        "url" : "https://twitter.com/myCompany"
      }
    ]
    ```
    - `url` (required)
      - **Valid values:** Valid url
    - `type` (optional)
      - **Valid values:** `website`, `twitter`, `facebook`, `linkedin` (types will be expanded upon)
- `personas` (optional)
  - **Valid values:** Array of persona objects
    - **Example:**
    ```
    [
      {
        "name": "Your name",
        "title": "Your company title",
        "url": "azerty12"
      },
      {
        "name": "Your CTO's name",
        "title": "Company CTO"
      }
    ]
    ```
    - `name` (required)
      - **Valid values:** Text string of maximum 120 characters  
    - `title` (optional)
      - **Valid values:** Text string of maximum 255 characters
    - `url` (optional)
      - **Valid values:** THINK ABOUT WORKING HERE, maybe rename field
- `availability` (optional)
  - **Valid values:** Array of availiability objects
    - **Example:**
    ```
    [
      {
        "start" : "1-1-2017",
        "end": "25-02-2017",
        "note" : "Only available via phone"
      },
      {
        "start" : "28-02-2017",
        "end": "14-03-2017",
        "note" : "We're on skibreak"
      }
    ]
    ```
    - `start` (required)
      - **Valid values:** Date with format d-m-Y
    - `end` (optional)
      - **Valid values:** Date with format d-m-Y
    - `note` (optional)
      - *Valid values:** Text string of maximum 1023 characters
- `opening_hours` (optional)
  - **Valid values:** Array of opening_hour objects  
    - **Example:**
    ```
    [
      {
        "note": "Business opening hours",
        "hours": [
          {
            "day":"1",
        	  "open":"08:30",
        	  "close":"17:00"
        	},
          {
            "day":"2",
            "open":"08:30",
            "close":"12:00"
          },
          {
            "day":"2",
            "open":"13:30",
            "close":"17:00"
          },
          {
            "day":"5",
            "open":"08:30",
            "close":"17:00"
          }
        ]
      },
      {
        "note": "Callcenter opening hours"
        "hours": [
          {
            "day":"1",
            "open":"08:30",
            "close":"23:00"
          },
          {
            "day":"2",
            "open":"08:30",
            "close":"23:00"
          },
          {
            "day":"5",
            "open":"08:30",
            "close":"23:00"
          }
        ]
      }
    ]
    ```
    - `note` (optional)
      - **Valid values:** Text string of maximum 1023 characters
    - `hours` (required)
      - **Valid values:** Hours object, you can have multiple Hours objects for the same day
        - `day` (required)
        - **Valid values:** 1-7, 1 being Monday, 7 being Sunday
        - `open` (required)
        - **Valid values:** Hour with format H:i
        - `close` (required)
        - **Valid values:** Hour with format H:i, after `open`
- `tags` (optional)
  - **Valid values:** Array of maximum 5 tags, each being maximum 25 characters long
    - **Example:** `[ "tag" , "your" , "place" ]`
- `custom_url` (optional)
  - **Valid values:** String of 2-45 characters long, no spaces, only letters, numbers, _ and -
- `custom_marker` (optional)
  - **Valid values:** Id of the custom marker you want to add

#### Full Example
```
{
  "name": "My first API Place",
  "geolat": "60.543232",
  "geolng": "30.321432",
  "description": "My place description goes here.",
  "published": true,
  "comments_enabled": true,
  "mails_enabled": false,
  "address": "SomeRoad 13, SomeCity",
  "phone_number": "123-45678-90",
  "email": "you@company.come",
  "videos": [
    "https://www.youtube.com/embed/zy41l5iYoBw",
    "https://player.vimeo.com/video/192438480"
  ],
  "links": [
    {
      "type" : "website",
      "url" : "http://my.site.com"
    },
    {
      "type" : "twitter",
      "url" : "https://twitter.com/myCompany"
    }
  ],
  "personas": [
    {
      "name": "Your name",
      "title": "Your company title",
      "url": "azerty12"
    },
    {
      "name": "Your CTO's name",
      "title": "Company CTO"
    }
  ],
  "availability": [
    {
      "start" : "1-1-2017",
      "end": "25-02-2017",
      "note" : "Only available via phone"
    },
    {
      "start" : "28-02-2017",
      "end": "14-03-2017",
      "note" : "We're on ski break"
    }
  ],
  "opening_hours": [
    {
      "note": "Business opening hours",
      "hours": [
        {
          "day":"1",
          "open":"08:30",
          "close":"17:00"
        },
        {
          "day":"2",
          "open":"08:30",
          "close":"12:00"
        },
        {
          "day":"2",
          "open":"13:30",
          "close":"17:00"
        },
        {
          "day":"5",
          "open":"08:30",
          "close":"17:00"
        }
      ]
    }
  ],
  "tags": [ "tag", "your", "place" ],
  "custom_url": "my_custom_url",
  "custom_marker": 32
}
```

#### Response
```
{
  "url": "xljh6of-nuntyhp-n3mde0p",
  "name": "My first API Place",
  "geolat": "60.543232",
  "geolng": "30.321432",
  "published": true,
  "mails_enabled": false,
  "comments_enabled": true,
  "description": "My place description goes here.",
  "address": "SomeRoad 13, SomeCity",
  "phone_number": "123-45678-90",
  "email": "you@company.come",
  "videos": [
    "https://www.youtube.com/embed/zy41l5iYoBw",
    "https://player.vimeo.com/video/192438480"
  ],
  "personas": [
    {
      "name": "Your name",
      "title": "Your company title",
      "url": "azerty12"
    },
    {
      "name": "Your CTO's name",
      "title": "Company CTO"
    }
  ],
  "availability": [
    {
      "start": "1-1-2017",
      "end": "25-02-2017",
      "note": "Only available via phone"
    },
    {
      "start": "28-02-2017",
      "end": "14-03-2017",
      "note": "We're on ski break"
    }
  ],
  "links": [
    {
      "url": "http://my.site.com",
      "type": "website"
    },
    {
      "url": "https://twitter.com/myCompany",
      "type": "twitter"
    }
  ],
  "opening_hours": [
    {
      "note": "Business opening hours",
      "hours": [
        {
          "day": "1",
          "open": "08:30",
          "close": "17:00"
        },
        {
          "day": "2",
          "open": "08:30",
          "close": "12:00"
        },
        {
          "day": "2",
          "open": "13:30",
          "close": "17:00"
        },
        {
          "day": "5",
          "open": "08:30",
          "close": "17:00"
        }
      ]
    }
  ],
  "suggested_address": "41K-17, Leningradskaya oblast', Russia, 188730",
  "country": "Russia",
  "region": "Leningradskaya oblast'",
  "subregion": "Priozerskiy rayon",
  "city": "",
  "id": 441,
  "custom_url": "my_custom_url",
  "tags": [
    "tag",
    "your",
    "place"
  ],
  "custom_marker": {
    "id": 32,
    "name": "Cheese",
    "path": "/assets/stickers/Food%20and%20drinks/Cheese.png",
    "category": "Food and drinks",
    "size_x": 45,
    "size_y": 45,
    "color": null
  }
}
```

## Update place

```
PUT /publicapi/places/{url}
```

Updating a place uses the same template as the one used for creating a place.  
If you want to empty a field, just add the key of the field, and an empty string/array after.

Regarding arrays, such as `personas`, `tags`, `videos`, `links`, `opening_hours` and `availability`:  
If you add them to your request, the whole previous array will be overwritten.  
So, if you already had 1 persona for example, if you want to add a 2nd, you have to send both personas in the request.

**TODO:** Example

#### URL parameters
- `url` The identifying url of a place

#### Arguments
```
...
```

## Delete Place

```
DELETE /publicapi/places/{url}
```

#### URL parameters
- `url` The identifying url of a place

#### Response
```
{
  "message": "Place succesfully deleted",
  "code": "200"
}
```

## Add image to place
```
POST /publicapi/places/{url}/images
```

#### URL parameters
- `url` The identifying url of a place

#### Arguments
- `image` (required)
  - **Valid values:** FILE

**TODO** response, example?

## Remove image from place
```
DELETE /publicapi/place/{url}/images/{id}
```

#### URL parameters
- `url` The identifying url of a place
- `id` The id of the image you want to remove

**TODO** response, example?


# Lists

## Get All Lists

```
GET /publicapi/lists
```

**TODO: Example output**


## Get List

```
GET /publicapi/lists/{url}
```

**TODO: Example output**

#### URL parameters
- `url` The identifying url of a list

Example request
```
https://place.guru/publicapi/lists/azerty4-ab713bc-qwerty2?key=YOUR_API_KEY
```

## Create list

```
POST /publicapi/lists
```

#### Arguments

- `name` (required)
  - **Valid values:** Text string of maximum 45 characters
- `description` (optional)
  - **Valid values:** Text string of maximum 65554 characters, supports **markdown** format
- `published` (optional)
  - **Valid values:** `true` or `false`
  - **Default:** `false`
  - **Description:** Whether the list shows up in explore or not
- `comments_enabled` (optional)
  - **Valid values:** `true` or `false`
  - **Default:** `true`
  - **Description:** Enable comments or not
- `mails_enabled` (optional)
  - **Valid values:** `true` or `false`
  - **Default:** `true`
  - **Description:** Enable e-mail updates when there is activity in the list (new comments)
- `address` (optional)
  - **Valid values:** Text string of maximum 255 characters
- `phone_number` (optional)
  - **Valid values:** Text string of maximum 255 characters
- `email` (optional)
  - **Valid values:** E-mail address of maximum 255 characters
- `videos` (optional)
  - **Valid values:** Array of urls for embedded videos
    - **Example:** `[ "link_1" , "link_2" ]`
    **TODO:** What kind of URLs will we allow, parse them in backend or not, ..., exampple links?
- `links` (optional)
  - **Valid values:** Array of link objects
    - **Example:**
    ```
    [
      {
        "type" : "website",
        "url" : "http://my.site.com"
      },
      {
        "type" : "twitter",
        "url" : "https://twitter.com/myCompany"
      }
    ]
    ```
    - `url` (required)
      - **Valid values:** Valid url
    - `type` (optional)
      - **Valid values:** `website`, `twitter`, `facebook`, `linkedin` (types will be expanded upon)
- `personas` (optional)
  - **Valid values:** Array of persona objects
    - **Example:**
    ```
    [
      {
        "name": "Your name",
        "title": "Your company title",
        "url": "azerty12"
      },
      {
        "name": "Your CTO's name",
        "title": "Company CTO"
      }
    ]
    ```
    - `name` (required)
      - **Valid values:** Text string of maximum 120 characters  
    - `title` (optional)
      - **Valid values:** Text string of maximum 255 characters
    - `url` (optional)
      - **Valid values:** THINK ABOUT WORKING HERE, maybe rename field
- `availability` (optional)
  - **Valid values:** Array of availiability objects
    - **Example:**
    ```
    [
      {
        "start" : "1-1-2017",
        "end": "25-02-2017",
        "note" : "Only available via phone"
      },
      {
        "start" : "28-02-2017",
        "end": "14-03-2017",
        "note" : "We're on skibreak"
      }
    ]
    ```
    - `start` (required)
      - **Valid values:** Date with format d-m-Y
    - `end` (optional)
      - **Valid values:** Date with format d-m-Y
    - `note` (optional)
      - *Valid values:** Text string of maximum 1023 characters
- `opening_hours` (optional)
  - **Valid values:** Array of opening_hour objects  
    - **Example:**
    ```
    [
      {
        "note": "Business opening hours"
        "hours": [
          {
            "day":"1",
        	  "open":"08:30",
        	  "close":"17:00"
        	},
          {
            "day":"2",
            "open":"08:30",
            "close":"12:00"
          },
          {
            "day":"2",
            "open":"13:30",
            "close":"17:00"
          },
          {
            "day":"5",
            "open":"08:30",
            "close":"17:00"
          }
        ]
      },
      {
        "note": "Callcenter opening hours",
        "hours": [
          {
            "day":"1",
            "open":"08:30",
            "close":"23:00"
          },
          {
            "day":"2",
            "open":"08:30",
            "close":"23:00"
          },
          {
            "day":"5",
            "open":"08:30",
            "close":"23:00"
          }
        ]
      }
    ]
    ```
    - `note` (optional)
      - **Valid values:** Text string of maximum 1023 characters
    - `hours` (required)
      - **Valid values:** Hours object, you can have multiple Hours objects for the same day
        - `day` (required)
        - **Valid values:** 1-7, 1 being Monday, 7 being Sunday
        - `open` (required)
        - **Valid values:** Hour with format H:i
        - `close` (required)
        - **Valid values:** Hour with format H:i, after `open`
- `tags` (optional)
  - **Valid values:** Array of maximum 5 tags, each being maximum 25 characters long
    - **Example:** `[ "tag" , "your" , "list" ]`
- `custom_url` (optional)
  - **Valid values:** String of 2-45 characters long, no spaces, only letters, numbers, _ and -

#### Full Example
```
{
  "name": "My first API List",
  "description": "My list description goes here.",
  "published": true,
  "comments_enabled": true,
  "mails_enabled": false,
  "address": "SomeRoad 13, SomeCity",
  "phone_number": "123-45678-90",
  "email": "you@company.come",
  "videos": [
    "https://www.youtube.com/embed/zy41l5iYoBw",
    "https://player.vimeo.com/video/192438480"
  ],
  "links": [
    {
      "type" : "website",
      "url" : "http://my.site.com"
    },
    {
      "type" : "twitter",
      "url" : "https://twitter.com/myCompany"
    }
  ],
  "personas": [
    {
      "name": "Your name",
      "title": "Your company title",
      "url": "azerty12"
    },
    {
      "name": "Your CTO's name",
      "title": "Company CTO"
    }
  ],
  "availability": [
    {
      "start" : "1-1-2017",
      "end": "25-02-2017",
      "note" : "Only available via phone"
    },
    {
      "start" : "28-02-2017",
      "end": "14-03-2017",
      "note" : "We're on ski break"
    }
  ],
  "opening_hours": [
    {
      "note": "Business opening hours",
      "hours": [
        {
          "day":"1",
          "open":"08:30",
          "close":"17:00"
        },
        {
          "day":"2",
          "open":"08:30",
          "close":"12:00"
        },
        {
          "day":"2",
          "open":"13:30",
          "close":"17:00"
        },
        {
          "day":"5",
          "open":"08:30",
          "close":"17:00"
        }
      ]
    }
  ],
  "tags": [ "tag", "your", "list" ],
  "custom_url": "my_custom_url"
}
```

#### Response
```
{
  "url": "xlezaf-nunezae-n3mde0p",
  "name": "My first API List",
  "published": true,
  "mails_enabled": false,
  "comments_enabled": true,
  "description": "My list description goes here.",
  "address": "SomeRoad 13, SomeCity",
  "phone_number": "123-45678-90",
  "email": "you@company.come",
  "videos": [
    "https://www.youtube.com/embed/zy41l5iYoBw",
    "https://player.vimeo.com/video/192438480"
  ],
  "personas": [
    {
      "name": "Your name",
      "title": "Your company title",
      "url": "azerty12"
    },
    {
      "name": "Your CTO's name",
      "title": "Company CTO"
    }
  ],
  "availability": [
    {
      "start": "1-1-2017",
      "end": "25-02-2017",
      "note": "Only available via phone"
    },
    {
      "start": "28-02-2017",
      "end": "14-03-2017",
      "note": "We're on ski break"
    }
  ],
  "links": [
    {
      "url": "http://my.site.com",
      "type": "website"
    },
    {
      "url": "https://twitter.com/myCompany",
      "type": "twitter"
    }
  ],
  "opening_hours": [
    {
      "note": "Business opening hours",
      "hours": [
        {
          "day": "1",
          "open": "08:30",
          "close": "17:00"
        },
        {
          "day": "2",
          "open": "08:30",
          "close": "12:00"
        },
        {
          "day": "2",
          "open": "13:30",
          "close": "17:00"
        },
        {
          "day": "5",
          "open": "08:30",
          "close": "17:00"
        }
      ]
    }
  ],
  "custom_url": "my_custom_url",
  "tags": [
    "tag",
    "your",
    "place"
  ]
}
```

## Update list

```
PUT /publicapi/lists/{url}
```

Updating a list uses the same template as the one used for creating a list.  
If you want to empty a field, just add the key of the field, and an empty string/array after.

Regarding arrays, such as `personas`, `tags`, `videos`, `links`, `opening_hours` and `availability`:  
If you add them to your request, the whole previous array will be overwritten.  
So, if you already had 1 persona for example, if you want to add a 2nd, you have to send both personas in the request.

**TODO:** Example

#### URL parameters
- `url` The identifying url of a list

#### Arguments
```
...
```

## Delete List

```
DELETE /publicapi/lists/{url}
```

#### URL parameters
- `url` The identifying url of a list

#### Response
```
{
  "message": "List succesfully deleted",
  "code": "200"
}
```

## Add places/lists to lists
```
POST /publicapi/lists/{url}/add
```

#### URL parameters
- `url` The identifying url of a list

#### Arguments

- `places` (optional)
  - **Valid values:** Array of urls for places you want to attach
    - **Example:** `[ "azerty1-432rez43-432azer" , "qwerty45-432rez43-432azer" ]`
- `children` (optional)
  - **Valid values:** Array of urls for lists you want to attach
    - **Example:** `[ "listay1-432rez43-432azer" , "listty45-432rez43-432aqaz" ]`

#### Full Example
```
{
  places: [
    'azerty1-432rez43-432azer',
    'qwerty45-432rez43-432azer'
  ],
  children: [
    'listay1-432rez43-432azer',
    'listty45-432rez43-432aqaz'
  ]
}
```

## Remove places/lists to lists
```
POST /publicapi/lists/{url}/remove
```

#### URL parameters
- `url` The identifying url of a list

#### Arguments

- `places` (optional)
  - **Valid values:** Array of urls for places you want to remove
    - **Example:** `[ "azerty1-432rez43-432azer" , "qwerty45-432rez43-432azer" ]`
- `children` (optional)
  - **Valid values:** Array of urls for lists you want to remove
    - **Example:** `[ "listay1-432rez43-432azer" , "listty45-432rez43-432aqaz" ]`

#### Full Example
```
{
  places: [
    'azerty1-432rez43-432azer',
    'qwerty45-432rez43-432azer'
  ],
  children: [
    'listay1-432rez43-432azer',
    'listty45-432rez43-432aqaz'
  ]
}
```

## Add image to list
```
POST /publicapi/lists/{url}/images
```

#### URL parameters
- `url` The identifying url of a list

#### Arguments
- `image` (required)
  - **Valid values:** FILE

**TODO** response, example?

## Remove image from list
```
DELETE /publicapi/lists/{url}/images/{id}
```

#### URL parameters
- `url` The identifying url of a list
- `id` The id of the image you want to remove

**TODO** response, example?

# Custom markers

## Get all custom markers

```
GET /publicapi/custommarkers
```

**TODO: Example output**

## Upload custom marker
```
POST /publicapi/custommarkers
```

#### Arguments
- `image` (required)
  - **Valid values:** FILE, maximum 100 kB, jpeg, gif or png

## Delete custom marker
```
DELETE /publicapi/custommarkers/{id}
```

#### URL parameters
- `id` The id of the custom marker you want to remove  
You can only remove your own custom markers

**TODO** response, example?



Under construction

```
Invite person to list				
Invite		
"[
   'email1',
   'email2',
   'email3'
]"		
Array van e-mail adressen om mensen mee uit te nodigen voor een lijst


Uninvite		
"[
   'email1',
   'email2',
   'email3'
]"		
Zelfde maar omgekeerd



createPlaceInList	POST /lists/{url}/places	...		
Maak nieuwe plaats, en zet ze meteen in lijst, mss multiple toelaten?
```
