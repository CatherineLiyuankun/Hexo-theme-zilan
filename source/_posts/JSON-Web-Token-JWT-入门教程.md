---
title: JSON Web Token (JWT) 入门教程
catalog: true
date: 2024-09-03 16:21:05
subtitle:
header-img:
tags:
- Authentication
categories:
- TECH
---

## JSON Web Token

`JWT (JSON Web Token)` is a compact, URL-safe means of representing claims to be transferred between two parties. The claims in a JWT are encoded as a JSON object that is used as the payload of the token. This JSON object is then digitally signed using a secret key or a public/private key pair.

### Structure of a JWT

它是一个很长的字符串，中间用点（.）分隔成三个部分。注意，JWT 内部是没有换行的，这里只是为了便于展示，将它写成了几行。
A JWT consists of three parts, separated by dots (`.`):

- **Header**: Contains metadata about the token, such as the type of token (`JWT`) and the signing algorithm (`HMAC SHA256` or `RSA`).
- **Payload**: Contains the claims, which are statements about an entity (typically, the user) and additional data.
- **Signature**: Used to verify that the token was not altered after it was issued.

Example of a JWT:

    ```bash
    # Header.Payload.Signature

    eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.
    eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.
    SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c
    ```

### Common Use Cases for JWT

- **Authentication**: JWTs are often used for securing APIs, where the client receives a token upon successful login and then includes this token in the Authorization header of subsequent requests.

- **Information Exchange**: JWTs can be used to securely transmit information between parties. Since they can be signed, the information can be trusted to be accurate.

### Summary

- **JWT** is a way to securely transmit information between two parties.
- It is composed of a header, payload, and signature.
- JWTs are commonly used for authentication in web applications.
- Libraries like `PyJWT` in Python and `jsonwebtoken` in Node.js make it easy to create and verify JWTs.

- JWT 默认是不加密，但也是可以加密的。生成原始 Token 以后，可以用密钥再加密一次。
- JWT 不加密的情况下，不能将秘密数据写入 JWT。
- JWT 不仅可以用于认证，也可以用于交换信息。有效使用 JWT，可以降低服务器查询数据库的次数。
- JWT 的最大缺点是，由于服务器不保存 session 状态，因此无法在使用过程中废止某个 token，或者更改 token 的权限。也就是说，一旦 JWT 签发了，在- 之前就会始终有效，除非服务器部署额外的逻辑
- JWT 本身包含了认证信息，一旦泄露，任何人都可以获得该令牌的所有权限。为了减少盗用，JWT 的有效期应该设置得比较短。对于一些比较重要的权限，使用时应该再次对用户进行认证。
- 为了减少盗用，JWT 不应该使用 HTTP 协议明码传输，要使用 HTTPS 协议传输。

### JWT 和 Session Id 的区别总结

### JWT

- 服务器上不保存任何东西，JWT 存储于客户端中
- 由服务器 加密（可选）和签名
- token 包含用户的所有信息
- 所有信息都存储于 token 本身中
- 易于扩展到cluster

![JWT workflow](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/JSON-Web-Token-JWT-%E5%85%A5%E9%97%A8%E6%95%99%E7%A8%8B/JWT.png)

### Session Id

- Session Id 保存于服务器和客户端中
- 加密并签名
- Session Id 是对用户的引用
- 服务器需要查找用户并进行必要的检查
- 难以扩展到cluster

![Session workflow](https://github.com/CatherineLiyuankun/PictureBed/raw/master/blog/post/JSON-Web-Token-JWT-%E5%85%A5%E9%97%A8%E6%95%99%E7%A8%8B/session.png)

## JWT教程

[JSON Web Token 入门教程 阮一峰](https://www.ruanyifeng.com/blog/2018/07/json_web_token-tutorial.html)
[JWT 介绍 - Step by Step](https://www.cnblogs.com/ittranslator/p/14595165.html)
    - [Intro to JWT - Step by Step](https://dev.to/moe23/intro-to-jwt-mcb)

## `jsonwebtoken` in Node.js

1. Installing Required Libraries

    ```bash
    npm install jsonwebtoken
    ```

2. Creating a JWT

    ```javascript
    const jwt = require('jsonwebtoken');

    // Define your secret key
    const secretKey = 'your-256-bit-secret';

    // Create the payload (claims)
    const payload = {
    sub: '1234567890', // subject
    name: 'John Doe',
    iat: Math.floor(Date.now() / 1000), // issued at
    exp: Math.floor(Date.now() / 1000) + (60 * 30) // expiration time
    };

    // Encode the payload to create a JWT
    const token = jwt.sign(payload, secretKey, { algorithm: 'HS256' });

    console.log(token);
    ```

3. Verifying a JWT

    ```javascript
    jwt.verify(token, secretKey, (err, decoded) => {
    if (err) {
        if (err.name === 'TokenExpiredError') {
        console.log("Token has expired");
        } else {
        console.log("Invalid token");
        }
    } else {
        console.log(decoded);
    }
    });

    ```

## `PyJWT` in Python

1. Installing Required Libraries

    ```bash
    pip install PyJWT
    ```

2. Creating a JWT

    ```python
    import jwt
    import datetime

    # Define your secret key
    secret_key = 'your-256-bit-secret'

    # Create the payload (claims)
    payload = {
        'sub': '1234567890',  # subject
        'name': 'John Doe',
        'iat': datetime.datetime.utcnow(),  # issued at
        'exp': datetime.datetime.utcnow() + datetime.timedelta(minutes=30)  # expiration time
    }

    # Encode the payload to create a JWT
    token = jwt.encode(payload, secret_key, algorithm='HS256')

    print(token)
    ```

3. Verifying a JWT

    ```python
    try:
        decoded_token = jwt.decode(token, secret_key, algorithms=['HS256'])
        print(decoded_token)
    except jwt.ExpiredSignatureError:
        print("Token has expired")
    except jwt.InvalidTokenError:
        print("Invalid token")

    ```
