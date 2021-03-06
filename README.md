# BitexBay-exchange-api-doc
BitexBay-exchange-api-doc
# BitexBay.com Official API Documentation

## Beta Warning
Please be kindly noticed that currently this version is in BETA and we may keep developing. Some changes would be expected in later versions.

**2018-07-25: 

## HTTP json API document


## Index
- [API End Point](#end-point)
    - [endpoint](#end-point)
- [Error Message](#error-message)
    - [error message](#error-message)
- [Public API](#public-api)
    - [markets](#markets)
    - [tickers](#tickers)
    - [tickers{market}](#tickersmarket)
    - [depth](#depth)
    - [trades](#trades)
    - [klines](#klines)
    - [allticker](#allticker)


**End Point**
----
The base API endpoint is `https://oapi.bitexbay.com`

apikey =md5(uid+email)+uid;

example:
uid : 11321
email : me@ofwho.com
        md5(11321me@ofwho.com)11321
apikey = 523030c0d5eb5b7321e8655b871beeed11321
&apikey=YourApiKeyToken  GET params

**Error Message**
----

If API request failed, the response will return HTTP status code, e.g. 500, 401, 404 etc., and detailed error message in JSON format.

```
  {
    "status": 0, // 1 for data is ok,0 is not ok
    "data": [], // array
    "msg": "", // error message
  }
```

**Public API**
----

### markets

* **URL**
  /v2/markets.php
  https://oapi.bitexbay.com/v2/markets.php?apikey=1a2bfb58b99c7e93f91ba5219bd96ef41

* **Description**
  Get all available markets.

* **Method:**
  `GET`
  
* **Success Response:**  
    * **Code:** 200
    * **Response Body:** 

    ```
    [
      {
        "currency_id": "29",         // Unique marked id.
        "currency_mark": "MOC",
        "currency_name": "MomoCash"       // market name
	"pairs_format_one":"MOC-BTC",
	"pairs_format_two":"MOC/BTC",
	"trade_currency_id":"30",       // Unique ticker id.
	"trade_currency_mark":"BTC",
      },
      {
        ...
      },
      ...
    ]
    ```
### depth

* **URL**
  /v2/depth.php
  https://oapi.bitexbay.com/v2/depth.php?apikey=1ba2bfb58b99c7e93f91ba5219bd96ef41&currency_id=29&currency_trade_id=30

* **Description**
  Get the depth information of specified market.

* **Method:**
  `GET`

* **Parameters**

* **Example Request:**
    * **Request:**
    `GET /v2/depth.php?market=moc-eth&limit=2`

    * **Success Response:**
        * **Code:** 200
        * **Content:**

        ```
        {
        }
        ```


### trades

* **URL**
  /v2/tickers.php
  https://oapi.bitexbay.com/v2/tickers.php?apikey=1ba2bfb58b99c7e93f91ba5219bd96ef41&tid=MOC-BTC
* **Description**
  Get recent trades on market, each trade is included only once. Trades are sorted in reverse creation order.


### timestamp

* **URL**
  /v2/timestamp.php
  https://oapi.bitexbay.com/v2/timestamp.php?apikey=1ba2bfb58b99c7e93f91ba5219bd96ef41

* **Description**
  Get server current time, in seconds since Unix epoch.

* **Method:**
  `GET`

* **Example Request:**
    * **Request:**
    `GET /v2/timestamp`
  
    * **Success Response:**  
        * **Code:** 200
        * **Content:** 

        ```
        1517740381
        ```

### klines

* **URL**
  /v2/klines.php
  https://oapi.bitexbay.com/v2/klines.php?apikey=1ba2bfb58b99c7e93f91ba5219bd96ef41&currency_id=29&currency_trade_id=30&ktime=kline_1h

* **Description**
  Get OHLC(k line) of specific market.

* **Method:**
  `GET`

* **Parameters**
ktim params include:   kline_5m  kline_15m  kline_30m  kline_8h  kline_1d

* **Example Request:**
    * **Request:**
    `GET /v2/klines.php?apikey=1ba2bfb58b99c7e93f91ba5219bd96ef41&currency_id=29&currency_trade_id=30
  
    * **Success Response:**  
        * **Code:** 200
        * **Content:** 

        ```
        [
          [
            "Jul 28 02:35:36", // An integer represents the seconds elapsed since Unix epoch.
            0.001159,   // K line open price
            0.001162,   // K line close price
            0.001157,   // K line lowest price
            0.001158,   //  K line highest price
	    1532716536
          ],
          [
            "Jul 28 02:35:36",
            0.001142,
            0.001160,
            0.001142,
            0.001159,
	    1532716536
          ]
        ]
        ```
### allticker

* **URL**
  /v2/allticker.php
  https://oapi.bitexbay.com/v2/allticker.php?apikey=1ba2bfb58b99c7e93f91ba5219bd96ef41

* **Description**
  Get all market and price.

* **Method:**
  `GET`

* **Parameters**


* **Example Request:**
    * **Request:**
    `GET /v2/allticker.php?apikey=1ba2bfb58b99c7e93f91ba5219bd96ef41
  
    * **Success Response:**  
        * **Code:** 200
        * **Content:** 

        ```
{ 
"date":"1410431279", 
"ticker":[{ 
"symbol":"ltc_usdt", 
"buy":"33.15", 
"high":"34.15", 
"last":"33.15", 
"low":"32.05", 
"sell":"33.16", 
"change":"4.5"
"vol":"10532696.39199642" 
},{ 
"symbol":"btc_usdt", 
"buy":"33.15", 
"high":"34.15", 
"last":"33.15", 
"low":"32.05", 
"sell":"33.16", 
"change":"-4.5"
"vol":"10532696.39199642" 
}] 
} 
return params
date: the server time 
symbol: pairs 
buy: buy price
high: the highest price 
last: the last price
low: the low price
sell: sell price 
vol: the volue of 24 hours
change: price change

返回值说明
date: 返回数据时服务器时间 
symbol: 交易对（交易对1简称_交易对2简称） 
buy: 买一价 
high: 最高价 
last: 最新成交价 
low: 最低价 
sell: 卖一价 
vol: 成交量(最近的24小时)
change:涨跌幅
        ```
