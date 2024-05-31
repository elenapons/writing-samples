# Tutorial: Branded Fares Upsell API with Postman

by Elena Pons

## Introduction

In this tutorial, you will learn to use the Branded Fares Upsell API.

This tutorial will help you familiarize yourself with the process of making requests to the Branded Fares Upsell API using Postman, an application used for API testing. To know more about Postman you can read its [documentation](https://learning.postman.com/docs/getting-started/introduction/).

This tutorial will walk you through simple steps to get an Amadeus developer account, obtain your credentials and make two API requests: one to the Flight Offers Search API and one to the Branded Fares Upsell API. By the end of this tutorial you will have a clear insight into the potential of this API and how it can be integrated with the flight offers search engine.

***What is the Branded Fares Upsell API?***

The Branded Fares API is integrated into the flight booking engine and provides branded fare options for any given flight. Branded fares are airline-created fares that bundle tickets with a variety of products and services such as checked bags, meals, free cancellation, special seats or lounge access. As you will see, the Branded Fares Upsell API provides the branded fares available, along with pricing and a fare description.

Integrating this API is useful for developers wishing to increase booking revenue by recommending higher-value fares during the shopping phase.

**Notice** that branded fares are provided directly by the airlines and therefore, their availability may vary.

### Prerequisites

- [Install Postman](https://www.postman.com/downloads/).
- [Create a Postman](https://www.postman.com/) account (you can sign up for free).

## Get your **Developer Account**

To have access to this API, you will need to have an account on the Amadeus for Developers portal. If you do not have one yet, you can [apply for one here](https://developers.amadeus.com/register).

## Get your API Key and API Secret

Before making any requests to the API, you need to get an API Key and API Secret.

Follow these simple steps in the [Amadeus for Developers portal](https://developers.amadeus.com/) to get your keys:

1. Click on your username (top right corner)
2. Go to **“My Self-Service Workspace”**
3. Click on the **“Create New App”** button
4. Enter your application details and click on **“Create”**. The following screenshot shows you what the form looks like.
    
    ![Screen Shot 2022-05-23 at 13.29.49.png](Tutorial%20Branded%20Fares%20Upsell%20API%20with%20Postman%202c554758d7144afdb845a1e241c43ce9/Screen_Shot_2022-05-23_at_13.29.49.png)
    
5. Once you have created the app, the API Key and API Secret will appear as shown in the following screenshot. 
    
    ![Screen Shot 2022-05-23 at 13.31.31.png](Tutorial%20Branded%20Fares%20Upsell%20API%20with%20Postman%202c554758d7144afdb845a1e241c43ce9/Screen_Shot_2022-05-23_at_13.31.31.png)
    

## Get your access token

The last step before getting to try out the API is getting an access token.

For security purposes, Amadeus uses the oauth2 authorization protocol. Thus, before using the API, you will need to obtain an access token using your API Key and API Secret.

### 1.  Fork the Amadeus for Developers public workspace

Amadeus for Developers has a [Public Workspace](https://www.postman.com/amadeus4dev/workspace/amadeus-for-developers-s-public-workspace/collection/2672636-27471449-d2ca-a8c4-1399-6b0cfbddd079?ctx=documentation) in Postman that includes a public collection you can fork into your workspace.

To that end, click on the Fork icon (next to the Share icon). It should look something like this:

![Screen Shot 2022-05-22 at 19.31.24.png](Tutorial%20Branded%20Fares%20Upsell%20API%20with%20Postman%202c554758d7144afdb845a1e241c43ce9/Screen_Shot_2022-05-22_at_19.31.24.png)

### 2.  Create an Environment & add your credentials

First, go to the Environments tab and click on the “**+”** sign to create a new environment.

Then, fill the table with your API Key (`client_id`) and API Secret (`client_secret`). It should look similar to this:

![Screen Shot 2022-05-22 at 20.32.43.png](Tutorial%20Branded%20Fares%20Upsell%20API%20with%20Postman%202c554758d7144afdb845a1e241c43ce9/Screen_Shot_2022-05-22_at_20.32.43.png)

Finally, go to options (three dots next to the Share button) and select “**Set as Active Environment**”.

### 3.  Get an access token

To get your access token, go to the Amadeus for Developers collection and select `POST` Access Granted Client Credentials in the Authorization folder.

![Screen Shot 2022-05-23 at 13.25.23.png](Tutorial%20Branded%20Fares%20Upsell%20API%20with%20Postman%202c554758d7144afdb845a1e241c43ce9/Screen_Shot_2022-05-23_at_13.25.23.png)

Then click “Send”. It should look similar to this:

![Screen Shot 2022-05-22 at 20.45.04.png](Tutorial%20Branded%20Fares%20Upsell%20API%20with%20Postman%202c554758d7144afdb845a1e241c43ce9/Screen_Shot_2022-05-22_at_20.45.04.png)

The response to this request contains your access token. The Postman collection takes care of updating the token of your environment for you.

```json
{
"type": "amadeusOAuth2Token",
"username": "*****[@****.com](mailto:eponsc@gmail.com)",
"application_name": "tutorial",
"client_id": "nRFvvoie0CeEdPRDhHCme8dfEcbFIxWH",
"token_type": "Bearer",
"access_token": "23Vyqw78RX61AKMj1OdXkGq5aNzn",
"expires_in": 1799,
"state": "approved",
"scope": ""
}
```

—**Now you are ready to use the API!**

**Notice** that the token will expire and you will need to get a new one. Renewing your token is very simple: you will only need to click on “**Send**”. Your token will get stored automatically in your environment and you will be able to continue working.

## Obtaining flights from the Flight Offers Search API

To use the Branded Fares Upsell API, first, you need to find some flight offers for which to get branded fare upsells.

Finding flight offers is easy! You can use the Flight Offers Search API.

The Flight Offers Search API finds the cheapest flight for a given itinerary from over 500 airlines. It returns information on fare details, airline names, baggage allowances and departure terminals.

To obtain a list of flights from the Flight Offers Search API follow these steps:

1. First, select the endpoint `GET` Flight Offers Search in the Amadeus collection.
2. Add some parameters for the search.
    
    For our example, we searched for a return flight from BCN to NYC for November 2022 (for the purposes of this tutorial, we limited the number of results to just one).
    
    **Notice** that you need to use the IATA airport codes.
    
    ![Screen Shot 2022-05-23 at 00.42.53.png](Tutorial%20Branded%20Fares%20Upsell%20API%20with%20Postman%202c554758d7144afdb845a1e241c43ce9/Screen_Shot_2022-05-23_at_00.42.53.png)
    
3. After sending the request you should receive a JSON that looks similar to this one:
- *toggle response*
    
    ```json
    {
        "meta": {
            "count": 1,
            "links": {
                "self": "https://test.api.amadeus.com/v2/shopping/flight-offers?originLocationCode=BCN&destinationLocationCode=NYC&departureDate=2022-11-01&returnDate=2022-11-30&adults=1&max=1"
            }
        },
        "data": [
            {
                "type": "flight-offer",
                "id": "1",
                "source": "GDS",
                "instantTicketingRequired": false,
                "nonHomogeneous": false,
                "oneWay": false,
                "lastTicketingDate": "2022-05-25",
                "numberOfBookableSeats": 7,
                "itineraries": [
                    {
                        "duration": "PT8H55M",
                        "segments": [
                            {
                                "departure": {
                                    "iataCode": "BCN",
                                    "terminal": "1",
                                    "at": "2022-11-01T10:40:00"
                                },
                                "arrival": {
                                    "iataCode": "JFK",
                                    "terminal": "8",
                                    "at": "2022-11-01T14:35:00"
                                },
                                "carrierCode": "AY",
                                "number": "4003",
                                "aircraft": {
                                    "code": "772"
                                },
                                "operating": {
                                    "carrierCode": "AA"
                                },
                                "duration": "PT8H55M",
                                "id": "1",
                                "numberOfStops": 0,
                                "blacklistedInEU": false
                            }
                        ]
                    },
                    {
                        "duration": "PT7H30M",
                        "segments": [
                            {
                                "departure": {
                                    "iataCode": "JFK",
                                    "terminal": "8",
                                    "at": "2022-11-30T19:10:00"
                                },
                                "arrival": {
                                    "iataCode": "BCN",
                                    "terminal": "1",
                                    "at": "2022-12-01T08:40:00"
                                },
                                "carrierCode": "AY",
                                "number": "4004",
                                "aircraft": {
                                    "code": "772"
                                },
                                "operating": {
                                    "carrierCode": "AA"
                                },
                                "duration": "PT7H30M",
                                "id": "2",
                                "numberOfStops": 0,
                                "blacklistedInEU": false
                            }
                        ]
                    }
                ],
                "price": {
                    "currency": "EUR",
                    "total": "327.12",
                    "base": "63.00",
                    "fees": [
                        {
                            "amount": "0.00",
                            "type": "SUPPLIER"
                        },
                        {
                            "amount": "0.00",
                            "type": "TICKETING"
                        }
                    ],
                    "grandTotal": "327.12"
                },
                "pricingOptions": {
                    "fareType": [
                        "PUBLISHED"
                    ],
                    "includedCheckedBagsOnly": false
                },
                "validatingAirlineCodes": [
                    "AY"
                ],
                "travelerPricings": [
                    {
                        "travelerId": "1",
                        "fareOption": "STANDARD",
                        "travelerType": "ADULT",
                        "price": {
                            "currency": "EUR",
                            "total": "327.12",
                            "base": "63.00"
                        },
                        "fareDetailsBySegment": [
                            {
                                "segmentId": "1",
                                "cabin": "ECONOMY",
                                "fareBasis": "OLN7T7B4",
                                "brandedFare": "ELIGHT",
                                "class": "O",
                                "includedCheckedBags": {
                                    "quantity": 0
                                }
                            },
                            {
                                "segmentId": "2",
                                "cabin": "ECONOMY",
                                "fareBasis": "OLN7T7B4",
                                "brandedFare": "ELIGHT",
                                "class": "O",
                                "includedCheckedBags": {
                                    "quantity": 0
                                }
                            }
                        ]
                    }
                ]
            }
        ],
        "dictionaries": {
            "locations": {
                "BCN": {
                    "cityCode": "BCN",
                    "countryCode": "ES"
                },
                "JFK": {
                    "cityCode": "NYC",
                    "countryCode": "US"
                }
            },
            "aircraft": {
                "772": "BOEING 777-200/200ER"
            },
            "currencies": {
                "EUR": "EURO"
            },
            "carriers": {
                "AA": "AMERICAN AIRLINES",
                "AY": "FINNAIR"
            }
        }
    }
    ```
    

The API returned flight offers with the lowest fares. As you can see, the offer of our request includes direct outbound and return flights with no checked baggage for 327,12€.

However, the lowest fares are not necessarily the best! In the following step, you will be able to get the rest of the fares.

## Obtaining branded fare offers

Now that you have got a list of flight offers, let’s search upsell options for our offers.

To obtain the branded fare offers:

1. Select the `POST` Branded Fares Upsell from the Amadeus for Developers collection.
2. Go to the “Body” section.
3. Copy the `data` array from the response in the previous step and paste it into the `flightOffers` array.
4. Send the request.
    - The response should look something like this:
        
        ```json
        {
            "meta": {
                "count": 10
            },
            "data": [
                {
                    "type": "flight-offer",
                    "id": "2",
                    "source": "GDS",
                    "instantTicketingRequired": false,
                    "paymentCardRequired": false,
                    "lastTicketingDate": "2022-05-25",
                    "itineraries": [
                        {
                            "segments": [
                                {
                                    "departure": {
                                        "iataCode": "BCN",
                                        "terminal": "1",
                                        "at": "2022-11-01T10:40:00"
                                    },
                                    "arrival": {
                                        "iataCode": "JFK",
                                        "at": "2022-11-01T14:35:00"
                                    },
                                    "carrierCode": "AY",
                                    "number": "4003",
                                    "aircraft": {
                                        "code": "772"
                                    },
                                    "operating": {
                                        "carrierCode": "AA"
                                    },
                                    "duration": "PT8H55M",
                                    "id": "1",
                                    "numberOfStops": 0,
                                    "blacklistedInEU": false
                                }
                            ]
                        },
                        {
                            "segments": [
                                {
                                    "departure": {
                                        "iataCode": "JFK",
                                        "terminal": "8",
                                        "at": "2022-11-30T19:10:00"
                                    },
                                    "arrival": {
                                        "iataCode": "BCN",
                                        "at": "2022-12-01T08:40:00"
                                    },
                                    "carrierCode": "AY",
                                    "number": "4004",
                                    "aircraft": {
                                        "code": "772"
                                    },
                                    "operating": {
                                        "carrierCode": "AA"
                                    },
                                    "duration": "PT7H30M",
                                    "id": "2",
                                    "numberOfStops": 0,
                                    "blacklistedInEU": false
                                }
                            ]
                        }
                    ],
                    "price": {
                        "currency": "EUR",
                        "total": "327.12",
                        "base": "63.00",
                        "fees": [
                            {
                                "amount": "0.00",
                                "type": "TICKETING"
                            }
                        ],
                        "grandTotal": "327.12"
                    },
                    "pricingOptions": {
                        "fareType": [
                            "PUBLISHED"
                        ],
                        "includedCheckedBagsOnly": false,
                        "refundableFare": false,
                        "noRestrictionFare": false,
                        "noPenaltyFare": false
                    },
                    "validatingAirlineCodes": [
                        "AY"
                    ],
                    "travelerPricings": [
                        {
                            "travelerId": "1",
                            "fareOption": "STANDARD",
                            "travelerType": "ADULT",
                            "price": {
                                "currency": "EUR",
                                "total": "327.12",
                                "base": "63.00",
                                "taxes": [
                                    {
                                        "amount": "6.71",
                                        "code": "XY"
                                    },
                                    {
                                        "amount": "3.27",
                                        "code": "QV"
                                    },
                                    {
                                        "amount": "0.63",
                                        "code": "OG"
                                    },
                                    {
                                        "amount": "5.37",
                                        "code": "AY"
                                    },
                                    {
                                        "amount": "180.00",
                                        "code": "YR"
                                    },
                                    {
                                        "amount": "3.80",
                                        "code": "XA"
                                    },
                                    {
                                        "amount": "16.40",
                                        "code": "JD"
                                    },
                                    {
                                        "amount": "5.86",
                                        "code": "YC"
                                    },
                                    {
                                        "amount": "37.76",
                                        "code": "US"
                                    },
                                    {
                                        "amount": "4.32",
                                        "code": "XF"
                                    }
                                ]
                            },
                            "fareDetailsBySegment": [
                                {
                                    "segmentId": "1",
                                    "cabin": "ECONOMY",
                                    "fareBasis": "OLN7T7B4",
                                    "brandedFare": "ELIGHT",
                                    "class": "O",
                                    "includedCheckedBags": {
                                        "quantity": 0
                                    },
                                    "amenities": [
                                        {
                                            "code": "09P",
                                            "description": "CABIN BAGGAGE",
                                            "isChargeable": false,
                                            "amenityType": "BAGGAGE"
                                        },
                                        {
                                            "code": "04J",
                                            "description": "PERSONAL ITEM",
                                            "isChargeable": false,
                                            "amenityType": "BAGGAGE"
                                        },
                                        {
                                            "code": "06B",
                                            "description": "50PCT FINNAIR PLUS POINTS",
                                            "isChargeable": false,
                                            "amenityType": "BRANDED_FARES"
                                        },
                                        {
                                            "code": "059",
                                            "description": "CHANGEABLE TICKET",
                                            "isChargeable": true,
                                            "amenityType": "BRANDED_FARES"
                                        },
                                        {
                                            "code": "0GO",
                                            "description": "CHECKED BAGGAGE UP TO 23KGS",
                                            "isChargeable": true,
                                            "amenityType": "BAGGAGE"
                                        },
                                        {
                                            "code": "0B3",
                                            "description": "MEAL AND BEVERAGE",
                                            "isChargeable": true,
                                            "amenityType": "MEAL"
                                        },
                                        {
                                            "code": "050",
                                            "description": "STANDARD AND PREFERRED SEATS",
                                            "isChargeable": true,
                                            "amenityType": "BRANDED_FARES"
                                        },
                                        {
                                            "code": "SPS",
                                            "description": "SPECIAL SEATS",
                                            "isChargeable": true,
                                            "amenityType": "BRANDED_FARES"
                                        },
                                        {
                                            "code": "0NI",
                                            "description": "POINT UPGRADE TO HIGHER CABIN",
                                            "isChargeable": true,
                                            "amenityType": "UPGRADES"
                                        },
                                        {
                                            "code": "04D",
                                            "description": "MONEY UPGRADE TO HIGHER CABIN",
                                            "isChargeable": true,
                                            "amenityType": "UPGRADES"
                                        },
                                        {
                                            "code": "04H",
                                            "description": "INTERNET ACCESS USB",
                                            "isChargeable": true,
                                            "amenityType": "ENTERTAINMENT"
                                        },
                                        {
                                            "code": "0BX",
                                            "description": "LOUNGE ACCESS",
                                            "isChargeable": true,
                                            "amenityType": "LOUNGE"
                                        }
                                    ]
                                },
                                {
                                    "segmentId": "2",
                                    "cabin": "ECONOMY",
                                    "fareBasis": "OLN7T7B4",
                                    "brandedFare": "ELIGHT",
                                    "class": "O",
                                    "includedCheckedBags": {
                                        "quantity": 0
                                    },
                                    "amenities": [
                                        {
                                            "code": "09P",
                                            "description": "CABIN BAGGAGE",
                                            "isChargeable": false,
                                            "amenityType": "BAGGAGE"
                                        },
                                        {
                                            "code": "04J",
                                            "description": "PERSONAL ITEM",
                                            "isChargeable": false,
                                            "amenityType": "BAGGAGE"
                                        },
                                        {
                                            "code": "06B",
                                            "description": "50PCT FINNAIR PLUS POINTS",
                                            "isChargeable": false,
                                            "amenityType": "BRANDED_FARES"
                                        },
                                        {
                                            "code": "0GO",
                                            "description": "CHECKED BAGGAGE UP TO 23KGS",
                                            "isChargeable": true,
                                            "amenityType": "BAGGAGE"
                                        },
                                        {
                                            "code": "0B3",
                                            "description": "MEAL AND BEVERAGE",
                                            "isChargeable": true,
                                            "amenityType": "MEAL"
                                        },
                                        {
                                            "code": "050",
                                            "description": "STANDARD AND PREFERRED SEATS",
                                            "isChargeable": true,
                                            "amenityType": "BRANDED_FARES"
                                        },
                                        {
                                            "code": "SPS",
                                            "description": "SPECIAL SEATS",
                                            "isChargeable": true,
                                            "amenityType": "BRANDED_FARES"
                                        },
                                        {
                                            "code": "0NI",
                                            "description": "POINT UPGRADE TO HIGHER CABIN",
                                            "isChargeable": true,
                                            "amenityType": "UPGRADES"
                                        },
                                        {
                                            "code": "04D",
                                            "description": "MONEY UPGRADE TO HIGHER CABIN",
                                            "isChargeable": true,
                                            "amenityType": "UPGRADES"
                                        },
                                        {
                                            "code": "04H",
                                            "description": "INTERNET ACCESS USB",
                                            "isChargeable": true,
                                            "amenityType": "ENTERTAINMENT"
                                        },
                                        {
                                            "code": "0BX",
                                            "description": "LOUNGE ACCESS",
                                            "isChargeable": true,
                                            "amenityType": "LOUNGE"
                                        }
                                    ]
                                }
                            ]
                        }
                    ]
                },
                {
                    "type": "flight-offer",
                    "id": "3",
                    "source": "GDS",
                    "instantTicketingRequired": false,
                    "paymentCardRequired": false,
                    "lastTicketingDate": "2022-05-25",
                    "itineraries": [
                        {
                            "segments": [
                                {
                                    "departure": {
                                        "iataCode": "BCN",
                                        "terminal": "1",
                                        "at": "2022-11-01T10:40:00"
                                    },
                                    "arrival": {
                                        "iataCode": "JFK",
                                        "at": "2022-11-01T14:35:00"
                                    },
                                    "carrierCode": "AY",
                                    "number": "4003",
                                    "aircraft": {
                                        "code": "772"
                                    },
                                    "operating": {
                                        "carrierCode": "AA"
                                    },
                                    "duration": "PT8H55M",
                                    "id": "1",
                                    "numberOfStops": 0,
                                    "blacklistedInEU": false
                                }
                            ]
                        },
                        {
                            "segments": [
                                {
                                    "departure": {
                                        "iataCode": "JFK",
                                        "terminal": "8",
                                        "at": "2022-11-30T19:10:00"
                                    },
                                    "arrival": {
                                        "iataCode": "BCN",
                                        "at": "2022-12-01T08:40:00"
                                    },
                                    "carrierCode": "AY",
                                    "number": "4004",
                                    "aircraft": {
                                        "code": "772"
                                    },
                                    "operating": {
                                        "carrierCode": "AA"
                                    },
                                    "duration": "PT7H30M",
                                    "id": "2",
                                    "numberOfStops": 0,
                                    "blacklistedInEU": false
                                }
                            ]
                        }
                    ],
                    "price": {
                        "currency": "EUR",
                        "total": "427.12",
                        "base": "163.00",
                        "fees": [
                            {
                                "amount": "0.00",
                                "type": "TICKETING"
                            }
                        ],
                        "grandTotal": "427.12"
                    },
                    "pricingOptions": {
                        "fareType": [
                            "PUBLISHED"
                        ],
                        "includedCheckedBagsOnly": false,
                        "refundableFare": false,
                        "noRestrictionFare": false,
                        "noPenaltyFare": false
                    },
                    "validatingAirlineCodes": [
                        "AY"
                    ],
                    "travelerPricings": [
                        {
                            "travelerId": "1",
                            "fareOption": "STANDARD",
                            "travelerType": "ADULT",
                            "price": {
                                "currency": "EUR",
                                "total": "427.12",
                                "base": "163.00",
                                "taxes": [
                                    {
                                        "amount": "6.71",
                                        "code": "XY"
                                    },
                                    {
                                        "amount": "3.27",
                                        "code": "QV"
                                    },
                                    {
                                        "amount": "0.63",
                                        "code": "OG"
                                    },
                                    {
                                        "amount": "5.37",
                                        "code": "AY"
                                    },
                                    {
                                        "amount": "180.00",
                                        "code": "YR"
                                    },
                                    {
                                        "amount": "3.80",
                                        "code": "XA"
                                    },
                                    {
                                        "amount": "16.40",
                                        "code": "JD"
                                    },
                                    {
                                        "amount": "5.86",
                                        "code": "YC"
                                    },
                                    {
                                        "amount": "37.76",
                                        "code": "US"
                                    },
                                    {
                                        "amount": "4.32",
                                        "code": "XF"
                                    }
                                ]
                            },
                            "fareDetailsBySegment": [
                                {
                                    "segmentId": "1",
                                    "cabin": "ECONOMY",
                                    "fareBasis": "OLN7T7M4",
                                    "brandedFare": "ECAMP",
                                    "class": "O",
                                    "includedCheckedBags": {
                                        "quantity": 1
                                    },
                                    "amenities": [
                                        {
                                            "code": "09P",
                                            "description": "CABIN BAGGAGE",
                                            "isChargeable": false,
                                            "amenityType": "BAGGAGE"
                                        },
                                        {
                                            "code": "0GO",
                                            "description": "CHECKED BAGGAGE UP TO 23KGS",
                                            "isChargeable": false,
                                            "amenityType": "BAGGAGE"
                                        },
                                        {
                                            "code": "04J",
                                            "description": "PERSONAL ITEM",
                                            "isChargeable": false,
                                            "amenityType": "BAGGAGE"
                                        },
                                        {
                                            "code": "0B3",
                                            "description": "MEAL AND BEVERAGE",
                                            "isChargeable": false,
                                            "amenityType": "MEAL"
                                        },
                                        {
                                            "code": "06D",
                                            "description": "100PCT FINNAIR PLUS POINTS",
                                            "isChargeable": false,
                                            "amenityType": "BRANDED_FARES"
                                        },
                                        {
                                            "code": "059",
                                            "description": "CHANGEABLE TICKET",
                                            "isChargeable": true,
                                            "amenityType": "BRANDED_FARES"
                                        },
                                        {
                                            "code": "050",
                                            "description": "STANDARD AND PREFERRED SEATS",
                                            "isChargeable": true,
                                            "amenityType": "BRANDED_FARES"
                                        },
                                        {
                                            "code": "SPS",
                                            "description": "SPECIAL SEATS",
                                            "isChargeable": true,
                                            "amenityType": "BRANDED_FARES"
                                        },
                                        {
                                            "code": "0NI",
                                            "description": "POINT UPGRADE TO HIGHER CABIN",
                                            "isChargeable": true,
                                            "amenityType": "UPGRADES"
                                        },
                                        {
                                            "code": "04D",
                                            "description": "MONEY UPGRADE TO HIGHER CABIN",
                                            "isChargeable": true,
                                            "amenityType": "UPGRADES"
                                        },
                                        {
                                            "code": "04H",
                                            "description": "INTERNET ACCESS USB",
                                            "isChargeable": true,
                                            "amenityType": "ENTERTAINMENT"
                                        },
                                        {
                                            "code": "0BX",
                                            "description": "LOUNGE ACCESS",
                                            "isChargeable": true,
                                            "amenityType": "LOUNGE"
                                        }
                                    ]
                                },
                                {
                                    "segmentId": "2",
                                    "cabin": "ECONOMY",
                                    "fareBasis": "OLN7T7M4",
                                    "brandedFare": "ECAMP",
                                    "class": "O",
                                    "includedCheckedBags": {
                                        "quantity": 1
                                    }
                                }
                            ]
                        }
                    ]
                },
                {
                    "type": "flight-offer",
                    "id": "4",
                    "source": "GDS",
                    "instantTicketingRequired": false,
                    "paymentCardRequired": false,
                    "lastTicketingDate": "2022-05-25",
                    "itineraries": [
                        {
                            "segments": [
                                {
                                    "departure": {
                                        "iataCode": "BCN",
                                        "terminal": "1",
                                        "at": "2022-11-01T10:40:00"
                                    },
                                    "arrival": {
                                        "iataCode": "JFK",
                                        "at": "2022-11-01T14:35:00"
                                    },
                                    "carrierCode": "AY",
                                    "number": "4003",
                                    "aircraft": {
                                        "code": "772"
                                    },
                                    "operating": {
                                        "carrierCode": "AA"
                                    },
                                    "duration": "PT8H55M",
                                    "id": "1",
                                    "numberOfStops": 0,
                                    "blacklistedInEU": false
                                }
                            ]
                        },
                        {
                            "segments": [
                                {
                                    "departure": {
                                        "iataCode": "JFK",
                                        "terminal": "8",
                                        "at": "2022-11-30T19:10:00"
                                    },
                                    "arrival": {
                                        "iataCode": "BCN",
                                        "at": "2022-12-01T08:40:00"
                                    },
                                    "carrierCode": "AY",
                                    "number": "4004",
                                    "aircraft": {
                                        "code": "772"
                                    },
                                    "operating": {
                                        "carrierCode": "AA"
                                    },
                                    "duration": "PT7H30M",
                                    "id": "2",
                                    "numberOfStops": 0,
                                    "blacklistedInEU": false
                                }
                            ]
                        }
                    ],
                    "price": {
                        "currency": "EUR",
                        "total": "677.12",
                        "base": "413.00",
                        "fees": [
                            {
                                "amount": "0.00",
                                "type": "TICKETING"
                            }
                        ],
                        "grandTotal": "677.12"
                    },
                    "pricingOptions": {
                        "fareType": [
                            "PUBLISHED"
                        ],
                        "includedCheckedBagsOnly": false,
                        "refundableFare": false,
                        "noRestrictionFare": false,
                        "noPenaltyFare": false
                    },
                    "validatingAirlineCodes": [
                        "AY"
                    ],
                    "travelerPricings": [
                        {
                            "travelerId": "1",
                            "fareOption": "STANDARD",
                            "travelerType": "ADULT",
                            "price": {
                                "currency": "EUR",
                                "total": "677.12",
                                "base": "413.00",
                                "taxes": [
                                    {
                                        "amount": "6.71",
                                        "code": "XY"
                                    },
                                    {
                                        "amount": "3.27",
                                        "code": "QV"
                                    },
                                    {
                                        "amount": "0.63",
                                        "code": "OG"
                                    },
                                    {
                                        "amount": "5.37",
                                        "code": "AY"
                                    },
                                    {
                                        "amount": "180.00",
                                        "code": "YR"
                                    },
                                    {
                                        "amount": "3.80",
                                        "code": "XA"
                                    },
                                    {
                                        "amount": "16.40",
                                        "code": "JD"
                                    },
                                    {
                                        "amount": "5.86",
                                        "code": "YC"
                                    },
                                    {
                                        "amount": "37.76",
                                        "code": "US"
                                    },
                                    {
                                        "amount": "4.32",
                                        "code": "XF"
                                    }
                                ]
                            },
                            "fareDetailsBySegment": [
                                {
                                    "segmentId": "1",
                                    "cabin": "ECONOMY",
                                    "fareBasis": "OLN7T7M6",
                                    "brandedFare": "ECLASSIC",
                                    "class": "O",
                                    "includedCheckedBags": {
                                        "quantity": 1
                                    },
                                    "amenities": [
                                        {
                                            "code": "059",
                                            "description": "CHANGEABLE TICKET",
                                            "isChargeable": false,
                                            "amenityType": "BRANDED_FARES"
                                        },
                                        {
                                            "code": "09P",
                                            "description": "CABIN BAGGAGE",
                                            "isChargeable": false,
                                            "amenityType": "BAGGAGE"
                                        },
                                        {
                                            "code": "0GO",
                                            "description": "CHECKED BAGGAGE UP TO 23KGS",
                                            "isChargeable": false,
                                            "amenityType": "BAGGAGE"
                                        },
                                        {
                                            "code": "04J",
                                            "description": "PERSONAL ITEM",
                                            "isChargeable": false,
                                            "amenityType": "BAGGAGE"
                                        },
                                        {
                                            "code": "0B3",
                                            "description": "MEAL AND BEVERAGE",
                                            "isChargeable": false,
                                            "amenityType": "MEAL"
                                        },
                                        {
                                            "code": "06D",
                                            "description": "100PCT FINNAIR PLUS POINTS",
                                            "isChargeable": false,
                                            "amenityType": "BRANDED_FARES"
                                        },
                                        {
                                            "code": "050",
                                            "description": "STANDARD AND PREFERRED SEATS",
                                            "isChargeable": true,
                                            "amenityType": "BRANDED_FARES"
                                        },
                                        {
                                            "code": "SPS",
                                            "description": "SPECIAL SEATS",
                                            "isChargeable": true,
                                            "amenityType": "BRANDED_FARES"
                                        },
                                        {
                                            "code": "0NI",
                                            "description": "POINT UPGRADE TO HIGHER CABIN",
                                            "isChargeable": true,
                                            "amenityType": "UPGRADES"
                                        },
                                        {
                                            "code": "04D",
                                            "description": "MONEY UPGRADE TO HIGHER CABIN",
                                            "isChargeable": true,
                                            "amenityType": "UPGRADES"
                                        },
                                        {
                                            "code": "04H",
                                            "description": "INTERNET ACCESS USB",
                                            "isChargeable": true,
                                            "amenityType": "ENTERTAINMENT"
                                        },
                                        {
                                            "code": "0BX",
                                            "description": "LOUNGE ACCESS",
                                            "isChargeable": true,
                                            "amenityType": "LOUNGE"
                                        }
                                    ]
                                },
                                {
                                    "segmentId": "2",
                                    "cabin": "ECONOMY",
                                    "fareBasis": "OLN7T7M6",
                                    "brandedFare": "ECLASSIC",
                                    "class": "O",
                                    "includedCheckedBags": {
                                        "quantity": 1
                                    },
                                    "amenities": [
                                        {
                                            "code": "059",
                                            "description": "CHANGEABLE TICKET",
                                            "isChargeable": false,
                                            "amenityType": "BRANDED_FARES"
                                        },
                                        {
                                            "code": "09P",
                                            "description": "CABIN BAGGAGE",
                                            "isChargeable": false,
                                            "amenityType": "BAGGAGE"
                                        },
                                        {
                                            "code": "0GO",
                                            "description": "CHECKED BAGGAGE UP TO 23KGS",
                                            "isChargeable": false,
                                            "amenityType": "BAGGAGE"
                                        },
                                        {
                                            "code": "04J",
                                            "description": "PERSONAL ITEM",
                                            "isChargeable": false,
                                            "amenityType": "BAGGAGE"
                                        },
                                        {
                                            "code": "0B3",
                                            "description": "MEAL AND BEVERAGE",
                                            "isChargeable": false,
                                            "amenityType": "MEAL"
                                        },
                                        {
                                            "code": "06D",
                                            "description": "100PCT FINNAIR PLUS POINTS",
                                            "isChargeable": false,
                                            "amenityType": "BRANDED_FARES"
                                        },
                                        {
                                            "code": "050",
                                            "description": "STANDARD AND PREFERRED SEATS",
                                            "isChargeable": true,
                                            "amenityType": "BRANDED_FARES"
                                        },
                                        {
                                            "code": "SPS",
                                            "description": "SPECIAL SEATS",
                                            "isChargeable": true,
                                            "amenityType": "BRANDED_FARES"
                                        },
                                        {
                                            "code": "0NI",
                                            "description": "POINT UPGRADE TO HIGHER CABIN",
                                            "isChargeable": true,
                                            "amenityType": "UPGRADES"
                                        },
                                        {
                                            "code": "04D",
                                            "description": "MONEY UPGRADE TO HIGHER CABIN",
                                            "isChargeable": true,
                                            "amenityType": "UPGRADES"
                                        },
                                        {
                                            "code": "04H",
                                            "description": "INTERNET ACCESS USB",
                                            "isChargeable": true,
                                            "amenityType": "ENTERTAINMENT"
                                        },
                                        {
                                            "code": "0BX",
                                            "description": "LOUNGE ACCESS",
                                            "isChargeable": true,
                                            "amenityType": "LOUNGE"
                                        }
                                    ]
                                }
                            ]
                        }
                    ]
                },
                {
                    "type": "flight-offer",
                    "id": "5",
                    "source": "GDS",
                    "instantTicketingRequired": false,
                    "paymentCardRequired": false,
                    "lastTicketingDate": "2022-05-25",
                    "itineraries": [
                        {
                            "segments": [
                                {
                                    "departure": {
                                        "iataCode": "BCN",
                                        "terminal": "1",
                                        "at": "2022-11-01T10:40:00"
                                    },
                                    "arrival": {
                                        "iataCode": "JFK",
                                        "at": "2022-11-01T14:35:00"
                                    },
                                    "carrierCode": "AY",
                                    "number": "4003",
                                    "aircraft": {
                                        "code": "772"
                                    },
                                    "operating": {
                                        "carrierCode": "AA"
                                    },
                                    "duration": "PT8H55M",
                                    "id": "1",
                                    "numberOfStops": 0,
                                    "blacklistedInEU": false
                                }
                            ]
                        },
                        {
                            "segments": [
                                {
                                    "departure": {
                                        "iataCode": "JFK",
                                        "terminal": "8",
                                        "at": "2022-11-30T19:10:00"
                                    },
                                    "arrival": {
                                        "iataCode": "BCN",
                                        "at": "2022-12-01T08:40:00"
                                    },
                                    "carrierCode": "AY",
                                    "number": "4004",
                                    "aircraft": {
                                        "code": "772"
                                    },
                                    "operating": {
                                        "carrierCode": "AA"
                                    },
                                    "duration": "PT7H30M",
                                    "id": "2",
                                    "numberOfStops": 0,
                                    "blacklistedInEU": false
                                }
                            ]
                        }
                    ],
                    "price": {
                        "currency": "EUR",
                        "total": "1668.12",
                        "base": "1084.00",
                        "fees": [
                            {
                                "amount": "0.00",
                                "type": "TICKETING"
                            }
                        ],
                        "grandTotal": "1668.12"
                    },
                    "pricingOptions": {
                        "fareType": [
                            "PUBLISHED"
                        ],
                        "includedCheckedBagsOnly": false,
                        "refundableFare": false,
                        "noRestrictionFare": false,
                        "noPenaltyFare": false
                    },
                    "validatingAirlineCodes": [
                        "AY"
                    ],
                    "travelerPricings": [
                        {
                            "travelerId": "1",
                            "fareOption": "STANDARD",
                            "travelerType": "ADULT",
                            "price": {
                                "currency": "EUR",
                                "total": "1668.12",
                                "base": "1084.00",
                                "taxes": [
                                    {
                                        "amount": "6.71",
                                        "code": "XY"
                                    },
                                    {
                                        "amount": "3.27",
                                        "code": "QV"
                                    },
                                    {
                                        "amount": "0.63",
                                        "code": "OG"
                                    },
                                    {
                                        "amount": "5.37",
                                        "code": "AY"
                                    },
                                    {
                                        "amount": "500.00",
                                        "code": "YR"
                                    },
                                    {
                                        "amount": "3.80",
                                        "code": "XA"
                                    },
                                    {
                                        "amount": "16.40",
                                        "code": "JD"
                                    },
                                    {
                                        "amount": "5.86",
                                        "code": "YC"
                                    },
                                    {
                                        "amount": "37.76",
                                        "code": "US"
                                    },
                                    {
                                        "amount": "4.32",
                                        "code": "XF"
                                    }
                                ]
                            },
                            "fareDetailsBySegment": [
                                {
                                    "segmentId": "1",
                                    "cabin": "BUSINESS",
                                    "fareBasis": "INX9C1S4",
                                    "brandedFare": "BCAMP",
                                    "class": "I",
                                    "includedCheckedBags": {
                                        "quantity": 2
                                    },
                                    "amenities": [
                                        {
                                            "code": "09P",
                                            "description": "CABIN BAGGAGE",
                                            "isChargeable": false,
                                            "amenityType": "BAGGAGE"
                                        },
                                        {
                                            "code": "0C6",
                                            "description": "CHECKED BAGGAGE UPTO 32KGS",
                                            "isChargeable": false,
                                            "amenityType": "BAGGAGE"
                                        },
                                        {
                                            "code": "04J",
                                            "description": "PERSONAL ITEM",
                                            "isChargeable": false,
                                            "amenityType": "BAGGAGE"
                                        },
                                        {
                                            "code": "0LF",
                                            "description": "PRIORITY BAGGAGE",
                                            "isChargeable": false,
                                            "amenityType": "TRAVEL_SERVICES"
                                        },
                                        {
                                            "code": "0B3",
                                            "description": "MEAL AND BEVERAGE",
                                            "isChargeable": false,
                                            "amenityType": "MEAL"
                                        },
                                        {
                                            "code": "06N",
                                            "description": "200PCT FINNAIR PLUS POINTS",
                                            "isChargeable": false,
                                            "amenityType": "BRANDED_FARES"
                                        },
                                        {
                                            "code": "0NI",
                                            "description": "POINT UPGRADE TO HIGHER CABIN",
                                            "isChargeable": false,
                                            "amenityType": "UPGRADES"
                                        },
                                        {
                                            "code": "04D",
                                            "description": "MONEY UPGRADE TO HIGHER CABIN",
                                            "isChargeable": false,
                                            "amenityType": "UPGRADES"
                                        },
                                        {
                                            "code": "04H",
                                            "description": "INTERNET ACCESS USB",
                                            "isChargeable": false,
                                            "amenityType": "ENTERTAINMENT"
                                        },
                                        {
                                            "code": "0BX",
                                            "description": "LOUNGE ACCESS",
                                            "isChargeable": false,
                                            "amenityType": "LOUNGE"
                                        },
                                        {
                                            "code": "PSB",
                                            "description": "PRIORITY SECURITY AND BOARDING",
                                            "isChargeable": false,
                                            "amenityType": "TRAVEL_SERVICES"
                                        },
                                        {
                                            "code": "03P",
                                            "description": "PRIORITY CHECK IN",
                                            "isChargeable": false,
                                            "amenityType": "TRAVEL_SERVICES"
                                        },
                                        {
                                            "code": "059",
                                            "description": "CHANGEABLE TICKET",
                                            "isChargeable": true,
                                            "amenityType": "BRANDED_FARES"
                                        },
                                        {
                                            "code": "050",
                                            "description": "STANDARD AND PREFERRED SEATS",
                                            "isChargeable": true,
                                            "amenityType": "BRANDED_FARES"
                                        }
                                    ]
                                },
                                {
                                    "segmentId": "2",
                                    "cabin": "BUSINESS",
                                    "fareBasis": "INX9C1S4",
                                    "brandedFare": "BCAMP",
                                    "class": "I",
                                    "includedCheckedBags": {
                                        "quantity": 2
                                    }
                                }
                            ]
                        }
                    ]
                },
                {
                    "type": "flight-offer",
                    "id": "6",
                    "source": "GDS",
                    "instantTicketingRequired": false,
                    "paymentCardRequired": false,
                    "lastTicketingDate": "2022-05-25",
                    "itineraries": [
                        {
                            "segments": [
                                {
                                    "departure": {
                                        "iataCode": "BCN",
                                        "terminal": "1",
                                        "at": "2022-11-01T10:40:00"
                                    },
                                    "arrival": {
                                        "iataCode": "JFK",
                                        "at": "2022-11-01T14:35:00"
                                    },
                                    "carrierCode": "AY",
                                    "number": "4003",
                                    "aircraft": {
                                        "code": "772"
                                    },
                                    "operating": {
                                        "carrierCode": "AA"
                                    },
                                    "duration": "PT8H55M",
                                    "id": "1",
                                    "numberOfStops": 0,
                                    "blacklistedInEU": false
                                }
                            ]
                        },
                        {
                            "segments": [
                                {
                                    "departure": {
                                        "iataCode": "JFK",
                                        "terminal": "8",
                                        "at": "2022-11-30T19:10:00"
                                    },
                                    "arrival": {
                                        "iataCode": "BCN",
                                        "at": "2022-12-01T08:40:00"
                                    },
                                    "carrierCode": "AY",
                                    "number": "4004",
                                    "aircraft": {
                                        "code": "772"
                                    },
                                    "operating": {
                                        "carrierCode": "AA"
                                    },
                                    "duration": "PT7H30M",
                                    "id": "2",
                                    "numberOfStops": 0,
                                    "blacklistedInEU": false
                                }
                            ]
                        }
                    ],
                    "price": {
                        "currency": "EUR",
                        "total": "2268.12",
                        "base": "1684.00",
                        "fees": [
                            {
                                "amount": "0.00",
                                "type": "TICKETING"
                            }
                        ],
                        "grandTotal": "2268.12"
                    },
                    "pricingOptions": {
                        "fareType": [
                            "PUBLISHED"
                        ],
                        "includedCheckedBagsOnly": false,
                        "refundableFare": false,
                        "noRestrictionFare": false,
                        "noPenaltyFare": false
                    },
                    "validatingAirlineCodes": [
                        "AY"
                    ],
                    "travelerPricings": [
                        {
                            "travelerId": "1",
                            "fareOption": "STANDARD",
                            "travelerType": "ADULT",
                            "price": {
                                "currency": "EUR",
                                "total": "2268.12",
                                "base": "1684.00",
                                "taxes": [
                                    {
                                        "amount": "6.71",
                                        "code": "XY"
                                    },
                                    {
                                        "amount": "3.27",
                                        "code": "QV"
                                    },
                                    {
                                        "amount": "0.63",
                                        "code": "OG"
                                    },
                                    {
                                        "amount": "5.37",
                                        "code": "AY"
                                    },
                                    {
                                        "amount": "500.00",
                                        "code": "YR"
                                    },
                                    {
                                        "amount": "3.80",
                                        "code": "XA"
                                    },
                                    {
                                        "amount": "16.40",
                                        "code": "JD"
                                    },
                                    {
                                        "amount": "5.86",
                                        "code": "YC"
                                    },
                                    {
                                        "amount": "37.76",
                                        "code": "US"
                                    },
                                    {
                                        "amount": "4.32",
                                        "code": "XF"
                                    }
                                ]
                            },
                            "fareDetailsBySegment": [
                                {
                                    "segmentId": "1",
                                    "cabin": "BUSINESS",
                                    "fareBasis": "INX9C1S6",
                                    "brandedFare": "BCLASSIC",
                                    "class": "I",
                                    "includedCheckedBags": {
                                        "quantity": 2
                                    },
                                    "amenities": [
                                        {
                                            "code": "059",
                                            "description": "CHANGEABLE TICKET",
                                            "isChargeable": false,
                                            "amenityType": "BRANDED_FARES"
                                        },
                                        {
                                            "code": "09P",
                                            "description": "CABIN BAGGAGE",
                                            "isChargeable": false,
                                            "amenityType": "BAGGAGE"
                                        },
                                        {
                                            "code": "0C6",
                                            "description": "CHECKED BAGGAGE UPTO 32KGS",
                                            "isChargeable": false,
                                            "amenityType": "BAGGAGE"
                                        },
                                        {
                                            "code": "04J",
                                            "description": "PERSONAL ITEM",
                                            "isChargeable": false,
                                            "amenityType": "BAGGAGE"
                                        },
                                        {
                                            "code": "0LF",
                                            "description": "PRIORITY BAGGAGE",
                                            "isChargeable": false,
                                            "amenityType": "TRAVEL_SERVICES"
                                        },
                                        {
                                            "code": "0B3",
                                            "description": "MEAL AND BEVERAGE",
                                            "isChargeable": false,
                                            "amenityType": "MEAL"
                                        },
                                        {
                                            "code": "06N",
                                            "description": "200PCT FINNAIR PLUS POINTS",
                                            "isChargeable": false,
                                            "amenityType": "BRANDED_FARES"
                                        },
                                        {
                                            "code": "0NI",
                                            "description": "POINT UPGRADE TO HIGHER CABIN",
                                            "isChargeable": false,
                                            "amenityType": "UPGRADES"
                                        },
                                        {
                                            "code": "04D",
                                            "description": "MONEY UPGRADE TO HIGHER CABIN",
                                            "isChargeable": false,
                                            "amenityType": "UPGRADES"
                                        },
                                        {
                                            "code": "04H",
                                            "description": "INTERNET ACCESS USB",
                                            "isChargeable": false,
                                            "amenityType": "ENTERTAINMENT"
                                        },
                                        {
                                            "code": "0BX",
                                            "description": "LOUNGE ACCESS",
                                            "isChargeable": false,
                                            "amenityType": "LOUNGE"
                                        },
                                        {
                                            "code": "PSB",
                                            "description": "PRIORITY SECURITY AND BOARDING",
                                            "isChargeable": false,
                                            "amenityType": "TRAVEL_SERVICES"
                                        },
                                        {
                                            "code": "03P",
                                            "description": "PRIORITY CHECK IN",
                                            "isChargeable": false,
                                            "amenityType": "TRAVEL_SERVICES"
                                        },
                                        {
                                            "code": "050",
                                            "description": "STANDARD AND PREFERRED SEATS",
                                            "isChargeable": true,
                                            "amenityType": "BRANDED_FARES"
                                        }
                                    ]
                                },
                                {
                                    "segmentId": "2",
                                    "cabin": "BUSINESS",
                                    "fareBasis": "INX9C1S6",
                                    "brandedFare": "BCLASSIC",
                                    "class": "I",
                                    "includedCheckedBags": {
                                        "quantity": 2
                                    },
                                    "amenities": [
                                        {
                                            "code": "059",
                                            "description": "CHANGEABLE TICKET",
                                            "isChargeable": false,
                                            "amenityType": "BRANDED_FARES"
                                        },
                                        {
                                            "code": "09P",
                                            "description": "CABIN BAGGAGE",
                                            "isChargeable": false,
                                            "amenityType": "BAGGAGE"
                                        },
                                        {
                                            "code": "0C6",
                                            "description": "CHECKED BAGGAGE UPTO 32KGS",
                                            "isChargeable": false,
                                            "amenityType": "BAGGAGE"
                                        },
                                        {
                                            "code": "04J",
                                            "description": "PERSONAL ITEM",
                                            "isChargeable": false,
                                            "amenityType": "BAGGAGE"
                                        },
                                        {
                                            "code": "0LF",
                                            "description": "PRIORITY BAGGAGE",
                                            "isChargeable": false,
                                            "amenityType": "TRAVEL_SERVICES"
                                        },
                                        {
                                            "code": "0B3",
                                            "description": "MEAL AND BEVERAGE",
                                            "isChargeable": false,
                                            "amenityType": "MEAL"
                                        },
                                        {
                                            "code": "06N",
                                            "description": "200PCT FINNAIR PLUS POINTS",
                                            "isChargeable": false,
                                            "amenityType": "BRANDED_FARES"
                                        },
                                        {
                                            "code": "04H",
                                            "description": "INTERNET ACCESS USB",
                                            "isChargeable": false,
                                            "amenityType": "ENTERTAINMENT"
                                        },
                                        {
                                            "code": "0BX",
                                            "description": "LOUNGE ACCESS",
                                            "isChargeable": false,
                                            "amenityType": "LOUNGE"
                                        },
                                        {
                                            "code": "PSB",
                                            "description": "PRIORITY SECURITY AND BOARDING",
                                            "isChargeable": false,
                                            "amenityType": "TRAVEL_SERVICES"
                                        },
                                        {
                                            "code": "03P",
                                            "description": "PRIORITY CHECK IN",
                                            "isChargeable": false,
                                            "amenityType": "TRAVEL_SERVICES"
                                        },
                                        {
                                            "code": "050",
                                            "description": "STANDARD AND PREFERRED SEATS",
                                            "isChargeable": true,
                                            "amenityType": "BRANDED_FARES"
                                        }
                                    ]
                                }
                            ]
                        }
                    ]
                },
                {
                    "type": "flight-offer",
                    "id": "7",
                    "source": "GDS",
                    "instantTicketingRequired": false,
                    "paymentCardRequired": false,
                    "lastTicketingDate": "2022-05-25",
                    "itineraries": [
                        {
                            "segments": [
                                {
                                    "departure": {
                                        "iataCode": "BCN",
                                        "terminal": "1",
                                        "at": "2022-11-01T10:40:00"
                                    },
                                    "arrival": {
                                        "iataCode": "JFK",
                                        "at": "2022-11-01T14:35:00"
                                    },
                                    "carrierCode": "AY",
                                    "number": "4003",
                                    "aircraft": {
                                        "code": "772"
                                    },
                                    "operating": {
                                        "carrierCode": "AA"
                                    },
                                    "duration": "PT8H55M",
                                    "id": "1",
                                    "numberOfStops": 0,
                                    "blacklistedInEU": false
                                }
                            ]
                        },
                        {
                            "segments": [
                                {
                                    "departure": {
                                        "iataCode": "JFK",
                                        "terminal": "8",
                                        "at": "2022-11-30T19:10:00"
                                    },
                                    "arrival": {
                                        "iataCode": "BCN",
                                        "at": "2022-12-01T08:40:00"
                                    },
                                    "carrierCode": "AY",
                                    "number": "4004",
                                    "aircraft": {
                                        "code": "772"
                                    },
                                    "operating": {
                                        "carrierCode": "AA"
                                    },
                                    "duration": "PT7H30M",
                                    "id": "2",
                                    "numberOfStops": 0,
                                    "blacklistedInEU": false
                                }
                            ]
                        }
                    ],
                    "price": {
                        "currency": "EUR",
                        "total": "2279.12",
                        "base": "2015.00",
                        "fees": [
                            {
                                "amount": "0.00",
                                "type": "TICKETING"
                            }
                        ],
                        "grandTotal": "2279.12"
                    },
                    "pricingOptions": {
                        "fareType": [
                            "PUBLISHED"
                        ],
                        "includedCheckedBagsOnly": false,
                        "refundableFare": false,
                        "noRestrictionFare": false,
                        "noPenaltyFare": false
                    },
                    "validatingAirlineCodes": [
                        "AY"
                    ],
                    "travelerPricings": [
                        {
                            "travelerId": "1",
                            "fareOption": "STANDARD",
                            "travelerType": "ADULT",
                            "price": {
                                "currency": "EUR",
                                "total": "2279.12",
                                "base": "2015.00",
                                "taxes": [
                                    {
                                        "amount": "6.71",
                                        "code": "XY"
                                    },
                                    {
                                        "amount": "3.27",
                                        "code": "QV"
                                    },
                                    {
                                        "amount": "0.63",
                                        "code": "OG"
                                    },
                                    {
                                        "amount": "5.37",
                                        "code": "AY"
                                    },
                                    {
                                        "amount": "180.00",
                                        "code": "YR"
                                    },
                                    {
                                        "amount": "3.80",
                                        "code": "XA"
                                    },
                                    {
                                        "amount": "16.40",
                                        "code": "JD"
                                    },
                                    {
                                        "amount": "5.86",
                                        "code": "YC"
                                    },
                                    {
                                        "amount": "37.76",
                                        "code": "US"
                                    },
                                    {
                                        "amount": "4.32",
                                        "code": "XF"
                                    }
                                ]
                            },
                            "fareDetailsBySegment": [
                                {
                                    "segmentId": "1",
                                    "cabin": "PREMIUM_ECONOMY",
                                    "fareBasis": "TLX8C0S4",
                                    "brandedFare": "PECAMP",
                                    "class": "T",
                                    "includedCheckedBags": {
                                        "quantity": 2
                                    },
                                    "amenities": [
                                        {
                                            "code": "09P",
                                            "description": "CABIN BAGGAGE",
                                            "isChargeable": false,
                                            "amenityType": "BAGGAGE"
                                        },
                                        {
                                            "code": "0GO",
                                            "description": "CHECKED BAGGAGE UP TO 23KGS",
                                            "isChargeable": false,
                                            "amenityType": "BAGGAGE"
                                        },
                                        {
                                            "code": "04J",
                                            "description": "PERSONAL ITEM",
                                            "isChargeable": false,
                                            "amenityType": "BAGGAGE"
                                        },
                                        {
                                            "code": "0B3",
                                            "description": "MEAL AND BEVERAGE",
                                            "isChargeable": false,
                                            "amenityType": "MEAL"
                                        },
                                        {
                                            "code": "06M",
                                            "description": "150PCT FINNAIR PLUS POINTS",
                                            "isChargeable": false,
                                            "amenityType": "BRANDED_FARES"
                                        },
                                        {
                                            "code": "0NI",
                                            "description": "POINT UPGRADE TO HIGHER CABIN",
                                            "isChargeable": false,
                                            "amenityType": "UPGRADES"
                                        },
                                        {
                                            "code": "04D",
                                            "description": "MONEY UPGRADE TO HIGHER CABIN",
                                            "isChargeable": false,
                                            "amenityType": "UPGRADES"
                                        },
                                        {
                                            "code": "059",
                                            "description": "CHANGEABLE TICKET",
                                            "isChargeable": true,
                                            "amenityType": "BRANDED_FARES"
                                        },
                                        {
                                            "code": "050",
                                            "description": "STANDARD AND PREFERRED SEATS",
                                            "isChargeable": true,
                                            "amenityType": "BRANDED_FARES"
                                        },
                                        {
                                            "code": "04H",
                                            "description": "INTERNET ACCESS USB",
                                            "isChargeable": true,
                                            "amenityType": "ENTERTAINMENT"
                                        },
                                        {
                                            "code": "0BX",
                                            "description": "LOUNGE ACCESS",
                                            "isChargeable": true,
                                            "amenityType": "LOUNGE"
                                        }
                                    ]
                                },
                                {
                                    "segmentId": "2",
                                    "cabin": "PREMIUM_ECONOMY",
                                    "fareBasis": "TLX8C0S4",
                                    "brandedFare": "PECAMP",
                                    "class": "T",
                                    "includedCheckedBags": {
                                        "quantity": 2
                                    }
                                }
                            ]
                        }
                    ]
                },
                {
                    "type": "flight-offer",
                    "id": "8",
                    "source": "GDS",
                    "instantTicketingRequired": false,
                    "paymentCardRequired": false,
                    "lastTicketingDate": "2022-05-25",
                    "itineraries": [
                        {
                            "segments": [
                                {
                                    "departure": {
                                        "iataCode": "BCN",
                                        "terminal": "1",
                                        "at": "2022-11-01T10:40:00"
                                    },
                                    "arrival": {
                                        "iataCode": "JFK",
                                        "at": "2022-11-01T14:35:00"
                                    },
                                    "carrierCode": "AY",
                                    "number": "4003",
                                    "aircraft": {
                                        "code": "772"
                                    },
                                    "operating": {
                                        "carrierCode": "AA"
                                    },
                                    "duration": "PT8H55M",
                                    "id": "1",
                                    "numberOfStops": 0,
                                    "blacklistedInEU": false
                                }
                            ]
                        },
                        {
                            "segments": [
                                {
                                    "departure": {
                                        "iataCode": "JFK",
                                        "terminal": "8",
                                        "at": "2022-11-30T19:10:00"
                                    },
                                    "arrival": {
                                        "iataCode": "BCN",
                                        "at": "2022-12-01T08:40:00"
                                    },
                                    "carrierCode": "AY",
                                    "number": "4004",
                                    "aircraft": {
                                        "code": "772"
                                    },
                                    "operating": {
                                        "carrierCode": "AA"
                                    },
                                    "duration": "PT7H30M",
                                    "id": "2",
                                    "numberOfStops": 0,
                                    "blacklistedInEU": false
                                }
                            ]
                        }
                    ],
                    "price": {
                        "currency": "EUR",
                        "total": "2529.12",
                        "base": "2265.00",
                        "fees": [
                            {
                                "amount": "0.00",
                                "type": "TICKETING"
                            }
                        ],
                        "grandTotal": "2529.12"
                    },
                    "pricingOptions": {
                        "fareType": [
                            "PUBLISHED"
                        ],
                        "includedCheckedBagsOnly": false,
                        "refundableFare": false,
                        "noRestrictionFare": false,
                        "noPenaltyFare": false
                    },
                    "validatingAirlineCodes": [
                        "AY"
                    ],
                    "travelerPricings": [
                        {
                            "travelerId": "1",
                            "fareOption": "STANDARD",
                            "travelerType": "ADULT",
                            "price": {
                                "currency": "EUR",
                                "total": "2529.12",
                                "base": "2265.00",
                                "taxes": [
                                    {
                                        "amount": "6.71",
                                        "code": "XY"
                                    },
                                    {
                                        "amount": "3.27",
                                        "code": "QV"
                                    },
                                    {
                                        "amount": "0.63",
                                        "code": "OG"
                                    },
                                    {
                                        "amount": "5.37",
                                        "code": "AY"
                                    },
                                    {
                                        "amount": "180.00",
                                        "code": "YR"
                                    },
                                    {
                                        "amount": "3.80",
                                        "code": "XA"
                                    },
                                    {
                                        "amount": "16.40",
                                        "code": "JD"
                                    },
                                    {
                                        "amount": "5.86",
                                        "code": "YC"
                                    },
                                    {
                                        "amount": "37.76",
                                        "code": "US"
                                    },
                                    {
                                        "amount": "4.32",
                                        "code": "XF"
                                    }
                                ]
                            },
                            "fareDetailsBySegment": [
                                {
                                    "segmentId": "1",
                                    "cabin": "PREMIUM_ECONOMY",
                                    "fareBasis": "TLX8C0S6",
                                    "brandedFare": "PECLASSIC",
                                    "class": "T",
                                    "includedCheckedBags": {
                                        "quantity": 2
                                    },
                                    "amenities": [
                                        {
                                            "code": "059",
                                            "description": "CHANGEABLE TICKET",
                                            "isChargeable": false,
                                            "amenityType": "BRANDED_FARES"
                                        },
                                        {
                                            "code": "09P",
                                            "description": "CABIN BAGGAGE",
                                            "isChargeable": false,
                                            "amenityType": "BAGGAGE"
                                        },
                                        {
                                            "code": "0GO",
                                            "description": "CHECKED BAGGAGE UP TO 23KGS",
                                            "isChargeable": false,
                                            "amenityType": "BAGGAGE"
                                        },
                                        {
                                            "code": "04J",
                                            "description": "PERSONAL ITEM",
                                            "isChargeable": false,
                                            "amenityType": "BAGGAGE"
                                        },
                                        {
                                            "code": "0B3",
                                            "description": "MEAL AND BEVERAGE",
                                            "isChargeable": false,
                                            "amenityType": "MEAL"
                                        },
                                        {
                                            "code": "06M",
                                            "description": "150PCT FINNAIR PLUS POINTS",
                                            "isChargeable": false,
                                            "amenityType": "BRANDED_FARES"
                                        },
                                        {
                                            "code": "0NI",
                                            "description": "POINT UPGRADE TO HIGHER CABIN",
                                            "isChargeable": false,
                                            "amenityType": "UPGRADES"
                                        },
                                        {
                                            "code": "04D",
                                            "description": "MONEY UPGRADE TO HIGHER CABIN",
                                            "isChargeable": false,
                                            "amenityType": "UPGRADES"
                                        },
                                        {
                                            "code": "050",
                                            "description": "STANDARD AND PREFERRED SEATS",
                                            "isChargeable": true,
                                            "amenityType": "BRANDED_FARES"
                                        },
                                        {
                                            "code": "04H",
                                            "description": "INTERNET ACCESS USB",
                                            "isChargeable": true,
                                            "amenityType": "ENTERTAINMENT"
                                        },
                                        {
                                            "code": "0BX",
                                            "description": "LOUNGE ACCESS",
                                            "isChargeable": true,
                                            "amenityType": "LOUNGE"
                                        }
                                    ]
                                },
                                {
                                    "segmentId": "2",
                                    "cabin": "PREMIUM_ECONOMY",
                                    "fareBasis": "TLX8C0S6",
                                    "brandedFare": "PECLASSIC",
                                    "class": "T",
                                    "includedCheckedBags": {
                                        "quantity": 2
                                    },
                                    "amenities": [
                                        {
                                            "code": "059",
                                            "description": "CHANGEABLE TICKET",
                                            "isChargeable": false,
                                            "amenityType": "BRANDED_FARES"
                                        },
                                        {
                                            "code": "09P",
                                            "description": "CABIN BAGGAGE",
                                            "isChargeable": false,
                                            "amenityType": "BAGGAGE"
                                        },
                                        {
                                            "code": "0GO",
                                            "description": "CHECKED BAGGAGE UP TO 23KGS",
                                            "isChargeable": false,
                                            "amenityType": "BAGGAGE"
                                        },
                                        {
                                            "code": "04J",
                                            "description": "PERSONAL ITEM",
                                            "isChargeable": false,
                                            "amenityType": "BAGGAGE"
                                        },
                                        {
                                            "code": "0B3",
                                            "description": "MEAL AND BEVERAGE",
                                            "isChargeable": false,
                                            "amenityType": "MEAL"
                                        },
                                        {
                                            "code": "06M",
                                            "description": "150PCT FINNAIR PLUS POINTS",
                                            "isChargeable": false,
                                            "amenityType": "BRANDED_FARES"
                                        },
                                        {
                                            "code": "0NI",
                                            "description": "POINT UPGRADE TO HIGHER CABIN",
                                            "isChargeable": false,
                                            "amenityType": "UPGRADES"
                                        },
                                        {
                                            "code": "04D",
                                            "description": "MONEY UPGRADE TO HIGHER CABIN",
                                            "isChargeable": false,
                                            "amenityType": "UPGRADES"
                                        },
                                        {
                                            "code": "050",
                                            "description": "STANDARD AND PREFERRED SEATS",
                                            "isChargeable": true,
                                            "amenityType": "BRANDED_FARES"
                                        },
                                        {
                                            "code": "04H",
                                            "description": "INTERNET ACCESS USB",
                                            "isChargeable": true,
                                            "amenityType": "ENTERTAINMENT"
                                        },
                                        {
                                            "code": "0BX",
                                            "description": "LOUNGE ACCESS",
                                            "isChargeable": true,
                                            "amenityType": "LOUNGE"
                                        }
                                    ]
                                }
                            ]
                        }
                    ]
                },
                {
                    "type": "flight-offer",
                    "id": "9",
                    "source": "GDS",
                    "instantTicketingRequired": false,
                    "paymentCardRequired": false,
                    "lastTicketingDate": "2022-06-19",
                    "itineraries": [
                        {
                            "segments": [
                                {
                                    "departure": {
                                        "iataCode": "BCN",
                                        "terminal": "1",
                                        "at": "2022-11-01T10:40:00"
                                    },
                                    "arrival": {
                                        "iataCode": "JFK",
                                        "at": "2022-11-01T14:35:00"
                                    },
                                    "carrierCode": "AY",
                                    "number": "4003",
                                    "aircraft": {
                                        "code": "772"
                                    },
                                    "operating": {
                                        "carrierCode": "AA"
                                    },
                                    "duration": "PT8H55M",
                                    "id": "1",
                                    "numberOfStops": 0,
                                    "blacklistedInEU": false
                                }
                            ]
                        },
                        {
                            "segments": [
                                {
                                    "departure": {
                                        "iataCode": "JFK",
                                        "terminal": "8",
                                        "at": "2022-11-30T19:10:00"
                                    },
                                    "arrival": {
                                        "iataCode": "BCN",
                                        "at": "2022-12-01T08:40:00"
                                    },
                                    "carrierCode": "AY",
                                    "number": "4004",
                                    "aircraft": {
                                        "code": "772"
                                    },
                                    "operating": {
                                        "carrierCode": "AA"
                                    },
                                    "duration": "PT7H30M",
                                    "id": "2",
                                    "numberOfStops": 0,
                                    "blacklistedInEU": false
                                }
                            ]
                        }
                    ],
                    "price": {
                        "currency": "EUR",
                        "total": "3029.12",
                        "base": "2765.00",
                        "fees": [
                            {
                                "amount": "0.00",
                                "type": "TICKETING"
                            }
                        ],
                        "grandTotal": "3029.12"
                    },
                    "pricingOptions": {
                        "fareType": [
                            "PUBLISHED"
                        ],
                        "includedCheckedBagsOnly": false,
                        "refundableFare": false,
                        "noRestrictionFare": false,
                        "noPenaltyFare": false
                    },
                    "validatingAirlineCodes": [
                        "AY"
                    ],
                    "travelerPricings": [
                        {
                            "travelerId": "1",
                            "fareOption": "STANDARD",
                            "travelerType": "ADULT",
                            "price": {
                                "currency": "EUR",
                                "total": "3029.12",
                                "base": "2765.00",
                                "taxes": [
                                    {
                                        "amount": "6.71",
                                        "code": "XY"
                                    },
                                    {
                                        "amount": "3.27",
                                        "code": "QV"
                                    },
                                    {
                                        "amount": "0.63",
                                        "code": "OG"
                                    },
                                    {
                                        "amount": "5.37",
                                        "code": "AY"
                                    },
                                    {
                                        "amount": "180.00",
                                        "code": "YR"
                                    },
                                    {
                                        "amount": "3.80",
                                        "code": "XA"
                                    },
                                    {
                                        "amount": "16.40",
                                        "code": "JD"
                                    },
                                    {
                                        "amount": "5.86",
                                        "code": "YC"
                                    },
                                    {
                                        "amount": "37.76",
                                        "code": "US"
                                    },
                                    {
                                        "amount": "4.32",
                                        "code": "XF"
                                    }
                                ]
                            },
                            "fareDetailsBySegment": [
                                {
                                    "segmentId": "1",
                                    "cabin": "ECONOMY",
                                    "fareBasis": "Y1N0C0S0",
                                    "brandedFare": "EFLEX",
                                    "class": "Y",
                                    "includedCheckedBags": {
                                        "quantity": 1
                                    },
                                    "amenities": [
                                        {
                                            "code": "059",
                                            "description": "CHANGEABLE TICKET",
                                            "isChargeable": false,
                                            "amenityType": "BRANDED_FARES"
                                        },
                                        {
                                            "code": "09P",
                                            "description": "CABIN BAGGAGE",
                                            "isChargeable": false,
                                            "amenityType": "BAGGAGE"
                                        },
                                        {
                                            "code": "0GO",
                                            "description": "CHECKED BAGGAGE UP TO 23KGS",
                                            "isChargeable": false,
                                            "amenityType": "BAGGAGE"
                                        },
                                        {
                                            "code": "04J",
                                            "description": "PERSONAL ITEM",
                                            "isChargeable": false,
                                            "amenityType": "BAGGAGE"
                                        },
                                        {
                                            "code": "0B3",
                                            "description": "MEAL AND BEVERAGE",
                                            "isChargeable": false,
                                            "amenityType": "MEAL"
                                        },
                                        {
                                            "code": "050",
                                            "description": "STANDARD AND PREFERRED SEATS",
                                            "isChargeable": false,
                                            "amenityType": "BRANDED_FARES"
                                        },
                                        {
                                            "code": "06M",
                                            "description": "150PCT FINNAIR PLUS POINTS",
                                            "isChargeable": false,
                                            "amenityType": "BRANDED_FARES"
                                        },
                                        {
                                            "code": "SPS",
                                            "description": "SPECIAL SEATS",
                                            "isChargeable": true,
                                            "amenityType": "BRANDED_FARES"
                                        },
                                        {
                                            "code": "0NI",
                                            "description": "POINT UPGRADE TO HIGHER CABIN",
                                            "isChargeable": true,
                                            "amenityType": "UPGRADES"
                                        },
                                        {
                                            "code": "04D",
                                            "description": "MONEY UPGRADE TO HIGHER CABIN",
                                            "isChargeable": true,
                                            "amenityType": "UPGRADES"
                                        },
                                        {
                                            "code": "04H",
                                            "description": "INTERNET ACCESS USB",
                                            "isChargeable": true,
                                            "amenityType": "ENTERTAINMENT"
                                        },
                                        {
                                            "code": "0BX",
                                            "description": "LOUNGE ACCESS",
                                            "isChargeable": true,
                                            "amenityType": "LOUNGE"
                                        }
                                    ]
                                },
                                {
                                    "segmentId": "2",
                                    "cabin": "ECONOMY",
                                    "fareBasis": "Y1N0C0S0",
                                    "brandedFare": "EFLEX",
                                    "class": "Y",
                                    "includedCheckedBags": {
                                        "quantity": 1
                                    },
                                    "amenities": [
                                        {
                                            "code": "059",
                                            "description": "CHANGEABLE TICKET",
                                            "isChargeable": false,
                                            "amenityType": "BRANDED_FARES"
                                        },
                                        {
                                            "code": "056",
                                            "description": "REFUNDABLE TICKET",
                                            "isChargeable": false,
                                            "amenityType": "BRANDED_FARES"
                                        },
                                        {
                                            "code": "09P",
                                            "description": "CABIN BAGGAGE",
                                            "isChargeable": false,
                                            "amenityType": "BAGGAGE"
                                        },
                                        {
                                            "code": "0GO",
                                            "description": "CHECKED BAGGAGE UP TO 23KGS",
                                            "isChargeable": false,
                                            "amenityType": "BAGGAGE"
                                        },
                                        {
                                            "code": "04J",
                                            "description": "PERSONAL ITEM",
                                            "isChargeable": false,
                                            "amenityType": "BAGGAGE"
                                        },
                                        {
                                            "code": "0B3",
                                            "description": "MEAL AND BEVERAGE",
                                            "isChargeable": false,
                                            "amenityType": "MEAL"
                                        },
                                        {
                                            "code": "050",
                                            "description": "STANDARD AND PREFERRED SEATS",
                                            "isChargeable": false,
                                            "amenityType": "BRANDED_FARES"
                                        },
                                        {
                                            "code": "06M",
                                            "description": "150PCT FINNAIR PLUS POINTS",
                                            "isChargeable": false,
                                            "amenityType": "BRANDED_FARES"
                                        },
                                        {
                                            "code": "SPS",
                                            "description": "SPECIAL SEATS",
                                            "isChargeable": true,
                                            "amenityType": "BRANDED_FARES"
                                        },
                                        {
                                            "code": "0NI",
                                            "description": "POINT UPGRADE TO HIGHER CABIN",
                                            "isChargeable": true,
                                            "amenityType": "UPGRADES"
                                        },
                                        {
                                            "code": "04D",
                                            "description": "MONEY UPGRADE TO HIGHER CABIN",
                                            "isChargeable": true,
                                            "amenityType": "UPGRADES"
                                        },
                                        {
                                            "code": "04H",
                                            "description": "INTERNET ACCESS USB",
                                            "isChargeable": true,
                                            "amenityType": "ENTERTAINMENT"
                                        },
                                        {
                                            "code": "0BX",
                                            "description": "LOUNGE ACCESS",
                                            "isChargeable": true,
                                            "amenityType": "LOUNGE"
                                        }
                                    ]
                                }
                            ]
                        }
                    ]
                },
                {
                    "type": "flight-offer",
                    "id": "10",
                    "source": "GDS",
                    "instantTicketingRequired": false,
                    "paymentCardRequired": false,
                    "lastTicketingDate": "2022-06-19",
                    "itineraries": [
                        {
                            "segments": [
                                {
                                    "departure": {
                                        "iataCode": "BCN",
                                        "terminal": "1",
                                        "at": "2022-11-01T10:40:00"
                                    },
                                    "arrival": {
                                        "iataCode": "JFK",
                                        "at": "2022-11-01T14:35:00"
                                    },
                                    "carrierCode": "AY",
                                    "number": "4003",
                                    "aircraft": {
                                        "code": "772"
                                    },
                                    "operating": {
                                        "carrierCode": "AA"
                                    },
                                    "duration": "PT8H55M",
                                    "id": "1",
                                    "numberOfStops": 0,
                                    "blacklistedInEU": false
                                }
                            ]
                        },
                        {
                            "segments": [
                                {
                                    "departure": {
                                        "iataCode": "JFK",
                                        "terminal": "8",
                                        "at": "2022-11-30T19:10:00"
                                    },
                                    "arrival": {
                                        "iataCode": "BCN",
                                        "at": "2022-12-01T08:40:00"
                                    },
                                    "carrierCode": "AY",
                                    "number": "4004",
                                    "aircraft": {
                                        "code": "772"
                                    },
                                    "operating": {
                                        "carrierCode": "AA"
                                    },
                                    "duration": "PT7H30M",
                                    "id": "2",
                                    "numberOfStops": 0,
                                    "blacklistedInEU": false
                                }
                            ]
                        }
                    ],
                    "price": {
                        "currency": "EUR",
                        "total": "4509.12",
                        "base": "4245.00",
                        "fees": [
                            {
                                "amount": "0.00",
                                "type": "TICKETING"
                            }
                        ],
                        "grandTotal": "4509.12"
                    },
                    "pricingOptions": {
                        "fareType": [
                            "PUBLISHED"
                        ],
                        "includedCheckedBagsOnly": false,
                        "refundableFare": false,
                        "noRestrictionFare": false,
                        "noPenaltyFare": false
                    },
                    "validatingAirlineCodes": [
                        "AY"
                    ],
                    "travelerPricings": [
                        {
                            "travelerId": "1",
                            "fareOption": "STANDARD",
                            "travelerType": "ADULT",
                            "price": {
                                "currency": "EUR",
                                "total": "4509.12",
                                "base": "4245.00",
                                "taxes": [
                                    {
                                        "amount": "6.71",
                                        "code": "XY"
                                    },
                                    {
                                        "amount": "3.27",
                                        "code": "QV"
                                    },
                                    {
                                        "amount": "0.63",
                                        "code": "OG"
                                    },
                                    {
                                        "amount": "5.37",
                                        "code": "AY"
                                    },
                                    {
                                        "amount": "180.00",
                                        "code": "YR"
                                    },
                                    {
                                        "amount": "3.80",
                                        "code": "XA"
                                    },
                                    {
                                        "amount": "16.40",
                                        "code": "JD"
                                    },
                                    {
                                        "amount": "5.86",
                                        "code": "YC"
                                    },
                                    {
                                        "amount": "37.76",
                                        "code": "US"
                                    },
                                    {
                                        "amount": "4.32",
                                        "code": "XF"
                                    }
                                ]
                            },
                            "fareDetailsBySegment": [
                                {
                                    "segmentId": "1",
                                    "cabin": "PREMIUM_ECONOMY",
                                    "fareBasis": "W1N0C0S0",
                                    "brandedFare": "PEFLEX",
                                    "class": "W",
                                    "includedCheckedBags": {
                                        "quantity": 2
                                    },
                                    "amenities": [
                                        {
                                            "code": "059",
                                            "description": "CHANGEABLE TICKET",
                                            "isChargeable": false,
                                            "amenityType": "BRANDED_FARES"
                                        },
                                        {
                                            "code": "09P",
                                            "description": "CABIN BAGGAGE",
                                            "isChargeable": false,
                                            "amenityType": "BAGGAGE"
                                        },
                                        {
                                            "code": "0GO",
                                            "description": "CHECKED BAGGAGE UP TO 23KGS",
                                            "isChargeable": false,
                                            "amenityType": "BAGGAGE"
                                        },
                                        {
                                            "code": "04J",
                                            "description": "PERSONAL ITEM",
                                            "isChargeable": false,
                                            "amenityType": "BAGGAGE"
                                        },
                                        {
                                            "code": "0B3",
                                            "description": "MEAL AND BEVERAGE",
                                            "isChargeable": false,
                                            "amenityType": "MEAL"
                                        },
                                        {
                                            "code": "050",
                                            "description": "STANDARD AND PREFERRED SEATS",
                                            "isChargeable": false,
                                            "amenityType": "BRANDED_FARES"
                                        },
                                        {
                                            "code": "06N",
                                            "description": "200PCT FINNAIR PLUS POINTS",
                                            "isChargeable": false,
                                            "amenityType": "BRANDED_FARES"
                                        },
                                        {
                                            "code": "0NI",
                                            "description": "POINT UPGRADE TO HIGHER CABIN",
                                            "isChargeable": false,
                                            "amenityType": "UPGRADES"
                                        },
                                        {
                                            "code": "04D",
                                            "description": "MONEY UPGRADE TO HIGHER CABIN",
                                            "isChargeable": false,
                                            "amenityType": "UPGRADES"
                                        },
                                        {
                                            "code": "04H",
                                            "description": "INTERNET ACCESS USB",
                                            "isChargeable": true,
                                            "amenityType": "ENTERTAINMENT"
                                        },
                                        {
                                            "code": "0BX",
                                            "description": "LOUNGE ACCESS",
                                            "isChargeable": true,
                                            "amenityType": "LOUNGE"
                                        }
                                    ]
                                },
                                {
                                    "segmentId": "2",
                                    "cabin": "PREMIUM_ECONOMY",
                                    "fareBasis": "W1N0C0S0",
                                    "brandedFare": "PEFLEX",
                                    "class": "W",
                                    "includedCheckedBags": {
                                        "quantity": 2
                                    },
                                    "amenities": [
                                        {
                                            "code": "059",
                                            "description": "CHANGEABLE TICKET",
                                            "isChargeable": false,
                                            "amenityType": "BRANDED_FARES"
                                        },
                                        {
                                            "code": "056",
                                            "description": "REFUNDABLE TICKET",
                                            "isChargeable": false,
                                            "amenityType": "BRANDED_FARES"
                                        },
                                        {
                                            "code": "09P",
                                            "description": "CABIN BAGGAGE",
                                            "isChargeable": false,
                                            "amenityType": "BAGGAGE"
                                        },
                                        {
                                            "code": "0GO",
                                            "description": "CHECKED BAGGAGE UP TO 23KGS",
                                            "isChargeable": false,
                                            "amenityType": "BAGGAGE"
                                        },
                                        {
                                            "code": "04J",
                                            "description": "PERSONAL ITEM",
                                            "isChargeable": false,
                                            "amenityType": "BAGGAGE"
                                        },
                                        {
                                            "code": "0B3",
                                            "description": "MEAL AND BEVERAGE",
                                            "isChargeable": false,
                                            "amenityType": "MEAL"
                                        },
                                        {
                                            "code": "050",
                                            "description": "STANDARD AND PREFERRED SEATS",
                                            "isChargeable": false,
                                            "amenityType": "BRANDED_FARES"
                                        },
                                        {
                                            "code": "06N",
                                            "description": "200PCT FINNAIR PLUS POINTS",
                                            "isChargeable": false,
                                            "amenityType": "BRANDED_FARES"
                                        },
                                        {
                                            "code": "0NI",
                                            "description": "POINT UPGRADE TO HIGHER CABIN",
                                            "isChargeable": false,
                                            "amenityType": "UPGRADES"
                                        },
                                        {
                                            "code": "04D",
                                            "description": "MONEY UPGRADE TO HIGHER CABIN",
                                            "isChargeable": false,
                                            "amenityType": "UPGRADES"
                                        },
                                        {
                                            "code": "04H",
                                            "description": "INTERNET ACCESS USB",
                                            "isChargeable": true,
                                            "amenityType": "ENTERTAINMENT"
                                        },
                                        {
                                            "code": "0BX",
                                            "description": "LOUNGE ACCESS",
                                            "isChargeable": true,
                                            "amenityType": "LOUNGE"
                                        }
                                    ]
                                }
                            ]
                        }
                    ]
                },
                {
                    "type": "flight-offer",
                    "id": "11",
                    "source": "GDS",
                    "instantTicketingRequired": false,
                    "paymentCardRequired": false,
                    "lastTicketingDate": "2022-06-19",
                    "itineraries": [
                        {
                            "segments": [
                                {
                                    "departure": {
                                        "iataCode": "BCN",
                                        "terminal": "1",
                                        "at": "2022-11-01T10:40:00"
                                    },
                                    "arrival": {
                                        "iataCode": "JFK",
                                        "at": "2022-11-01T14:35:00"
                                    },
                                    "carrierCode": "AY",
                                    "number": "4003",
                                    "aircraft": {
                                        "code": "772"
                                    },
                                    "operating": {
                                        "carrierCode": "AA"
                                    },
                                    "duration": "PT8H55M",
                                    "id": "1",
                                    "numberOfStops": 0,
                                    "blacklistedInEU": false
                                }
                            ]
                        },
                        {
                            "segments": [
                                {
                                    "departure": {
                                        "iataCode": "JFK",
                                        "terminal": "8",
                                        "at": "2022-11-30T19:10:00"
                                    },
                                    "arrival": {
                                        "iataCode": "BCN",
                                        "at": "2022-12-01T08:40:00"
                                    },
                                    "carrierCode": "AY",
                                    "number": "4004",
                                    "aircraft": {
                                        "code": "772"
                                    },
                                    "operating": {
                                        "carrierCode": "AA"
                                    },
                                    "duration": "PT7H30M",
                                    "id": "2",
                                    "numberOfStops": 0,
                                    "blacklistedInEU": false
                                }
                            ]
                        }
                    ],
                    "price": {
                        "currency": "EUR",
                        "total": "5767.12",
                        "base": "5183.00",
                        "fees": [
                            {
                                "amount": "0.00",
                                "type": "TICKETING"
                            }
                        ],
                        "grandTotal": "5767.12"
                    },
                    "pricingOptions": {
                        "fareType": [
                            "PUBLISHED"
                        ],
                        "includedCheckedBagsOnly": false,
                        "refundableFare": false,
                        "noRestrictionFare": false,
                        "noPenaltyFare": false
                    },
                    "validatingAirlineCodes": [
                        "AY"
                    ],
                    "travelerPricings": [
                        {
                            "travelerId": "1",
                            "fareOption": "STANDARD",
                            "travelerType": "ADULT",
                            "price": {
                                "currency": "EUR",
                                "total": "5767.12",
                                "base": "5183.00",
                                "taxes": [
                                    {
                                        "amount": "6.71",
                                        "code": "XY"
                                    },
                                    {
                                        "amount": "3.27",
                                        "code": "QV"
                                    },
                                    {
                                        "amount": "0.63",
                                        "code": "OG"
                                    },
                                    {
                                        "amount": "5.37",
                                        "code": "AY"
                                    },
                                    {
                                        "amount": "500.00",
                                        "code": "YR"
                                    },
                                    {
                                        "amount": "3.80",
                                        "code": "XA"
                                    },
                                    {
                                        "amount": "16.40",
                                        "code": "JD"
                                    },
                                    {
                                        "amount": "5.86",
                                        "code": "YC"
                                    },
                                    {
                                        "amount": "37.76",
                                        "code": "US"
                                    },
                                    {
                                        "amount": "4.32",
                                        "code": "XF"
                                    }
                                ]
                            },
                            "fareDetailsBySegment": [
                                {
                                    "segmentId": "1",
                                    "cabin": "BUSINESS",
                                    "fareBasis": "DNN0C0S0",
                                    "brandedFare": "BFLEX",
                                    "class": "D",
                                    "includedCheckedBags": {
                                        "quantity": 2
                                    },
                                    "amenities": [
                                        {
                                            "code": "059",
                                            "description": "CHANGEABLE TICKET",
                                            "isChargeable": false,
                                            "amenityType": "BRANDED_FARES"
                                        },
                                        {
                                            "code": "09P",
                                            "description": "CABIN BAGGAGE",
                                            "isChargeable": false,
                                            "amenityType": "BAGGAGE"
                                        },
                                        {
                                            "code": "0C6",
                                            "description": "CHECKED BAGGAGE UPTO 32KGS",
                                            "isChargeable": false,
                                            "amenityType": "BAGGAGE"
                                        },
                                        {
                                            "code": "04J",
                                            "description": "PERSONAL ITEM",
                                            "isChargeable": false,
                                            "amenityType": "BAGGAGE"
                                        },
                                        {
                                            "code": "0LF",
                                            "description": "PRIORITY BAGGAGE",
                                            "isChargeable": false,
                                            "amenityType": "TRAVEL_SERVICES"
                                        },
                                        {
                                            "code": "0B3",
                                            "description": "MEAL AND BEVERAGE",
                                            "isChargeable": false,
                                            "amenityType": "MEAL"
                                        },
                                        {
                                            "code": "050",
                                            "description": "STANDARD AND PREFERRED SEATS",
                                            "isChargeable": false,
                                            "amenityType": "BRANDED_FARES"
                                        },
                                        {
                                            "code": "06H",
                                            "description": "250PCT FINNAIR PLUS POINTS",
                                            "isChargeable": false,
                                            "amenityType": "BRANDED_FARES"
                                        },
                                        {
                                            "code": "0NI",
                                            "description": "POINT UPGRADE TO HIGHER CABIN",
                                            "isChargeable": false,
                                            "amenityType": "UPGRADES"
                                        },
                                        {
                                            "code": "04D",
                                            "description": "MONEY UPGRADE TO HIGHER CABIN",
                                            "isChargeable": false,
                                            "amenityType": "UPGRADES"
                                        },
                                        {
                                            "code": "04H",
                                            "description": "INTERNET ACCESS USB",
                                            "isChargeable": false,
                                            "amenityType": "ENTERTAINMENT"
                                        },
                                        {
                                            "code": "0BX",
                                            "description": "LOUNGE ACCESS",
                                            "isChargeable": false,
                                            "amenityType": "LOUNGE"
                                        },
                                        {
                                            "code": "PSB",
                                            "description": "PRIORITY SECURITY AND BOARDING",
                                            "isChargeable": false,
                                            "amenityType": "TRAVEL_SERVICES"
                                        },
                                        {
                                            "code": "03P",
                                            "description": "PRIORITY CHECK IN",
                                            "isChargeable": false,
                                            "amenityType": "TRAVEL_SERVICES"
                                        }
                                    ]
                                },
                                {
                                    "segmentId": "2",
                                    "cabin": "BUSINESS",
                                    "fareBasis": "DNN0C0S0",
                                    "brandedFare": "BFLEX",
                                    "class": "D",
                                    "includedCheckedBags": {
                                        "quantity": 2
                                    },
                                    "amenities": [
                                        {
                                            "code": "059",
                                            "description": "CHANGEABLE TICKET",
                                            "isChargeable": false,
                                            "amenityType": "BRANDED_FARES"
                                        },
                                        {
                                            "code": "056",
                                            "description": "REFUNDABLE TICKET",
                                            "isChargeable": false,
                                            "amenityType": "BRANDED_FARES"
                                        },
                                        {
                                            "code": "09P",
                                            "description": "CABIN BAGGAGE",
                                            "isChargeable": false,
                                            "amenityType": "BAGGAGE"
                                        },
                                        {
                                            "code": "0C6",
                                            "description": "CHECKED BAGGAGE UPTO 32KGS",
                                            "isChargeable": false,
                                            "amenityType": "BAGGAGE"
                                        },
                                        {
                                            "code": "04J",
                                            "description": "PERSONAL ITEM",
                                            "isChargeable": false,
                                            "amenityType": "BAGGAGE"
                                        },
                                        {
                                            "code": "0LF",
                                            "description": "PRIORITY BAGGAGE",
                                            "isChargeable": false,
                                            "amenityType": "TRAVEL_SERVICES"
                                        },
                                        {
                                            "code": "0B3",
                                            "description": "MEAL AND BEVERAGE",
                                            "isChargeable": false,
                                            "amenityType": "MEAL"
                                        },
                                        {
                                            "code": "050",
                                            "description": "STANDARD AND PREFERRED SEATS",
                                            "isChargeable": false,
                                            "amenityType": "BRANDED_FARES"
                                        },
                                        {
                                            "code": "06H",
                                            "description": "250PCT FINNAIR PLUS POINTS",
                                            "isChargeable": false,
                                            "amenityType": "BRANDED_FARES"
                                        },
                                        {
                                            "code": "04H",
                                            "description": "INTERNET ACCESS USB",
                                            "isChargeable": false,
                                            "amenityType": "ENTERTAINMENT"
                                        },
                                        {
                                            "code": "0BX",
                                            "description": "LOUNGE ACCESS",
                                            "isChargeable": false,
                                            "amenityType": "LOUNGE"
                                        },
                                        {
                                            "code": "PSB",
                                            "description": "PRIORITY SECURITY AND BOARDING",
                                            "isChargeable": false,
                                            "amenityType": "TRAVEL_SERVICES"
                                        },
                                        {
                                            "code": "03P",
                                            "description": "PRIORITY CHECK IN",
                                            "isChargeable": false,
                                            "amenityType": "TRAVEL_SERVICES"
                                        }
                                    ]
                                }
                            ]
                        }
                    ]
                }
            ],
            "dictionaries": {
                "locations": {
                    "BCN": {
                        "cityCode": "BCN",
                        "countryCode": "ES"
                    },
                    "JFK": {
                        "cityCode": "NYC",
                        "countryCode": "US"
                    }
                }
            }
        }
        ```
        

The response to our request is similar to the result of the flight search offers. In this case, it lists 10 branded fares, the second of which includes checked baggage, a meal and mileage accrual for 427,12€.

**—If you followed the steps you now have obtained branded fare offers!**

### Tips to understand the Branded Fare Upsell API response

- If the flight offers search provides you with the cheapest flights, branded fares are more expensive offers. The ‘id’ of the offer will reflect this: the numbering of the branded offers will start after the last offer of the flight offers.
- Notice that there are multiple flight offers for the same itinerary. If the request includes various offers, you can use the information in the `meta` section of the response to correlate to the flight offers provided in the request.