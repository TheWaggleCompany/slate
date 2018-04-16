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
