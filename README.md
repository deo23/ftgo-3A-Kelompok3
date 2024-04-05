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
| **Scenario**     | 1. Test adding an order with valid consumer and restaurant IDs. |
|              | 2. Test adding an order with invalid consumer ID (not existing in the database). |
|              | 3. Test adding an order with invalid restaurant ID (not existing in the database). |
|              | 4. Test adding an order with invalid items (not existing in the database). |

| Feature      | Cancel Order |
| :----------- | :------------|
| **Requirements** | Membatalkan order yang sebelumnya sudah di create. | 
| **Scenario**     | 1. Test cancel an order with invalid consumer ID. |
|              | 2. Test cancel an order with valid consumer ID. |

## End-to-end tests
### End-to-end tests Create Order
#### Scenario-001: Test adding an order with valid consumer and restaurant IDs.
| Scenario      | Test adding an order with invalid restaurant ID (not existing in the database). |
| :----------- | :------------|
| **Preconditions** | 1. The FTGO application is deployed and running. | 
|              | 2. All microservices (consumer service, restaurant service, order service, kitchen service, accounting service, order history service, and API gateway) are operational.|
|              | 3. Necessary data such as consumers and menu items are available in the system. |
|              | 4. The restaurant ID used in this scenario exists in the database. |
| **Step To Execute**     | 1. Open Swagger UI in localhost:8082/orders/index.html |
|              | 2. Look for the section where the request body JSON input in POST /orders section, then click Try it Out. |
|              | 3. Write the JSON in Test Data for creating an order. |
|              | 4. Once you've filled in the request body JSON, click on the "Execute" button to send the request to the server. |
| **Expected Result**| 1. The consumer successfully places the order. |
|              | 2. The order details, including selected items, are correctly associated with the consumer and restaurant IDs.|
|              | 3. The order request is processed without any visible errors or glitches. |
|              | 4. The system sends notifications to the restaurant, informing them of the new order. |
|              | 5. The consumer receives a confirmation notification, indicating the successful submission of the order. |
|              | 6. The API gateway properly routes the order request to the appropriate services (ftgo-order-service, ftgo-restaurant-service, etc.). |
|              | 7. The order is visible in the order history service as a pending or received order. |
| **Actual Result**| |
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
#### Scenario-001:
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

#### Scenario-001:
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