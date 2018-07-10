---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - json

toc_footers:
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

search: true
---

# Introduction

Welcome to the Waggle API! Here you fill find info on using our API for the client, admin, and team member applications.

# Authentication

All authentication is handled by a Firebase JWT, passed in as an auth header, such as `Authorization: Bearer eyfj123...` . All endpoints require this authentication.

# Team Member Endpoints

## Device Tokens

This endpoint handles refreshing the user's device token.

### HTTP Request

`POST http://example.com/sitter/device-token`

### Request Body

Key | Required | Description
--------- | ------- | -----------
device_token | true | the user's new device token

## Get Team Member Profile

> Team member profile returns JSON like this:

```json
{
      "address": {
        "address_line_1": "809 West Hill St",
        "address_line_2": "Unit B",
        "city": "Charlotte",
        "state": "NC",
        "zip_code": "28202"
      },
      "secondary_address": {
        "address_line_1": "12424 Agate Ln.",
        "address_line_2": null,
        "city": "Pineville",
        "state": "NC",
        "zip_code": "28134"
      },
      "use_secondary_for_routing": true
    }
```

This endpoint retrieves the team member's profile.

### HTTP Request

`GET http://example.com/sitter/profile`


## Update Team Member Profile

> Update TM profile both accepts & returns JSON structured like this:

```json
{
      "address": {
        "address_line_1": "809 West Hill St",
        "address_line_2": "Unit B",
        "city": "Charlotte",
        "state": "NC",
        "zip_code": "28202"
      },
      "secondary_address": {
        "address_line_1": "12424 Agate Ln.",
        "address_line_2": null,
        "city": "Pineville",
        "state": "NC",
        "zip_code": "28134"
      },
      "use_secondary_for_routing": true
    }
```

This endpoint updates a team member profile. The `use_secondary_for_routing` key is whether or not the team member's starting location will be calculated using their secondary address.

### HTTP Request

`PUT http://example.com/sitter/profile`

## Get List of Appointments

> Returns an array of appointment objects:

```json
[

    {
        "createdAt": "2018-01-15T09:52:44.396Z",
        "id": "5a5c79ecac24280014d01006",
        "appointment_status": {
            "id": 4,
            "name": "In Progress"
        },
        "scheduled_start_time": "2018-03-23T15:30:00.000Z",
        "window_start_time": "2018-03-23T15:30:00.000Z",
        "window_end_time": "2018-03-23T17:00:00.000Z",
        "appointment_type": "10 Min Visit",
        "duration_in_minutes": 10,
        "sitter_viewed": true,
        "pets": [
            {
                "id": "5a4f87441a06183b2ffcb6ec",
                "name": "Fenway",
                "image_url": "https://waggle-keys-stage.s3.amazonaws.com/939abdc3-fcac-4695-b1e9-2bbf136d320f.jpeg",
                "pet_class": "Green"
            },
            {
                "id": "5a4f87431a06183b2ffcb6eb",
                "name": "Bryce",
                "image_url": "https://waggle-keys-stage.s3.amazonaws.com/58305fa2-65fa-432d-b772-51b923a50c82.jpeg",
                "pet_class": "Green"
            }
        ],
        "home": {
            "home_class": "Green",
            "tz_locale": "America/New_York",
            "address": {
                "enforce_device_within_region": true
            }
        }
    },
    {
        "createdAt": "2018-01-15T09:52:44.393Z",
        "id": "5a5c79ebac24280014d01003",
        "appointment_status": {
            "id": 5,
            "name": "Completed"
        },
        "scheduled_start_time": "2018-03-20T15:30:00.000Z",
        "actual_start_time": "2018-03-20T14:07:23.864Z",
        "window_start_time": "2018-03-20T15:30:00.000Z",
        "window_end_time": "2018-03-20T17:00:00.000Z",
        "appointment_type": "10 Min Visit",
        "duration_in_minutes": 10,
        "sitter_viewed": true,
        "pets": [
            {
                "id": "5a4f87441a06183b2ffcb6ec",
                "name": "Fenway",
                "image_url": "https://waggle-keys-stage.s3.amazonaws.com/939abdc3-fcac-4695-b1e9-2bbf136d320f.jpeg",
                "pet_class": "Green"
            },
            {
                "id": "5a4f87431a06183b2ffcb6eb",
                "name": "Bryce",
                "image_url": "https://waggle-keys-stage.s3.amazonaws.com/58305fa2-65fa-432d-b772-51b923a50c82.jpeg",
                "pet_class": "Green"
            }
        ],
        "home": {
            "home_class": "Green",
            "tz_locale": "America/New_York",
            "address": {
                "enforce_device_within_region": true
            }
        }
    },
]

```
### HTTP Request

`GET http://example.com/sitter/appointments`

### List of Appointment Statuses

Status ID | Name
--------- | -------
1 | Pending
2 | Approved
3 | Change Requested
4 | In Progress
5 | Completed
6 | Rejected
7 | Canceled

## Get Single Appointment

> Response body includes all information needed for visit, including client contact & pet information. This is the same information returned in the start & end operations.

```json
{
    "id": "5aafb04f580d62e1145990a5",
    "show_survey": false,
    "appointment_status": {
        "name": "Pending",
        "id": 1
    },
    "appointment_type": {
        "id": 8,
        "name": "Consultation",
        "duration_in_minutes": 30
    },
    "admin_notes": "5019209816 ",
    "visit_routine": "Walk Brinkley for entire visit to burn as much energy as possible.",
    "duration_in_minutes": 30,
    "sitter_viewed": true,
    "addons": [],
    "scheduled_start_time": "2018-03-19T12:36:00.000Z",
    "window_start_time": "2018-03-19T14:00:00.000Z",
    "window_end_time": "2018-03-19T15:00:00.000Z",
    "kml": null,
    "requires_tracking": true,
    "appointment_images": [],
    "client_images": [
        {
            "id": "5ab2fe3d7f9ff30014591012",
            "image_url": "https://waggle-keys-stage.s3.amazonaws.com/56aca046-f979-4e0f-a71b-98a8e9a970a6.jpeg"
        },
        {
            "id": "5ab303ad4262910014aa3474",
            "image_url": "https://waggle-keys-stage.s3.amazonaws.com/ff8c5873-2b87-41ce-a030-9f21d4c20515.jpg"
        },
        {
            "id": "5ab308cc512bb90014544f60",
            "image_url": "https://waggle-keys-stage.s3.amazonaws.com/ff8c5873-2b87-41ce-a030-9f21d4c20515.jpg"
        },
        {
            "id": "5ab3111934b8380014e1115f",
            "image_url": "https://waggle-keys-stage.s3.amazonaws.com/15277E3F-86DE-46A9-A282-42AFE050DB78-5596-000006549798FCC1.jpeg"
        }
    ],
    "sitter_full_name": "Luke Griffith",
    "pets": [
        {
            "id": "5a4f87161a06183b2ffcb4aa",
            "name": "Brinkley",
            "animal_type": "Dog",
            "size": "L (50-80)",
            "image_url": "https://waggle-keys-stage.s3.amazonaws.com/ff8c5873-2b87-41ce-a030-9f21d4c20515.jpg",
            "breed": "Blue Tick Coon Hound Mix",
            "gender": "Neutered Male",
            "age": "Senior (>7 years)",
            "color": "Black and Brown",
            "weight": null,
            "litterbox": "",
            "pet_location": "Free roaming",
            "leash_collar": "Leash/harness hanging to left of washer in laundry closet",
            "harness": "Leg steps into each triangle, clips together on back",
            "toy_info": "",
            "personality": "Friendly",
            "pet_class": "Yellow",
            "pet_class_notes": "Dog aggressive--avoid other dogs.",
            "pet_add_ons": [
                {
                    "id": 1,
                    "name": "Pee",
                    "completed": false,
                    "pet_id": "5a4f87161a06183b2ffcb4aa"
                },
                {
                    "id": 2,
                    "name": "Poop",
                    "completed": false,
                    "pet_id": "5a4f87161a06183b2ffcb4aa"
                }
            ],
            "food": {
                "bowl_location": "Kitchen",
                "food_treat_location": "Dry food in laundry closet. Open canned food in fridge, or new can in laundry.",
                "brand_of_food": "",
                "food_instructions": "1 cup dry food a.m., 1.5 cup dry p.m. Add 3 TBSP canned food to dry.",
                "water_instructions": "",
                "treat_info": "Treats above dry food."
            },
            "medical": {
                "allergies": "",
                "fixed": null,
                "medications": []
            },
            "vet": {
                "full_name": "Nick's Veterinary Hospital",
                "address_line_2": null,
                "state": "NC"
            }
        }
    ],
    "contact": {
        "first_name": "Abbie",
        "last_name": "Example",
        "full_name": "Abbie Example",
        "email": "example@gmail.com",
        "phone_numbers": [
            {
                "number": "5619209516",
                "type": "mobile"
            }
        ]
    },
    "home": {
        "address": {
            "address_line_1": "1829 Logie Ave",
            "address_line_2": "",
            "city": "Charlotte",
            "state": "NC",
            "zip_code": "28205",
            "map_image_url": "https://waggle-keys-stage.s3.amazonaws.com/undefined",
            "street_view_image_url": "https://waggle-keys-stage.s3.amazonaws.com/undefined",
            "coordinates": {
                "latitude": 35.22264513423151,
                "longitude": -80.7987217
            },
            "enforce_device_within_region": true
        },
        "tz_locale": "America/New_York",
        "alarm_code": "Disarm: 0212212316. Arm: Arm+Bypass All+Away. Alarm is on left as you walk in front door.",
        "parking": "",
        "home_access_notes": "Owner's lockbox on front door handle. CODE: 2323914, press top button down and pull toward you. Enter code again to close box. Enter home through front door.",
        "home_class": "Green",
        "home_class_notes": "",
        "waste_disposal": "Garbage bin in driveway.",
        "secured_yard": "Yes",
        "apartment_info": "",
        "notes": "Brinkley pulls for squirrels."
    }
}
```

Get all the information for a single visit.

### HTTP Request

`GET http://example.com/sitter/appointments/<appointmentId>`

## Start an Appointment

> Starting visit accepts three keys, but none are required. They tell the API whether or not the visit was started out of proper GPS range, and pass in the coordinates if true.

```json
{
  "override_device_within_region": true,
  "override_start_longitude": 35.1234567,
  "override_start_latitude": 83.390193
    }
```

> Returns the updated visit (same as GET single visit response):

```json
{
    "id": "5aafb04f580d62e1145990a5",
    "show_survey": false,
    "appointment_status": {
        "name": "Pending",
        "id": 1
    },
    "appointment_type": {
        "id": 8,
        "name": "Consultation",
        "duration_in_minutes": 30
    },
    "admin_notes": "5019209816 ",
    "visit_routine": "Walk Brinkley for entire visit to burn as much energy as possible.",
    "duration_in_minutes": 30,
    "sitter_viewed": true,
    "addons": [],
    "scheduled_start_time": "2018-03-19T12:36:00.000Z",
    "window_start_time": "2018-03-19T14:00:00.000Z",
    "window_end_time": "2018-03-19T15:00:00.000Z",
    "kml": null,
    "requires_tracking": true,
    "appointment_images": [],
    "client_images": [
        {
            "id": "5ab2fe3d7f9ff30014591012",
            "image_url": "https://waggle-keys-stage.s3.amazonaws.com/56aca046-f979-4e0f-a71b-98a8e9a970a6.jpeg"
        },
        {
            "id": "5ab303ad4262910014aa3474",
            "image_url": "https://waggle-keys-stage.s3.amazonaws.com/ff8c5873-2b87-41ce-a030-9f21d4c20515.jpg"
        },
        {
            "id": "5ab308cc512bb90014544f60",
            "image_url": "https://waggle-keys-stage.s3.amazonaws.com/ff8c5873-2b87-41ce-a030-9f21d4c20515.jpg"
        },
        {
            "id": "5ab3111934b8380014e1115f",
            "image_url": "https://waggle-keys-stage.s3.amazonaws.com/15277E3F-86DE-46A9-A282-42AFE050DB78-5596-000006549798FCC1.jpeg"
        }
    ],
    "sitter_full_name": "Luke Griffith",
    "pets": [
        {
            "id": "5a4f87161a06183b2ffcb4aa",
            "name": "Brinkley",
            "animal_type": "Dog",
            "size": "L (50-80)",
            "image_url": "https://waggle-keys-stage.s3.amazonaws.com/ff8c5873-2b87-41ce-a030-9f21d4c20515.jpg",
            "breed": "Blue Tick Coon Hound Mix",
            "gender": "Neutered Male",
            "age": "Senior (>7 years)",
            "color": "Black and Brown",
            "weight": null,
            "litterbox": "",
            "pet_location": "Free roaming",
            "leash_collar": "Leash/harness hanging to left of washer in laundry closet",
            "harness": "Leg steps into each triangle, clips together on back",
            "toy_info": "",
            "personality": "Friendly",
            "pet_class": "Yellow",
            "pet_class_notes": "Dog aggressive--avoid other dogs.",
            "pet_add_ons": [
                {
                    "id": 1,
                    "name": "Pee",
                    "completed": false,
                    "pet_id": "5a4f87161a06183b2ffcb4aa"
                },
                {
                    "id": 2,
                    "name": "Poop",
                    "completed": false,
                    "pet_id": "5a4f87161a06183b2ffcb4aa"
                }
            ],
            "food": {
                "bowl_location": "Kitchen",
                "food_treat_location": "Dry food in laundry closet. Open canned food in fridge, or new can in laundry.",
                "brand_of_food": "",
                "food_instructions": "1 cup dry food a.m., 1.5 cup dry p.m. Add 3 TBSP canned food to dry.",
                "water_instructions": "",
                "treat_info": "Treats above dry food."
            },
            "medical": {
                "allergies": "",
                "fixed": null,
                "medications": []
            },
            "vet": {
                "full_name": "Nick's Veterinary Hospital",
                "address_line_2": null,
                "state": "NC"
            }
        }
    ],
    "contact": {
        "first_name": "Abbie",
        "last_name": "Example",
        "full_name": "Abbie Example",
        "email": "example@gmail.com",
        "phone_numbers": [
            {
                "number": "5619209516",
                "type": "mobile"
            }
        ]
    },
    "home": {
        "address": {
            "address_line_1": "1829 Logie Ave",
            "address_line_2": "",
            "city": "Charlotte",
            "state": "NC",
            "zip_code": "28205",
            "map_image_url": "https://waggle-keys-stage.s3.amazonaws.com/undefined",
            "street_view_image_url": "https://waggle-keys-stage.s3.amazonaws.com/undefined",
            "coordinates": {
                "latitude": 35.22264513423151,
                "longitude": -80.7987217
            },
            "enforce_device_within_region": true
        },
        "tz_locale": "America/New_York",
        "alarm_code": "Disarm: 0212212316. Arm: Arm+Bypass All+Away. Alarm is on left as you walk in front door.",
        "parking": "",
        "home_access_notes": "Owner's lockbox on front door handle. CODE: 2323914, press top button down and pull toward you. Enter code again to close box. Enter home through front door.",
        "home_class": "Green",
        "home_class_notes": "",
        "waste_disposal": "Garbage bin in driveway.",
        "secured_yard": "Yes",
        "apartment_info": "",
        "notes": "Brinkley pulls for squirrels."
    }
}
```

Start a visit. In order to start, the visit must have the status of 'Approved', and the team member must be within the time window.

### HTTP Request

`PUT http://example.com/sitter/appointments/<AppointmentId>/start`

## End an Appointment

> Request body includes array of completed visit addons, with a pet id if the addon is pet-specific (like feeding)

```json
{
  "completed_addons": [{
    "id": 1,
    "name": "Pee",
    "completed": true,
    "pet_id": "5a4f87161a06183b2ffcb4aa"
  }]
}
```
> Returns the updated visit (same as GET single visit response):

```json
{
    "id": "5aafb04f580d62e1145990a5",
    "show_survey": false,
    "appointment_status": {
        "name": "Pending",
        "id": 1
    },
    "appointment_type": {
        "id": 8,
        "name": "Consultation",
        "duration_in_minutes": 30
    },
    "admin_notes": "5019209816 ",
    "visit_routine": "Walk Brinkley for entire visit to burn as much energy as possible.",
    "duration_in_minutes": 30,
    "sitter_viewed": true,
    "addons": [],
    "scheduled_start_time": "2018-03-19T12:36:00.000Z",
    "window_start_time": "2018-03-19T14:00:00.000Z",
    "window_end_time": "2018-03-19T15:00:00.000Z",
    "kml": null,
    "requires_tracking": true,
    "appointment_images": [],
    "client_images": [
        {
            "id": "5ab2fe3d7f9ff30014591012",
            "image_url": "https://waggle-keys-stage.s3.amazonaws.com/56aca046-f979-4e0f-a71b-98a8e9a970a6.jpeg"
        },
        {
            "id": "5ab303ad4262910014aa3474",
            "image_url": "https://waggle-keys-stage.s3.amazonaws.com/ff8c5873-2b87-41ce-a030-9f21d4c20515.jpg"
        },
        {
            "id": "5ab308cc512bb90014544f60",
            "image_url": "https://waggle-keys-stage.s3.amazonaws.com/ff8c5873-2b87-41ce-a030-9f21d4c20515.jpg"
        },
        {
            "id": "5ab3111934b8380014e1115f",
            "image_url": "https://waggle-keys-stage.s3.amazonaws.com/15277E3F-86DE-46A9-A282-42AFE050DB78-5596-000006549798FCC1.jpeg"
        }
    ],
    "sitter_full_name": "Luke Griffith",
    "pets": [
        {
            "id": "5a4f87161a06183b2ffcb4aa",
            "name": "Brinkley",
            "animal_type": "Dog",
            "size": "L (50-80)",
            "image_url": "https://waggle-keys-stage.s3.amazonaws.com/ff8c5873-2b87-41ce-a030-9f21d4c20515.jpg",
            "breed": "Blue Tick Coon Hound Mix",
            "gender": "Neutered Male",
            "age": "Senior (>7 years)",
            "color": "Black and Brown",
            "weight": null,
            "litterbox": "",
            "pet_location": "Free roaming",
            "leash_collar": "Leash/harness hanging to left of washer in laundry closet",
            "harness": "Leg steps into each triangle, clips together on back",
            "toy_info": "",
            "personality": "Friendly",
            "pet_class": "Yellow",
            "pet_class_notes": "Dog aggressive--avoid other dogs.",
            "pet_add_ons": [
                {
                    "id": 1,
                    "name": "Pee",
                    "completed": false,
                    "pet_id": "5a4f87161a06183b2ffcb4aa"
                },
                {
                    "id": 2,
                    "name": "Poop",
                    "completed": false,
                    "pet_id": "5a4f87161a06183b2ffcb4aa"
                }
            ],
            "food": {
                "bowl_location": "Kitchen",
                "food_treat_location": "Dry food in laundry closet. Open canned food in fridge, or new can in laundry.",
                "brand_of_food": "",
                "food_instructions": "1 cup dry food a.m., 1.5 cup dry p.m. Add 3 TBSP canned food to dry.",
                "water_instructions": "",
                "treat_info": "Treats above dry food."
            },
            "medical": {
                "allergies": "",
                "fixed": null,
                "medications": []
            },
            "vet": {
                "full_name": "Nick's Veterinary Hospital",
                "address_line_2": null,
                "state": "NC"
            }
        }
    ],
    "contact": {
        "first_name": "Abbie",
        "last_name": "Example",
        "full_name": "Abbie Example",
        "email": "example@gmail.com",
        "phone_numbers": [
            {
                "number": "5619209516",
                "type": "mobile"
            }
        ]
    },
    "home": {
        "address": {
            "address_line_1": "1829 Logie Ave",
            "address_line_2": "",
            "city": "Charlotte",
            "state": "NC",
            "zip_code": "28205",
            "map_image_url": "https://waggle-keys-stage.s3.amazonaws.com/undefined",
            "street_view_image_url": "https://waggle-keys-stage.s3.amazonaws.com/undefined",
            "coordinates": {
                "latitude": 35.22264513423151,
                "longitude": -80.7987217
            },
            "enforce_device_within_region": true
        },
        "tz_locale": "America/New_York",
        "alarm_code": "Disarm: 0212212316. Arm: Arm+Bypass All+Away. Alarm is on left as you walk in front door.",
        "parking": "",
        "home_access_notes": "Owner's lockbox on front door handle. CODE: 2323914, press top button down and pull toward you. Enter code again to close box. Enter home through front door.",
        "home_class": "Green",
        "home_class_notes": "",
        "waste_disposal": "Garbage bin in driveway.",
        "secured_yard": "Yes",
        "apartment_info": "",
        "notes": "Brinkley pulls for squirrels."
    }
}
```

