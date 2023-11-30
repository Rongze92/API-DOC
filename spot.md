# Spot

## Public

### Security: [None](general-info.md#endpoint-security-type)

Endpoints under **Public** section can be accessed freely without requiring any API-key or signatures.

{% swagger baseUrl="https://openapi.xxx.com" path="/sapi/v1/ping" method="get" summary=" Test Connectivity" %}
{% swagger-description %}
&#x20;This endpoint checks connectivity to the host

sdk:[https://github.com/exchange2021/openapidemo/blob/master/src/main/java/com/spot/TestConnectivity.java](https://github.com/exchange2021/openapidemo/blob/master/src/main/java/com/spot/TestConnectivity.java)
{% endswagger-description %}

{% swagger-response status="200" description=" Connection normal" %}
```
{}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://openapi.xxx.com" path="/sapi/v1/time" method="get" summary=" Check Server Time" %}
{% swagger-description %}
&#x20;This endpoint checks connectivity to the server and retrieves server timestamp

sdk:[https://github.com/exchange2021/openapidemo/blob/master/src/main/java/com/spot/CheckServerTime.java\
](https://github.com/exchange2021/openapidemo/blob/master/src/main/java/com/spot/CheckServerTime.java)
{% endswagger-description %}

{% swagger-response status="200" description=" Successfully retrieved server time" %}
```java
{
    "timezone": "GMT+08:00",
    "serverTime": 1595563624731
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://openapi.xxx.com" path="/sapi/v1/symbols" method="get" summary="Pairs List " %}
{% swagger-description %}
sdk:[https://github.com/exchange2021/openapidemo/blob/master/src/main/java/com/spot/PairsList.java](https://github.com/exchange2021/openapidemo/blob/master/src/main/java/com/spot/PairsList.java)
{% endswagger-description %}

{% swagger-response status="200" description="Successfully retrieved pairs list" %}
```java
{
    "symbols": [
        {
            "quantityPrecision": 3,
            "symbol": "sccadai",
            "pricePrecision": 6,
            "baseAsset": "SCCA",
            "quoteAsset": "DAI"
        },
        {
            "quantityPrecision": 8,
            "symbol": "btcusdt",
            "pricePrecision": 2,
            "baseAsset": "BTC",
            "quoteAsset": "USDT"
        },
        {
            "quantityPrecision": 3,
            "symbol": "bchusdt",
            "pricePrecision": 2,
            "baseAsset": "BCH",
            "quoteAsset": "USDT"
        },
        {
            "quantityPrecision": 2,
            "symbol": "etcusdt",
            "pricePrecision": 2,
            "baseAsset": "ETC",
            "quoteAsset": "USDT"
        },
        {
            "quantityPrecision": 2,
            "symbol": "ltcbtc",
            "pricePrecision": 6,
            "baseAsset": "LTC",
            "quoteAsset": "BTC"
        }
    ]
}
```
{% endswagger-response %}
{% endswagger %}

#### Response:

| name              | type    | example   | description                     |
| ----------------- | ------- | --------- | ------------------------------- |
| symbol            | string  | `BTCUSDT` | Name of the symbol              |
| baseAsset         | string  | `BTC`     | Underlying asset for the symbol |
| quoteAsset        | string  | `USDT`    | Quote asset for the symbol      |
| pricePrecision    | integer | `2`       | Precision of the price          |
| quantityPrecision | integer | `6`       | Precision of the quantity       |

## Market

### Security Type: [None](general-info.md#endpoint-security-type)

**Market** section can be accessed freely without requiring any API-key or signatures.

{% swagger baseUrl="https://openapi.xxx.com" path="/sapi/v1/depth" method="get" summary=" Depth" %}
{% swagger-description %}
&#x20;market detpth data

sdk:[https://github.com/exchange2021/openapidemo/blob/master/src/main/java/com/spot/Depth.java\
](https://github.com/exchange2021/openapidemo/blob/master/src/main/java/com/spot/Depth.java)
{% endswagger-description %}

{% swagger-parameter in="query" name="limit" type="integer" required="true" %}
&#x20;Default 100; Max 100
{% endswagger-parameter %}

{% swagger-parameter in="query" name="symbol" type="string" required="true" %}
&#x20;Symbol Name E.g. BTCUSDT
{% endswagger-parameter %}

{% swagger-response status="200" description=" Successfully retrieved market depth data" %}
```java
{
  "bids": [
    [
      "3.90000000",   // price
      "431.00000000"  // vol
    ],
    [
      "4.00000000",
      "431.00000000"
    ]
  ],
  "asks": [
    [
      "4.00000200",  // price
      "12.00000000"  // vol
    ],
    [
      "5.10000000",
      "28.00000000"
    ]
  ]
}
```
{% endswagger-response %}
{% endswagger %}

#### Response:

| name | type | example         | description                                                     |
| ---- | ---- | --------------- | --------------------------------------------------------------- |
| time | long | `1595563624731` | Current timestamp (ms)                                          |
| bids | list | ;               | List of all bids, best bids first. See below for entry details. |
| asks | list | ;               | List of all asks, best asks first. See below for entry details. |

The fields bids and asks are lists of order book price level entries, sorted from best to worst.

| name | type  | example | description                                       |
| ---- | ----- | ------- | ------------------------------------------------- |
| ' '  | float | `131.1` | price level                                       |
| ' '  | float | `2.3`   | The total quantity of orders for this price level |

{% swagger baseUrl="https://openapi.xxx.com" path="/sapi/v1/ticker" method="get" summary=" 24hrs ticker" %}
{% swagger-description %}
&#x20;24 hour price change statistics.

sdk:[https://github.com/exchange2021/openapidemo/blob/master/src/main/java/com/spot/Ticker.java](https://github.com/exchange2021/openapidemo/blob/master/src/main/java/com/spot/Ticker.java)
{% endswagger-description %}

{% swagger-parameter in="query" name="symbol" type="string" required="true" %}
Symbol Name. E.g. `BTCUSDT`
{% endswagger-parameter %}

{% swagger-response status="200" description=" Successfully retrieved ticker data" %}
```java
{
    "high": "9279.0301",
    "vol": "1302",
    "last": "9200",
    "low": "9279.0301",
    "rose": "0",
    "time": 1595563624731
}
```
{% endswagger-response %}
{% endswagger %}

#### Response:

| name | type  | example         | description  |
| ---- | ----- | --------------- | ------------ |
| time | long  | `1595563624731` | Open Time    |
| high | float | `9900`          | High Price   |
| low  | float | `8800.34`       | Low Price    |
| last | float | `8900`          | Last Price   |
| vol  | float | `4999`          | Trade Volume |

{% swagger baseUrl="https://openapi.xxx.com" path="/api/v1/trades" method="get" summary="Recent Trades List" %}
{% swagger-description %}
sdk:[https://github.com/exchange2021/openapidemo/blob/master/src/main/java/com/spot/RecentTradesList.java](https://github.com/exchange2021/openapidemo/blob/master/src/main/java/com/spot/RecentTradesList.java)
{% endswagger-description %}

{% swagger-parameter in="query" name="symbol" type="string" required="true" %}
&#x20;Symbol Name. E.g. `BTCUSDT`
{% endswagger-parameter %}

{% swagger-parameter in="query" name="limit" type="string" required="true" %}
&#x20;Default 100; Max 1000
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```java
[
  {
    "price": "3.00000100",
    "qty": "11.00000000",
    "time": 1499865549590,
    "side": "BUY"
  },...
]
```
{% endswagger-response %}
{% endswagger %}

#### **Response:**

| name    | type   | example         | description            |
| ------- | ------ | --------------- | ---------------------- |
| `price` | float  | `0.055`         | The price of the trade |
| `time`  | long   | `1537797044116` | Current timestamp (ms) |
| `qty`   | float  | `5`             | The quantity traded    |
| `side`  | string | `BUY/SELL`      | Taker side             |

{% swagger baseUrl="https://openapi.xxx.com" path="/sapi/v1/klines" method="get" summary="Kline/candlestick data" %}
{% swagger-description %}
sdk:[https://github.com/exchange2021/openapidemo/blob/master/src/main/java/com/spot/KlineCandlestickData.java](https://github.com/exchange2021/openapidemo/blob/master/src/main/java/com/spot/KlineCandlestickData.java)
{% endswagger-description %}

{% swagger-parameter in="query" name="symbol" type="string" required="true" %}
&#x20;Symbol Name. E.g. `BTCUSDT`
{% endswagger-parameter %}

{% swagger-parameter in="query" name="interval" type="string" required="true" %}
&#x20;Interval of the Kline. Possible values include: `1min`,`5min`,`15min`,`30min`,`60min`,`1day`,`1week`,`1month`
{% endswagger-parameter %}

{% swagger-parameter in="query" name="limit" type="integer" required="true" %}
&#x20;Default 100; Max 300
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```java
[
    {
        "high": "6228.77",
        "vol": "111",
        "low": "6228.77",
        "idx": 1594640340,
        "close": "6228.77",
        "open": "6228.77"
    },
    {
        "high": "6228.77",
        "vol": "222",
        "low": "6228.77",
        "idx": 1587632160,
        "close": "6228.77",
        "open": "6228.77"
    },
    {
        "high": "6228.77",
        "vol": "333",
        "low": "6228.77",
        "idx": 1587632100,
        "close": "6228.77",
        "open": "6228.77"
    }
]
```
{% endswagger-response %}
{% endswagger %}

#### **Response:**

| 名称      | 类型    | 例子              | 描述          |
| ------- | ----- | --------------- | ----------- |
| `idx`   | long  | `1538728740000` | Open time   |
| `open`  | float | `36.00000`      | open price  |
| `close` | float | `33.00000`      | close price |
| `high`  | float | `36.00000`      | high price  |
| `low`   | float | `30.00000`      | low price   |
| `vol`   | float | `2456.111`      | volume      |

## Trade

### Security Type: [TRADE](general-info.md#endpoint-security-type)

Endpoints under **Trade** require an [API-key and a signature.](general-info.md#signed-trade-yu-userdata-endpoint-security)

{% swagger baseUrl="https://openapi.xxx.com" path="/sapi/v1/order" method="post" summary=" New Order" %}
{% swagger-description %}
&#x20;**Rate Limit: 100times/2s**

**sdk:**[**https://github.com/exchange2021/openapidemo/blob/master/src/main/java/com/spot/NewOrder.java**](https://github.com/exchange2021/openapidemo/blob/master/src/main/java/com/spot/NewOrder.java)
{% endswagger-description %}

{% swagger-parameter in="header" name="X-CH-SIGN" type="string" required="true" %}
&#x20;Sign
{% endswagger-parameter %}

{% swagger-parameter in="header" name="X-CH-APIKEY" type="string" required="true" %}
&#x20;Your API-key
{% endswagger-parameter %}

{% swagger-parameter in="header" name="X-CH-TS" type="integer" required="true" %}
&#x20;timestamp
{% endswagger-parameter %}

{% swagger-parameter in="body" name="symbol" type="string" required="true" %}
&#x20;Symbol Name. E.g. `BTCUSDT`
{% endswagger-parameter %}

{% swagger-parameter in="body" name="volume" type="number" required="true" %}
&#x20;Order vol. For MARKET BUY orders,  vol=amount.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="side" type="string" required="true" %}
&#x20;Side of the order,`BUY/SELL`
{% endswagger-parameter %}

{% swagger-parameter in="body" name="type" type="string" required="true" %}
&#x20;Type of the order, `LIMIT/MARKET`
{% endswagger-parameter %}

{% swagger-parameter in="body" name="price" type="number" %}
&#x20;Order price, REQUIRED for LIMIT orders
{% endswagger-parameter %}

{% swagger-parameter in="body" name="newClientOrderId" type="string" %}
&#x20;Unique order ID generated by users to mark their orders
{% endswagger-parameter %}

{% swagger-parameter in="body" name="recvWindow" type="integer" %}
&#x20;Time window
{% endswagger-parameter %}

{% swagger-response status="200" description=" Successfully post new order" %}
```java
{
    'symbol': 'LXTUSDT', 
    'orderId': '150695552109032492', 
    'clientOrderId': '157371322565051',
    'transactTime': '1573713225668', 
    'price': '0.005452', 
    'origQty': '110', 
    'executedQty': '0', 
    'status': 'NEW',
    'type': 'LIMIT', 
    'side': 'SELL'
}
```
{% endswagger-response %}
{% endswagger %}

#### **Response:**

| name            | type    | example              | description                                                                                                     |
| --------------- | ------- | -------------------- | --------------------------------------------------------------------------------------------------------------- |
| `orderId`       | long    | `150695552109032492` | ID of the order                                                                                                 |
| `clientOrderId` | string  | `213443`             | A unique ID of the order.                                                                                       |
| `symbol`        | string  | `BTCUSDT`            | Symbol Name                                                                                                     |
| `transactTime`  | integer | `1273774892913`      | Time the order is placed                                                                                        |
| `price`         | float   | `4765.29`            | Price of the order                                                                                              |
| `origQty`       | float   | `1.01`               | Quantity ordered                                                                                                |
| `executedQty`   | float   | `1.01`               | Quantity of orders that has been executed                                                                       |
| `type`          | string  | `LIMIT`              | Order type `LIMIT,MARKET`                                                                                       |
| `side`          | string  | `BUY`                | Order side：`BUY, SELL`                                                                                          |
| `status`        | string  | `NEW`                | The state of the order.Possible values include `NEW`, `PARTIALLY_FILLED`, `FILLED`, `CANCELED`, and `REJECTED`. |

{% swagger baseUrl="https://openapi.xxx.com" path="/sapi/v1/order/test" method="post" summary=" Test New Order" %}
{% swagger-description %}
&#x20;Test new order creation and signature/recvWindow length. Creates and validates a new order but does not send the order into the matching engine.

sdk：[https://github.com/exchange2021/openapidemo/blob/master/src/main/java/com/spot/TestNewOrder.java\
](https://github.com/exchange2021/openapidemo/blob/master/src/main/java/com/spot/TestNewOrder.java)
{% endswagger-description %}

{% swagger-parameter in="header" name="X-CH-SIGN" type="string" required="true" %}
&#x20;Sign
{% endswagger-parameter %}

{% swagger-parameter in="header" name="X-CH-APIKEY" type="string" required="true" %}
&#x20;Your API-key
{% endswagger-parameter %}

{% swagger-parameter in="header" name="X-CH-TS" type="integer" required="true" %}
&#x20;timestamp
{% endswagger-parameter %}

{% swagger-parameter in="body" name="recvWindow" type="integer" %}
&#x20;Time window
{% endswagger-parameter %}

{% swagger-parameter in="body" name="symbol" type="string" required="true" %}
&#x20;Symbol Name. E.g. `BTCUSDT`
{% endswagger-parameter %}

{% swagger-parameter in="body" name="volume" type="number" required="true" %}
&#x20;Order vol. For MARKET BUY orders, vol=amount.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="side" type="string" required="true" %}
&#x20;Side of the order, `BUY/SELL`
{% endswagger-parameter %}

{% swagger-parameter in="body" name="type" type="string" required="true" %}
&#x20;Type of the order, `LIMIT/MARKET`
{% endswagger-parameter %}

{% swagger-parameter in="body" name="price" type="number" required="false" %}
&#x20;Order price, REQUIRED for `LIMIT` orders
{% endswagger-parameter %}

{% swagger-parameter in="body" name="newClientOrderId" type="string" %}
&#x20;Unique order ID generated by users to mark their orders
{% endswagger-parameter %}

{% swagger-response status="200" description=" Successfully test new order" %}
```
{}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://openapi.xxx.com" path="/sapi/v1/batchOrders" method="post" summary=" Batch Orders" %}
{% swagger-description %}
&#x20;**Rate Limit: 50times/2s A batch contains at most 10 orders**

sdk:[https://github.com/exchange2021/openapidemo/blob/master/src/main/java/com/spot/BatchOrders.java](https://github.com/exchange2021/openapidemo/blob/master/src/main/java/com/spot/BatchOrders.java)
{% endswagger-description %}

{% swagger-parameter in="header" name="X-CH-SIGN" type="string" required="true" %}
&#x20;Sign
{% endswagger-parameter %}

{% swagger-parameter in="header" name="X-CH-APIKEY" type="string" required="true" %}
&#x20;Your API-key
{% endswagger-parameter %}

{% swagger-parameter in="header" name="X-CH-TS" type="integer" required="true" %}
&#x20;timestamp
{% endswagger-parameter %}

{% swagger-parameter in="body" name="orders" type="array" required="true" %}
&#x20;Batch order param &#x20;
{% endswagger-parameter %}

{% swagger-parameter in="body" name="symbol" type="string" required="true" %}
&#x20;Symbol Name. E.g. `BTCUSDT`
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```java
{
    "ids": [
        165964665990709251,
        165964665990709252,
        165964665990709253
    ]
}
```
{% endswagger-response %}
{% endswagger %}

#### Resquest `orders` field:

| name        | type   | example        | description             |
| ----------- | ------ | -------------- | ----------------------- |
| `price`     | folat  | 1000           | Price of the order      |
| `volume`    | folat  | 20.1           | Vol of the order        |
| `side`      | string | `BUY/SELL`     | Side of the order       |
| `batchType` | string | `LIMIT/MARKET` | Batch type of the order |

{% swagger baseUrl="https://openapi.xxx.com" path="/sapi/v1/order" method="get" summary=" Query Order" %}
{% swagger-description %}
&#x20;**Rate Limit: 20times/2s**

**sdk：**[**https://github.com/exchange2021/openapidemo/blob/master/src/main/java/com/spot/QueryOrder.java**](https://github.com/exchange2021/openapidemo/blob/master/src/main/java/com/spot/QueryOrder.java)
{% endswagger-description %}

{% swagger-parameter in="header" name="X-CH-SIGN" type="string" required="true" %}
&#x20;Sign
{% endswagger-parameter %}

{% swagger-parameter in="header" name="X-CH-APIKEY" type="string" required="true" %}
&#x20;Your API-key
{% endswagger-parameter %}

{% swagger-parameter in="header" name="X-CH-TS" type="integer" required="true" %}
&#x20;timestamp
{% endswagger-parameter %}

{% swagger-parameter in="query" name="orderId" type="string" required="true" %}
&#x20;Order ID
{% endswagger-parameter %}

{% swagger-parameter in="query" name="newClientOrderId" type="string" %}
&#x20;Client Order Id, Unique order ID generated by users to mark their orders. E.g. 354444heihieddada
{% endswagger-parameter %}

{% swagger-parameter in="query" name="symbol" type="string" required="true" %}
&#x20;Symbol Name. E.g. `BTCUSDT`
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```java
{
    'orderId': '499890200602846976', 
    'clientOrderId': '157432755564968', 
    'symbol': 'BHTUSDT', 
    'price': '0.01', 
    'origQty': '50', 
    'executedQty': '0', 
    'avgPrice': '0', 
    'status': 'NEW', 
    'type': 'LIMIT', 
    'side': 'BUY', 
    'transactTime': '1574327555669'
}
```
{% endswagger-response %}
{% endswagger %}

#### **Response:**

| name            | type   | example              | description                                                                                                     |
| --------------- | ------ | -------------------- | --------------------------------------------------------------------------------------------------------------- |
| `orderId`       | long   | `150695552109032492` | ID of the order                                                                                                 |
| `clientOrderId` | string | `213443`             | Unique ID of the order.                                                                                         |
| `symbol`        | string | `BTCUSDT`            | Name of the symbol                                                                                              |
| `price`         | float  | `4765.29`            | Price of the order                                                                                              |
| `origQty`       | float  | `1.01`               | Quantity ordered                                                                                                |
| `executedQty`   | float  | `1.01`               | Quantity of orders that has been executed                                                                       |
| `avgPrice`      | float  | `4754.24`            | Average price of filled orders.                                                                                 |
| `type`          | string | `LIMIT`              | The order type`LIMIT,MARKET`                                                                                    |
| `side`          | string | `BUY`                | The order side`BUY,SELL`                                                                                        |
| `status`        | string | `NEW`                | The state of the order.Possible values include `NEW`, `PARTIALLY_FILLED`, `FILLED`, `CANCELED`, and `REJECTED`. |

{% swagger baseUrl="https://openapi.xxx.com" path="/sapi/v1/cancel" method="post" summary=" Cancel Order" %}
{% swagger-description %}
&#x20;**Rate Limit: 100time/2s**

**sdk:**[**https://github.com/exchange2021/openapidemo/blob/master/src/main/java/com/spot/CancelOrder.java**](https://github.com/exchange2021/openapidemo/blob/master/src/main/java/com/spot/CancelOrder.java)
{% endswagger-description %}

{% swagger-parameter in="header" name="X-CH-SIGN" type="string" required="true" %}
&#x20;Sign
{% endswagger-parameter %}

{% swagger-parameter in="header" name="X-CH-APIKEY" type="string" required="true" %}
&#x20;Your API-key
{% endswagger-parameter %}

{% swagger-parameter in="header" name="X-CH-TS" type="integer" required="true" %}
&#x20;timestamp
{% endswagger-parameter %}

{% swagger-parameter in="body" name="orderId" type="string" required="true" %}
&#x20;Order ID
{% endswagger-parameter %}

{% swagger-parameter in="body" name="newClientOrderId" type="string" %}
&#x20;Client Order Id, Unique order ID generated by users to mark their orders. E.g. 354444heihieddada
{% endswagger-parameter %}

{% swagger-parameter in="body" name="symbol" type="string" required="true" %}
&#x20;Symbol Name. E.g. `BTCUSDT`&#x20;
{% endswagger-parameter %}

{% swagger-response status="200" description=" 撤销订单成功" %}
```java
{
    'symbol': 'BHTUSDT', 
    'clientOrderId': '0', 
    'orderId': '499890200602846976', 
    'status': 'CANCELED'
}

```
{% endswagger-response %}
{% endswagger %}

#### Response:

| name            | type   | example              | description                                                                                                     |
| --------------- | ------ | -------------------- | --------------------------------------------------------------------------------------------------------------- |
| `orderId`       | long   | `150695552109032492` | ID of the order                                                                                                 |
| `clientOrderId` | string | `213443`             | Unique ID of the order.                                                                                         |
| `symbol`        | string | `BHTUSDT`            | Name of the symbol                                                                                              |
| `status`        | string | `NEW`                | The state of the order.Possible values include `NEW`, `PARTIALLY_FILLED`, `FILLED`, `CANCELED`, and `REJECTED`. |

{% swagger baseUrl="https://openapi.xxx.com" path="/sapi/v1/batchCancel" method="post" summary=" Batch cancel orders" %}
{% swagger-description %}
&#x20;**Rate Limit: 50times/2s A batch contains at most 10 orders**

**sdk:**[**https://github.com/exchange2021/openapidemo/blob/master/src/main/java/com/spot/BatchCancelOrders.java**](https://github.com/exchange2021/openapidemo/blob/master/src/main/java/com/spot/BatchCancelOrders.java)
{% endswagger-description %}

{% swagger-parameter in="header" name="X-CH-SIGN" type="string" required="true" %}
&#x20;Sign
{% endswagger-parameter %}

{% swagger-parameter in="header" name="X-CH-APIKEY" type="string" required="true" %}
&#x20;Your API-key
{% endswagger-parameter %}

{% swagger-parameter in="header" name="X-CH-TS" type="integer" required="true" %}
&#x20;timestamp
{% endswagger-parameter %}

{% swagger-parameter in="body" name="symbol" type="string" required="true" %}
&#x20;Symbol Name. E.g. `BTCUSDT`
{% endswagger-parameter %}

{% swagger-parameter in="body" name="orderIds" type="array" required="true" %}
&#x20;Order ID collection `[123,456]`
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```java
{
    "success": [
        165964665990709251,
        165964665990709252,
        165964665990709253
    ],
    "failed": [ //cancel fails because the order does not exist or the order state has expired
        165964665990709250  
    ]
}
```
{% endswagger-response %}
{% endswagger %}

{% swagger baseUrl="https://openapi.xxx.com" path="/sapi/v1/openOrders" method="get" summary=" Current Open Orders" %}
{% swagger-description %}
**Rate Limit: 20times/2s**

**sdk:**[**https://github.com/exchange2021/openapidemo/blob/master/src/main/java/com/spot/CurrentOpenOrders.java**](https://github.com/exchange2021/openapidemo/blob/master/src/main/java/com/spot/CurrentOpenOrders.java)
{% endswagger-description %}

{% swagger-parameter in="header" name="X-CH-SIGN" type="string" required="true" %}
&#x20;Sign
{% endswagger-parameter %}

{% swagger-parameter in="header" name="X-CH-APIKEY" type="string" required="true" %}
&#x20;Your API-key
{% endswagger-parameter %}

{% swagger-parameter in="header" name="X-CH-TS" type="integer" required="true" %}
&#x20;timestamp
{% endswagger-parameter %}

{% swagger-parameter in="query" name="symbol" type="string" required="true" %}
&#x20;Symbol Name. E.g. `BTCUSDT`
{% endswagger-parameter %}

{% swagger-parameter in="query" name="limit" type="integer" required="true" %}
&#x20;Default 100; Max 1000
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```java
[
    {
        'orderId': '499902955766523648', 
        'symbol': 'BHTUSDT', 
        'price': '0.01', 
        'origQty': '50', 
        'executedQty': '0', 
        'avgPrice': '0', 
        'status': 'NEW', 
        'type': 'LIMIT', 
        'side': 'BUY', 
        'time': '1574329076202'
        },...
]
```
{% endswagger-response %}
{% endswagger %}

#### **Response:**

| name            | type   | example              | description                                                                                                     |
| --------------- | ------ | -------------------- | --------------------------------------------------------------------------------------------------------------- |
| `orderId`       | long   | `150695552109032492` | ID of the order                                                                                                 |
| `clientOrderId` | string | `213443`             | Unique ID of the order.                                                                                         |
| `symbol`        | string | `BTCUSDT`            | Name of the symbol                                                                                              |
| `price`         | float  | `4765.29`            | Price of the order                                                                                              |
| `origQty`       | float  | `1.01`               | Quantity ordered                                                                                                |
| `executedQty`   | float  | `1.01`               | Quantity of orders that has been executed                                                                       |
| `avgPrice`      | float  | `4754.24`            | Average price of filled orders.                                                                                 |
| `type`          | string | `LIMIT`              | The order type`LIMIT,MARKET`                                                                                    |
| `side`          | string | `BUY`                | The order side `BUY,SELL`                                                                                       |
| `status`        | string | `NEW`                | The state of the order.Possible values include `NEW`, `PARTIALLY_FILLED`, `FILLED`, `CANCELED`, and `REJECTED`. |

{% swagger baseUrl="https://openapi.xxx.com" path="/sapi/v1/myTrades" method="get" summary=" Trades" %}
{% swagger-description %}
&#x20;**Rate Limt: 20times/2s**

**sdk:**[**https://github.com/exchange2021/openapidemo/blob/master/src/main/java/com/spot/Trades.java**](https://github.com/exchange2021/openapidemo/blob/master/src/main/java/com/spot/Trades.java)
{% endswagger-description %}

{% swagger-parameter in="header" name="X-CH-SIGN" type="string" required="true" %}
&#x20;Sign
{% endswagger-parameter %}

{% swagger-parameter in="header" name="X-CH-APIKEY" type="string" required="true" %}
&#x20;Your API-key
{% endswagger-parameter %}

{% swagger-parameter in="header" name="X-CH-TS" type="integer" required="true" %}
&#x20;timestamp
{% endswagger-parameter %}

{% swagger-parameter in="query" name="symbol" type="string" required="true" %}
&#x20;Symbol Name. E.g. `BTCUSDT`
{% endswagger-parameter %}

{% swagger-parameter in="query" name="limit" type="string" required="true" %}
&#x20;Default 100; Max1000
{% endswagger-parameter %}

{% swagger-parameter in="query" name="fromId" type="integer" required="true" %}
&#x20;Trade Id to fetch from
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```java
[
  {
    "symbol": "ETHBTC",
    "id": 100211,
    "bidId": 150695552109032492,
    "askId": 150695552109032493,
    "price": "4.00000100",
    "qty": "12.00000000",
    "time": 1499865549590,
    "isBuyer": true,
    "isMaker": false,
    "feeCoin": "ETH",
    "fee":"0.001"
  },...
]
```
{% endswagger-response %}
{% endswagger %}

#### **Response:**

| name      | type    | example              | description                   |
| --------- | ------- | -------------------- | ----------------------------- |
| `symbol`  | string  | `ETHBTC`             | Symbol Name                   |
| `id`      | integer | `28457`              | Trade ID                      |
| `bidId`   | long    | `150695552109032492` | Bid Order ID                  |
| `askId`   | long    | `150695552109032493` | Ask Order ID                  |
| `price`   | integer | `4.01`               | Price of the trade            |
| `qty`     | float   | `12`                 | Quantiry of the trade         |
| `time`    | number  | `1499865549590`      | timestamp of the trade        |
| `isBuyer` | bool    | `true`               | `true`= Buyer `false`= Seller |
| `isMaker` | bool    | `false`              | `true`=Maker `false`=Taker    |
| `feeCoin` | string  | `ETH`                | Trading fee coin              |
| `fee`     | number  | `0.001`              | Trading fee                   |

## Account

### Security Type:[ USER\_DATA](general-info.md#endpoint-security-type)

Endpoints under Account require an [API-key and a signature.](general-info.md#signed-trade-yu-userdata-endpoint-security)

{% swagger baseUrl="https://openapi.xxx.com" path="/sapi/v1/account" method="get" summary=" Account Information" %}
{% swagger-description %}
&#x20;**Rate Limit: 20times/2s**

**sdk:**[**https://github.com/exchange2021/openapidemo/blob/master/src/main/java/com/spot/AccountInformation.java**](https://github.com/exchange2021/openapidemo/blob/master/src/main/java/com/spot/AccountInformation.java)
{% endswagger-description %}

{% swagger-parameter in="header" name="X-CH-SIGN" type="string" required="true" %}
&#x20;Sign
{% endswagger-parameter %}

{% swagger-parameter in="header" name="X-CH-APIKEY" type="string" required="true" %}
&#x20;Your API-key
{% endswagger-parameter %}

{% swagger-parameter in="header" name="X-CH-TS" type="integer" required="true" %}
&#x20;timestamp
{% endswagger-parameter %}

{% swagger-response status="200" description=" Successfully retrieved account information." %}
```java
{
    'balances': 
        [
            {
                'asset': 'BTC', 
                'free': '0', 
                'locked': '0'
                }, 
            {
                'asset': 'ETH', 
                'free': '0', 
                'locked': '0'
                },...
        ]
}
```
{% endswagger-response %}
{% endswagger %}

#### Response:

| 名称         | 类型   | 描述                   |
| ---------- | ---- | -------------------- |
| `balances` | `[]` | Show balance details |

`balances` field:

| name     | type   | example | description                     |
| -------- | ------ | ------- | ------------------------------- |
| `asset`  | string | `USDT`  | Name of the asset               |
| `free`   | float  | 1000.30 | Amount available for use        |
| `locked` | float  | 400     | Amount locked (for open orders) |
