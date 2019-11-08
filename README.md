# Junction Baggage API

### Table of Contents

- [Junction Baggage API](#junction-baggage-api)
    - [Table of Contents](#table-of-contents)
  - [Business case](#business-case)
  - [API Description](#api-description)
    - [Prerequisites](#prerequisites)
    - [Baggage](#baggage)
      - [Properties](#properties)
      - [baggageId](#baggageid)
      - [customerId](#customerid)
    - [Customers](#customers)
      - [Properties](#properties-1)
      - [customerId](#customerid-1)
    - [Events](#events)
      - [Properties](#properties-2)
      - [eventId](#eventid)
      - [baggageId](#baggageid-1)
  - [Support](#support)
  - [Known limitations](#known-limitations)

## Business case

Challenge description:
https://2019.hackjunction.com/challenges/smooth-travels

## API Description

The Bagage API consists of three APIs:

- Baggage
- Customers
- Events

The data presented here is generated test data.

### Prerequisites

### Baggage

A baggage is the single luggage or other cargo that the passenger takes with them on the flight.
Baggage information is returned by a GET call:

```
/dev/baggage
```

Without identifiers, the API return list of all baggage.

#### Properties

Parameters:

| Attribute  | Type   | Description                                               |
| :--------- | :----- | :-------------------------------------------------------- |
| baggageId  | String | Baggage ID, unique identifier                             |
| customerId | String | Baggage owners ID                                         |
| rushbag    | String | Y or N, Baggage needs to hurry to a connecting flight     |
| special    | String | Baggage type, one or multiple (e.g. ALH), see codes below |
| weight     | Number | Weight of the baggage                                     |

Special codes:

| Code | Name                  | Information                                                 |
| :--- | :-------------------- | :---------------------------------------------------------- |
| N    | Normal                | Standard luggage                                            |
| A    | Animal                | Live animal, requires heated cargo                          |
| L    | Long baggage          | Baggage that is longer than usual, e.g. ski bag             |
| H    | Heavy baggage         | Baggage that is heavier than 23 kg                          |
| C    | Special condition     | Baggage that requires specific temperature, e.g. medication |
| T    | Toxic chemicals       | Larger amount of possibly hazardous chemicals               |
| W    | Weapons or ammunition | Weapons or hunting gear, e.g. ammunition                    |

#### baggageId

```
/dev/baggage?baggageId=123-456-789
```

Get information of a baggage.

#### customerId

```
/dev/baggage?customerId=123-456-789
```

Get all baggage of customer

### Customers

Customer is the one passenger traveling on the flight.
The API has stored the relevant information of the passenger regarding baggage operations.

```
/dev/customers
```

Without parameters the API returns list of all customers.

#### Properties

Parameters:

| Attribute  | Type   | Description                                 |
| :--------- | :----- | :------------------------------------------ |
| customerId | String | Baggage owners ID, unique identifer         |
| name       | String | Full name of customer                       |
| email      | String | Email address of the customer               |
| phone      | String | Phone number of the customer                |
| target     | String | Destination airport, three-letter IATA code |

Airport codes follow standard IATA codes:
https://en.wikipedia.org/wiki/Category:Lists_of_airports_by_IATA_code

#### customerId

```
/dev/customers?customerId=123-456-789
```

Get information of a customer (passenger).

### Events

The baggage events contain all the checkpoints of the baggage from the check in to the destination baggage claim.

```
/dev/events
```

#### Properties

Parameters:

| Attribute    | Type   | Description                                                  |
| :----------- | :----- | :----------------------------------------------------------- |
| eventId      | String | Baggage events ID, unique identifer                          |
| baggageId    | String | Baggage ID                                                   |
| airport      | String | Airport of the event, three-letter IATA code                 |
| timestamp    | String | Timestamp of the event in UTC                                |
| type         | String | Event type, one per event, see codes below                   |
| flightNumber | String | Number of flight: operator prefix + route suffix, e.g. AY123 |

Airport codes follow standard IATA codes:
https://en.wikipedia.org/wiki/Category:Lists_of_airports_by_IATA_code

Event types:

| Type       | Description                                |
| :--------- | :----------------------------------------- |
| CHECKED_IN | Baggage registered at the check-in counter |
| LOADED     | Baggage loaded on to the aircraft          |
| UNLOADED   | Baggage loaded off the aircraft            |
| DAMAGED    | Baggage is found damaged                   |
| CLAIMED    | Baggage taken from baggage claim           |
| MISSING    | Baggage marked missing                     |

#### eventId

```
/dev/events?eventId=123-456-789
```

Get a specific event.

#### baggageId

```
/dev/events?baggageId=123-456-789
```

Get all events for a baggage.

## Support

Contact us on Discord for further information.

... Or visit us at QOCO Booth!

## Known limitations

A list of known limitations or issues. This might not be necessary as issues could be tracked using other issue tracking methods, but if there is something that should be mentioned in README already, it could be added here.