End a visit. This is a multipart-formdata request that includes two files. The first is named `kml` and is a .kml file of where the visit took place. The second is named `raw_location_dump`, and is a .csv of the raw locations generated during the walk.

### HTTP Request

`POST http://example.com/sitter/appointments/<AppointmentId>/end`

## Update Appointment Notes

> Request body includes sitter notes to admin, and sitter notes to client.

```json
{
  "sitter_notes_to_client": "We had a great time on our visit today! Your dog is hilarious. Etc Etc Etc.",
  "sitter_notes_to_admin": "Dog is slightly aggressive towards other dogs."
}
```

> Returns same appointment json as GET single visit.

Setting notes for an appointment. This can happen during an in-progress visit, or within ten minutes after the visit is ended.

### HTTP Request

`PUT http://example.com/sitter/appointments/<AppointmentId>/notes`

## Add Appointment Images

> Request body includes keys for image url and favorite:

```json
{
  "image_url": "https://s3.amazonaws.ours3bucket.com/1234u909jdlkj.jpeg",
  "favorite": false
}
```

> Returns an array of the appointment images:

```json
{
  [
    {
      "id": "5dk09jdklkd902jk",
      "image_url": "https://s3.amazonaws.ours3bucket.com/1234u909jdlkj.jpeg",
      "favorite": false    
    },
    {
      "id": "5dk09jdklkd902jefsdf",
      "image_url": "https://s3.amazonaws.ours3bucket.com/2jlkd929090sd93.jpeg",
      "favorite": true  
    },
  ]
}
```

Images are uploaded directly to S3. This route updates the visit with the URL of the image in S3. It also includes a key `favorite` to indicate if the image is the best image from the visit.

### HTTP Request

`POST http://example.com/sitter/appointments/<appointmentId>/images`

## Add Client Images

> Request body includes image url

```json
{
  "image_url": "https://s3.amazonaws.ours3bucket.com/2jlkd929090sd93.jpeg"
}
```

> Response includes url and id from DB

```json
{
  "image_url": "https://s3.amazonaws.ours3bucket.com/2jlkd929090sd93.jpeg",
  "id": "5ajkd9ijldk2jlkjd09lk"
}
```
Images are uploaded directly to S3.

### HTTP Request

`POST http://example.com/sitter/appointments/<appointmentId>/clientImages`

## Add Pet Images

> Request body includes image url

```json
{
  "image_url": "https://s3.amazonaws.ours3bucket.com/2jlkd929090sd93.jpeg"
}
```

> Response includes url and id from DB

```json
{
  "image_url": "https://s3.amazonaws.ours3bucket.com/2jlkd929090sd93.jpeg",
  "id": "5ajkd9ijldk2jlkjd09lk"
}
```
These are pet-specific images, to be used as a pet's 'profile' picture. Images are uploaded directly to S3.

### HTTP Request

`POST http://example.com/sitter/pets/<petId>/images`

## Delete Appointment Image

> Successful response is an object with message 'Image deleted.':

```json
{
  "message": "Image Deleted."
}
```

Delete a specific image for a visit.

### HTTP Request

`DELETE http://example.com/sitter/appointments/<appointmentId>/images/<imageId>`

## Edit Appointment Image

> Request body currently is only key of favorite true/false:

```json
{
  "favorite": true
}
```
> Returns image object:

```json
{
  "id": "5jk90ljkddkjlkjs",
  "image_url": "https://s3.amazonaws.ours3bucket.com/2jlkd929090sd93.jpeg",
  "favorite": true
}
```

### HTTP Request

`PUT http://example.com/sitter/appointments/<appointmentId>/images/<imageId>`

## Complete/Uncomplete Add-On

> Request body includes an array of addOns:

```json
{
  "addOns": [{"id": 2, "name": "Pee", "completed": true, "pet_id": "5a4f87201a06183b2ffcb532"}]
}
```

This will complete or un-complete an appointment add-on. The array should include the add-on id, whether or not the add-on is completed, add the pet_id, if applicable.

### HTTP Request

`PUT http://example.com/sitter/appointments/<appointmentId>/addOns`

# Admin Endpoints

## Get Constants

> Successful response is an object containing application constants:

```json
{  
   "markets":[  
      {  
         "_id":"5a7ef4b208abad6d70537e5f",
         "updatedAt":"2018-06-26T03:25:59.494Z",
         "createdAt":"2018-02-10T13:33:38.060Z",
         "longitude":"-80.9799136",
         "latitude":"35.2030728",
         "state":"NC",
         "city":"Charlotte",
         "__v":0,
         "time_zone":"America/New_York",
         "start_date":"2018-05-29T03:25:14.776Z"
      },
      {  
         "_id":"5b1df0e5fe776f0014d67050",
         "updatedAt":"2018-06-11T03:47:49.239Z",
         "createdAt":"2018-06-11T03:47:49.239Z",
         "longitude":"-97.7431",
         "latitude":"30.2672",
         "time_zone":"America/Chicago",
         "state":"TX",
         "city":"Austin",
         "start_date":"2018-06-19T13:33:38.060Z",
         "__v":0
      }
   ],
   "constants":{  
      "contactTypes":[  
         {  
            "id":1,
            "name":"Primary"
         },
         {  
            "id":2,
            "name":"Secondary"
         },
         {  
            "id":3,
            "name":"Emergency"
         }
      ],
      "genders":[  
         {  
            "id":1,
            "name":"Male"
         },
         {  
            "id":2,
            "name":"Female"
         }
      ],
      "payTypes":[  
         {  
            "id":1,
            "name":"Fixed Annual"
         },
         {  
            "id":2,
            "name":"Fixed Per Visit"
         },
         {  
            "id":3,
            "name":"Fixed Hourly"
         },
         {  
            "id":4,
            "name":"Percent Per Visit"
         }
      ],
      "phoneNumberTypes":[  
         {  
            "id":1,
            "name":"Mobile"
         },
         {  
            "id":2,
            "name":"Home"
         },
         {  
            "id":3,
            "name":"Work"
         }
      ],
      "staffTypes":[  
         {  
            "id":1,
            "name":"Employee"
         },
         {  
            "id":2,
            "name":"Contractor"
         }
      ],
      "states":[  
         {  
            "id":33,
            "name":"North Carolina",
            "abbreviation":"NC"
         },
         {  
            "id":43,
            "name":"Texas",
            "abbreviation":"TX"
         }
      ],
      "classifications":[  
         {  
            "id":1,
            "name":"Green"
         },
         {  
            "id":2,
            "name":"Yellow"
         },
         {  
            "id":3,
            "name":"Red"
         }
      ],
      "buildingTypes":[  
         {  
            "id":1,
            "name":"Apartment / Condo"
         },
         {  
            "id":2,
            "name":"Townhouse"
         },
         {  
            "id":3,
            "name":"House"
         },
         {  
            "id":4,
            "name":"Other"
         }
      ],
      "appointmentStatuses":[  
         {  
            "id":1,
            "name":"Pending"
         },
         {  
            "id":2,
            "name":"Approved"
         }
      ],
      "appointmentTypes":[  
         {  
            "id":20,
            "name":"20 Min Visit",
            "duration_in_minutes":20,
            "active":true,
            "admin_only":false
         },
         {  
            "id":40,
            "name":"40 Min Visit",
            "duration_in_minutes":40,
            "active":true,
            "admin_only":false
         }
      ],
      "addOnServicesPet":[  
         {  
            "id":1,
            "name":"Pee",
            "price":0,
            "active":true
         },
         {  
            "id":2,
            "name":"Poop",
            "price":0,
            "active":true
         }
      ],
      "addOnServicesGeneral":[  
         {  
            "id":5,
            "name":"Bring in Mail",
            "price":0,
            "active":true
         },
         {  
            "id":6,
            "name":"Clean Litter Box",
            "price":0,
            "active":true
         }
      ],
      "zones":[  
         {  
            "id":1,
            "zone_name":"Uptown",
            "background_color":"#AD8DEA",
            "text_color":"#FFFFFF",
            "created_at":"2017-03-09T17:45:59.000Z",
            "updated_at":"2017-03-09T17:45:59.000Z",
            "deleted_at":null
         },
         {  
            "id":2,
            "zone_name":"South End",
            "background_color":"#E985C4",
            "text_color":"#FFFFFF",
            "created_at":"2017-03-09T17:45:59.000Z",
            "updated_at":"2017-03-09T17:45:59.000Z",
            "deleted_at":null
         }
      ],
      "timezones":[  
         {  
            "name":"Eastern",
            "value":"America/New_York"
         },
         {  
            "name":"Central",
            "value":"America/Chicago"
         }
      ]
   }
}

```

Get application constants

### HTTP Request

`GET https://waggle-api-prod.herokuapp.com/admin/constants/`

## Calculate Routes

> Successful response is an object containing a job id

```json
{
  "job_id":"jiw2nzom842"
}
```

Triggers a job to assign sitters to appointments.


### HTTP Request

`GET https://waggle-api-prod.herokuapp.com/calculateRoutes?market=5a7ef4b208abad6d70537e5f`

### Request body

Key|Required|Description
---|--------|-----------
appointments|false|An array of appointment ids sent in the request body
sitters|false|An array of sitter ids sent in the request body


###Query String

Key|Required|Description
---|--------|-----------
market|true|ID of market to schedule appointments for
startDate|false|Beginning of interval to schedule appointments
endDate|false|End of interval to schedule appointments
minVisits|false|Minimum number of visits to schedule
lateness|false|Additional time to allow for sitters to arrive at appointments
traffic|false|Traffic adjustment settings

## Get Client Credits

> Successful response is an array of walk credit objects':

```json
[  
   {  
      "name":"twenty",
      "number":4,
      "auto_renew":5,
      "type":"20 Minute"
   },
   {  
      "name":"forty",
      "number":0,
      "type":"40 Minute"
   },
   {  
      "name":"sixty",
      "number":0,
      "type":"60 Minute"
   },
   {  
      "name":"play_care",
      "number":0,
      "type":"PlayCare"
   }
]
```

Returns remaining credits purchased by client.

### HTTP Request

`GET https://waggle-api-prod.herokuapp.com/admin/client/<clientId>/credits`

## Get Staff by Activation

> Successful response is an object containing staff email':

```json
{
  "email": "scott@walkskipper.com"
}
```

Returns staff email given a corresponding activation ID

### HTTP Request

`GET https://waggle-api-prod.herokuapp.com/admin/adminActivation/<activationId>`

## Set Password

> Successful response is an object containing success flag':

```json
{
  "success": true
}
```

Sets password for Staff Members.

### HTTP Request

`POST https://waggle-api-prod.herokuapp.com/admin/setPassword`

### Request Body

Key|Required|Description
---|--------|-----------
activationId|true|Unique identifier for users without credentials
password|true|Password to set for user

## Clear Appointment From Dashboard

Removes appointment from dashboard.

### HTTP Request

`POST https://waggle-api-prod.herokuapp.com/admin/appointments/<appointmentId>/clear`

### Request Body

Key|Required|Description
---|--------|-----------
clear_dash|true|Flag that must be set to true or error is thrown
clear_notes|false|Flag that will clear appointment notes from dashboard if set to true

## Unassign Appointment

> Successful response is an object containing success flag':

```json
{
  "success": true
}
```

Removes sitter from the appointment with the `appointmentId` specified in the URI

### HTTP Request

`POST https://waggle-api-prod.herokuapp.com/admin/appointments/<appointmentId>/unassign`

### Request Body

Key|Required|Description
---|--------|-----------
market_id|true|ID of the market to which the appointment belongs
draft|false|Draft schedule object, if specified the changes made will not be immediately posted.

## Get Activities

> Successful response is an array containing objects with appointment, client and pet data':

```json
[  
   {  
      "_id":"5b12bd144b17150014ce3d84",
      "actual_start_time":"2018-06-26T14:00:31.000Z",
      "actual_end_time":"2018-06-26T14:21:48.000Z",
      "appointment_status":{  
         "name":"Completed",
         "id":5
      },
      "appointment_type":{  
         "duration_in_minutes":20,
         "name":"20-Minute Visit",
         "id":20
      },
      "created_at":"2018-06-02T15:51:48.935Z",
      "updated_at":"2018-06-26T20:39:18.509Z",
      "images":[  
         {  
            "id":"5b324bc2bff659001436844e",
            "file_name":"https://waggle-keys-prod.s3.amazonaws.com/5b12bd144b17150014ce3d84_7A323B88-6E53-40B2-846E-AA7A0DF6F033-3695-000004AACBCCA064.jpeg",
            "favorite":true
         }
      ],
      "time_zone":"America/New_York",
      "recurrence":{  
         "is_recurring":false,
         "weekdays":null
      },
      "client_notes":"Walk for the entire visit! Please use the stairs when going downstairs! Give puppy pop from freezer and re-fill his water. ",
      "clear_notes_from_dashboard":false,
      "sitter_notes_to_client":"Brody old friend, old pal!!😍😍 He gave off a “super ferocious” bark🦁, but I always feel loved when Brody greets me at the door🚪💕 I at least got him to sit while I was approaching him with the leash😆, and then we set off down the stairs📶! Brody went straight to “business”👏🏽🚽; he struggled a little and produced something blue😳, but he was all smiles when he was done😂 He even rolled around🔄in the grass🌱and spied👀another doggy friend🐕across the street! After Brody did #1️⃣, we headed back upstairs so he could get water💦and a puppy pop🍭😋! He’s one of the few pups I know who’s more hyper AFTER the walk🤣!! I gave him plenty of scratchies💟before I said goodbye👋🏽 See you later today, Bro’!!🐾❤️",
      "duration_in_minutes":20,
      "addons":[  
         {  
            "id":1,
            "name":"Pee",
            "completed":true,
            "pet_id":"5a4f87561a06183b2ffcb7d6"
         },
         {  
            "id":2,
            "name":"Poop",
            "completed":true,
            "pet_id":"5a4f87561a06183b2ffcb7d6"
         }
      ],
      "scheduled_start_time":"Tue Jun 26 2018 10:00",
      "scheduled_end_time":"2018-06-26T10:20:00.000Z",
      "window_start_time":"Tue Jun 26 2018 9:30",
      "window_end_time":"Tue Jun 26 2018 11:00",
      "sitter":{  
         "full_name":"Scott Huff",
         "_id":"5a57b07afb3833c6c51e1d8f"
      },
      "sitter_id":"5a57b07afb3833c6c51e1d8f",
      "contact":{  
         "client_id":"5a4d05f5360d607ef03f623f",
         "first_name":"Scott",
         "last_name":"Huff",
         "full_name":"Scott Huff",
         "email":"scott@walkskipper.com"
      },
      "pets":[  
         {  
            "_id":"5a4f87561a06183b2ffcb7d6",
            "name":"Brody",
            "image_url":"https://waggle-keys-prod.s3.amazonaws.com/bb28f69d-f5f8-4745-a7c6-14f691ce043e.jpeg",
            "pet_class":"Yellow",
            "pet_class_notes":"Use treats to help him warm up to you! MAKE SURE CRATE IS COMPLETELY SECURE BEFORE LEAVING."
         }
      ],
      "home":{  
         "home_class":"Yellow",
         "home_class_notes":"Follow Entry notes carefully!",
         "admin_client_notes":"",
         "zones":[  
            {  
               "id":5,
               "zone_name":"Southpark",
               "background_color":"#F27C7C",
               "text_color":"#FFFFFF",
               "created_at":"2017-03-09T17:45:59.000Z",
               "updated_at":"2017-03-09T17:45:59.000Z",
               "deleted_at":null
            }
         ],
         "address":{  
            "enforce_device_within_region":true,
            "street_view_image_file_name":"ba539d0d-249a-4a98-9f5a-f8e47faf8bf6.jpg",
            "map_image_file_name":"57cfb74a-7833-4c87-be91-64af255baa20.png",
            "longitude":"-80.82444147775449",
            "latitude":"35.15683433323797",
            "zip_code":"28211",
            "state":"33",
            "city":"Charlotte",
            "address_line_2":"Unit 526",
            "address_line_1":"721 Governor Morrison St"
         }
      }
   }
]
```

