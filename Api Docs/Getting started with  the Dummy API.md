# Getting started with  the Dummy API

---

#### In this article

Introduction.

About request to the Dummy API.

---



### Introduction

Welcome to the Dummy API Example!

This API is designed to provide fake online REST services for testing and prototyping applications that utilize REST calls. Whether you need to display listings, perform CRUD operations, or explore REST API functionalities, our Dummy API offers a comprehensive environment for your development needs.



#### Key Features

- **Sample Data:** Utilize pre-defined data for realistic testing and development scenarios.

- **CRUD Operations:** Easily perform Create, Read, Update, and Delete operations to test your application's functionality.

- **Comprehensive Tutorials:** Access detailed tutorials and code examples to guide you through various use cases and help you get the most out of the API.

  

In addition, we're offering the subdomain `restapiexample.com` along with the main domain for sale. The package includes all codes, tutorials, social media pages, and the domain itself. Interested parties can [contact us](https://dummy.restapiexample.com/contact) for more details.

Use this documentation to explore all available REST services and enhance your development and prototyping processes with ease.



### About request to the Dummy API

This section describes the elements that make up an API request:  



#### HTTP methods

The HTTP method of an endpoint defines the type of action it performs on a given resource. Some common HTTP methods are `GET`, `POST`,  and`DELETE`. The Dummy API reference documentation provides the HTTP method for every endpoint. Where possible, the Dummy API strives to use an appropriate HTTP method for each action.

- `GET`: Used for retrieving resources.
- `POST`: Used for creating resources.
- `PUT`: Used for replacing resources or collections of resources.
- `DELETE`: Used for deleting resources.



#### Available Public APIs

| #    | Route            | Method   | Type   | Full Route                                                   | Description                   | Details                                                      |
| ---- | ---------------- | -------- | ------ | ------------------------------------------------------------ | ----------------------------- | ------------------------------------------------------------ |
| 1    | `/employee`      | `GET`    | `JSON` | https://dummy.restapiexample.com/api/v1/employees            | Get all employee data         | [Details](https://dummy.restapiexample.com/api/v1/employees) |
| 2    | `/employee/{id}` | `GET`    | `JSON` | [https://dummy.restapiexample.com/api/v1/employee/{id}](https://dummy.restapiexample.com/api/v1/employee/1) | Get a single employee data    | [Details](https://dummy.restapiexample.com/api/v1/employee/1) |
| 3    | `/create`        | `POST`   | `JSON` | https://dummy.restapiexample.com/api/v1/create               | Create new record in database | [Details](https://dummy.restapiexample.com/api/v1/create)    |
| 4    | `/update/{id}`   | `PUT`    | `JSON` | [https://dummy.restapiexample.com/api/v1/update/{id}](https://dummy.restapiexample.com/api/v1/update/21) | Update an employee record     | [Details](https://dummy.restapiexample.com/api/v1/update/21) |
| 5    | `/delete/{id}`   | `DELETE` | `JSON` | [https://dummy.restapiexample.com/api/v1/delete/{id}](https://dummy.restapiexample.com/api/v1/delete/2) | Delete an employee record     | [Details](https://dummy.restapiexample.com/api/v1/delete/2)  |