# Margin

## Trade

### Security Type: [TRADE](general-info.md#endpoint-security-type)

Endpoints under **Trade** require an [API-key and a signature.​](general-info.md#signed-trade-yu-userdata-endpoint-security)

{% swagger baseUrl="https://openapi.xxx.com" path="/sapi/v1/margin/order" method="post" summary=" New Order" %}
{% swagger-description %}
&#x20;**Rate Limit：100times/2s**
{% endswagger-description %}

{% swagger-parameter in="header" name="X-CH-SIGN" type="string" %}
&#x20;Sign
{% endswagger-parameter %}

{% swagger-parameter in="header" name="X-CH-APIKEY" type="string" %}
&#x20;Your API-key
{% endswagger-parameter %}

{% swagger-parameter in="header" name="X-CH-TS" type="integer" %}
&#x20;timestamp
{% endswagger-parameter %}

{% swagger-parameter in="body" name="symbol" type="string" %}
&#x20;Symbol Name. E.g. `BTCUSDT`
{% endswagger-parameter %}

{% swagger-parameter in="body" name="volume" type="number" %}
&#x20;Order vol. For MARKET BUY orders, vol=amount.
{% endswagger-parameter %}

{% swagger-parameter in="body" name="side" type="string" %}
&#x20;Side of the order, `BUY/SELL`
{% endswagger-parameter %}

{% swagger-parameter in="body" name="type" type="string" %}
&#x20;Type of the order, `LIMIT/MARKET`
{% endswagger-parameter %}

{% swagger-parameter in="body" name="price" type="number" %}
&#x20;Order price, REQUIRED for LIMIT orders
{% endswagger-parameter %}

{% swagger-parameter in="body" name="newClientOrderId" type="string" %}
&#x20;Unique order ID generated by users to mark their orders
{% endswagger-parameter %}

{% swagger-parameter in="body" name="recvWindow" type="string" %}
&#x20;Time window
{% endswagger-parameter %}

{% swagger-response status="200" description=" 发送杠杆订单成功" %}
```java
{
    'symbol': 'LXTUSDT', 
    'orderId': '494736827050147840', 
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

{% swagger baseUrl="https://openapi.xxx.com" path="/sapi/v1/margin/order" method="get" summary=" Query Order" %}
{% swagger-description %}
&#x20;**Rate Limit: 20times/2s**
{% endswagger-description %}

{% swagger-parameter in="header" name="X-CH-SIGN" type="string" %}
&#x20;Sign
{% endswagger-parameter %}

{% swagger-parameter in="header" name="X-CH-APIKEY" type="string" %}
&#x20;Your API-key
{% endswagger-parameter %}

{% swagger-parameter in="header" name="X-CH-TS" type="integer" %}
&#x20;timestamp
{% endswagger-parameter %}

{% swagger-parameter in="query" name="orderId" type="string" %}
&#x20;Order ID
{% endswagger-parameter %}

{% swagger-parameter in="query" name="newClientOrderId" type="string" %}
&#x20;Client Order Id, Unique order ID generated by users to mark their orders. E.g. 354444heihieddada
{% endswagger-parameter %}

{% swagger-parameter in="query" name="symbol" type="string" %}
&#x20;Symbol Name.E.g. `BTCUSDT`
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

{% swagger baseUrl="https://openapi.xxx.com" path="/sapi/v1/margin/cancel" method="post" summary=" Cancel Order" %}
{% swagger-description %}
&#x20;**Rate Limit: 100times/2s**
{% endswagger-description %}

{% swagger-parameter in="header" name="X-CH-SIGN" type="string" %}
&#x20;Sign
{% endswagger-parameter %}

{% swagger-parameter in="header" name="X-CH-APIKEY" type="string" %}
&#x20;Your API-key
{% endswagger-parameter %}

{% swagger-parameter in="header" name="X-CH-TS" type="integer" %}
&#x20;timestamp
{% endswagger-parameter %}

{% swagger-parameter in="body" name="orderId" type="string" %}
&#x20;Order ID
{% endswagger-parameter %}

{% swagger-parameter in="body" name="newClientOrderId" type="string" %}
&#x20;Client Order Id, Unique order ID generated by users to mark their orders. E.g. 354444heihieddada
{% endswagger-parameter %}

{% swagger-parameter in="body" name="symbol" type="string" %}
&#x20;Symbol Name. E.g. `BTCUSDT`
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
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

{% swagger baseUrl="https://openapi.xxx.com" path="/sapi/v1/margin/openOrders" method="get" summary=" Current Open Orders" %}
{% swagger-description %}
&#x20;**Rate Limit: 20times/2s**
{% endswagger-description %}

{% swagger-parameter in="header" name="X-CH-SIGN" type="string" %}
&#x20;Sign
{% endswagger-parameter %}

{% swagger-parameter in="header" name="X-CH-APIKEY" type="string" %}
&#x20;Your API-key
{% endswagger-parameter %}

{% swagger-parameter in="header" name="X-CH-TS" type="integer" %}
&#x20;timestamp
{% endswagger-parameter %}

{% swagger-parameter in="query" name="symbol" type="string" %}
Symbol Name. E.g. `BTCUSDT`
{% endswagger-parameter %}

{% swagger-parameter in="query" name="limit" type="string" %}
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

{% swagger baseUrl="https://openapi.xxx.com" path="/sapi/v1/margin/myTrades" method="get" summary=" Trades" %}
{% swagger-description %}
&#x20;**Rate Limit: 20times/2s**
{% endswagger-description %}

{% swagger-parameter in="header" name="X-CH-SIGN" type="string" %}
&#x20;Sign
{% endswagger-parameter %}

{% swagger-parameter in="header" name="X-CH-APIKEY" type="string" %}
&#x20;Your API-key
{% endswagger-parameter %}

{% swagger-parameter in="header" name="X-CH-TS" type="integer" %}
&#x20;timestamp
{% endswagger-parameter %}

{% swagger-parameter in="query" name="symbol" type="string" %}
&#x20;Symbol Name.  E.g. `BTCUSDT`
{% endswagger-parameter %}

{% swagger-parameter in="query" name="limit" type="string" %}
&#x20;Default 100; Max 1000
{% endswagger-parameter %}

{% swagger-parameter in="query" name="fromId" type="integer" %}
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
