dev1
- 修复巨人投掷边界条件
- 修复小鬼判定用纵坐标的计算错误
- 输出巨人坐标保留三位小数向下取整
- 修复恢复原速问题，包括巨人投掷中恢复原速、小鬼落地恢复原速、小鬼恢复原速对啃食的影响

dev2
- 接入分布计算器（调试模式）
- 冰时机按照avz基准
        iceable = Some(tick);
        .filter(|&&v| v > 0 && v <= cob_time)
        (Some(last_ice_time), cob_time) => ICE_SLOW_TOTAL_TIME - cob_time + last_ice_time - 1,

dev3
- 合并表达式输入

dev4
- imp支持屋顶，并且使用了精度更高的数据

dev5
- 支持计算投掷区间小鬼的巨人横坐标范围
- 支持计算特定坐标巨人投掷的小鬼横坐标范围
- 核拦截输出的啃食时机为真实啃食时机(avz基准时机) 
        Eat shift_to_plant_intercept 
- 修复屋顶400-680坐标范围巨人投出小鬼的初始化问题


t冰 
- [1, t): t - 1 原速
- [t, t + 399): 399 冻结
- [t + 399, t + 1999): 1999 - 399 减速 
- [t + 1999, now]: now - t - 1999 + 1

last_ice_time                   2000 -> 1999
cob_time                        2000 - (cob_time - last_ice_time) -> [1999 - (cob_time - last_ice_time)] = iced
cob_time + 1                    2000 - (cob_time - last_ice_time) - 1 -> 1999 - (cob_time - last_ice_time) - 1
cob_time + 1                    巨人进status投掷，开始投掷
cob_time + imp_spawn_time       动画循环率更新到满足条件imp_spawn_time = 105 or 210
cob_time + imp_spawn_time + 1   iced - imp_spawn_time -> iced - imp_spawn_time - 1
                                imp出生