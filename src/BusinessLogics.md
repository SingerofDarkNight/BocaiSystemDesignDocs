# 业务逻辑

说明：此文档描述的业务逻辑有缺陷，它默认了站点拥有无限的代币。
说明：此文档描述的业务并不完全。

## 单个盘口的流程
![flow of a specific betting game](images/flow-of-betting-games.png)

## 用户代币的出入图
![flow of a user's lumbers](images/flow-of-lumbers.png)

## 基于use case的业务流程
### 创建盘口
**Role**: admin

**URL**: games/

**HTTP Verb**: POST

**required field**: *name*, *options*(an option must include *name* and *odds*
at the same time)

**optional fields**: *maximum_bet_options*(allow bet on multiple fields, no
bigger than the number of the options)

**forbidden fields**: *status*, *enrolled*, *winning_option*

**response**:
1. the response should not contain the *enrolled* fields;
2. If the game is created, the server should repond with "201 Created" along
   with the game data;
3. If the server failed to create the game, the server should respond with
   "400 Bad Request" and provide a message describing the problem;

example request data:
```json
{
    "name": "2018 TI8淘汰赛 LGD vs OG",
    "description": "TI8 上班赛区 LGD vs OG",
    "end_time_for_bet": "2018-12-01T14:20:31.002Z",
    "time_for_payoff": "2018-12-09T14:20:31.002Z",
    "options": [{
        "name": "LGD 2:0 OG",
        "odds": 2.0
    }, {
        "name": "LGD 2:1 OG",
        "odds": 3.0
    }, {
        "name": "LGD 1:2 OG",
        "odds": 6.0
    }, {
        "name": "LGD 0:2 OG",
        "odds": 2.0
    },]
}
```

example successful response data:
```json
{
    "id": 1,
    "name": "2018 TI8淘汰赛 LGD vs OG",
    "description": "TI8 上班赛区 LGD vs OG",
    "maximum_bet_options": 1,
    "end_time_for_bet": "2018-12-01T14:20:31.002Z",
    "time_for_payoff": "2018-12-09T14:20:31.002Z",
    "status": "draft",
    "options_slot": [{
        "id": 1,
        "name": "LGD 2:0 OG",
        "odds": 2.0
    }, {
        "id": 2,
        "name": "LGD 2:1 OG",
        "odds": 3.0
    }, {
        "id": 3,
        "name": "LGD 1:2 OG",
        "odds": 6.0
    }, {
        "id": 4,
        "name": "LGD 0:2 OG",
        "odds": 2.0
    },]
}
```

example failed response data
```json
{
    "error": "\'maximum_bet_options\' is bigger than \'options\' numbers"
}
```

### 删除盘口
**Role**: admin

**URL**: games/[id] or games/delete/[id]

**HTTP Verb**: DELETE or POST

**response**:
1. If the server successfully delete the game, the server should respond with
   "200 OK" along with an optional message;
2. If the server reject to delete the game, the server should respond with
   "400 Bad Request" along with a message describing the problem;
3. The server should reject deleting games with status marked as "open", "close
   for bets", "paying off", "paid off";
4. The server should remove the related options fields;

example successful response data
```json
{
    "message": "game deleted"
}
```

example failed response data
```json
{
    "error": "the games marked as \'open\' can not be deleted"
}
```


### 读取盘口
**Role**: admin, user

**URL**: games/, games/[id]

**Queries**:
1. status: possible value are "draft", "published", "open", "closed",
   "closedforbets", "payingoff", "paidoff";
2. page, perpage: paginated resources, optional at first;
3. allow_multiple_bets: games allowed for multiple bets;
4. endtime: games before a specific time

**Admin Only fields**: *enrolled*

**HTTP Verb**: GET

**response**:
1. The server should respond with a list of games according to the query
   information;
2. The server should respond with a single game when accessing a specific game;
3. The server should reject non admin user to access "draft" games;
4. The server should respond with "404 Not Found" when there is no game for a
   certain criteria;

### 更新盘口

### 预览盘口（前端）

### 公开盘口

### 开盘和关闭盘口

### 撤回开盘（优先级：低)

### 参与投注

### 撤回投注

### 确定结果

### 结算流程和结束