Returns a list of appointment objects that are within a given time interval.  If no interval
is specified then appointments for the current day are returned.

### HTTP Request

`GET https://waggle-api-prod.herokuapp.com/admin/activities?city=5a7ef4b208abad6d70537e5f`

### Query Parameters

Key|Required|Description
---|--------|-----------
city|true|Market object for the market to get appointments for
startDate|false|Datetime for the beginning of appointment interval
endDate|false|Datetime for the end of appointment interval

## Activate Client

Activates user with `clientId` specified in the URI in firebase, assigns them an
`activation_id` and sends a confirmation email. Activates both clients and staff.

### HTTP Request

`GET https://waggle-api-prod.herokuapp.com/admin/activateClient/<clientId>`

## Create Client

> Successful response is an object containing success flag and newly created client object':

```json
{  
   "success":true,
   "client":{  
      "first_name":"Scott",
      "last_name":"Huff",
      "full_name":"Scott Huff",
      "market_id":"5a7ef4b208abad6d70537e5f",
      "email":"shuff703@gmail.com",
      "home_class":{  
         "id":2,
         "name":"Yellow"
      },
      "home_class_notes":"Home Class Notes",
      "signup_date":"2018-06-26",
      "visit_routine":"Visit Routine notes go here",
      "secured_yard":false,
      "zones":[  
         {  
            "id":2,
            "zone_name":"South End",
            "background_color":"#E985C4",
            "text_color":"#FFFFFF",
            "created_at":"2017-03-09T17:45:59.000Z",
            "updated_at":"2017-03-09T17:45:59.000Z",
            "deleted_at":null
         }
      ],
      "contact":{  
         "phone_number":"7033039405",
         "address":{  
            "address_line_1":"2225 Hawkins St",
            "address_line_2":"Unit 261",
            "city":"Charlotte",
            "state":33,
            "zip_code":"28203",
            "enforce_device_within_region":true,
            "latitude":35.2079082,
            "longitude":-80.8646226,
            "map_image_file_name":"ebad5d64-d9a5-4d18-8850-70fe77bbad65.png",
            "street_view_image_file_name":"c603f2df-89e1-428e-a779-cde066968034.jpg"
         }
      },
      "secondary_contact":{  

      },
      "emergency_contact":{  

      },
      "stripe_id":"cus_D7eB1oapuqgByB"
   }
}
```

Accepts multipart form data resembling a `Client` object and creates a client user.

### HTTP Request

`POST https://waggle-api-prod.herokuapp.com/admin/createClient`

### Request Body

Key|Required|Description
---|--------|-----------
Client|true|Object containing form data used to create Client

## Create Staff

> Successful response is an object containing success flag, and newly created Staff object':

```json
{  
   "success":true,
   "staff":{  
      "first_name":"Scott",
      "last_name":"Huff",
      "email":"scott@walkskipper.com",
      "roles":[  
         "admin",
         "oa",
         "sitter"
      ],
      "dob":"1992-09-10",
      "staff_type":"Employee",
      "pay_type":"Fixed Annual",
      "market_id":"5b1ffdb258e7e43a386d4a99",
      "hire_date":"2018-06-27T12:24:02.854Z",
      "gender":"Male",
      "notes":"Notes about Scott",
      "zones":[  
         {  
            "id":2,
            "zone_name":"South End",
            "background_color":"#E985C4",
            "text_color":"#FFFFFF",
            "created_at":"2017-03-09T17:45:59.000Z",
            "updated_at":"2017-03-09T17:45:59.000Z",
            "deleted_at":null
         },
         {  
            "id":1,
            "zone_name":"Uptown",
            "background_color":"#AD8DEA",
            "text_color":"#FFFFFF",
            "created_at":"2017-03-09T17:45:59.000Z",
            "updated_at":"2017-03-09T17:45:59.000Z",
            "deleted_at":null
         }
      ],
      "trainings_completed":[  

      ],
      "full_time":true,
      "contact":{  
         "phone_number":"1234567890",
         "address":{  
            "address_line_1":"2225 Hawkins St, 261",
            "address_line_2":"261",
            "city":"Charlotte",
            "zip_code":"28203",
            "state":33
         },
         "secondary_address":{  

         }
      },
      "emergency_contact":{  
         "first_name":"Scott",
         "last_name":"Huff",
         "phone_number":"1234567890"
      }
   }
}

```

Accepts multipart form data resembling a `Staff` object to create a staff user.

### HTTP Request

`POST https://waggle-api-prod.herokuapp.com/admin/createStaff`

### Request Body

Key|Required|Description
---|--------|-----------
Staff|true|Object containing form data used to create Staff

## Save Map Appointment

> Successful response is an object containing success flag':

```json
{
  "updated": true
}
```

Assigns a `Sitter` to multiple `Appointment` objects passed in an array to the server

### HTTP Request

`PUT https://waggle-api-prod.herokuapp.com/admin/saveMapAppointment`

### Request Body

Key|Required|Description
---|--------|-----------
Appointments|true|An array of Appointment objects to be saved
draft|false|Draft schedule object, if specified the changes made will not be immediately posted.

## Get Staff List

> Successful response is an array of Staff objects':

```json
[  
   {  
      "_id":"5a4fdbbaa4b87e0014fcb531",
      "hire_date":"2017-06-03T04:00:00.000Z",
      "active":true,
      "staff_type":"Employee",
      "trainings_completed":[  
         "Basic Training",
         "Consultation Training",
         "OA Training",
         "Shadow Training",
         "Event Training"
      ],
      "full_name":"Lizzy Greene",
      "full_time":true,
      "contact":{  
         "first_name":"Lizzy",
         "last_name":"Greene",
         "full_name":"Lizzy Greene",
         "email":"lizzy@thewagglecompany.com",
         "phone_number":"7045331835"
      },
      "home":{  
         "address":{  
            "address_line_1":"4413 Crestmont Dr",
            "city":"Charlotte",
            "zip_code":"28205"
         }
      },
      "zones":[  
         {  
            "deleted_at":null,
            "updated_at":"2017-03-09T17:45:59.000Z",
            "created_at":"2017-03-09T17:45:59.000Z",
            "text_color":"#FFFFFF",
            "background_color":"#57A8E5",
            "zone_name":"Noda-PM",
            "id":4
         },
         {  
            "deleted_at":null,
            "updated_at":"2017-03-09T17:45:59.000Z",
            "created_at":"2017-03-09T17:45:59.000Z",
            "text_color":"#FFFFFF",
            "background_color":"#E985C4",
            "zone_name":"South End",
            "id":2
         },
         {  
            "deleted_at":null,
            "updated_at":"2017-03-09T17:45:59.000Z",
            "created_at":"2017-03-09T17:45:59.000Z",
            "text_color":"#FFFFFF",
            "background_color":"#5CCCB3",
            "zone_name":"Cotswold",
            "id":3
         }
      ]
   },
   {  
      "_id":"5a5121b44949400014cd3dd0",
      "hire_date":"2018-01-01T05:00:00.000Z",
      "active":true,
      "staff_type":"Employee",
      "trainings_completed":[  
         "Basic Training"
      ],
      "full_name":"Luke Griffith",
      "lateness":0,
      "full_time":false,
      "contact":{  
         "first_name":"Luke",
         "last_name":"Griffith",
         "full_name":"Luke Griffith",
         "email":"luke+testtest@thewagglecompany.com",
         "phone_number":"3348053345"
      },
      "home":{  
         "address":{  
            "address_line_1":"809 West Hill St",
            "address_line_2":"Unit B",
            "city":"Charlotte",
            "zip_code":"28202"
         }
      },
      "zones":[  
         {  
            "deleted_at":null,
            "updated_at":"2017-03-09T17:45:59.000Z",
            "created_at":"2017-03-09T17:45:59.000Z",
            "text_color":"#FFFFFF",
            "background_color":"#AD8DEA",
            "zone_name":"Uptown",
            "id":1
         },
         {  
            "deleted_at":null,
            "updated_at":"2017-03-09T17:45:59.000Z",
            "created_at":"2017-03-09T17:45:59.000Z",
            "text_color":"#FFFFFF",
            "background_color":"#E985C4",
            "zone_name":"South End",
            "id":2
         }
      ]
   }
]
```

Returns an array of `Staff` users.

### HTTP Request

`GET https://waggle-api-prod.herokuapp.com/admin/staff-list?city=5a7ef4b208abad6d70537e5f`

### Query Parameters

Key|Required|Description
---|--------|-----------
city|true|ID of market to retrieve Staff from

## Get Client List

> Successful response is an array of Client objects':

```json
[  
   {  
      "_id":"5b1d81364970b50014159df8",
      "updatedAt":"2018-06-10T19:55:22.030Z",
      "createdAt":"2018-06-10T19:51:18.977Z",
      "first_name":"Aaron",
      "last_name":"Manning",
      "full_name":"Aaron Manning",
      "email":"Aaron@tarheels.com",
      "market_id":"5a7ef4b208abad6d70537e5f",
      "uid":"CJh0Mqtl3aYi5l5TlWu8N0wPui63",
      "signUpStep":4,
      "stripe_id":"cus_D1cot3gmfkbb5o",
      "time_zone":"America/New_York",
      "signup_complete":true,
      "consultation_status":"scheduled",
      "override_geocode":false,
      "team_members":[  

      ],
      "restrict_personnel":false,
      "images":[  

      ],
      "access_method":[  

      ],
      "exit_survey":[  

      ],
      "entry_survey":[  

      ],
      "has_valid_payment_method":false,
      "active":false,
      "confirmation_email_sent":true,
      "pet_ids":[  
         "5b1d822a4970b50014159dfa"
      ],
      "zones":[  

      ],
      "contact":{  
         "address":{  
            "zip_code":"28202",
            "state":"33",
            "city":"Charlotte",
            "enforce_device_within_region":true,
            "address_line_1":"530 N Poplar St",
            "address_line_2":null
         },
         "phone_number":"1234567890"
      },
      "legalAgreement":false,
      "profileReviewed":false,
      "paymentReviewed":false,
      "petReviewed":false,
      "__v":1,
      "pets":[  
         {  
            "_id":"5b1d822a4970b50014159dfa",
            "updatedAt":"2018-06-10T19:55:51.625Z",
            "createdAt":"2018-06-10T19:55:22.017Z",
            "client_id":"5b1d81364970b50014159df8",
            "origin":"Niki's Puppy House",
            "birthday_month":"January",
            "indoor":"Indoor",
            "color":"Chestnut",
            "age":"Adult",
            "sex":"Neutered Male",
            "breed":"Miniature Bull Terrier",
            "animal_type":"Dog",
            "name":"Captain",
            "approved":false,
            "active":true,
            "medicine":[  

            ],
            "__v":0,
            "profile_image_file_name":"6c3c499b-5c7e-4c80-90bc-e0be6de0c0d2.jpeg"
         }
      ]
   },
   {  
      "_id":"5a4d0b6a6fb72380abf757e2",
      "updatedAt":"2018-06-14T21:49:24.293Z",
      "createdAt":"2018-01-03T16:57:14.256Z",
      "referral_specifics":"Internet Search",
      "private_admin_notes":"If there are packages or laundry on the porch, please leave them as they are waiting to be picked up. c",
      "visit_routine":"Walk Brinkley for entire visit to burn as much energy as possible.",
      "waste_disposal":"Garbage bin in driveway.",
      "home_class_notes":"",
      "alarm_code":"Disarm: 0216. Arm: Arm+Bypass All+Away. Alarm is on left as you walk in front door.",
      "parking":"",
      "home_access_notes":"Owner's lockbox on front door handle. CODE: 0914, press top button down and pull toward you. Enter code again to close box. Enter home through front door.",
      "secured_yard":true,
      "apartment_complex":"",
      "building_type":"House",
      "email":"abgolden7@gmail.com",
      "full_name":"Abbie Golden",
      "last_name":"Golden",
      "first_name":"Abbie",
      "has_valid_payment_method":true,
      "active":true,
      "confirmation_email_sent":true,
      "home_class":{  
         "name":"Green",
         "id":1
      },
      "pet_ids":[  
         "5a4d1584a81631830fad495f",
         "5b058d144336c91f13ce827c"
      ],
      "zones":[  
         {  
            "id":4,
            "zone_name":"Noda-PM",
            "background_color":"#57A8E5",
            "text_color":"#FFFFFF",
            "created_at":"2017-03-09T17:45:59.000Z",
            "updated_at":"2017-03-09T17:45:59.000Z",
            "deleted_at":null
         }
      ],
      "emergency_contact":{  
         "first_name":"Kimberly",
         "last_name":"Golden",
         "phone_number":"5012315990"
      },
      "secondary_contact":{  
         "first_name":"Blake",
         "last_name":"Winston",
         "phone_number":null,
         "email":"09winstonb@gmail.com"
      },
      "contact":{  
         "phone_number":"5019209816",
         "address":{  
            "address_line_1":"1829 Logie Ave",
            "address_line_2":"",
            "city":"Charlotte",
            "state":"33",
            "zip_code":"28205",
            "latitude":"35.22264513423151",
            "longitude":"-80.7987217",
            "enforce_device_within_region":true
         }
      },
      "profileReviewed":false,
      "paymentReviewed":false,
      "petReviewed":false,
      "__v":11,
      "stripe_id":"cus_C4P9DTFwDlTzOw",
      "uid":"KEZt29sg56RiEWAWAKG8ySP9t4w1",
      "activation_id":null,
      "notes":"Brinkley pulls for squirrels.",
      "signup_date":"2018-01-08T00:00:00.000Z",
      "legalAgreement":true,
      "market_id":"5a7ef4b208abad6d70537e5f",
      "access_method":[  

      ],
      "entry_survey":[  
         2,
         2,
         4,
         2,
         2,
         2
      ],
      "exit_survey":[  
         2,
         2,
         4,
         2,
         2,
         2
      ],
      "images":[  
         {  
            "file_name":"https://waggle-keys-stage.s3.amazonaws.com/56aca046-f979-4e0f-a71b-98a8e9a970a6.jpeg",
            "id":"5ab2fe3d7f9ff30014591012"
         },
         {  
            "file_name":"https://waggle-keys-stage.s3.amazonaws.com/ff8c5873-2b87-41ce-a030-9f21d4c20515.jpg",
            "id":"5ab303ad4262910014aa3474"
         },
         {  
            "file_name":"https://waggle-keys-stage.s3.amazonaws.com/ff8c5873-2b87-41ce-a030-9f21d4c20515.jpg",
            "id":"5ab308cc512bb90014544f60"
         },
         {  
            "file_name":"https://waggle-keys-stage.s3.amazonaws.com/15277E3F-86DE-46A9-A282-42AFE050DB78-5596-000006549798FCC1.jpeg",
            "id":"5ab3111934b8380014e1115f"
         }
      ],
      "gender_preference":"None",
      "team_members":[  

      ],
      "restrict_personnel":false,
      "time_zone":"America/New_York",
      "override_geocode":true,
      "signup_complete":true,
      "auto_renew":{  
         "20":null,
         "40":null,
         "60":15
      },
      "bundle_size":1,
      "consultation_status":"completed",
      "pets":[  
         null,
         {  
            "_id":"5b058d144336c91f13ce827c",
            "updatedAt":"2018-05-23T15:47:32.906Z",
            "createdAt":"2018-05-23T15:47:32.906Z",
            "client_id":"5a4d0b6a6fb72380abf757e2",
            "animal_type":"Dog",
            "sex":"Neutered Male",
            "pet_class_notes":"notes",
            "size":"Medium (20 - 50 lbs)",
            "color":"Black",
            "age":"Puppy (< 1 Year)",
            "breed":"American English Coonhound",
            "name":"Doggo",
            "approved":false,
            "active":true,
            "medicine":[  

            ],
            "pet_class":{  
               "id":2,
               "name":"Yellow"
            },
            "__v":0
         }
      ]
   }
]
```

Returns an array of `Client` users

### HTTP Request

`GET https://waggle-api-prod.herokuapp.com/admin/client-list`

### Request Body

Key|Required|Description
---|--------|-----------
city|true|ID of market to get Clients from

## Get Client by ID

> Successful response is an object containing success flag':

```json
{
  "updated": true
}
```

Returns a `Client` object corresponding to the `clientId` parameter passed in URI

### HTTP Request

`GET https://waggle-api-prod.herokuapp.com/admin/clients/<clientId>`

## Edit Client

> Successful response is a Client object:

```json
{  
  "_id":"5a4d05e8360d607ef03f6053",
  "uid":"W3J1zXOixyQbPDrHOgM72xhIbo63",
  "market_id":"5a7ef4b208abad6d70537e5f",
  "apartment":{  
     "_id":"5af066dcf36d2837eae7166b",
     "name":"Inspire",
     "market_id":"5a7ef4b208abad6d70537e5f",
     "updatedAt":"2018-06-06T20:02:20.802Z",
     "createdAt":"2018-06-06T20:01:23.412Z",
     "playcare":true
  },
  "confirmation_email_sent":true,
  "signup_date":"2018-01-10T00:00:00.000Z",
  "active":true,
  "notes":"Stella is timid and may be hiding under bed.",
  "stripe_id":"cus_C2ClfvMDa9T49R",
  "visit_routine":"Take Stella on walk for potty break.",
  "secured_yard":false,
  "waste_disposal":"",
  "private_admin_notes":null,
  "restrict_personnel":false,
  "team_members":[  

  ],
  "override_geocode":false,
  "contact":{  
     "first_name":"Alexa",
     "last_name":"Glover",
     "full_name":"Alexa Glover",
     "email":"aglover@hornets.com",
     "phone_number":"9788866102"
  },
  "home":{  
     "entry_time":{  
        "name":"Really Long (9 + min)",
        "value":15
     },
     "exit_time":{  
        "name":"Really Long (9 + min)",
        "value":15
     },
     "access_method":[  

     ],
     "address":{  
        "address_line_1":"120 W. Kingston Ave",
        "address_line_2":"K-321",
        "city":"Charlotte",
        "state":{  
           "id":33,
           "name":"North Carolina",
           "abbreviation":"NC"
        },
        "zip_code":"28203",
        "latitude":"35.21412604382667",
        "longitude":"-80.85885901813832",
        "enforce_device_within_region":true
     },
     "apartment_id":"5af066dcf36d2837eae7166b",
     "building_type":"Apartment/Condo",
     "home_class":{  
        "id":2,
        "name":"Yellow"
     },
     "home_class_notes":"Apartment is in separate building as leasing office.",
     "alarm_code":"",
     "parking":"",
     "home_access_notes":"No lockbox. Check out key from leasing office, walk to 120 building, and take elevator to 3rd floor. Go left out of elevator lobby, and home is on left."
  },
  "zones":[  
     {  
        "id":2,
        "zone_name":"South End",
        "background_color":"#E985C4",
        "text_color":"#FFFFFF",
        "created_at":"2017-03-09T17:45:59.000Z",
        "updated_at":"2017-03-09T17:45:59.000Z",
        "deleted_at":null
     }
  ],
  "balances":{  
     "account":0,
     "pending":0,
     "outstanding":0
  },
  "has_valid_payment_method":true,
  "notes_list":[  

  ],
  "pets":[  
     {  
        "_id":"5a4f87161a06183b2ffcb4b0",
        "name":"Stella",
        "active":true,
        "animal_type":"Dog",
        "image_url":"https://waggle-keys-stage.s3.amazonaws.com/3289cb97-3d1e-400e-a853-4488772e3de9.jpg",
        "breed":"Pomeranian",
        "sex":"Spayed Female",
        "gender_preference":"",
        "age":"Adult",
        "color":"Black, Tan and White",
        "size":"S (<20)",
        "harness":"",
        "litterbox":"",
        "pet_location":"Free roaming.",
        "leash_collar":"Leash on table by front door.",
        "toy_info":"",
        "personality":"Friendly, but timid.",
        "pet_class_id":2,
        "pet_class":{  
           "name":"Yellow",
           "id":2
        },
        "birthday_month":"April",
        "pet_class_notes":"Stella was attacked by a dog about a year ago, and she is scared of other dogs.",
        "food":{  
           "bowl_location":"Bowls in kitchen.",
           "food_location":"Food in closet between front door and kitchen.",
           "brand_of_food":"",
           "food_instructions":"Stella grazes on food. If bowl is empty, refill.",
           "treat_info":"",
           "water_instructions":""
        },
        "medical":{  
           "allergies":"",
           "medications":[  

           ]
        },
        "vet":{  
           "vet_clinic":"Dilworth Animal Hospital",
           "phone":"704-808-7387",
           "address_line_1":"814 East Blvd",
           "address_line_2":null,
           "city":"Charlotte",
           "state":33,
           "zip_code":"28203"
        }
     }
  ],
  "cards":[  

  ],
  "line_items":[  

  ],
  "appointments":[  
     {  
        "_id":"5a6b6be0a064e50014f18ca6",
        "sitter":{  
           "full_name":null,
           "_id":null
        },
        "appointment_status":{  
           "id":3,
           "name":"Change Requested"
        },
        "appointment_type":{  
           "id":20,
           "name":"20 Minutes",
           "duration_in_minutes":20
        },
        "created_at":"2018-01-26T17:56:48.647Z",
        "updated_at":"2018-06-26T14:58:54.125Z",
        "price":2000,
        "pets":[  

        ],
        "recurrence":{  
           "is_recurring":false,
           "weekdays":null
        },
        "client_notes":"sdfasfd",
        "sitter_notes_to_client":"Stella is such a sweetie! 😍 She was a little nervous at first and went under the bed 🛏 after seeing me come in. She came out when I got a beggin strip for her 🥓 I put the leash on her once we were acquainted and we headed downstairs and outside for her walk. Stella went pee as soon as we got to the grass 👏 She also went 💩 later on. I walked her up and down Kingston and Hawkins because I was a little worried she would be scared to walk on the busier streets. At one point there was a lot of dogs 🐕 walking around us so I put her up on a stoop and she enjoyed being tall even for just a minute 😉 She is just too stinkin’ cute, I didn’t want to leave her!! I can’t wait until the next time I get to walk her! 😊",
        "duration_in_minutes":20,
        "addons":[  
           {  
              "id":1,
              "name":"Pee",
              "pet_id":"5b046fc6511d5f41e1dc7039"
           },
           {  
              "id":2,
              "name":"Poop",
              "pet_id":"5b046fc6511d5f41e1dc7039"
           },
           {  
              "id":1,
              "name":"Pee",
              "pet_id":"5b04764e511d5f41e1dc703a"
           },
           {  
              "id":2,
              "name":"Poop",
              "pet_id":"5b04764e511d5f41e1dc703a"
           },
           {  
              "id":7,
              "name":"Turn On Lights",
              "pet_id":null
           },
           {  
              "id":4,
              "name":"Give Medication",
              "pet_id":"5b046fc6511d5f41e1dc7039"
           },
           {  
              "id":3,
              "name":"Provide Meal",
              "pet_id":"5b04764e511d5f41e1dc703a"
           }
        ],
        "scheduled_start_time":null,
        "scheduled_end_time":null,
        "window_start_time":"Fri Jan 26 2018 10:00",
        "window_end_time":"Fri Jan 26 2018 11:30"
     },
     {  
        "_id":"5aa03d67b7a9a80014b8572c",
        "sitter":{  
           "full_name":"Austin Semple",
           "_id":"5a57b08afb3833c6c51e1da0"
        },
        "appointment_status":{  
           "id":3,
           "name":"Change Requested"
        },
        "appointment_type":{  
           "id":20,
           "name":"20 Minutes",
           "duration_in_minutes":20
        },
        "created_at":"2018-03-07T19:28:39.594Z",
        "updated_at":"2018-06-26T15:03:03.962Z",
        "price":2000,
        "pets":[  

        ],
        "recurrence":{  
           "is_recurring":false,
           "weekdays":[  

           ]
        },
        "client_notes":"sdfasfd",
        "duration_in_minutes":20,
        "addons":[  
           {  
              "id":1,
              "name":"Pee",
              "pet_id":"5b046fc6511d5f41e1dc7039"
           },
           {  
              "id":2,
              "name":"Poop",
              "pet_id":"5b046fc6511d5f41e1dc7039"
           },
           {  
              "id":1,
              "name":"Pee",
              "pet_id":"5b04764e511d5f41e1dc703a"
           },
           {  
              "id":2,
              "name":"Poop",
              "pet_id":"5b04764e511d5f41e1dc703a"
           },
           {  
              "id":7,
              "name":"Turn On Lights",
              "pet_id":null
           },
           {  
              "id":4,
              "name":"Give Medication",
              "pet_id":"5b046fc6511d5f41e1dc7039"
           },
           {  
              "id":3,
              "name":"Provide Meal",
              "pet_id":"5b04764e511d5f41e1dc703a"
           }
        ],
        "scheduled_start_time":"Wed Mar 07 2018 15:25:00 GMT-0500 (EST)",
        "scheduled_end_time":"2018-03-07T20:45:00.000Z",
        "window_start_time":"Wed Mar 7 2018 10:00",
        "window_end_time":"Wed Mar 7 2018 11:30"
     }
  ],
  "secondary_contact":{  
     "first_name":"",
     "last_name":"",
     "full_name":" ",
     "email":"",
     "phone_number":""
  },
  "emergency_contact":{  
     "first_name":"",
     "last_name":"",
     "full_name":" ",
     "phone_number":""
  }
}
```

Updates `Client` object specified in `clientId` parameter of URI

### HTTP Request

`PUT https://waggle-api-prod.herokuapp.com/admin/clients/<clientId>`

### Request Body

Key|Required|Description
---|--------|-----------
Client|true|Client object to update

## Update Client Activation

> Successful response is an object containing success flag':

```json
{
  "success": true
}
```

Updates `Client` corresponding to `clientId` passed in parameters and sets their status
as active or inactive.

### HTTP Request

`PUT https://waggle-api-prod.herokuapp.com/admin/clients/<clientId>/activation`

### Request Body

Key|Required|Description
---|--------|-----------
active|false|Boolean flag to set status. If missing Client will be set inactive

## Add Pet

> Successful response is an object containing success flag and newly created pet object':

```json
{  
   "success":true,
   "pet":{  
      "__v":0,
      "updatedAt":"2018-06-27T15:59:49.343Z",
      "createdAt":"2018-06-27T15:59:49.343Z",
      "pet_class_notes":"",
      "client_id":"5b06e488374c820ae73772f1",
      "animal_type":"Dog",
      "sex":"Unknown",
      "rabies_vaccination_date":"2018-06-27T00:00:00.000Z",
      "size":"Extra Large (>80 lbs)",
      "color":"Brown",
      "age":"Adult",
      "breed":"Great Dane",
      "name":"Scooby Doo",
      "_id":"5b33b4756092a281b2c7bda8",
      "approved":false,
      "active":true,
      "medicine":[  

      ],
      "pet_class":{  
         "id":1,
         "name":"Green"
      }
   }
}
#1

```

Creates `Pet` object associated with `Client` specified by `clientId` parameter
in URI. Takes multipart form data that specifies a `Pet` object and `file` which is a profile image.

### HTTP Request

`POST https://waggle-api-prod.herokuapp.com/admin/clients/<clientId>/pets`

### Request Body

Key|Required|Description
---|--------|-----------
Pet|true|Pet object to be saved for Client

### File
Key|Required|Description
profile_image|false|Profile image to use for pet that is added

## Update Pet

> Successful response is an object containing updated pet object':

```json
{  
   "_id":"5b33b4756092a281b2c7bda8",
   "updatedAt":"2018-06-27T16:04:47.227Z",
   "createdAt":"2018-06-27T15:59:49.343Z",
   "pet_class_notes":"",
   "client_id":"5b06e488374c820ae73772f1",
   "animal_type":"Dog",
   "sex":"Unknown",
   "rabies_vaccination_date":"2018-06-26T04:00:00.000Z",
   "size":"Extra Large (>80 lbs)",
   "color":"Brown",
   "age":"Puppy (< 1 Year)",
   "breed":"Great Dane",
   "name":"Scrappy Doo",
   "__v":0,
   "approved":false,
   "active":true,
   "medicine":[  

   ],
   "pet_class":{  
      "id":1,
      "name":"Green"
   }
}
```

Updates `Pet` object specified by `petId` included in the URI. Accepts multipart form data
consisting of a `Pet` object and a `profile_image` file

### HTTP Request

`PUT https://waggle-api-prod.herokuapp.com/admin/clients/pets/<petId>`

### Request Body

Key|Required|Description
---|--------|-----------
Pet|true|Pet object to be saved for Client

### File
Key|Required|Description
profile_image|false|Profile image to use for pet that is added

## Deactivate Pet

> Successful response is an object containing success flag':

```json
{
  "success": true
}
```

Deactivates `Pet` object by `petId` specified in URI.  Calling this action will remove
the pet from any pending, approved or change-requested `Appointment`

### HTTP Request

`PUT https://waggle-api-prod.herokuapp.com/admin/pets/<petId>/deactivate`


## Get Staff Data

> Successful response is an object containing Staff and Appointment arrays':

```json
{  
   "staff":[
      {  
         "_id":"5a9854b779af2a001489a06f",
         "appointments":[  

         ],
         "hire_date":"2018-03-02T00:00:00.000Z",
         "staff_type":"Employee",
         "contact":{  
            "first_name":"Chloe",
            "last_name":"Chicola",
            "full_name":"Chloe Chicola",
            "email":"chloe.chicola76@gmail.com",
            "phone_number":"(904) 440-4421"
         },
         "home":{  
            "address":{  
               "address_line_1":"tbd",
               "city":"tbd",
               "zip_code":"tbd"
            }
         },
         "zones":[  
            {  
               "deleted_at":null,
               "updated_at":"2017-03-09T17:45:59.000Z",
               "created_at":"2017-03-09T17:45:59.000Z",
               "text_color":"#FFFFFF",
               "background_color":"#AD8DEA",
               "zone_name":"Uptown",
               "id":1
            }
         ]
      }
   ],
   "appointments":[  
      {  
         "_id":"5b23d58a7be4b2b25b5428a0",
         "updatedAt":"2018-06-26T15:00:26.057Z",
         "createdAt":"2018-06-15T15:04:42.767Z",
         "visit_date":"2018-06-16T15:30:00.000Z",
         "kml":null,
         "client_notes":"",
         "window_start_time":"Sat Jun 16 2018 11:30",
         "window_end_time":"Sat Jun 16 2018 13:00",
         "actual_start_time":null,
         "actual_end_time":null,
         "appointment_status_id":2,
         "client_id":"5afadc9d556397001462d25f",
         "exclude_from_scheduler":false,
         "en_route":false,
         "clear_notes_from_dashboard":false,
         "clear_from_dashboard":false,
         "sitter_viewed":false,
         "add_on_services":[  

         ],
         "recurrence_weekdays":[  

         ],
         "price_overridden":false,
         "images":[  

         ],
         "requires_tracking":true,
         "override_device_within_region":false,
         "appointment_status":{  
            "id":2,
            "name":"Approved"
         },
         "appointment_type":{  
            "duration_in_minutes":40,
            "name":"40 Minutes",
            "id":40
         },
         "pet_ids":[  
            "5afb2c8934c3e50014b054e2"
         ],
         "pets":[  

         ],
         "__v":0,
         "visit_date_string":"06-16-2018",
         "client":{  
            "_id":"5afadc9d556397001462d25f",
            "updatedAt":"2018-06-25T17:35:13.909Z",
            "createdAt":"2018-05-15T13:11:57.840Z",
            "time_zone":"America/New_York",
            "stripe_id":"cus_CrmVzQ8h97BmdN",
            "secured_yard":false,
            "signup_date":"2018-05-13T00:00:00.000Z",
            "email":"scott+client@thewagglecompany.com",
            "market_id":"5a7ef4b208abad6d70537e5f",
            "full_name":"scott huff",
            "last_name":"huff",
            "first_name":"scott",
            "override_geocode":false,
            "team_members":[  

            ],
            "restrict_personnel":false,
            "images":[  

            ],
            "access_method":[  

            ],
            "exit_survey":[  
               2
            ],
            "entry_survey":[  
               2
            ],
            "has_valid_payment_method":true,
            "active":true,
            "confirmation_email_sent":true,
            "pet_ids":[  
               "5afb2c8934c3e50014b054e2",
               "5b311100dbb46f80e2815192",
               "5b3127d1ab69a811428310fb"
            ],
            "zones":[  

            ],
            "contact":{  
               "phone_number":"2342343232",
               "address":{  
                  "address_line_1":"809 w. hill st",
                  "city":"charlotte",
                  "state":"33",
                  "zip_code":"28202",
                  "latitude":"35.22819079675003",
                  "longitude":"-80.85664215897583",
                  "enforce_device_within_region":false,
                  "map_image_file_name":"8895271d-faf6-45b2-8cbe-d985e8c22fdb.png",
                  "street_view_image_file_name":"6011a69f-f04d-4775-9d59-9c83d38fc3ec.jpg"
               }
            },
            "legalAgreement":true,
            "profileReviewed":false,
            "paymentReviewed":false,
            "petReviewed":true,
            "__v":4,
            "uid":"EoNMkYxCdtX3p9ywzFJrXntN6Qz2",
            "activation_id":"3cfc6044-47b5-474b-8cca-18b498263e7a",
            "signup_complete":true,
            "bundle_size":5,
            "auto_renew":{  
               "20":0,
               "40":0,
               "60":0
            },
            "emergency_contact":{  

            },
            "secondary_contact":{  

            },
            "home_class":null,
            "signUpStep":4,
            "consultation_status":"completed",
            "apartment_id":"5b183e10577cdd159c502d7a"
         },
         "price":0,
         "credit":null
      }
   ]
}
```

Returns array of `Staff` objects with their corresponding `Appointment` list in the given
time interval.  Separate `Appointment` list is returned for the specified interval as well

### HTTP Request

`GET https://waggle-api-prod.herokuapp.com/admin/staffData`

### Query Parameters

Key|Required|Description
---|--------|-----------
market|true|ID of market to retrieve Staff data from
startDate|false|Beginning of time interval to retrieve Staff Data, default is beginning of current week
endDate|false|End of time interval to retrieve Staff Data, default is end of current week

## Staff Mileage

> Successful response is an array containing objects corresponding to mileage per day:

```json
[  
   {  
      "date":"2018-06-25T04:00:00.000Z",
      "mileage":10.804739999999999
   },
   {  
      "date":"2018-06-26T04:00:00.000Z",
      "mileage":5.712680000000001
   }
]
```

Retrieves total mileage for `Staff` object specified by `staffId` in URI over a
specified time interval.  Default interval is the current week.

### HTTP Request

`GET https://waggle-api-prod.herokuapp.com/admin/staffMileage/<staffId>`

### Request Body

Key|Required|Description
---|--------|-----------
startDate|false|Beginning of time interval to retrieve Staff Data, default is beginning of current week
endDate|false|End of time interval to retrieve Staff Data, default is end of current week

## Get Staff by ID

> Successful response is an Staff object:

```json
{  
   "roles":[  
      "admin",
      "oa",
      "sitter"
   ],
   "uid":"lkbeheaKbLOXlAB8JvU2KwSmaJk2",
   "_id":"5afadb95556397001462d25e",
   "market_id":"5a7ef4b208abad6d70537e5f",
   "active":true,
   "hire_date":"2018-05-15T04:00:00.000Z",
   "dob":"1900-12-01T00:00:00.000Z",
   "gender":"Male",
   "trainings_completed":[  

   ],
   "use_secondary_for_routing":false,
   "use_break":false,
   "full_time":false,
   "contact":{  
      "first_name":"scott",
      "last_name":"huff",
      "full_name":"scott huff",
      "email":"scott@thewagglecompany.com",
      "phone_number":"0928098098"
   },
   "emergency_contact":{  
      "full_name":"undefined undefined"
   },
   "home":{  
      "address":{  
         "state":{  
            "id":33,
            "name":"North Carolina",
            "abbreviation":"NC"
         },
         "latitude":35.7595731,
         "longitude":-79.01929969999999
      },
      "secondary_address":{  

      }
   },
   "zones":[  

   ]
}
```

Returns a `Staff` object specified by `staffId` in URI.

### HTTP Request

`GET https://waggle-api-prod.herokuapp.com/admin/staff/<staffId>`

