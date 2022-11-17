<div align="center"><img src="./logo.svg" alt="Logo" width="80" height="80"></div>

<h1 align="center">Technical Challenge - Holiday Agency</h1>

# Brief
A holiday agency would like to suggest the lowest travel cost for holiday journeys to their customers.  
A return journey consists of the following parts:

1. Journey to the airport:
    * **Taxi**: £0.40/mile - (allows up to 4 people per taxi - e.g. require 2 taxis if 5 people travel together)
    * **Car**: £0.20/mile - (allows up to 4 people per car), additional £3 parking fee

2. An outbound and an inbound flight journey:
    * **Flight**: £0.10/passenger/mile

This flight agency keeps a table with its airports and their connections:

| Airport ID | Airport Name                                | Latitude  | Longitude | Connections and distance                                                                                           |
| ---------- | ------------------------------------------- | --------- | --------- | ------------------------------------------------------------------------------------------------------------------ |
| IST        | Istanbul Airport                            | 41.262222 | 28.727778 | ATH: 100mi<br/>AMS: 1200mi<br/>SVO: 800mi<br/>VIE: 750mi                                                           |
| CDG        | Charles de Gaulle Airport                   | 49.009722 | 2.547778  | ORY: 10mi<br/>LHR: 100mi<br/>AMS: 120mi<br/>FRA: 130mi<br/>ZRH: 120mi<br/>FCO: 500mi<br/>LIS: 750mi<br/>MAD: 600mi |
| LHR        | Heathrow Airport                            | 51.4775   | -0.461389 | LGW: 10mi<br/>CDG: 50mi<br/>AMS: 100mi<br/>FRA: 230mi<br/>MAD: 500mi<br/>LIS: 350mi                                |
| AMS        | Schiphol Airport                            | 52.308056 | 4.764167  | LHR: 100mi<br/>FRA: 90mi<br/>CDG: 110mi<br/>OSL: 500mi                                                             |
| SVO        | Sheremetyevo International Airport          | 55.972778 | 37.414722 | VKO: 10mi<br/>DME: 15mi<br/>LED: 200mi<br/>ATH: 1300mi                                                             |
| FRA        | Frankfurt Airport                           | 50.033333 | 8.570556  | VIE: 300mi<br/>MUC: 90mi<br/>ZRH: 100mi<br/>CDG: 105mi<br/>LHR: 120mi<br/>AMS: 100mi<br/>DME: 1500mi               |
| MAD        | Adolfo Suárez Madrid-Barajas Airport        | 40.472222 | -3.560833 | LIS: 145mi<br/>FCO: 220mi<br/>LHR: 500mi<br/>BCN: 120mi                                                            |
| DME        | Moscow Domodedovo Airport                   | 55.408611 | 37.906111 | ATH: 1105mi<br/>OSL: 980mi<br/>VKO: 15mi<br/>SVO: 20mi<br/>LED: 210mi<br/>ATH: 1000mi                              |
| BCN        | Josep Tarradellas Barcelona-El Prat Airport | 41.296944 | 2.078333  | MAD: 50mi<br/>FCO: 140mi                                                                                           |
| VKO        | Vnukovo International Airport               | 55.596111 | 37.2675   | SVO: 5mi<br/>DME: 8mi                                                                                              |
| MUC        | Munich Airport                              | 48.353889 | 11.786111 | VIE: 90mi<br/>ZRH: 80mi<br/>FRA: 100mi<br/>FCO: 200mi                                                              |
| LED        | Pulkovo Airport                             | 59.800278 | 30.2625   | VKO: 190mi<br/>SVO: 170mi<br/>OSL: 300mi<br/>LIS: 2500mi                                                           |
| ORY        | Orly Airport                                | 48.723333 | 2.379444  | CDG: 5mi<br/>AMS: 150mi                                                                                            |
| LGW        | Gatwick Airport                             | 51.148056 | -0.190278 | LHR: 10mi<br/>ORY: 125mi                                                                                           |
| FCO        | Leonardo da Vinci-Fiumicino Airport         | 41.800278 | 12.238889 | ATH: 200mi<br/>BCN: 190mi<br/>IST: 310mi<br/>AMS: 495mi                                                            |
| LIS        | Lisbon Airport                              | 38.774167 | -9.134167 | MAD: 100mi<br/>BCN: 300mi<br/>LHR: 300mi<br/>SVO: 2100mi                                                           |
| OSL        | Oslo Airport - Gardermoen                   | 60.202778 | 11.083889 | LED: 320mi<br/>LHR: 390mi<br/>FRA: 720mi<br/>AMS: 690mi<br/>VKO: 980mi                                             |
| ZRH        | Zurich Airport                              | 47.464722 | 8.549167  | FCO: 150mi<br/>MUC: 85mi<br/>VIE: 190mi<br/>FRA: 100mi<br/>CDG: 180mi<br/>AMS: 310mi                               |
| ATH        | Athens International Airport                | 37.936389 | 23.947222 | IST: 150mi<br/>FCO: 200mi<br/>MAD: 500mi                                                                           |
| VIE        | Vienna International Airport                | 48.110833 | 16.570833 | IST: 350mi<br/>VKO: 890mi<br/>OSL: 880mi<br/>MUC: 95mi<br/>FCO: 200mi                                              |

While the route `A->B` can exist, it doesn't necessarily mean that `B->A` exists. Additionally, the mileage may be different for each direction.

As a side-note, some of the mileages might not be at all accurate but imagine that someone make some fairly large one-way portals in the sky that can shorten the distance between two airports.

## Airport Data
Feel free to use any form of storage for the airport and route information.

You can make use of [`create-local-db.sh`](./create-local-db.sh) which sets up a local DynamoDB with the data in the table above.


## Your task:
Write a program that suggests the cheapest quote for their journeys.

This program should expose its logic via an API so that it can be consumed by other services or a browser client.

The API should expose, at least, the following endpoints:
* `GET`: `/vehicle/{numberOfPeople}/{distance}` - returns the cheapest vehicle to use (and the cost) for the given `numberOfPeople` and `distance` in miles
* `GET`: `/airports` - returns a list of airports
* `GET`: `/airports/{airportId}` - return details of a single airport
* `GET`: `/airports/{airportId}/to/{airportToId}` - returns the cheapest quote for a journey from `airportId` to `airportToId`

These endpoints should be public.

### Expectations
* A git repository with the solution
    * Application code
        * Use any programming language you like
    * API documentation - e.g. Swagger, Postman collection
    * Any tests
    * Any CI/CD configuration - e.g. github actions
    * Any infrastructure-like config - e.g. Dockerfile(s)
    * Any supporting scripts to generate, package, run, etc...
* A dockerhub image with the solution and instructions on how to run it (and/or a docker-compose file)
    * Optionally, feel free to host this for us somewhere as well.

# Getting help
If you have any questions, please feel free to reach out to me via email (tco@keyholding.com).

**This is a genuine offer for help** - I want to see you succeed! - and it lets me understand how you work and communicate.