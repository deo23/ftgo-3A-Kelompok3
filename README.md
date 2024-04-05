# Scenario FTGO Kelompok 3

**Endpoint:**
* Penambahan Order : POST /order
* Perubahan Order: POST /order/{orderId}/revise
* Pembatalan Order: POST /order/{orderId}/cancel

| Feature      | Create Order |
| :----------- | :------------|
| **Requirements** | Membuat Order | 
| **Scenario**     |<ol><li>Test adding an order with valid consumer and restaurant IDs.</li><li>Test adding an order with invalid consumer ID (not existing in the database).</li><li>Test adding an order with invalid restaurant ID (not existing in the database).</li><li>Test adding an order with invalid items (not existing in the database).</li></ol>|

| Feature      | Create Order |
| :----------- | :------------|
| **Requirements** | Mengubah orderan yang sebelumnya telah di create. | 
| **Scenario**     | <ol><li>Test adding an order with valid consumer and restaurant IDs.</li><li>Test adding an order with invalid consumer ID (not existing in the database).</li><li>Test adding an order with invalid restaurant ID (not existing in the database).</li><li>Test adding an order with invalid items (not existing in the database).</li><li>Test revise an order with valid quantit.</li><li>Test revise an order came up with grand total of order after update.</li></ol>|

| Feature      | Cancel Order |
| :----------- | :------------|
| **Requirements** | Membatalkan order yang sebelumnya sudah di create. | 
| **Scenario**     | <ol><li>Test cancel an order with invalid consumer ID.</li><li>Test cancel an order with valid consumer ID.</li></ol>|

