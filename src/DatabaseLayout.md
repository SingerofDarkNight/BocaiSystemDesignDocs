# 数据库布局

本文档描述了菠菜系统基本的数据库布局。此文档可能并不完全。如果遇到需要更多表和字段，请自行添加。如果遇到数据表和字段的名称不可用，请自行修改。

## Details
1. 用户数据
> users
> - user_id (用户id，和论坛id匹配)
> - lumbers (代币)
> - follows (关注的盘口计数器)
> - enrolled (参与过的计数器)
> - wons (赢过的计数器)
> - lost (输掉的计数器)
> - lumbers_earned (赢得的代币的总和)
> - lumbers_lost (输掉的代币的总和)
> - timestamps (时间戳，可以有created_at和updated_at, 没有需要可不添加)

2. 系列赛(optional)
> tournaments
> - id (主键)
> - name (系列赛的名称，如2018megafon冬季冲突赛)
> - timestamps (时间戳，可以有created_at和updated_at, 没有需要可不添加)

3. 具体的盘口
> games
> - id (主键)
> - tournament_id (系列赛的外键，optional)
> - winning_slot_id (盘口结果的外键)
> - name (盘口名称，如小组赛LGD vs VG。没有tournament_id时，填写完整名称)
> - description (详细的说明)
> - maximum_bet_slots (是否允许投注多个选项, 推荐integer类型，default value为1)
> - end_time_for_bet (时间戳，停止投注的时间)
> - time_for_payoff (时间戳，结算时间)
> - status (盘口的状态，如未开放，正在进行，正在结算，已结算)
> - enrolled(参与本盘口的计数器，一个投注算一次)
> - timestamps (时间戳，可以有created_at和updated_at, 没有需要可不添加)

4. 盘口投注的选项
> slots
> - id (主键)
> - game_id (盘口的外键)
> - name (名称，如LGD 2:0 VG、LGD胜)
> - odds (赔率，> 1)
> - timestamps (时间戳，可以有created_at和updated_at, 没有需要可不添加)

5. 未结算投注详情
> bets
> - id (主键)
> - user_id (用户id外键)
> - game_id (盘口外键)
> - slot_id (投注选项外键)
> - betted (投注金额)
> - timestamps (时间戳，可以有created_at和updated_at, 没有需要可不添加)

6. 已结算投注详情
> paidoff_bets
> - id (主键)
> - user_id (用户id外键)
> - game_id (盘口外键)
> - slot_id (投注选项外键)
> - betted (投注金额)
> - inout (是否有进账，boolean, default value为false)
> - lumbers (进账金额，推荐unsigned integer, default value为0)
> - timestamps (时间戳，可以有created_at和updated_at, 没有需要可不添加)

7. 关注的盘口
> follows
> - id (主键)
> - user_id (用户的外键)
> - game_id (盘口的外键)
> - timestamps (时间戳，可以有created_at和updated_at, 没有需要可不添加)

8. 评论
> comments
> - id (主键)
> - game_id (盘口的外键)
> - user_id (用户的外键)
> - content (评论内容)
> - timestamps (时间戳，可以有created_at和updated_at, 没有需要可不添加)

9. 短消息
> messages
> - id (主键)
> - from (短消息发出者外键)
> - to (短消息接收者外键)
> - content (短消息内容)
> - timestamps (时间戳，可以有created_at和updated_at, 没有需要可不添加)

10. 其他结算历史
> transaction_history
> - id (主键)
> - description (结算说明)
> - user_id (用户id外键)
> - inout (是否有进账，boolean, default value为false)
> - lumbers (进账金额，推荐unsigned integer, default value为0)
> - timestamps (时间戳，可以有created_at和updated_at, 没有需要可不添加)
