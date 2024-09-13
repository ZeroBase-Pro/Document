# ZeroBase Documentation

## Hub API

### Fetch Node List
- API : `https://api.example.com/api/v1/hub/node`
- Method: `Get`
- Payload
    - Token : `string` - Unique order number
- Response
    - status : `200` - Correct HTTP status code
    - body
        - code : `int` - Status code
        - msg : `string` - Message
        - results : `Array` - List of nodes

### Create Order
- API : `https://api.example.com/api/v1/hub/token`
- Method: `Post`
- Payload
    - `None`
- Response
    - status : `200` - Correct HTTP status code
    - body
        - code : `int` - Status code
        - msg : `string` - Message
        - results : `string` - Order number

## Node API

### Proto
    syntax = "proto3";  // Specify the proto version

    package prove_service;  // Specify the package name

    message ProveRequest {
        string prover = 1;  // Specify Prover
        string temp = 2;    // Specify the circuit template
        string input = 3;   // Specify Input
        bool is_encrypted = 4; // Whether the Input is encrypted
        string token = 5;   // Unique order number
        bool to_caicro = 6;    // whether to generating caicro
    }

    message ProveResponse {
        int32 code = 1; // Status code
        string response = 2;    // Returns Proof if successful, otherwise returns an error message
    }

    message EmptyRequest {

    }
    message EmptyResponse {

    }

    service ProveService {
        rpc prove(ProveRequest) returns (ProveResponse);  // Execute the Prove
        rpc get_public_key(EmptyRequest) returns (ProveResponse);   // Return the public key needed to encrypt the input
        rpc ping(EmptyRequest) returns (EmptyResponse);  // Determine if this node is currently available
    }

### Service Method Descriptions

- Prove
    - Function: `prove`
    - Request: `ProveRequest`
        - prover: Specify the Prover
        - temp: Specify the circuit template
        - input: Input data
        - is_encrypted: Whether the Input is encrypted
        - token: Unique order number
        - to_caicro: whether to generating caicro
    - Response: `ProveResponse`
        - Code: 0 - Successfully
        - Response: Returns Proof if successful, otherwise returns an error message


- Get Public Key
    - Function: `get_public_key`
    - Request: `EmptyRequest`
    - Response: `ProveResponse`
        - Code: 0 - Successfully
        - Response: Returns public key if successful, otherwise returns an error message

- Check Node Availability
    - Function: `ping`
    - Request: `EmptyRequest`
    - Response: `EmptyResponse`

### Current Supported Prover List
- circom

### Current Circuit Template List
- ZkLogin
