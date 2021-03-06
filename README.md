VeracoreRESTInterface
===========
This project is a REST API built on Silex as a wrapper for Veracore's SOAP API. All methods require *application/json* as the request content type.

## Install
Clone the repo, install Composer, and then run 'php composer.phar install'. 

## Usage
To use this project, you'll have to set an "Authorization" header when making requests. The "Authorization" header should be the Veracore web services credentials (created in Veracore PMA) as a base64 encoded JSON object. Here is an example:

```php
    // Build credentials object
    $credentials = new \stdClass();
    $credentials->username = 'myTestUser';
    $credentials->password = 'myTestPass';
    
    // Encode
    $authorization = base64_encode(json_encode($credentials)); // eyJ1c2VybmFtZSI6Im15VGVzdFVzZXIiLCJwYXNzd29yZCI6Im15VGVzdFBhc3MifQ==
    
    // Example of setting headers with CURL
    curl_setopt($ch, CURLOPT_HTTPHEADER, array(
        'Content-Type: application/json',
        'Authorization: ' . $authorization
      )
    );
```

To test the requests using something like Postman, you'll need to set the Authorization header as the base64 encoded string like so:

![Postman auhorization example](https://i.imgur.com/JpbVNPW.png "Postman auhorization example")

## Methods
###AddOrder
Submits an order into Veracore. See the [AddOrder example JSON](https://github.com/dominickp/VeracoreREST/blob/master/example/AddOrder.json).

Route: ```POST /order```

###GetOrderInfo
Gets information related to a particular Veracore order.

Route: ```GET /order/{order_id}```

###GetOffer
Gets information related to a particular Veracore offer. Additional GET parameters are *id* and *name* which dictate if the *search_string* should be used to search for the Offer ID, Offer Name, or both. Booleans are expected and if both are left blank, it will default to both true. Is possible to return more than one result if the query is vague enough.

Route: ```GET /offer/{search_string}?id=true&name=false```

###GetOffers
Returns offer information for any offers within a category access group. You can further specify a search term but that is optional. It also has the same GET parameters from GetOffer.

Route: ```GET /offers/{category_access_group}/{search_string}?id=true&name=false```

Example: ```GET /offers/salesforce```

### License
VeracoreRESTInterface
Copyright (C) 2015 Shawmut Communications Group, Dominick G. Peluso

This program is free software; you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation; either version 2 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License along
with this program; if not, write to the Free Software Foundation, Inc.,
51 Franklin Street, Fifth Floor, Boston, MA 02110-1301 USA.