## Edit Staff

> Successful response is an object containing a success flag:

```json
{
  "success": true
}
```

Updates a `Staff` object specified by `staffId` in URI.

### HTTP Request

`PUT https://waggle-api-prod.herokuapp.com/admin/staff/<staffId>`

### Request Body

Key|Required|Description
---|--------|-----------
Staff|true|Staff object to update

## Activate Staff

> Successful response is an object containing a success flag:

```json
{
  "success":true
}
```

Sets `active` property of a `Staff` object specified by `staffId` in URI. Setting
`active` to false will result in the `Staff` member being removed from all future
`Appointments`

### HTTP Request

`PUT https://waggle-api-prod.herokuapp.com/admin/staff/<staffId>/activation`

### Request Body

Key|Required|Description
---|--------|-----------
active|false|Boolean that sets active. If active is not specified it is treated as false.

## Get Appointments

> Successful response is an array of Appointment objects:

```json
[{  
      "recurrence_id":"adaffa36-0f66-42ff-9edf-a05aa0b1886f",
      "_id":"5a5646ab740a01a84da2a163",
      "client_id":"5a4d05e8360d607ef03f6054",
      "updatedAt":"2018-06-26T14:56:59.947Z",
      "appointment_status":{  
         "id":2,
         "name":"Approved"
      },
      "appointment_type":{  
         "id":2,
         "name":"20 Min Visit (Puppy; Schedule 2+ visits/day)",
         "duration_in_minutes":20
      },
      "created_at":"2018-01-10T17:00:27.547Z",
      "updated_at":"2018-06-26T14:56:59.947Z",
      "price":1300,
      "recurrence":{  
         "is_recurring":true,
         "weekdays":[  
            "Monday",
            "Tuesday",
            "Wednesday",
            "Thursday",
            "Friday"
         ],
         "recurrence_end_date":"2018-12-13T05:00:00.000Z"
      },
      "client_notes":"Hi Waggle! A few things: please check the crate for accidents, please wipe his bum with a baby wipe (located above trashcan) if he poops, and see if you can get him to sip some water (unlikely lol).  If he spits up or has a loose poop, please let us know. But most of all please give our boy some love. He loves his Waggle fur-fiends!! Thank you so much!!",
      "en_route":false,
      "admin_notes_to_sitter":"",
      "duration_in_minutes":20,
      "addons":[  
         {  
            "id":1,
            "name":"Pee",
            "pet_id":"5a4f87161a06183b2ffcb4ae"
         },
         {  
            "id":2,
            "name":"Poop",
            "pet_id":"5a4f87161a06183b2ffcb4ae"
         }
      ],
      "scheduled_start_time":null,
      "scheduled_end_time":null,
      "window_start_time":"Wed Jun 27 2018 11:30",
      "window_end_time":"Wed Jun 27 2018 13:00",
      "sitter":{  
         "_id":null,
         "full_name":null
      },
      "sitter_id":null,
      "time_zone":"America/New_York",
      "contact":{  
         "client_id":"5a4d05e8360d607ef03f6054",
         "first_name":"Alana",
         "last_name":"Van Ness",
         "full_name":"Alana Van Ness",
         "email":"ajlinn521@gmail.com",
         "time_zone":"America/New_York"
      },
      "pets":[  
         {  
            "_id":"5a4f87161a06183b2ffcb4ae",
            "name":"Hamilton",
            "image_url":"https://waggle-keys-stage.s3.amazonaws.com/230f2a69-4712-4bff-852b-83df9783056f.jpg",
            "pet_class":"Green",
            "pet_class_notes":"",
            "gender_preference":""
         }
      ],
      "home":{  
         "home_class":"Yellow",
         "home_class_notes":"Back door locks automatically--do not shut back door while walking Hamilton in yard!",
         "admin_client_notes":"Hamilton MUST be on leash while outside!",
         "zones":[  
            {  
               "id":4,
               "zone_name":"Noda-PM",
               "background_color":"#57A8E5",
               "text_color":"#FFFFFF",
               "created_at":"2017-03-09T17:45:59.000Z",
               "updated_at":"2017-03-09T17:45:59.000Z",
               "deleted_at":null
            }
         ],
         "address":{  
            "enforce_device_within_region":true,
            "street_view_image_file_name":"78d16724-f26e-4bdd-be92-f4dac4bdf96c.jpg",
            "map_image_file_name":"385babbd-4541-472e-b6b1-e058c363ea6b.png",
            "longitude":"-80.80350271919546",
            "latitude":"35.22543242810814",
            "zip_code":"28205",
            "state":"33",
            "city":"Charlotte",
            "address_line_2":"",
            "address_line_1":"2012 Ashland Avenue"
         }
      }
   }]
```

Returns a list of `Appointment` objects based on the parameters specified.

### HTTP Request

`GET https://waggle-api-prod.herokuapp.com/admin/appointments?city=5a7ef4b208abad6d70537e5f`

### Query Parameters

Key|Required|Description
---|--------|-----------
city|true|ID of market to get Appointments for
draft|false|Draft schedule object. If specified, the call will return the Draft schedule for that market
startDate|false|Beginning of time interval to retrieve Appointments for. Default is beginning of current day
endDate|false|End of time interval to retrieve Appointments for. Default is end of current day
recurrence_id|false|ID that returns all Appointments from a recurring series

## Get Appointment by ID

> Successful response is an Appointment object

```json
{  
   "_id":"5b2d341e45341a00143f2aa6",
   "client_id":"5a4d51ff1e121f0014902ffd",
   "market_id":"5a7ef4b208abad6d70537e5f",
   "appointment_status":{  
      "name":"Approved",
      "id":2
   },
   "appointment_type":{  
      "duration_in_minutes":40,
      "name":"40 Min Visit",
      "id":40
   },
   "created_at":"2018-06-22T17:38:38.972Z",
   "updated_at":"2018-06-26T15:04:10.753Z",
   "price_overridden":false,
   "calculated_price":null,
   "client_notes":"",
   "duration_in_minutes":40,
   "time_zone":"America/New_York",
   "add_on_services":[  
      {  
         "id":1,
         "name":"Pee",
         "completed":false,
         "pet_id":"5a4f9648a4b87e0014fcb529"
      },
      {  
         "id":2,
         "name":"Poop",
         "completed":false,
         "pet_id":"5a4f9648a4b87e0014fcb529"
      }
   ],
   "scheduled_start_time":null,
   "window_start_time":"Wed Jun 27 2018 10:30",
   "visit_date":"2018-06-27T06:30:00.000Z",
   "window_end_time":"Wed Jun 27 2018 12:00",
   "recurrence":{  
      "recurrence_id":"6888d044-73af-41ec-aa2d-178590688632",
      "is_recurring":true,
      "weekdays":[  
         "Monday",
         "Wednesday",
         "Friday"
      ],
      "start_date":"Mon Jun 25 2018 12:00",
      "end_date":"Fri Aug 10 2018 12:00"
   },
   "window_end_date":"Fri Aug 10 2018 12:00",
   "kml":null,
   "raw_location_dump":null,
   "appointment_images":[  

   ],
   "sitter":{  

   },
   "appointment_pet_ids":[  
      "5a4f9648a4b87e0014fcb529"
   ],
   "exclude_from_scheduler":false,
   "all_client_pets":[  
      {  
         "_id":"5a4f9648a4b87e0014fcb529",
         "name":"Alfie",
         "active":true,
         "animal_type":"Dog",
         "is_on_appointment":true,
         "image_url":"https://waggle-keys-stage.s3.amazonaws.com/f46e8625-a261-477d-a969-fbde78912816.jpg",
         "breed":"Poodle Mix",
         "age":"Adult",
         "color":"Cream",
         "pet_location":"Free roaming",
         "leash_collar":"Grey leash on hook in entry way",
         "toy_info":"Loves squeaky toys - on bedroom floor",
         "pet_class":{  

         },
         "food":{  
            "bowl_location":"Right of bedroom door",
            "food_instructions":"1/2 cup 2x/day - add splash of Swanson chicken broth from fridge door"
         },
         "medical":{  
            "allergies":"Grain-free",
            "medications":[  

            ]
         },
         "vet":{  
            "phone":"(704) 808-7387",
            "address_line_1":"814 East Blvd",
            "address_line_2":null,
            "city":"Charlotte",
            "state":33,
            "zip_code":"28203"
         }
      }
   ],
   "contact":{  
      "client_id":"5a4d51ff1e121f0014902ffd",
      "first_name":"Niki",
      "last_name":"Chimberg",
      "full_name":"Niki Chimberg",
      "email":"niki+alfie@thewagglecompany.com",
      "phone_number":"6174486660"
   },
   "home":{  
      "address":{  
         "address_line_1":"2522 McClintock Rd",
         "address_line_2":"Unit 205",
         "city":"Charlotte",
         "state":"NC",
         "zip_code":"28205",
         "map_image_url":"https://waggle-keys-stage.s3.amazonaws.com/54ee432d-dd86-4322-9038-12986701ef6e.png",
         "street_view_image_url":"https://waggle-keys-stage.s3.amazonaws.com/33d94af3-fa35-4347-951f-639f1a83a1ef.jpg",
         "coordinates":{  
            "latitude":"35.21516932126725",
            "longitude":"-80.80256179361571"
         },
         "enforce_device_within_region":true
      },
      "zone":{  
         "id":4,
         "zone_name":"Noda-PM",
         "background_color":"#57A8E5",
         "text_color":"#FFFFFF",
         "created_at":"2017-03-09T17:45:59.000Z",
         "updated_at":"2017-03-09T17:45:59.000Z",
         "deleted_at":null
      },
      "tz_locale":"America/New_York",
      "parking":"Park anywhere",
      "home_access_notes":"Leasing office on Lorna between McClintock & Ivey. Get fob for L205. Second floor - no elevator.",
      "home_class":{  
         "id":1,
         "name":"Green"
      },
      "notes":null
   },
   "line_items":[  

   ],
   "walk_credits":[  

   ]
}
```

Returns `Appointment` object specified by `appointmentId` parameter in the URI.

### HTTP Request

`GET https://waggle-api-prod.herokuapp.com/admin/appointments/<appointmentId>`

## Create Appointment

> Successful response is an object containing a success flag and array of Appointments created:

```json
{  
   "success":true,
   "appointments":[  
      {  
         "__v":0,
         "updatedAt":"2018-06-27T18:12:41.983Z",
         "createdAt":"2018-06-27T18:12:41.983Z",
         "market_id":"5a7ef4b208abad6d70537e5f",
         "visit_date":"2018-06-27T17:28:01.219Z",
         "window_end_time":"Wed Jun 27 2018 14:00",
         "window_start_time":"Wed Jun 27 2018 13:20",
         "client_id":"5b06e488374c820ae73772f1",
         "appointment_status_id":1,
         "_id":"5b33d399c20dcd008f838601",
         "client_confirmed":false,
         "exclude_from_scheduler":false,
         "en_route":false,
         "clear_notes_from_dashboard":false,
         "clear_from_dashboard":false,
         "sitter_viewed":false,
         "add_on_services":[  
            {  
               "pet_id":"5b115fcc6cc1854ce25fe170",
               "completed":false,
               "name":"Pee",
               "id":1
            },
            {  
               "pet_id":"5b115fcc6cc1854ce25fe170",
               "completed":false,
               "name":"Poop",
               "id":2
            },
            {  
               "pet_id":"5b115fe56cc1854ce25fe171",
               "completed":false,
               "name":"Pee",
               "id":1
            },
            {  
               "pet_id":"5b115fe56cc1854ce25fe171",
               "completed":false,
               "name":"Poop",
               "id":2
            },
            {  
               "pet_id":"5b115ffa6cc1854ce25fe172",
               "completed":false,
               "name":"Pee",
               "id":1
            },
            {  
               "pet_id":"5b115ffa6cc1854ce25fe172",
               "completed":false,
               "name":"Poop",
               "id":2
            }
         ],
         "recurrence_weekdays":[  

         ],
         "price_overridden":false,
         "images":[  

         ],
         "requires_tracking":true,
         "override_device_within_region":false,
         "appointment_status":{  
            "id":1,
            "name":"Pending"
         },
         "appointment_type":{  
            "id":20,
            "name":"20 Min Visit",
            "duration_in_minutes":20
         },
         "pet_ids":[  
            "5b115fcc6cc1854ce25fe170",
            "5b115fe56cc1854ce25fe171",
            "5b115ffa6cc1854ce25fe172"
         ],
         "pets":[  

         ]
      }
   ]
}

```

Creates one or many `Appointment` objects. To create multiple `Appointment` objects,
`is_recurring` flag must be set to `true`, an array of `weekdays` and `startDate` for
the recurring series must also be specified.

### HTTP Request

`POST https://waggle-api-prod.herokuapp.com/admin/appointments`

### Request Body

Key|Required|Description
---|--------|-----------
Appointment|true|Appointment object used to create one or many Appointments

## Approve Appointment

> Successful response is an object containing a success flag:

```json
{
  "success":true
}
```

Sets `appointment_status` of `Appointment` specified by `appointmentId` parameter
in URI equal to "Approved".  When `Appointment` is approved the `Client` who requested
the `Appointment` receives a text message along with the `Client.secondary_contact` if
specified.

### HTTP Request

`PUT https://waggle-api-prod.herokuapp.com/admin/appointments/<appointmentId>/approve`

### Request Body

Key|Required|Description
---|--------|-----------
Appointment|true|Appointment object to approve

## Reject Appointment

Sets `appointment_status` of `Appointment` specified by `appointmentId` parameter
in URI equal to "Rejected".  When `Appointment` is rejected the `Client` who requested
the `Appointment` receives a text message along with the `Client.secondary_contact` stating
the `rejection_reason` which by default is "No reason provided".

### HTTP Request

`PUT https://waggle-api-prod.herokuapp.com/admin/appointments/<appointmentId>/reject`

### Request Body

Key|Required|Description
---|--------|-----------
Appointment|true|Appointment object to reject

## Edit Appointment

> Successful response is an object containing a success flag:

```json
{
  "success":true
}
```

Updates `Appointment` object specified by `appointmentId` parameter. If updating
an `Appointment` with a specified `recurrence_id`, `weekdays_changed` or `series_changed`
must be specified to update `weekdays` or `window_end_date` properties.  If not updating
`weekdays` or `window_end_date`, the `Appointment` details will be updated for every
`Appointment` in the series with the exception of `appointment_status`.  For non-recurring
`Appointment`, the single object is updated.

### HTTP Request

`PUT https://waggle-api-prod.herokuapp.com/admin/appointments/<appointmentId>`

### Request Body

Key|Required|Description
---|--------|-----------
Appointment|true|Appointment object to reject

## Reject Appointment

> Successful response is an object containing a canceled flag:

```json
{
  "canceled":true
}
```

Sets `appointment_status` of `Appointment` specified by `appointmentId` parameter
in URI equal to "Canceled".  When `Appointment` is canceled, if the call is made within
1 hour of `window_start_time` a `WalkCredit` object is updated to `used`: true, or a
`LineItem` with `amount` equal to `Prices` object for that `appointment_type` or a default
of $10.  If call is made after 8AM on `visit_date` a flat rate `LineItem` is created for
$5, and otherwise there is no Cancellation fee. Cancellation fees can be waived and if
`Appointment` is part of a recurring series, all `Appointment` objects with matching
`recurrence_id` values may be deleted if specified in parameters.

### HTTP Request

`PUT https://waggle-api-prod.herokuapp.com/admin/appointments/<appointmentId>/reject`

### Request Body

Key|Required|Description
---|--------|-----------
shouldCancelSeries|false|Defaults to false. If specified true, all Appointments with matching recurrence_id values are deleted
waiveLatePenalty|false|Defaults to false. If specified true, no WalkCredit or LineItem objects are affected by cancellation

## Set Payment Method

> Successful response is an object containing a success flag:

```json
{
  "success":true
}
```

Sends a `Source` object to Stripe API to process future `LineItem` objects.  For more
information about Stripe's Source API, follow this link https://stripe.com/docs/sources.
After `Source` object is sent to Stripe, `Client.has_valid_payment_method` is set to true.
Previous cards added to Stripe are then removed.

### HTTP Request

`POST https://waggle-api-prod.herokuapp.com/admin/clients/<clientId>/payment-method/set`

### Request Body

Key|Required|Description
---|--------|-----------
Source|true|Stripe Source object to create payment source

## Add Line item

> Successful response is an object containing a success flag:

```json
{
  "success":true
}
```

Creates `LineItem` object. If the system hasn't already created the first `LineItem`
(appointment charge or late cancellation fee), an exception is thrown.  If the `Appointment`
doesn't belong to the `Client` a separate exception is thrown.


### HTTP Request

`POST https://waggle-api-prod.herokuapp.com/admin/line-items/add`

### Request Body

Key|Required|Description
---|--------|-----------
LineItem|true|LineItem object to create

## Review Line Items

> Successful response is an array of objects containing Client object and LineItem array:

