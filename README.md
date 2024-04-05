# Scenario FTGO Kelompok 3

**Endpoint:**
* Penambahan Order : POST /order
* Perubahan Order: POST /order/{orderId}/revise
* Pembatalan Order: POST /order/{orderId}/cancel

| Feature      | Create Order |
| :----------- | :------------|
| **Requirements** | Membuat Order | 
| **Scenario**     | 1. Test adding an order with valid consumer and restaurant IDs. |
|              | 2. Test adding an order with invalid consumer ID (not existing in the database). |
|              | 3. Test adding an order with invalid restaurant ID (not existing in the database). |
|              | 4. Test adding an order with invalid items (not existing in the database). |

| Feature      | Create Order |
| :----------- | :------------|
| **Requirements** | Mengubah orderan yang sebelumnya telah di create. | 
| **Scenario**     | 1. Test revise an order with valid menu item ID. |
|              | 2. Test revise an order with invalid menu item ID (not existing in the database). |
|              | 3. Test revise an order with valid menu order ID. |
|              | 4. Test revise an order came up with grand total of order after update. |

| Feature      | Cancel Order |
| :----------- | :------------|
| **Requirements** | Membatalkan order yang sebelumnya sudah di create. | 
| **Scenario**     | 1. Test cancel an order with invalid consumer ID. |
|              | 2. Test cancel an order with valid consumer ID. |

