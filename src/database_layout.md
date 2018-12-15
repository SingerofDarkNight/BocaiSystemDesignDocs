1. games

   | Name                | Type       | Description                            |
   | ------------------- | ---------- | -------------------------------------- |
   | id                  | int32      | 主键                                   |
   | name                | char(80)   | 盘口名称                               |
   | description         | vchar(512) | 详细的说明                             |
   | normal_user_visible | boolean    | 普通用户是否可见                       |
   | status              | tinyint    | 盘口的状态                             |
   | maximum_bet_options | tinyint    | 是否允许投注多个选项，default value为1 |
   | bet_money_least     | int32      | 最小投注                               |
   | bet_money_highest   | int32      | 最大投注                               |
   | end_time_ms         | int64      | 截至投注时间                           |
   | enrolled            | uint32     | 参与本盘口的计数器                     |
2. betting_options

   | Name    | Type        | Description                     |
   | ------- | ----------- | ------------------------------- |
   | Id      | int32       | 主键                            |
   | game_id | foreign key | 盘口的外键                      |
   | name    | char(40)    | 选项描述/名称                   |
   | odds    | float       | 赔率                            |
   | winning | boolean     | 投注选项是否获胜，默认值为false |

3. bets

   | Name              | Type        | Description |
   | ----------------- | ----------- | ----------- |
   | id                | int32       | 主键        |
   | user_id           | foreign key | 用户的外键  |
   | betting_option_id | foreign key | 投注的外键  |
   | money             | int32       | 投注数量    |
   | created           | datetme     | 投注的时间  |

4. paidoff_bets

   | Name              | Type        | Description       |
   | ----------------- | ----------- | ----------------- |
   | id                | int32       | 主键              |
   | user_id           | foreign key | 用户的外键        |
   | betting_option_id | foreign key | 投注的外键        |
   | money             | int32       | 投注数量          |
   | earning           | int32       | 进账数量，默认为0 |
   | created           | datetme     | 投注的时间        |


<!-- TODO: tables needed from discuz -->