## End-to-end tests
### End-to-end tests Create Order
#### Scenario-001: Test adding an order with valid consumer and restaurant IDs.
| Scenario      | Test adding an order with valid consumer and restaurant IDs. |
| :----------- | :------------|
| **Preconditions** | <ol><li>The FTGO application is deployed and running.</li><li>All microservices (consumer service, restaurant service, order service, kitchen service, accounting service, order history service, and API gateway) are operational.</li><li>Necessary data such as consumers and menu items are available in the system.</li><li>The restaurant ID used in this scenario exists in the database.</li></ol> |
| **Step To Execute**     | <ol><li>Open Swagger UI in localhost:8082/orders/index.html</li><li>Look for the section where the request body JSON input in POST /orders section, then click Try it Out.</li><li>Write the JSON in Test Data for creating an order.</li><li>Once you've filled in the request body JSON, click on the "Execute" button to send the request to the server.</li></ol>|
| **Expected Result**| The consumer successfully places the order. The order details, including selected items, are correctly associated with the consumer and restaurant IDs. Upon submission, the order status transitions to "Pending" or "Received". |
| **Actual Result**| The actual result aligns with the expected result. The consumer successfully places the order. The order details, including selected items, are correctly associated with the consumer and restaurant IDs. |
|              | Response body:<br><pre lang="json">{&#13;  "orderId": 3&#13;}</pre> Response Headers:<br><pre lang="json">connection: keep-alive  content-type: application/json &#13;date: Fri05 Apr 2024 09:30:14 GMT keep-alive: timeout=60&#13;transfer-encoding: chunked  zipkin-trace-id: 78bca4589393d379</pre>|
| **Test Result**| PASS|
| **Test Data** | <pre lang="json">{&#13;  "consumerId": 2,&#13;  "deliveryAddress": {&#13;    "city": "bandung",&#13;    "state": "indonesia",&#13;    "street1": "ciwaruga",&#13;    "street2": "polban",&#13;    "zip": "12345"&#13;  },&#13;  "deliveryTime": "2024-04-05T07:59:41.408Z",&#13;  "lineItems": [&#13;    {&#13;      "menuItemId": "001",&#13;      "quantity": "1"&#13;    },&#13;    {&#13;      "menuItemId": "002",&#13;      "quantity": "2"&#13;    },&#13;    {&#13;      "menuItemId": "003",&#13;      "quantity": "1"&#13;    },&#13;    {&#13;      "menuItemId": "004",&#13;      "quantity": "2"&#13;    },&#13;    {&#13;      "menuItemId": "005",&#13;      "quantity": "1"&#13;    }&#13;  ],&#13;  "restaurantId": 3&#13;}</pre>|

#### Scenario-002: Test adding an order with invalid consumer ID (not existing in the database).
| Scenario      | Test adding an order with invalid consumer ID (not existing in the database). |
| :----------- | :------------|
| **Preconditions** | <ol><li>The FTGO application is deployed and running.</li><li>All microservices (consumer service, restaurant service, order service, kitchen service, accounting service, order history service, and API gateway) are operational.</li><li>Write the JSON in Test Data for creating an order.</li><li>Once the request body JSON is filled, click on the "Execute" button to send the request to the server.</li></ol> |
| **Step To Execute**     | <ol><li>Open Swagger UI in localhost:8082/orders/index.html</li><li>Look for the section where the request body JSON input in POST /orders section, then click Try it Out.</li><li>Write the JSON in Test Data for creating an order.</li><li>Once you've filled in the request body JSON, click on the "Execute" button to send the request to the server.</li></ol> |
| **Expected Result**| The order creation process fails. The system returns an error response indicating that the consumer ID provided is invalid or not found. No order is created or persisted in the system. The API gateway properly handles the error response from the order service. |
| **Actual Result**| Actual results do not match expected results. The order creation process seemingly succeeds. The system does not return an error response despite the invalid consumer ID. An order is created and assigned a consumer ID, but the association is invalid as the consumer ID does not exist in the database. The system erroneously treats the invalid consumer ID as valid, leading to a potentially incorrect representation of the order. |
|               | Response body:<br><pre lang="json">{&#13;  "orderId": 3&#13;}</pre> Response Headers:<br><pre lang="json">connection: keep-alive  content-type: application/json &#13;date: Fri05 Apr 2024 09:45:32 GMT keep-alive: timeout=60&#13;transfer-encoding: chunked  zipkin-trace-id: 6c34b51d9aba602e</pre>|
| **Test Result**| FAIL |
| **Test Data** | <pre lang="json">{&#13;  "consumerId": 100,&#13;  "deliveryAddress": {&#13;    "city": "bandung",&#13;    "state": "indonesia",&#13;    "street1": "ciwaruga",&#13;    "street2": "polban",&#13;    "zip": "12345"&#13;  },&#13;  "deliveryTime": "2024-04-05T07:59:41.408Z",&#13;  "lineItems": [&#13;    {&#13;      "menuItemId": "001",&#13;      "quantity": "1"&#13;    },&#13;    {&#13;      "menuItemId": "002",&#13;      "quantity": "2"&#13;    },&#13;    {&#13;      "menuItemId": "003",&#13;      "quantity": "1"&#13;    },&#13;    {&#13;      "menuItemId": "004",&#13;      "quantity": "2"&#13;    },&#13;    {&#13;      "menuItemId": "005",&#13;      "quantity": "1"&#13;    }&#13;  ],&#13;  "restaurantId": 3&#13;}</pre>|

#### Scenario-003: Test adding an order with invalid restaurant ID (not existing in the database).
| Scenario      | Test adding an order with invalid restaurant ID (not existing in the database). |
| :----------- | :------------|
| **Preconditions** | <ol><li>The FTGO application is deployed and running.</li><li>All microservices (consumer service, restaurant service, order service, kitchen service, accounting service, order history service, and API gateway) are operational.</li><li>Necessary data such as consumers and menu items are available in the system.</li><li>Once the request body JSON is filled, click on the "Execute" button to send the request to the server.</li></ol> |
| **Step To Execute**     | <ol><li>Open Swagger UI in localhost:8082/orders/index.html</li><li>Look for the section where the request body JSON input in POST /orders section, then click Try it Out.</li><li>Write the JSON in Test Data for creating an order.</li><li>Once you've filled in the request body JSON, click on the "Execute" button to send the request to the server.</li></ol> |
| **Expected Result**| Upon sending the request to create an order with an invalid restaurant ID, the API should respond with an error message indicating that the specified restaurant is not found. |
| **Actual Result**| The actual result aligns with the expected result. Upon sending the request to create an order with an invalid restaurant ID, the API responds with an error message indicating that the specified restaurant is not found. The response includes the error message "Restaurant not found with id 999", accurately identifying the issue encountered.  |
|               | <pre lang="json">{&#13;  "timestamp": "2024-04-05T09:25:10.101+0000"&#13;  "status": 500,&#13;  "error": "Internal Server Error",&#13;  "message": "Restaurant not found with id 999",&#13;  "path": "/orders"&#13;}</pre> |
| **Test Result**| PASS |
| **Test Data** | <pre lang="json">{&#13;  "consumerId": 3,&#13;  "deliveryAddress": {&#13;    "city": "New York",&#13;    "state": "New Jersey",&#13;    "street1": "123 Main Street",&#13;    "street2": "Suite 101",&#13;    "zip": "12345"&#13;  },&#13;  "deliveryTime": "2024-04-05T08:40:20.096Z",&#13;  "lineItems": [&#13;    {&#13;      "menuItemId": "001",&#13;      "quantity": "1"&#13;    },&#13;    {&#13;      "menuItemId": "002",&#13;      "quantity": "2"&#13;    },&#13;     ],&#13;  "restaurantId": 999&#13;}</pre>|

#### Scenario-004: Test adding an order with invalid items (not existing in the database).
| Scenario      | Test adding an order with invalid items (not existing in the database). |
| :----------- | :------------|
| **Preconditions** | <ol><li>The FTGO application is deployed and running.</li><li>All microservices (consumer service, restaurant service, order service, kitchen service, accounting service, order history service, and API gateway) are operational.</li><li>Necessary data such as consumers and restaurants are available in the system.</li><li>Once the request body JSON is filled, click on the "Execute" button to send the request to the server.</li></ol> |
| **Step To Execute**     | <ol><li>Open Swagger UI in localhost:8082/orders/index.html</li><li>Look for the section where the request body JSON input in POST /orders section, then click Try it Out.</li><li>Write the JSON in Test Data for creating an order.</li><li>Once you've filled in the request body JSON, click on the "Execute" button to send the request to the server.</li></ol> |
| **Expected Result**| Upon sending the request to create an order with an invalid items ID, the API should respond with an error message indicating that the specified restaurant is not found. |
| **Actual Result**| The actual result aligns with the expected result. Upon sending the request to create an order with an invalid restaurant ID, the API responds with an error message indicating that the specified item is not found. The response includes the error message "Invalid menu item id 999", accurately identifying the issue encountered. |
|               | <pre lang="json">{&#13;  "timestamp": "2024-04-05T09:23:51.992+0000"&#13;  "status": 500,&#13;  "error": "Internal Server Error",&#13;  "message": "Invalid menu item id 999",&#13;  "path": "/orders"&#13;}</pre> |
| **Test Result**| PASS |
| **Test Data** | <pre lang="json">{&#13;  "consumerId": 3,&#13;  "deliveryAddress": {&#13;    "city": "New York",&#13;    "state": "New Jersey",&#13;    "street1": "123 Main Street",&#13;    "street2": "Suite 101",&#13;    "zip": "12345"&#13;  },&#13;  "deliveryTime": "2024-04-05T08:40:20.096Z",&#13;  "lineItems": [&#13;    {&#13;      "menuItemId": "001",&#13;      "quantity": "1"&#13;    },&#13;    {&#13;      "menuItemId": "999",&#13;      "quantity": "2"&#13;    },&#13;     ],&#13;  "restaurantId": 3&#13;}</pre>|

### End-to-end tests Revise Order
#### Scenario-001:
| Scenario      |  |
| :----------- | :------------|
| **Preconditions** |  | 
|              |  |
|              |  |
|              |  |
|              |  |
| **Step To Execute**     |  |
|              |  |
|              |  |
|              |  |
| **Expected Result**| |
| **Actual Result**| |
| **Test Result**|  |
**Test Data**
```json

```

#### Scenario-002:
| Scenario      |  |
| :----------- | :------------|
| **Preconditions** |  | 
|              |  |
|              |  |
|              |  |
|              |  |
| **Step To Execute**     |  |
|              |  |
|              |  |
|              |  |
| **Expected Result**| |
| **Actual Result**| |
| **Test Result**|  |
**Test Data**
```json

```

#### Scenario-003:
| Scenario      |  |
| :----------- | :------------|
| **Preconditions** |  | 
|              |  |
|              |  |
|              |  |
|              |  |
| **Step To Execute**     |  |
|              |  |
|              |  |
|              |  |
| **Expected Result**| |
| **Actual Result**| |
| **Test Result**|  |
**Test Data**
```json

```

### End-to-end tests Cancel Order
#### Scenario-001: Test cancel an order with invalid consumer ID.
| Scenario      | Test cancel an order with invalid consumer ID. |
| :----------- | :------------|
| **Preconditions** |  | 
|              |  |
|              |  |
|              |  |
|              |  |
| **Step To Execute**     |  |
|              |  |
|              |  |
|              |  |
| **Expected Result**| |
| **Actual Result**| |
| **Test Result**|  |
**Test Data**
```json

```

#### Scenario-002: Test cancel an order with valid consumer ID.
| Scenario      | Test cancel an order with valid consumer ID. |
| :----------- | :------------|
| **Preconditions** |  | 
|              |  |
|              |  |
|              |  |
|              |  |
| **Step To Execute**     |  |
|              |  |
|              |  |
|              |  |
| **Expected Result**| |
| **Actual Result**| |
| **Test Result**|  |
**Test Data**
```json

```