## End-to-end tests
### End-to-end tests Create Order
#### Scenario-001: Test adding an order with valid consumer and restaurant IDs.
| Scenario      | Test adding an order with valid consumer and restaurant IDs. |
| :----------- | :------------|
| **Preconditions** | 1. The FTGO application is deployed and running. | 
|              | 2. All microservices (consumer service, restaurant service, order service, kitchen service, accounting service, order history service, and API gateway) are operational.|
|              | 3. Necessary data such as consumers and menu items are available in the system. |
|              | 4. The restaurant ID used in this scenario exists in the database. |
| **Step To Execute**     | 1. Open Swagger UI in localhost:8082/orders/index.html |
|              | 2. Look for the section where the request body JSON input in POST /orders section, then click Try it Out. |
|              | 3. Write the JSON in Test Data for creating an order. |
|              | 4. Once you've filled in the request body JSON, click on the "Execute" button to send the request to the server. |
| **Expected Result**| The consumer successfully places the order. The order details, including selected items, are correctly associated with the consumer and restaurant IDs. Upon submission, the order status transitions to "Pending" or "Received". |
| **Actual Result**| The actual result aligns with the expected result. The consumer successfully places the order. The order details, including selected items, are correctly associated with the consumer and restaurant IDs. |
|              | Response body:<br><pre lang="json">{&#13;  "orderId": 3&#13;}</pre> Response Headers:<br><pre lang="json">connection: keep-alive  content-type: application/json &#13;date: Fri05 Apr 2024 09:30:14 GMT keep-alive: timeout=60&#13;transfer-encoding: chunked  zipkin-trace-id: 78bca4589393d379</pre>|
| **Test Result**| PASS|
**Test Data**
```json
{
  "consumerId": 2,
  "deliveryAddress": {
    "city": "bandung",
    "state": "indonesia",
    "street1": "ciwaruga",
    "street2": "polban",
    "zip": "12345"
  },
  "deliveryTime": "2024-04-05T07:59:41.408Z",
  "lineItems": [
    {
      "menuItemId": "001",
      "quantity": "1"
    },
    {
      "menuItemId": "002",
      "quantity": "2"
    },
    {
      "menuItemId": "003",
      "quantity": "1"
    },
    {
      "menuItemId": "004",
      "quantity": "2"
    },
    {
      "menuItemId": "005",
      "quantity": "1"
    }
  ],
  "restaurantId": 3
}
``` 
#### Scenario-002: Test adding an order with invalid consumer ID (not existing in the database).
| Scenario      | Test adding an order with invalid items (not existing in the database). |
| :----------- | :------------|
| **Preconditions** | 1. The FTGO application is deployed and running. | 
|              | 2. All microservices (consumer service, restaurant service, order service, kitchen service, accounting service, order history service, and API gateway) are operational.|
|              | 3. Necessary data such as consumers and menu items are available in the system. |
|              | 4. The restaurant ID used in this scenario exists in the database. |
|              | 4. Once the request body JSON is filled, click on the "Execute" button to send the request to the server. |
| **Step To Execute**     | 1. Open Swagger UI in localhost:8082/orders/index.html |
|              | 2. Look for the section where the request body JSON input in POST /orders section, then click Try it Out. |
|              | 3. Write the JSON in Test Data for creating an order. |
|              | 4. Once you've filled in the request body JSON, click on the "Execute" button to send the request to the server. |
| **Expected Result**| |
| **Actual Result**| |
| **Test Result**| PASS|
**Test Data**
```json
{
  "consumerId": 100,
  "deliveryAddress": {
    "city": "bandung",
    "state": "indonesia",
    "street1": "ciwaruga",
    "street2": "polban",
    "zip": "12345"
  },
  "deliveryTime": "2024-04-05T07:59:41.408Z",
  "lineItems": [
    {
      "menuItemId": "001",
      "quantity": "1"
    },
    {
      "menuItemId": "002",
      "quantity": "2"
    },
    {
      "menuItemId": "003",
      "quantity": "1"
    },
    {
      "menuItemId": "004",
      "quantity": "2"
    },
    {
      "menuItemId": "005",
      "quantity": "1"
    }
  ],
  "restaurantId": 3
}
``` 

### End-to-end tests Revise Order
#### Scenario-005: Test revise an order with valid items.
| Scenario      | Test revise an order with valid menu item ID. |
| :----------- | :------------|
| **Preconditions** | 1. The FTGO application is deployed and running. | 
|              | 2. All microservices (consumer service, restaurant service, order service, kitchen service, accounting service, order history service, and API gateway) are operational.  |
|              | 3. Necessary data such as consumers and menu items are available in the system. |
|              | 4. The restaurant ID used in this scenario exists in the database. |
| **Step To Execute**     | 1. Open Swagger UI in localhost:8082/orders/index.html |
|              | 2. Navigate to the section where the request body JSON input in POST /revise  section, then click Try it Out. |
|              | 3. Write the JSON in Test Data for creating an order. |
|              | 4. Once the request body JSON is filled, click on the "Execute" button to send the request to the server. |
| **Expected Result**| The order will be updated and a message will be displayed that the update has been successful "APPROVED" and also displays the total order price after the update |
| **Actual Result**|  The expected result is the actual result displayed as follows The order will be updated and a message will be displayed that the update has been successful "APPROVED" and also displays the total order price after the update |
|              | Response body:<br><pre lang="json">{&#13;  "orderId": 2,&#13; &#13;  "state": "APPROVED",&#13; &#13;  "orderTotal": "73.43"&#13;} | 
| **Test Result**| PASS |
**Test Data**
```json
{
  "orderId": "2"
   "state": "APPROVED",
   "orderTotal": "73.43"
}
```

#### Scenario-006: Test revise an order with invalid menu item ID (not existing in the database). 
| Scenario      | Test revise an order with invalid menu item ID (not existing in the database). |
| :----------- | :------------|
| **Preconditions** | 1. The FTGO application is deployed and running. | 
|              | 2. All microservices (consumer service, restaurant service, order service, kitchen service, accounting service, order history service, and API gateway) are operational. |
|              | 3. Necessary data such as consumers and menu items are available in the system. |
|              | 4. The restaurant ID used in this scenario exists in the database. |
| **Step To Execute**     | 1. Open Swagger UI in localhost:8082/orders/index.html |
|              | 2. Navigate to the section where the request body JSON input in POST /revise  section, then click Try it Out. |
|              | 3. Write the JSON in Test Data for creating an order. |
|              | 4. Once the request body JSON is filled, click on the "Execute" button to send the request to the server. |
| **Expected Result**| By sending an ID that is not in the database, the system will display an error message. |
| **Actual Result**| the actual result is the expected result. The system will display an error message because it sent an ID that does not exist in the database. |
|              |  Error:<br><pre lang="json">connection: keep-alive  content-Length: 0  &#13;date: Fri05 Apr 2024 09:55:57 GMT keep-alive: timeout=60&#13;zipkin-trace-id: 6dab539f68650c17</pre> | 
| **Test Result**| PASS |
**Test Data**
```json
Input_id: "10"

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
#### Scenario-009: Test cancel an order with invalid Order ID.
| Scenario      | Test cancel an order with invalid Order ID. |
| :----------- | :------------|
| **Preconditions** | 1. The FTGO application is deployed and running. | 
|              | 2. All microservices (consumer service, restaurant service, order service, kitchen service, accounting service, order history service, and API gateway) are operational. |
|              | 3. Necessary data such as consumers and menu items are available in the system. |
|              | 4. The order ID used in this scenario exists in the database. |
| **Step To Execute**     | 1. Open Swagger UI in localhost:8082/orders/index.html |
|              | 2. Navigate to the section where the request order id input in POST /cancel section, then click Try it Out. |
|              | 3. Input the order id in the order id input box. |
|              | 4. Once the order id is filled, click on the "Execute" button to send the request to the server. |
| **Expected Result**| 1. Order cancellation should be failed, because the order id is not exist in the database so the API cannot cancel the order. |
|              | 2. The system should return an error response, indicating that order ID is invalid or not found in the database. |
| **Actual Result**| The actual result aligned with the expected result, Upon sending the request to cancel an order with an invalid order ID, the API responds with an error message indicating that the specified item is not found, so the system could not cancel any order id that was not stored in the database. Although there was no message that indicating the specified order ID that was not found. |
|              | Error:<br><pre lang="json">connection: keep-alive  content-type: application/json &#13;date: Fri05 Apr 2024 10:35:11 GMT keep-alive: timeout=60&#13;transfer-encoding: chunked  zipkin-trace-id: 6dab539f68650c17</pre>|
| **Test Result**| PASS |
**Test Data**
```json
{
“orderId”: “2003”
}
```

#### Scenario-010: Test cancel an order with valid Order ID.
| Scenario      | Test cancel an order with valid Order ID. |
| :----------- | :------------|
| **Preconditions** | 1. The FTGO application is deployed and running. | 
|              | 2. All microservices (consumer service, restaurant service, order service, kitchen service, accounting service, order history service, and API gateway) are operational. |
|              | 3. Necessary data such as consumers and menu items are available in the system. |
|              | 4. The order ID used in this scenario exists in the database. |
| **Step To Execute**     | 1. Open Swagger UI in localhost:8082/orders/index.html |
|              | 2. Navigate to the section where the request order id input in POST /cancel section, then click Try it Out. |
|              | 3. Input the order id in the order id input box. |
|              | 4. Once the order id is filled, click on the "Execute" button to send the request to the server. |
| **Expected Result**| 1. Order cancellation should be success, because the order id is  exist in the database so the API can cancel the order. |
|              | 2. The system shouldn’t return an error response, indicating that order ID is valid or found in the database |
| **Actual Result**| By entering  orderId correctly, the order data will be deleted and the system will display the message “APPROVAL_PENDING”. |
|              | Response body:<br><pre lang="json">{&#13;  "orderId": 7,&#13; &#13;  "state": "APPROVAL_PENDING",&#13; &#13;  "orderTotal": "73.43"&#13;}
| **Test Result**| PASS |
**Test Data**
```json
{
“orderId”: “7”
}
```
