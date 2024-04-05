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
| **Expected Result**| Upon sending the request to create an order with an invalid items ID, the API should respond with an error message indicating that the specified restaurant is not found.|
| **Actual Result**| The actual result aligns with the expected result. Upon sending the request to create an order with an invalid restaurant ID, the API responds with an error message indicating that the specified item is not found. The response includes the error message "Invalid menu item id 999", accurately identifying the issue encountered. |
| **Test Result**| PASS|
| **Test Data**      | 
```json
{
  "consumerId": 3, 
  "deliveryAddress": {
    "city": "New York",
    "state": "New Jersey",
    "street1": "123 Main Street",
    "street2": "Suite 101",
    "zip": "12345"
  },
  "deliveryTime": "2024-04-05T08:40:20.096Z",
  "lineItems": [
    {
      "menuItemId": "001", 
      "quantity": 1
    },
    {
      "menuItemId": "002", 
      "quantity": 2
    }
  ],
  "restaurantId": 999 
}
``` 

| Scenario      | Test adding an order with invalid items (not existing in the database). |
| :----------- | :------------|
| **Preconditions** | 1. Open Swagger UI in localhost:8082/orders/index.html | 
|              | 2. Navigate to the section where the request body JSON input in POST /orders section, then click Try it Out. |
|              | 3. Write the JSON in Test Data for creating an order. |
|              | 4. Once the request body JSON is filled, click on the "Execute" button to send the request to the server. |
| **Step To Execute**     | 1. Open Swagger UI in localhost:8082/orders/index.html |
|              | 2. Look for the section where the request body JSON input in POST /orders section, then click Try it Out. |
|              | 3. Write the JSON in Test Data for creating an order. |
|              | 4. Once you've filled in the request body JSON, click on the "Execute" button to send the request to the server. |
| **Expected Result**| Upon sending the request to create an order with an invalid restaurant ID, the API should respond with an error message indicating that the specified restaurant is not found.|
| **Actual Result**| The actual result aligns with the expected result. Upon sending the request to create an order with an invalid restaurant ID, the API responds with an error message indicating that the specified restaurant is not found. The response includes the error message "Restaurant not found with id 999", accurately identifying the issue encountered. |
| **Test Result**| PASS|
| **Test Data**      | 
```json
{
  "consumerId": 3, 
  "deliveryAddress": {
    "city": "New York",
    "state": "New Jersey",
    "street1": "123 Main Street",
    "street2": "Suite 101",
    "zip": "12345"
  },
  "deliveryTime": "2024-04-05T08:40:20.096Z",
  "lineItems": [
    {
      "menuItemId": "001", 
      "quantity": 1
    },
    {
      "menuItemId": "002", 
      "quantity": 2
    }
  ],
  "restaurantId": 999 
}
``` 

### End-to-end tests Revise Order


### End-to-end test Cancel Order
