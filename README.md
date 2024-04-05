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
| **Scenario**     | <ol><li>Test adding an order with valid consumer and restaurant IDs.</li><li>Test adding an order with invalid consumer ID (not existing in the database).</li><li>Test adding an order with invalid restaurant ID (not existing in the database).</li><li>Test adding an order with invalid items (not existing in the database).</li><li>Test revise an order with valid quantit.<br>6. Test revise an order came up with grand total of order after update.</li></ol>|

| Feature      | Cancel Order |
| :----------- | :------------|
| **Requirements** | Membatalkan order yang sebelumnya sudah di create. | 
| **Scenario**     | 1. Test cancel an order with invalid consumer ID.<br>2. Test cancel an order with valid consumer ID. |

## End-to-end tests
### End-to-end tests Create Order
#### Scenario-001: Test adding an order with valid consumer and restaurant IDs.
| Scenario      | Test adding an order with valid consumer and restaurant IDs. |
| :----------- | :------------|
| **Preconditions** | 1. The FTGO application is deployed and running.<br>2. All microservices (consumer service, restaurant service, order service, kitchen service, accounting service, order history service, and API gateway) are operational.<br>3. Necessary data such as consumers and menu items are available in the system.<br>4. The restaurant ID used in this scenario exists in the database. |
| **Step To Execute**     | 1. Open Swagger UI in localhost:8082/orders/index.html<br>2. Look for the section where the request body JSON input in POST /orders section, then click Try it Out.<br>3. Write the JSON in Test Data for creating an order.<br>4. Once you've filled in the request body JSON, click on the "Execute" button to send the request to the server. |
| **Expected Result**| The consumer successfully places the order. The order details, including selected items, are correctly associated with the consumer and restaurant IDs. Upon submission, the order status transitions to "Pending" or "Received". |
| **Actual Result**| The actual result aligns with the expected result. The consumer successfully places the order. The order details, including selected items, are correctly associated with the consumer and restaurant IDs. |
|              | Response body:<br><pre lang="json">{&#13;  "orderId": 3&#13;}</pre> Response Headers:<br><pre lang="json">connection: keep-alive  content-type: application/json &#13;date: Fri05 Apr 2024 09:30:14 GMT keep-alive: timeout=60&#13;transfer-encoding: chunked  zipkin-trace-id: 78bca4589393d379</pre>|
| **Test Result**| PASS|
| **Test Data** | <pre lang="json">{&#13;  "consumerId": 2,&#13;  "deliveryAddress": {&#13;    "city": "bandung",&#13;    "state": "indonesia",&#13;    "street1": "ciwaruga",&#13;    "street2": "polban",&#13;    "zip": "12345"&#13;  },&#13;  "deliveryTime": "2024-04-05T07:59:41.408Z",&#13;  "lineItems": [&#13;    {&#13;      "menuItemId": "001",&#13;      "quantity": "1"&#13;    },&#13;    {&#13;      "menuItemId": "002",&#13;      "quantity": "2"&#13;    },&#13;    {&#13;      "menuItemId": "003",&#13;      "quantity": "1"&#13;    },&#13;    {&#13;      "menuItemId": "004",&#13;      "quantity": "2"&#13;    },&#13;    {&#13;      "menuItemId": "005",&#13;      "quantity": "1"&#13;    }&#13;  ],&#13;  "restaurantId": 3&#13;}</pre>|

#### Scenario-002: Test adding an order with invalid consumer ID (not existing in the database).
| Scenario      | Test adding an order with invalid consumer ID (not existing in the database). |
| :----------- | :------------|
| **Preconditions** | 1. The FTGO application is deployed and running.<br>2. All microservices (consumer service, restaurant service, order service, kitchen service, accounting service, order history service, and API gateway) are operational.<br>3. Write the JSON in Test Data for creating an order.<br>4. Once the request body JSON is filled, click on the "Execute" button to send the request to the server. |
| **Step To Execute**     | 1. Open Swagger UI in localhost:8082/orders/index.html<br>2. Look for the section where the request body JSON input in POST /orders section, then click Try it Out.<br>3. Write the JSON in Test Data for creating an order.<br>4. Once you've filled in the request body JSON, click on the "Execute" button to send the request to the server. |
| **Expected Result**| The order creation process fails. The system returns an error response indicating that the consumer ID provided is invalid or not found. No order is created or persisted in the system. The API gateway properly handles the error response from the order service. |
| **Actual Result**| Actual results do not match expected results. The order creation process seemingly succeeds. The system does not return an error response despite the invalid consumer ID. An order is created and assigned a consumer ID, but the association is invalid as the consumer ID does not exist in the database. The system erroneously treats the invalid consumer ID as valid, leading to a potentially incorrect representation of the order. |
|               | Response body:<br><pre lang="json">{&#13;  "orderId": 3&#13;}</pre> Response Headers:<br><pre lang="json">connection: keep-alive  content-type: application/json &#13;date: Fri05 Apr 2024 09:45:32 GMT keep-alive: timeout=60&#13;transfer-encoding: chunked  zipkin-trace-id: 6c34b51d9aba602e</pre>|
| **Test Result**| FAIL |
| **Test Data** | <pre lang="json">{&#13;  "consumerId": 100,&#13;  "deliveryAddress": {&#13;    "city": "bandung",&#13;    "state": "indonesia",&#13;    "street1": "ciwaruga",&#13;    "street2": "polban",&#13;    "zip": "12345"&#13;  },&#13;  "deliveryTime": "2024-04-05T07:59:41.408Z",&#13;  "lineItems": [&#13;    {&#13;      "menuItemId": "001",&#13;      "quantity": "1"&#13;    },&#13;    {&#13;      "menuItemId": "002",&#13;      "quantity": "2"&#13;    },&#13;    {&#13;      "menuItemId": "003",&#13;      "quantity": "1"&#13;    },&#13;    {&#13;      "menuItemId": "004",&#13;      "quantity": "2"&#13;    },&#13;    {&#13;      "menuItemId": "005",&#13;      "quantity": "1"&#13;    }&#13;  ],&#13;  "restaurantId": 3&#13;}</pre>|

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
