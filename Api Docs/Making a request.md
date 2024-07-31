# Making a request

---

This section describes how to make requests to the Dummy API to retrieve employee data:

- Get all employees.

- Get a single record.
- Create a record.
- Update a record.
- Delete data.

---



#### Get all employees

To access all employee data, use the `/employees` endpoint with the `GET` method. This endpoint returns a list of all employees in JSON format.

**Endpoint:**

- **Route:** `/employees`
- **Method:** `GET`

**Sample request:**

<div style="background-color: #d9edf7; padding: 10px; border: 1px solid #bce8f1; border-radius: 5px;">
  <strong>GET </strong> https://dummy.restapiexample.com/api/v1/employees
</div>

**Sample response:**

``` json
{
  "status": "success",
  "data": [
    {
      "id": "1",
      "employee_name": "Tiger Nixon",
      "employee_salary": "320800",
      "employee_age": "61",
      "profile_image": ""
    },
    {
      "id": "2",
      "employee_name": "Garrett Winters",
      "employee_salary": "170750",
      "employee_age": "63",
      "profile_image": ""
    }
    // More employee records...
  ]
}

```

This response includes the status of the request and an array of employee data, with each employee's ID, name, salary, age, and profile image.



#### Get a Single Record

To access data for a specific employee, use the `/employee/{id}` endpoint with the `GET` method. Replace `{id}` with the employee's ID to retrieve their information.

**Endpoint:**

- **Route:** `/employee/{id}`
- **Method:** `GET`

**Sample request:**

<div style="background-color: #d9edf7; padding: 10px; border: 1px solid #bce8f1; border-radius: 5px;">
  <strong>GET </strong> https://dummy.restapiexample.com/api/v1/employee/1
</div>

**Sample response:**

```json
{
  "status": "success",
  "data": {
    "id": "1",
    "employee_name": "Tiger Nixon",
    "employee_salary": "320800",
    "employee_age": "61",
    "profile_image": ""
  }
}
```

This response includes the status of the request and the data for the specified employee, such as their ID, name, salary, age, and profile image.

**cURL for `/employee/{id}`:**

<div style="background-color: #d9edf7; padding: 10px; border: 1px solid #bce8f1; border-radius: 5px;">
  <strong>curl -X GET </strong>  https://dummy.restapiexample.com/api/v1/employee/1

**Expected Result:** This command retrieves the data for the employee with ID 1, returning a JSON object with the employee's details.



#### Create a Record

To create employee data, use the `/create` endpoint with the `POST` method. This endpoint allows you to add a new employee record.

**Endpoint:**

- **Route:** `/create`
- **Method:** `POST`

**Sample request:**

<div style="background-color: #dff0d8; padding: 10px; border: 1px solid #d6e9c6; border-radius: 5px;">
  <strong>POST </strong> https://dummy.restapiexample.com/api/v1/create
</div>

Fields required for creating an employee:

- **Name:** A string representing the employee's name.
- **Salary:** A string or number representing the employee's salary.
- **Age:** A string or number representing the employee's age.

Other elements that could be included:

- **Profile Image:** A URL or base64 encoded string for the employee's profile image.
- **Department:** A string representing the department the employee belongs to.
- **Position:** A string representing the employee's job position.

<div style="background-color: #dff0d8; padding: 10px; border: 1px solid #d6e9c6; border-radius: 5px;">
  <strong>POST </strong> https://dummy.restapiexample.com/api/v1/create?name=Camilo Garcia&salary=1000&age=26
</div>

``` json
Content-Type: application/json 

{  
	"name": "Camilo Garcia",  
	"salary": "1000",  
	"age": "26" 
}
```

**Sample response:**

```json
{
    "status": "success",
    "data": {
        "name": "Camilo Garcia",
        "salary": "1000",
        "age": "26",
        "id": 9025
    },
    "message": "Successfully! Record has been added."
}
```

<div style="background-color: #dff0d8; padding: 10px; border: 1px solid #d6e9c6; border-radius: 5px;">   <strong>Success:</strong> The response includes the status of the request and the data for the newly created employee, including their ID. </div>

**cURL for `/create`:**

```
curl -X POST "https://dummy.restapiexample.com/api/v1/create" -H "Content-Type: application/json" -d '{
  "name": "test",
  "salary": "123",
  "age": "23"
}'
```

**Expected Result:** This command creates a new employee record with the provided name, salary, and age, returning a JSON object with the newly created employee's details, including their ID.



#### Update a Record

To update an existing employee record, use the `/update/{id}` endpoint with the `PUT` method. Replace `{id}` with the employee's ID to update their information.

**Endpoint:**

- **Route:** `/update/{id}`
- **Method:** `PUT`

**Sample Request:**

<div style="background-color: #f2dede; padding: 10px; border: 1px solid #d6e9c6; border-radius: 5px;">
  <strong>PUT </strong> https://dummy.restapiexample.com/api/v1/update/9025
</div>

```json
Content-Type: application/json

{
  "name": "test",
  "salary": "123",
  "age": "23"
}
```

<div style="background-color: #f2dede; padding: 10px; border: 1px solid #d6e9c6; border-radius: 5px;">
  <strong>PUT </strong> https://dummy.restapiexample.com/api/v1/update/9025?name=Juan Garcia&age=34
</div>

**Sample Response:**

```json
{
    "status": "success",
    "data": {
        "name": "Juan Garcia",
        "age": "34"
    },
    "message": "Successfully! Record has been updated."
}
```

<div style="background-color: #dff0d8; padding: 10px; border: 1px solid #d6e9c6; border-radius: 5px;">   <strong>Success:</strong> The response includes the status of the request and the updated data for the specified employee. </div>



#### Delete Data

To delete an employee record, use the `/delete/{id}` endpoint with the `DELETE` method. Replace `{id}` with the employee's ID to delete their record.

**Endpoint:**

- **Route:** `/delete/{id}`
- **Method:** `DELETE`

**Sample Request:**

<div style="background-color: #f2defe; padding: 10px; border: 1px solid #d6e9c6; border-radius: 5px;">
  <strong>DELETE </strong> https://dummy.restapiexample.com/api/v1/delete/9025
</div>

**Sample Response:**

``` json
{
    "status": "success",
    "data": "9025",
    "message": "Successfully! Record has been deleted"
}
```

<div style="background-color: #dff0d8; padding: 10px; border: 1px solid #ebccd1; border-radius: 5px;">   <strong>Success:</strong> The response includes the status of the request and a message confirming the deletion of the specified employee record. </div>



### Summary

- **Get All Employees:** Use the `/employees` endpoint to retrieve a list of all employees.
- **Get a Single Record:** Use the `/employee/{id}` endpoint to retrieve data for a specific employee by their ID.
- **Create a Record:** Use the `/create` endpoint with the `POST` method to add new employee data.
- **Update a Record:** Use the `/update/{id}` endpoint with the `PUT` method to modify existing employee data.
- **Delete Data:** Use the `/delete/{id}` endpoint with the `DELETE` method to remove an employee record.

These endpoints are designed to help you easily access employee data for testing and prototyping your applications and  supporting the basic CRUD operations in your applications.