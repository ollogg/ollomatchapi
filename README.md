<h1 align="center">OLLO MATCH DATA API</h1>

This api based on GraphQL language

API documentation 
## 1. Authorization 
#### Authorization is based on an OAuth token that must be passed in the request headers (required for each request)

#### `"Authorization: OAuth TOKEN"`

## 2. Queries
### 2.1 getMatchById(params)
#### This request supports parameters such as
``` 
match_id: Number // Scalar type
```
#### Example request
```
getMatchById(match_id:3298697){
    teams{
      name
    }
  }
```
#### Example response (for valid request)
```
{
  "data": {
    "getMatchById": {
      "teams": [
        {
          "name": "StylDunow"
        },
        {
          "name": "GROND"
        }
      ]
    }
  }
}
```

### 2.2 getMatchByStatus(params)
#### This request supports parameters such as
``` 
status: String // enum type: live, upcoming, completed, deleted
offset: Number // Scalar type -- offset parameter relative to the beginning of the list
limit: Number  // Scalar type -- parameter for limiting the number of records in the output
sort: Number   // Scalar type -- according to the standard, all matches are sorted by the startTime field and we can only specify the sorting direction with integer values [1,-1]
```
#### In this request, only the status parameter is required, the other parameters and their order are not required.

#### Example request
```
getMatchByStatus(status:upcoming, offset: 0, sort:1,limit:2){
    teams{
      name
    }
  }
```
#### Example response (for valid request)
```
{
  "data": {
    "getMatchByStatus": [
      {
        "teams": [
          {
            "name": "100PG"
          },
          {
            "name": "MAD Lions"
          }
        ]
      },
      {
        "teams": [
          {
            "name": "Renewal"
          },
          {
            "name": "Wings Up"
          }
        ]
      }
    ]
  }
}
```
### 2.3 getMatchlist(params)
#### This request supports parameters such as
``` 
offset: Number // Scalar type -- offset parameter relative to the beginning of the list
limit: Number  // Scalar type -- parameter for limiting the number of records in the output
```
#### There are no required parameters in this request

#### Example request
```
getMatchlist( offset: 0, limit:2){
    teams{
      name
    }
}
```
#### Example response (for valid request)
```
{
  "data": {
    "getMatchlist": [
      {
        "teams": [
          {
            "name": "100PG"
          },
          {
            "name": "MAD Lions"
          }
        ]
      },
      {
        "teams": [
          {
            "name": "Renewal"
          },
          {
            "name": "Wings Up"
          }
        ]
      }
    ]
  }
}
```
## 3. Schema
#### The schema of your data source--that is, the entity types, values, and relationships that are available to query--are defined through the GraphQL Interface Definition Langauge (IDL).

### All available fields are displayed in this data schema:
```
type Country {
  name: String
}

type TeamPlayers {
  name: String
}

type Team {
  id: Number
  name: String
  logo: String
  players: [TeamPlayers]
  country: Country
}

type MatchScore {
  teamA: String
  teamB: String
}

type Map {
  isActive: Boolean
  name: String
  score: MatchScore
}

type Event {
  name: String
  logo: String
}

type Match {
  _id: ID!
  url: String
  match_id: Number
  data: String
  bestOf: Number
  parseUrl: String
  teams: [Team]
  status: MatchStatus
  tournament: String
  matchScore: MatchScore
  maps: [Map]
  liveScore: MatchScore
  startTime: String
  event: Event
  description: String
  id: Number
}
```
