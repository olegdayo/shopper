# Shopper

## Architecture

### Schema

![Architecture](https://github.com/offluck/shopper/blob/master/documents/arch.drawio.svg)

### Description

Platform services:
- *HTTP-GateWay*: Handles HTTP request and, processes its contents and passes resulting gRPC request to other services
- *Auth*: Gives JWT over Bearer, based on user's credentials

Product services:
- *CheckOut*: Handles with user's "shopping cart"
- *OMS (Order Management Service)*: Hadles user's orders
- *Billing*: Handles user's financial tasks

## API

This is an API description. Source file can be found in `./{service-name}/api` folder

### HTTP

- **HTTP-GateWay**:
  - */api/v1/registration*
  - */api/v1/login*

### gRPC

      - Status code 0 (OK)
        - Token: string
      - Status code 1 (CANCELLED)
      - Status code 2 (UNKOWN)
      - Status code 3 (INVALID_ARGUMENT)
      - Status code 4 (DEADLINE_EXCEEDED)
      - Status code 5 (NOT_FOUND)
      - Status code 6 (ALREADY_EXISTS)
      - Status code 9 (FAILED_PRECONDITION)
      - Status code 13 (INTERNAL)
      - Status code 14 (UNAVAILABLE)

- ***Auth***:
  - **Register**: Registration of a new user
    - *Request*:
      - Username: string
      - Password: string
      - FirstName: string
      - LastName: string
      - Email: string
      - PhoneNumber: string
    - *Responses*:
      - Status code 0 (OK)
        - Token: string
      - Status code 1 (CANCELLED)
      - Status code 2 (UNKOWN)
      - Status code 3 (INVALID_ARGUMENT)
      - Status code 4 (DEADLINE_EXCEEDED)
      - Status code 6 (ALREADY_EXISTS)
      - Status code 13 (INTERNAL)

  - **Login**: User login
    - *Request*:
      - Username: string
      - Password: string
    - *Responses*:
      - Status code 0 (OK)
        - Token: string
      - Status code 1 (CANCELLED)
      - Status code 2 (UNKOWN)
      - Status code 3 (INVALID_ARGUMENT)
      - Status code 4 (DEADLINE_EXCEEDED)
      - Status code 5 (NOT_FOUND)
      - Status code 13 (INTERNAL)

- ***CheckOut***:
  - **AddToCart**: Adds product to cart
    - *Request*:
      - UserID: uint64
      - SKU: uint32
      - Count: uint32
    - *Responses*:
      - Status code 0 (OK)
      - Status code 1 (CANCELLED)
      - Status code 2 (UNKOWN)
      - Status code 3 (INVALID_ARGUMENT)
      - Status code 4 (DEADLINE_EXCEEDED)
      - Status code 5 (NOT_FOUND)
      - Status code 13 (INTERNAL)
      - Status code 14 (UNAVAILABLE)
  - **DeleteFromCart**: Deletes product from cart
    - *Request*:
      - UserID: uint64
      - SKU: uint32
      - Count: uint32
    - *Responses*:
      - Status code 0 (OK)
      - Status code 1 (CANCELLED)
      - Status code 2 (UNKOWN)
      - Status code 3 (INVALID_ARGUMENT)
      - Status code 4 (DEADLINE_EXCEEDED)
      - Status code 5 (NOT_FOUND)
      - Status code 9 (FAILED_PRECONDITION)
      - Status code 13 (INTERNAL)
      - Status code 14 (UNAVAILABLE)
  - **ListCart**: Shows cart info
    - *Request*:
      - UserID: string
    - *Responses*:
      - Status code 0 (OK)
        - []Items
          - SKU: uint32
          - Count: uint32
          - Name: string
          - Price: uint32
        - TotalPrice: uint32
      - Status code 1 (CANCELLED)
      - Status code 2 (UNKOWN)
      - Status code 3 (INVALID_ARGUMENT)
      - Status code 4 (DEADLINE_EXCEEDED)
      - Status code 13 (INTERNAL)
      - Status code 14 (UNAVAILABLE)
  - **Order**: Sends order request
    - *Request*:
    - *Responses*:
      - Status code 0 (OK)
        - Token: string
      - Status code 1 (CANCELLED)
      - Status code 2 (UNKOWN)
      - Status code 3 (INVALID_ARGUMENT)
      - Status code 4 (DEADLINE_EXCEEDED)
      - Status code 5 (NOT_FOUND)
      - Status code 6 (ALREADY_EXISTS)
      - Status code 9 (FAILED_PRECONDITION)
      - Status code 13 (INTERNAL)
      - Status code 14 (UNAVAILABLE)

- ***OMS***:


- ***Billing***:
