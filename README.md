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
#### Scenario-005: Test revise an order with valid items.
| Scenario      | Test revise an order with valid menu item ID. |
| :----------- | :------------|
| **Preconditions** | 1. The FTGO application is deployed and running.<br>2. All microservices (consumer service, restaurant service, order service, kitchen service, accounting service, order history service, and API gateway) are operational.<br>3. Necessary data such as consumers and menu items are available in the system.<br>4. The restaurant ID used in this scenario exists in the database. |
| **Step To Execute**     | 1. Open Swagger UI in localhost:8082/orders/index.html<br>2. Navigate to the section where the request body JSON input in POST /revise  section, then click Try it Out.<br>3. Write the JSON in Test Data for creating an order.<br>4. Once the request body JSON is filled, click on the "Execute" button to send the request to the server. |
| **Expected Result**| The order will be updated and a message will be displayed that the update has been successful "APPROVED" and also displays the total order price after the update |
| **Actual Result**|  The expected result is the actual result displayed as follows The order will be updated and a message will be displayed that the update has been successful "APPROVED" and also displays the total order price after the update |
|              | Response body:<br><pre lang="json">{&#13;"orderId": 2,&#13; &#13;"state": "APPROVED",&#13; &#13;"orderTotal": "73.43"&#13;} | 
| **Test Result**| PASS |
| **Test Data** | <pre lang="json">{&#13;  "orderId": "2",&#13;  "state": "APPROVED",&#13;  "orderTotal": "73.43"&#13;}</pre>|

#### Scenario-006: Test revise an order with invalid menu item ID (not existing in the database). 
| Scenario      | Test revise an order with invalid menu item ID (not existing in the database). |
| :----------- | :------------|
| **Preconditions** | 1. The FTGO application is deployed and running.<br>2. All microservices (consumer service, restaurant service, order service, kitchen service, accounting service, order history service, and API gateway) are operational.<br>3. Necessary data such as consumers and menu items are available in the system.<br>4. The restaurant ID used in this scenario exists in the database. |
| **Step To Execute**     | 1. Open Swagger UI in localhost:8082/orders/index.html<br>2. Navigate to the section where the request body JSON input in POST /revise  section, then click Try it Out.<br>3. Write the JSON in Test Data for creating an order.<br>4. Once the request body JSON is filled, click on the "Execute" button to send the request to the server. |
| **Expected Result**| By sending an ID that is not in the database, the system will display an error message. |
| **Actual Result**| the actual result is the expected result. The system will display an error message because it sent an ID that does not exist in the database. |
|              |  Error:<br><pre lang="json">connection: keep-alive  content-Length: 0  &#13;date: Fri05 Apr 2024 09:55:57 GMT keep-alive: timeout=60&#13;zipkin-trace-id: 6dab539f68650c17</pre> | 
| **Test Result**| PASS |
| **Test Data** | <pre lang="json">Input_id: 10&#13;&#13;{&#13;  "revisedOrderLineItems": [&#13; {&#13;  "menuItemId": "001",&#13;  "quantity": 5&#13;},&#13;{&#13;  "menuItemId": "002",&#13;  "quantity": 7&#13;}&#13;]&#13;}</pre>|

#### Scenario-007: Test revise an order with valid menu order ID
| Scenario      | Test revise an order with valid menu order ID |
| :----------- | :------------|
| **Preconditions** | 1. The FTGO application is deployed and running. | 
|              | 2. All microservices (consumer service, restaurant service, order service, kitchen service, accounting service, order history service, and API gateway) are operational. |
|              | 3. Necessary data such as consumers and menu items are available in the system. |
|              | 4. The restaurant ID used in this scenario exists in the database. |
| **Step To Execute**     | 1. Open Swagger UI in localhost:8082/orders/index.html |
|              | 2. Navigate to the section where the request body JSON input in POST /revise  section, then click Try it Out. |
|              | 3. Write the JSON in Test Data for creating an order. |
|              | 4. Once the request body JSON is filled, click on the "Execute" button to send the request to the server. |
| **Expected Result**| By entering a valid menu ID, the order will be updated, and then the system will display the message “APPROVED" and also display the total order price after the update |
| **Actual Result**| because you entered a valid menu ID, the expected result is the same as the actual result. The data was successfully updated and displayed the message and also display the total order price after the update |
|              | Response body:<br><pre lang="json">{&#13;"orderId": 2,&#13; &#13;"state": "APPROVED",&#13; &#13;"orderTotal": "73.43"&#13;} |
| **Test Result**| PASS |
| **Test Data** | <pre lang="json">Input_id: 2&#13;&#13;{&#13;  "revisedOrderLineItems": [&#13; {&#13;  "menuItemId": "001",&#13;  "quantity": 5&#13;},&#13;{&#13;  "menuItemId": "002",&#13;  "quantity": 7&#13;}&#13;]&#13;}</pre>|
```json
Input_id: 2

{
  "revisedOrderLineItems": [
    {
      "menuItemId": "001",
      "quantity": 5
    },
    {
      "menuItemId": "002",
      "quantity": 7
    }
  ]
}

```

#### Scenario-008: Test revise an order came up with grand total of order after update. 
| Scenario      | Test revise an order came up with grand total of order after update. |
| :----------- | :------------|
| **Preconditions** | 1. The FTGO application is deployed and running.<br>2. All microservices (consumer service, restaurant service, order service, kitchen service, accounting service, order history service, and API gateway) are operational.<br>3. Necessary data such as consumers and menu items are available in the system.<br>4. The restaurant ID used in this scenario exists in the database. |
| **Step To Execute**     | 1. Open Swagger UI in localhost:8082/orders/index.html<br>2. Navigate to the section where the request body JSON input in POST /revise  section, then click Try it Out.<br>3. Write the JSON in Test Data for creating an order.<br>4. Once the request body JSON is filled, click on the "Execute" button to send the request to the server. |
| **Expected Result**  | By entering the order ID, menu ID correctly, the order data will be updated and then the system will display the message "APPROVED" and also display the total order price after the update. |
| **Actual Result**  | by entering the order ID, menu ID correctly, the expected result and actual result will be the same so that the order data will be updated and then the system will display the message "APPROVED" and also display the total order price after the update. |
|              | Response body:<br><pre lang="json">{&#13;"orderId": 2,&#13; &#13;"state": "APPROVED",&#13; &#13;"orderTotal": "73.43"&#13;} |
| **Test Result**| PASS |
| **Test Data**| <pre lang="json">{&#13;  "orderId": "2",&#13; &#13;  "state": "APPROVED",&#13; &#13;  "orderTotal": "73.43",&#13;} |

### End-to-end tests Cancel Order
#### Scenario-009: Test cancel an order with invalid Order ID.
| Scenario      | Test cancel an order with invalid Order ID. |
| :----------- | :------------|
| **Preconditions** | 1. The FTGO application is deployed and running.<br>2. All microservices (consumer service, restaurant service, order service, kitchen service, accounting service, order history service, and API gateway) are operational.<br>3. Necessary data such as consumers and menu items are available in the system.<br>4. The order ID used in this scenario exists in the database. |
| **Step To Execute**     | 1. Open Swagger UI in localhost:8082/orders/index.html<br>2. Navigate to the section where the request order id input in POST /cancel section, then click Try it Out.<br>3. Input the order id in the order id input box.<br>4. Once the order id is filled, click on the "Execute" button to send the request to the server. |
| **Expected Result**| 1. Order cancellation should be failed, because the order id is not exist in the database so the API cannot cancel the order.<br>2. The system should return an error response, indicating that order ID is invalid or not found in the database. |
| **Actual Result**| The actual result aligned with the expected result, Upon sending the request to cancel an order with an invalid order ID, the API responds with an error message indicating that the specified item is not found, so the system could not cancel any order id that was not stored in the database. Although there was no message that indicating the specified order ID that was not found. |
|              | Error:<br><pre lang="json">connection: keep-alive  content-type: application/json &#13;date: Fri05 Apr 2024 10:35:11 GMT keep-alive: timeout=60&#13;transfer-encoding: chunked  zipkin-trace-id: 6dab539f68650c17</pre>|
| **Test Result**| PASS |
| **Test Data**| <pre lang="json">{&#13;  "orderId": "2003",&#13;} |

#### Scenario-010: Test cancel an order with valid Order ID.
| Scenario      | Test cancel an order with valid Order ID. |
| :----------- | :------------|
| **Preconditions** | 1. The FTGO application is deployed and running.<br>2. All microservices (consumer service, restaurant service, order service, kitchen service, accounting service, order history service, and API gateway) are operational.<br>3. Necessary data such as consumers and menu items are available in the system.<br>4. The order ID used in this scenario exists in the database. |
| **Step To Execute**     | 1. Open Swagger UI in localhost:8082/orders/index.html<br>2. Navigate to the section where the request order id input in POST /cancel section, then click Try it Out.<br>3. Input the order id in the order id input box.<br>4. Once the order id is filled, click on the "Execute" button to send the request to the server. |
| **Expected Result**| 1. Order cancellation should be success, because the order id is  exist in the database so the API can cancel the order.<br>2. The system shouldn’t return an error response, indicating that order ID is valid or found in the database |
| **Actual Result**| By entering  orderId correctly, the order data will be deleted and the system will display the message “APPROVAL_PENDING”. |
|              | Response body:<br><pre lang="json">{&#13;  "orderId": 7,&#13; &#13;  "state": "APPROVAL_PENDING",&#13; &#13;  "orderTotal": "73.43"&#13;} |
| **Test Result**| PASS |
| **Test Data**| <pre lang="json">{&#13;  "orderId": "7",&#13;} |
