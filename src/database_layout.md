1. games

   | Name             | Type        | Description                            |
   | ---------------- | ----------- | -------------------------------------- |
   | id               | int32       | 主键                                   |
   | name             | char(80)    | 盘口名称                               |
   | description      | vchar(512)  | 详细的说明                             |
   | max_bet_options  | tinyint     | 是否允许投注多个选项，default value为1 |
   | status           | tinyint     | 盘口的状态                             |
   | bet_min          | int32       | 最小投注                               |
   | bet_max          | int32       | 最大投注                               |
   | endtime_for_bet  | datetime    | 截至投注时间                           |
   | winningoption_id | foreign key | 盘口结果的外键                         |
   | enrolled         | uint32      | 参与本盘口的计数器                     |
2. betting_options

   | Name    | Type        | Description   |
   | ------- | ----------- | ------------- |
   | Id      | Int32       | 主键          |
   | game_id | foreign key | 盘口的外键    |
   | name    | char(40)    | 选项描述/名称 |
   | odds    | float       | 赔率          |

3. bets

   | Name              | Type        | Description |
   | ----------------- | ----------- | ----------- |
   | id                | int32       | 主键        |
   | user_id           | foreign key | 用户的外键  |
   | betting_option_id | foreign key | 投注的外键  |
   | betted            | int32       | 投注数量    |
   | created           | datetme     | 投注的时间  |

4. paidoff_bets

   | Name              | Type        | Description       |
   | ----------------- | ----------- | ----------------- |
   | id                | int32       | 主键              |
   | user_id           | foreign key | 用户的外键        |
   | betting_option_id | foreign key | 投注的外键        |
   | betted            | int32       | 投注数量          |
   | earning           | int32       | 进账数量，默认为0 |
   | created           | datetme     | 投注的时间        |

5. user_info

   | Name           | Type        | Description      |
   | -------------- | ----------- | ---------------- |
   | user_id        | foreign key | 用户外键         |
   | enrolled       | uint32      | 参与过的盘口数量 |
   | wons           | uint32      | 赢过的次数       |
   | lost           | uint32      | 输掉的次数       |
   | credits_earned | uint32      | 总共赢了多少     |
   | credits_lost   | uint32      | 总共输了多少     |

<!-- TODO: tables needed from discuz -->
