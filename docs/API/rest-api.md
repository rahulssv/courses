# Rest API
## Tour Batch
- (GET)getBatches
`localhost:8080/batches`
- (GET)getBatchByID
`localhost:8080/batches/2`
- (GET)status
`localhost:8080/metadata/status`
- (POST)addBatch
`localhost:8080/tours`
```json
  {
    "startDate": "2023-11-03",
    "capacity": 1,
    "perParticipantCost": 6000.00,
    "guide": {
        "name": {
            "first": "Tusar",
            "last": "Gandi"
        },
        "mobile": {
            "number": "9900000010"
        }
    }
}
```
- (PUT)updateBatches
`localhost:8080/tours/1`
```json
{
        "id": 2,
        "startDate": "2023-11-01",
        "endDate": "2023-11-04",
        "status": "ACTIVE",
        "capacity": 2,
        "perParticipantCost": 5000.0,
        "availableSeats": 10,
        "guide": {
            "sequence": 0,
            "name": {
                "first": "Tushar",
                "last": "Gandhi"
            },
            "mobile": {
                "number": "9900000010"
            }
        },
        "tour": {
            "id": 1,
            "name": "MUMBAI-NASIK",
            "mode": "BICYCLE",
            "itinerary": {
                "dayPlans": [
                    {
                        "dayCount": 1,
                        "place": "Mumbai",
                        "distance": 0.0,
                        "activity": "reporting between 5 pm to 7 pm. Introduction, tour briefing and ice breaker",
                        "accomodation": {
                            "hotelName": "Hotel Mayur",
                            "address": "SB road, Thane",
                            "roomType": "TWIN_BED"
                        }
                    },
                    {
                        "dayCount": 2,
                        "place": "NASIK",
                        "distance": 150.0,
                        "activity": "Ride on Mumbai Agra road",
                        "accomodation": {
                            "hotelName": "Dwaraka",
                            "address": "Dwaraka",
                            "roomType": "TWIN_BED"
                        }
                    },
                    {
                        "dayCount": 3,
                        "place": "NASIK",
                        "distance": 0.0,
                        "activity": "Breakfast, Certifiate distribution and tour ends. Participants return home",
                        "accomodation": {
                            "hotelName": "Dwaraka",
                            "address": "Dwaraka",
                            "roomType": "TWIN_BED"
                        }
                    }
                ]
            },
            "days": 3,
            "nights": 2,
            "difficultyLevel": "MODERATE",
            "startAt": "Mumbai",
            "endAt": "Nasik"
        },
        "bookings": []
    }
```
- (DELETE)deleteBatch
`localhost:8080/batches/1`

### Booking
- (GET)getBookings
`localhost:8080/bookings`
- (POST)bookParticipants
`localhost:8080/batches/book`
```json

{
    "date" : "2023-10-15",
    "amount" : 10000.00,
    "username" : "harsh@gmail.com",
    "batchId" : 3,
    "travellers" : [
        {
            "name" : {
                "first" : "Bhavana",
                "last"  : "Pradhan"
            },
            "mobile" : {
                "number" : "999999922222"
            }
        },
        {
            "name" : {
                "first" : "Ramesh",
                "last"  : "Pradhan"
            },
            "mobile" : {
                "number" : "999999922222"
            }
        }
    ]
}
```

