# API

月初补贴点餐系统API文档

## 目录

* [约定](#约定)
* [安卓客户端API](#安卓客户端API)
  * [用户](#用户)
    * [注册验证码](#注册验证码)
    * [用户注册](#用户注册)
    * [用户登录](#用户登录)
    * [微信用户登录](#微信用户登录)
    * [用户登出（access_token）](#用户登出（access_token）)
    * [用户登出（refresh_token）](#用户登出（refresh_token）)
    * [令牌刷新](#令牌刷新)
  * [餐馆](#餐馆)
    * [所有餐馆](#所有餐馆)
    * [餐馆查询](#餐馆查询)
    * [单个餐馆资料](#单个餐馆资料)
  * [餐桌](#餐桌)
    *  [单个餐桌](#单个餐桌)
  * [餐馆食物类别](#餐馆食物类别)
    * [单个类别](#单个类别)
  * [食物](#食物)
    * [单个食物](#单个食物)
  * [订单单项](#订单单项)
    * [订单单项状态](#订单单项状态)
    * [某餐桌的所有订单单项](#某餐桌的所有订单单项)
    * [单个订单单项](#单个订单单项)
  * [订单](#订单)
    * [订单状态](#订单状态)
    * [个人的所有订单及提交订单](#个人的所有订单及提交订单)
    * [单个订单](#单个订单)
* 管理后台API

## 约定

* 在url路径中的<>符号中括起来的信息，是作为后端接受的变量，一般来说是指某个对象的id。例如路径***/users/\<int: user_id\>/add***，其中int则指该变量的类型，user_id指的的是这里填入该user对象的id，如id为1，则该路径实际应为***/users/1/add***

## 安卓客户端API

### 用户

#### 注册验证码

* **url:**

  > /captcha

* **请求方法：GET**

  * Request：

    * Header：None
    * body:  None

  * Response：

    * success: 200

      ```json
      {
          "captcha_id": "DCO5D9D23I",
          "url": "https://www.example.com/static/captchas/DCO5D9D23I"
      }
      ```

- **请求方法：POST**

  - Request：

    - Header：None

    - body:  

      ```json
      {
          "captcha_id": "DCO5D9D23I",
          "captcha": "287a"
      }
      ```

  - Response：

    - Success: 200

      验证码正确

    * Fail: 403

      验证码错误

#### 用户注册

- **url:**

  > /registration

- **请求方法：POST**

  - Request：

    - Header：None

    - body:  

      ```json
      {
          "captcha_id": "DCO5D9D23I",
          "captcha": "287a",
          "nickname": "leo",
          "username": "your username",
          "password": "your password"
      }
      ```

  - Response：

    - Success: 200

      ```json
      {
          "captcha_id": "DCO5D9D23I",
          "url": "https://www.example.com/static/captchas/DCO5D9D23I"
      }
      ```


    * Fail:
    
      403：验证码错误或用户名已存在
    
      500：出错

#### 用户登录

- **url:**

  > /login

- **请求方法：POST**

  - Request：

    - Header：None

    - body:  

      ```json
      {
          "username": "your username",
          "password": "your password"
      }
      ```

  - Response：

    - Success: 200

      ```json
      {
          "message": "Logged in as <username>.",
          "access_token": "<jwt_access_token>",
          "refresh_token": "<jwt_refresh_token>"
      }
      ```

    - Fail

      403：用户不存在

      401：密码错误

#### 微信用户登录

- **url:**

  > /wxlogin

- **请求方法：POST**

  - Request：

    - Header：None

    - body:  

      ```json
      {
          "code": "weixin code",
          "nickname": "leo"
      }
      ```

  - Response：

    - Success: 200

      ```json
      {
          "message": "Logged in as <username>.",
          "access_token": "<jwt_access_token>",
          "refresh_token": "<jwt_refresh_token>"
      }
      ```

    - Fail

      500：出错

#### 用户登出（access_token）

- **url:**

  > /logout/access

- **请求方法：POST**

  - Request：

    - Header：

      Authorization: Bearer \<jwt_access_token\>

    - body:  None

  - Response：

    - Success: 200

    - Fail: 500

#### 用户登出（refresh_token）

- **url:**

  > /logout/refresh

- **请求方法：POST**

  - Request：

    - Header：

      Authorization: Bearer \<jwt_refresh_token\>

    - body:  None

  - Response：

    - Success: 200

    - Fail: 500

#### 令牌刷新

- **url:**

  > /token/refresh

- **请求方法：POST**

  - Request：

    - Header：

      Authorization: Bearer \<jwt_refresh_token\>

    - body:  None

  - Response：

    - Success: 200

      ```json
      {
          "access_token": "<jwt_access_token>"
      }
      ```

    - Fail: 401

### 餐馆

#### 所有餐馆

- **url:**

  > /api/restaurants

- **请求方法：GET

  - Request：

    - Header：None
    - body:  None

  - Response：

    - Success: 200

      ```json
      {
          "restaurants": [
              {
                  "id": 1,
                  "name": "Happy Day",
                  "introduction": "A restaurant in china.",
                  "opening_time": "周一至周五，11：00am-10:00pm",
                  "address": "大学城北xxx路",
                  "images": [
                      {
                          "id": 1,
                          "order_id": 1,
                          "image_url": "https://example.com/static/images/DNIDJDIFXC1454DF892DF.jpg",
                          "restaurant_id": 1
                      }
                  ],
                  "boards": [
                      {
                          "id": 1,
                          "occupation": False,
                          "name": "A1",
                          "seat_num": 2,
                          "qr_code": "https://example.com/static/images/DNIDJDIFXC1454DF892DF.jpg",
                          "restaurant_id": 1
                      }
                  ],
                  "categories": [
                      {
                          "id": 1,
                          "name": "主食",
                          "priority": 1,
                          "restaurant_id": 1,
                          "food": [
                              {
                                  "id": 1,
                                  "name": "米饭",
                                  "description": "中国人最爱",
                                  "price": 1.00,
                                  "image": "https://example.com/static/images/DNIDJDIFXC1454DF892DF.jpg",
                                  "likes": 1,
                                  "sales": 1,
                                  "category_id": 1
                              }
                          ]
                      }
                  ]
              }
          ]
      }
      ```

#### 餐馆查询

- **url:**

  > /api/restaurants/query?name="xxx"

- **请求方法：GET

  - Request：

    - Header：None
    - body:  None

  - Response：

    - Success: 200

      与所有餐馆api的respond相似

#### 单个餐馆资料

- **url:**

  > /api/restaurants/\<int: restaurant_id\>

- **请求方法：GET

  - Request：

    - Header：None
    - body:  None

  - Response：

    - Success: 200

      ```json
      {
          "restaurant": {
              "id": 1,
              "name": "Happy Day",
              "introduction": "A restaurant in china.",
              "opening_time": "周一至周五，11：00am-10:00pm",
              "address": "大学城北xxx路",
              "images": [
                  {
                      "id": 1,
                      "order_id": 1,
                      "image_url": "https://example.com/static/images/DNIDJDIFXC1454DF892DF.jpg",
                      "restaurant_id": 1
                  }
              ],
              "boards": [
                  {
                      "id": 1,
                      "occupation": False,
                      "name": "A1",
                      "seat_num": 2,
                      "qr_code": "https://example.com/static/images/DNIDJDIFXC1454DF892DF.jpg",
                      "restaurant_id": 1
                  }
              ],
              "categories": [
                  {
                      "id": 1,
                      "name": "主食",
                      "priority": 1,
                      "restaurant_id": 1,
                      "food": [
                          {
                              "id": 1,
                              "name": "米饭",
                              "description": "中国人最爱",
                              "price": 1.00,
                              "image": "https://example.com/static/images/DNIDJDIFXC1454DF892DF.jpg",
                              "likes": 1,
                              "sales": 1,
                              "category_id": 1
                          }
                      ]
                  }
              ]
          }
      }
      ```

### 餐桌

#### 单个餐桌

- **url:**

  > /api/restaurants/\<int: restaurant_id\>/boards/\<int: board_id\>

- **请求方法：GET**

  - Request：

    - Header：None
    - body:  None

  - Response：

    - Success: 200

      ```json
      {
          "board": {
              "id": 1,
              "occupation": False,
              "name": "A1",
              "seat_num": 2,
              "qr_code": "https://example.com/static/images/DNIDJDIFXC1454DF892DF.jpg",
              "restaurant_id": 1
          }
      }
      ```

### 餐馆食物类别

#### 单个类别

- **url:**

  > /api/restaurants/\<int: restaurant_id\>/categories/\<int: category_id\>

- **请求方法：GET**

  - Request：

    - Header：None
    - body:  None

  - Response：

    - Success: 200

      ```json
      {
          "category": {
              "id": 1,
              "name": "主食",
              "priority": 1,
              "restaurant_id": 1,
              "food": [
                  {
                      "id": 1,
                      "name": "米饭",
                      "description": "中国人最爱",
                      "price": 1.00,
                      "image": "https://example.com/static/images/DNIDJDIFXC1454DF892DF.jpg",
                      "likes": 1,
                      "sales": 1,
                      "category_id": 1
                  }
              ]
          }
      }
      ```

### 食物

#### 单个食物

- **url:**

  > /api/categories/\<int: category_id\>/foods/\<int: food_id\>

- **请求方法：GET**

  - Request：

    - Header：None
    - body:  None

  - Response：

    - Success: 200

      ```json
      {
          "food": {
              "id": 1,
              "name": "米饭",
              "description": "中国人最爱",
              "price": 1.00,
              "image": "https://example.com/static/images/DNIDJDIFXC1454DF892DF.jpg",
              "likes": 1,
              "sales": 1,
              "category_id": 1
          }
      }
      ```

### 订单单项

#### 订单单项状态

* ORDERING: 选中，还没提交
* CONFIRMED：已提交
* CANCELED：被商家取消的

#### 某个餐桌的所有订单单项

- **url:**

  > /api/boards/\<int: board_id\>/order_items/\<int: order_item_id\>

- **请求方法：GET**

  - Request：

    - Header：None
    - body:  None

  - Response：

    - Success: 200

      ```json
      {
          "_comment": "have status like: ORDERING/CONFIRMED/CANCELED",
          "order_items": [
              {
                  "id": 1,
                  "status": "ORDERING",
                  "quantity": 2,
                  "owner": {
                      "id": 1,
                      "username": "test",
                      "nickname": "leo"
                  },
                  "board_id": 1,
                  "food": {
                      "id": 1,
                      "name": "米饭"
                  }
              }
          ]
      }
      ```

* **请求方法：POST**

- Request：

  - 备注：

    - 当同一个用户添加同一个食品（food_id）的时候，后端会寻找当前购物车中是否存在该用户之前已经添加的该食品关联的order_item项，并修改其quantity值为新值，并返回该order_item。如购物车中没有，则创建一个新的order_item项。

  - Header：

    Authorization: Bearer \<jwt_access_token\>

  - body:  

    ```json
    {
        "quantity": 2,
        "food_id": 1
    }
    ```

- Response：

  - Success: 200

    ```json
    {
        "_comment": "have status like: ORDERING/CONFIRMED/CANCELED",
        "order_item": {
            "id": 1,
            "status": "ORDERING",
            "quantity": 2,
            "owner": {
                "id": 1,
                "username": "test",
                "nickname": "leo"
            },
            "board_id": 1,
            "food": {
                "id": 1,
                "name": "米饭"
            }
        }
    }
    ```

  - Fail:

    500：出错

#### 单个订单单项

- **url:**

  > /api/order_items/\<int: order_item_id\>

- **请求方法：GET**

  - Request：

    - Header：None
    - body:  None

  - Response：

    - Success: 200

      ```json
      {
          "_comment": "have status like: ORDERING/CONFIRMED/CANCELED",
          "order_item": [
              {
                  "id": 1,
                  "status": "ORDERING",
                  "quantity": 2,
                  "owner": {
                      "id": 1,
                      "username": "test",
                      "nickname": "leo"
                  },
                  "board_id": 1,
                  "food": {
                      "id": 1,
                      "name": "米饭"
                  }
              }
          ]
      }
      ```

- **请求方法：PUT

- Request：

  - 备注：

    - 这里post的数据中，quantity和action是二选其一的，可以只提供quantity或只提供action。后端逻辑：先判断action，如果为increment则根据原来的quantity加一，为decrement则减一。再判断是否有quantity，如果有就直接覆盖原来的quantity值。

  - Header：

    Authorization: Bearer \<jwt_access_token\>

  - body:  

    ```json
    {
        "quantity": 3,
        "action": "increment or decrement"
    }
    ```

- Response：

  - Success: 200

    ```json
    {
        "order_item": {
            "id": 1,
            "status": "ORDERING",
            "quantity": 3,
            "owner": {
                "id": 1,
                "username": "test",
                "nickname": "leo"
            },
            "board_id": 1,
            "food": {
                "id": 1,
                "name": "米饭"
            }
        }
    }
    ```

  - Fail:

    500：出错

    403： 未知的操作或修改的是他人的订单项

- **请求方法：DELETE**

  - Request：

    - Header：

      Authorization: Bearer \<jwt_access_token\>

    - body:  None

  - Response：

    - Success: 200

    - Fail：

      500：出错

      403：删除他人的订单项

### 订单

#### 订单状态

* UNFILLED：已提交商家，用户还没用餐完毕
* UNPAID：用户确认用餐完毕，但还没付款
* FINISHED：商家确认收到钱，订单完成

#### 个人的所有订单及提交订单

- **url:**

  > /api/orders

- **请求方法：GET**

  - Request：

    - Header：

      Authorization: Bearer \<jwt_access_token\>

    - body:  None

  - Response：

    - Success: 200

      ```json
      {
          "_comment": "have status like: UNFILLED/UNPAID/FINISHED",
          "orders": [
              {
                  "id": 1,
                  "created_time": "2018-12-12 02:22:23",
                  "updated_time": "2018-12-12 02:23:45",
                  "status": "UNFILLED",
                  "remark": "少盐少油",
                  "total_cost": 1.00,
                  "owner_id": 1,
                  "restaurant": {
                      "id": 1,
                      "name": "Happy Day"
                  },
                  "items": [
                      {
                          "id": 1,
              			"status": "CONFIRMED",
              			"quantity": 3,
              			"owner": {
                 				"id": 1,
                  			"username": "test",
                              "nickname": "leo"
              			},
              			"board_id": 1,
              			"food": {
                  			"id": 1,
                  			"name": "米饭"
              			}
                      }
                  ]
              }
          ]
      }
      ```

- **请求方法：POST**

- Request：

  - Header：

    Authorization: Bearer \<jwt_access_token\>

  - body:  

    ```json
    {
        "remark": "少盐少油",
        "restaurant_id": 1,
        "items": [1, 2, 3]
    }
    ```

- Response：

  - Success: 200

    ```json
    {
        "_comment": "have status like: UNFILLED/UNPAID/FINISHED",
        "order": {
            "id": 1,
            "created_time": "2018-12-12 02:22:23",
            "updated_time": "2018-12-12 02:23:45",
            "status": "UNFILLED",
            "remark": "少盐少油",
            "total_cost": 1.00,
            "owner_id": 1,
            "restaurant": {
                "id": 1,
                "name": "Happy Day"
            },
            "items": [
                {
                    "id": 1,
                    "status": "CONFIRMED",
                    "quantity": 3,
                    "owner": {
                        "id": 1,
                        "username": "test",
                        "nickname": "leo"
                    },
                    "board_id": 1,
                    "food": {
                        "id": 1,
                        "name": "米饭"
                    }
                }
            ]
        }
    }
    ```

  - Fail:

    500：出错

#### 单个订单

- **url:**

  > /api/orders/\<int: order_id\>

- **请求方法：GET**

  - Request：

    - Header：

      Authorization: Bearer \<jwt_access_token\>

    - body:  None

  - Response：

    - Success: 200

      ```json
      {
          "_comment": "have status like: UNFILLED/UNPAID/FINISHED",
          "order": {
              "id": 1,
              "created_time": "2018-12-12 02:22:23",
              "updated_time": "2018-12-12 02:23:45",
              "status": "UNFILLED",
              "remark": "少盐少油",
              "total_cost": 1.00,
              "owner_id": 1,
              "restaurant": {
                  "id": 1,
                  "name": "Happy Day"
              },
              "items": [
                  {
                      "id": 1,
                      "status": "CONFIRMED",
                      "quantity": 3,
                      "owner": {
                          "id": 1,
                          "username": "test",
                          "nickname": "leo"
                      },
                      "board_id": 1,
                      "food": {
                          "id": 1,
                          "name": "米饭"
                      }
                  }
              ]
          }
      }
      ```

- **请求方法：POST**

- Request：

  - Header：

    Authorization: Bearer \<jwt_access_token\>

  - body:  

    ```json
    {
        "remark": "少盐少油",
        "restaurant_id": 1,
        "items": [4, 5, 6]
    }
    ```

- Response：

  - Success: 200

    同上

  - Fail:

    500：出错

    403：给他人的订单加菜

- **请求方法：PUT**

- Request：

  - Header：

    Authorization: Bearer \<jwt_access_token\>

  - body:  None

- Response：

  - Success: 200

  - Fail:

    500：出错

    403：给他人的订单申请结账