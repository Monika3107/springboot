# Rubicon Water order
API creation using springboot and using in memory H2 database 

Functional areas covered
1. API for quering the existing water orders.
2. API for placing the order and simultaneously checking that there are no overalpping orders
3. Cancel the order if not delivered
4. Scheduler for updating the status of the orders

Proper comments all along the code for maintainin readability of code.

Sample request and resonse point of the application :
GET : http://localhost:8080/order?id=1

Response :
  {
      "code": 200,
      "response": "Success",
      "model": {
          "id": 1,
          "farmId": 1,
          "startDateTime": "2020-01-27 03:41:00",
          "duration": 2,
          "status": "IN_PROGRESS"
      }
  }

Place order Request and Response :
POST : http://localhost:8080
Request :
  {
    "farmId" : 3,
    "startDateTime" : "2020-01-27 14:41:00",
    "duration" : 1
  }
Response :
  {
    "code": 200,
    "response": "Success",
    "model": {
        "id": 3,
        "farmId": 4,
        "startDateTime": "2020-01-27 02:41:00",
        "duration": 1,
        "status": "REQUESTED"
    }
  }
 
Overlaping order Request and Response :
  Request :
    {
    "farmId" : 3,
    "startDateTime" : "2020-01-27 14:41:00",
    "duration" : 1
    }
  Response :
    {
    "code": 404,
    "response": "An Order Already Exists",
    "model": null
  }
  
Cancel order Request and Response : 
POST : http://localhost:8080
  Request :
    {
      "id" : 2
    }
  Response :
    {
    "code": 200,
    "response": "Success",
    "model": {
        "id": 2,
        "farmId": 3,
        "startDateTime": "2020-01-27 02:41:00",
        "duration": 1,
        "status": "CANCELLED"
    }
}
