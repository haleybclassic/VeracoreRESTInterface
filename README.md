VeracoreApi
===========
The plan is to develop a REST API built on Silex as a wrapper for Veracore's SOAP API. All methods require *application/json* as the request content type.

## Methods
###AddOrder
Submits an order into Veracore. See the [AddOrder example JSON](https://github.com/dominickp/VeracoreREST/blob/master/example/AddOrder.json).

Route: ```POST /order```

###GetOrderInfo
Gets information related to a particular Veracore order.

Route: ```GET /order/{order_id}```

###GetOffer
Gets information related to a particular Veracore offer. Additional GET parameters are *id* and *name* which dictate if the *search_string* should be used to search for the Offer ID, Offer Name, or both. Booleans are expected and if both are left blank, it will default to both true. Is possible to return more than one result if the query is vague enough.

Route: ```GET /offer/{search_tring}?id=true&name=false```