```json
[
  {
      "client":{  
         "_id":"5a5eb6c748cb060014effba1",
         "updatedAt":"2018-05-18T19:34:25.374Z",
         "createdAt":"2018-01-17T02:36:55.527Z",
         "uid":"mqs6uGHvSfU90QPAq8WCy5nm1kB3",
         "stripe_id":"cus_C9Pc8JroF1ezML",
         "secured_yard":false,
         "signup_date":"2018-01-12T00:00:00.000Z",
         "email":"kmdinla@yahoo.com",
         "full_name":"Kathleen Davis",
         "last_name":"Davis",
         "first_name":"Kathleen",
         "__v":5,
         "visit_routine":"Jamie may bark when you arrive but he'll calm down! Walk for entire visit.",
         "home_access_notes":"Lockbox on front door. CODE: 386.",
         "parking":"In driveway.",
         "building_type":"House",
         "alarm_code":"DISARM: 7674 + Off, ARM: 7674 + Away. Alarm by garage door, turn left & left down hallway after entering home.",
         "activation_id":null,
         "notes":"Owner's father may be home during visit. ",
         "market_id":"5a7ef4b208abad6d70537e5f",
         "gender_preference":"None",
         "time_zone":"America/New_York",
         "signup_complete":true,
         "consultation_status":"unscheduled",
         "override_geocode":false,
         "team_members":[  

         ],
         "restrict_personnel":false,
         "images":[  

         ],
         "access_method":[  

         ],
         "exit_survey":[  
            2,
            2,
            2,
            2
         ],
         "entry_survey":[  
            2,
            2,
            2,
            2
         ],
         "has_valid_payment_method":true,
         "active":true,
         "confirmation_email_sent":true,
         "home_class":{  
            "name":"Green",
            "id":1
         },
         "pet_ids":[  
            "5a5faf5855f0b00014956b18"
         ],
         "zones":[  
            {  
               "deleted_at":null,
               "updated_at":"2017-03-09T17:45:59.000Z",
               "created_at":"2017-03-09T17:45:59.000Z",
               "text_color":"#FFFFFF",
               "background_color":"#F27C7C",
               "zone_name":"Matthews",
               "id":7
            }
         ],
         "contact":{  
            "phone_number":"(386) 566-8538",
            "address":{  
               "address_line_1":"7514 Shadowstone Dr. ",
               "city":"Charlotte",
               "state":"33",
               "zip_code":"28270",
               "latitude":"35.14234091244655",
               "longitude":"-80.75670512438111",
               "map_image_file_name":"8ca3cbcb-a3c5-4718-9dc6-859d009dc913.png",
               "street_view_image_file_name":"f0845ac7-c78e-41ea-88aa-89a5680211ee.jpg",
               "enforce_device_within_region":true
            }
         },
         "legalAgreement":true,
         "profileReviewed":false,
         "paymentReviewed":false,
         "petReviewed":false
      },
      "line_items":[  
         {  
            "_id":"5b1dea7bcf3fe32355b5b4c1",
            "updatedAt":"2018-06-11T03:20:27.496Z",
            "createdAt":"2018-06-11T03:20:27.496Z",
            "client_id":"5a5eb6c748cb060014effba1",
            "amount":22500,
            "description":"15-walk bundle (20-min visits).",
            "__v":0
         },
         {  
            "_id":"5b1dea31dd8e42234549a1d3",
            "updatedAt":"2018-06-11T03:19:13.581Z",
            "createdAt":"2018-06-11T03:19:13.581Z",
            "client_id":"5a5eb6c748cb060014effba1",
            "amount":22500,
            "description":"15-walk bundle (20-min visits).",
            "__v":0
         }
      ],
      "total":45000
   }
 ]
```

Returns list containing objects with `Client` object and an array of their
associated `LineItem` objects.


### HTTP Request

`GET https://waggle-api-prod.herokuapp.com/admin/reviewPayments`

## Process Payments

> Successful response is an objects to update the UI on status of job:

```json
{ "status": 1, "num_payments": 95 }
{ "status": 2, "message": "failed", "num_payments": 95 }
{  
   "status":2,
   "message":"success",
   "charge":{  
      "relatedTo":{  
         "clientId":"5afadc9d556397001462d25f",
         "lineItemIds":[  
            "5b22c0e4a043cd97a10dcb09",
            "5b22c0f0a043cd97a10dcb0a",
            "5b22c10ca043cd97a10dcb0b",
            "5b2be7f7b0559b4cd9412e3e",
            "5b2be800b0559b4cd9412e3f",
            "5b2be858b0559b4cd9412e40"
         ]
      },
      "stripePayment":{  
         "customer":"cus_CrmVzQ8h97BmdN",
         "currency":"usd",
         "amount":6000,
         "description":"Charge from Skipper.",
         "metadata":{  
            "clientId":"5afadc9d556397001462d25f"
         }
      }
   },
   "num_payments":95
}
{ "status": 2, "message": "mystery", "num_payments": 95 }
{ "status": 3, "message": "payments complete" }
```

Posts array of objects in format of `/admin/stripe-charges` response to process through
Stripe. As each object is processed, there is a response from a websocket subscribed to `update-payment`
with the following codes & supporting data:

Code|Status|Description
----|------|-----------
1|Begin|Processing has started, length of payments to process is returned
2|Processed|A payment has been processed, message containing `success`, `failed`, or `mystery` returned along with length of payments & payment
3|Finished|All payments in payload have been processed, message of `payments complete` returned


### HTTP Request

`POST https://waggle-api-prod.herokuapp.com/admin/process-payments`

## Add Walk Credit

Creates `WalkCredit` objects based on the request payload. Updates `Client` object
specified by `clientId` parameter in URI `bundle_size` property the the number of
`WalkCredit` objects being created.  Also updates `auto_renew` property accordingly
if specified in the payload


### HTTP Request

`POST https://waggle-api-prod.herokuapp.com/admin/walkCredits/<clientId>`

### Request Body

Key|Required|Description
---|--------|-----------
number|true|The number of WalkCredit objects to create
length|true|The duration of the WalkCredit objects
auto_renew|true|Updates `auto_renew` property of `Client` for the length specified
discount|true|Discount percentage, must be 0 < x < 100

## Remove Walk Credits

Deletes `WalkCredit` objects with `client_id` specified by `clientId` parameter
in URI based on `duration` and `quantity` specified in query string.


### HTTP Request

`DELETE https://waggle-api-prod.herokuapp.com/admin/walkCredits/<clientId>?quantity=3&duration=20`

### Query Parameters

Key|Required|Description
---|--------|-----------
quantity|true|The number of WalkCredit objects to remove
duration|true|The type of WalkCredits to delete, valid options are 20, 40, 60 & 120

## Edit Auto Renew

Updates `auto_renew` for `Client` object based on the request payload.


### HTTP Request

`PUT https://waggle-api-prod.herokuapp.com/admin/autoRenew/<clientId>`

### Request Body

Key|Required|Description
---|--------|-----------
twenty|false|Then number of credits to auto renew
forty|false|Then number of credits to auto renew
sixty|false|Then number of credits to auto renew
play_care|false|Then number of credits to auto renew

## Upload Images

Adds images to `Appointment` object specified by `appointmentId` parameter of URI.
FormData object containing `file` which is the image to add to the `Appointment`
array of `images`


### HTTP Request

`POST https://waggle-api-prod.herokuapp.com/admin/appointments/<appointmentId>/images`

### Request Body

Key|Required|Description
---|--------|-----------
file|true|Image file to add to the Appointment

## Get Markets

> Successful response is an array of Market objects

```json
[  
   {  
      "_id":"5addfe32efbc33d7532ff9d7",
      "updatedAt":"2018-06-19T16:43:14.020Z",
      "createdAt":"2018-04-23T15:39:30.790Z",
      "longitude":"-97.7431",
      "latitude":"30.2672",
      "state":"Texas",
      "city":"Austin",
      "time_zone":"America/Chicago",
      "phone_number":"+15122014125",
      "__v":0,
      "start_date":"2018-06-30T16:42:42.111Z"
   },
   {  
      "_id":"5a7ef4b208abad6d70537e5f",
      "updatedAt":"2018-06-26T17:06:53.135Z",
      "createdAt":"2018-02-10T13:33:38.060Z",
      "longitude":"-80.832285",
      "latitude":"35.196901",
      "state":"NC",
      "city":"Charlotte",
      "time_zone":"America/New_York",
      "phone_number":"+17043436658",
      "__v":0,
      "start_date":"2018-06-19T20:29:15.786Z"
   }
]
```

Returns a list of all `Market` objects.

### HTTP Request

`GET https://waggle-api-prod.herokuapp.com/admin/markets`

## Add Market

> Successful response is a Market object

```json
{  
   "__v":0,
   "updatedAt":"2018-06-29T13:24:19.965Z",
   "createdAt":"2018-06-29T13:24:19.965Z",
   "time_zone":"America/New_York",
   "start_date":"2018-06-30T13:14:29.235Z",
   "longitude":"77.0369",
   "latitude":"38.9072",
   "state":"DC",
   "city":"D.C",
   "_id":"5b363303cd2f801c04377a48"
}
```

Posts a `Market` object based on the request body. Returns new `Market` object
after it is created.

### Request Body

Key|Required|Description
---|--------|-----------
Market|true|Market object to create

### HTTP Request

`POST https://waggle-api-prod.herokuapp.com/admin/market`

## Get Market by ID

> Successful response is a Market object

```json
{  
   "__v":0,
   "updatedAt":"2018-06-29T13:24:19.965Z",
   "createdAt":"2018-06-29T13:24:19.965Z",
   "time_zone":"America/New_York",
   "start_date":"2018-06-30T13:14:29.235Z",
   "longitude":"77.0369",
   "latitude":"38.9072",
   "state":"DC",
   "city":"D.C",
   "_id":"5b363303cd2f801c04377a48"
}
```

Gets `Market` specified by `marketId` parameter in URI

### HTTP Request

`GET https://waggle-api-prod.herokuapp.com/admin/market/<marketId>`

## Edit Market

> Successful response is a Market object

```json
{  
   "__v":0,
   "updatedAt":"2018-06-29T13:24:19.965Z",
   "createdAt":"2018-06-29T13:24:19.965Z",
   "time_zone":"America/New_York",
   "start_date":"2018-06-30T13:14:29.235Z",
   "longitude":"77.0369",
   "latitude":"38.9072",
   "state":"DC",
   "city":"D.C",
   "_id":"5b363303cd2f801c04377a48"
}
```

Updates `Market` specified by `marketId` parameter in URI

### HTTP Request

`PUT https://waggle-api-prod.herokuapp.com/admin/market/<marketId>`

## Delete Market

Deletes `Market` specified by `marketId` parameter in URI

### HTTP Request

`DELETE https://waggle-api-prod.herokuapp.com/admin/market/<marketId>`

## Get Zip Codes

> Successful response is an array of Zip objects

```json
[  
   {  
      "_id":"5b363759cd2f801c04377a4a",
      "updatedAt":"2018-06-29T13:42:49.960Z",
      "createdAt":"2018-06-29T13:42:49.960Z",
      "market_id":"5b363303cd2f801c04377a48",
      "state_abbreviation":"DC",
      "zip_code":"20151",
      "state":"51",
      "__v":0,
      "wait_list":true
   },
   {  
      "_id":"5b363761cd2f801c04377a4b",
      "updatedAt":"2018-06-29T13:42:57.655Z",
      "createdAt":"2018-06-29T13:42:57.655Z",
      "market_id":"5b363303cd2f801c04377a48",
      "state_abbreviation":"DC",
      "zip_code":"22033",
      "state":"51",
      "__v":0,
      "wait_list":true
   }
]
```

Returns `Zip` objects with `market_id` property matching `marketId` parameter
specified in URI.

### HTTP Request

`GET https://waggle-api-prod.herokuapp.com/admin/market/<marketId>/zipCodes`

## Create Zip Code

Posts `Zip` object defined in request body, `wait_list` property is defaulted to
false, if you wish to enable use Edit Zip endpoint.

### HTTP Request

`POST https://waggle-api-prod.herokuapp.com/admin/zip`

### Request Body

Key|Required|Description
---|--------|-----------
market_id|true|Market ID to associate zip code with
state_abbreviation|true|Two letter state abbreviation corresponding to `State` model
zip_code|true|5 digit zip code to create
state|true|ID of `State` model

## Delete Zip Code

Deletes `Zip` object defined in by `zipId` parameter specified in request.

### HTTP Request

`DELETE https://waggle-api-prod.herokuapp.com/admin/zip/<zipId>`

## Edit Zip Code

Updates `Zip` object specified by `zipId` parameter in request. Primary use is to
update `wait_list` to make `Zip` active or inactive.

### HTTP Request

`POST https://waggle-api-prod.herokuapp.com/admin/zip/<zipId>`

### Request Body

Key|Required|Description
---|--------|-----------
market_id|true|Market ID to associate zip code with
state_abbreviation|true|Two letter state abbreviation corresponding to `State` model
zip_code|true|5 digit zip code to create
state|true|ID of `State` model
wait_list|false|Flag specifying if `Zip` is currently serviced.  Default is `false`

## Publish Draft

Updates `Appointment` objects in `Draft` specified by `marketId` in request body.
The properties `appointment_status`, `schedule_time`, `sitter`, and `idle_time` are
updated.

### HTTP Request

`POST https://waggle-api-prod.herokuapp.com/admin/publishDraft`

### Query Parameters

Key|Required|Description
---|--------|-----------
discard|false|Deletes `Draft` if `true`. Default is `false`

## Get Apartments

> Successful response is an array of Apartment objects

```json
[  
   {  
      "apartment_id":"5b1d1fd628c3bbe7bdf5f856",
      "name":"austin apt",
      "playcare":true,
      "market_id":"5addfe32efbc33d7532ff9d7"
   },
   {  
      "apartment_id":"5b364158b5842d2778cbaa18",
      "name":"TEST",
      "playcare":true,
      "market_id":"5addfe32efbc33d7532ff9d7"
   }
]
```

Returns `Apartment` objects containing `market_id` equal to query parameter `market`

### HTTP Request

`GET https://waggle-api-prod.herokuapp.com/admin/apartments?market=5a7ef4b208abad6d70537e5f`

### Query Parameters

Key|Required|Description
---|--------|-----------
market|true|Market ID of apartments to retrieve

## Create Apartment

> Successful response is an Apartment object

```json
{  
   "apartment_id":"5b364158b5842d2778cbaa18",
   "name":"TEST",
   "playcare":true,
   "market_id":"5addfe32efbc33d7532ff9d7"
}
```

Creates an `Apartment` object specified in the request body

### HTTP Request

`GET https://waggle-api-prod.herokuapp.com/admin/apartments`

### Request Body

Key|Required|Description
---|--------|-----------
name|true|Name of Apartment Complex
market_id|true|Market to associate Apartment Complex with
playcare|false|Flag that specifies if Apartment Complex does PlayCare visits

## Edit Apartment

> Successful response is an Apartment object

```json
{  
   "apartment_id":"5b364158b5842d2778cbaa18",
   "name":"TEST",
   "playcare":true,
   "market_id":"5addfe32efbc33d7532ff9d7"
}
```

Updates `Apartment` object specified by `apartmentId` parameter of request URI. Updates
`Apartment` to the request body

### HTTP Request

`PUT https://waggle-api-prod.herokuapp.com/admin/apartment/<apartmentId>`

### Request Body

Key|Required|Description
---|--------|-----------
name|true|Name of Apartment Complex
market_id|true|Market to associate Apartment Complex with
playcare|false|Flag that specifies if Apartment Complex does PlayCare visits

## Get Favorite Images

> Successful response is an array of Image objects

```json
[  
   {  
      "_id":"5b364eb2ac363500144a3072",
      "appt_id":"5b33a0165cb9113f77e4dba8",
      "original":"https://waggle-keys-stage.s3.amazonaws.com/5b33a0165cb9113f77e4dba8_077AFE7C-F493-443A-8F46-FC73AED9E4C5-1719-0000016E1D31CB4D.jpeg",
      "thumbnail":"https://waggle-keys-stage.s3.amazonaws.com/5b33a0165cb9113f77e4dba8_077AFE7C-F493-443A-8F46-FC73AED9E4C5-1719-0000016E1D31CB4D.jpeg",
      "pets":[  
         {  
            "_id":"5a4f87161a06183b2ffcb4ab",
            "name":"Millie",
            "image_url":null,
            "pet_class":"Green",
            "pet_class_notes":"",
            "gender_preference":""
         }
      ]
   }
]
```

Returns `Images` for specified `date` in Query String

### HTTP Request

`GET https://waggle-api-prod.herokuapp.com/admin/images/favorite?date=Fri%20Jun%2029%202018%2012%3A15%3A06%20GMT-0400%20%28Eastern%20Daylight%20Time%29`

### Query Parameters

Key|Required|Description
---|--------|-----------
date|true|Date object to retrieve favorite images for

## Hide Image

Updates `Image` object specified by `imageId` parameter in request URI. Sets `hide_from_dashboard`
property to true

### HTTP Request

`PUT https://waggle-api-prod.herokuapp.com/admin/hideImage/<imageId>`

### Request Body

Key|Required|Description
---|--------|-----------
Image|true|Image object to update

## Delete Image

Deletes `Image` object specified by `imageId` parameter in request URI.

### HTTP Request

`DELETE https://waggle-api-prod.herokuapp.com/admin/image/<imageId>`

## Get Prices

> Successful response is a Prices object

```json
{  
   "20":{  
      "1":1900,
      "5":1700,
      "15":1500
   },
   "40":{  
      "1":2700,
      "5":2500,
      "15":2300
   },
   "60":{  
      "1":3400,
      "5":3200,
      "15":3000
   },
   "120":{  
      "1":2400,
      "5":2200,
      "15":2000
   },
   "market_id":"5a7ef4b208abad6d70537e5f"
}
```

Returns `Price` object specified by `marketId` parameter in request URI.

### HTTP Request

`GET https://waggle-api-prod.herokuapp.com/admin/prices/<marketId>`

## Edit Prices

Updates `Prices` object specified by `marketId` parameter in request URI. Object is
updated to the request body.

### HTTP Request

`GET https://waggle-api-prod.herokuapp.com/admin/prices/<marketId>`

### Query Parameters

Key|Required|Description
---|--------|-----------
Prices|true|Prices object to update

# Client Endpoints

All authentication is handled by a Firebase JWT, passed in as an auth header, such as `Authorization: Bearer eyfj123...` . All endpoints require this authentication.

## CSRF Token

Generates a random token for `Client`

### HTTP Request

`GET https://waggle-api-prod.herokuapp.com/client/csrf`

## Login

> Successful response contains a success flag of true

```json
{
  "status":"success"
}
```

Authenticates user with Firebase, and creates a session cookie if necessary

### HTTP Request

`POST https://waggle-api-prod.herokuapp.com/client/login`

## Logout

Clears session cookie, and revokes refresh tokens from Firebase

### HTTP Request

`POST https://waggle-api-prod.herokuapp.com/client/logout`

## Get Prices

> Successful response contains a Prices object

```json
{  
   "20":{  
      "1":1900,
      "5":1700,
      "15":1500
   },
   "40":{  
      "1":2700,
      "5":2500,
      "15":2300
   },
   "60":{  
      "1":3400,
      "5":3200,
      "15":3000
   },
   "120":{  
      "1":2400,
      "5":2200,
      "15":2000
   },
   "_id":null,
   "__v":0,
   "market_id":"5a7ef4b208abad6d70537e5f"
}

```

Returns a `Prices` object specified by the logged in `user` objects `market_id`

### HTTP Request

`GET https://waggle-api-prod.herokuapp.com/client/prices`

## Is Authed