## Tour
- (GET)getTours
`localhost:8080/tours`
```json
{
                    "bookingDate":"12-10-2023",
                    "participants":[
                        {
                            "name":{
                                "first":"Rohit",
                                "last":"Vishwakarma"
                            },
                            "email":{
                                "id":"rohit@gmail.com"
                            },
                            "mobile":{
                                "number":"7972614545"
                            }

                        }




                        {
                            "name":{
                                "first":"Rahul",
                                "last":"Vishwakarma"
                            },
                            "email":{
                                "id":"rahul@gmail.com"
                            },
                            "mobile":{
                                "number":"8788582604"
                            }

                        },



                        "guide":{},
            "bookings":[
                
                    ]
                }
            ]
```
- (GET)getTourById
`localhost:8080/tours/1`
- (GET)DifficultyLevels
`localhost:8080/metadata/difficultyLevels`
- (GET)Modes
`localhost:8080/metadata/modes`
- (GET)RoomTypes
`localhost:8080/metadata/roomTypes`
- (POST)addTour
`localhost:8080/tours`
```json
{
    "name": "MUMBAI-NASIK",
	"startAt" : "Mumbai",
	"endAt" : "Nasik",
    "mode": "BICYCLE",
    "difficultyLevel": "MODERATE",
    "itinerary": {
        "dayPlans": [
            {
                "dayCount": 1,
                "place": "Mumbai",
                "distance": 0.0,
                "activity" : "reporting between 5 pm to 7 pm. Introduction, tour briefing and ice breaker",
                "accomodation" : {
                    "hotelName" : "Hotel Mayur",
                    "address" : "SB road, Thane",
                    "roomType" : "TWIN_BED"
                }
            },
            {
                "dayCount": 2,
                "place": "NASIK",
                "distance": 150.0,
                "activity" : "Ride on Mumbai Agra road",
                "accomodation" : {
                    "hotelName" : "Dwaraka",
                    "address" : "Dwaraka",
                    "roomType" : "TWIN_BED"
                }
            },
            {
                "dayCount": 3,
                "place": "NASIK",
                "distance": 0,
                "activity" : "Breakfast, Certifiate distribution and tour ends. Participants return home",
                "accomodation" : {
                    "hotelName" : "Dwaraka",
                    "address" : "Dwaraka",
                    "roomType" : "TWIN_BED"
                }
            }
        ]
    }
}

```
- (PUT)updateTourById
`localhost:8080/batches`
```json
{
    "id": 1,
    "name": "MUMBAI-GOA",
    "mode": "WALk",
    "noDays": "3",
    "difficulty": "EASY",
    "startAt": "nov",
    "endAt": "jan",
    "itinerary": {
        "id": 2,
        "dailyPlans": [
            {
                "dayCount": 3,
                "place": "DHULE",
                "distanceToCover": 50.0,
                "accomodation": {
                    "hotelName": "Dhule Palace",
                    "address": "102, main crossroad, Dhule-424006",
                    "roomType": "TWIN_BED"
                }
            },
            {
                "dayCount": 0,
                "place": "IGATPURI",
                "distanceToCover": 60.0,
                "accomodation": {
                    "hotelName": "Kasara Hotel",
                    "address": "12, Kasara, Igatpuri-414006",
                    "roomType": "SINGLE"
                }
            },
            {
                "dayCount": 1,
                "place": "NASIK",
                "distanceToCover": 55.0,
                "accomodation": {
                    "hotelName": "Dwarka Palace",
                    "address": "12, Dwarka Chauk, Nasik-414006",
                    "roomType": "SINGLE"
                }
            },
            {
                "dayCount": 2,
                "place": "SHIRPUR",
                "distanceToCover": 30.0,
                "accomodation": {
                    "hotelName": "Shirpur Guest house",
                    "address": "12, MIDC, Shirpur-433006",
                    "roomType": "SINGLE"
                }
            }
        ]
    },
    "batches": [
        {
            "batch_id": 3,
            "startDate": "27-10-2023",
            "endDate": "27-01-2024",
            "status": "ACTIVE",
            "capacity": 50,
            "perParticipantCost": 5999.9,
            "guide": {
                "id": 4,
                "name": {
                    "first": "Rahul",
                    "last": "Vishwakarma"
                },
                "email": {
                    "id": "rahul@gmail.com"
                },
                "mobile": {
                    "number": "8788582604"
                }
            },
            "bookings": []
        }
    ]
}
```
- (PUT)updateTour
`localhost:8080/tours`
```json
 {
        "id": 1,
        "name": "MUMBAI-GOA",
        "mode": "BICYCLE",
        "itinerary": {
            "id": 2,
            "dailyPlans": [
                {
                    "dayCount": 3,
                    "place": "DHULE",
                    "distanceToCover": 50.0,
                    "accomodation": {
                        "hotelName": "Dhule Palace",
                        "address": "102, main crossroad, Dhule-424006",
                        "roomType": "TWIN_BED"
                    }
                },
                {
                    "dayCount": 0,
                    "place": "IGATPURI",
                    "distanceToCover": 60.0,
                    "accomodation": {
                        "hotelName": "Kasara Hotel",
                        "address": "12, Kasara, Igatpuri-414006",
                        "roomType": "SINGLE"
                    }
                },
                {
                    "dayCount": 1,
                    "place": "NASIK",
                    "distanceToCover": 55.0,
                    "accomodation": {
                        "hotelName": "Dwarka Palace",
                        "address": "12, Dwarka Chauk, Nasik-414006",
                        "roomType": "SINGLE"
                    }
                },
                {
                    "dayCount": 2,
                    "place": "SHIRPUR",
                    "distanceToCover": 30.0,
                    "accomodation": {
                        "hotelName": "Shirpur Guest house",
                        "address": "12, MIDC, Shirpur-433006",
                        "roomType": "SINGLE"
                    }
                }
            ]
        },
        "noDays": "3",
        "difficulty": "EASY",
        "startAt": "oct",
        "endAt": "jan",
        "batches": [
            {
                "batch_id": 3,
                "startDate": "27-10-2023",
                "endDate": "27-01-2024",
                "status": "ACTIVE",
                "capacity": 50,
                "perParticipantCost": 5999.9,
                "guide": {
                    "id": 4,
                    "name": {
                        "first": "Rahul",
                        "last": "Vishwakarma"
                    },
                    "email": {
                        "id": "rahul@gmail.com"
                    },
                    "mobile": {
                        "number": "8788582604"
                    }
                },
                "bookings": []
            }
        ]
    }
```
- (DELETE)deleteTour
`localhost:8080/tours/1`
## Auth
- (POST)Register
`localhost:8080/auth/register`
```json
{
    "userName":"harsh@gmail.com",
    "password":"harsh",
    "role":"CUSTOMER"
}
```
- (POST)Login
`localhost:8080/auth/login`
```
{
    "userName":"harsh@gmail.com",
    "password":"harsh"
}
```
