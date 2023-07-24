# StockAnalyzer
## Introduction
The **`StockAnalyzer`** is a web application that provides a service for analysing stock price movement. using these services we can monitor
the previously created graph and plan different strategies. Some of our services include ORB and combining multiple candles etc.

This is what a sample candle data looks like.
```
 {
   "LastTradeTime": "02-19-2021 09:15:00",
   "QuotationLot": "1",
   "TradedQty": "1251410",
   "OpenInterest": "0",
   "Open": "696",
   "High": "696",
   "Low": "682",
   "Close": "682.85"
 }
```
## Features
**1.**  Reading data from JSON file and mapping it to the specific object.<br>
**2.**  Getting Opening Range Breakout (ORB) for a given time interval.<br>
**3.**  Combining multiple candle data into a single unit and analysing it.<br>
## Installation & Getting started
To run the project locally, follow these steps:
1. Clone the repository to your local machine.
2. Ensure you have Java and Spring Framework installed.
3. Open the project in your preferred IDE.
4. Build the project to resolve dependencies.
5. Run the application using Maven:
```
mvn spring-boot:run
```
## Usage
## APIs Used
No external API's used in this application.
## Api Endpoints
- ### CustomerContoller:-
  #### **1. Register Customer**
   - **Endpoint:-** **`http://localhost:8085/customers`** (POST)
   - **Description:-** This is for registering for an application.
   - **Request:-**
     - `{
    "username":"raghu",
    "password":"1234"
        }`
   - **Response:-** Success: HTTP `202`
 ```
{
    "userId": 1,
    "username": "raghu",
    "password": "$2a$10$WVD8PeDLcK51oKLhpRrsVedbE.OWXCILdqKxTpwtKI2k90wEWF18u"
}
```
  #### **2. Login**
   - **Endpoint:-** **`http://localhost:8085/customers/signIn`** (GET)
   - **Description:-** This is authenticating user.
   - **Request:-** In headers you need to pass the `Authentication` object which contains `username`, `password`
   - **Response:-** Success HTTP `200`
```
## After success you will get JWT token
## NOTE:- This token we have to use for  accessing any web services.
{
    "username": "raghu",
    "password": "",
    "jwt": "eyJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJJbnZlc3RfQnVsbCIsInN1YiI6IkpXVCBUb2tlbiIsInVzZXJuYW1lIjoicmFnaHUiLCJyb2xlIjpbXSwiaWF0IjoxNjkwMTg1MTIzLCJleHAiOjE2OTAxOTIxMjN9.1b6V_7x5OLVM1RphTD-zjYMj5U8LdxgrYlY-BgTcBcI"
}
```
- ### StockController:-
  #### **3. Save Candles to DB**
   - **Endpoint:-** **`http://localhost:8085/stocks/save`** (POST)
   - **Description:-** This is for storing data from JSON file  to DB.
   - **Request:-** Here we have to pass the **`BearerToken`** with headers.
   - **Response:-** Success: HTTP `200`
```
[
    {
        "stockId": 1,
        "lastTradeTime": "2021-02-19T09:15:00",
        "quotationLot": 1,
        "tradedQty": 1251410,
        "openInterest": 0,
        "open": 696.0,
        "high": 696.0,
        "low": 682.0,
        "close": 682.85
    },
    {
        "stockId": 2,
        "lastTradeTime": "2021-02-19T09:20:00",
        "quotationLot": 1,
        "tradedQty": 933175,
        "openInterest": 0,
        "open": 681.65,
        "high": 682.8,
        "low": 678.4,
        "close": 679.75
    },
//more.
]
```
     
  #### **4. Finding ORB for stock**
   - **Endpoint:-** **`http://localhost:8085/stocks/orb/{minutes}`** (GET)
   - **Description:-** This is for getting the Opening Range Breakout (ORB) for a given period.
   - **Parameter** We have to pass the time interval as minutes, like (15,25,45)
   - **Request:-** **`http://localhost:8085/stoks/orb/15`**
   - **Response:-** Success: HTTP `200`
```
## This is Opening Range Breakout.
ORB candle generated at2021-02-19T13:30
```
     
  #### **5. Combining Candles**
   - **Endpoint:-** **`http://localhost:8085/stocks/combination/{minutes}`** (GET)
   - **Description:-** This is for  combining more than one candle of data into a single
   - **Parameter** We have to pass the time interval as minutes, like (15,25,45)
   - **Request:-** **`http://localhost:8085/stoks/combination/60`**
   - **Response:-** Success: HTTP `200`
```
[
    {
        "stockId": 0,
        "lastTradeTime": "2021-02-19T09:15:00",
        "quotationLot": 1,
        "tradedQty": 6189321,
        "openInterest": 0,
        "open": 696.0,
        "high": 696.0,
        "low": 675.0,
        "close": 682.6
    },
    {
        "stockId": 1,
        "lastTradeTime": "2021-02-19T10:15:00",
        "quotationLot": 1,
        "tradedQty": 2603201,
        "openInterest": 0,
        "open": 682.5,
        "high": 684.95,
        "low": 677.4,
        "close": 679.5
    },
//more.
]
```

## TechStack used
- SpringBoot
- Spring Data Japa
- Spring Security
- H2 Database
- JWT
