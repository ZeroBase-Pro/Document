# ZeroBase API 调用文档

## Hub相关API

### 获取节点列表
- API : `https://api.example.com/api/v1/hub/node`
- Method: `Get`
- Payload
    - Token : `string` - 唯一订单号
- Response
    - status : `200` - 返回正确状态码为200
    - body
        - code : `int` - 状态码
        - msg : `string` - 信息
        - results : `Array` - 节点列表

### 创建订单
- API : `https://api.example.com/api/v1/hub/token`
- Method: `Post`
- Payload
    - `None`
- Response
    - status : `200` - 返回正确状态码为200
    - body
        - code : `int` - 状态码
        - msg : `string` - 信息
        - results : `string` - 订单号

## Node相关API

### Proto定义
    syntax = "proto3";  // 指定proto版本

    package prove_service;  // 指定包名称

    message ProveRequest {
        string prover = 1;  // 指定Prover
        string temp = 2;    // 指定电路模板
        string input = 3;   // 指定Input
        bool is_encrypted = 4; // Input是否被加密
        string token = 5;   // 唯一订单号
        bool to_caicro = 6;    // 决定是否返回生成caicro的参数
    }

    message ProveResponse {
        int32 code = 1; // 状态码
        string response = 2;    // 如果状态码不为0的话则是返回错误信息, 为0则返回Proof
    }

    message EmptyRequest {

    }
    message EmptyResponse {

    }

    service ProveService {
        rpc prove(ProveRequest) returns (ProveResponse);  // 执行Prove操作
        rpc get_public_key(EmptyRequest) returns (ProveResponse);   // 返回加密input需要的公钥
        rpc ping(EmptyRequest) returns (EmptyResponse);  // 判断这个节点当前是否可用
    }

### 服务方法描述

- Prove操作
    - Function: `prove`
    - Request: `ProveRequest`
        - prover: 指定Prover
        - temp: 指定电路模板。
        - input: Input数据。
        - is_encrypted: Input否加密。
        - token: 订单号用于认证。
        - to_caicro: 是否返回生成caicro的参数。
    - Response: `ProveResponse`
        - Code: 状态码 : 0 - 表示成功。
        - Response: 成功时返回Proof，失败时返回错误信息。

- 获取公钥
    - Function: `get_public_key`
    - Request: `EmptyRequest`
    - Response: `ProveResponse`
        - Code: 状态码。
        - Response: 公钥或错误信息。

- 判断该节点是否可用
    - Function: `ping`
    - Request: `EmptyRequest`
    - Response: `EmptyResponse`

### 当前支持Prover列表
- circom

### 当前电路模板列表
- ZkLogin