> Successful response contains an object with isAuthed set to true

```json
{
  "isAuthed": true
}
```

Returns object with key `isAuthed` set to `true`, if the `user` logged in is not
authenticated, the request will be denied.

### HTTP Request

`GET https://waggle-api-prod.herokuapp.com/client/isAuthed`

## Confirm Consultation

> Successful response contains an Appointment object

```json
{  
   "_id":"5b366a14eaa7c33113085c0f",
   "updatedAt":"2018-06-29T17:19:16.326Z",
   "createdAt":"2018-06-29T17:19:16.326Z",
   "client_id":"5b3669ebeaa7c33113085c0e",
   "market_id":"5a7ef4b208abad6d70537e5f",
   "price":1000,
   "visit_date":"2018-07-02T16:00:00.000Z",
   "window_start_time":"Mon Jul 2 2018 12:00",
   "window_end_time":"Mon Jul 2 2018 12:10",
   "__v":0,
   "client_confirmed":false,
   "exclude_from_scheduler":false,
   "en_route":false,
   "clear_notes_from_dashboard":false,
   "clear_from_dashboard":false,
   "sitter_viewed":false,
   "add_on_services":[  

   ],
   "recurrence_weekdays":[  

   ],
   "price_overridden":false,
   "images":[  

   ],
   "requires_tracking":true,
   "override_device_within_region":false,
   "appointment_status":{  
      "id":2,
      "name":"Approved"
   },
   "appointment_type":{  
      "name":"Consultation",
      "id":8,
      "duration_in_minutes":30
   },
   "pet_ids":[  

   ],
   "pets":[  

   ]
}
```

Updates `Appointment` object specified by `appointmentId` parameter in URI,
setting `client_confirmed` to `true` and returns the new `Appointment`

### HTTP Request

`GET https://waggle-api-prod.herokuapp.com/client/confirmConsulation/<appointmentId>`

## Sign Up One

> Successful response contains a formatted User object

```json
{  
   "user":{  
      "_id":"5b36770deaa7c33113085c10",
      "contact":{  
         "first_name":"UHHHH",
         "last_name":"WUUUUUT",
         "email":"wuuuut@womm.com"
      },
      "home":{  
         "address":{  
            "city":"Charlotte",
            "state":{  
               "id":33,
               "name":"North Carolina",
               "abbreviation":"NC"
            },
            "zip_code":"28203"
         }
      },
      "uid":"sqDWidCfElMKO08zrGACAMIwGcV2",
      "signUpStep":2,
      "consultation_status":"unscheduled",
      "pets":[  

      ],
      "punchCard":{  
         "number":0
      }
   }
}
```

Standard website sign up.  Checks users `zip_code` sent in request body and sends
Out of Area, or Wait List emails.  If `zip_code` is active, a user is created in
Firebase, Stripe, and a `Client` object is created.

### HTTP Request

`POST https://waggle-api-prod.herokuapp.com/client/signUp/one`

### Request Body

Key|Required|Description
---|--------|-----------
first_name|true|Client first name
last_name|true|Client last name
email|true|Client email
zip_code|true|Client zip code

## Sign Up Two

Standard website sign up.  Part two of sign up form updates `Client` object created
in part one based on request body

### HTTP Request

`POST https://waggle-api-prod.herokuapp.com/client/signUp/two`

### Request Body

Key|Required|Description
---|--------|-----------
phone_number|true|Client phone number
home_type|true|Client home type which is one of the following: "Apartment / Condo", "Townhouse", "House", "Other"
address_line_1|false|Client address line 1
address_line_2|false|Client address line 2

## Get Consultation Dates

> Successful response is an object containing dates key with array of dates

```json
{
  "dates": [
    {
      "date":"Mon Jul 2nd",
      "full_date":"2018-07-02T04:00:00.000Z",
      "times":[  
         {  
            "time":"10:00 AM",
            "visit":null,
            "consults":0
         },
         {  
            "time":"10:30 AM",
            "visit":null,
            "consults":0
         },
         {  
            "time":"11:00 AM",
            "visit":null,
            "consults":0
         },
         {  
            "time":"11:30 AM",
            "visit":null,
            "consults":0
         },
         {  
            "time":"12:00 PM",
            "visit":null,
            "consults":1
         },
         {  
            "time":"12:30 PM",
            "visit":null,
            "consults":1
         },
         {  
            "time":"01:00 PM",
            "visit":null,
            "consults":0
         },
         {  
            "time":"01:30 PM",
            "visit":null,
            "consults":0
         },
         {  
            "time":"02:00 PM",
            "visit":null,
            "consults":0
         },
         {  
            "time":"02:30 PM",
            "visit":null,
            "consults":0
         },
         {  
            "time":"03:00 PM",
            "visit":null,
            "consults":0
         },
         {  
            "time":"03:30 PM",
            "visit":null,
            "consults":0
         },
         {  
            "time":"04:00 PM",
            "visit":null,
            "consults":0
         },
         {  
            "time":"04:30 PM",
            "visit":null,
            "consults":0
         },
         {  
            "time":"05:00 PM",
            "visit":null,
            "consults":0
         },
         {  
            "time":"05:30 PM",
            "visit":null,
            "consults":0
         },
         {  
            "time":"06:00 PM",
            "visit":null,
            "consults":0
         },
         {  
            "time":"06:30 PM",
            "visit":null,
            "consults":0
         }
       ]
     }
  ]  
}
```

Returns list of dates containing available times to schedule consultation `Appointment`
objects

### HTTP Request

`GET https://waggle-api-prod.herokuapp.com/client/consultationDates`

## Sign Up Three

> Successful response contains an object with consultation date/time

```json
{  
   "consultationDate":"Monday, Jul 2nd",
   "consultationTime":"10:00 AM",
   "consultationStart":"10:00",
   "consultationEnd":"10:10"
}
```

Creates `Appointment` object for `Client` consultation

### HTTP Request

`POST https://waggle-api-prod.herokuapp.com/client/signUp/three`

### Request Body

Key|Required|Description
---|--------|-----------
date|true|Date object for date of consultation to be scheduled
time|true|Object for time of consultation to be scheduled

## Get Client by Activation ID

> Successful response contains a formatted User object

```json
{
    "_id": "5a4d05e8360d607ef03f604a",
    "uid": "g5wRx4inZ9TaFLsifHNTFjrL9893",
    "first_name": "Scott",
    "last_name": "Huff",
    "full_name": "Scott Huff",
    "email": "scott@walkskipper.com",
    "phone_number": "1234567890",
}
```

Returns formatted `Client` object specified by `activationId` parameter in request
URI.

### HTTP Request

`GET https://waggle-api-prod.herokuapp.com/client/clientActivation/<activationId>`

## Set Password

> Successful response contains an object with success flag set to true

```json
{
  "success": true
}
```

Updates user in Firebase assigning them the `password` specified in the request body.
`Client` object is then updated and assigned new `uid` corresponding to Firebase and
`activation_id` is set to `null`

### HTTP Request

`POST https://waggle-api-prod.herokuapp.com/client/setPassword`

### Request Body

Key|Required|Description
---|--------|-----------
activation_id|true|Temporary activation ID for user without password
password|true|New password for Client

## Set Pet Profile Image

The `image` specified in the request body is saved to AWS, and `Pet` object specified by
parameter `petId` in URI is updated setting `profile_image_file_name` equal to the generated
file name saved to AWS.

### HTTP Request

`PUT https://waggle-api-prod.herokuapp.com/client/setPetProfileImage/<petId>`

### Request Body

Key|Required|Description
---|--------|-----------
image|true|Image to save as Pet's profile image

## Get Appointments

> Successful response contains array of Appointment objects

```json
{  
   "appointments":[  
      {  
         "formatted_date":"2018-06-12",
         "formatted_date_full":"Jun 12th, 2018",
         "window_start_time":"10:00",
         "window_end_time":"10:10",
         "visit_type":{  
            "name":"Consultation",
            "id":8,
            "duration_in_minutes":30
         },
         "visit_status":{  
            "id":5,
            "name":"Completed"
         },
         "pet_ids":[  

         ],
         "_id":"5b1ec09c70a1bd0014097c3c",
         "visit_date":"2018-06-12T12:00:00.000Z",
         "sitter_name":"scott H."
      },
      {  
         "formatted_date":"2018-06-29",
         "formatted_date_full":"Jun 29th, 2018",
         "window_start_time":"01:40",
         "window_end_time":"03:30",
         "visit_type":{  
            "id":8,
            "name":"Consultation",
            "duration_in_minutes":30
         },
         "visit_status":{  
            "id":1,
            "name":"Pending"
         },
         "pet_ids":[  
            "5afb2c8934c3e50014b054e2",
            "5b3127d1ab69a811428310fb",
            "5b311100dbb46f80e2815192"
         ],
         "_id":"5b36698fac363500144a3074",
         "visit_date":"2018-06-29T17:16:05.643Z"
      }
   ]
}
```

Returns `Appointment` objects within a specified time interval passed in the Query
String

### HTTP Request

`GET https://waggle-api-prod.herokuapp.com/client/appointments`

### Query Parameters

Key|Required|Description
---|--------|-----------
startDate|false|Beginning of interval to get Appointments. Default is beginning of current month
endDate|false|End of interval to get Appointments. Default is end of current month.

## Create Appointments

> Successful response contains success flag set to true and array of Appointment objects

```json
{  
   "success":true,
   "appointments":[  
      {  
         "__v":0,
         "updatedAt":"2018-06-29T20:22:02.075Z",
         "createdAt":"2018-06-29T20:22:02.075Z",
         "client_id":"5afadc9d556397001462d25f",
         "market_id":"5a7ef4b208abad6d70537e5f",
         "scheduled_time":null,
         "window_end_time":"2018-06-29 18:30",
         "window_start_time":"2018-06-29 17:00",
         "client_notes":"1 posty boi",
         "visit_date":"2018-06-29T16:00:00.000Z",
         "_id":"5b3694ea563b66379a913837",
         "client_confirmed":false,
         "exclude_from_scheduler":false,
         "en_route":false,
         "clear_notes_from_dashboard":false,
         "clear_from_dashboard":false,
         "sitter_viewed":false,
         "add_on_services":[  
            {  
               "pet_id":"5afb2c8934c3e50014b054e2",
               "completed":false,
               "name":"Pee",
               "id":1
            },
            {  
               "pet_id":"5afb2c8934c3e50014b054e2",
               "completed":false,
               "name":"Poop",
               "id":2
            },
            {  
               "pet_id":"5b311100dbb46f80e2815192",
               "completed":false,
               "name":"Pee",
               "id":1
            },
            {  
               "pet_id":"5b311100dbb46f80e2815192",
               "completed":false,
               "name":"Poop",
               "id":2
            },
            {  
               "pet_id":"5b3127d1ab69a811428310fb",
               "completed":false,
               "name":"Pee",
               "id":1
            },
            {  
               "pet_id":"5b3127d1ab69a811428310fb",
               "completed":false,
               "name":"Poop",
               "id":2
            }
         ],
         "recurrence_weekdays":[  

         ],
         "price_overridden":false,
         "images":[  

         ],
         "requires_tracking":true,
         "override_device_within_region":false,
         "appointment_status":{  
            "id":1,
            "name":"Pending"
         },
         "appointment_type":{  
            "id":20,
            "name":"20 Min Visit",
            "duration_in_minutes":20
         },
         "pet_ids":[  
            "5afb2c8934c3e50014b054e2",
            "5b311100dbb46f80e2815192",
            "5b3127d1ab69a811428310fb"
         ],
         "pets":[  

         ]
      }
   ]
}

```

Posts one or many `Appointment` objects. If `recurring` flag is set to `true`, multiple
`Appointment` objects will be created for every day specified in `weekdays` array before the
`window_end_date` or 1 year if not specified. If `recurring` flag is set to `false` (default)
then only one `Appointment` is created.

### HTTP Request

`POST https://waggle-api-prod.herokuapp.com/client/appointments`

### Request Body

Key|Required|Description
---|--------|-----------
Appointment|true|Appointment model to be created

## Create Pet

> Successful response contains success flag set to true and the new Pet object

```json
{  
   "success":true,
   "pet":{  
      "__v":0,
      "updatedAt":"2018-07-01T19:03:54.295Z",
      "createdAt":"2018-07-01T19:03:54.295Z",
      "client_id":"5afadc9d556397001462d25f",
      "allergies":"Allergies",
      "birthday_month":"March",
      "pet_location":"Crate",
      "indoor":"Indoor/Outdoor",
      "color":"Black",
      "age":"Puppy (< 1 Year)",
      "sex":"Neutered Male",
      "breed":"American Foxhound",
      "animal_type":"Dog",
      "name":"Pupperino",
      "_id":"5b39259a563b66379a913838",
      "approved":false,
      "active":true,
      "medicine":[  

      ]
   }
}

```

Posts a `Pet` object to create

### HTTP Request

`POST https://waggle-api-prod.herokuapp.com/client/pets`

### Request Body

Key|Required|Description
---|--------|-----------
Pet|true|Pet model to be created

## Edit Pet

> Successful response contains the updated Pet object

```json
{  
   "vet_phone":"1234567890",
   "_id":"5b39259a563b66379a913838",
   "updatedAt":"2018-07-02T12:03:17.628Z",
   "createdAt":"2018-07-01T19:03:54.295Z",
   "client_id":"5afadc9d556397001462d25f",
   "allergies":"Allergies",
   "birthday_month":"March",
   "pet_location":"Crate",
   "indoor":"Indoor/Outdoor",
   "color":"Black",
   "age":"Puppy (< 1 Year)",
   "sex":"Neutered Male",
   "breed":"American Foxhound",
   "animal_type":"Dog",
   "name":"Pupperino",
   "__v":0,
   "approved":false,
   "active":true,
   "medicine":[  

   ]
}
```

Updates a `Pet` object specified by `petId` parameter in URI

### HTTP Request

`PUT https://waggle-api-prod.herokuapp.com/client/pets/<petId>`

### Request Body

Key|Required|Description
---|--------|-----------
Pet|true|Pet model to be updated

## Get Pet by ID

> Successful response contains a formatted Pet object

```json
{  
   "_id":"5afb2c8934c3e50014b054e2",
   "name":"Doggo",
   "active":true,
   "animal_type":"Dog",
   "image_url":"https://waggle-keys-stage.s3.amazonaws.com/pet-placeholder.jpg",
   "sex":"Intact Male",
   "age":"Puppy (< 1 Year)",
   "food":{  

   },
   "medical":{  
      "medications":[  

      ]
   },
   "vet":{  

   }
}
```

Returns a `Pet` object specified by `petId` parameter in URI

### HTTP Request

`GET https://waggle-api-prod.herokuapp.com/client/pets/<petId>`

## Deactivate Pet

> Successful response is an object containing success flag':

```json
{
  "success": true
}
```

Deactivates `Pet` object by `petId` specified in URI.  Calling this action will remove
the pet from any pending, approved or change-requested `Appointment`.  Same controller as
Admin Endpoints

### HTTP Request

`PUT https://waggle-api-prod.herokuapp.com/admin/clients/pets/<petId>/deactivate`

## Get Profile

> Successful response contains a formatted Client object

```json
{  
   "_id":"5afadc9d556397001462d25f",
   "uid":"EoNMkYxCdtX3p9ywzFJrXntN6Qz2",
   "market_id":"5a7ef4b208abad6d70537e5f",
   "consultation_status":"completed",
   "signup_date":"2018-05-13T00:00:00.000Z",
   "active":true,
   "secured_yard":false,
   "contact":{  
      "first_name":"scott",
      "last_name":"huff",
      "full_name":"scott huff",
      "email":"scott+client@thewagglecompany.com",
      "phone_number":"2342343232"
   },
   "home":{  
      "address":{  
         "address_line_1":"809 w. hill st",
         "city":"charlotte",
         "state":"North Carolina",
         "zip_code":"28202"
      }
   },
   "secondary_contact":{  
      "full_name":"undefined undefined"
   },
   "emergency_contact":{  
      "full_name":"undefined undefined"
   }
}
```

Returns a `Client` object for the current `Client` that is logged in.

### HTTP Request

`GET https://waggle-api-prod.herokuapp.com/client/profile`

## Get Appointment by ID

> Successful response contains a formatted Appointment object

```json
{  
   "_id":"5b23d58a7be4b2b25b5428a6",
   "appointment_status":{  
      "name":"Approved",
      "id":2
   },
   "appointment_type":{  
      "id":40,
      "name":"40 Minutes",
      "duration_in_minutes":40
   },
   "created_at":"Jun 15th, 2018",
   "updated_at":"2018-06-26T15:00:26.177Z",
   "visit_date":"2018-07-07T15:30:00.000Z",
   "price_overridden":false,
   "recurrence":{  
      "is_recurring":false,
      "weekdays":[  

      ]
   },
   "kml":null,
   "client_notes":"",
   "duration_in_minutes":40,
   "appointment_images":[  

   ],
   "addons":[  

   ],
   "scheduled_start_time":"2018-07-02T15:14:44.718Z",
   "window_start_time":"11:30 am",
   "window_end_time":"1:00 pm",
   "window_start_formatted":"Sat Jul 7 2018 11:30",
   "actual_start_time":null,
   "actual_end_time":null,
   "sitter_name":null,
   "walk_bank":{  
      "20":0,
      "40":5,
      "60":0,
      "120":0,
      "total_walks_remaining":5
   },
   "auto_renew":{  
      "20":0,
      "40":0,
      "60":0
   },
   "contact":{  
      "first_name":"scott",
      "last_name":"huff",
      "full_name":"scott huff"
   },
   "appointment_pet_ids":[  
      "5afb2c8934c3e50014b054e2"
   ],
   "all_client_pets":[  
      {  
         "_id":"5afb2c8934c3e50014b054e2",
         "name":"Doggo",
         "active":true,
         "is_on_appointment":true,
         "image_url":"https://waggle-keys-stage.s3.amazonaws.com/pet-placeholder.jpg",
         "add_ons":[  

         ]
      },
      {  
         "_id":"5b311100dbb46f80e2815192",
         "name":"Derp",
         "active":true,
         "is_on_appointment":false,
         "image_url":"https://waggle-keys-stage.s3.amazonaws.com/pet-placeholder.jpg",
         "add_ons":[  

         ]
      },
      {  
         "_id":"5b3127d1ab69a811428310fb",
         "name":"Gary",
         "active":true,
         "is_on_appointment":false,
         "image_url":"https://waggle-keys-stage.s3.amazonaws.com/pet-placeholder.jpg",
         "add_ons":[  

         ]
      },
      {  
         "_id":"5b39259a563b66379a913838",
         "name":"Pupperino",
         "active":true,
         "is_on_appointment":false,
         "image_url":"https://waggle-keys-stage.s3.amazonaws.com/pet-placeholder.jpg",
         "add_ons":[  

         ]
      }
   ],
   "line_items":[  

   ]
}
```

Returns an `Appointment` object specified by the `appointmentId` parameter specified in the URI

### HTTP Request

`GET https://waggle-api-prod.herokuapp.com/client/appointmentById/<appointmentId>`

## Get Appointment for Edit

> Successful response contains a formatted Appointment object

```json
{  
   "playCareAvailable":true,
   "days":[  
      "2018-05-28",
      "2018-07-04"
   ],
   "appointment":{  
      "_id":"5b30f2b79336607ec8a5dd11",
      "appointment_status":{  
         "name":"Approved",
         "id":2
      },
      "appointment_type":{  
         "id":20,
         "name":"20 Min Visit",
         "duration_in_minutes":20
      },
      "created_at":"Jun 25th, 2018",
      "updated_at":"2018-06-26T15:03:11.008Z",
      "visit_date":"2018-07-22",
      "price_overridden":false,
      "recurrence":{  
         "is_recurring":true,
         "recurrence_id":"c21b18ae-eacc-4b59-a70d-0a73a1a2d42f",
         "recurrence_end_date":"Invalid date",
         "weekdays":[  
            "Sunday",
            "Saturday"
         ]
      },
      "kml":null,
      "client_notes":"",
      "duration_in_minutes":20,
      "add_on_services":[  

      ],
      "scheduled_start_time":"2018-07-02T15:29:14.827Z",
      "window_start_time":"14:30",
      "window_end_time":"16:00",
      "window_start_formatted":"Sun Jul 22 2018 14:30",
      "actual_start_time":null,
      "actual_end_time":null,
      "sitter_name":null,
      "contact":{  
         "_id":"5afadc9d556397001462d25f",
         "first_name":"scott",
         "last_name":"huff",
         "full_name":"scott huff"
      },
      "appointment_pet_ids":[  
         "5afb2c8934c3e50014b054e2"
      ],
      "all_client_pets":[  
         {  
            "_id":"5afb2c8934c3e50014b054e2",
            "name":"Doggo",
            "active":true,
            "is_on_appointment":true,
            "image_url":"https://waggle-keys-stage.s3.amazonaws.com/pet-placeholder.jpg",
            "add_ons":[  

            ]
         },
         {  
            "_id":"5b311100dbb46f80e2815192",
            "name":"Derp",
            "active":true,
            "is_on_appointment":false,
            "image_url":"https://waggle-keys-stage.s3.amazonaws.com/pet-placeholder.jpg",
            "add_ons":[  

            ]
         },
         {  
            "_id":"5b3127d1ab69a811428310fb",
            "name":"Gary",
            "active":true,
            "is_on_appointment":false,
            "image_url":"https://waggle-keys-stage.s3.amazonaws.com/pet-placeholder.jpg",
            "add_ons":[  

            ]
         },
         {  
            "_id":"5b39259a563b66379a913838",
            "name":"Pupperino",
            "active":true,
            "is_on_appointment":false,
            "image_url":"https://waggle-keys-stage.s3.amazonaws.com/pet-placeholder.jpg",
            "add_ons":[  

            ]
         }
      ]
   }
}
```

Returns an `Appointment` specified by `appointmentId` parameter in URI. This call is used
to get a View Model for `/visit/edit/_id` and `/visit/editSeries/_id`

### HTTP Request

`GET https://waggle-api-prod.herokuapp.com/client/appointmentForEdit/<appointmentId>`

## Visit Report

> Successful response contains a formatted Appointment object

```json
{  
   "_id":"5b1ec09c70a1bd0014097c3c",
   "visit_date":"6/12/18",
   "appointment_status":{  
      "name":"Completed",
      "id":5
   },
   "appointment_type":{  
      "duration_in_minutes":30,
      "id":8,
      "name":"Consultation"
   },
   "created_at":"2018-06-11T18:34:04.822Z",
   "updated_at":"2018-06-26T15:03:51.652Z",
   "price":10,
   "price_overridden":false,
   "recurrence":{  
      "is_recurring":false,
      "weekdays":[  

      ]
   },
   "kml":"https://waggle-keys-stage.s3.amazonaws.com/d25246c7-ca7b-4010-8b74-fb5bcd4b86e6.kml",
   "raw_location_dump":"https://waggle-keys-stage.s3.amazonaws.com/e6653617-d8f0-4b91-8ec8-a16f973224e8.csv",
   "sitter_notes_to_client":"Ndjdjdj",
   "duration_in_minutes":0,
   "images":[  

   ],
   "addons":[  

   ],
   "pet_addons":[  

   ],
   "scheduled_start_time":"2018-06-12T18:00:00.000Z",
   "scheduled_end_time":"2018-06-12T18:30:00.000Z",
   "window_start_time":"2018-06-12T18:00:00.000Z",
   "window_end_time":"2018-06-12T18:10:00.000Z",
   "start_time":"2018-06-12T18:17:47.000Z",
   "end_time":"2018-06-12T18:18:16.000Z",
   "sitter_name":"scott H.",
   "contact":{  
      "first_name":"scott",
      "last_name":"huff",
      "full_name":"scott huff"
   },
   "appointment_pet_ids":[  

   ],
   "pets":[  

   ],
   "home":{  
      "address":{  

      }
   },
   "line_items":[  

   ]
}
```

Returns an `Appointment` specified by `appointmentId` parameter in URI. This call is used
to get a View Model specific for a Visit Report

### HTTP Request

`GET https://waggle-api-prod.herokuapp.com/client/visitReport/<appointmentId>`

## Cancel Appointment

> Successful response contains a success flag set to true

```json
{  
   "success": true
}
```

Updates an `Appointment` object specified by `appointmentId` parameter in URI. Sets
`appointment_status` object `id` equal to `7` and `name` equal to `Canceled`

### HTTP Request

`PUT https://waggle-api-prod.herokuapp.com/client/appointments/<appointmentId>/cancel`


## Get User Info

> Successful response contains user object and array of appointments for the user

```json
{  
   "user":{  
      "_id":"5afadc9d556397001462d25f",
      "uid":"EoNMkYxCdtX3p9ywzFJrXntN6Qz2",
      "market_id":"5a7ef4b208abad6d70537e5f",
      "images":[  

      ],
      "legalAgreement":true,
      "signup_complete":true,
      "consultation_status":"completed",
      "punchCard":{  
         "_id":"5b1fd3ecacccc4749ad4dbbe",
         "client_id":"5afadc9d556397001462d25f",
         "number":1,
         "__v":0
      },
      "contact":{  
         "first_name":"scott",
         "last_name":"huff",
         "full_name":"scott huff",
         "email":"scott+client@thewagglecompany.com",
         "phone_number":"2342343232"
      },
      "home":{  
         "address":{  
            "address_line_1":"809 w. hill st",
            "city":"charlotte",
            "state":{  
               "id":33,
               "name":"North Carolina",
               "abbreviation":"NC"
            },
            "zip_code":"28202",
            "enforce_device_within_region":false
         },
         "home_class":null
      },
      "has_valid_payment_method":true,
      "pets":[  
         {  
            "_id":"5afb2c8934c3e50014b054e2",
            "name":"Doggo",
            "add_ons":[  

            ],
            "image_url":"https://waggle-keys-stage.s3.amazonaws.com/pet-placeholder.jpg"
         },
         {  
            "_id":"5b311100dbb46f80e2815192",
            "name":"Derp",
            "add_ons":[  

            ],
            "image_url":"https://waggle-keys-stage.s3.amazonaws.com/pet-placeholder.jpg"
         }
      ]
   },
   "appointments":[  
      {  
         "formatted_date":"2018-07-14",
         "formatted_date_full":"Jul 14th, 2018",
         "window_start_time":"11:30",
         "window_end_time":"02:30",
         "visit_type":{  
            "duration_in_minutes":20,
            "name":"20 Min Visit",
            "id":20
         },
         "visit_status":{  
            "id":2,
            "name":"Approved"
         },
         "pet_ids":[  
            "5afb2c8934c3e50014b054e2",
            "5b3127d1ab69a811428310fb",
            "5b311100dbb46f80e2815192",
            "5b39259a563b66379a913838"
         ],
         "_id":"5b3e94703855c80014437ced",
         "visit_date":"2018-07-14T11:30:00.000Z"
      },
      {  
         "formatted_date":"2018-07-15",
         "formatted_date_full":"Jul 15th, 2018",
         "window_start_time":"11:30",
         "window_end_time":"02:30",
         "visit_type":{  
            "duration_in_minutes":20,
            "name":"20 Min Visit",
            "id":20
         },
         "visit_status":{  
            "id":2,
            "name":"Approved"
         },
         "pet_ids":[  
            "5b39259a563b66379a913838",
            "5b311100dbb46f80e2815192",
            "5afb2c8934c3e50014b054e2",
            "5b3127d1ab69a811428310fb"
         ],
         "_id":"5b3e94703855c80014437cee",
         "visit_date":"2018-07-15T11:30:00.000Z"
      }
   ]
}
```

Returns `User` model of the current logged in user and array of `Appointment` objects
over a specified interval or default of the current month

### HTTP Request

`GET https://waggle-api-prod.herokuapp.com/client/user-info`

### Query Parameters

Key|Required|Description
---|--------|-----------
startDate|false|Date beginning time interval to retrieve Appointments for. Default is beginning of the current month.
endDate|false|Date ending time interval to retrieve Appointments for. Default is end of the current month.


## Account Info

> Successful response contains an object containing data for a Client account

```json
{  
   "_id":"5afadc9d556397001462d25f",
   "uid":"EoNMkYxCdtX3p9ywzFJrXntN6Qz2",
   "market_id":"5a7ef4b208abad6d70537e5f",
   "prices":{  
      "20":{  
         "1":1900,
         "5":1700,
         "15":1500
      },
      "40":{  
         "1":2700,
         "5":2500,
         "15":2300
      },
      "60":{  
         "1":3400,
         "5":3200,
         "15":3000
      },
      "120":{  
         "1":2400,
         "5":2200,
         "15":2000
      },
      "_id":null,
      "__v":0,
      "market_id":"5a7ef4b208abad6d70537e5f"
   },
   "stripe_id":"cus_CrmVzQ8h97BmdN",
   "auto_renew":{  
      "twenty":0,
      "forty":0,
      "sixty":0
   },
   "apartment":{  
      "_id":"5b183e10577cdd159c502d7a",
      "updatedAt":"2018-06-06T20:03:28.133Z",
      "createdAt":"2018-06-06T20:03:28.133Z",
      "market_id":"5a7ef4b208abad6d70537e5f",
      "name":"WOOOOOMMMMMMM",
      "__v":0,
      "playcare":true
   },
   "playCareAvailable":true,
   "pendingCharges":[  
      {  
         "_id":"5b3e42454a0eeb3d97ea7cca",
         "createdAt":"Jul 5th, 2018",
         "amount":"$-114.00",
         "description":"CLEAR THE DEBT"
      },
      {  
         "_id":"5b3e5f0b34063040122ddd9f",
         "createdAt":"Jul 5th, 2018",
         "amount":"$55.55",
         "description":"will this acct work???"
      }
   ],
   "has_valid_payment_method":true,
   "walk_bank":{  
      "total_walks_remaining":4,
      "twenty":0,
      "forty":4,
      "sixty":0,
      "play_care":0
   },
   "cards":[  
      {  
         "id":"card_1CS8J1Dx2Br4K8FgL5Icu9mI",
         "brand":"Visa",
         "exp_month":10,
         "exp_year":2020,
         "last4":"4242"
      }
   ],
   "paymentHistory":[  
      {  
         "_id":"5b1fd3a4acccc4749ad4dbbc",
         "date":"Jun 12th, 2018",
         "amount":"$20.00",
         "description":"30 minute appointment completed on Tuesday, Jun 12, 2018",
         "appointment_id":"5b19748badbd1c3fd72d7b05",
         "stripe_charge_id":"ch_1CcD9kDx2Br4K8Fg62hIi0nz",
         "stripe_charge_status":"succeeded"
      },
      {  
         "_id":"5b1fd3ecacccc4749ad4dbbd",
         "date":"Jun 12th, 2018",
         "amount":"$19.00",
         "description":"20 minute appointment completed on Tuesday, Jun 12, 2018",
         "appointment_id":"5b1fd3d6c6adf60014e6f91e",
         "stripe_charge_id":"ch_1CcDAuDx2Br4K8FgVSUUwCRU",
         "stripe_charge_status":"succeeded"
      }
   ]
}
```

Returns View Model containing `Prices` object, an array of `LineItem` objects, and
`paymentMethod` information for the logged in `Client`

### HTTP Request

`GET https://waggle-api-prod.herokuapp.com/client/account`


## Update Profile

> Successful response contains the newly updated Client object

```json
{  
   "visit_routine":"This is an example",
   "_id":"5afadc9d556397001462d25f",
   "updatedAt":"2018-07-10T15:15:25.239Z",
   "createdAt":"2018-05-15T13:11:57.840Z",
   "time_zone":"America/New_York",
   "stripe_id":"cus_CrmVzQ8h97BmdN",
   "secured_yard":false,
   "signup_date":"2018-05-13T00:00:00.000Z",
   "email":"scott+client@thewagglecompany.com",
   "market_id":"5a7ef4b208abad6d70537e5f",
   "full_name":"scott huff",
   "last_name":"huff",
   "first_name":"scott",
   "__v":5,
   "uid":"EoNMkYxCdtX3p9ywzFJrXntN6Qz2",
   "activation_id":"3cfc6044-47b5-474b-8cca-18b498263e7a",
   "bundle_size":5,
   "signUpStep":4,
   "apartment_id":"5b183e10577cdd159c502d7a",
   "signup_complete":true,
   "consultation_status":"completed",
   "auto_renew":{  
      "20":0,
      "40":0,
      "60":0
   },
   "override_geocode":false,
   "team_members":[  

   ],
   "restrict_personnel":false,
   "images":[  

   ],
   "access_method":[  

   ],
   "exit_survey":[  
      2
   ],
   "entry_survey":[  
      2
   ],
   "has_valid_payment_method":true,
   "active":true,
   "confirmation_email_sent":true,
   "home_class":null,
   "pet_ids":[  
      "5afb2c8934c3e50014b054e2",
      "5b311100dbb46f80e2815192",
      "5b3127d1ab69a811428310fb",
      "5b39259a563b66379a913838"
   ],
   "zones":[  

   ],
   "emergency_contact":{  
      "phone_number":null
   },
   "secondary_contact":{  
      "phone_number":null
   },
   "contact":{  
      "phone_number":"2342343232",
      "address":{  
         "address_line_1":"809 w. hill st",
         "city":"charlotte",
         "state":"33",
         "zip_code":"28202",
         "latitude":"35.22819079675003",
         "longitude":"-80.85664215897583",
         "map_image_file_name":"8895271d-faf6-45b2-8cbe-d985e8c22fdb.png",
         "street_view_image_file_name":"6011a69f-f04d-4775-9d59-9c83d38fc3ec.jpg",
         "enforce_device_within_region":false
      }
   },
   "legalAgreement":true,
   "profileReviewed":false,
   "paymentReviewed":false,
   "petReviewed":true
}
```

Updates a `Client` object specified by `clientId` parameter in URI.

### HTTP Request

`PUT https://waggle-api-prod.herokuapp.com/client/<clientId>/update-profile`

### Request Body

Key|Required|Description
---|--------|-----------
Client|true|Client object to update


## Add Walk Credits

Creates `WalkCredit` objects for logged in `Client`

### HTTP Request

`POST https://waggle-api-prod.herokuapp.com/client/walkBank`

### Request Body

Key|Required|Description
---|--------|-----------
number|true|The number of WalkCredit objects to create
length|true|The duration of WalkCredit objects to create
auto_renew|false|Flag to set auto renew for Client.  Default is false


## Add Playcare

Creates `WalkCredit` objects with `playcare` field set to `true` for logged in `Client`

### HTTP Request

`POST https://waggle-api-prod.herokuapp.com/client/addPlayCare`

### Request Body

Key|Required|Description
---|--------|-----------
number|true|The number of WalkCredit objects to create
auto_renew|false|Flag to set auto renew for Client.  Default is false


## Set Payment Method

> Successful response returns an object containing a success flag set to struggled

```json
{
  "success": true
}
```

Updates a `Client` object payment method within Stripe. Removes all other payment methods
from Stripe.

### HTTP Request

`POST https://waggle-api-prod.herokuapp.com/client/payment-method/set`

### Request Body

Key|Required|Description
---|--------|-----------
token|true|Generated token required by Stripe to update payment info


## Set Payment Method

> Successful response returns an object containing a success flag set to struggled

```json
{
  "success": true
}
```

Updates a `Client` object payment method within Stripe. Removes all other payment methods
from Stripe.

### HTTP Request

`POST https://waggle-api-prod.herokuapp.com/client/payment-method/set`

### Request Body

Key|Required|Description
---|--------|-----------
token|true|Generated token required by Stripe to update payment info


## Set Auto Renew

Updates `auto_renew` property of `Client` object.

### HTTP Request

`PUT https://waggle-api-prod.herokuapp.com/client/autoRenew`

### Request Body

Key|Required|Description
---|--------|-----------
20|false|The number of 20 minute Walk Credits to auto renew. Default is none.
40|false|The number of 40 minute Walk Credits to auto renew. Default is none.
60|false|The number of 60 minute Walk Credits to auto renew. Default is none.


## Set Auto Renew

Updates `auto_renew` property of `Client` object.

### HTTP Request

`PUT https://waggle-api-prod.herokuapp.com/client/autoRenew`

### Request Body

Key|Required|Description
---|--------|-----------
20|false|The number of 20 minute Walk Credits to auto renew. Default is none.
40|false|The number of 40 minute Walk Credits to auto renew. Default is none.
60|false|The number of 60 minute Walk Credits to auto renew. Default is none.
