https://www.joinquant.com/help/api/help#name:api  

感谢您使用JoinQuant（聚宽）量化平台，以下内容主要介绍聚宽量化平台的API 使用方法，目录中带有"♠" 标识的API 是 "回测环境/模拟"的专用API，不  

# 支持在投资研究模块中调用。  

内容较多，可使用Ctrl+F 进行搜索。  

如果以下内容仍没有解决您的问题，请您查看常见问题、常见Bug 或者警告解决方法或者通过社区提问的方式告诉我们。此外您也可以通过在线客服免费咨询  

![](images/860904ead3644800958a7284b8cff47aaef26d0be27fb86060e9d58ebdf35770.jpg)  

# 开始写策略  

# 简单但是完整的策略  

先来看一个简单但是完整的策略:  

def initialize(context):  

# 定义一个全局变量, 保存要操作的股票  
g.security $=$ '000001.XSHE'  
# 运行函数  
run_daily(market_open, time $=$ 'every_bar')  

def market_open(context):  

if g.security not in context.portfolio.positions: order(g.security, 1000)   
else: order(g.security, -800)  

一个完整策略只需要两步:  

设置初始化函数: initialize,上面的例子中, 只操作一支股票:'000001.XSHE', 平安银行  

实现一个函数, 来根据历史数据调整仓位.  

这个策略里, 每当我们没有股票时就买入1000 股, 每当我们有股票时又卖出800 股, 具体的下单API 请看order 函数.  

这个策略里, 我们有了交易, 但是只是无意义的交易, 没有依据当前的数据做出合理的分析  

下面我们来看一个真正实用的策略  

# 实用的策略  

在这个策略里, 我们会根据历史价格做出判断:  

如果上一时间点价格高出五天平均价 $1\%,$ 则全仓买入如果上一时间点价格低于五天平均价, 则空仓卖出  

# 导入聚宽函数库import jqdata  

# 初始化函数，设定要操作的股票、基准等等def initialize(context):# 定义一个全局变量, 保存要操作的股票# 000001(股票:平安银行)g.security $=$ '000001.XSHE'# 设定沪深300 作为基准set_benchmark('000300.XSHG')# 开启动态复权模式(真实价格)set_option('use_real_price', True)# 运行函数run_daily(market_open, time $=$ 'every_bar')  

# 每个单位时间(如果按天回测,则每天调用一次,如果按分钟,则每分钟调用一次)调用一次  

def market_open(context): security $=$ g.security # 获取股票的收盘价  

close_data $=$ attribute_history(security, 5, '1d', ['close'])  

MA5 $=$ close_data['close'].mean()   
# 取得上一时间点价格   
current_price $=$ close_data['close'][-1]   
# 取得当前的现金   
cash $=$ context.portfolio.available_cash  

# 如果上一时间点价格高出五天平均价 $\underline{{1}}\%$ , 则全仓买入if current_price > 1.01\*MA5:# 用所有 cash 买入股票order_value(security, cash)# 记录这次买入log.info("Buying %s" % (security))  

# 如果上一时间点价格低于五天平均价, 则空仓卖出  

elif current_price < MA5 and context.portfolio.positions[security].closeable_amount > 0:  

# 卖出所有股票,使这只股票的最终持有量为0 order_target(security, 0)   
# 记录这次卖出   
log.info("Selling %s" % (security))  

# 画出上一时间点价格record(stock_price=current_price)  

# 策略引擎介绍  

# 安全  

1. 保证您的策略安全是我们的第一要务  

2. 在您使用我们网站的过程中, 我们全程使用https 传输  

3. 策略会加密存储在数据库  

4. 请不要在其他非聚宽平台登录聚宽账号。  

5. 回测时您的策略会在一个安全的进程中执行, 我们使用了进程隔离的方案来确保系统不会被任何用户的代码攻击, 每个用户的代码都运行在一个有很强限制的进程中:  

只能读指定的一些python 库文件  

不能写和执行任何文件, 如果您需要保存和读取私有文件, 请看  

write_file/read_file  

限制了cpu 和内存, 堆栈的使用，当使用多核时，回测耗时按CPU 占用耗时计算  

可以访问网络, 但是对带宽做了限制, 下载最大带宽为500Kbps, 上传带宽为10Kbps  

有严格的超时机制, 如果handle_data 超过30 分钟则立即停止运行 对于读取回测所需要的数据, 和输出回测结果, 我们使用一个辅助进程来帮它完成, 两者之间通过管道连接.  

我们使用了linux 内核级别的apparmer 技术来实现这一点. 有了这些限制我们确保了任何用户不能侵入我们的系统, 更别提盗取他人的策略了.  

# 数据  

1. 股票数据：我们拥有所有A 股上市公司2005 年以来的股票行情数据、财务数据、上市公司基本信息、融资融券信息等。为了避免幸存者偏差，我们包括了已经退市的股票数据。其中volume（成交量）字段单位是股。  

2. 基金数据：我们目前提供了600 多种在交易所上市的基金的行情、净值等数据，包含ETF、LOF、分级A/B 基金以及货币基金的完整的行情、净值数据等，请点击基金数据查看。  

3. 金融期货数据：我们提供中金所推出的所有金融期货产品的行情数据，并包含历史产品的数据。  

4. 股票指数：我们支持近600 种指数数据，包括指数的行情数据以及成分股数据。为了避免未来函数，我们支持获取历史任意时刻的指数成分股信息，具体见get_index_stocks。  

5. 行业板块：我们支持按行业、按板块选股，具体见get_industry_stocks  

6. 概念板块：我们支持按概念板块选股，具体见get_concept_stocks  

7. 所有的行情数据我们均已处理好前复权信息。  

8. 我们当日的回测数据会在收盘后通过多数据源进行校验，并在 $\mathsf{T}+\mathsf{1}$ （第二天）的00:01 更新。  

9. 我们提供的所有行情K 线数据为后对齐，标识K 线的时间为数据的结束时间。在一分钟K 线上，没有09:30，从09:31 开始，有15:00 的K 线，共计240 根。表示时间为09:31 的一分钟K 线，其数据时间为09:25:00\~09:30:59，这一分钟的开盘价是09:25 的集合竞价的价格。  

10. 期货K 线的划分方式：将标的当天的开盘时间到收盘时间的日历时间按照划分单位划分区间，然后将同一个区间的分钟bar 合并。例如，某个标的的开盘时间为09:30,收盘时间为15:00，然后划分单位为5m，划分bar 的逻辑如下：将09:30-15:00 按照5m 划分区间，然后将这个标当天行情在同一个区间的分钟bar 合并。  

# 运行频率  

聚宽支持天、分钟及tick 频率，其他频率您可以在此基础上自己根据时间判断，有关运行频率解析及隔固定时间运行方法请点击查看，下面是运行频率的详细说明。  

# 1. Bar 的概念  

在一定时间段内的时间序列就构成了一根 K 线（日本蜡烛图），单根 K 线被称为 Bar。  

如果是一分钟内的 Tick 序列，即构成一根分钟 K 线，又称分钟 Bar;如果是一天内的分钟序列，即构成一根日线 K 线，又称日线 Bar;Bar 的示意图如下所示：  

![](images/ea341a8f533ff2c44d874b5796558970816067829fb1940e1d9e0c42d57a88bd.jpg)  
Bar示意图  

Bar 就是时间维度上，价格在空间维度上变化构成的数据单元。如下图所示，多个数据单元 Bar 构成的一个时间序列。  

K线序列（Bar序列）  

![](images/90b4c5bb7891c6f597fa79f284b044063384ff09253846b5be391bb44e3e5712.jpg)  

# 2. 频率详解  

下列图片中齿轮为 handle_data(context, data) 的运行时间，  

before_trading_start(context) 等其他函数运行时间详见相关API。  

# 频率：天  

当选择天频率时， 算法在每根日线 Bar 都会运行一次，即每天运行一次。  
在算法中，可以获取任何粒度的数据。  

![](images/8d081f4fb065b752359ace49ddf86acee67d68e96ee9514b0a69bc134b85b316.jpg)  
日K线（Bar序列）  

# 频率：分钟  

当选择分钟频率时， 算法在每根分钟 Bar 都会运行一次，即每分钟运行一次。  

在算法中，可以获取任何粒度的数据。  

# 分钟K线（Bar序列）  

![](images/b2751c77ff0f547fecfb881e3e4b09b13d3f09ad761301b781add544f1107aa7.jpg)  

频率：Tick  

当选择 Tick 频率时，每当新来一个 Tick，算法都会被执行一次。  

执行示意图如下图所示：  

Tick序列  

![](images/ca49b6b456e93c8aed1d9d1c1c84da68a2c321503975ddf2d4550209eefbe6eb.jpg)  

# 运行时间  

设置您的策略什么时候运行，主要由设置策略频率（天、分钟或者tick）与控制策略运行时间的API 共同完成  

开盘前(9:00)运行:  

run_monthly/run_weekly/run_daily 中指定tim $e\mathrm{=}\ '09\mathrm{:}00^{\prime}$ 运行的函   
数   
before_trading_start  

盘中运行:  

run_monthly/run_weekly/run_daily 中在指定交易时间执行的函数, 执行时间为这分钟的第一秒. 例如: run_daily(func,'14:50') 会在每天的14:50:00(精确到秒)执行o handle_data  

按日回测/模拟, 在9:30:00(精确到秒)运行, data 为昨天的天数据  
按分钟回测/模拟, 在每分钟的第一秒运行, 每天执行240次, 不包括11:30 和15:00 这两分钟, data 是上一分钟的分钟数据. 例如: 当天第一次执行是在9:30:00, data 是昨天14:59 至15:00 这一分钟的分钟数据, 当天最后一次执行是在14:59:00, data 是14:58 至14:59:00 这一分钟的分钟数据.  

收盘后(15:00 后半小时内)运行:  

run_monthly/run_weekly/run_daily 中指定t $i m e{=}^{\prime}15{:}30^{\prime}$ 运行的函  
数  
after_trading_end  

同一个时间点, 总是先运行 run_xxx 指定的函数, 然后是 before_trading_start , handle_data 和 after_trading_endo 为了避免您换算错误，建议设置time 为具体的时间（例如：time='9:30'）;run_xxx 指run_monthly/run_weekly/run_daily 中的任意一个  

run_xxx 指定的函数只能有一个参数 context, data 不再提供, 请使用 history 等获取;initialize / before_trading_start / after_trading_end / handle_data都是可选的, 如果不是必须的, 不要实现这些函数, 一个空函数会降低运行速度;o run_xxx 和handle_data 不要在同一个策略中使用，建议使用run_xxxx;一个策略中可以写多个run_xxx 函数，例如需要每分钟运行和定时运行的话，可以这样设置：  

## func1, func2, func3 都是您自己实现的函数  

# 每分钟运行 run_daily(func1, time $=1$ every_bar') # 11:00 定时运行 run_daily(func2, time='11:00') # 14:00 定时运行 • run_daily(func3, time='14:00') # 14:50 定时运行 run_daily(func2, time='14:50')  

# 订单处理  

# 订单处理总体过程：  

从委托到成交的流程:  
订单创建->订单检查- $->$ 报单 $->$ 确认委托- $\cdot>$ 撮合，在订单检查时未通过则订单取消；  
回测模式整个过程是同步进行，order_\*函数执行成功后会创建一个order 对象,市价单的order 对象撮合后(交易时间下单立即撮合)会立即获得交易的结果,限价单的order 对象每次成交后都会立即更新；  
目前官网的模拟盘过程同回测；  

所有未完成订单将在本交易日结束后撤销。  

<html><body><table><tr><td>运行 频率</td><td>委托 类型</td><td>关闭盘口撮合</td><td>启用盘口撮合</td></tr><tr><td>天</td><td>市价 单</td><td>按最新价+滑点撮合</td><td>按盘口撮合</td></tr><tr><td></td><td>限价 单</td><td>下单时尝试按最新价+滑点撮 合，剩余部分挂单每分钟尝试按 分钟 Bar 撮合</td><td>下单时按盘口撮合，剩余 部分挂单每分钟尝试按分 钟 Bar 撮合</td></tr><tr><td>分钟</td><td>市价 单</td><td>按最新价+滑点撮合</td><td>按盘口撮合</td></tr><tr><td></td><td>限价 单</td><td>下单时尝试按最新价+滑点撮 合，剩余部分挂单每分钟尝试按 分钟 Bar 撮合</td><td>下单时按盘口撮合，剩余 部分挂单每分钟尝试按分 钟 Bar 撮合</td></tr><tr><td>tick</td><td>市价 单</td><td>按最新价+滑点撮合</td><td>按盘口撮合</td></tr><tr><td></td><td>限价 单 撮合</td><td>下单时尝试按最新价+滑点撮 合，剩余部分挂单每 tick按 tick</td><td>下单时按盘口撮合，剩余 部分挂单每tick按tick撮 合</td></tr></table></body></html>  

# 撮合流程  

在回测和模拟交易中，所有的委托（无论市价单还是限价单）在下单后都将尝试进行撮合，撮合的逻辑根据是否打开盘口撮合进行选择；若委托未能完全成交且为限价单，则挂单，然后根据挂单撮合逻辑进行后续的流程。  

# 下单时的撮合逻辑  

•  当 “最新价 $^+$ 滑点” 在涨跌停范围内将尝试进行撮合，若满足以下条件则成交，成交价为最新价 $^+$ 滑点：o 买入/开多/平空时，委托价 $>=$ 最新价 $^+$ 滑点；o 卖出/开空/平多时，委托价 $<=$ 最新价-滑点；若标的“最新价 $^+$ 滑点”不低于涨停或者不高于跌停时：o 跌停时市价卖单会被撤销，涨停时市价买单会被撤销；o 限价单会挂单等待撮合。  
•  交易价格: 最新价 $^+$ 滑点，如果在开盘时刻运行， 最新价格为开盘价。 其他情况下， 为上一分钟的最后一个价格或上一个tick 的最新价。满足撮合条件时成交量的限制：o  回测：不超过当日总成交量 \* order_volume_ratio；o 模拟交易：全部成交；  
• 超出最大成交量的部分：o 对于市价单，剩余部分将撤单；o 对于限价单，将按委托价挂单，根据策略频率使用不同的后续逻辑。  

# 注意:  

回测中可通过选项 order_volume_ratio 设置每日最大的成交量, 例如:0.25 表示下单成交量不会超过本日成交量的 $25\%$ ；  

o  通过选项 order_volume_ratio 设置每日最大的成交量仅限制了每个订单的成交量, 虽然你可以通过多次下单来超过该限制, 但是为了对你的回测负责请不要这么做；context.portfolio 中的持仓价格会使用上一分钟的最后一个价格更新。  

# 启用盘口撮合时  

仅在模拟交易中可启用盘口撮合。  

根据对手盘盘口进行撮合；  

优先从一档（买一/卖一）开始撮合，根据成交量算出加权均价；  

盘口撮合不限制成交量；  

若无盘口数据，使用未启用盘口撮合时的逻辑尝试进行撮合；  

当盘口无法完全成交时：  

o 对于市价单，剩余部分将全部按最高一档盘口撮合；o 对于限价单，将按委托价挂单，根据策略频率使用不同的后续逻辑；  

若涨跌停时存在对手盘，则按盘口正常撮合；o 若没有对手盘，此时转入未启用盘口时的撮合逻辑：跌停时市价卖单会被撤销，涨停时市价买单会被撤销；限价单会挂单等待撮合。  

# 挂单时的撮合逻辑  

针对不同频率（天/分钟，tick）的策略，挂单的限价单将有以下撮合逻辑  

# 按分钟Bar 撮合  

天/分钟频率的策略，挂单的限价单每分钟都将尝试在本分钟Bar 结束时按照Bar 信息尝试进行撮合，若满足以下条件则成交，成交价为委托价：买入/开多/平空时，委托价 $>$ Bar 的最低价；o 卖出/开空/平多时，委托价 $<$ Bar 的最高价；  
•  成交量限制：o 模拟交易中不超过本分钟Bar 成交量；o  回测中不超过本分钟Bar 成交量 \* order_volume_ratio；  

• 若订单未完全成交，剩余部分将在每个分钟bar 结束时继续尝试撮合直到全部成交或收盘；  

# 按tick 撮合  

挂单的限价单每个tick 都将尝试在tick 结束时按照tick 信息尝试进行撮合，若满足以下条件则成交，成交价为委托价：  

买入/开多/平空时，若委托价 $>$ tick 的最新价，则进行撮合；卖出/开空/平多时，若委托价 $<$ tick 的最新价，则进行撮合；成交量限制：按tick 撮合时不检查成交量，当出现满足撮合条件的价格后，剩余部分全部以委托价成交。  

# 非交易时段下单的特别说明  

如果非交易时间下单且不撮合，不管是市价单还是限价单，都会挂单  
对于日频级策略，会在开盘时尝试进行撮合；对于分钟或者tick 频率的  
策略，会在下一个分钟bar 或者tick 完成时尝试撮合  
市价单挂单后开始交易时会按照下单时的逻辑撮合，限价单按照  
bar/tick 来撮合  
如果用户在 11:30:01 下单，那么订单挂单，引擎退出；下午开盘前引  
擎恢复运行时，账户初始化会定位未完成订单的对应频率的数据，如果  
是tick，可能会影响用户的tick 订阅数量  

# 下单和挂单，合的关系：  

下单：瞬间行为  
挂单：订单的状态，非交易时间下单则挂单至开盘，限价单  
不成交则挂单等待下次提合  
提合：订单处理的瞬间行为，一个订单可能分多次成交  

![](images/f32c8fd4efa3986f54ceec402faa7641dbed031de8bd8a04adad1f781fa96819.jpg)  

# 拆分合并与分红  

传统前复权回测模式：当股票发生拆分，合并或者分红时，股票价格会受到影响，为了保证价格的连续性, 我们使用前复权来处理之前的股票价格，给您的所有股票价格已经是前复权的价格。真实价格（动态复权）回测模式：当股票发生拆分，合并或者分红时，会按照历史情况，对账户进行处理，会在账户账户中增加现金或持股数量发生变化，并会有日志提示。  

内容  

传统前复权回测模式 与 真实价格（动态复权）回测模式 区别使用前复权价格，不论回测开始时间、结束时间是何时，使用的数据都是基于今天（回测当天）或某个时间的复权因子进行前复权获得的价格，因此使用前复权价格进行回测，回测结果肯定有问题。示意图如下：  

前复权时间轴历史时刻2图1传统前复权回测模式  

不论历史时刻1 或历史时刻2，拿到的数据都是基于未来某一天的前复权价格，使用这样的数据存在未来函数（未来函数是回测最大的敌人之一）  

![](images/8b705f77b9a628e494478ec03be76256ca3b5ef437429de8e10f82dbf0004bad.jpg)  

图2使用真实价格回测模式  

使用真实价格回测模式，回测到历史时刻1，使用历史时刻1 的真实价格撮合成交；如果需要复权，会使用的历史时刻1 的复权因子，对“历史时刻1"之前的价格进行前复权，这样有效避免了未来函数，因为回测全程都不可能使用未来的数据。  

你可能没有看懂，下面举个例子：  

# 股价：8  

![](images/5f3d24da750cfcd8ab1cd95bbc3f646212fd107a5326a7b552d19799989eee4e.jpg)  

# 时间轴  

历史时刻3 历史时刻2 历史时刻1如现有一只股票，股价一直没有波动，只进行了拆分。  

前复权回测模式  

站在“历史时刻 $3\,^{\bullet}$ 看历史数据：因为使用今天的复权因子，“历史时刻 $3\,^{\circ}$ 之前的股价均为2；o 站在“历史时刻 $2\,^{,}$ 看历史数据：因为使用今天的复权因子，“历史时刻3”的股价是2；站在“历史时刻1”看历史数据，因为使用今天的复权因子，“历史时刻 $2\,^{,}$ 和“历史时刻3”的股价是2；  

真实价格回测模式  

o 站在“历史时刻 $3\,^{\bullet}$ 看历史数据：因为使用历史时刻3 的复权因子，“历史时刻3”之前的股价均为8  
o 站在“历史时刻2”看历史数据：因为使用历史时刻2 的复权因子，“历史时刻3”的股价是4；  
o 站在“历史时刻1”看历史数据：因为使用历史时刻1 的复权因子，“历史时刻2”和“历史时刻3”的股价是2；  

因为使用了未来的复权因子，前复权回测模式，回测过程中使用的价格是不正确的。  

下面再举一个真实的例子，比较一下前复权回测模式和真实价格回测模式的区别  

![](images/f232271b4a79cacc3e520abd688ef8707059c56a77e969e5a9b657095c97fdcb.jpg)  

2007-01-30，波导股份的真实股价（绿色曲线）是低于格力电器（黑色曲线）的；但使用前复权价格，波导股份的价格会高于格力电器。 采用最简单的交易思路，购买股价低的股票并持有，前复权模式会买入格力电器，真实价格回测模式会买入波导股份。  

下面我们进行回测，根据2007-01-30 当天格力电器与波导股份的收盘价，买入低价位股票并持有到现在。回测结果如下所示：  

前复权回测模式的回测结果： 初始资金：100,000 策略收益： $776.\,54\%$ 沪深300 收益：21. $98\%$ 最大回撤： $64.\,98\%$  

![](images/c4dfef7ec115432ebf96990c0dd81ab6d56aad25586b0aaa5904501f6c017c09.jpg)  

# 日志  

2007-01-3109:20：60-INF0-关闭oinQuant真实价格回测模式：启用传统前复积回测视式  
2007-01-3109:30:09-INF0-2007-01-31日交5230下:  
2007-01-3169:30：e0-INF0-格力电器作日收盘价：2.21，波导展份昨日收盘价：4.46，  
2007-01-9109:90:00-INF0-买入股票：000651.XSHE格力电器  

真实价格回测模式的回测结果： 初始资金：100,000 策略收益： $78.\,35\%$ 沪深300 收益： $21.\,98\%$ 最大回撤： $79.\ 78\%$  

![](images/f4c454c7725386d1d3bf9327a05f8b70e79f903d85be1ce7701ed530e67dc074.jpg)  

# 日志 错误  

87-01-31091200 TNFO 开启3oinQuant真实价格回别模式国 91 09：30:00-1NF0-2007-01-31日交易记录如下：  
2807-01-3109:30:00-1NF0-格力电器昨日收盘价：18.7，波导股份昨日收盘价：4.44，09:30:00 TNFO 买入股票：600130.XSHG波导股份  

由回测结果不难看出，前复权回测模式因为存在未来函数，结果是不准确的，使用前复权回测模式可能会让你获得非常高的收益，但实盘时，效果却非常一般；在某些策略中，如使用到价格因子，前复权模式会导致回测中买卖信号与实际中不一致，从而导致回测结果不准确，影响策略在真实场景中的应用。  

开启真实价格回测功能其实很简单，只需一步即可搞定：  

在initialize 中使用set_option 即可，如下所示：  

def initialize(context):  

set_option('use_real_price', True)是否开启动态复权(真实价格)模式对模拟交易的影响近来，很多用户反馈在模拟盘看到的有些股票价格与在炒股软件上看到的不一样，对此表示很疑惑。  

这是因为在模拟交易中，在未开启动态复权(真实价格)模式时，我们是使用基于模拟交易创建日期的后复权价格。  
后复权模式示意图如下图所示：  

![](images/8f094aa1e283968662f0f79c5babf3c7f2000a29897113a2ac589140ece10c3b.jpg)  

# 图1未使用动态复权（真实价格）模式  

不开启真实价格模拟盘的运算结果是没有错误，只是会让您理解起来更费劲一些。  

用户如果想知道今天的真实价格，还需知道模拟创建的日期，并进行复权计算。  

为了让用户使用更便于理解、更真实的模拟系统，我们强烈建议您开启动态复权(真实价格)模式。开启方式：用户可在代码中调用  
set_option('use_real_price', True).  
开启动态复权(真实价格)模式示意图如下图所示：  

![](images/510ef088d238f72cc68294a028b3835d714413bb9b5f9d91643e47a6f2de644c.jpg)  

开启动态复权(真实)模式后，您看到的价格都是最新的，每到新的一天, 如果持仓中有股票发生了拆合或者分红或者其他可能影响复权因子的情形, 我们会根据复权因子自动调整股票的数量. 但不要跨日期缓存这些 API 返回的结果  

# 我们强烈建议您开启动态复权(真实价格)模式，进行模拟与回测！  

# 注意：  

1. 开启真实价格回测之后，为了让编写代码简单, 通过history/attribute_history/get_price/SecurityUnitData.mavg/vwap等 API 拿到的都是基于当天日期的前复权价格. 另一方面, 你在不同日期调用history/attribute_history/get_price/SecurityUnitData.mavg/vwap返回的价格可能是不一样的, 因为我们在不同日期看到的前复权价格是不一样的. 所以不要跨日期缓存这些 API 返回的结果.  
2. 每到新的一天, 如果持仓中有股票发生了拆合或者分红或者其他可能影响复权因子的情形, 我们会根据复权因子自动调整股票的数量, 如果调整后的数量是小数, 则向下取整到整数, 最后为了保证context.portfolio.total_value 不变,context.portfolio.available_cash 可能有略微调整.  

# 股息红利税的计算  

# 真实的税率计算方式如下：  

分红派息的时候，不扣税；  
等你卖出该只股票时，会根据你的股票持有时间（自你买进之日，算到你卖出之日的前一天，下同）超过一年的免税。2015 年9 月之前的政策是，满一年的收 $5\%$ 。现在执行的是,2015 年9 月份的新优惠政策：满一年的免税；  
等你卖出股票时，你的持有时间在1 个月以内（含1 个月）的，补交红利的 $20\%$ 税款，券商会在你卖出股票当日清算时直接扣收；  
等你卖出股票时，你的持有时间在1 个月至1 年间（含1 年）的，补交红利的10%税款，券商直接扣；  

分次买入的股票，一律按照“先进先出”原则，对应计算持股时间；  

• 当日有买进卖出的（即所谓做盘中 $\mathsf{T}\!+\!0$ ），收盘后系统计算你当日净额，净额为买入，则记录为今日新买入。净额为卖出，则按照先进先出原则，算成你卖出了你最早买入的对应数量持股，并考虑是否扣税和税率问题。  

在回测及模拟交易中，由于需要在分红当天将扣税后的分红现金发放到账户，因此无法准确计算用户的持仓时间（不知道股票卖出时间），我们的计算方式是，统一按照 $20\%$ 的税率计算的。  

# 滑点  

在实战交易中，往往最终成交价和预期价格有一定偏差，因此我们加入了滑点模式来帮助您更好地模拟真实市场的表现，可以使用set_slippage 设置滑点。  

# 交易税费  

交易税费包含券商手续费和印花税。您可以通过set_order_cost 来设置具体的交易税费的参数。  

券商手续费  

中国A 股市场目前为双边收费，券商手续费系默认值为万分之三，即 $0.03\%$ ，最少5 元。  

印花税  

印花税对卖方单边征收，对买方不再征收，系统默认为千分之一，即 $0.1\%$ 。  

# 风险指标  

风险指标数据有利于您对策略进行一个客观的评价。  

注意: 无论是回测还是模拟, 所有风险指标(年化收益  

/alpha/beta/sharpe/max_drawdown 等指标)都只会每天于17:00 左右更新一次, 也只根据每天收盘后的收益计算, 并不考虑每天盘中的收益情况. 例外:  

分钟和TICK 模拟盘每分钟会更新策略收益和基准收益按天模拟盘每天开盘后和收盘后会更新策略收益和基准收益基准收益的计算起点取的是回测开始时间前一个交易日的收盘价  

那么可能会造成这种现象: 模拟时收益曲线中有回撤, 但是 max_drawdown 可  

能为0.  

# 名称 描述  

Total Returns 策略收益  
Total Annualized Returns 策略年化收益  
Alpha 阿尔法  
Beta 贝塔  
Sharpe 夏普比率  
Sortino 索提诺比率  
Information Ratio 信息比率  
Algorithm Volatility 策略波动率  
Benchmark Volatility 基准波动率  
Max Drawdown 最大回撤  
Downside Risk 下行波动率  
胜率 胜率 $(\%)$   
日胜率 日胜率 $(\%)$   
盈亏比 盈亏比  
AEI 日均超额收益  
超额收益最大回撤 超额收益最大回撤  
超额收益夏普比率 超额收益夏普比率  
超额收益 除法版超额收益率说明  
对数轴 对数轴说明  
对数轴上的超额收益 对数轴上的超额收益的计算方法  

# 回测环境  

1. 回测引擎可在Python2.7 与Python3.6 上运行,默认使用Python3.6。我们将在未来逐步停止对Python2.7 引擎的更新，强烈建议您使用Python3.6 开发策略。  

2. 我们支持所有的Python 标准库和部分常用第三方库, 具体请看: 研究和回测（模拟）中都支持哪些第三方Python 库. 另外您可以把.py 文件放在研究根目录, 回测中可以直接import, 具体请看: 自定义python 库  

3. 安全是平台的重中之重, 您的策略的运行也会受到一些限制, 具体请看: 安全  

# 回测过程  

1. 准备好您的策略, 选择要操作的股票池, 实现handle_data 函数  

2. 选定一个回测开始和结束日期, 选择初始资金、调仓间隔(每天还是每分钟), 开始回测  

3. 引擎根据您选择的股票池和日期, 取得股票数据, 然后每一天或者每一分钟调用一次您的handle_data 函数, 同时告诉您现金、持仓情况和股票在上一天或者分钟的数据. 在此函数中, 您还可以调用函数获取任何多天的历史数据, 然后做出调仓决定.  

4. 当您下单后, 我们会根据接下来时间的实际交易情况, 处理您的订单. 具体细节参见订单处理  

5. 下单后您可以调用get_open_orders 取得所有未完成的订单, 调用cancel_order 取消订单  

6. 您可以在handle_data 里面调用record()函数记录某些数据, 我们会以图表的方式显示在回测结果页面  

7. 您可以在任何时候调用log.info/debug/warn/error 函数来打印一些日志8. 回测结束后我们会画出您的收益和基准(参见set_benchmark)收益的曲线, 列出每日持仓,每日交易和一系列风险数据。  

# 模拟盘注意事项  

模拟交易是根据回测的策略创建的，因此需要先回测，再创建模拟交易，如何创建模拟交易？  

• 为了避免以不合理的价格对标的进行下单，模拟盘在下单时会检查开盘（例如股票为9:25）到下单时刻的累积成交量，若为0 则会拒绝，提示：WARNING - 该标的截至到目前成交量为0 ，暂时无法成交。  

模拟盘中因尽量避免在距离开盘时间较早的时间点进行下单, 比如9 点以前对股票下单，可能导致当时还没有拿到涨跌停价而产生比较异常的委托甚至委托失败。  

在日级模拟中使用时，使用handle_data 或者run_daily 中time $=^{\prime}9{\cdot}30^{\prime}$ ，策略的实际运行时间是9:27\~9:30 之间；股指期货在 $9{:}27{\sim}9{:}30$ 之间有可能没有产生集合竞价，会出现9:30 下单提示该标的截至到目前成交量为0，可以忽略或者在9:31 及之后运行；  

模拟盘在每天运行结束后会保存状态, 结束进程(相当于休眠). 然后在第二天恢复.  

进程结束时会保存这些状态:  

o 用户账户, 持仓使用 pickle 保存 g 对象. 注意g 中以 '__' 开头的变量将被忽略, 不会被保存g 中不能序列化的变量不会被保存, 重启后会不存在. 如果你写了如下的代码:  

o def initialize(context):  

g.query $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ query(valuation)  

g 将不能被保存, 因为 query() 返回的对象并不能被持久化. 重启后也不会再执行 initialize, 使用 g.query 将会抛出 AttributeError 异常。正确的做法是,在 process_initialize 中初始化它, 并且名字以 '__' 开头.  

o def process_initialize(context):  

g.__query $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ query(valuation)  

注意: 涉及到IO(打开的文件, 网络连接, 数据库连接)的对  
象是不能被序列化的:query(valuation) : 数据库连接open("some/path") : 打开的文件requests.get('') : 网络连接  

使用 pickle 保存 context 对象, 处理方式跟 g 一样o 为了防止恶意攻击, 序列化之后的状态大小不能超过 30M, 如果超出将在保存状态时运行失败. 当超过 20M 时日志中会有警告提示, 请注意日志.  

恢复过程是这样的:  

1. 加载策略代码, 因为python 是动态语言, 编译即运行, 所以全局的(在函数外写的)代码会被执行一遍.  

2. 使用保存的状态恢复 g, context, 和函数外定义的全局变量.  
3. 如果策略代码和上一次运行时发生了修改，而且代码中定义了after_code_changed 函数，则会运行after_code_changed(#after_code_changed) 函数。  

4.  执行 process_initialize, 每次启动时都会执行这个函数.  

重启后不再执行 initialize 函数, initialize 函数在整个模拟盘的生命周期中只执行一次. 即使是更改回测后, initialize 也不会执行.  

模拟盘更改回测之后上述的全局变量(包括 g 和 context 中保存的)不会丢失. 新代码中 initialize 不会执行. 如果需要修改原来的值, 可以在 after_code_changed 函数里面修改, 比如, 原来代码是:  

def initialize(context):  

g.stock $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ '000001.XSHE' 代码改成:  

def initialize(context):g.stock $=$ '000002.XSHE'  
执行时, g.stock 仍然是 '000001.XSHE', 要修改他们的值, 必须定  

# 义 after_code_changed:  

def after_code_changed(context): g.stock $=$ '000002.XSHE'  

创建模拟交易时, 如果选择的日期是今天, 则从今天当前时间点开始运行, 应该在当前时间点之前运行的函数不再运行. 比如: 今天10:00 创建了按天的模拟交易, 选择日期是今天, 代码中实现了 handle_data 和after_trading_end, 则 handle_data 今天不运行, 而 after_trading_end会在 15:30 运行  

当模拟交易在A 时间点失败后, 然后在B 时间点"重跑", 那么 A-B 之间的时间点应该运行的函数不再运行  

因为模拟盘资源有限, 为了防止用户创建之后长期搁置浪费资源, 我们做出如下限制: 如果一个模拟盘同时满足下面条件, 则暂缓运行:  

o 模拟盘所有者在最近一个月内没有访问过聚宽网站当用户重新使用网站后, 第二天会继续运行(会把之前的交易日执行一遍,并不会跳过日期)  

由于模拟盘资源有限及防止恶意攻击, 我们设置：（1）模拟交易序列化之后的状态大小不能超过 30M；（2）每个函数运行时间不能超过1800s；（3）进程占用内存不能超过3G。如果日志中出现这样的提示或者模拟交易因此提示而失败的话，请优化策略，具体的参考常见Bug 或者警告解决方法。  

强烈建议模拟盘使用真实价格成交, 即调  
用 set_option('use_real_price', True). 更多细节  
模拟交易替换代码参考教程  
替换代码时，版本模拟交易和回测的版本需要对应，python2(python3)  
版本的模拟交易不能使用python3(python2)版本的回测替换  

# 模拟交易和回测的差别  

比较的前提是策略、起始资金、时间区间及频率等完全一致。模拟交易现在和回测还是有些微小的差别, 具体原因如下:  

策略运行的环境如果不相同的话，可能导致不同，例如Python2 和Python3，聚宽官网和一创聚宽;  

策略中有随机因素，例如：使用随机数、不稳定的排序、遍历 dict 中的元素等；  
回测的策略使用了未来数据，例如开盘前获取当天的收盘价、财务数据、技术指标等；  
替换代码：回测不支持替换代码，模拟交易中间替换了代码，回测使用替换后的代码，导致策略不一致；  
暂停及重启策略：回测中不支持暂停，模拟交易可以暂停策略，暂停期间策略不运行；  

# 期货交割日  

期货持仓到交割日，没有手动交割，系统会以当天结算价平仓, 没有手续费, 不会有交易记录.  

# 还券细则  

$T+1,$ , 当日融的券当日不能还还券时要扣除利息直接还券时, 可以使用当日买入的券还(不受 $\mathsf{T}+\mathsf{\tau}^{\mathsf{\tau}}$ 限制), 且优先使用当日买入的券还  

# 投资组合优化器  

投资组合优化是指应用概率论与数理统计、最优化方法以及线性代数等相关数学理论方法，根据既定目标收益和风险容许程度（例如最大化收益，最小化风险，风险平价等），将投资重新组合，分散风险的过程，它体现了投资者的意愿和投资者所受到的约束，即在一定风险水平下收益最大化或一定收益水平下的风险最小化。  

投资组合管理者在设定了投资收益预期、风险预算、相关约束和风险模型之后， 依托优化器的快速计算优势，得到资产配置最优化结果。  

由于不同的约束条件、目标函数，会形成不同的优化器，优化器的处理结果依赖用户输入的相关信息，因此投资者对收益率的预期和风险模型本身估计的准确性，都会影响最终的分析结果，再考虑到交易成本等各类因素的影响，所以从用户使用上而言， 没有绝对意义上最好的优化器。对于资产组合优化问题，我们可以通过使用优化器，进行一个较长时间的回测，测试整个投资过程，在所有组合输入一致的情况下通过策略的绩效对比来看哪一个优化器有更好的表现， 或者更符合自己的需求。  

组合优化器支持对股票、基金进行投资优化，支持如下优化模型：  

MinVariance - 组合风险最小化（均值-方差优化）  
MaxProfit - 组合收益最大化  
MaxSharpeRatio - 组合夏普比率最大化  
MinTrackingError - 追踪误差最小化  
RiskParity - 风险平价  
MaxScore - 组合标的打分最大化  
MinScore - 组合标的打分最小化  
MaxFactorValue - 因子值最大化  
MinFactorValue - 因子值最小化  
自定义约束条件的优化模型  

对使用优化器的投资组合管理者来说，只需根据收益预期、风险预算，选择恰当的优化模型，并设定相关的约束限制条件。优化器程序可以基于选定的优化模型，输出优化后的投资权重调整建议。我们会对投资组合优化器的进行持续创新与改进。  

# 示例  

下面选出上证50 成分股的一部分与选定的ETF 基金进行组合构成股票池，设定不同的投资组合优化约束条件，并进行回测，测试投资组合优化器对整个投资的影响。  

模型1：等权重配置  

![](images/8cc6b36615578cc907d1accfe5b88a2fcd681c6707d243e53a3895796f382491.jpg)  

•  模型2：组合风险平价；股票的总权重限制为0 到 $90\%$ ，ETF 的总权重限制为0 到 $10\%$ ；每只标的权重不超过 $10\%$  

![](images/c472b94de911024e92840f7b0e92af6678d64babdb1682551d9f71afef9fd886.jpg)  

• 模型3：组合风险最小化（最小化组合方差）；组合总权重限制为 $90\%$ 到 $100\%$ ；组合年化收益率目标下限为 $10\%$  

![](images/ad80dfae33c785bade77b0785cf3263185a0d9e8b8ddca4e272f17809176a709.jpg)  

•  模型4：'人气指标5 日均值'最大化；组合年化收益率目标下限为  

$10\%$ ；每只标的权重不超过 $\mathbf{20\%}$ 模型5：组合夏普比率最大化；每只标的权重不超过 $10\%$ 回测代码如下, 优化函数API 详情见 portfolio_optimizer - 投资组合优化：  

![](images/6f26d08900549de3bca3a9017a39301c6ea0f4d3576d86a0c43901b3d550ef43.jpg)  

![](images/ef0b096248fdde9a5d64d23caf6e635985196730383c31ce24452a2be06bfde7.jpg)  

# 导入函数库  

import pandas as pdfrom jqdata import $\star$ from jqfactor import Factorfrom jqlib.optimizer import \*# 初始化函数，设定基准等等def initialize(context):# 设定沪深300 作为基准set_benchmark('000300.XSHG')# 开启动态复权模式(真实价格)set_option('use_real_price', True)  

# 过滤掉order 系列API 产生的比error 级别低的log# log.set_level('order', 'error')  

### 股票相关设定 ### # 股票类每笔交易时的手续费是：买入时佣金万分之三，卖出时佣金万分   
之三加千分之一印花税, 每笔交易佣金最低扣5 块钱 set_order_cost(OrderCost(close_ta $\mathbf{\Delta}\times=\odot.\,\odot\odot1$ ,   
open_commission $=\odot$ .0003, close_commission $=\odot$ .0003, min_commission $^{=5}$ ), type $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ 'stock')  

# 优化器设置  

g.optimizer $=$ 2 #设定使用的优化模型optimize_model $=$ {  

1:"模型1：等权重配置",2:"模型2：组合风险平价；股票的总权重限制为0到 $9\Theta_{\prime0}^{\circ\prime}$ ，ETF 的总权重限制为0 到 $\tt16\%$ ；每只标的权重不超过 $\tt{1070}^{11}$ ,3:"模型3：组合风险最小化（最小化组合方差）；组合总权重限制为90%到 $\tt{100\%}$ ；组合年化收益率目标下限为 $\tt{10\%^{\prime\prime}}$ ,4:"模型4：'人气指标5 日均值'最大化；组合年化收益率目标下限为 $\tt16\%$ ；每只标的权重不超过 $2\Theta_{\prime0}^{\circ\prime\prime1\prime}$ ,5:"模型5：组合夏普比率最大化；每只标的权重不超过10%"  

print("优化%s"%(optimize_model[g.optimizer]))  

## 运行函数（reference_security 为运行时间的参考标的；传入的标的只做种类区分，因此传入'000300.XSHG'或'510300.XSHG'是一样的）# 开盘前运行run_monthly(before_market_open, monthday $^{=1}$ ,time='9:00', reference_security='000300.XSHG')# 开盘运行run_monthly(market_open, monthday $^{=1}$ , time $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ '9:30',reference_security='000300.XSHG')  

## 开盘前运行函数  

def before_market_open(context):print('调仓日期：%s'%context.current_dt.date())  

# 选出上证50 成分股的一部分与选定的ETF 基金进行组合,构成股票池。  

etf = [ '159902.XSHE', '159903.XSHE', '510050.XSHG', '510880.XSHG', '510440.XSHG', ] g.buy_list $=$ list(get_index_stocks('000016.XSHG')[- 15:]) $^+$ etf  

## 开盘时运行函数def market_open(context):  

# 将不在股票池中的股票卖出 sell_list $=$ set(context.portfolio.positions.keys()) - set(g.buy_list) for stock in sell_list: order_target_value(stock, 0)  

# 组合优化模型if g.optimizer $\mathbf{\tau}=\mathbf{\tau}\perp$ :# 模型1：等权重配置optimized_weight $=$  

elif g.optimizer $\qquad\qquad\qquad\qquad\qquad\qquad\qquad=\quad2\qquad$ :# 模型2：组合风险平价；股票的总权重限制为0 到90%，ETF 的总权重限制为0 到 $\underline{{\boldsymbol{1}}}\,\underline{{\boldsymbol{\Theta}}}_{\boldsymbol{0}}^{\boldsymbol{0}\prime}$ ；每只标的权重不超过 $\underline{{\boldsymbol{1}}}\,\underline{{\boldsymbol{\Theta}}}_{\boldsymbol{0}}^{\boldsymbol{0}\prime}$ optimized_weight $=$  

portfolio_optimizer(date $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ context.previous_date, securities $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ g.buy_list, target $\underline{{\underline{{\mathbf{\delta\pi}}}}}$  

constraints $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ [MarketConstraint('stock', ${\sf10w=\odot.\odot}$ , high $=\!\left(\cdot\right.9$ ),  

MarketConstraint('etf', ${\sf10w=\odot.\odot}$ , high=0.1)], bounds $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ [Bound(0, 0.1)], default_port_weight_range $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ [0., 1.0], ftol=1e-09, return_none_if_fail $\cdot\,$ True)  

elif g.optimizer $\qquad\qquad\qquad\qquad\qquad\qquad=\qquad\qquad3$ :  

# 模型3：组合风险最小化（最小化组合方差）；组合总权重限制为 90%到 $\underline{{\sf1}}\odot\odot_{\prime0}^{}$ ；组合年化收益率目标下限为 $\beth\b{\odot}_{\prime0}^{\circ\prime}$ optimized_weight $=$  

portfolio_optimizer(date $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ context.previous_date, securities $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ g.buy_list, target $\underline{{\underline{{\mathbf{\delta\pi}}}}}$  

MinVariance(count $=\mathtt{250}$ ), constraints $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ [WeightConstraint( $\scriptstyle\mathtt{10w=0.9}$ , high=1.0),  

AnnualProfitConstraint(limit $\operatorname{\mu=0}\cdot1$ , count=250)], bounds $.=\left[\,\right]$ ,  

default_port_weight_range $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ [0., 1.0], ftol=1e-09, return_none_if_fail $\cdot\,$ True)  

elif g.optimizer $\mathit{\Theta}=\mathit{\Theta}4$ :  

# 模型4：组合标的因子值最大化# 定义因子：人气指标5 日均值class AR(Factor):name $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ 'ar'# 每天获取过去五日的数据max_window $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ 5# 获取的数据是人气指标dependencies $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ ['AR']def calc(self, data):return data['AR'].mean()  

# 模型4：'人气指标5 日均值'最大化；组合年化收益率目标下限为10%；每只标的权重不超过 $2\lvert\boldsymbol{\Theta}_{\boldsymbol{\cdot}0}^{0\prime}$ optimized_weight $=$  

portfolio_optimizer(date $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ context.previous_date, securities $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ g.buy_list, target $\underline{{\underline{{\mathbf{\delta\pi}}}}}$   
MaxFactorValue(factor=AR, count $\mathrel{\mathop:}=\beth$ ), constraints $\underline{{\underline{{\mathbf{\delta\pi}}}}}$   
[AnnualProfitConstraint(limit $\operatorname{\prime}=\!\Theta\,,2$ , count $=\mathtt{250}$ )], bounds $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ [Bound(0, 0.2)],  

default_port_weight_range $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ [0., 1.0], ftol=1e-09, return_none_if_fail $\cdot\,$ True)  

lif g.optimizer $\mathit{\Theta}=\mathit{\Theta}\;5$ :# 模型5：组合夏普比率最大化；每只标的权重不超过 $\underline{{\boldsymbol{1}}}\,\underline{{\boldsymbol{\Theta}}}_{\boldsymbol{0}}^{\boldsymbol{0}\prime}$ optimized_weight $=$  

portfolio_optimizer(date $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ context.previous_date, securities $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ g.buy_list, target $\underline{{\underline{{\mathbf{\delta\pi}}}}}$  

MaxSharpeRatio( $\mathbf{\boldsymbol{r}}\mathbf{\boldsymbol{f}}\!=\!\boldsymbol{\Theta}\cdot\boldsymbol{\Theta}$ ,weight_sum_equal $=\!\odot.5$ , count $=\,\!25\odot$ ),#无风险利率为0，最大化夏普比率需要约束组合权重的和为0.5constraints $\mathrm{~\textbf~{~=~}~}\left[\,\right]$ ,bounds $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ [Bound(0, 0.1)],default_port_weight_range $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ [0., 1.0],ftol=1e-09,return_none_if_fail $\cdot\,$ True)  

# 查看优化结果 print(optimized_weight)  

# 优化失败，给予警告  

if type(optimized_weight) $==$ type(None):  

print('警告：组合优化失败')  

# 按优化结果，执行调仓操作  

else: total_value $=$ context.portfolio.total_value # 获取总  

资产 for stock in optimized_weight.keys(): value $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ total_value $\star$ optimized_weight[stock] #   
确定每个标的的权重 order_target_value(stock, value) # 调整标的至目标   
权重  

# 策略程序架构  

名称 描述  

initialize 初始化函数  
initialize(context)  
初始化方法，在整个回测、模拟中最开始执行一次，用于初始一些全局变量  

参数 context: Context 对象, 存放有当前的账户/股票持仓信息返回 None  

def initialize(context):# g 为全局变量g.security $=$ "000001.XSHE"  

run_daily/run_weekly/run_monthly 定时运行策略(可选)  

run_monthly run_weekly run_daily  

def initialize(context):## func 是您自己定义的函数# 按月运行  

run_monthly(func, monthday, time $=$ '9:30', reference_security, force $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ False)  

# 按周运行 run_weekly(func, weekday, time $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ '9:30', reference_security, force $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ False) # 每天内何时运行(没有force 属性) run_daily(func, time $=$ '9:30', reference_security)  

回测环境/模拟专用API指定每月, 每周或者每天要运行的函数, 可以在具体每月/周的第几个交易日(或者倒数第几天)的某一分钟执行。  

在日级模拟中使用时，如果设置tim $\mathrm{e}\mathrm{=}^{\prime}\,9\!:\!30^{\prime}$ ，策略的实际运行时间是$9\colon27^{\sim}9\colon30$ 之间。策略内获取到逻辑时间(context.current_dt)仍然是 9:30。注意只有在使用相同的参照标的时，定时运行函数的优先级别  

为:run_monthly>run_weekly>run_daily 且与函数被注册的顺序无关；handle_data 与handle_tick 的执行顺序与前述函数无关。用户策略不应该依赖于这些计划任务执行的顺序。  

调用这些函数后, handle_data 可以不实现参数  


<html><body><table><tr><td>参数</td><td>解释</td></tr><tr><td>func</td><td>一个自定义的函数，此函数必须接受context 参数;例 如自定义函数名 market_open(context)</td></tr><tr><td>force</td><td>run_weekly和run_monthly中使用，run_daily不可 使用；表示若注册回调函数的时间晚于第一次回调的 执行时间是否就近执行；默认为True，建议使用 False</td></tr><tr><td>monthday</td><td>每月的第几个交易日，可以是负数，表示倒数第几个 交易日。开始策略的那个月会运行的，开始这个月第 几个交易日不是从当月第一天开始算的，而是从开始 运行当天开始算的（举例说明：假设您策略是3月20 号开始运行的，3月1号和3月20都是交易日，系统 会认为3月20是3月的第一个交易日，4月不会受影 响的）。force=True时如果超出每月总交易日个数， 则取临近的交易日执行。force=False,若注册回调函 数的时间晚于第一次回调的执行时间不会就近执行。 （具体见下方注意中的示例)</td></tr><tr><td>weekday</td><td>每周的第几个交易日，可以是负数，表示倒数第几个 交易日。开始策略的那一周第一个交易日是从策略开 始的那一天 计算的。force=True 如果超出每周总交 易日个数，则取临近的交易日执行；force=False,若 注册回调函数的时间晚于第一次回调的执行时间不会 就近执行。（具体见下方注意中的示例)</td></tr><tr><td>time</td><td>具体执行时间，一个字符串格式的时间，有三种方式： （1）24小时内的任意时间，例如"10:00"，"01:00"; 在tick频率的策略中，可以精确到秒。指定为具体时 间时，不可设置reference_security参数 (2)time="every_bar"，只能在 run_daily中调用,运 行时间和您设置的频率(回测页面右上方设置)一致， 按天会在交易日的开盘时调用一次，按分钟会在交易 时间每分钟运行。（3）’open’或’open+5m’或’open-</td></tr></table></body></html>  

10m' 这种形式，代表在reference_security 对应标的开盘时间(或加减X 分钟)运行一次，一般用于期货，因为期货有夜盘，开盘时间点不定。  

reference_security 时间的参照标的代码，字符串类型，默认为000001.XSHG’。 如参照 '000001.XSHG'，交易时间为 9:30-15:00；如参照'IF9999.CCFX'，2016-01-01 之后的交易时间为 9:30-15:00，在此之前为9:15-15:15；如参照'A9999.XDCE'，因为有夜盘，因此开始时间为21:00，结束时间为15:00。期货策略一定要修改参考标的，建议修改为对应的主力合约。当time 为具体时间时请勿设置此参数  

返回值 None注意  

一个策略中尽量不要同时使用run_daily 和handle_data，更不能使用run_daily(handle_data, "xx:xx")  

建议使用run_daily；【API 解析】策略运行频率（附隔固定时间运行方法）run_daily 中的函数只能有一个参数context，具体示例如下：  

def initialize(context): run_daily(func, time $=$ '10:00')  

def func(context): parm1 $=$ 'JoinQuant' func1(context, parm1)  

def func1(context, parm1):print(parm1)print(context.current_dt)print $\because\cdots+50.$ )•  参数 func 必须是一个全局的函数, 不能是类的成员函数, 示例:  

def on_week_start(context): pass  

class MyObject(object): def on_week_start2(self, context): pass  

def initialize(context):# OKrun_weekly(on_week_start, 1)# 错误, 下面的语句会报错  

run_weekly(MyObject().on_week_start2, 1)  

通过history/attribute_history 取天数据时, 是不包括当天的数据的(即使在15:00 和after_close 里面也是如此), 要取得当天数据, 只能取分钟的  

这些函数可以重复调用, 比如下面的代码可以在每周的第一个交易日和最后一个交易日分别调用两个函数:  

def on_week_start(context):  

# pass  

def on_week_end(context):  

# pass  

def initialize(context): run_weekly(on_week_start, 1) run_weekly(on_week_end, -1)  

每次调用这些函数都会产生一个新的定时任务, 如果想修改或者删除旧的定时任务, 请先调用 unschedule_all 来删除所有定时任务, 然后再添加新的.  

在一月/一周交易日数不够以致于monthday/weekday 无法满足时, 我们  
会找这周内最近的一个日期来执行, 比如, 如果某一周只有4 个交易日:o  若 weekday $\mathrm{\Lambda}=\,\,5$ , 我们会在第4 个交易日执行o  若 weekday $==~-5$ , 我们会在第1 个交易日执行  
如果要避免这样的行为, 您可以这样做:  

def initialize(context): run_weekly(weekly, 1)  

def weekly(context):  

if context.current_dt.isoweekday() != 1: # 不在周一, 跳过执行 return  

示例  

def initialize(context): run_weekly(market_open, weekday $^{=2}$ , force $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ False)  

def market_open(context):print("今天是周内第二个交易日") #注意策略开始的那一周,第一个交  
易日是按策略开始的日期开始计算的  
def weekly(context):print('weekly %s %s' % (context.current_dt,  
context.current_dt.isoweekday()))  
def monthly(context):print('monthly %s %s' % (context.current_dt,  
context.current_dt.month))  

def daily(context): print('daily %s' % context.current_dt)  

# def initialize(context):  

# 指定每月第一个交易日, 在开盘后十分钟执行  
# 注意策略开始的那一月,第一个交易日是按策略开始的日期开始计算的  
run_monthly(monthly, 1, '09:40')  
# 指定每周倒数第一个交易日, 在开盘前执行  
run_weekly(weekly, -1, '9:00')  
# 指定每天收盘前10 分钟运行  
run_daily(daily, '14:50')  
# 指定每天收盘后执行  
run_daily(daily, '15:30')  
# 指定在每天的10:00 运行  
run_daily(daily, '10:00')  
# 指定在每天的01:00 运行  
run_daily(daily, '01:00')  

# 参照股指期货的时间每分钟运行一次, 必须选择分钟回测, 否则每天执行  

run_daily(daily, 'every_bar',reference_security $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ 'IF9999.CCFX')handle_data 运行策略(可选)handle_data(context, data)该函数每个单位时间会调用一次, 如果按天回测,则每天调用一次,如果按分钟,则每分钟调用一次。  

该函数依据的时间是股票的交易时间，即 9:30 - 15:00. 期货请使用定时运行函数。  

该函数在回测中的非交易日是不会触发的（如回测结束日期为2016 年1 月5日，则程序在2016 年1 月1 日-3 日时，handle_data 不会运行，4 日继续运行）。  

对于使用当日开盘价撮合的日级模拟盘，在9:25 集合竞价完成时就可以获取到开盘价，出于减少并发运行模拟盘数量的目的，我们会提前到 $9\colon27^{\sim}9\colon30$ 之间运行, 策略内获取到逻辑时间(context.current_dt)仍然是 9:30。  

参数 context: Context 对象, 存放有当前的账户/标的持仓信息 data: 一个字典(dict), key 是股票代码, value 是当时的SecurityUnitData 对象.存放前一个单位时间(按天回测, 是前一天, 按分钟回测, 则是前一分钟) 的数据. 注意:  

为了加速, data 里面的数据是按需获取的, 每次 handle_data 被调用时, data 是空的 dict, 当你使用data[security]时该 security 的数据才会被获取.  
data 只在这一个时间点有效, 请不要存起来到下一个 handle_data 再用  
注意, 要获取回测当天的开盘价/是否停牌/涨跌停价, 请使  
用 get_current_data  

返回None示例  

def handle_data(context, data):  

order("000001.XSHE",100) on_event 事件回调(可选)  

on_event(context, event)  
用户在策略中定义on_event，在账户中持仓的标的发生对应的事件时on_event会被调用。建议用户使用isinstance 对事件类型进行判断。 目前已支持的事件有：  

DividendsEvent：分红送股事件ForcedLiquidationEvent：强行平仓事件  

# 参数  

context: Context 对象, 存放有当前的账户/标的持仓信息event: 发生的事件，一个事件对象。详见事件对象  

# 返回  

Nonebefore_trading_start 开盘前运行策略(可选)  

before_trading_start(context)  
该函数会在每天开始交易前被调用一次, 您可以在这里添加一些每天都要初始化的东西.  

该函数依据的时间是股票的交易时间，即该函数启动时间为'09:00'. 期货请使用定时运行函数，time 参数设定为'08:30' 。  

参数 context: Context 对象, 存放有当前的账户/股票持仓信息返回 None  

示例  

def before_trading_start(context):  

log.info(str(context.current_dt))  

after_trading_end 收盘后运行策略(可选)  

after_trading_end(context)  
该函数会在每天结束交易后被调用一次, 您可以在这里添加一些每天收盘后要执行的内容. 这个时候所有未完成的订单已经取消.  
该函数依据的时间是股票的交易时间，即该函数启动时间为 15:30. 期货请使  
用定时运行函数，time 参数设定为'15:30  
参数 context: Context 对象, 存放有当前的账户/股票持仓信息  
返回 None  

示例 def after_trading_end(context):  

log.info(str(context.current_dt))on_strategy_end 策略运行结束时调用(可选)def on_strategy_end(context)在回测、模拟交易正常结束时被调用， 失败时不会被调用。  

在模拟交易到期结束时也会被调用， 手动在到期前关闭不会被调用。  

参数 context: Context 对象, 存放有当前的账户/股票持仓信息  

返回 None  

示例 def on_strategy_end(context):  

print('回测结束')process_initialize 每次程序启动时运行函数(可选)process_initialize(context)该函数会在每次模拟盘/回测进程重启时执行, 一般用来初始化一些不能持久化保存的内容. 在 initialize 后执行.因为模拟盘会每天重启, 所以这个函数会每天都执行.  

参数 context: Context 对象, 存放有当前的账户/股票持仓信息返回 None  

示例 def process_initialize(context):  

# query 对象不能被 pickle 序列化, 所以不能持久保存, 所以每次进  
程重启时都给它初始化# 以两个下划线开始, 系统序列化 [g](#g) 时就会自动忽略这个变量,  
更多信息, 请看 [g](#g) 和 [模拟盘注意事项](#simulation_matters)g.__q $=$ query(valuation)  

def handle_data(context, data): get_fundamentals(g.__q)  

after_code_changed 模拟交易更换代码后运行函数(可选)  

after_code_changed(context)  
模拟盘在每天的交易时间结束后会休眠，第二天开盘时会恢复，如果在恢复时发现代码已经发生了修改，则会在恢复时执行这个函数。 具体的使用场景：可以利用这个函数修改一些模拟盘的数据。  

注意: 因为一些原因, 执行回测时这个函数也会被执行一次,在 process_initialize 执行之前执行.参数 context: Context 对象, 存放有当前的账户/股票持仓信息  

返回 None  

示例 def after_code_changed(context): g.stock $=$ '000001.XSHE'  

unschedule_all 取消所有定时运行(可选)   
# 取消所有定时运行   
unschedule_all()  

示例 def after_code_changed(context):  

# 取消所有定时运行  
unschedule_all()  
# 设定新的定时运行函数，指定函数在每天的10:00 运行  
run_daily(func, '10:00')  

# 策略API 介绍  

# 注意事项  

【取数据函数】【其它函数】目录中带有"♠" 标识的API 是 "回测环境/模拟"专用的API，不能在研究模块中调用。整个 【jqdata 模块】在研究环境与回测环境下都可以使用.  

所有价格单位是元  

时间表示:所有时间都是北京时间, 时区:UTC+8所有时间都是datetime.datetime 对象  

•  每个交易日结束时自动撤销所有未完成订单， 例如A 股是在17:00 之后。  

•  下文中提到 Context, SecurityUnitData, Portfolio, Position, Order 对象都是只读的, 尝试修改他们会报错或者无效.  

没有python 基础的同学请注意, 有的函数的定义中, 某些参数是有值的,这个值是参数的默认值, 这个参数是可选的, 可以不传.  

回测和模拟中，每日下单的最大数量为10000 笔  

如需使用策略组合或分仓操作，请看策略组合操作  

# 策略设置函数  

名称 描述  

set_benchmark 设置基准  

set_benchmark(security)  
默认我们选定了沪深300 指数的每日价格作为判断您策略好坏和一系列风险值计算的基准. 您也可以使用set_benchmark 指定其他股票/指数/ETF/自定义组合的价格作为基准。  

如果在期货策略中不希望看到基准，可以这样设置：  

set_benchmark({"000001.XSHG":0})，策略可以正常运行 （但无法计算alpha等收益）。  

# 参数  

security:股票/指数/ETF 代码，或者一个dict，key 为股票/指数/ETF代码，value 为小于1 的浮点数，代表对应标的的权重，权重之和必须小于等于1（小于1 代表基准中部分资金闲置）。  

返回 None示例一  

set_benchmark('600000.XSHG') 示例二，设置自定义组合为基准  

set_benchmark({'000001.XSHG':0.5,'000300.XSHG':0.3,'60000  
0.XSHG':0.2})  
set_order_cost 设置佣金/印花税  
set_order_cost(cost, type, ref $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ None)  
指定每笔交易要收取的手续费, 系统会根据用户指定的费率计算每笔交易的手  
续费  

# 参数  

cost: OrderCost 对象  

open_tax，买入时印花税 (只股票类标的收取，基金与期货不收) close_tax，卖出时印花税 (只股票类标的收取，基金与期货不收)  

open_commission，买入时佣金close_commission, 卖出时佣金close_today_commission, 平今仓佣金min_commission, 最低佣金，不包含印花税type: 股票、场内基金、场内交易的货币基金、分级A 基金、分级B 基金、分级母基金、金融期货、期货、债券基金、股票基金、QDII 基金、混合基金，'stock'/ 'fund' / 'mmf' /'fja'/'fjb'/ 'fjm'/'index_futures' / 'futures' / 'bond_fund' / 'stock_fund' /'QDII_fund' / / ‘mixture_fund' /ref: 参考代码，支持股票代码/基金代码/期货合约代码，以及期货的品种，如 '000001.XSHE'/'510180.XSHG'/'IF1709'/'IF'/'000300.OF  

注意：针对特定的交易品种类别设置手续费时，必须将ref 设为None；若针对特定的交易品种或者标的，需要将type 设置为对应的交易品种类别，将ref设置为对应的交易品种或者标的  

# 默认与示例  

# 股票类每笔交易时的手续费是：买入时佣金万分之三，卖出时佣金万分之三 加千分之一印花税, 每笔交易佣金最低扣5 块钱  

set_order_cost(OrderCost(open_ $\mathbf{t}\,\mathbf{a}\,\mathbf{x}\,{=}\,\Theta$ , close_tax $=\odot$ .001, open_commission $=\odot$ .0003, close_commission $=\odot$ .0003, close_today_commission $=\odot$ , min_commission $^{=5}$ ), type $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ 'stock')  

# 期货类每笔交易时的手续费是：买入时万分之0.23,卖出时万分之0.23,平 今仓为万分之23  

set_order_cost(OrderCost(open_tax $=\odot$ , close_tax $=\odot$ , open_commission $=\odot$ .000023, close_commission $=\odot$ .000023, close_today_commission $=\odot$ .0023, min_commission $=\odot$ ), type $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ 'index_futures')  

# 单独设置 000300.XSHG 的费用  

set_order_cost(OrderCost(open_tax $=\odot$ , close_tax $=\odot$ .001, open_commission=0.0003, close_commission $=\odot$ .0003, close_today_commission $=\odot$ , min_commission $^{=5}$ ), type='stock', ref='000300.XSHG')  

# # 设置所有期货（包括金融指数期货）的费用  

set_order_cost(OrderCost(open_ $\mathbf{t}\,\mathbf{a}\,\mathbf{x}\,{=}\,\Theta$ , close_tax $=\odot$ .001, open_commission=0.0003, close_commission $=\odot$ .0003,  

close_today_commission $=\odot$ , min_commission $^{=5}$ ), type $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ 'futures')  

# # 对 IF/IH/IC 三个品种有效  

set_order_cost(OrderCost(open_ $\mathbf{t}\,\mathbf{a}\,\mathbf{x}\,{=}\,\Theta$ , close_tax $=\odot$ .001, open_commission $=\odot$ .0003, close_commission $\mathbf{\check{\rho}}{=}\boldsymbol{\Theta}\,.\,\boldsymbol{\Theta}\boldsymbol{\Theta}\boldsymbol{\Theta}3$ , close_today_commission $=\odot$ , min_commission $^{=5}$ ), type='index_futures')  

# # 单独设置AU 期货品种的费用  

set_order_cost(OrderCost(open_ $\mathbf{t}\,\mathbf{a}\,\mathbf{x}\,{=}\,\Theta$ , close_tax=0.001, open_commission $=\odot$ .0003, close_commission $\!1\!=\!\!\Theta\,.\,\Theta\Theta\Theta3$ , close_today_commission $=\odot$ , min_commission $^{=5}$ ), type='futures', ref $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ 'AU')  

# # 单独设置AU1709 合约的费用  

set_order_cost(OrderCost(open_tax $=\odot$ , close_tax $=\odot$ .001, open_commission $=\odot$ .0003, close_commission $=\odot$ .0003,   
close_today_commission $=\odot$ , min_commission $^{=5}$ ),   
type='futures', ref='AU1709')   
注：期货持仓到交割日会以当天结算价平仓, 没有手续费, 不会有交易记录. set_slippage 设置滑点   
set_slippage(object,type $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ None, ref $\backslash=$ None)   
设定滑点，回测/模拟时有效.  

当您下单后, 真实的成交价格与下单时预期的价格总会有一定偏差, 因此我们加入了滑点模式来帮您更好的模拟真实市场的表现. 我们暂时只支持固定滑点。同时，我们也支持为交易品种和特定的交易标的设置滑点。  

# 参数  

type：交易品种，支持股票、基金、金融期货、期货、债券基金、股票基金、QDII 基金、货币基金、混合基金，'stock'/ 'fund' /'index_futures' （金融期货）/ 'futures'（包含股指期货和商品期货） / 'bond_fund' / 'stock_fund' / 'QDII_fund' /'money_market_fund' / ‘mixture_fund' 。为None 时则应用于全局。当type 被设定而ref 为None 时，表示将滑点应用于交易品种为type 的所有交易标的。•  ref: 标的代码。如要为特定交易标的单独设置滑点，必须同时设置type 为交易标的的交易品种。  

固定滑点 当您使用固定滑点的时候, 我们认为您的落单的多少并不会影响您最后的成交价格. 您只需要指定一个价差, 当您下达一个买单指令的时候, 成交的价格等于当时(您执行order 函数所在的单位时间)的平均价格加上价差的一半；当您下达一个卖出指令的时候，卖出的价格等于当时的平均价格减去价差的一半. 价差可以设定为一个固定值或者按照百分比设定。  

固定值： 这个价差可以是一个固定的值(比如0.02 元, 交易时加减0.01 元), 设定方式为：FixedSlippage(0.02)百分比： 这个价差可以是是当时价格的一个百分比(比如 $0.\;2\%$ , 交易时加减当时价格的 $0.\ 1\%)$ ), 设定方式为：PriceRelatedSlippage(0.002)跳数（期货专用，双边）: 这个价差可以是合约的价格变动单位（跳数），比如2 跳，设定方式为： StepRelatedSlippage(2)；滑点为小数时，向下取整，例如设置为3 跳，单边1.5，向下取整为1 跳。  

# 为全部交易品种设定固定值滑点 set_slippage(FixedSlippage(0.02))  

# 为股票设定滑点为百分比滑点  

set_slippage(PriceRelatedSlippage(0.00246),type $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ 'stock')  

# 设置CU 品种的滑点为跳数滑点2  

set_slippage(StepRelatedSlippage(2),type $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ 'futures',ref = 'CU')  

# 为螺纹钢RB1809 设定滑点为跳数滑点(注意只是这一个合约，不是所有的RB 合约)  

set_slippage(StepRelatedSlippage(2),type='futures', ref $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ "RB1809.XSGE")  

# StepRelatedSlippage(2)表示开平的单边滑点为1 个价格最小单位，螺  
纹钢价格最小变动单位为1 元/吨  
# 如果以市价单进行开多仓（或者平空仓），现价3000 元，成交价  
$3000+1\times2/2{=}3001$ 元  

# 如果以市价单进行开空仓（或者平多仓），现价3000 元，成交价3000-$_{\textrm{1}\times2/2=}$ 2999 元  

注：(1)如果您没有调用 set_slippage 函数, 系统默认的滑点是PriceRelatedSlippage(0.00246)；(2)所有类型为 "mmf"与  

"money_market_fund"的标的滑点默认为0，且调用set_slippage 重新设置也不会生效。  

use_real_price 设置动态复权(真实价格)模式，建议开启 set_option('use_real_price', value)  

该设定必须在initialize 中调用，建议开启设置是否开启动态复权（真实价格）模式，默认是False(主要是为了让旧的策略不会出错)。 是否开启动态复权模式对模拟交易是有影响的，原理参考拆分合并与分红，【API 解析】| 动态复权与技术指标。  

# 参数  

value: True / False示例# 开启动态复权模式  

set_option('use_real_price', True)  
是否开启动态复权对于回测及模拟交易的影响（原理参考拆分合并与分红）：•  开启，value 值为 True: 回测过程中:  

每天看到的当天的价格都是真实的(不复权的)  

o 使用真实的价格下单, 交易详情和持仓详情里看到的都是真实价格  

o 为了让编写代码简单, 通过数据获取函数API 拿到的都是基于当天日期的前复权价格. 比如: 回测运行到了2015-01-01 这一天, 那么history(3, '1d', 'close')取得的就是你穿越到2015-01-01 这一天所看到的前复权价格. 另一方面, 你在不同日期调用数据获取函数API 返回的价格可能是不一样的, 因为我们在不同日期看到的前复权价格是不一样的. 所以不要跨日期缓存这些API 返回的结果.  

o 每到新的一天, \*\*如果持仓中有股票发生了送股或者分红，对应的股数/现金会自动在账户中体现  

注意事项:  

如上所说, 不要跨日期缓存数据获取函数API 返回的结果开启真实价格回测之后, 回测结果可能会之前不一样, 因为交易时买入数量必须是100 的倍数, 使用前复权价格和实际价格能买入的数量是不一样的.  
如果想通过 history 拿到昨天的真实价格, 还是需要用取得价格除以factor, 因为可能今天发生了拆合分红, 导致拿到的昨天的价格是相对于今天的前复权价格.  
s = '000001.XSHE'  
df $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ attribute_history(s, 1, '1d',  
fields $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ ['close', 'factor'])  
real_close $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ df['close'][-1] /  
df['factor'][-1]  

关闭，value 值为 False: 此选项的核心是选定一个日期作为基准, 保证这个日期的价格是真实价格, 然后调整其他日期的价格. 最终保证所有价格是连续的, 在回测或者模拟交易过程中不同日期看到的价格是一致的. 下面分回测和模拟交易单独做介绍:  

o 回测: 基准日期是建立回测的日期, 回测过程中所看到的所有价格都是基于此日期的前复权价格. 比如说, 我昨天跑了一个回测,那么回测过程所有价格都是在昨天所看到的前复权价格. 这会导致两个问题:  

回测过程中使用了前复权价格下单, 这是违背真实场景的.不同的日期建立的回测跑出来的结果可能会有差异, 因为如果这两次回测之间回测的股票发生了拆合或者分红, 会导致回测中看到前复权价格会不一致.  

o 模拟交易: 基准日期是建立模拟交易的日期, 模拟交易过程所看到的所有价格都是基于此日期调整过的. 为了方便计算, 我举一个虚拟的例子: 某只股票在如下三个日期的实际价格和后复权因子分别是:  

# 日期 价格 后复权因子  

2015-09-01 1 1   
2015-10-01 2 2  

2015-11-01 4 4  

如果你在 09-01 建立了一个模拟交易, 你在不同日期看到的所有价格都是 1如果你在 10-01 建立了一个模拟交易, 你在不同日期看到的所有价格都是 2如果你在 11-01 建立了一个模拟交易, 你在不同日期看到的所有价格都是 4•  为了更好的模拟, 建议大家都设成 True.  

注意： (1)对期货不生效,对场内基金会生效, 但因场内基金在拆分/合并时除权日披露不标准,目前采用的是折算基准日，和实际除权日可能有差异，鉴于此原因不建议给含有场内基金的策略开启动态复权 (2) 设置 use_real_price 为True 之后, 如下的按天回测的代码是不对的：  

def initialize(context): g.cached_data $=$ [] g.s = '000001.XSHE' def handle_data(content, data): g.cached_data.append(data) if len(g.cached_data) > 1:  

# 如果昨天收盘价比前天涨了 $^{5\%}$ , 则买入. 这是不对的, 如果昨天早上发生了拆合, 则昨天和前天的股价不具可比性.if g.cached_data[-1][g.s].close > g.cached_data[-2][g.s].close $\star$ 1.05:order(g.s, 1000)order_volume_ratio 设置成交量比例set_option('order_volume_ratio', value)设定成交量比例，根据实际行情限制每个订单的成交量.  

# 参数  

value: value 是一个 float 值, 默认为1.0, 根据实际行情限制每个  
订单的成交量.o 对于每一笔订单：  

如果是市价单, 成交量不超过: 每日成交量 \* value如果是限价单, 限价单撮合时设定分价表中每一个价格的成交量的比率, 假设某一分钟分价表如下:  

价格 成交量  

10.0 10  
10.1 11  
10.2 12  
撮合时, 按价格 10.0 成交 $^{10\ *}$ value 股, 按价格 10.1  
成交 $^\mathrm{~11~*~}$ value 股, 按价格 10.2 成交 $12~*$ value 股  

# 示例  

# 设定成交量比例  

set_option('order_volume_ratio', 0.25) # 成交量不超过总成交量的四分之一  

# 注意  

当下单量超过了当日全市场所有的成交量，系统成交数量是直接取全市场所有的成交量  

match_with_order_book 设置是否开启盘口撮合模式set_option('match_with_order_book', value)设定是否使用盘口撮合模式. 此选项只对模拟盘生效，默认关闭  

# 参数  

value: 默认关闭True，开启，使用盘口进行撮合，撮合方式详见订单处理False，关闭，使用 Bar 进行撮合，撮合方式详见订单处理  

set_universe(history 专用) 设定股票池  

set_universe(security_list)设置或者更新此策略要操作的股票池 context.universe. 请注意:  

该函数现在只用于设定history 函数的默认security_list, 除此之外并无其他用处。  

参数  

security_list: 股票列表返回 None  

示例   
set_universe(['000001.XSHE', '600000.XSHG'])   
set_commission(已废弃) 设定费率  

set_commission(object)已废弃。请使用set_order_cost 替代  

指定每笔交易要收取的手续费, 系统会根据用户指定的费率计算每笔交易的手续费  

# 此函数已废弃，请使用 set_order_cost - 设置佣金/印花税  

参数 object: 一个PerTrade 对象• PerTrade.buy_cost，买入时手续费PerTrade.sell_cost，卖出时手续费PerTrade.min_cost，最少的手续费默认：PerTrade(buy_cost=0.0003, sell_cost=0.0013, min_cost $=5,$ ) 每笔交易时的手续费是, 买入时万分之三，卖出时万分之三加千分之一印花税, 每笔交易最低扣5 块钱  

disable_cache 关闭缓存  

# disable_cache()  

在默认情况下系统启用了缓存以加快运行速度，但在策略内存占用较大时容易超过设置的内存上限而触发系统杀死进程。若用户反复出现策略因内存占用超限而被终止的情况，可以考虑在initialize 函数中调用disable_cache 来关闭缓存机制。  

# 注意在关闭缓存后会导致策略运行速度明显下降。  

实验性设置项 实验性设置项  

为了方便用户进行策略研究，我们开放了部分实验性的设置项。开启这些设置项后，系统将允许策略进行一些不符合交易规则的非常规操作。  

# $\mathsf{T}+\Theta$ 模式，A 股买入后可以立刻卖出set_option("t0_mode", True)  

# 总是撮合市价单，支持在非交易时间下市价单，按照最新的数据立即撮合set_option("always_match_market_order", True)# 强制撮合，仅支持限价单。使用限价单进行委托时将不对委托价格和成交数量进行任何检查而直接成交，当开启此设置项时，市价单的成交价也不会受滑点的影响  

set_option("match_by_signal", True)avoid_future_data 设置是否开启避免未来数据模式set_option("avoid_future_data", True)设置回测是否开启避免未来数据模式，默认关闭【API 解析】避免未来数据  

# 参数  

False, 关闭，回测可能带入未来数据True,开启，系统会提示或者处理未来数据  

# 未来函数，未来数据  

回测中能够引入未来数据的函数，即可以返回未来数据的函数；通过未来函数获取到的数据为未来数据；例如开盘使用get_price 获取当天的收盘价，则get_price 为未来函数，当天的收盘价为未来数据。  
更多的数据可以参考数据更新频率  

# 使用方法  

在策略中使用set_option("avoid_future_data", True)来开启此功能，该选项默认为False，表示关闭。开启此功能之后，如果用户在策略中调用API 的过程中，尝试通过API 获取未来数据，就会抛出FutureDataError。  

# 未来数据类型及处理方法  

可以通过时间参数避免的未来数据：回测中使用我们提供的包含时间参数的API 去取current_dt 之后的数据（比如get_bars 取current_dt 之后的分钟数据）；设置"avoid_future_data"为True 后，如果获取未来数据则抛出异常；  
没法通过时间参数主动避免的未来数据：对于用户没法通过函数参数主动避免的未来数据（比如get_call_auction）；设置  
"avoid_future_data"为True 后，如果获取未来数据，我们会将返回结果中的未来数据剔除掉，而不会抛出异常。  

# 注意  

avoid_future_data 只是帮助大家在写策略过程中，避免一些常见引入未来数据的问题；? avoid_future_data 不是万能的，不是包含所有检测未来数据的方法；写策略过程中，如果引入外部数据(自己本地数据、连网获取数据等)也有可能带入未来数据，这些使用avoid_future_data 是检测不到的；策略中设置固定的股票池，设置固定时间点交易一些标的，也有可能引入未来数据，例如设置一些历史上涨幅比较大的标的在低点买入高点卖出；  

# 数据获取函数  

小提示：  

• 在日级策略中可以获取分钟级K 线数据，反之亦然；取多支标的的数据时，不要获取交易时段不同的标的（例如：不同交易时间的期货标的），否则会报错；天、分钟、tick 行情里成交量单位是股，复权数据中成交量也是复权后的成交量；更多数据，请访问数据页面查看。聚宽目前提供哪些数据及数据更新频率获取频率非一天或者非一分钟的数据，请使用get_bars.获取数据参考教程：聚宽新手指南-获取数据教程数据相关教程Query 及查询财务数据的简单教程数据常见疑问汇总数据获取问题快问快答JQData 安装的问题  

# 常用数据获取及计算系列外部数据获取及分享【集合贴】数据相关  

【API 解析】有关数据获取方法  

# 【API 解析】get_bars 定义和逻辑  

名称 描述  

get_price 获取历史数据，可查询多个标的多个数据字段，返回数据格式为DataFrame  

get_price(security, start_date=None, end_date $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ None,frequency='daily', fields $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ None, skip_paused=False,fq='pre', count $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ None, panel $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ True, fill_paused=True)获取一支或者多只股票的行情数据, 按天或者按分钟，这里在使用时注意end_date 的设置， 传入的值不要大于context.current_dt，否则会引入未来函数。  

关于停牌: 因为此API 可以获取多只股票的数据, 可能有的股票停牌有的没有,为了保持时间轴的一致,  

我们默认没有跳过停牌的日期, 停牌时使用停牌前的数据填充(请看 SecurityUnitData 的 paused 属性). 如想跳过, 请使用skip_paused $\cdot$ True 参数, 注意当 panel $\pm$ True 且获取多标的时不支持(panel结构需要索引对齐)  

# 参数  

security: 一支股票代码或者一个股票代码的list  

count: 与 start_date 二选一，不可同时使用. 数量, 返回的结果集  
的行数, 即表示获取 end_date 之前几个 frequency 的数据  
start_date: 与 count 二选一，不可同时使用. 字符串或者  
datetime.datetime/datetime.date 对象, 开始时间.o 如果 count 和 start_date 参数都没有, 则 start_date 生效,值是 '2015-01-01'. 注意:当取分钟数据时, 时间可以精确到分钟, 比如: 传入datetime.datetime(2015, 1, 1, 10, 0, 0)或者'2015-01-01 10:00:00'.o 当取分钟数据时, 如果只传入日期, 则日内时间是当日的00:00:00.当取天数据时, 传入的日内时间会被忽略  
end_date: 格式同上, 结束时间, 默认是'2015-12-31', 包含此日  
期. 注意: 当取分钟数据时, 如果 end_date 只有日期, 则日内时间  
等同于 00:00:00, 所以返回的数据是不包括 end_date 这一天的.  

frequency: 单位时间长度, 几天或者几分钟, 现在支持'Xd','Xm','daily'(等同于'1d'), 'minute'(等同于'1m'), X 是一个正整数, 分别表示X 天和X 分钟(不论是按天还是按分钟回测都能拿到这两种单位的数据), 注意, 当X > 1 时, fields 只支持['open', 'close', 'high',  

'low', 'volume', 'money']这几个标准字段,合成数据的逻辑见下文.默认值是daily  

fields: 字符串list, 选择要获取的行情数据字段, 默认是None(表示['open', 'close', 'high', 'low', 'volume', 'money']这几个标准字段), 支持SecurityUnitData 里面的所有基本属性,，包含：['open','close', 'low', 'high', 'volume', 'money', 'factor','high_limit','low_limit', 'avg', 'pre_close','paused','open_interest'],其中paused 为1 表示停牌。  

skip_paused: 是否跳过不交易日期(包括停牌, 未上市或者退市后的日  
期). 如果不跳过, 停牌时会使用停牌前的数据填充(具体请看  
SecurityUnitData 的paused 属性), 上市前或者退市后数据都为 nan,  
但要注意:o  默认为 Falseo 当 skip_paused 是 True 时, 获取多个标的时需要将panel 参数设置为False(panel 结构需要索引对齐)  
fq: 复权选项(对股票/基金的价格字段、成交量字段及factor 字段生  
效) :o 'pre', 前复权(根据'use_real_price'选项不同含义会有所不同, 参见[set_option]), 默认是前复权o None,不复权, 返回实际价格o 'post',后复权  
panel：在pandas 0.25 版后，panel 被彻底移除。获取多标的数据时建  
议设置panel 为False，返回等效的dataframe  
fill_paused：对于停牌股票的价格处理，默认为True；True 表示用  
pre_close 价格填充；False 表示使用NAN 填充停牌的数据。  

# 合成数据的逻辑  

当frequency 为X 天和X 分钟时，代表使用以X 为长度的滑动窗口进行合并数据。举例：  

9:33:00 调用get_price 获取1 个单位的数据，frequency $\cdot\!=^{,}$ 5min',表示使用上一交易日14:58、14:59、15:00、本交易日9:31、9:32 这5 根1分钟K 线来合成数据；  
9:37:00 调用get_price 获取1 个单位的数据，frequency $\cdot\!=^{,}$ 5min',表示使用本交易日9:32、9:33、9:34、9:35、9:36 这5 根1 分钟K 线来合成数据；  

# 返回  

请注意, 为了方便比较一只股票的多个属性, 同时也满足对比多只股票的一个属性的需求, 我们在security 参数是一只股票和多只股票时返回的结构完全不一样(默认panel=False 时)  

如果是一支股票, 则返回[pandas.DataFrame]对象, 行索引是[datetime.datetime]对象, 列索引是行情字段名字, 比如'open'/'close'. 比如:get_price('000300.XSHG')[:2]返回:  

open close high low volume money 2015 3566.0 3641.5 3669.0 3551.5 451198098. 519849817448. -01- 9 4 4 1 0 0 05  

2015 3608.4 3641.0 3683.2 3587.2 420962185. 498529588258. -01- 3 6 3 3 0 0 06  

如果是多支股票, 则返回[pandas.Panel]对象, 里面是很多  
[pandas.DataFrame]对象, 索引是行情字段(open/close/…), 每个  
[pandas.DataFrame]的行索引是[datetime.datetime]对象, 列索引是股  
票代号. 比如get_price(['000300.XSHG',  
'000001.XSHE'])['open'][:2]返回:  

2015-01-05 3566.09 13.21   
2015-01-06 3608.43 13.09  

# 示例  

# 获取一支股票  

df $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ get_price('000001.XSHE') # 获取000001.XSHE 的2015 年的按天数据  

df $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ get_price('000001.XSHE', start_date $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ '2015-01-01',  
end_date='2015-01-31 23:00:00', frequency $\mathrel{\mathop{:}}=\mathsf{^{\prime}1m}\,^{\prime}$ ,  
fields $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ ['open', 'close']) # 获得000001.XSHG 的2015 年01 月的  
分钟数据, 只获取open+close 字段  
df $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ get_price('000001.XSHE', count $=~2$ , end_date $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ '2015-  
01-31', frequency='daily', fields $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ ['open', 'close']) # 获  
取获得000001.XSHG 在2015 年01 月31 日前2 个交易日的数据  
df $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ get_price('000001.XSHE', start_date $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ '2015-12-01  
$14:00:00^{\prime}$ , end_date='2015-12-02 12:00:00',  
frequency='1m') # 获得000001.XSHG 的2015 年12 月1 号14:00-  
2015 年12 月2 日12:00 的分钟数据  

# 获取多只股票  

panel $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ get_price(get_index_stocks('000903.XSHG')) # 获取中证100 的所有成分股的2015 年的天数据, 返回一个[pandas.Panel]df_open $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ panel['open']  # 获取开盘价的[pandas.DataFrame],行索引是[datetime.datetime]对象, 列索引是股票代号  

df_volume $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ panel['volume']  # 获取交易量的  

[pandas.DataFrame]  

df_open['000001.XSHE'] # 获取平安银行的2015 年每天的开盘价数据history 获取历史数据，可查询多个标的单个数据字段，返回数据格式为DataFrame 或 Dict(字典)  
history(count, unit='1d', field='avg',  
security_list=None, df $\backslash=$ True, skip_paused=False, fq='pre')回测环境/模拟专用API，可以在投资研究中获取  
查看历史的行情数据。  

关于停牌: 因为获取了多只股票的数据, 可能有的股票停牌有的没有, 为了保持时间轴的一致, 我们默认没有跳过停牌的日期, 停牌时使用停牌前的数据填充(请看[SecurityUnitData]的paused 属性). 如想跳过, 请使用  

skip_paused $\pm$ True 参数  

当取天数据时, 不包括当天的, 即使是在收盘后；分钟数据不包括当前分钟的数据，没有未来  

# 参数  

count: 数量, 返回的结果集的行数unit: 单位时间长度, 几天或者几分钟, 现在支持'Xd','Xm', X 是一个正整数, 分别表示X 天和X 分钟(不论是按天还是按分钟回测都能拿到这两种单位的数据), 注意, 当 $\mathrm{~X~}>~1$ 时, field 只支持['open','close', 'high', 'low', 'volume', 'money']这几个标准字段.  

field: 要获取的数据类型, 支持SecurityUnitData 里面的所有基本属性,，包含：['open', ' close', 'low', 'high', 'volume', 'money','factor', 'high_limit',' low_limit', 'avg', ' pre_close','paused']  

security_list:  

要获取数据的股票列表  

None 表示查询 context.universe 中所有股票的数据，context.universe 需要使用set_universe 进行设定，形如：set_universe(['000001.XSHE', '600000.XSHG'])。  

df: 若是True, 返回[pandas.DataFrame], 否则返回一个dict, 具体请看下面的返回值介绍. 默认是True. 我们之所以增加df 参数, 是因为[pandas.DataFrame]创建和操作速度太慢, 很多情况并不需要使用它.为了保持向上兼容, df 默认是True, 但是如果你的回测速度很慢, 请考虑把df 设成False.  

skip_paused: 是否跳过不交易日期(包括停牌, 未上市或者退市后的日期). 如果不跳过, 停牌时会使用停牌前的数据填充(具体请看  

SecurityUnitData 的paused 属性), 上市前或者退市后数据都为 nan,但要注意:  

默认为 False  
如果跳过, 则行索引不再是日期, 因为不同股票的实际交易日期  
可能不一样  

fq: 复权选项(对股票/基金的价格字段、成交量字段及factor 字段生 效) :  

o 'pre': 前复权(根据'use_real_price'选项不同含义会有所不同, 参见[set_option]), 默认是前复权  
o None: 不复权, 返回实际价格  
o 'post': 后复权  

# 返回  

df $:=$ True: [pandas.DataFrame]对象, 行索引是[datetime.datetime]对象, 列索引是股票代号. 比如: 如果当前时间是2015-01-07, universe是['000300.XSHG', '000001.XSHE'],history(2, '1d', 'open')将返回:  

000300.XSHG 000001.XSHE  

2015-01-05 3566.09 13.21  

2015-01-06  3608.43 13.09关于numpy 和pandas, 请看下面的第三方库介绍df=False: dict, key 是股票代码, value 是一个numpy 数组[numpy.ndarray], 对应上面的DataFrame 的每一列, 例如history(2, '1d', 'open', df=False)将返回:python{ '000300.XSHG': array([ 3566.09, 3608.43]), '000001.XSHE': array([ 13.21, 13.09]) }  

# 示例  

h $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ history(5, security_list $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ ['000001.XSHE', '000002.XSHE'])  

h['000001.XSHE'] #000001(平安银行)过去5 天的每天的平均价, 一个pd.Series 对象, index 是datatime  

h['000001.XSHE'][-1] #000001(平安银行)昨天(数组最后一项)的平均价  

h.iloc[-1] #所有股票在昨天的平均价, 一个pd.Series 对象, index是股票代号  

h.iloc[-1]['000001.XSHE'] #000001(平安银行)昨天(数组最后一项)的平均价  

h.mean() # 取得每一列的平均值  
## set_universe 之后可以，调用 history 可以不用指定  
security_list  

set_universe(['000001.XSHE']) # 设定universe  

history(5) # 获取universe 中股票的过去5 天(不包含今天)的每天的平均价  
history(5, '1m') # 获取universe 中股票的过去5 分钟(不包含当前分钟)的每分钟的平均价  
history(5, '1m', 'price') # 获取universe 中股票的过去5 分钟(不包含当前分钟)的每分钟的平均价  
history(5, '1m', 'volume') # 获取universe 中股票的过去5 分钟(不包含当前分钟)的每分钟的交易额  
history(5, '1m', 'price', ['000001.XSHE']) # 获取平安银行的过去5 分钟(不包含当前分钟)的每分钟的平均价  
h = history(5, security_list=['000001.XSHE',  
'000002.XSHE'], df=False)  
h['000001.XSHE'] #h 是一个 dict，获取 h 中 000001.XSHE 对应的值。  
h['000001.XSHE'][0] #返回000001.XSHE 第五天的数据  
h['000001.XSHE'][-1] #返回000001.XSHE 最新一日的数据  
h['000001.XSHE'].sum() #对返回的五日数据求和  
h['000001.XSHE'].mean() # 对返回的五日数据求平均  
# 因为h 本身是一个dict, 下列panda.DataFrame 的特性将不可用:# h.illoc[-1]  
# h.sum()  
attribute_history 获取历史数据，可查询单个标的多个数据字段，返回数据格式为 DataFrame 或 Dict(字典)  
attribute_history(security, count, unit='1d',  
fields $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ ['open', 'close', 'high', 'low',  
'volume', 'money'],  
skip_paused $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ True, df=True, fq='pre')  
回测环境/模拟专用API  
查看某一支股票的历史数据, 可以选这只股票的多个属性, 默认跳过停牌日期.  
当取天数据时, 不包括当天的, 即使是在收盘后；分钟数据不包括当前分钟的数据，没有未来；  
参数  

#  

# security: 股票代码  

count: 数量, 返回的结果集的行数unit: 单位时间长度, 几天或者几分钟, 现在支持 'Xd', 'Xm', X 是一个正整数, 分别表示X 天和X 分钟(不论是按天还是按分钟回测都能拿到这两种单位的数据), 注意, 当 X > 1 时, field 只支持 ['open','close', 'high', 'low', 'volume', 'money'] 这几个标准字段.  

fields: 股票属性的list, 支持SecurityUnitData 里面的所有基本属性，包含：['open', ' close', 'low', 'high', 'volume', 'money','factor', 'high_limit',' low_limit', 'avg', pre_close','paused']  

skip_paused: 是否跳过不交易日期(包括停牌, 未上市或者退市后的日期). 如果不跳过, 停牌时会使用停牌前的数据填充(具体请看[SecurityUnitData]的paused 属性), 上市前或者退市后数据都为  

# nan, 默认是True  

df: 若是True, 返回[pandas.DataFrame], 否则返回一个dict, 具体请看下面的返回值介绍. 默认是True.我们之所以增加df 参数, 是因为[pandas.DataFrame]创建和操作速度太慢, 很多情况并不需要使用它.为了保持向上兼容, df 默认是True, 但是如果你的回测速度很慢, 请考虑把df 设成False.  

fq: 复权选项(对股票/基金的价格字段、成交量字段及factor 字段生 效) :  

o 'pre': 前复权(根据'use_real_price'选项不同含义会有所不同, 参见[set_option]), 默认是前复权  
o None: 不复权, 返回实际价格  
o 'post': 后复权  

# 返回  

df $:=$ True [pandas.DataFrame]对象, 行索引是[datetime.datetime]对象, 列索引是属性名字. 比如: 如果当前时间是2015-01-  

07,attribute_history('000300.XSHG', 2)将返回:  

<html><body><table><tr><td>111</td><td>open</td><td>close</td><td>high</td><td>low</td><td>volume</td><td>money</td></tr><tr><td>2015</td><td>3566.0</td><td>3641.5</td><td>3669.0</td><td>3551.5</td><td>451198098.</td><td>519849817448.</td></tr><tr><td>-01-</td><td>6</td><td>4</td><td>4</td><td>1</td><td>0</td><td>0</td></tr><tr><td>05</td><td></td><td></td><td></td><td></td><td></td><td></td></tr></table></body></html>  

2015 3608.4 3641.0 3683.2 3587.2 420962185. 498529588258. -01- 3 6 3 3 0 0  

df=False: dict, key 是fields 中的属性, value 是一个numpy 数组[numpy.ndarray], 对应上面的DataFrame 的每一列, 例如  

attribute_history('000300.XSHG', 2, df $\equiv$ False)将返回: {  

'volume': array([ 4.51198098e+08, 4.20962185e+08]),  

'money': array([ 5.19849817e+11,  

4.98529588e+11]),  

'high': array([ 3669.04, 3683.23]), 'low': array([ 3551.51,  3587.23]), 'close': array([ 3641.54, 3641.06]),  

'open': array([ 3566.09, 3608.43])  

# 示例  

stock $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ '000001.XSHE'  
h $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ attribute_history(stock, 5, '1d', ('open','close',  
'volume', 'factor')) # 取得000001(平安银行)过去5 天的每天的开  
盘价, 收盘价, 交易量, 复权因子  
# 不管df 等于True 还是False, 下列用法都是可以的  
h['open'] #过去5 天的每天的开盘价, 一个pd.Series 对象, index 是  
datatime  
h['close'][-1] #昨天的收盘价  
h['open'].mean()  

# 下面的pandas.DataFrame 的特性, df=False 时将不可用# 行的索引可以是整数, 也可以是日期的各种形式:  

h['open']['2015-01-05'] h['open'][datetime.date(2015, 1, 5)] h['open'][datetime.datetime(2015, 1, 5)]  

# # 按行取数据  

h.iloc[-1] #昨天的开盘价和收盘价, 一个pd.Series 对象, index 是  
字符串 $\because1$ open $"/"$ close'  
h.iloc[-1]['open'] #昨天的开盘价  
h.loc['2015-01-05']['open']  

# 高级运算  

h = h[h['volume'] > 1000000] # 只保留交易量>1000000 股的行  
h['open'] $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ h['open']/h['factor'] #让open 列都跟factor 列相  
除, 把价格都转化成原始价格  
$h[\mathsf{^{\prime}c l o s e^{\prime}]}=h[\mathsf{^{\prime}c l o s e^{\prime}]}/h[\mathsf{^{\prime}f a c t o r^{\prime}]}$   
get_bars 获取历史数据(包含快照数据)，可查询单个或多个标的多个数据字  
段，返回数据格式为 numpy.ndarray 或DataFrame  
get_bars(security, count, unit='1d',fields $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ ['date',  
'open','high','low','close'],include_now $=$ False, end_dt $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ None, fq_ref_date $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ None,  
df=False)  

获取各种时间周期的 bar 数据， bar 的分割方式与主流股票软件相同， 而且支持返回当前时刻所在 bar 的数据；  

get_bars 开盘时取的bar 高开低收都是当天的开盘价，成交量成交额为0；get_bars 没有跳过停牌选项，所获取的数据都是不包含停牌的数据，如果bar个数少于count 个，则返回实际个数，并不会填充。更详细的get_bars 解释，【API 解析】get_bars 定义和逻辑  

参数  

security: 标的代码或包含交易代码的列表,支持一个或多个标的，多个标的用list 或tuple。  

count: 大于0 的整数，表示获取bar 的个数。如果行情数据的bar 不足count 个，返回的长度则小于count 个数。unit: bar 的时间单位, 支持标准bar 和非标准bar当unit 为'1m', '5m', '15m', '30m', '60m', '120m', '1d', '1w'(一周), '1M'（一月）标准bar 时，bar 的分割方式与主流股票软件类似，期货的bar 各平台也许稍微有差异，我们与文华接近；当unit 为非上述标准bar 时('xm', 例如'3m')，只支持分钟级别的，x需要小于240，以每天的开盘为起始点，每x 分钟为一条bar；fields: 获取数据的字段， 支持如下值：'date', 'open', 'close','high', 'low', 'volume', 'money', 'open_interest'(持仓量，是期货和期权特有的字段), 'factor'(后复权因子)include_now: 取值True 或者False。 表示是否包含当前bar, 比如策略时间是9:33，unit 参数为5m， 如果 include_now $r=$ True,则返回9:30-9:33 这个分钟 bar。end_dt：查询的截止时间，支持的类型为datetime.datetime 或None 或str。默认值为Noneo  在回测/模拟环境下默认为context.current_dto  在投资研究环境下默认为datetime.now()o 由于bar 的最小单位是一分钟，所以end_dt 的秒和毫秒没有什么意义，会被替换为0，例如：end_dt $=$ datetime.datetime(2019,11, 22, 9, 35, 23) 和 end_dt $=$ datetime.datetime(2019, 11,22, 9, 35, 00) 是一样的  
•  fq_ref_date：复权基准日期，支持的类型为datetime.datetime 或None,为None 时为不复权数据。o  投资研究环境中默认为 datetime.date.today()o  回测/模拟环境中默认为 context.current_dt.date()o  如果用户输入 fq_ref_date $=$ None, 则获取到的是不复权的数据o 如果用户想获取后复权的数据，可以将fq_ref_date 指定为一个很早的日期，比如 datetime.date(2000, 1, 1)o 定点复权，以某一天价格点位为参照物，进行的前复权或后复权。设置为datetime.datetime.now()即返回前复权数据 ; 设置为context.current_dt 返回动态复权数据，更多关于动态复权解释o 对股票/基金的价格字段、成交量字段生效 ,factor 字段不受影响,只返回后复权因子  
•  df:是否返回pandas.DataFrame 对象，默认为False，返回的是numpy.ndarray 对象  

# 返回值  

df $=$ Falseo 若security 为字符串格式的标的代码时，返回一个numpy.ndarry 对象。o 若security 为list 或者tuple 格式的标的代码时，返回一个dict，key 为标的代码，value 为numpy.ndarry 对象。  

# df $=$ True  

o 若security 为字符串格式的标的代码时，返回pandas.DataFrame，dataframe 的index 是一个整数数组  
o  若security 为list 或者tuple 格式的标的代码时，返回pandas.DataFrame，dataframe 的index 是一个MultiIndex  

# 示例  

get_bars(["ER8888.XZCE", "AP1905.XZCE"], end_dt $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ datetime.datetime.now(), count $^{=3}$ ,include_now $=$ False)  

array $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ get_bars('000001.XSHG', 5,   
unit='1d',fields=['open','close'],include_now $^1=$ False)   
array['close']  

# 设置复权基准日为 2018-01-05 , 取得的最近5 条包括 end_dt 的天数据  

get_bars('600507.XSHG',5,unit='1d',  
fields $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ ('date','open', 'high', 'low', 'close'),include_now $=$ True, end_dt $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ '2018-01-05 11:00:00',  
fq_ref_date $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ datetime.date(2018,1,5))  
# 取得距离 2018-01-05 最近五周不包括这一周的 不复权的周数据  
get_bars('600507.XSHG',5,unit='1w',  
fields=('date','open', 'high', 'low', 'close'),include_now=False, end_dt='2018-01-05',  
fq_ref_date $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ None)  

# # 取得最近五个月不包括这一月的 前复权数据(和行情软件上看到的前复权数据一致)  

now $=$ datetime.datetime.now().date()   
get_bars('600507.XSHG',5,unit='1M',   
fields $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ ('date','open', 'high', 'low', 'close'), include_now=False, end_dt='2018-01-05',   
fq_ref_date $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ now)   
# 取2019-03-04 平安银行的不复权收盘价（end_dt 如果输入2019-03-   
04，默认2019-03-04 00:00:00）   
array $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ get_bars('000001.XSHE', count $^{=1}$ , unit $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ '1d', fields $=$ ['date', 'close'], include_now $:=$ True, end_dt='2019-03-04   
15:30:00', fq_ref_date $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ None)   
print(array[0][1])  

get_current_tick♠ 获取最新的 tick 数据get_current_tick(security, dt $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ None, df=False)  

# 参数  

security: 标的代码， 支持股票、场内基金、商品期货和股指期货以及包含标的代码的列表。 期货需要使用具体合约代码，不可以使用主力合约和指数合约代码。  
dt: datetime 格式的时刻。指定时代表返回离指定时刻最近的一条tick。默认为None。  
df: 默认为False，表示用Tick 对象来封装tick 数据，df=True 的时候，tick 数据使用dataframe 返回。  

# 返回  

当传入参数为标的代码时，返回tick 对象；  
当传入包含标的代码的列表则返回一个dict，key 是标的代码，value和传入一个字符串的返回值一样  
当参数df $=$ True 时，返回Dataframe 格式数据  

# 注意  

目前不支持在研究中使用,支持回测及模拟交易的tick、分钟及天频率中使用；get_current_tick 依赖上下文，可以在run_daily、handle_data 或handle_tick 中调用；•  当天截至当天时刻未产生tick 时返回None；  

# 示例  

import datetime   
def initialize(context): run_daily(market_open, time $=$ '10:00')   
def market_open(context): print(get_current_tick('000001.XSHE')) print(get_current_tick(['000001.XSHE',   
'600000.XSHG'])) print(get_current_tick('000001.XSHE',   
dt $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ datetime.datetime(2018,11,1,10,00,00)))   
get_ticks 获取股票、期货、50ETF 期权、股票指数及场内基金的 tick 数据   
get_ticks(security, end_dt, start_dt $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ None, count $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ None,   
fields $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ ['time', 'current', 'high', 'low', 'volume',   
'money'], skip $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ True, df $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ False)  

# 参数：  

security: 一只str 格式的股票代码或期货代码，或者一个list 格式的股票或者期货列表  

end_dt: 结束日期  

start_dt: 开始日期, 与count 参数二选  

count: 取出指定时间区间内前多少条的tick 数据, 与start_dt 参数二选一  

fields: 选择要获取的行情数据字段，默认为["time", "current","high", "low", "volume", "money"], 默认的fields 没有a1_v\~a5_v等数据，需要这些字段的话，需要您在fields 中自己添加，即可获取  

skip:默认为True，过滤掉无成交变化的tick 数据；当指定skip $=$ False时，返回的tick 数据会保留无成交有盘口变化的tick 数据（股票自2013 年1 月1 日以后；期货自2019 年8 月19 日以后）  

df:默认为False，返回numpy.ndarray 格式的tick 数据；df=True 的时候，返回pandas.Dataframe 格式的数据。  

# 返回值  

df 为False返回numpy.ndarray 格式的数据。ndarray 打印输出没有附带字段名，但您仍然可以通过array[field]的形式获取对应字段的数据。  

df 为True返回pandasDataframe 格式的数据股票tick 返回结果期货tick 返回结果：  

<html><body><table><tr><td>字段名 说明</td><td>字段类型</td></tr><tr><td>time</td><td>时间 float</td></tr><tr><td>open</td><td>当日开盘价 float</td></tr><tr><td>current</td><td>当前价 float</td></tr><tr><td>high</td><td>截至到当前时刻的日内最高价 float</td></tr><tr><td>1ow</td><td>截至到当前时刻的日内最低价 float</td></tr><tr><td>volume</td><td>累计成交量 float</td></tr><tr><td>money</td><td>累计成交额 float</td></tr><tr><td>a1_v~a5_v</td><td>五档卖量 float</td></tr><tr><td>a1_p~a5_p</td><td>五档卖价 float</td></tr><tr><td>b1_v~b5_v</td><td>五档买量 float</td></tr><tr><td>b1_p~b5_p</td><td>五档买价 float</td></tr></table></body></html>  

time 时间 floatcurrent 当前价 floatopen 当日开盘价 floathigh 截至到当前时刻的日内最高价 floatlow 截至到当前时刻的日内最低价 floatvolume 累计成交量 floatmoney 累计成交额 floatposition 持仓量 floata1_v 一档卖量 floata1_p 一档卖价 floatb1_v 一档买量 floatb1_p 一档买价 float  

# 注意  

股票及场内基金部分， 支持 2010-01-01 至今的tick 数据，提供买五卖五数据；期货部分， 支持 2010-01-01 至今的tick 数据，提供买一卖一数据。\*\* 如果要获取主力合约的tick 数据，可以先使用get_dominant_future(underlying_symbol,dt)获取主力合约对应的标的，然后再用get_ticks()获取该合约的tick 数据；期权部分，上交所ETF（2017-01-01 起），商品期权（2019-12-02起），提供买五卖五数据；目前期权仅提供数据，不支持回测模拟等；  
•  支持在tick、分钟及天频率的策略中使用；  

# 示例  

•  股票tick 数据示例#获取平安银行2018-07-01 的tick 数据，start_dt 和count 只能有一个不为None 值, 不带时分秒时，默认00:00:00d $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ get_ticks("000001.XSHE",start_dt $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ None, end_dt $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ "2018-07-02", count $=\tt1(\theta)$ )print(d)  

[(20180629145636.0, 9.1, 9.13, 8.96, 66367900.0,   
600781695.0) (20180629145639.0, 9.09, 9.13, 8.96, 66373200.0,   
600829823.0) (20180629145642.0, 9.1, 9.13, 8.96, 66374900.0,   
600845311.0) (20180629145645.0, 9.1, 9.13, 8.96, 66375900.0,   
600854399.0) (20180629145648.0, 9.1, 9.13, 8.96, 66436600.0,   
601406783.0) (20180629145651.0, 9.1, 9.13, 8.96, 66447200.0,   
601503231.0) (20180629145654.0, 9.1, 9.13, 8.96, 66461700.0,   
601635199.0) (20180629145657.0, 9.09, 9.13, 8.96, 66462000.0,   
601637887.0) (20180629145700.0, 9.1, 9.13, 8.96, 66468300.0,   
601695231.0) (20180629150003.0, 9.09, 9.13, 8.96, 67530000.0,   
611346111.0)]  

# skip $=$ True,返回空值  

d $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ get_ticks("000068.XSHE",start_dt $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ "2019-10-11   
$\odot9:15:\odot\odot^{\prime1}$ ,   
end_dt $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ "2019-10-11 09:25:00", count $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ None,   
fields $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ ['time', 'current',   
'volume','money','a1_v','a2_v', 'b1_v', 'b2_v'],   
skip $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ True)   
print(d)  

# skip $=$ False,有数据  

d $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ get_ticks("000068.XSHE",start_dt $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ "2019-10-11   
$\odot9:15:\odot\odot^{\prime1}$ ,   
end_dt $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ "2019-10-11 09:25:00", count $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ None,   
fields $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ ['time', 'current',   
'volume','money','a1_v','a2_v', 'b1_v', 'b2_v'],   
skip $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ False)   
print(d)  

# df $=$ True,返回DataFrame 格式的数据  

df2 $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ get_ticks('000001.XSHE', end_dt='2019-11-05  
$10:40:10^{\prime}$ ,  
start_dt $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ '2019-11-05 10:40:00', df=True)  
print(df2)期货tick 数据示例  

d = get_ticks('AU1812.XSGE',start_dt $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ '2018-07-02 21:00:00',end_dt='2018-07-03 15:30:00',count $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ None) print(d)  

[(20180702210000.0, 272.9, 272.95, 272.9, 492.0,   
134285000.0) (20180702210001.0, 272.85, 272.95, 272.85, 884.0,   
241270200.0) (20180702210001.5, 272.9, 272.95, 272.85, 1280.0,   
349320300.0) (20180703145958.5, 271.9, 272.95, 271.3, 123526.0,   
33623516800.0) (20180703145959.0, 271.85, 272.95, 271.3, 123528.0,   
33624060500.0) (20180703150000.0, 271.9, 272.95, 271.3, 123536.0,   
33626235700.0)]  

get_current_data $\spadesuit$ 获取当前时间数据  

# get_current_data()  

# 回测环境/模拟专用API  

获取当前单位时间（当天/当前分钟）的涨跌停价, 是否停牌，当天的开盘价等。  

回测时, 通过其他获取数据的API 获取到的是前一个单位时间(天/分钟)的数据, 而有些数据, 我们在这个单位时间是知道的, 比如涨跌停价, 是否停牌,当天的开盘价. 我们添加了这个API 用来获取这些数据.  

# 参数  

•  现在不需要传入, 即使传入了, 返回的 dict 也是空的, dict 的 value会按需获取.  

返回值 一个dict, 其中 key 是股票代码, value 是拥有如下属性的对象  

last_price : 最新价• high_limit: 涨停价low_limit: 跌停价paused: 是否停止或者暂停了交易, 当停牌、未上市或者退市后返回Trueis_st: 是否是 ST(包括ST, $*\mathrm{S}\mathrm{T}$ )，是则返回 True，否则返回 Falseday_open: 当天开盘价,当天的开盘价至少09:27 分之后才可获取name: 股票现在的名称, 可以用这个来判断股票当天是否是 ST, \*ST,是否快要退市industry_code: 股票现在所属行业代码, 参见 行业概念数据  

# 注意  

•  为了加速, 返回的 dict 里面的数据是按需获取的, dict 初始是空的,当你使用 current_data $=$ get_current_data();  

current_data[security]时(假设 current_data 是返回的 dict),该 security 的数据才会被获取.  

返回的结果只在当天有效, 请不要存起来到隔天再用  

该函数仅仅限在要获取数据的标的在交易时段时调用  

# 示例  

def handle_data(context, data): current_data $=$ get_current_data() print(current_data) print(current_data['000001.XSHE'].last_price) print(current_data['000001.XSHE'].paused) print(current_data['000001.XSHE'].day_open)  

get_extras 获取基金单位/累计净值，期货结算价/持仓量等 get_extras(info, security_list, start_date='2015-01-01', end_date='2015-12-31', df $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ True, count $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ None)  

得到多只标的在一段时间的如下额外的数据:  

is_st: 是否股改s, st,\*st 和退市整理期标的acc_net_value: 基金累计净值• unit_net_value: 基金单位净值futures_sett_price: 期货结算价futures_positions: 期货持仓量adj_net_value: 场外基金的复权净值  

# 参数  

info: ['is_st', 'acc_net_value', 'unit_net_value','futures_sett_price', 'futures_positions', 'adj_net_value'] 中的一个  
• security_list: 股票列表  
• start_date/end_date: 开始结束日期, 同 get_pricedf: 返回[pandas.DataFrame]对象还是一个dict, 同 [history]count: 数量, 与 start_date 二选一, 不可同时使用, 必须大于 0.表示取 end_date 往前的 count 个交易日的数据  

# 返回值  

df $:=$ True: [pandas.DataFrame]对象, 列索引是股票代号, 行索引是 [datetime.datetime], 比如get_extras('acc_net_value', ['510300.XSHG', '510050.XSHG'], start_date $=$ '2015-12-01', end_date $=$ '2015-12-03')返回:  

510300.XSHG 510050.XSHG  

2015-12-01 1.395 3.119   
2015-12-02 1.4432 3.251   
2015-12-03 1.4535 3.254  

get_extras('is_st', ['000001.XSHE', '000018.XSHE'], start_date $=$ '2013-12-01', end_date $=$ '2013-12-03')返回:  

# 000001.XSHE 000018.XSHE  

2013-12-02  False True  

2013-12-03 False True  

df=False 一个dict, key 是基金代号, value 是[numpy.ndarray], 比  
如get_extras('acc_net_value', ['510300.XSHG',  
'510050.XSHG'], start_date $=$ '2015-12-01', end_date $=$ '2015-  
12-03', df $\equiv$ False)返回:  
{u'510050.XSHG': array([ 3.119,  3.251,  3.254]),u'510300.XSHG': array([ 1.395 ,  1.4432,  1.4535])  
示例  
info $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ 'acc_net_value'  
security_list $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ ['519671.OF', '110003.OF']  
df $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ get_extras(info, security_list, start_date $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ '2019-05-  
$\mathtt{10}^{\prime}$ , end_date $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ '2019-05-15')  
print(df)  
get_all_factors 获取聚宽因子库中所有因子的信息  
get_all_factors()  
参数  

返回pandas.DataFrame，包含因子代码、因子名称、因子分类示例from jqfactor import get_all_factorsprint(get_all_factors())  

# 输出  

index factor   
factor_intro category  \   
0 administration_expense_ttm 管理   
费用TTM basics   
1 asset_impairment_loss_ttm 资产减   
值损失TTM basics   
2 EBIT 息税前   
利润 basics   
3 EBITDA 息税折旧摊   
销前利润 basics  

4  

费用TTM basics  

5 goods_sale_and_service_render_cash_ttm 销售商品提供劳务收到的现金   basics  

get_factor_values 质量、基础、情绪、成长、风险、每股等数百个因子数据# 导入函数库  

from jqfactor import get_factor_values  

# 取值函数  

get_factor_values(securities, factors, start_date, end_date, count)  

获取质量因子、基础因子、情绪因子、成长因子、风险因子、每股因子等数百个因子数据，详细的因子列表请参考因子库  

# 参数  

securities:股票池，单只股票（字符串）或一个股票列表• factors: 因子名称，单个因子（字符串）或一个因子列表start_date:开始日期，字符串或 datetime 对象，与 coun t 参数二选一end_date: 结束日期， 字符串或 datetime 对象，可以与 start_date或 count 配合使用count: 截止 end_date 之前交易日的数量（含 end_date 当日），与start_date 参数二选一  

# 返回  

• 一个 dict： key 是因子名称， value 是 pandas.dataframe。  
• dataframe 的 index 是日期， column 是股票代码， value 是因子值为了防止单次返回数据时间过长，每次调用 api 请求的因子值(因子数股票数交易日数)不能超过 200000 个 示例  

# 导入函数库  

from jqfactor import get_factor_values# 获取因子Skewness60(个股收益的60 日偏度)从 2017-01-01 至2017-03-04 的因子值  

factor_data $\underline{{\underline{{\mathbf{\delta\pi}}}}}$  

get_factor_values(securities $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ ['000001.XSHE'], factors $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ ['Skewness60'], start_date $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ '2017-01-01', end_date='2017-03-04')  

# 查看因子值  

factor_data['Skewness60']get_factor_kanban_values 获取因子看板列表数据from jqfactor import $\star$ df $\underline{{\underline{{\mathbf{\delta\pi}}}}}$  

get_factor_kanban_values(universe $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ 'hs300',bt_cycle $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ 'month _3',model $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ 'long_only',category $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ ['quality','basics','emoti on','growth','risk','pershare'],skip_paused=False,commisi on_slippage $=\odot$ )  

# print(df)  

# 参数  

universe：股票池o ' $\mathrm{hs300^{\circ}}$ : 沪深300o ' $\mathrm{zz500}^{\prime}$ : 中证500， ' $\mathrm{z}800^{\circ}$ : 中证800oo 'zz1000': 中证1000o 'zzqz': 中证全指  
bt_cycle：测试周期o 'month_3'：近三个月o 'year_1'：近一年o year_3'：近三年o year_10'：近十年  
model：组合构建模型o 'long_only'：纯多头组合o 'long_short'：多空组合  
category：分类o 'quality': 质量类o 'basics': 基础类o emotion': 情绪类o 'growth': 成长类o 'risk': 风险类o 'pershare': 每股类o 'style': 风险因子 - 风格因子o 'technical': 技术类o 'momentum': 动量类  
skip_paused: 过滤涨停及停牌股o False: 否o True: 是  
commision_slippage: 手续费及滑点o 0: 无o 1: $3\%$ 佣金 $+1\%$ 印花税 $^+$ 无滑点o 2: $3\%$ 佣金 $+1\%$ 印花税 $+1\%$ 滑点  

# 返回  

pandas.DataFrame 针对 [model - 组合构建模型]选择的不同，返回的结构有所差异  

一、long_only - 纯多头组合  

• index：自然增长的数字，从0 开始，无意义column：o date：数据的更新日期，因子的收益需要下一交易日才可得到 ,因此实际数据的时间比date 晚一天(T 日收盘后的因子收益需要  

$\mathrm{T}{+1}$ 的收盘价才可得出，数据需要在 $\mathrm{T}{+}2$ 日凌晨3 点计算之后才可得到)o universe: 股票池o bt_cycle: 测试周期o skip_paused: 过滤涨停及停牌股o commision_slippage: 手续费及滑点o category: 因子分类o code：因子代码o compound_return_1q：一分位数累积收益o compound_return_5q：五分位数累积收益o annualized_return_1q：一分位数年化收益率o annualized_return_5q：五分位数年化收益率o max_drawdown_1q：一分位数最大回撤o max_drawdown_5q：五分位数最大回撤o sharpe_1q：一分位数夏普比率o sharpe_5q：五分位数夏普比率o turnover_ratio_1q：一分位数换手率o turnover_ratio_5q：五分位数换手率o annual_return_bm：基准指数年化收益率o ic_mean：IC 均值o ir：IR 值o good_ic：IC 绝对值大于0.02 的比率  

二、long_short - 多空组合  

index：自然增长的数字，从0 开始，无意义• column：o date：数据的更新日期，因子的收益需要下一交易日才可得到 ,因此实际数据的时间比date 晚一天(T 日收盘后的因子收益需要$\mathrm{T}{+1}$ 的收盘价才可得出，数据需要在 $\mathrm{T}{+}2$ 日凌晨3 点计算之后才可得到)o universe: 股票池o bt_cycle: 测试周期o skip_paused: 过滤涨停及停牌股o commision_slippage: 手续费及滑点o category: 因子分类o code：因子代码o compound_return_ls：累积收益o annualized_return_ls：年化收益率o max_drawdown_ls：最大回撤o sharpe_ls：夏普比率o turnover_ratio_ls：换手率o annual_return_bm：基准指数年化收益率o ic_mean：IC 均值o ir：IR 值  

o good_ic：IC 绝对值大于0.02 的比率get_fundamentals 查询财务数据  

get_fundamentals(query_object, date $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ None, statDate $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ None)查询财务数据，详细的财务数据表及字段描述请点击财务数据文档查看，Query对象的使用方法请参考Query 的简单教程  

date 和statDate 参数只能传入一个:  

传入date 时, 查询指定日期date 收盘后所能看到的最近(对市值表来说, 最近一天, 对其他表来说, 最近一个季度)的数据, 我们会查找上市公司在这个日期之前(包括此日期)发布的数据, 不会有未来函数.  
•  传入statDate 时, 查询 statDate 指定的季度或者年份的财务数据.注意:  
1. 由于公司发布财报不及时, 一般是看不到当季度或年份的财务报表的,回测中使用这个数据可能会有未来函数, 请注意规避.  
2. 由于估值表每天更新, 当按季度或者年份查询时, 返回季度或者年份最后一天的数据  
3. 由于“资产负债数据”这个表是存量性质的， 查询年度数据是返回第四季度的数据。  
4. 银行业、券商、保险专项数据只有年报数据，需传入statDate 参数，当传入 date 参数 或 statDate 传入季度时返回空，请自行避免未来函数。  

当 date 和 statDate 都不传入时, 相当于使用 date 参数, date 的默认值下面会描述.  

# 参数  

query_object: 一个sqlalchemy.orm.query.Query 对象, 可以通过全局的 query 函数获取 Query 对象,Query 对象的简单使用教程date: 查询日期, 一个字符串(格式类似'2015-10-15')或者[datetime.date]/[datetime.datetime]对象, 可以是None, 使用默认日期. 这个默认日期在回测和研究模块上有点差别:1. 回测模块: 默认值会随着回测日期变化而变化, 等于context.current_dt 的前一天(实际生活中我们只能看到前一天的财报和市值数据, 所以要用前一天)2. 研究模块: 使用平台财务数据的最新日期, 一般是昨天.•  statDate: 财报统计的季度或者年份, 一个字符串, 有两种格式:1. 季度: 格式是: 年 $+\,\,{^\bullet\,}_{\bf{q}}\,\,\,+$ 季度序号, 例如: '2015q1', '2013q4'.2. 年份: 格式就是年份的数字, 例如: '2015', '2016'.  

返回 返回一个 [pandas.DataFrame], 每一行对应数据库返回的每一行(可能是几个表的联合查询结果的一行), 列索引是你查询的所有字段 注意：  

1. 为了防止返回数据量过大, 我们每次最多返回5000 行  
2. 当相关股票上市前、退市后，财务数据返回各字段为空  

# 示例  

# 查询'000001.XSHE'的所有市值数据, 时间是2015-10-15  

# q $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ query(  

valuation  

).filter( valuation.code == '000001.XSHE' df $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ get_fundamentals(q, '2015-10-15')  

# 打印出总市值 log.info(df['market_cap'][0])  

# 获取多只股票在某一日期的市值, 利润  

df $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ get_fundamentals(query(valuation, income).filter(# 这里不能使用 in 操作, 要使用in_()函数valuation.code.in_(['000001.XSHE', '600000.XSHG'])), date='2015-10-15')  
# 选出所有的总市值大于1000 亿元, 市盈率小于10, 营业总收入大于200  
亿元的股票  

df $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ get_fundamentals(query( valuation.code, valuation.market_cap, valuation.pe_ratio, income.total_operating_revenue ).filter( valuation.market_cap > 1000, valuation.pe_ratio < 10, income.total_operating_revenue > 2e10 ).order_by( # 按市值降序排列 valuation.market_cap.desc() ).limit( # 最多返回100 个 100 ), date='2015-10-15')  

# 使用 or_ 函数: 查询总市值大于1000 亿元 \*\*或者\*\* 市盈率小于10 的股票  

from sqlalchemy.sql.expression import or_ get_fundamentals(query( valuation.code ).filter( or_( valuation.market_cap > 1000, valuation.pe_ratio < 10 ))  

# 查询平安银行2014 年四个季度的季报, 放到数组中q $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ query(income.statDate,income.code,  

income.basic_eps, balance.cash_equivalents, cash_flow.goods_sale_and_service_render_cash ).filter( income.code == '000001.XSHE', )  

rets $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ [get_fundamentals(q, statDate $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ '2014q'+str(i)) for i in range(1, 5)]  

# 查询平安银行2014 年的年报  

q = query( income.statDate, income.code, income.basic_eps, cash_flow.goods_sale_and_service_render_cash ).filter( income.code $==$ '000001.XSHE',  

ret = get_fundamentals(q, statDate='2014')  

get_fundamentals_continuously 查询多日的财务数据  
get_fundamentals_continuously(query_object,  
end_date $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ None,count $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ None, panel $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ True)  
查询多日财务数据，详细的财务数据表及字段描述请点击财务数据文档查看，  
Query 对象的使用方法请参考Query 的简单教程  

# 参数  

query_object: 一个sqlalchemy.orm.query.Query 对象, 可以通过全局的 query 函数获取 Query 对象,Query 对象的简单使用教程end_date: 查询日期, 一个字符串(格式类似'2015-10-15')或者[datetime.date]/[datetime.datetime]对象, 可以是None, 使用默认日期. 这个默认日期在回测和研究模块上有点差别:  
1. 回测模块: 默认值会随着回测日期变化而变化, 等于context.current_dt 的前一天(实际生活中我们只能看到前一天的财报和市值数据, 所以要用前一天)  
2. 研究模块: 使用平台财务数据的最新日期, 一般是昨天.  
•  count: 获取 end_date 前 count 个日期的数据  
• panel：在pandas 0.24 版后，panel 被彻底移除。获取多标的数据时建议设置panel 为False，返回等效的dataframe  

返回  

默认panel $\pm$ True，返回一个 pandas.Panel；  
建议设置panel 为False，返回等效的dataframe；  

出于性能方面考虑，我们做出了返回总条数不超过5000 条的限制。 也就是说：查询的股票数量\*count 要小于5000。 否则，返回的数据会不完整。示例  

>>> q $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ query(valuation.turnover_ratio, valuation.market_cap, indicator.eps ).filter(valuation.code.in_(['000001.XSHE',   
'600000.XSHG']))  

>>> panel $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ get_fundamentals_continuously(q, end_date $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ '2018-01-01', count $^{=5}$ )  

>>> panel  

\<class 'pandas.core.panel.Panel'\>   
Dimensions: 3 (items) x 5 (major_axis) x 2 (minor_axis)   
Items axis: turnover_ratio to eps   
Major_axis axis: 2017-12-25 to 2017-12-29   
Minor_axis axis: 000001.XSHE to 600000.XSHG  

>>> panel.minor_xs('600000.XSHG')  

turnover_ratio market_cap eps  

2017-12-25 0.0687 3695.4270 0.48   
2017-12-26 0.0542 3710.1030 0.48   
2017-12-27 0.1165 3704.2324 0.48   
2017-12-28 0.0849 3680.7510 0.48   
2017-12-29 0.0582 3695.4270 0.48  

>>> panel.major_xs('2017-12-25')  

turnover_ratio  market_cap eps code 000001.XSHE 0.9372 2275.0796 0.38 600000.XSHG 0.0687 3695.4270 0.48  

>>> panel.xs('turnover_ratio',axis $=\odot$ )  
# axis=0 表示 items axis; axis $^{=1}$ 表示 major axis; axis $=2$ 表  
示 minor axis  

code 000001.XSHE 600000.XSHG day 2017-12-25 0.9372 0.0687 2017-12-26 0.6642 0.0542 2017-12-27 0.8078 0.1165  

2017-12-28 0.9180 0.08492017-12-29 0.5810 0.0582finance.run_query 深沪港通股东信息等数据from jqdata import $\star$  

finance.run_query(query_object)  
查询深沪港通、股东信息、公司概况等数据，详细的数据字段描述请点击市场  
通（沪港通深港通和港股通）查看  

# 参数  

query_object: 一个sqlalchemy.orm.query.Query 对象, 可以通过全局的query 函数获取Query 对象。返回 返回一个 dataframe， 每一行对应数据库返回的每一行， 列索引是你所查询的字段注意  

1. 为了防止返回数据量过大, 我们每次最多返回4000 行  
2. 不能进行连表查询，即同时查询多张表内数据  

示例# 查询万科 AH 股价格的前10 条数据${\mathfrak{q}}^{=}$ query(finance.STK_AH_PRICE_COMP).filter(finance.STK_AH_PRICE_COMP.a_code $==$ '000002.XSHE').order_by(finance.STK_AH_PRICE_COMP.day).limit(10)  

df=finance.run_query(q)  
#指定查询对象为恒瑞医药（600276.XSHG)的十大股东情况，限定返回条数  
为10 条  

q=query(finance.STK_SHAREHOLDER_TOP10 ).filter( finance.STK_SHAREHOLDER_TOP10.code=='600276.XSHG', finance.STK_SHAREHOLDER_TOP10.pub_date>'2015-01-01' ).limit(10)  

df $\backslash=$ finance.run_query(q)macro.run_query 获取聚宽宏观经济数据  

# 数据调用方法  

from jqdata import $\star$   
macro.run_query(query_object)  
查询宏观经济数据，详细的数据字段描述请点击宏观经济数据查看  

# 参数  

query_object: 一个sqlalchemy.orm.query.Query 对象, 可以通过全局的query 函数获取Query 对象。  

返回 返回一个 dataframe， 每一行对应数据库返回的每一行， 列索引是你  
所查询的字段  
注意  

1. 为了防止返回数据量过大, 我们每次最多返回4000 行  
2. 不能进行连表查询，即同时查询多张表内数据  

示例# 查询分地区农林牧渔业总产值表(季度累计) 的前10 条数据  

$\textsf{q}=$   
query(macro.MAC_INDUSTRY_AREA_AGR_OUTPUT_VALUE_QUARTER).limit(10)  
df $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ macro.run_query(q)  
# 查询2014 年的分地区农林牧渔业总产值表(年度)  
q $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ query(macro.MAC_INDUSTRY_AREA_AGR_OUTPUT_VALUE_YEAR).filter(macro.MAC_INDUSTRY_AREA_AGR_OUTPUT_VALUE_Y  
EAR.stat_year=='2014')  
df $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ macro.run_query(q)  
get_billboard_list 获取龙虎榜数据  
get_billboard_list(stock_list, start_date, end_date,  
count)  
获取指定日期区间内的龙虎榜数据  

# 参数  

stock_list: 一个股票代码的 list。 当值为 None 时， 返回指定日期的所有股票。• start_date:开始日期end_date: 结束日期count: 交易日数量， 可以与 end_date 同时使用， 表示获取end_date 前 count 个交易日的数据(含 end_date 当日)  

返回值pandas.DataFrame， 各 column 的含义如下:  

o code: 股票代码  
o day: 日期  
o direction: ALL 表示『汇总』，SELL 表示『卖』，BUY 表示『买』  
o abnormal_code: 异常波动类型  
o abnormal_name: 异常波动名称  
o sales_depart_name: 营业部名称  
o rank: 0 表示汇总， $1^{\sim}5$ 表示买一到买5， $6^{\sim}10$ 表示卖一到卖五  
o buy_value:买入金额  
o buy_rate:买入金额占比(买入金额/市场总成交额)  
o sell_value:卖出金额  
o sell_rate:卖出金额占比(卖出金额/市场总成交额)  
o net_value:净额(买入金额 - 卖出金额)  
o amount:市场总成交额  
o total_value：买入卖出金额之和（买入金额 $^+$ 卖出金额）  

# 示例  

# 在策略中获取前一日的龙虎榜数据  

get_billboard_list(stock_list $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ None, end_date $\underline{{\underline{{\mathbf{\delta\pi}}}}}$   
context.previous_date, count $^{=1}$ )   
get_index_stocks 获取指数成份股   
get_index_stocks(index_symbol, date $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ None)  

获取一个指数给定日期在平台可交易的成分股列表，请点击指数列表查看指数信息  

# 参数  

index_symbol: 指数代码  
date: 查询日期, 一个字符串(格式类似'2015-10-15')或者  
datetime.date/datetime.datetime 对象, 可以是None, 使用默认日期.  
这个默认日期在回测和研究模块上有点差别:1. 回测模块: 默认值会随着回测日期变化而变化, 等于context.current_dt2. 研究模块: 默认是今天  

返回 返回股票代码的list  

# 示例  

# 获取所有沪深300 的股票  

stocks $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ get_index_stocks('000300.XSHG')  
log.info(stocks)  
get_index_weights 获取指数成分股权重  
get_index_weights(index_id, date=None)  
获取指数成分股权重，每月更新一次，一般在月底或者月初  

# 参数  

index_id: 必选参数，代表指数的标准形式代码， 形式：指数代码.交易所代码，例如"000001.XSHG"。若代码格式错误或传入无效的指数代码，报错。date: 可选参数， 查询权重信息的日期，形式： $\!\!\!\langle\!\!\gamma_{0}\!\mathrm{Y}\!-\!\!\%\mathrm{m}\!-\!\!\%\mathrm{d}^{\prime\prime}$ ，例如$^{\prime\prime}2018{-}05{-}03^{\prime\prime}$ ，除此之外其他日期格式报错。当date 为None，在回测、模拟环境中，默认为context.current_dt.date()；在研究环境中，默认为datetime.now().date()。  

# 返回  

查询到对应日期，且有权重数据，返回 pandas.DataFrame， index 是股票代码，columns 为 display_name(股票名称), date(日期),weight(权重)；查询到对应日期，且无权重数据， 返回距离查询日期最近日期的权重信息；找不到对应日期的权重信息， 返回距离查询日期最近日期的权重信息；  

示例  
>>> get_index_weights(index_id="000001.XSHG", date $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ "2018-  
05-09")  

code display_name date weight  

000002.XSHG 万科A 2018-04-27 1.43  
000001.XSHG 平安银行 2018-04-27 0.93  

get_industry_stocks 获取行业成份股 get_industry_stocks(industry_code, date $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ None)  

获取在给定日期一个行业的所有股票，行业分类列表见数据页面-行业概念数据。  

# 参数  

industry_code: 行业编码  
date: 查询日期, 一个字符串(格式类似'2015-10-15')或者  
[datetime.date]/[datetime.datetime]对象, 可以是None, 使用默认  
日期. 这个默认日期在回测和研究模块上有点差别:1. 回测模块: 默认值会随着回测日期变化而变化, 等于context.current_dt2. 研究模块: 默认是今天  

返回 返回股票代码的list 示例 # 获取计算机/互联网行业的成分股  

stocks $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ get_industry_stocks('I64')  
get_concept_stocks 获取概念成份股  
get_concept_stocks(concept_code, date $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ None)  
获取在给定日期一个概念板块的所有股票，概念板块分类列表见数据页面-行业概念数据。  

# 参数  

concept_code: 概念板块编码  
date: 查询日期, 一个字符串(格式类似'2015-10-15')或者  
[datetime.date]/[datetime.datetime]对象, 可以是None, 使用默认  
日期. 这个默认日期在回测和研究模块上有点差别:1. 回测模块: 默认值会随着回测日期变化而变化, 等于context.current_dt2. 研究模块: 默认是今天  

返回 返回股票代码的list 示例 # 获取风电概念板块的成分股  

stocks $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ get_concept_stocks('SC0084', date='2019-04-16') print(stocks)  

注意  

申万在2014 年2 月21 做了调整，2014 年2 月21 日有几个行业被剔除了，同时又增加了新的行业，2014 年2 月21 日之后的行业是28 个，之前是23 个，历史上总共有34 个。  

get_industries 获取行业列表from jqdata import \*  

# get_industries(name, date=None)  

按照行业分类获取行业列表。  

# 参数  

name: 行业代码， 取值如下：o "sw_l1": 申万一级行业o $\ensuremath{{^\prime}\mathrm{sw}}_{-}12^{\prime\prime}$ : 申万二级行业o "sw_l3": 申万三级行业o "jq_l1": 聚宽一级行业o "jq_ $12^{\prime\prime}$ : 聚宽二级行业o "zjw": 证监会行业  
date: 获取数据的日期，默认为None，返回历史上所有行业；传入  

date，返回date 当天存在的行业；研究和回测中返回结果相同；  

# 返回值  

pandas.DataFrame， 各 column 的含义如下:o index: 行业代码o name: 行业名称o start_date: 开始日期  

示例  

# from jqdata import $\star$  

get_industries(name='zjw')  
get_industries(name $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ 'zjw', date='2016-01-01')get_concepts 获取概念列表  
from jqdata import $\star$   
get_concepts()  
获取所有的概念板块列表，行业分类列表见数据页面-行业概念数据。  

# 返回值  

pandas.DataFrame， 各 column 的含义如下:o index: 概念代码o name: 概念名称o start_date: 开始日期  

get_all_securities 获取所有标的信息get_all_securities(types $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ [], date=None)获取平台支持的所有股票、基金、指数、期货、期权信息  

# 参数  

types: list: 用来过滤securities 的类型, list 元素可选: 'stock','fund', 'index', 'futures', 'options', 'etf', 'lof', 'fja','fjb', 'open_fund', 'bond_fund', 'stock_fund', 'QDII_fund'(QDII基金), 'money_market_fund', 'mixture_fund'。 types 为空时返回所有股票, 不包括基金,指数和期货  

date: 日期, 一个字符串或者 datetime.datetime /datetime.date 对象, 用于获取某日期还在上市的股票信息. 默认值为 None, 表示获取所有日期的股票信息.建议使用时添加上指定date  

返回 [pandas.DataFrame], 比如:get_all_securities()[:2]返回:display_name name start_date end_date type  

000001.XSHE 平安银行 PAYH  1991-04-03  9999-01-01  stock  

000002.XSHE 万 科Ａ WKA 1991-01-29 9999-01-01  stock  

•  display_name: 中文名称,只返回最新的，判断是否st 请使用get_extras  
• name: 缩写简称，同上  
• start_date: 上市日期end_date: 退市日期（股票是最后一个交易日，不同于摘牌日期），如果没有退市则为2200-01-01；type: 类型，stock(股票)，index(指数)，etf(场内ETF 基金)，fja（场内分级A），fjb（场内分级B），fjm（场内分级母基金），mmf（场内交易的货币基金），lof（上市型开放基金），open_fund（开放式基金）, bond_fund（债券基金）, stock_fund（股票型基金）,money_market_fund（场外交易的货币基金）, mixture_fund（混合型基金）,fund_fund（联接基金) options(期权),  

示例 def initialize(context):  

#获得所有股票列表  

log.info(get_all_securities()) log.info(get_all_securities(['stock']))  

#将所有股票列表转换成数组  

stocks $=$ list(get_all_securities(['stock']).index)  

#获得所有指数列表  

get_all_securities(['index'])  

#获得所有基金列表  

df $=$ get_all_securities(['fund'])  

#获取所有期货列表  

get_all_securities(['futures'])  

#获取所有期货列表  

get_all_securities(['options'])  

#获得etf 基金列表  

df $=$ get_all_securities(['etf'])  

#获得lof 基金列表  

df $=$ get_all_securities(['lof'])#获得分级A 基金列表  
df $=$ get_all_securities(['fja'])#获得分级B 基金列表  
df $=$ get_all_securities(['fjb'])  

#获得2015 年10 月10 日还在上市的所有股票列表  

get_all_securities(date='2015-10-10')#获得2015 年10 月10 日还在上市的 etf 和 lof 基金列表get_all_securities(['etf', 'lof'], '2015-10-10')get_security_info 获取单个标的信息get_security_info(code, date $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ None)获取股票/基金/指数/期货的信息.  

# 参数  

code: 证券代码date：查询日期,默认为None，仅支持股票返回值一个对象, 有如下属性:  

o display_name: 中文名称  
o name: 缩写简称  
o start_date: 上市日期, [datetime.date] 类型end_date: 退市日期（股票是最后一个交易日，不同于摘牌日期）， [datetime.date] 类型, 如果没有退市则为2200-01-01type: 股票、基金、金融期货、期货、债券基金、股票基金、QDII 基金、货币基金、混合基金、场外基金，'stock'/ 'fund/ 'index_futures' / 'futures' / 'etf'/'bond_fund' /'stock_fund' / 'QDII_fund' / 'money_market_fund' /‘mixture_fund' / 'open_fundparent: 分级基金的母基金代码  

示例# 获取000001.XSHE 的上市时间  

start_date $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ get_security_info('000001.XSHE').start_date print(start_date)  

get_industry 查询股票所属行业get_industry(security, date $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ None)  

# 参数  

security：标的代码。类型为字符串，形式如"000001.XSHE"；或为包含标的代码字符串的列表，形如["000001.XSHE", "000002.XSHE"]date：查询的日期。类型为字符串，形如"2018-06-01"或"2018-06-01$09\!:\!00\!:\!00^{\prime\prime}$ ；或为datetime.datetime 对象和datetime.date。注意传入对象的时分秒将被忽略。默认值为None，研究中默认值为当天，回测中默认值会随着回测日期变化而变化, 等于context.current_dt。  

# 返回结果  

一个dict， key 是标的代码。  

# 示例  

>>> get_industry(security $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ ['000001.XSHE','000002.XSHE'], date $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ "2018-06-01")  

{'000001.XSHE': {'jq_l1': {'industry_code': 'HY007',   
'industry_name': '金融指数'}, 'jq_l2': {'industry_code': 'HY493',   
'industry_name': '多元化银行指数'}, 'sw_l1': {'industry_code': '801780',   
'industry_name': '银行I'}, 'sw_l2': {'industry_code': '801192',   
'industry_name': '银行II'}, 'sw_l3': {'industry_code': '851911',   
'industry_name': '银行III'}, 'zjw': {'industry_code': 'J66',   
'industry_name': '货币金融服务'} }, '000002.XSHE': {'jq_l1': {'industry_code': 'HY011',   
'industry_name': '房地产指数'}, 'jq_l2': {'industry_code': 'HY509',   
'industry_name': '房地产开发指数'}, 'sw_l1': {'industry_code': '801180',   
'industry_name': '房地产I'}, 'sw_l2': {'industry_code': '801181',   
'industry_name': '房地产开发II'}, 'sw_l3': {'industry_code': '851811',   
'industry_name': '房地产开发III'}, 'zjw': {'industry_code': 'K70',   
'industry_name': '房地产业'} }  

}  

# 注意  

# python2 中print 打印一个unicode 对象的时候，调用的是这个对象的"__str__"，而打印一个类似{"a": u"中文"}的时候，调用的是"__repr__"。因此可以这样使用：  

$r{\in}s_{}=$  

get_industry(security $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ ['000001.XSHE','000002.XSHE'],date $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ "2018-06-01")print(repr(res).decode("unicode-escape"))  

get_all_trade_days 获取所有交易日  

from jqdata import $\star$   
get_all_trade_days()  
获取所有交易日, 不需要传入参数, 返回一个包含所有交易日的numpy.ndarray, 每个元素为一个datetime.date 类型.  

注： 需导入 jqdata 模块，即在策略或研究起始位置加入import jqdata  

get_trade_days 获取指定范围交易日  
from jqdata import \*  
get_trade_days(start_date=None, end_date=None,  
count $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ None)  
获取指定日期范围内的所有交易日, 返回一个包含datetime.date object 的列  
表, 包含指定的 start_date 和 end_date, 默认返回至  
datetime.date.today() 的所有交易日  

注意get_trade_days 最多只能获取到截至现实时间的当前年份的最后一天的交易日数据  

注： 需导入 jqdata 模块，即在策略或研究起始位置加入import jqdata  

# 参数  

start_date: 开始日期, 与 count 二选一, 不可同时使用.  
str/datetime.date/datetime.datetime 对象  
end_date: 结束日期, str/datetime.date/datetime.datetime 对象,默认为 datetime.date.today()  
count: 数量, 与 start_date 二选一, 不可同时使用, 必须大于 0.表示取 end_date 往前的 count 个交易日，包含 end_date 当天。  

get_money_flow 获取资金流信息  

from jqdata import $\star$   
get_money_flow(security_list, start_date $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ None,  
end_date $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ None, fields $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ None, count $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ None)  
获取一只或者多只股票在一个时间段内的资金流向数据，仅包含股票数据，不可用于获取期货数据;  
提供2010 年至今的数据，数据频率为天;  
净额 : 为正是资金流入, 为负为资金流出;  

# 参数  

• security_list: 一只股票代码或者一个股票代码的 list  
• start_date: 开始日期, 与 count 二选一, 不可同时使用, 一个字符串或者 [datetime.datetime]/[datetime.date] 对象, 默认为平台提供的数据的最早日期end_date: 结束日期, 一个字符串或者datetime.date/datetime.datetime 对象, 默认为datetime.date.today()count: 数量, 与 start_date 二选一，不可同时使用, 必须大于 0.表示返回 end_date 之前 count 个交易日的数据, 包含 end_datefields: 字段名或者 list, 可选. 默认为 None, 表示取全部字段, 各字段含义如下：返回  
返回一个 pandas.DataFrame 对象，默认的列索引为取得的全部字段. 如果给定了 fields 参数, 则列索引与给定的 fields 对应.  

<html><body><table><tr><td>字段名</td><td>含义</td><td>备注</td></tr><tr><td>date</td><td>日期</td><td></td></tr><tr><td>sec_code</td><td>股票代码</td><td></td></tr><tr><td>change_pct</td><td>涨跌幅(%)</td><td></td></tr><tr><td>net_amount_main</td><td>主力净额 (万)</td><td>主力净额 = 超大单净额 +大单净额</td></tr><tr><td>net_pct_main</td><td>主力净占比 (%)</td><td>主力净占比=主力净额／成交额</td></tr><tr><td>net_amount_xl</td><td>超大单净额 (万)</td><td>超大单：大于等于50万股或者100万元的 成交单</td></tr><tr><td>net_pct_xl</td><td>超大单净占 比(%)</td><td>超大单净占比 =超大单净额／成交额</td></tr><tr><td>net_amount_1</td><td>大单净额 (万)</td><td>大单：大于等于10万股或者20万元且小于 50万股或者100万元的成交单</td></tr><tr><td>net_pct_1</td><td>大单净占比 (%)</td><td>大单净占比=大单净额／成交额</td></tr><tr><td>net_amount_m</td><td>中单净额 (万)</td><td>中单：大于等于2万股或者4万元且小于 10万股或者 20万元的成交单</td></tr><tr><td>net_pct_m</td><td>中单净占比 (%)</td><td>中单净占比=中单净额／成交额</td></tr><tr><td>net_amount_s</td><td>小单净额 (万)</td><td>小单：小于2万股或者4万元的成交单</td></tr><tr><td>net_pct_s</td><td>小单净占比 (%)</td><td>小单净占比=小单净额／成交额</td></tr></table></body></html>  

# 示例 from jqdata import \*  

# 获取一只股票在一个时间段内的资金流量数据get_money_flow('000001.XSHE', '2016-02-01', '2016-02-04')  

get_money_flow('000001.XSHE', '2015-10-01', '2015-12-30',   
fields $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ "change_pct")   
get_money_flow(['000001.XSHE'], '2010-01-01', '2010-01-   
30', ["date", "sec_code", "change_pct",   
"net_amount_main", "net_pct_l", "net_amount_m"])  

![](images/2115c39832a179a0ae3deda7751e14d1974e3b62fa30d24f13919d7937b359a6.jpg)  

# 获取多只股票在一个时间段内的资金流向数据get_money_flow(['000001.XSHE', '000040.XSHE','000099.XSHE'], '2010-01-01', '2010-01-30')  

# 获取多只股票在某一天的资金流向数据get_money_flow(['000001.XSHE', '000040.XSHE','000099.XSHE'], '2016-04-01', '2016-04-01')  

![](images/843fa698b2436ae11ca63fece7dd3c881e0375196edc529c8cb87165ce07d8aa.jpg)  

# 获取股票 000001.XSHE 在日期 2016-06-30 往前 20 个交易日的资金流量数据  

get_money_flow('000001.XSHE', end_date="2016-06-30", count $=2\,\odot$ )  

# 获取股票 000001.XSHE 往前 20 个交易日的资金流量数据get_money_flow('000001.XSHE', count=20)  

# 注意  

需要导入：from jqdata import \*在回测中，为避免未来函数，无法获取回测当前逻辑时间的那一条数据（所以有时会出现实际获取数据比count 少一条的现象）  

get_concept 获取股票所属概念板块  

# 数据调用方法  

get_concept(security, date $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ None)获取股票所属概念板块。返回一个dict，key 为标的代码，value 详见示例。  

security：标的代码或包含标的代码的列表  
query_dt：时刻,datetime 或时刻形式的字符串,只传入日期代表日内时间为00:00:00.  
security: 标的代码或标的列表  
date: 要查询的日期，日期字符串/date 对象/datetime 对象，注意传入datetime 对象时忽略日内时间；默认值为None，研究中默认值为当天，回测中默认值会随着回测日期变化而变化, 等于context.current_dt。示例：  
{code: { 'jq_concept':[{ 'concept_code': XX1; 'concept_name':  
YY1 },{ 'concept_code': XX2; 'concept_name':  
YY2 },{ 'concept_code': XX3; 'concept_name':  
YY3 }]}  

code 是传入的股票代码；多个code 返回嵌套的多个字典。 ‘jq_concept’代表聚宽概念； XX 是code 所在的概念代码； YY 是code 所在的概念名称。  

# 示例  

dict1 $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ get_concept('000001.XSHE', date $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ '2019-07-15') print(dict1)  

get_call_auction 获取指定时间区间内集合竞价时的 tick 数据获取指定时间区间内交易日09:25 的集合竞价数据，支持股票（2010 年至今）、场内基金（2019 年至今）、指数（2017 年至今）和上交所ETF 期权（2017 年至今）的集合竞价数据，当日的集合竞价数据最晚于9:28 分返回。  

# from jqdata import $\star$  

get_call_auction(security, start_date $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ None, end_date $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ None, fields $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ None)  

# 参数：  

security: 标的代码或者标的代码组成的列表,支持股票、指数、50ETF期权  

start_date: 开始日期，一个时间字符串, 比如"2019-01-01"  

end_date: 结束日期，一个时间字符, 比如"2019-02-01"  

fields: 选择要获取的行情字段(类似tick 数据的每一个字段)，字段介绍如下:  

<html><body><table><tr><td>字段名</td><td>说明</td><td>字段类型</td></tr><tr><td>time</td><td>时间</td><td>datetime</td></tr><tr><td>current</td><td>当前价</td><td>float</td></tr><tr><td>volume</td><td>累计成交量 (股)</td><td>float</td></tr><tr><td>money</td><td>累计成交额</td><td>float</td></tr><tr><td>b1_v~b5_v</td><td>五档买量</td><td>float</td></tr></table></body></html>  

<html><body><table><tr><td>字段名</td><td>说明</td><td>字段类型</td></tr><tr><td>b1_p~b5_p</td><td>五档买价</td><td>float</td></tr><tr><td>al_va5_</td><td>五档卖量</td><td>float</td></tr><tr><td>al_p~a5_p</td><td>五档卖价</td><td>float</td></tr></table></body></html>  

# 返回值  

返回一个dataframe，索引为pandas 默认的整数索引。  

# 注意  

fields 为None 的时候，默认获取全部字段；• start_date 和end_date 不能为None，否则将抛出异常；为了防止返回数据量过大, 我们每次最多返回5000 行；  

# 示例  

from jqdata import $\star$  

d $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ get_call_auction(['000001.XSHE', '000002.XSHE'],start_date='2019-01-01', end_date $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ '2019-10-10',fields $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ ['time', 'current', 'a1_v', 'b1_v'])print(d)  

code time current a1_v  

b1_v  

0 000001.XSHE 2019-01-02 09:25:03 9.3900 13400.0   
183300.0   
1 000001.XSHE 2019-01-03 09:25:03 9.1800 99200.0   
37200.0   
2 000001.XSHE 2019-01-04 09:25:03 9.2400 47000.0   
56500.0   
3 000001.XSHE 2019-01-07 09:25:03 9.8400 186300.0   
47300.0   
352  000002.XSHE 2019-09-19 09:25:03  27.0500 32300.0   
18200.0   
353  000002.XSHE 2019-09-20 09:25:03 26.8900 17280.0   
700.0   
354  000002.XSHE 2019-09-23 09:25:03  26.4900 199614.0   
32300.0   
355 000002.XSHE 2019-09-24 09:25:03  26.2400 701.0   
7300.0  

[356 rows x 5 columns]  

d = get_call_auction('000001.XSHE','2019-08-10','2019-08-   
20')   
print(d)  

code time  current a3_p a4_p   
a5_p   
0 000001.XSHE 2019-08-12 09:25:03 14.61 14.63   
14.64 14.65   
1 000001.XSHE 2019-08-13 09:25:03 15.00 15.02   
15.03 15.04   
2 000001.XSHE 2019-08-14 09:25:03 15.14 15.17   
15.18 15.19   
3 000001.XSHE 2019-08-15 09:25:03 14.64 14.66   
14.67  14.68   
4 000001.XSHE 2019-08-16 09:25:03 15.09 15.11   
15.12 15.13   
5 000001.XSHE 2019-08-19 09:25:03 14.91 14.93   
14.94 14.95   
6 000001.XSHE 2019-08-20 09:25:03 14.92 14.94   
14.95 14.96  

[7 rows x 25 columns]  

get_trade_day 根据标的获取指定时刻标的对应的交易日获取指定时刻标的对应的交易日。返回一个dict，key 为标的代码，value 为标的在此时刻对应的交易日。  

get_trade_day(security, query_dt)示例：  

>>> get_trade_day(["RB1901.XSGE", "000001.XSHE"],   
query_dt $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ "2019-01-04 22:00:00")   
{'RB1901.XSGE': datetime.date(2019, 1, 7), '000001.XSHE':   
datetime.date(2019, 1, 4)}  

备注  

对于A 股，交易日即为传入时刻的日期；  
对于有夜盘的交易标的：  
若传入时刻处于夜盘，则返回下一个交易日的日期对于错误的标的代码，抛出异常提示代码无效对于未上市或退市标的也返回None  
对于非交易日dt，返回None  

dt 不提供默认值交易日的定义：  

对于无夜盘品种，以每日0 点作为一个交易日的开始，至下一个交易日0 点结束；  

对于有夜盘品种，以夜盘集合竞价开始时作为一个交易日开始，至下一个交易日夜盘集合竞价开始时结束；  

如果传入的dt 在两个交易日之间，返回上一个交易日；  

get_history_fundamentals 获取多个季度/年度的历史财务数据获取多个季度/年度的三大财务报表和财务指标数据. 可指定单季度数据, 也可以指定年度数据。可以指定观察日期, 也可以指定最后一个报告期的结束日期get_history_fundamentals(security, fields,watch_date $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ None, stat_date $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ None, count $^{=1}$ , interval='1q',stat_by_year $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ False)  

# 参数  

security：股票代码或者股票代码列表。  
fields：要查询的财务数据的列表, 季度数据和年度数据可选择的列不同。示例：  
[balance.cash_equivalents, cash_flow.net_deposit_increase,income.total_operating_revenue]  
watch_date：观察日期, 如果指定, 将返回 watch_date 日期前(包含该日期)发布的报表数据  
stat_date：统计日期, 可以是 '2019'/'2019q1'/'2018q4' 格式, 如果指定, 将返回 stat_date 对应报告期及之前的历史报告期的报表数据o  watch_date 和 stat_date 只能指定一个, 而且必须指定一个o 如果没有 stat_date 指定报告期的数据, 则该数据会缺失一行.  

count：查询历史的多个报告期时, 指定的报告期数量. 如果股票历史报告期的数量小于 count, 则该股票返回的数据行数将小于 countinterval：查询多个报告期数据时, 指定报告期间隔, 可选值:  

'1q'/'1y', 表示间隔一季度或者一年, 举例说明:  

o stat_date $\mathrel{\mathop:}$ 2019q1', interval $\varDelta^{\gamma}$ 1q', count $\mathrel{=}4$ , 将返回2018q2,2018q3,2018q4,2019q1 的数据  
o stat_date $\mathbf{\omega}^{,}$ 2019q1', interval $\varDelta^{\gamma}$ 1y', count $=\!4$ , 将返回2016q1,2017q1,2018q1,2019q1 的数据  
o stat_by_year $\cdots$ True, stat_date $\varXi^{\prime}$ 2018', interval $\mathbf{\omega}^{,}$ 1y',count $=\!4$ 将返回 2015/2016/2017/2018 年度的年报数据  

stat_by_year：bool, 是否返回年度数据. 默认返回的按季度统计的数据(比如income 表中只有单个季度的利润).  

如果是True：  

interval 必须是 '1y如果指定了 stat_date 的话, stat_date 必须是一个代表年份整数、字符串, 表明统计的年份，比如2019,$\prime2019^{\prime\prime}$ 。但不能是"20191q"这种格式。fields 可以选择balance/income/cash_flow/indicator/bank_indicator/security_indicator/insurance_indicator 表中的列如果是False：fields 只能选择balance/income/cash_flow/indicator 表中的列  

# 返回值  

pandas.DataFrame, 数据库查询结果. 数据格式同 get_fundamentals. 每个股票每个报告期(一季度或者一年)的数据占用一行.  

# 注意  

不支持valuation 市值表推荐用户对结果使用pandas 的groupby 方法来进行分组分析数据每次最多返回5000 条数据，更多数据需要根据标的或者时间分多次获取  

# 示例  

from jqdata import $\star$   
security $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ ['000001.XSHE', '600000.XSHG']   
df $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ get_history_fundamentals(security,   
fields $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ [balance.cash_equivalents, cash_flow.net_deposit_increase,   
income.total_operating_revenue], watch_date $=$ None, stat_date $=$ '2019q1', count $^{=5}$ ,   
interval='1q', stat_by_year=False)   
print(df)   
print(df.groupby('code').mean())   
get_valuation 获取多个标的在指定交易日范围内的市值表数据   
from jqdata import $\star$   
get_valuation(security, start_date=None, end_date $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ None,   
fields $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ None, count $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ None)   
获取多个标的在指定交易日范围内的市值表数据  

# 参数  

•  security: 标的code 字符串列表或者单个标的字符串  
• end_date: 查询结束时间  
• start_date: 查询开始时间，不能与count 共用count: 表示往前查询每一个标的count 个交易日的数据，如果期间标的停牌，则该标的返回的市值数据数量小于countfields: 财务数据中市值表的字段，返回结果中总会包含code、day 字段，可用字段如下： |code| 股票代码 带后缀.XSHE/.XSHG| |day |日  

期 取数据的日期| | capitalization |总股本(万股)||circulating_cap| 流通股本(万股)| |market_cap |总市值(亿元)||circulating_market_cap| 流通市值(亿元)| |turnover_ratio |换手率(%)| |pe_ratio |市盈率(PE, TTM)| |pe_ratio_lyr |市盈率(PE)||pb_ratio |市净率(PB)| | ps_ratio| 市销率(PS, TTM)| |pcf_ratio|市现率(PCF, 现金净流量TTM)|  

# 返回值  

返回一个dataframe，索引默认是pandas 的整数索引，返回的结果中总会包含code、day 字段。  

# 注意  

每次最多返回5000 条数据，更多数据需要根据标的或者时间分多次获取  

# from jqdata import $\star$  

# 传入单个标的  

df1 $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ get_valuation('000001.XSHE', end_date $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ "2019-11-18", count $^{=3}$ , fields $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ ['capitalization', 'market_cap']) print(df1)  

# 传入多个标的  

df2 $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ get_valuation(['000001.XSHE', '000002.XSHE'],   
end_date $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ "2019-11-18", count $^{=3}$ , fields $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ ['capitalization',   
'market_cap'])   
print(df2)  

# jqlib  

名称 描述  

alpha101 Alpha 101 因子alpha191 Alpha 191 因子technical_analysis 技术分析指标  

# 数据处理函数  

名称 描述  

neutralize 中性化  

neutralize(series, how $^1=$ None, date $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ None, axi $s{=}1$ , fillna $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ None, add_constant $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ False)  

# 参数  

data: pd.Series/pd.DataFrame , 待中性化的序列，序列的 index 为股票的 code  

how: str list 。 中性化使用的因子名称列表。默认为 ['jq_l1','market_cap'] 支持的内容包括：  

财务数据：如 'market_cap', 'net_profit'等；也可以输入对数市值'ln_market_cap' 和 对数流通市值'ln_circulating_market_cap';行业数据：可输入行业分类代码（如 'jq_l1', 'sw_l1'）或行业代码（如 'HY001'）行业代码分类会被替换为行业代码，例如输入 how $\leftharpoondown$ ['jq_l1'] 和how $=$ ['HY001','HY002','HY003','HY004','HY005','HY006','HY007', 'HY008','HY009','HY010','HY011'] 是等价的'jq_l1'： 聚宽一级行业■ 'jq_l2'： 聚宽二级行业■ 'sw_l1'： 申万一级行业sw_l2'： 申万二级行业sw_l3'： 申万三级行业  
o 聚宽因子库因子名称，如 'operating_profit_ttm', 'VOL240'  
o 风险因子：可以使用的风险因子包括： ['size', 'beta','momentum', 'residual_volatility', 'non_linear_size''book_to_price_ratio', 'liquidity', 'earnings_yield',growth', 'leverage']  

date: 日期格式 str 将用 date 这天的相关变量数据对 series 进行中性化；请注意date 不要为实时数据中的天（例如设置  

date $=$ datetime.date.today())，因为此时处理依赖的当天财务数据还没有更新，默认依赖数据为Nan；如果依赖数据为Nan , 直接忽略,返回原始数据, 不中性化；  

axis: 默认为 1。仅在 data 为 pd.DataFrame 时生效。 表示沿哪个方向做中性化，0 为对每列做中性化，1 为对每行做中性化  

•  fillna: 缺失值填充方式，默认为None，表示不填充。支持的值：  

o 'jq_l1'： 聚宽一级行业  
o 'jq_l2'： 聚宽二级行业  
o sw_l1'： 申万一级行业  
o 'sw_l2'： 申万二级行业  
o sw_l3'： 申万三级行业 表示使用某行业分类的均值进行填充。  

add_constant: 中性化时是否添加常数项, 默认为 False  

示例  

# 导入需要的函数库  

import pandas as pd   
import numpy as np   
from jqfactor import neutralize  

# 生成数据  

data $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ pd.DataFrame(np.random.rand(3,300), columns $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ get_index_stocks('000300.XSHG', date $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ '2018-05- 02'),index $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ ['a', 'b', 'c'])  

# 数据中性化  

neutralize(data, $\mathsf{h o w}\!=\![\mathsf{\Omega}^{\prime}\,\mathsf{j}\,\mathsf{q}_{-}\mathsf{1}\,\mathsf{1}\,^{\prime}$ , 'market_cap'], date $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ '2018- 05-02', axi $s{=}1$ )  

winsorize 去极值  

winsorize(series, scale $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ None, range $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ None, qrange $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ None, inclusive $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ True, inf2nan $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ True, axis $^{=1}$ )  

# 参数  

•  data: pd.Series/pd.DataFrame/np.array, 待缩尾的序列  
• scale: 标准差倍数，与 range，qrange 三选一，不可同时使用。会将位于 [mu - scale \* sigma, mu $^{+}$ scale \* sigma] 边界之外的值替换为边界值range: 列表， 缩尾的上下边界。与 scale，qrange 三选一，不可同时使用。  
• qrange: 列表，缩尾的上下分位数边界，值应在 0 到 1 之间，如[0.05, 0.95]。与 scale，range 三选一，不可同时使用。inclusive: 是否将位于边界之外的值替换为边界值，默认为 True。如果为 True，则将边界之外的值替换为边界值，否则则替换为 np.naninf2nan: 是否将 np.inf 和 -np.inf 替换成 np.nan，默认为 True 如果为 True，在缩尾之前会先将 np.inf 和 -np.inf 替换成 np.nan，缩尾的时候不会考虑 np.nan，否则 inf 被认为是在上界之上，-inf 被认为在下界之下axis: 在 data 为 pd.DataFrame 时使用，沿哪个方向做标准化，默认为 1。 0 为对每列做缩尾，1 为对每行做缩尾。  

# 返回  

去极值处理之后的因子数据  

示例# 导入需要的函数库  

import pandas as pd   
import numpy as np   
from jqfactor import winsorize  

# 生成数据  

data $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ pd.DataFrame(np.random.rand(3,300), columns=get_index_stocks('000300.XSHG', date $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ '2018-05- 02'),index $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ ['a', 'b', 'c'])  

# 数据去极值  

winsorize(data, $\mathtt{q r a n g e=}[\Theta\,.\,\Theta5\,,\Theta\,.\,\Theta3]$ , inclusive=True, inf2nan $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ True, axis $^{=1}$ )  

winsorize_med 中位数去极值  

winsorize_med(series, scale=1, inclusive $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ True, inf2nan $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ True, axi $s{=}1$ )  

# 参数  

•  data: pd.Series/pd.DataFrame/np.array, 待缩尾的序列  
• scale: 倍数，默认为 1.0。会将位于 [med - scale \* distance, med$^+$ scale \* distance] 边界之外的值替换为边界值/np.naninclusive bool 是否将位于边界之外的值替换为边界值，默认为True。 如果为 True，则将边界之外的值替换为边界值，否则则替换为np.naninf2nan: 是否将 np.inf 和 -np.inf 替换成 np.nan，默认为 True。如果为 True，在缩尾之前会先将 np.inf 和 -np.inf 替换成 np.nan，缩尾的时候不会考虑 np.nan，否则 inf 被认为是在上界之上，-inf 被认为在下界之下axis: 在 data 为 pd.DataFrame 时使用，沿哪个方向做标准化，默认为 1。0 为对每列做缩尾，1 为对每行做缩尾  

返回中位数去极值之后的因子数据示例# 导入需要的函数库  

import pandas as pd   
import numpy as np   
from jqfactor import winsorize_med  

# 生成数据  

data $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ pd.DataFrame(np.random.rand(3,300), columns=get_index_stocks('000300.XSHG', date $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ '2018-05- 02'),index $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ ['a', 'b', 'c'])  

# 数据中位数去极值  

winsorize_med(data, scale=1, inclusive $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ True, inf2nan $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ True, axi $\scriptstyle{\mathsf{S}}=\left\emptyset$ )  

standardlize 标准化(z-score)  

standardlize(series, inf2nan $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ True, axi $s{=}1$ )  

# 参数  

data: pd.Series/pd.DataFrame/np.array, 待标准化的序列• inf2nan: 是否将 np.inf 和 -np.inf 替换成 np.nan。默认为 Trueaxis $\mathrel{\mathop:}=1$ : 在 data 为 pd.DataFrame 时使用，如果 series 为pd.DataFrame，沿哪个方向做标准化。0 为对每列做标准化，1 为对每行做标准化  

# 返回  

标准化后的因子数据  

示例# 导入需要的函数库  

import pandas as pd   
import numpy as np   
from jqfactor import standardlize  

# 生成数据  

data $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ pd.DataFrame(np.random.rand(3,300), columns $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ get_index_stocks('000300.XSHG', date $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ '2018-05- 02'),index $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ ['a', 'b', 'c'])  

# 数据标准化  

standardlize(data, inf2nan $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ True, axi $\scriptstyle{\mathsf{S}}=\left\emptyset$ )  

# 组合优化函数  

portfolio_optimizer - 投资组合优化 portfolio_optimizer(date, securities, target, constraints, bounds $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ [Bound(0.0, 1.0)], default_port_weight_range $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ [0.0, 1.0], ftol=1e-9, return_none_if_fail $\cdot\,$ True)  

优化函数, 用于计算在某些约束条件下的最优组合权重  

# 参数  

date: 优化发生的日期，请注意未来函数  
o securities: 股票代码列表  
target: 优化目标函数，只能选择一个，目标函数详见下方  
o constraints: 限制函数，用以对组合总权重进行限制，可设置一个或多个相同/不同类别的函数，限制函数详见下方  
bounds: 边界函数，用以对组合中单标的权重进行限制，可设置一个或多个相同/不同类别的函数，边界函数详见下方。如果不填，默认为 Bound(0., 1.)；如果有多个 bound，则一只股票的权重下限取所有 Bound 的最大值，上限取所有 Bound 的最小值  

o  default_port_weight_range: 长度为2 的列表，默认的组合权重之和的范围，默认值为 [0.0, 1.0]。如果限制函数(constraints) 中没有 WeightConstraint 或 WeightEqualConstraint 限制，则会添加 WeightConstraint(low $=$ default_port_weight_range[0],high $=$ default_port_weight_range[1]) 到 constraints 列表中。  

ftol: 默认为 1e-9，优化函数触发结束的函数值。当求解结果精度不够时可以适当降低 ftol 的值，当求解时间过长时可以适当提高 ftol 值  

return_none_if_fail: 默认为 True，如果优化失败，当return_none_if_fail 为 True 时返回 None，为 False 时返回全为0 的组合权重  

# 相关参数  

# 参数名称 描述  

目标函数(target) 优化目标函数，只能选择一个  

MinVariance(count $=\!250$ ) - 组合风险最小化（最小化组合方差）最小化组合方差参数：count: 默认为 250，向前取 returns 的天数示例：target $=$ MinVariance(count $=\!250$ )  
MaxProfit(count $\it{\Delta}=250_{\cdot}$ ) - 组合收益最大化o  参数：count: 默认为 250，向前取 returns 的天数  

o 示例：  

target $=$ MaxProfit(count $=\!250\!\!\!$ )  

MaxSharpeRatio( $\mathrm{\stackrel{\rf=}{1}}0.\,0$ , weight_sum_equal $=\!1.0$ , count $=\!250$ ) - 组合夏普比率最大化  

rf: 年化无风险利率，默认为 0weight_sum_equal：组合总权重的值（默认值为1.0），在该权重下进行优化，使得组合的夏普比率最大化count: 默认为 250，向前取 returns 的天数o  示例：target $=$ MaxSharpeRatio(count $=\!250$ )  

MinTrackingError(benchmark, count $\it{\Delta}=250_{\cdot}$ ) - 追踪误差最小化  

参数：  

benchmark: 基准的 ticker，例如 '000300.XSHG  
count: 默认为 250，向前取 returns 的天数  
示例：  
target $=$ MinTrackingError(benchmark $\supseteq^{\bullet}$ 000300.XSHG',  
count $=\!250$ )  

RiskParity(count $=\!250$ , risk_budget=None) - 风险平价风险平价（Risk Parity）是对投资组合中不同资产分配相同的风险权重的一种资产配置理念，资产配置的风险平价方法允许投资者针对具体的风险水平，并在整个投资组合中平均分配风险，以实现每个投资者的最佳投资组合多元化。  

参数：  

count: 默认为 250，向前取 returns 的天数risk_budget: pandas.Series，风险预算，股票的每只对组合风险的贡献，risk_budget 为 None 默认为每只股票贡献相等  

# 示例：  

target $=$ RiskParity(count $=\!250$ ,   
risk_budget=pd.Series([0.3, 0.3, 0.4],   
index $\because$ ['000001.XSHE', '000002.XSHE', '000005.XSHE']))  

MaxScore(scores) - 打分最大化在满足约束条件的情况下，给予打分高的标的更高权重（前提假设：用户已知晓打分大的标的表现更好）。  

如有经过因子分析检验，打分越高越有正向效果的[A,B,C] 三只标的，打分分别为 [3,2,1] , 约束条件为年化波动率小于 $15\%$ 。 如果组合全部配置A 可获得最高的收益，但波动率大于 $15\%$ ，不满足约束条件；通过优化器优化，则会配置一定比例的B 与C，在满足波动率小于 $15\%$ 的条件下，获得最高收益。  

# 参数：  

scores: pandas.Series，每只股票的打分  

o 示例：  

target $=$ MaxScore(scores=pd.Series([0.1, 0.2, 0.3], index $\equiv$ ['000001.XSHE', '000002.XSHE', '000005.XSHE']))  

MinScore(scores) - 打分最小化  

在满足约束条件的情况下，给予打分低的标的更高权重（前提假设：用户已知晓打分小的标的表现更好）。可参考 [打分最大化] 的示例说明。  

# o  参数：  

scores: pandas.Series，每只股票的打分  

示例：  

target $=$ MinScore(scores=pd.Series([0.1, 0.2, 0.3], index $\equiv$ ['000001.XSHE', '000002.XSHE', '000005.XSHE']))  

MaxFactorValue(factor, count $=\!1$ ) - 因子值最大化(只支持股票)  

在满足约束条件的情况下，给予因子值大的标的更高权重（前提假设：用户已知晓因子值大的标的表现更好）。可参考 [打分最大化] 的示例说明。  

o  参数：factor: Factor 的子类count: 默认为 1，用过去几天的因子取平均示例：  

from jqfactor import Factor  
# 定义因子：人气指标5 日均值  
class AR(Factor):name $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ 'AR_M5'# 每天获取过去五日的数据max_window $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ 5# 获取的数据是人气指标dependencies $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ ['AR']def calc(self, data):return data['AR'].mean()  
target $=$ MaxFactorValue(factor=AR, count $^{=1}$ )  

MinFactorValue(factor, count $=\!1$ ) - 因子值最小化(只支持股票)  

在满足约束条件的情况下，给予因子值小的标的更高权重（前提假设：用户已知晓因子值小的标的表现更好）。可参考 [打分最大化] 的示例说明。  

# o  参数：  

factor: Factor 的子类  
count: 默认为 1，用过去几天的因子取平均  
示例：  
参考 [因子值最大化] 的示例  

限制函数(constraints) 用以对组合总权重进行限制，可设置一个或多个相同/不同类别的函数  

WeightConstraint( $\mathrm{1ow}{=}0.\ 0$ , high=1.0) - 组合总权重限制设定组合优化结果总权重的上下限，即优化结果的总权重在此范围间。  

o  参数：  

low: 默认为 0.0，权重下限 high: 默认为 1.0，权重上限 示例： constraint $=$ WeightConstraint( $10\mathrm{w}{=}0.\ 5$ , high=0.9)  

WeightEqualConstraint(limit=1.0) - 组合总权重和限制设定组合优化结果总权重的和，即优化结果的总权重等于该值。  

o 参数： limit: 默认为 1.0，组合权重等式约束 示例： constraint $=$ WeightEqualConstraint(limit=0.5)  

AnnualStdConstraint(limit, count $=\!250$ ) - 组合年化收益率标准差限制  

o  参数：limit: 标准差上限count: 默认为 250，向前取 returns 的天数示例：constraint $=$ AnnualStdConstraint(limit=0.15, count $=\!250$ )  

AnnualProfitConstraint(limit, count $=\!250$ ) - 组合年化收益率预期限  
制o  参数：limit: 收益率预期下限count: 默认为 250，向前取 returns 的天数o  示例：constraint $=$ AnnualProfitConstraint(limit $\it=0.1$ , count $=\!250$ )  

IndustryConstraint(industry_code, $1\,\mathrm{ow}{=}0.\;0$ , high $\scriptstyle=1.\;0$ ) - 组合行业权重限制  

o  参数：  

industry_code: 单一或多个行业代码，如 'HY001'。如果为多个  
行业代码的列表，则表示所有属于列表中行业的股票的权重之和  
满足限制条件  
low: 默认为 0.0，行业权重下限  
high: 默认为 1.0，行业权重上限  
示例：  
constraint $=$ IndustryConstraint(['HY007'], $10\mathrm{w}{=}0.\ 0,$ ,  
high $\scriptstyle\lvert=0.\;2$ )  

IndustriesConstraint(industry_code, low=0.0, high=1.0)- 组合行业分类权重限制  

参数：  

industry_code: 行业分类代码，如 'jq_l1'。表示这个行业分  
类下的所有行业都需满足权重限制  
low: 默认为 0.0，行业权重下限  
high: 默认为 1.0，行业权重上限  
示例  

constraint $=$ IndustriesConstraint('jq_l1', low=0.0, high $\scriptstyle\lvert=0.\;2$ )  

•  MarketConstraint(market_type, low=0.0, high=1.0) - 组合市场权重限制  

o  参数：  

market_type: ('stock', 'index', 'fund', 'futures', 'etf',  
'lof', 'fja', 'fjb', 'open_fund', 'bond_fund',  
'stock_fund', 'QDII_fund', 'money_market_fund',  
'mixture_fund') 中的一种  
low: 默认为 0.0，市场权重下限  
high: 默认为 1.0，市场权重上限  
示例：  
constraint $=$ MarketConstraint('stock', $1_{\mathrm{OW}}{=}0.\ 0$ , high=0.2)  

ExposureConstraint(factor, low=0.0, high=1.0, count=1) - 因子暴露限制  

o 参数：factor: Factor 的子类low: 默认为 0.0，因子暴露度下限high: 默认为 1.0，因子暴露度上限count: 默认为 1，用过去几天的因子取平均  
o 示例：  
from jqfactor import Factor  
# 定义因子：人气指标5 日均值  
class AR(Factor):name $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ 'AR_M5'# 每天获取过去五日的数据max_window $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ 5# 获取的数据是人气指标dependencies $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ ['AR']def calc(self, data):return data['AR'].mean()  

constraint $=$ ExposureConstraint(AR, ${\sf1}_{0}{\bf w}{=}\odot.\odot$ , high $=\!\!1\!\,\Theta\cdot\Theta$ , count $^{=1}$ )  

风险暴露限制函数 - BarraConstraint(size $:=$ None, beta $\equiv$ None, momentum=None, residual_volatility $=$ None, no_linear_size $=$ None, book_to_price $=$ None, liquidity $:=$ None, earning_yield $\equiv$ None, growth $\equiv$ None, leverage $=$ None, standardlize $=$ True, winsorize $=$ True)  

参数：  

# 其中  

size/beta/momentum/residual_volatility/no_linear_si ze/book_to_price/liquidity/earning_yield/growth/lev erage  

分别代表'市值因子'/'贝塔因子'/'动量因子'/'残差波动因子'/'非线性市值因子'/'账面市值比因子'/'流动性因子'/'盈利预期因子'/'成长因子'/'杠杆因子'；需传入长度为2 的列表, 代表对应因子的上下限,如 [-0.5, 0.5], 默认为 None, 即无限制  

standardlize: 是否对因子值进行标准化处理, 默认为True  
winsorize: 是否对因子值去极值, 默认为 True, 即将因子值 [MED-3MEDMED, MED+3MEDMED] 之外的因子值赋成边界值 (MED 为因子值的中位数, MEDMED 为 ABS(因子值-MED) 的中位数)  

o 示例：  

constraint $=$ BarraConstraint(size=[-0.5, 0.5], beta $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ [None, 1.5], winsorize $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ False)  

IndustryDeviationConstraint - 行业偏离度限制某一行业权重与基准权重偏离度限制  

IndustryDeviationConstraint(industry_code, benchmark, limit)  

参数：  

industry_code: 单一行业代码或者行业代码的列表，如'HY001'。  
benchmark: 基准指数代码  
limit: 偏离度限制  
例子：  
constraint $=$   
IndustryDeviationConstraint(industry_code $\supseteq^{\bullet}$ 'HY001',benchmark $\omega$ 000300.XSHG', limit=0.05)  

IndustriesDeviationConstraint - 行业分类偏离度限制行业分类权重与基准权重偏离度限制  

IndustriesDeviationConstraint(industry_code, benchmark, limit)  

参数：  

industry_code: 行业分类代码，如 'jq_l1'。表示这个行业分类下的所有行业都需满足权重限制benchmark: 基准指数代码limit: 偏离度限制例子：  

constraint $=$   
IndustriesDeviationConstraint(industry_code $\varDelta^{\gamma}$ HY001',   
benchmark $\omega$ 000300.XSHG', limit=0.05)  

TrackingErrorConstraint - 追踪误差限制参数：benchmark: 基准的 ticker，例如 '000001.XSHElimit: (年化)追踪误差限制count: 默认为 250，向前取 returns 的天数例子：constraint $=$ TrackingErrorConstraint(benchmark $\omega$ '000001.XSHE',limit $\it=0.1$ , count $=\!250$ )  

TurnoverConstraint - 换手率限制  

TurnoverConstraint(limit, current_portfolio $\div$ None)  

o  参数：limit: 换手率限制current_portfolio: 默认为 None，当前投资组合权重，如果为None 则认为是空仓例子：constraint $=$ TurnoverConstraint(limit ${=}0.\,5$ ,current_portfolio $,=$ pd.Series([0.1, 0.2, 0.3, 0.4],index $\equiv$ ['000001.XSHE', '000002.XSHE', '000004.XSHE','000005.XSHE']))  

RatioConstraint - 比率限制  

RatioConstraint(ratio, low $\fallingdotseq$ None, high $\equiv$ None, rf $\leftoverleftarrow{}$ None, benchmark $\equiv$ None, count $=\!250_{\cdot}$ )  

o 参数：  

ratio: 比率名称，可选 "sharpe_ratio" /"information_ratio" / "calmar_ratio" / "omega_ratio" /"sortino_ratio" / "var" / "cvar"low: 默认为 None，比率的下限，如果为 None 则无下限high: 默认为 None，比率的上限，如果为 None 则无上限rf: 默认为 None, 无风险利率，适用于 "sharpe_ratio" /"omega_ratio"，如果为 None 则认为是 0benchmark: 默认为 None, 基准，适用于"information_ratio"。如果为 None 则认为是 '000300.XSHGcount: 默认为 250，向前取 returns 的天数o  例子：constraint $=$ RatioConstraint('var', low=-0.03)constraint $=$ RatioConstraint('sharpe_ratio', $\mathrm{1ow}{=}1$ ,$_\mathrm{rf=0.}\,02$ , count $\,=\!300$ )MaxDrawdownConstraint(limit, count $=\!250$ ) - 最大回撤限制o  参数：limit: 最大回撤限制，如 $-0.\;25$  

count: 默认为 250，向前取 returns 的天数  

例子：  

边界函数(bounds) 用以对组合中单标的权重进行限制，可设置一个或多个相同/不同类别的函数  

Bound $\langle\mathrm{low}{=}0.\ 0$ , $\mathrm{{high}}\mathrm{{=}}1.\,0.$ ) - 每只标的的权重限制  

# o  参数：  

low: 默认为 0.0，每只标的的权重下限high: 默认为 1.0，每只标的的权重上限  

示例：  

bound $=$ Bound(low=0.0, high=0.1)  

IndustryBound(industry_code, low=0.0, high=1.0) - 属于某一行业的每只股票的权重限制  

参数：  

industry_code: 单一行业代码或者行业代码的列表。  
low: 默认为 0.0，如果一只股票属于所选行业，则股票权重的下限为 low，否则下限为 0  
high: 默认为 1.0，如果一只股票属于所选行业，则股票权重的上限为 high，否则上限为 1  
示例：  
bound $=$ IndustryBound(['HY001', 'HY007'], low=0.0,  
high $\left.=0.\ 05\right.$ )  

LiquidityBound(limit, capital, count $\left.=1\right.$ , subset=None) - 流动性限 制  

购买数量不超过成交量的百分比  

参数：  

limit: 成交量百分比限制，如 0.5capital: 目前可用资金，如 1000000count: 前几个交易日的平均成交量，默认为 1subset: 股票代码的列表，限制只有特定的股票需要满足流动性限制，如 ['000001.XSHE', '000002.XSHE']，默认为 None，即所有股票都要满足流动性限制  
o 例子：  
o bound $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ LiquidityBound(0.5, capital=1000000)  
o  
o bound $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ LiquidityBound(0.25, capital $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ 1000000,count $^{=5}$ , subset $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ ['000001.XSHE', '000002.XSHE'])  

CapBound(limit, capital, count $=\!1$ , subset=None) - 市值限制  

购买金额不超过总市值的百分比  

参数：  

limit: 市值百分比限制，如 0.025  
capital: 目前可用资金，如 100000000  

count: 前几个交易日的平均市值，默认为 1subset: 股票代码的列表，限制只有特定的股票需要满足市值限制，如 ['000001.XSHE', '000002.XSHE']，默认为 None，即所有股票都要满足市值限制  

# o 例子：  

bound $=$ CapBound(0.025, capital $=$ 100000000,subset $=$ ['000001.XSHE', '000002.XSHE'])  

示例代码 给了五个应用示例，修改参数即可生效  

# 导入函数库  

import pandas as pdfrom jqdata import $\star$ from jqfactor import Factorfrom jqlib.optimizer import \*# 初始化函数，设定基准等等def initialize(context):  

# 设定沪深300 作为基准  
set_benchmark('000300.XSHG')  
# 开启动态复权模式(真实价格)  
set_option('use_real_price', True)  

# 过滤掉order 系列API 产生的比error 级别低的log# log.set_level('order', 'error')  

### 股票相关设定 ### # 股票类每笔交易时的手续费是：买入时佣金万分之三，卖出时佣金万分   
之三加千分之一印花税, 每笔交易佣金最低扣5 块钱 set_order_cost(OrderCost(close_tax=0.001,   
open_commission $=\odot$ .0003, close_commission $=\odot$ .0003, min_commission $^{=5}$ ), type $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ 'stock')  

# 优化器设置  

optimize_model $=$ {1:"模型1：等权重配置",2:"模型2：组合风险平价；股票的总权重限制为0到 $9\Theta_{\prime0}^{\circ\prime}$ ，ETF 的总权重限制为0 到 $\tt16\%$ ；每只标的权重不超过 $\tt{1070}^{11}$ ,  

3:"模型3：组合风险最小化（最小化组合方差）；组合总权重限制为90%到100%；组合年化收益率目标下限为10%",4:"模型4：'人气指标5 日均值'最大化；组合年化收益率目标下限为 $\tt16\%$ ；每只标的权重不超过 $2\Theta_{\prime0}^{\circ\prime\prime1\prime}$ ,5:"模型5：组合夏普比率最大化；每只标的权重不超过 $\tt{10\%^{\prime\prime}}$  

print("优化%s"%(optimize_model[g.optimizer]))  

## 运行函数（reference_security 为运行时间的参考标的；传入的标的只做种类区分，因此传入'000300.XSHG'或'510300.XSHG'是一样的）# 开盘前运行run_monthly(before_market_open, monthday $^{=1}$ ,time $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ '09:00', reference_security $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ '000300.XSHG')# 开盘运行run_monthly(market_open, monthday $^{=1}$ , time $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ '09:30',reference_security='000300.XSHG')  

## 开盘前运行函数  

def before_market_open(context):print('调仓日期：%s'%context.current_dt.date())  

# 选出上证50 成分股的一部分与选定的ETF 基金进行组合,构成股票池。  

etf = [ '159902.XSHE' '159903.XSHE' '510050.XSHG' '510880.XSHG' '510440.XSHG  

g.buy_list $=$ list(get_index_stocks('000016.XSHG')[- 15:]) $^+$ etf  

## 开盘时运行函数def market_open(context):  

# 将不在股票池中的股票卖出  

sell_list $=$ set(context.portfolio.positions.keys()) - set(g.buy_list) for stock in sell_list: order_target_value(stock, 0)  

# 组合优化模型 if g.optimizer $\mathbf{\tau}=\mathbf{\tau}\perp$ :  

# 模型1：等权重配置optimized_weight $=$  

pd.Series(data $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ [1.0/len(g.buy_list)]\*len(g.buy_list), index $=\!\mathrm{g}$ .buy_list) elif g.optimizer $\qquad\qquad\qquad\qquad\qquad\qquad\qquad=\quad2\qquad$ : # 模型2：组合风险平价；股票的总权重限制为0 到90%，ETF 的总   
权重限制为0 到 $\underline{{\boldsymbol{1}}}\,\underline{{\boldsymbol{\Theta}}}_{\boldsymbol{0}}^{\boldsymbol{0}\prime}$ ；每只标的权重不超过 $\underline{{\boldsymbol{1}}}\,\underline{{\boldsymbol{\Theta}}}_{\boldsymbol{0}}^{\boldsymbol{0}\prime}$ optimized_weight $=$   
portfolio_optimizer(date $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ context.previous_date, securities $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ g.buy_list, target $\underline{{\underline{{\mathbf{\delta\pi}}}}}$   
RiskParity(count $=\mathtt{250}$ , risk_budget $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ None),# risk_budget 为   
None 默认为每只股票贡献相等 constraints $\underline{{\underline{{\mathbf{\delta\pi}}}}}$   
[MarketConstraint('stock', ${\sf10w=\odot.\odot}$ , high $=\!\left(\cdot\right.9$ ),   
MarketConstraint('etf', ${\sf10w=\odot.\odot}$ , high=0.1)], bounds $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ [Bound(0, 0.1)],   
default_port_weight_range $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ [0., 1.0], $+\mathtt{t o l=1e-}\Theta3$ , return_none_if_fail $\cdot\,$ True) elif g.optimizer $\qquad\qquad\qquad\qquad\qquad\qquad=\qquad\qquad3$ : # 模型3：组合风险最小化（最小化组合方差）；组合总权重限制为   
90%到100%；组合年化收益率目标下限为10%  

optimized_weight $=$ portfolio_optimizer(date $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ context.previous_date, securities $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ g.buy_list, target $\underline{{\underline{{\mathbf{\delta\pi}}}}}$  

MinVariance(count $=\mathtt{250}$ ), [WeightConstraint( $\scriptstyle\mathtt{10w=0.9}$ , high=1.0),  

AnnualProfitConstraint(limit $\operatorname{\mu=0}\cdot1$ , count $=\!25\!\,\mathrm{6}$ )], bound $\mathfrak{s}\!=\![\,]$ ,  

default_port_weight_range $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ [0., 1.0], ftol=1e-09, return_none_if_fail $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ True)  

elif g.optimizer $\mathit{\Theta}=\mathit{\Theta}4$ :# 模型4：组合标的因子值最大化# 定义因子：人气指标5 日均值class AR(Factor):  

name $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ 'ar'  
# 每天获取过去五日的数据  
max_window $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ 5  
# 获取的数据是人气指标  
dependencies $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ ['AR']  
def calc(self, data):return data['AR'].mean()  

# 模型4：'人气指标5 日均值'最大化；组合年化收益率目标下限为10%；每只标的权重不超过 $2\lvert\boldsymbol{\Theta}_{\boldsymbol{\cdot}0}^{0\prime}$ optimized_weight $=$  

portfolio_optimizer(date $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ context.previous_date, securities $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ g.buy_list, target $\underline{{\underline{{\mathbf{\delta\pi}}}}}$   
MaxFactorValue(factor=AR, count $^{=1}$ ), constraints $\underline{{\underline{{\mathbf{\delta\pi}}}}}$   
[AnnualProfitConstraint(limit $=\!\left(\cdot\right.2$ , count $=\mathtt{250}$ )], bounds $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ [Bound(0, 0.2)],  

default_port_weight_range $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ [0., 1.0], ftol=1e-09, return_none_if_fail $\cdot\,$ True)  

lif g.optimizer $\mathit{\Theta}=\mathit{\Theta}\;5$ :# 模型5：组合夏普比率最大化；每只标的权重不超过 $\underline{{\boldsymbol{1}}}\,\underline{{\boldsymbol{\Theta}}}_{\boldsymbol{0}}^{\boldsymbol{0}\prime}$ optimized_weight $=$  

portfolio_optimizer(date $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ context.previous_date, securities $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ g.buy_list, target $\underline{{\underline{{\mathbf{\delta\pi}}}}}$  

MaxSharpeRatio(rf=0.0,weight_sum_equal $=\!\odot.5$ , count=250),#无风险利率为0，最大化夏普比率需要约束组合权重的和为0.5constraints $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ [],bounds $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ [Bound(0, 0.1)],default_port_weight_range $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ [0., 1.0],ftol=1e-09,return_none_if_fail $\cdot\,$ True)  

# 查看优化结果 print(optimized_weight)  

# 优化失败，给予警告  

if type(optimized_weight) $==$ type(None): print('警告：组合优化失败') # 按优化结果，执行调仓操作  

# else:  

total_value $=$ context.portfolio.total_value # 获取总  

for stock in optimized_weight.keys(): value $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ total_value $\star$ optimized_weight[stock] #  

order_target_value(stock, value) # 调整标的至目标 权重  

# 交易函数  

# 提示  

•  所有下单函数可以在 handle_data 中 与 定时运行函数 的 time 参数为"every_bar"或具体的时间点（例如:time='10:00'）时使用  

创建订单失败（返回None）的可能原因： 股票停牌；标的代码错误、已退市、未上市；账户错误(如给股票下单,指定pindex 为期货账户)；调整下单手数为0；股票下空单等  

了解更多:关于下单函数的说明  

名称 描述order 按股数下单  

order(security, amount, style $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ None, side $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ 'long',  
pindex $=\odot$ , close_today $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ False)  
买卖标的。调用成功后, 您将可以调用[get_open_orders]取得所有未完成的交  
易, 也可以调用[cancel_order]取消交易  

# 参数  

security: 标的代码  

amount: 交易数量, 正数表示买入, 负数表示卖出• style: 参见OrderStyle, None 代表MarketOrderside: 'long'/'short'，操作多单还是空单。默认为多单，股票、基金暂不支持开空单。pindex: 在使用set_subportfolios 创建了多个仓位时，指定subportfolio 的序号, 从 0 开始, 比如 0 指定第一个 subportfolio,1 指定第二个 subportfolio，默认为0。close_today: 平今字段，close_today: 平今字段，仅对上海国际能源中心，上海期货交易所，中金所生效，其他交易所将会报错（其他交易所没有区分平今与平昨，均按照先开先平的方法处理）。o 对上海国际能源中心，上海期货交易所，中金所的标的：  

close_today $=$ True, 只平今仓，今仓不足的时候，订单将会被废单。▪  close_today $\mathbf{\xi}=\ \operatorname{F}\!\varepsilon$ alse, 优先平昨仓，昨仓不足部分平今仓o  不管close_today 是True 还是False，此函数只会产生一个订单，区别在于平仓时的手续费计算，平昨仓使用close_commission 对应手续费率，平今仓使用close_today_commission 手续费率。  

返回 Order 对象或者None, 如果创建订单成功, 则返回Order 对象, 失败则返回None  

# 示例  

#买入平安银行股票100 股  

order('000001.XSHE', 100) # 下一个市价单  
order('000001.XSHE', 100, MarketOrderStyle()) # 下一个市价  
单, 功能同上(科创板市价单需要指定保护价)  
order('688001.XSHG', 100, MarketOrderStyle(10)) #科创板设置  
保护价, 买入时成交价不得高于10 元  
order('000001.XSHE', 100, LimitOrderStyle(10.0)) # 以10 块  
价格下一个限价单  

# 可能的失败原因:  

1. 股票数量经调整后变成0 (请看下面的说明)  
2. 股票停牌  
3. 股票未上市或者退市  
4. 股票不存在  
5. 为股票、基金开了空单  
6. 选择了不存在的仓位号，如没有建立多个仓位，而设定pindex 的数大于  
0  
7. 科创板市价单未指定保护价  

# 注意:  

因为下列原因, 有时候实际买入或者卖出的股票数量跟您设置的不一样，这个时候我们会在您的log 中添加警告信息。  
1. 买入时会根据您当前的现金来限制您买入的数量  
2. 卖出时会根据您持有股票的数量来限制您卖出的数量  
3. 我们会遵守A 股交易规则: 每次交易数量只能是100 的整数倍, 但是卖光所有股票时不受这个限制(科创板200 起可交易200 以上的零散股)根据交易所规则, 每天结束时会取消所有未完成交易  

order_target 目标股数下单  

order_target(security, amount, style $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ None, side $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ 'long', pindex $=\odot$ , close_today $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ False)  

买卖标的, 使最终标的的数量达到指定的amount，注意使用此接口下单时若指定的标的有未完成的订单，则先前未完成的订单将会被取消  

# 参数  

security: 标的代码amount: 期望的最终数量  

style: 参见OrderStyle, None 代表MarketOrderside: 'long'/'short'，操作多单还是空单。默认为多单。默认为多  

单，股票、基金暂不支持开空单。  

pindex: 在使用set_subportfolios 创建了多个仓位时，指定subportfolio 的序号, 从 0 开始, 比如 0 为 指定第一个subportfolio, 1 为指定第二个 subportfolio，默认为0。  

•  close_today: 平今字段，close_today: 平今字段，仅对上海国际能源中心，上海期货交易所，中金所生效，其他交易所将会报错（其他交易所没有区分平今与平昨，均按照先开先平的方法处理）。  

o 对上海国际能源中心，上海期货交易所，中金所的标的：▪  close_today $=$ True, 只平今仓，今仓不足的时候，订单将会被废单。▪  close_today $=$ False, 优先平昨仓，昨仓不足部分平今仓  
o  不管close_today 是True 还是False，此函数只会产生一个订单，区别在于平仓时的手续费计算，平昨仓使用close_commission 对应手续费率，平今仓使用close_today_commission 手续费率。  

返回 Order 对象或者None, 如果创建委托成功, 则返回Order 对象, 失败则返回None  

# 示例  

# 卖出平安银行所有股票  

order_target('000001.XSHE', 0)  

# 买入平安银行所有股票到100 股  

order_target('000001.XSHE', 100)order_target('688001.XSHG', 100, MarketOrderStyle(10)) #科  

创板设置保护价, 买入时成交价不得高于10  

order_value 按价值下单  

order_value(security, value, style=None, side $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ 'long', pindex $=\odot$ , close_today $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ False)  

买卖价值为value 的标的。  

# 参数  

security: 股票名字  

value: 股票价值，value $=$ 最新价 $*$ 手数 $*$ 保证金率（股票为1） \*乘数（股票为100）style: 参见OrderStyle, None 代表MarketOrderside: 'long'/'short'，操作多单还是空单。默认为多单。默认为多单，股票、基金暂不支持开空单。pindex: 在使用set_subportfolios 创建了多个仓位时，指定subportfolio 的序号, 从 0 开始, 比如 0 为 指定第一个subportfolio, 1 为指定第二个 subportfolio，默认为0。  

• close_today: 平今字段，close_today: 平今字段，仅对上海国际能源中心，上海期货交易所，中金所生效，其他交易所将会报错（其他交易所没有区分平今与平昨，均按照先开先平的方法处理）。  

o 对上海国际能源中心，上海期货交易所，中金所的标的：close_today $=$ True, 只平今仓，今仓不足的时候，订单将会被废单。close_today $=$ False, 优先平昨仓，昨仓不足部分平今仓不管close_today 是True 还是False，此函数只会产生一个订单，区别在于平仓时的手续费计算，平昨仓使用close_commission 对应手续费率，平今仓使用close_today_commission 手续费率。  

返回 Order 对象或者None, 如果创建委托成功, 则返回Order 对象, 失败则返回None  

# 示例  

#卖出价值为10000 元的平安银行股票  
order_value('000001.XSHE', -10000)  
#买入价值为10000 元的平安银行股票  
order_value('000001.XSHE', 10000)  
order_value('688001.XSHG', 100, MarketOrderStyle(10)) #科  
创板设置保护价, 买入时成交价不得高于10 元  
order_target_value 目标价值下单  
order_target_value(security, value, style $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ None,  
side $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ 'long', pindex $=\odot$ , close_today $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ False)  
调整标的仓位到value 价值，注意使用此接口下单时若指定的标的有未完成的  
订单，则先前未完成的订单将会被取消  

# 参数  

security: 标的名字  
• value: 期望的标的最终价值，value $=$ 最新价 $*$ 手数 $*$ 保证金率（股票为1） \* 乘数（股票为100）  
• style: 参见OrderStyle, None 代表MarketOrder  
• side: 'long'/'short'，操作多单还是空单。默认为多单。pindex: 在使用set_subportfolios 创建了多个仓位时，指定subportfolio 的序号, 从 0 开始, 比如 0 为 指定第一个subportfolio, 1 为指定第二个 subportfolio，默认为0。close_today: 平今字段，close_today: 平今字段，仅对上海国际能源中心，上海期货交易所，中金所生效，其他交易所将会报错（其他交易所没有区分平今与平昨，均按照先开先平的方法处理）。o 对上海国际能源中心，上海期货交易所，中金所的标的：▪  close_today $=$ True, 只平今仓，今仓不足的时候，订单将会被废单。close_today $=$ False, 优先平昨仓，昨仓不足部分平今仓不管close_today 是True 还是False，此函数只会产生一个订单，区别在于平仓时的手续费计算，平昨仓使用  

close_commission 对应手续费率，平今仓使用close_today_commission 手续费率。  

返回 Order 对象或者None, 如果创建委托成功, 则返回Order 对象, 失败则返回None  

示例#卖出平安银行所有股票  

order_target_value('000001.XSHE', 0)   
#调整平安银行股票仓位到10000 元价值   
order_target_value('000001.XSHE', 10000)   
order_target_value('688001.XSHG', 100,   
MarketOrderStyle(10)) #科创板设置保护价, 买入时成交价不得高于10   
元   
cancel_order 撤单   
cancel_order(order)  

取消订单  

# 参数  

• order: [Order]对象或者order_id返回 Order 对象或者None, 如果取消委托成功, 则返回Order 对象, 委托不存在返回None  

示例#每个交易日结束运行  

def after_trading_end(context):# 得到当前未完成订单orders $=$ get_open_orders()# 循环，撤销订单for _order in orders.values():cancel_order(_order)  

get_open_orders()获得当天的所有未完成的订单  

参数 无返回 返回一个dict, key 是order_id, value 是[Order]对象  

示例#每个交易日结束运行  

def after_trading_end(context): #得到当前未完成订单 orders $=$ get_open_orders() for _order in orders.values(): log.info(_order.order_id)  

ge 日芯 get_orders(order_id=None, security $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ None, status $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ None) 获取当天的所有订单  

# 参数  

order_id: 订单 idsecurity: 标的代码，可以用来查询指定标的的所有订单返回 返回一个dict, key 是order_id, value 是[Order]对象示例  

#每个交易日结束运行 orders $=$ get_orders() for _order in orders.values(): log.info(_order.order_id)  

# 根据订单id 查询订单get_orders(order_id='1517627499')  

# 查询所有标的为 000002.XSHE 的订单get_orders(security='000002.XSHE')  

# 查询订单状态为 OrderStatus.held 的所有订单get_orders(status=OrderStatus.held)  

# 查询标的为 000002.XSHE 且状态为 OrderStatus.held 的所有订单get_orders(security $=$ '000002.XSHE',status $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ OrderStatus.held)  

注意  
非交易时间下单，开盘后订单状态会从new 变为open；new 是指订单新创建未委托；open 是指已委托未完成。  
get_trades 获取成交信息  
get_trades()  
获取当天的所有成交记录, 一个订单可能分多次成交  
参数 无  
返回 返回一个dict, key 是trade_id, value 是[Trade]对象  
示例  

#每个交易日结束运行  

def after_trading_end(context): #得到当天所有成交记录 trades $=$ get_trades() for _trade in trades.values(): log.info(_trade.trade_id)  

inout_cash 账户出入金 inout_cash(cash, pindex $=\odot$ )  

账户转入或转出资金，当日的出入金从当日开始记入成本，用于计算收益，即当日结束计算收益时的本金是包含当日出入金金额的；  

# 参数  

cash： 可正可负，正为入金，负为出金。pindex： 在使用set_subportfolios 创建了多个仓位时，指定subportfolio 的序号, 从 0 开始, 比如 0 为 指定第一个subportfolio, 1 为指定第二个 subportfolio，默认为0。  

# 示例  

# 查看账户可用资金  

log.info('账户可用资金：  
',context.portfolio.subportfolios[0].available_cash)  
# 增加资金：6666  
inout_cash(6666, pindex $=\odot$ )  
# 查看增加资金之后账户的可用资金  
log.info('账户可用资金：  
',context.portfolio.subportfolios[0].available_cash)  
batch_submit_orders 篮子下单  
batch_submit_orders(orders)  
对一系列标的进行批量委托，委托时会对每一个委托进行验资验券，若其中任  
一个委托校验失败，则整个委托将会失败  

# 参数  

orders: 一个list，元素是包含订单信息的dict  

[{  

'security': 'xxxx',  
'amount': 'xxxx', # amount > 0 为买入，< 0 为卖出  
'style': xxxx,  # 同 order()的style 参数, 可选, 默认是 None  
'side': 'long', # 默认是'long'  
},  

]  

security: 标的代码• amount: 交易数量, 正数表示买入, 负数表示卖出style: 参见[order styles], None 代表MarketOrderside: 'long'/'short'，操作多单还是空单。默认为多单，股票、基金暂不支持开空单。pindex: 在使用set_subportfolios 创建了多个仓位时，指定subportfolio 的序号, 从 0 开始, 比如 0 指定第一个 subportfolio,1 指定第二个 subportfolio，默认为0。close_today: 平今字段。o 对上海国际能源中心，上海期货交易所，中金所的标的：▪  close_today $=$ True, 只平今仓■ close_today $=$ False, 优先平昨仓，昨仓不足部分平今仓对其他交易所标的：close_today $=$ True, 优先平今，超出则平昨仓close_today $=$ False, 优先平昨，超出则平今仓返回 一个包含Order 对象的list示例#买入平安银行和福耀玻璃各股票100 股  

orders $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ [{ "security":"000001.XSHE", "amount":100, "pindex":0}, "security":"600660.XSHG", "amount":100, "pindex":0},   
]  

batch_submit_orders(orders) batch_cancel_orders 篮子撤单 batch_cancel_orders(orders) 批量撤单  

参数orders：列表，包含订单对象或订单ID。  

# 对象♠  

名称 描述  

g 全局变量对象全局对象 g，用来存储用户的各类可被pickle.dumps 函数序列化的全局数据  

在模拟盘中，如果中途进程中断，我们会使用[pickle.dumps]序列化所有的g下面的变量内容, 保存到磁盘中，再启动的时候模拟盘就不会有任何数据影响。如果没有用g 声明，会出现模拟盘重启后，变量数据丢失的问题。  

如果不想 $\pmb{g}$ 中的某个变量被序列化, 可以让变量以 '__' 开头, 这样, 这个变量在序列化时就会被忽略  

注意保存的大小有限制,上限30M,超出后将报错  
注意避免对context 及其下属的order/trade/position 等对象进行持久化保  
存，因为账户信息是可变的,这种操作可能导致异常  

def initialize(context): g.security $=$ "000001.XSHE" g.count = 1  

g.flag = 0  

# def process_initialize(context):  

# 保存不能被序列化的对象, 进程每次重启都初始化, 更多信息, 请看[process_initialize]  

g.__q = query(valuation)  

def handle_data(context, data): log.info(g.security) log.info(g.count) log.info(g.flag)  

Context 策略信息总览，包含账户、时间等信息subportfolios: 当前单个操作仓位的资金、标的信息，是一个SubPortfolio 的数组portfolio: 账户信息，即subportfolios 的汇总信息, Portfolio 对象，单个操作仓位时，portfolio 指向 subportfolios[0]current_dt: 当前单位时间的开始时间, [datetime.datetime]对象  

previous_date: 前一个交易日, [datetime.date]对象, 注意, 这是一个日期, 是 date, 而不是 datetime  

universe: 查询set_universe()设定的股票池, 比如: ['000001.XSHE', '600000.XSHG']  

run_params: 表示此次运行的参数, 有如下属性  

o start_date: 回测/模拟开始日期, [datetime.date]对象  
o end_date: 回测/模拟结束日期, [datetime.date]对象  
o type: 运行方式, 如下四个字符串之一'simple_backtest': 回测, 通过点击'编译运行'运行'full_backtest': 回测, 通过点击'运行回测'运行'sim_trade': 模拟交易  
o frequency: 运行频率, 如下三个字符串之一'day''minute''tick'  

为了让从其他平台迁移过来的同学更顺手的使用系统, 我们对此对象也做了和 [g] 一样的处理:o 可以添加自己的变量, 每次进程关闭时持久保存, 进程重启时恢复.o 以 '__' 开头的变量不会被持久保存o 如果添加的变量与系统的冲突, 将覆盖掉系统变量, 如果想恢复系统变量, 请删除自己的变量. 示例:def handle_data(context, data):  

# 执行下面的语句之后, context.portfolio 的整数 1  

context.portfolio $=$ 1  
• log.info(context.portfolio)  
· # 要恢复系统的变量, 只需要使用下面的语句即可del context.portfolio# 此时, context.portfolio 将变成账户信息.log.info(context.portfolio.total_value)我们以后可能会往 context 添加新的变量来支持更多功能, 为了减少不必要的迷惑, 还是建议大家使用 gcontext 对象综述及获取方法  

def handle_data(context, data):  

#获得当前回测相关时间 year $=$ context.current_dt.year month $=$ context.current_dt.month day $=$ context.current_dt.day hour $=$ context.current_dt.hour minute $=$ context.current_dt.minute second $=$ context.current_dt.second  

#得到"年-月-日"格式  

date $=$ context.current_dt.strftime("%Y-%m-%d") #得到周几 weekday $=$ context.current_dt.isoweekday()  

# 获取总账户的持仓价值  

positions_value $=$ context.portfolio.positions_value  

# 总权益的累计收益  

returns $=$ context.portfolio.returns # 获取仓位subportfolios[0]的可用资金 available_cash $=$  

context.subportfolios[0].available_cash# 获取subportfolios[0]中多头仓位的security 的持仓成本  

hold_cost $=$ context.subportfolios[0].long_positions[security].hold_co st  

# 这是一个dict,键是标的代码,值是对应的position 对象context.subportfolios[0].long_positionsfor position in list(long_positions_dict.values()):  

print("标的:{0},总仓位:{1},标的价 值:{2}".format(position.security,position.total_amount,pos ition.value))  

SubPortfolio 子账户信息  

某个仓位的资金，标的信息，如未使用 SubPortfolioConfig 设置多仓位，默认只有subportfolios[0]一个仓位，Portfolio 指向该仓位。  

inout_cash: 累计出入金, 比如初始资金 1000, 后来转移出去 100, 则这个值是 1000 - 100  
• available_cash: 可用资金, 可用来购买证券的资金  
• transferable_cash: 可取资金, 即可以提现的资金, 不包括今日卖出证券所得资金locked_cash: 挂单锁住资金  
• type: 账户所属类型long_positions: 多单的仓位, 一个 dict, key 是标的代码, value 是[Position]对象short_positions: 空单的仓位, 一个 dict, key 是标的代码, value是 [Position]对象  
• positions_value: 持仓价值total_value: 总资产, 包括现金, 保证金(期货)或者仓位(股票)的总价值, 可用来计算收益total_liability: 总负债, 等于融资负债、融券负债、利息总负债的总和  
• net_value: 净资产, 等于总资产减去总负债  
• cash_liability: 融资负债  
• sec_liability: 融券负债  
• interest: 利息总负债  
• maintenance_margin_rate: 维持担保比例  
• available_margin: 融资融券可用保证金margin: 保证金，股票、基金保证金都为 $100\%$ ；融资融券保证金为0；期货保证金会实时更新, 总是等于当前期货价值 乘以 保证金比率, 当保证金不足时, 强制平仓. 平仓顺序是: 亏损多的(相对于开仓均价)先平仓  

# print("累计出入  

金:{0}".format(context.subportfolios[0].inout_cash))print("可用资  

金:{0}".format(context.subportfolios[0].available_cash))print("可取资  

金:{0}".format(context.subportfolios[0].transferable_cash))  

# print("挂单锁住资  

金:{0}".format(context.subportfolios[0].locked_cash))print("账户所属类型:{0}".format(context.subportfolios[0].type))  

# 这是一个dict,键是标的代码,值是对应的position 对象  

long_positions_dict $=$  

context.subportfolios[0].long_positions for position in list(long_positions_dict.values()): print(" 标的:{0},总仓位:{1},标的价  

值:{2}".format(position.security,position.total_amount,pos ition.value))  

print("持仓价  

值:{0}".format(context.subportfolios[0].positions_value)) print("总资  

产:{0}".format(context.subportfolios[0].total_value))  

Portfolio 总账户信息  

账户当前的资金，标的信息，即所有标的操作仓位的信息汇总。如未使用SubPortfolioConfig 设置多仓位，默认只有subportfolios[0]一个仓位，Portfolio 指向该仓位。注意区分多仓和空仓。  

inout_cash: 累计出入金, 比如初始资金 1000, 后来转移出去 100, 则这个值是 1000 - 100available_cash: 可用资金, 可用来购买证券的资金transferable_cash: 可取资金, 即可以提现的资金, 不包括今日卖出证券所得资金  
• locked_cash: 挂单锁住资金  
• margin: 保证金，股票、基金保证金都为 $100\%$   
• positions: 等同于 long_positionslong_positions: 多单的仓位, 一个 dict, key 是证券代码, value 是[Position]对象short_positions: 空单的仓位, 一个 dict, key 是证券代码, value是 [Position]对象total_value: 总的权益, 包括现金, 保证金(期货)或者仓位(股票)的总价值, 可用来计算收益returns: 总权益的累计收益；（当前总资产 $^+$ 今日出入金 - 昨日总资产） / 昨日总资产；  
• starting_cash: 初始资金, 现在等于 inout_cash  
• positions_value: 持仓价值  
• cash: 已过时，等价于 available_cash  
• portfolio_value: 已过时，等价于 total_valueunsell_positions: 已过时, 请使用 positions 代替, 当前持有的不可以卖出的持仓(比如在A 股T+1 市场, 今天购票的股票), 并没有考虑股票今天是否停牌, 一个dict, key 是股票代码, value 是[Position]对象.  

print("多单的仓  

位:{0}".format(context.portfolio.long_positions))print("空单的仓  

位:{0}".format(context.portfolio.short_positions))print("总权益:{0}".format(context.portfolio.total_value))  

print("总权益的累计收  

益:{0}".format(context.portfolio.returns)) print("初始资  

金:{0}".format(context.portfolio.starting_cash))print("持仓价  

值:{0}".format(context.portfolio.positions_value))  

Position 持仓标的信息持有的某个标的的信息,注意区分多仓和空仓  

# security: 标的代码  

# •  price: 最新行情价格  

acc_avg_cost 是累计的持仓成本，在清仓/减仓时也会更新，该持仓累积的收益都会用于计算成本（一开始acc_avg_cost 为0，amount 也为0），加仓：new_acc_avg_cost $=$ (acc_avg_cost $*$ amount $^{+}$ trade_value $^+$ commission) / (amount $^+$ trade_amount)；减仓：new_acc_avg_cost $=$ (acc_avg_cost \* amount - trade_value $^{+}$ commission) / (amount - trade_amount) 说明：commission 是本次买入或者卖出的手续费avg_cost 是当前持仓成本，只有在开仓/加仓时会更新： new_avg_cost$=$ (position_value $^+$ trade_value $^{+}$ commission) /(position_amount $^{+}$ trade_amount)每次买入后会调整avg_cost, 卖出时avg_cost 不变. 这个值也会被用来计算浮动盈亏.hold_cost: 当日持仓成本，计算方法：当日无收益：hold_cost $=$ 前收价 （清算后），加仓：hold_cost $=$ (hold_cost \* amount $^{+}$ trade_value)/(amount $^+$ trade_amount)，减仓：hold_cost $=$ (hold_cost $*$ amount - trade_value)/(amount - trade_amount)；trade_value $=$ trade_price \* trade_amountinit_time: 建仓时间，格式为 datetime.datetime  
• transact_time: 最后交易时间，格式为 datetime.datetime  
• locked_amount: 挂单冻结仓位total_amount: 总仓位, 但不包括挂单冻结仓位( 如果要获取当前持仓的仓位,需要将locked_amount 和total_amount 相加)  
• closeable_amount: 可卖出的仓位  
• today_amount: 今天开的仓位value: 标的价值，计算方法是: price \* total_amount \* multiplier,其中股票、基金的multiplier 为1，期货为相应的合约乘数side: 多/空，'long' or 'short'  
• pindex: 仓位索引，subportfolio index  
• sellable_amount: 已过时, 为了向前兼容, 等同于 closeable_amount  
• amount: 已过时, 为了向前兼容, 等同于 closeable_amountprint(type(context.portfolio.long_positions))long_positions_dict $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ context.portfolio.long_positions  
for position in list(long_positions_dict.values()):print("标的:{0},总仓位:{1},标的价值:{2}, 建仓时  
间:{3}".format(position.security,  
position.total_amount, position.value,  
position.init_time))  
print(type(context.subportfolios[0].short_positions)  
)  
short_positions_dict =  
context.portfolio.short_positions  
for position in list(short_positions_dict.values()):print("标的:{0},总仓位:{1},标的价值:{2}, 建仓时  
间:{3}".format(position.security,  
position.total_amount, position.value,  
position.init_time))  

SecurityUnitData data 对象一个单位时间内的股票的数据  

# 为了向前兼容，保留data 对象，由于效率问题不推荐使用  

基本属性  

以下属性也能通过history/attribute_history/get_price 获取到  

• open: 时间段开始时价格(当天天级别的开盘价至少需要09:27 分之后才可获取)  
•  close: 时间段结束时价格  
• low: 时间段中的最低价  
• high: 时间段中的最高价  
• volume: 时间段中的成交的股票数量  
• money: 时间段中的成交的金额factor: 前复权因子, 我们提供的价格都是前复权后的, 但是利用这个值可以算出原始价格, 方法是价格除以factor, 比如:close/factor  
•  high_limit: 时间段中的涨停价  
•  low_limit: 时间段中的跌停价avg: 这段时间的平均价。计算方法（1）天级别：股票是成交额除以成交量；期货是直接从CTP 行情获取的，计算方法为成交额除以成交量再除以合约乘数；（2）分钟级别：用该分钟所有tick 的现价乘以该tick的成交量加起来之后，再除以该分钟的成交量。price: 已经过时, 为了向前兼容, 等同于 avg  
• pre_close: 前一个单位时间结束时的价格, 按天则是前一天的收盘价（期货中pre_close 是前前一天结算价，建议使用get_extras 获取结算价）, 注意：在分钟频率下pre_close=open；  
•  paused: bool 值, 这只股票是否停牌, 停牌时open/close/low/high/pre_close 依然有值,都等于停牌前的收盘价,volume $=$ money $=0$  

额外的属性和方法  

security: 股票代码, 比如'000001.XSHE  
returns: 股票在这个单位时间的相对收益比例, 等于(close-  
pre_close)/pre_close  
isnan(): 数据是否有效, 当股票未上市或者退市时, 无数据, isnan()  
返回True  
mavg(days, field='close'): 过去days 天的每天收盘价的平均值,  
把field 设成'avg'(等同于已过时的'price')则为每天均价的平均价,  
下同  
vwap(days): 过去days 天的每天均价的加权平均值, 以days=2 为例  
子, 算法是:  
(avg1 \* volume1 + avg2 \* volume2) / (volume1 +  
volume2)  
stddev(days): 过去days 天的每天收盘价的标准差  
注：mavg/vwap/stddev:都会跳过停牌日期, 如果历史交易天数不足, 则  
返回nan  

tick 对象 tick 对象  

一个 tick 所包含的信息。 tick 中的信息是在 tick 事件发生时， 盘面的一个快照。  

code: 标的的代码• datetime: tick 发生的时间• current: 最新价• open：当日开盘价• high: 截至到当前时刻的最高价• low: 截至到当前时刻的最低价• volume: 截至到当前时刻的成交量• money: 截至到当前时刻的成交额position: 截至到当前时刻的持仓量，只适用于期货 tick 对象• a1_v \~ a5_v: 卖一量到卖五量，对于期货，只有卖一量• a1_p a5_p: 卖一价到卖五价，对于期货，只有卖一价• b1_v b5_v: 买一量到买五量，对于期货，只有买一量• b1_p b5_p: 买一价到买五价，对于期货，只有买一价  

Trade 对象 订单的一次交易记录,一个订单可能分多次交易.  

订单的一次交易记录,一个订单可能分多次交易关于order/trader 对象及订单处理  

time: 交易时间, [datetime.datetime]对象security：标的代码  
• amount: 交易数量  
• price: 交易价格trade_id: 交易记录idorder_id: 对应的订单id  

trades $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ get_trades()  

for _trade in trades.values():  

print('成交记录：'+str(_trade))print('交易时间：{0}'.format(_trade.time))print('对应的订单id：{0}'.format(_trade.order_id))Order 对象 买卖订单信息  

买卖订单关于order/trader 对象及订单处理以csv 格式保存order、trade、position 数据  

status: 状态, 一个OrderStatus 值  
• add_time: 订单添加时间, [datetime.datetime]对象is_buy: bool 值, 买还是卖，对于期货:开多/平空 -> 买开空/平多 -> 卖amount: 下单数量, 不管是买还是卖, 都是正数  
• filled: 已经成交的股票数量, 正数  
• security: 股票代码  
• order_id: 订单IDprice: 平均成交价格, 已经成交的股票的平均成交价格(一个订单可能分多次成交)avg_cost: 卖出时表示下卖单前的此股票的持仓成本, 用来计算此次卖出的收益. 买入时表示此次买入的均价(等同于price).side: 多/空，'long'/'short'  
• action: 开/平， 'open'/'closecommission：交易费用（佣金、税费等）  

orders $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ order('000001.XSHE', 100) print(orders)  

if orders is None: print("创建订单失败...")  

# else:  

print("交易费用单：{0}".format(orders.commission)) print("是否买单：{0}".format(orders.is_buy)) print("订单状态：{0}".format(orders.status)) print("订单平均成交价格：{0}".format(orders.price))  

# 注意  

• 不可以在策略中保存当天的订单信息到下一个或者之后的交易日使用；OrderStatus 订单状态订单状态, Enum 特性使用的第三方库(https://pypi.python.org/pypi/enum34)获取订单状态的方法请参考上面Order 对象  

# 订单新创建未委托，用于盘前/隔夜单，订单在开盘时变为 open 状态开始撮合  

new = 8  

# 订单未完成, 无任何成交open $=$ 0  

# 订单未完成, 部分成交filled $=$ 1  

# 订单完成, 已撤销, 可能有成交, 需要看 Order.filled 字段canceled $=$ 2  

# 订单完成, 交易所已拒绝, 可能有成交, 需要看 Order.filled 字段rejected $=$ 3  

# 订单完成, 全部成交, Order.filled 等于 Order.amountheld $=$ 4  

注意订单状态数据类型为Enum，判断时可以转为字符串，示例代码如下：  

def initialize(context): run_daily(market_open, time $=$ 'every_bar')  

def market_open(context): orders $=$ order('000001.XSHE', 100) print(orders) # 如果创建订单成功, 则返回Order 对象, 失败则返回None if orders is None:  

print("创建订单成功失败...")  

else:print(orders.is_buy)print(orders.price)print(orders.status)# 注意返回的status 数据类型为，enum 'OrderStatus'print(type(orders.status))# 判断订单的状态是否指定的状态，需要先转换为str 类型print(str(orders.status) $==$ 'open')print(str(orders.status) $==$ 'held')  
print( $\mathsf{I}=\mathsf{I}\star\mathsf{5}\Theta\,.$ )  
OrderStyle 下单方式  
具体订单处理方法请查看订单处理>>>  
下单方式, 有如下子类市价单  

class MarketOrderStyle(OrderStyle): def __init__(self, limit_price $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ None): self.limit_price $=$ limit_price  

市价单示例  

参数：  

limit_price：科创板市价单的保护价，对非科创板标的无效。# 在仓位0，以市价单买入平安银行股票100 股order('000001.XSHE', 100)# 在仓位0，以市价单买入平安银行股票100 股Gorder('000001.XSHE', 100, MarketOrderStyle())# 在仓位0 中开一手沪深300 指数期货的多单order('IF1412.CCFX', 1 , side='long', pindex=0)# 在仓位0，以市价单买入科创板天准科技股票200 股，保护价为200order('688003.XSHG', 200, MarketOrderStyle(200))  

科创板保护价逻辑：  

市价买入时成交的最高价格不高于本价格，若最优一档的价格高于该价格，剩余未成交部分撤单；  

市价卖出时成交的最低价格不低于本价格，若最优一档的价格低于该价格，剩余未成交部分撤单；  

限价单  

class LimitOrderStyle(OrderStyle): def __init__(self, limit_price): self.limit_price $=$ limit_price  

限价单示例  

# 以10 块价格下一个限价单order('000001.XSHE', 100, LimitOrderStyle(10.0))  

# 在仓位1 中以3600 的限价单，平一手沪深300 指数期货的空单order('IF1412.CCFX', -1 , LimitOrderStyle(3600.0),side $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ 'short', pindex $^{=1}$ )  

停止单   
StopMarketOrderStyle(mode, stop_price)StopLimitOrderStyle(   
mode, stop_price, limit_price)  

使用方法： 在order/order_target/order_value/order_target_value 函数中指定委托类型为停止单。停止单会在标的价格突破（向上或向下）时转化为对应的市价单或限价单  

参数 mode："stop_loss", "take_profit"，指定该停止单是止盈模式还是止损模式，具体解释见下文 stop_price：停止单被触发的价格，当价格突破（向上或向下）时将停止单转为对应种类（市价单/限价单）的订单 limit_price：限价，同限价单  

止盈模式与止损模式 若为止损单模式，平空、做多或买入时触发价必须大于最新价，平多、做空或卖出时触发价必须小于最新价； 若为止盈单模式，平多、做空或卖出时触发价必须大于最新价，平空、做多或买入时触发价必须小于最新价； 若触发价不满足条件，该停止单会立即触发  

备注  

停止单不会提前锁定持仓和资金，触发时不满足委托条件（如资金不足  
或可交易数量不足）直接委托失败  
订单生效的时间仅限于标的交易时间，当天未完成的停止单盘后撤销  
order_value/order_target_value 使用停止单进行委托时，由value 计  
算实际委托数量的规则：o 实际委托数量 $=$ value / 价格 / 保证金率 / 乘数o  StopMarketOrderStyle 以stop_price 计算实际委托数量o  StopLimitOrderStyle 以limit_price 计算实际委托数量  

Event 事件对象  

DividendsEvent - 分红送股事件  

属性  

name：事件的名称，这里为Dividends  
• pindex：子账户索引  
• security：标的代码  
• side：仓位方向，long/shortdividends：分红配送信息，一个字典列表，直接从数据中获取，通常只有一个元素。例如，税前分红可以用dividends[0]['bonus_pre_tax']表示，所有可能的key 如下：o date：发生分红送股的日期o scale_factor：配送股比例（股票，场内基金）o bonus_pre_tax：税前分红（股票，场内基金）bonus_post_tax：税后分红（场内基金）  

ForcedLiquidationEvent：强行平仓事件  

# 属性  

name：事件的名称，这里为ForcedLiquidation  
pindex：子账户索引  
security：标的  
side：仓位方向，long/short  
amount：平仓数量  

# 其他函数  

名称 描述  

record $\spadesuit$ 画图函数 record(\*\*kwargs)  

回测环境/模拟专用API如调用该函数，需要从回测开始时调用，不支持在回测周期中间时段调用我们会帮您在图表上画出收益曲线和基准的收益曲线，您也可以调用record 函数来描画额外的曲线。 因为我们是按天展现的，如果您使用按分钟回测，我们画出的点是您最后一次调用record 的值（不是每分钟的）。 以16:00 为界限，16:00 之后绘制的属于第二天。  

参数 一个或多个key $=$ value 形式的参数，key 为曲线名称，value 为值（不能是列表）  

返回 None  

# 示例  

# 初始化函数，设定基准等等def initialize(context):# 开启动态复权模式(真实价格)set_option('use_real_price', True)# 设置日志级别为infolog.set_level('order', 'info')  

def handle_data(context, data):d $=$ data['000001.XSHE']  

# d 是一个SecurityUnitData 结构体，会画出每个单元时间(天或分钟)的平均价,开始价,结束价record(price $=$ d.price, open=d.open, close=d.close)# 也可以画一条值为100 的直线record(price=100)send_message $\spadesuit$ 发送自定义消息  

send_message(message, channel $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ 'weixin')聚宽官网实时运行模拟交易专用API给用户自己发送消息, 暂时只支持微信消息.  

参数 message: 消息内容. 字符串. channel: 消息渠道, 暂时只支持微信:weixin. 默认值是 weixin  

返回值 True/False, 表示是否发送成功. 当发送失败时, 会在日志中显示错误信息.  

注意  

要使用模拟交易发送微信功能, 必须绑定及开启微信通知；  
此功能只能在 聚宽官网的实时运行模拟交易 中使用, 回测中使用会直接忽略, 无任何提示；有关实时和延时运行  
请注意区分自定义消息和下单通知，send_message 对应的是自定义微信消息，下单通知是模拟交易策略有下单时（交易详情页面有下单记录）同时发送微信消息；自定义消息只要绑定了微信，都会发送；下单信息只有开启具体模拟交易的微信通知开关，此策略才发送微信消息；  
下单通知：每个账号每天最多60 条；自定义消息每个账号每天最多 5 条, 超出会发送失败，需要更多条数可以使用积分兑换  
自定义消息长度不得超过 200 个字符, 也不能包含回车和换行这些特殊字符，否则会发送失败  
一个账号模拟交易只能被一个用户绑定，多个微信绑定后，前面失效，以最后一个绑定的微信号为准  

# 示例  

send_message("测试消息")  

log 日志log 信息  
log.error(content)  
log.warn(content)  
log.info(content)  
log.debug(content)  
print(content1, content2, ...)  
分级别打log,跟python 的logging 模块一致 print 输出的结果等同于  
log.info, 但是print 后面的每一个元素会占用一行  

参数 参数可以是字符串、对象等  

返回 None  

# 示例  

log.info(history(10)) # 打印出 history(10)返回的结果 log.info("Selling %s, amount=%s", security, amount) # 打印 出一个格式化后的字符串 print(history(10), data, context.portfolio)  

设定log 级别：log.set_level log.set_level(name, level)  

设置不同种类的log 的级别, 低于这个级别的log 不会输出. 所有log 的默认级别是debug，为了降低排查问题的难度，建议日志级别保持为默认级别(不设置日志级别，或者设置log.set_level('order', 'info'))。  

参数 name: 字符串, log 种类, 必须是'order', 'history', 'strategy'中的一个, 含义分别是:  

order: 调用order 系列API 产生的log  
history: 调用history 系列  
API(history/attribute_history/get_price)产生的log  
strategy: 您自己在策略代码中打的log  
system：系统日志，除以上三类之外的日志  

level: 字符串, 必须是'debug', 'info', 'warning', 'error'中的一个, 级别: debug < info < warning < error  

# 示例  

# 设置日志级别为debuglog.set_level('order', 'debug')  

$\star\star$ 注意 $\star\star$  

- 尽量设置日志级别为debug，或者不设置（使用系统默认级别），有利于您快速的发现问题；  
- 模拟交易中，需要修改日志级别，可以在after_code_changed 中，重新设置日志级别。  
write_file 将回测或模拟交易数据写入到投资研究文件中  
write_file(path, content, append $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ False)  
将回测或者模拟交易的数据写入投资研究path 文件, 写入后, 您可以立即在研究模块中看到这个文件,默认在投资研究的根目录  
在回测及模拟交易中读取/写入研究中不同格式的文件  

# 参数  

• path: 相对路径, 相对于您的私有空间的根目录的路径content: 文件内容, str 或者unicode, 如果是unicode, 则会使用UTF-8 编码再存储.可以是二进制内容.append: 是否是追加模式, 当为False 会清除原有文件内容，默认为False.  

返回 None 如果写入失败(一般是因为路径不合法), 会抛出异常示例write_file("test.txt", "hello world")  

# 写入沪深300 的股票到HS300.stocks.json 文件中  

import json   
write_file('HS300.stocks.json',   
json.dumps(get_index_stocks('000300.XSHG')))  

# 把 DataFrame 表保存到文件  

df $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ attribute_history('000001.XSHE', 5, '1d') #获取DataFrame 表write_file('df.csv', df.to_csv(), append=False) #写到文件中  

## 详细用法可以参考文档：https://www.joinquant.com/post/580 以  
及  
https://www.joinquant.com/view/community/detail/a9f7577b3  
7265f78ffc2c6bb2467d47e?type=1  
read_file 在回测或者模拟交易中读取您研究中文件  

在回测及模拟交易中读取你的私有文件(您的私有文件可以在研究模块中看到)在回测及模拟交易中读取/写入研究中不同格式的文件  

参数 path: 相对路径, 相对于您的私有空间的根目录的路径返回 返回文件的原始内容, 不做任何decode.  

示例#解析json 文件  

import json   
content $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ read_file('HS300.stocks.json')   
securities $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ json.loads(content)   
log.info(securities)  

#解析csv 文件（python2 环境）  

import pandas as pd from six import StringIO body $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ read_file("open.csv") data $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ pd.read_csv(StringIO(body))  

#解析csv 文件（python3 环境）  

import pandas as pd from six import BytesIO body $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ read_file("open.csv") data $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ pd.read_csv(BytesIO(body))  

## 详细用法可以参考文档：https://www.joinquant.com/post/580  

不能在官网的回测及模拟中读取您本地的文件，本地文件需要上传到官网的投资研究中；  
支持读取csv, excel, json 等格式文件，具体教程参考在回测及模拟交易中读取研究中不同格式的文件；  
注意区分Python2 和Python3，  
自定义python 库 自定义私人的Python 库文件  
您可以在把.py 文件放在'研究'的根目录, 然后在回测中就可以通过import 的  
方式来引用此文件. 比如  

研究根目录/mylib.py:  

#-\*- coding: utf-8 -\*-  

# 如果你的文件包含中文, 请在文件的第一行使用上面的语句指定你的文件编码  

# 用到策略及数据相关API 请加入下面的语句(如果要兼容研究使用可以使用  
try except 导入  
from kuanke.user_space_api import \*  

my_stocks = get_index_stocks('000300.XSHG') 在策略代码中:  

# 导入自己创建的库from mylib import \*def initialize(context):  

log.info(my_stocks)  

# 注意  

此方法主要用来读取研究根目录中的.py 文件，读取其他格式的文件请参考read_file;  
暂时只能import 研究根目录下的.py 文件, 还不能import 子目录下的文件(比如通过 import a.b.c 来引用a/b/c.py)  

create_backtest 通过一个策略ID 从研究中创建回测  

create_backtest(algorithm_id, start_date, end_date,  
frequency $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ "day", initial_cash=10000,  
initial_positions $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ None, extras $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ None, name $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ None, code $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ "",benchmark $\equiv$ None, python_version $^{=2}$ , use_credit $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ False)  
通过一个策略ID 从研究中创建回测，只能在研究中使用，目前不支持在回测及模拟交易中使用；  

# 参数：  

algorithm_id: 策略ID，从策略编辑页的 url 中获取, 比如'/algorithm/index/edit?algorithmId=xxxx'，则策略ID 为: xxxx。如下图所示：  

![](images/8d4d2a8681fbfdb087007bc7e371a554590090a102f9876d82d9525f0dd8068b.jpg)  

# ill JoinQuant  

test  

策略ID：在策略研究，策略列表页面，打开start_date: 回测开始日期end_date: 回测结束日期frequency: 数据频率，支持 day, minute, tickinitial_cash: 初始资金  

<html><body><table><tr><td>已保存</td><td>编译运行</td><td>函数库</td><td>2to3</td><td>API</td><td></td><td></td><td></td><td></td></tr></table></body></html>  

extras: 额外参数，一个 dict， 用于设置全局的 $^\mathrm{g}$ 变量，如extras $=$ {'x':1, 'y':2}，则回测中 $\mathrm{~g.~x~}=\,1$ , $\mathrm{~g.~y~}=~2$ ，需要注意的是，该参数的值是在 initialize 函数执行之后才设置给 $_\mathrm{g}$ 变量的，所以这会覆盖掉 initialize 函数中 $^\mathrm{g}$ 变量同名属性的值  

name: 回测名, 用于指定回测名称, 如果没有指定则默认采用策略名作为回测名  

initial_positions: 初始持仓。持仓会根据价格换成现金加到初始资金中，如果没有给定价格则默认获取股票最近的价格。格式如下:  

initial_positions $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ [  

'security':'000001.XSHE','amount':'100',  
},  
{'security':'000063.XSHE','amount':'100','avg_cost': '1.0'  
code：策略代码。现在支持从研究中传入策略代码进行回测。指定之后将使用传入的代码来创建回测。  
benchmark: 为回测设置基准。默认为None，表示使用策略中原有set_benchmark 设置的基准。若不为None，则表示使用当前传入的基准覆盖原策略的基准。benchmark 支持的基准同set_benchmark  
python_version: 创建回测的python 的版本，2 或者3，默认为2(python2);注意客户端没有这个参数，默认python3 的use_credit:是否允许消耗积分新建回测。当每个自然日内编译运行、回测超过免费时间时，继续运行每30 分钟需消耗2 积分。默认为False，表示不允许消耗积分新建回测，设为True 表示接受消耗积分新建回测。需注意，对于已经在运行中的回测，此配置不生效。  

# 返回：  

一个字符串, 即 backtest_id  

# 示例一：  

algorithm_id = "xxxx"   
extra_vars $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ {'a': 1, 'b': 2, 'c': 3, 'd': 4, 'e': 5}   
initial_positions $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ [ { 'security':'000001.XSHE', 'amount':'100', } { 'security':'000063.XSHE', 'amount':'100', 'avg_cost': '1.0' },  

params $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ { "algorithm_id": algorithm_id, "start_date": "2015-10-01", "end_date": "2016-07-31", "frequency": "day", "initial_cash": "1000000",  

"initial_positions": initial_positions, "extras": extra_vars, }  

created_bt_id $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ create_backtest(\*\*params)  
print(created_bt_id)  
示例二，在研究中指定回测用策略代码：  
code $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ """  

# 导入函数库from jqdata import \*# 初始化函数，设定基准等等  

def initialize(context):# 设定沪深300 作为基准set_benchmark('000300.XSHG')# 开启动态复权模式(真实价格)set_option('use_real_price', True)# 输出内容到日志 log.info()log.info('初始函数开始运行且全局只运行一次')# 过滤掉order 系列API 产生的比info 级别低的log# log.set_level('order', 'info')  

### 股票相关设定 ###  

# 股票类每笔交易时的手续费是：买入时佣金万分之三，卖出时佣金万分 之三加千分之一印花税, 每笔交易佣金最低扣5 块钱 set_order_cost(OrderCost(close_tax=0.001, open_commission $=\odot$ .0003, close_commission $=\odot$ .0003, min_commission $^{=5}$ ), type $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ 'stock')  

## 运行函数（reference_security 为运行时间的参考标的；传入的标的只做种类区分，因此传入'000300.XSHG'或'510300.XSHG'是一样的）# 开盘前运行run_daily(before_market_open, time $=$ '09:00',reference_security='000300.XSHG')# 开盘时运行run_daily(market_open, time='09:30',reference_security='000300.XSHG')# 收盘后运行run_daily(after_market_close, time $=$ '15:30',reference_security='000300.XSHG')  

# ## 开盘前运行函数  

def before_market_open(context):# 输出运行时间  

log.info('函数运行时间(before_market_open)：'+str(context.current_dt.time()))  

# 给微信发送消息（添加模拟交易，并绑定微信生效）send_message('美好的一天\~')  

# 要操作的股票：平安银行（g.为全局变量）g.security $=$ '000001.XSHE'  

# ## 开盘时运行函数  

def market_open(context):log.info('函数运行时间  
(market_open):'+str(context.current_dt.time()))security $=$ g.security# 获取股票的收盘价close_data $=$ attribute_history(security, 5, '1d',  
['close'])# 取得过去五天的平均价格MA5 $=$ close_data['close'].mean()# 取得上一时间点价格current_price $=$ close_data['close'][-1]# 取得当前的现金cash $=$ context.portfolio.available_cash# 如果上一时间点价格高出五天平均价1%, 则全仓买入if current_price > $1\,.\,\odot1{\star}\mathsf{M A}5$ :# 记录这次买入log.info("价格高于均价 1%%, 买入 %s" % (security))# 用所有 cash 买入股票order_value(security, cash)# 如果上一时间点价格低于五天平均价, 则空仓卖出elif current_price < MA5 and  
context.portfolio.positions[security].closeable_amount >  
0:# 记录这次卖出log.info("价格低于均价, 卖出 %s" % (security))# 卖出所有股票,使这只股票的最终持有量为0order_target(security, 0)  
## 收盘后运行函数  
def after_market_close(context):log.info(str('函数运行时间  
(after_market_close):'+str(context.current_dt.time())))#得到当天所有成交记录  
trades $=$ get_trades()  
for _trade in trades.values():log.info('成交记录：'+str(_trade))  
log.info('一天结束')  

log.info('############################################### ###############')  

"""  

algorithm_id $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ "xxxx"   
extra_vars $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ {'a': 1, 'b': 2, 'c': 3, 'd': 4, 'e': 5}   
initial_positions $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ [ { 'security':'000001.XSHE', 'amount':'100', } { 'security':'000063.XSHE', 'amount':'100', 'avg_cost': '1.0' },   
]  

params $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ { "algorithm_id": algorithm_id, "start_date": "2015-10-01", "end_date": "2016-07-31", "frequency": "day", "initial_cash": "1000000", "initial_positions": initial_positions, "extras": extra_vars,  

created_bt_id $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ create_backtest(code=code, \*\*params)  
get_backtest 研究中获取回测与模拟交易信息  
gt $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ get_backtest(backtest_id)  
研究中获取回测与模拟交易信息，只能在研究中使用，目前不支持在回测及模  
拟交易中使用；使用方法及参考教程：  
参数优化及并行回测参考教程  
区分create_backtest(策略ID)和get_backtest(回测ID)  
create_backtest 与get_backtest  

# 参数：  

backtest_id: 回测ID，从回测详情页以及模拟交易详情页的 url 中获取, 比如 '/algorithm/backtest/detail?backtestId $\supseteq^{\bullet}$ 以及'/algorithm/live/index?backtestId='，则回测ID 为:xxxx。如下图所示：  

G joinquant.com/algorithm/ backtest/detaill backtestld ecac584110bce8ac3d33f0  

# Ill JoinQuant  

首页 策略研究  

设置：2019-01-01到2019-08-20，￥500000，每天 状态： 回测完成，耗时2.67s Python3  

# 收益概述  

# 收益概述  

返回：  

gt.get_status():获取回测状态. 返回一个字符串，其含义分别为：  

o none: 未开始 o running: 正在进行 o done: 完成 o failed: 失败 o canceled: 取消 o paused: 暂停 o deleted: 已删除  

gt.get_params()：获得回测参数. 返回一个 dict, 包含调用create_backtest 时传入的所有信息. (注： algorithm_id，initial_positions，extras 只有在研究中创建的回测才能取到)  

gt.get_results()：获得收益曲线. 返回一个 list，每个交易日是一个dict，键的含义如下：o time: 时间o returns: 收益o benchmark_returns: 基准收益o 如果没有收益则返回一个空的 list  

gt.get_positions(start_date $=$ None, end_date=None)：获得持仓详情.  
返回一个 list，默认取所有回测时间段内的数据。每个交易日为一个  
dict，键的含义为：o  time: 时间o amount: 持仓数量,  
o avg_cost: 开场均价,  
o closeable_amount: 可平仓数量,  
o daily_gains: 当日收益,  
o gains: 累积收益,  
o hold_cost: 持仓成本（期货）,  
o margin: 保证金,  
o price: 当前价格,  
o security: 标的代码,  
o security_name: 标的名,  
o side: 仓位方向,  
o today_amount: 今开仓量  
o 如果没有持仓则返回一个空的 list  

gt.get_orders(start_date $=$ None, end_date=None)：获得交易详情. 返回一个 list，默认取所有回测时间段内的数据。每个交易日为一个  

ct，键的含义为：o time: 时间o action: 开平仓，'open'/'close',o amount: 数量,o commission: 手续费,o filled: 已成交量,o gains: 收益,o limit_price: 限价单委托价,o match_time: 最新成交时间,o price: 成交价,o security: 标的代码,security_name: 标的名,o side: 仓位方向,o status: 订单状态,o time: 委托时间,o type: 委托方式，市价单/限价单如果没有交易则返回一个空的 listgt.get_records()：获得所有 record 记录. 返回一个 list，每个交易日为一个 dict，键是 time 以及调用 record() 函数时设置的值.gt.get_risk()：获得总的风险指标. 返回一个 dict，键是各类收益指标数据，如果没有风险指标则返回一个空的 dict.gt.get_period_risks()：获得分月计算的风险指标. 返回一个 dict，键是各类指标, 值为一个 pandas.DataFrame. 如果没有风险指标则返回一个空的 dict.gt.get_balances(start_date $=$ None, end_date=None): 获取回测每日市值. 返回一个 list，默认取所有回测时间段内的数据。每个交易日为一个 dict  

# 示例：  

gt = get_backtest("xxxx")  

gt.get_status() # 获取回测状态  
gt.get_params() # 获取回测参数  
gt.get_results() # 获取收益曲线  
gt.get_positions() # 获取所有持仓列表  
gt.get_orders() # 获取交易列表  
gt.get_records() # 获取所有record()记录gt.get_risk() # 获取总的风险指标  
gt.get_period_risks()  # 获取分月计算的风险指标gt.get_balances() # 获取回测每日市值  
normalize_code 股票代码格式转换  
normalize_code()  
将其他形式的股票代码转换为聚宽可用的股票代码形式。  

仅适用于A 股市场股票代码、期货以及场内基金代码，输入字符串格式或int格式的其他形式标的代码,也支持list 或tuple 来转换多个标的代码  

示例#输入  

codes $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ ('000001', 'SZ000001', '000001SZ', '000001.sz', '000001.XSHE')  

print(normalize_code(codes ))  

#输出  

['000001.XSHE', '000001.XSHE' '000001.XSHE' '000001.XSHE' '000001.XSHE']  

enable_profile $\spadesuit$ 性能分析enable_profile()回测环境专用API  

开启性能分析功能, 请在所有代码之前调用这句话(即在策略编译页面的代码编辑框最上方放置该代码), 只在点击 '运行回测' 运行的时候才能看到性能分析结果. 开启性能分析之后, 你会在回测结果页面看到性能分析结果. 请注意,不需要时, 请不要调用此函数, 因为它本身会影响程序性能. 对于耗时较长的回测, 建议开启性能分析后先回测一个较短的周期比如一周来分析耗时优化代码, 避免运行时间过长 结果示例(真实输出中没有中文说明):  

// 时间单位: 微秒Timer unit: 1e-06 s  

# // 函数执行总时间  

Total time: 0.00277 s   
// 文件名   
File: user_code.py   
// 函数名   
Function: initialize at line 3  

//  行号, 这一行执行次数,总执行时间,每次执行时间, 这一行执行时间在整个函数的比例  

Line # Hits Time  Per Hit % Time  Line Contents  

# 定义一个全局变量, 保存要操作的股票作的股票池, 这里我们只操作一支股票  

9 1 2739 2739.0 98.9 set_universe([g.security])  

Total time: 0.426325   
File: user_code.py   
Function: handle_data at line 12  

Line # Hits Time  Per Hit % Time  Line Contents  

二二=  

12 handle_data(context, data):  

13 122 398 3.3 0.1 security = g.security  

15 122 168565 1381.7 39.5average_price $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ data[security].mavg(5)16 # 取得上一时间点价格  

17 122 493 4.0 0.1  

current_price $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ data[security].price18  
金  

# 取得当前的现  

19 122 240 2.0 0.1 cash = context.portfolio.available_cash 20  

21点价格高出五天平均价 $\tt{1}\%$ , 则全仓买入  

# 如果上一时间  

22 122 396 3.2 0.1 if  

current_price $>$ 1.01\*average_price: 23   
买多少只股票  

24 30 124 4.1 0.0number_of_shares $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ int(cash/current_price)25 # 购买量大于0 时，下单  

26 30 56 1.9 0.0 ifnumber_of_shares > 0:27 # 买入  

28 30 83190 2773.0 19.5 order(security, +number_of_shares)  

这次买入30 30 16202 540.1 3.8log.info("Buying %s" % (security))31 # 如果上一时间点价格低于五天平均价, 则空仓卖出  

32 92 1119 12.2 0.3 elif  

current_price < average_price and   
context.portfolio.positions[security].amount > 0: 33 # 卖出所有   
股票,使这只股票的最终持有量为0  

34 13 86702 6669.4 20.3 order_target(security, 0)  

卖出  

36 13 8210 631.5 1.9  

log.info("Selling %s" % (security))37 # 画出上一时间  
点价格  

38 122 60630 497.0 14.2 record(stock_price=data[security].price)  

# 策略组合操作  

名称 描述  

set_subportfolios 初始化策略子账户 subportfolios  
SubPortfolio 子账户信息  
transfer_cash 账户间转移资金  

# Tick 级策略专用函数  

Tick 级回测模拟需要权限才可以开通：立即加入会员获取tick 权限或者使用积分兑换tick 权限  

# 注意Tick 级回测必须使用真实价格模式，设置方式详见设置真实价格模式  

股票部分：支持 2017-01-01 至今的tick 数据，提供买五卖五数据，每  
3 秒一次快照  
期货部分：支持 2010-01-01 至今的tick 数据，提供买一卖一数据，每  
0.5 秒一次快照  
场内基金：支持 2019-01-01 至今的tick 数据，提供买五卖五盘口数  
据，每3 秒一次快照  
指数：支持 2017-01-01 至今的tick 数据，每3 秒一次快照  

# Tick 级专用API  

名称 描述handle_tick 策略运行  

subscribe 订阅标的的 tick 事件unsubscribe 取消订阅标的的 tick 事件unsubscribe_all 取消订阅所有 tick 事件  

# Tick 级示例策略  

示例1：  

# 回测时间段2019-06-03 到2019-06-04，运行频率设置为tick# 初始化  

def initialize(context):# 获取起始资金init_cash $=$ context.portfolio.starting_cash# 交易品种为期货set_subportfolios([SubPortfolioConfig(cash $=$ init_cash,  
type='futures')])# 定义一个全局变量, 保存要操作的期货g.code1 $=$ 'RB1909.XSGE'  

# 08:30 运行自定义开盘前运行函数 run_daily(before_market_open, time $=$ '08:30',  

reference_security='RB9999.XSGE') # 15:30 运行自定义收盘后运行函数 run_daily(after_market_open, time $=$ '15:30',   
reference_security $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ 'RB9999.XSGE')  

# 开盘前运行函数  

def before_market_open(context):# 订阅要操作的期货subscribe(g.code1, 'tick')  

# 有tick 事件时运行函数  

def handle_tick(context, tick):# 获取最新的 tick 数据tick_data $=$ get_current_tick(g.code1)print(tick_data)  

# 收盘后运行函数  

def after_market_close(context): # 取消今天订阅的标的 unsubscribe_all()  

示例2：  

# 导入函数库  

import jqdata   
def initialize(context): set_benchmark('000300.XSHG') set_option('use_real_price', True) set_order_cost(OrderCost(close_tax $=\odot$ .001,   
open_commission $=\odot$ .0003, close_commission $=\odot$ .0003,   
min_commission $^{=5}$ ), type $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ 'stock')  

def before_trading_start(context):subscribe('000001.XSHE','tick')  

def handle_tick(context, tick): log.info(tick)  

def after_trading_end(context): unsubscribe_all()  

融资融券专用函数  

# 初始化融资融券账户  

初始化的仓位是不允许直接进行融资融券操作的，因为初始默认subportfolios[0] 中 SubPortfolioConfig 的 type $=$ 'stock'，只允许买卖股票与场内基金等。  

因此要进行融资融券，您需要设定 SubPortfolioConfig 的 type $=$  

'stock_margin'，具体方法如下：  

# def initialize(context):  

## 设置单个账户 # 获取初始资金  

init_cash $=$ context.portfolio.starting_cash  

# 设定账户为融资融券账户，初始资金为 init_cash 变量代表的数值（如不使用设置多账户，默认只有subportfolios[0]一个账户，Portfolio 指向该账户。）  

set_subportfolios([SubPortfolioConfig(cash $=$ init_cash,type $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ 'stock_margin')])  

## 设置多个账户# 获取初始资金，并等分为三份init_cash $=$ context.portfolio.starting_cash/3  

# 设定subportfolios[0]为 股票和基金仓位，初始资金为init_cash 变量代表的数值# 设定subportfolios[1]为 金融期货仓位，初始资金为 init_cash变量代表的数值# 设定subportfolios[2]为 融资融券账户，初始资金为 init_cash变量代表的数值set_subportfolios([SubPortfolioConfig(cash=init_cash,type $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ 'stock'),\SubPortfolioConfig(cash=init_cash,type $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ 'index_futures'),\SubPortfolioConfig(cash=init_cash,type $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ 'stock_margin')])  

# 融资融券专用API  

注意：get_marginsec_stocks 和get_margincash_stocks 无法获取当前未完结交易日的数据，因为交易所的数据尚未生成。  

# 名称 描述  

margincash_interest_rate 设置融资利率  
margincash_margin_rate 设置融资保证金比率  
marginsec_interest_rate 设置融券利率  
marginsec_margin_rate 设置融券保证金比率  
margincash_open 融资买入  
margincash_close 卖券还款  
margincash_direct_refund 直接还款  
marginsec_open 融券卖出  
marginsec_close 买券还券  
marginsec_direct_refund 直接还券  
get_margincash_stocks 获取融资标的列表  
get_marginsec_stocks 获取融券标的列表  
get_mtss 获取融资融券信息  

初始化期货账户  

初始化的仓位是不允许直接买卖期货的，因为初始默认 subportfolios[0] 中SubPortfolioConfig 的 type $=$ 'stock'，只允许买卖股票与场内基金等。  

因此要买卖期货，您需要设定 SubPortfolioConfig 的 type $=$ 'futures'，具  

体方法如下：def initialize(context):  

## 设置单个账户 # 获取初始资金  

init_cash $=$ context.portfolio.starting_cash  

# 设定账户为金融账户，初始资金为 init_cash 变量代表的数值（如不使用设置多账户，默认只有subportfolios[0]一个账户，Portfolio 指向该账户。）  

set_subportfolios([SubPortfolioConfig(cash $=$ init_cash,type $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ 'futures')])  

# 设置运行函数的参考(market_open 为自定义函数，需要自己实现；参考标的默认为沪深300，需要根据策略自己设置，下面只是举例)run_daily(market_open, time $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ 'every_bar',reference_security $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ 'CU9999.XSGE')  

# 期货信息  

名称 描述  
主力连续合约 主力连续合约信息品种指数 品种指数信息  
期货注意事项 期货策略注意事项  

# 期货专用API  

了解更多:关于下单函数的说明  

名称 描述  

get_dominant_future 获取主力合约对应的标的   
get_future_contracts 期货可交易合约列表   
futures_margin_rate 设置期货保证金比例   
is_dangerous 期货保证金预警   
get_price 等 获取期货的行情数据   
order 期货按手数下单   
order_target 期货目标手数下单   
order_value 期货按保证金下单   
order_target_value 期货目标保证金下单  

# 归因分析说明  

# 净值分析  

# 收益分析  

累计收益：累计收益  

对数轴累计收益：对数轴累计收益  

日内收益：每天收益的时间序列图  

滑点对列净值曲线的影响：通过受滑点影响的每日收益计算出的累计收益，受滑点影响的每日收益 $=$ 每日收益 - 滑点 \* 每日换手率 $^\ast2$  

年度收益：分年度计算的累计收益的终值月度收益的时间序列：分月度计算的累计收益的终值  

月度收益热力图：分月度计算的累计收益的终值  

月度收益频次分布图：查看月度收益频次分布  

# 风险指标  

滚动beta 指标：滚动 6 个月 $(21^{\star}\,6$ 个交易日) 和 12 个月 $(21\star12$   
个交易日) 的 beta  
滚动sharpe 指标（6 个月时间窗口）：滚动 6 个月 $(21^{\star}\,6$ 个交易日)  
的夏普比率  
前五大回撤区间：找到前5 大回撤区间  

# 持仓分析  

前10 大持仓：显示股票前10 大持仓  
持仓收益：显示股票的持仓收益，其中内部收益率为一项投资可望到达的报酬率。  
日交易股数：每日交易股数的绝对值的和  
日换手率：(每日交易市值的绝对值的和 / 2) / 当日总市值  

基准指沪深300 指数，采用减法超额，详细见Brinson 模型介绍  

总超额收益：策略相对于基准获得的额外收益，是下面主动配置收益、标的选择收益以及交互效应收益的汇总。  
主动配置收益：主动配置的收益来源于对上涨行业的超配或对下跌行业的低配，是衡量对大类资产强弱走势进行判断的能力。如果大于零则意味着看准了市场大方向，并且高配了好的资产。  
标的选择收益：标的选择的收益来源于对行业中表现好的个股的超配或对行业中表现差个股的低配。是对能否选出高于市场基准收益的资产，即在相同资金分配比例下，能否获得更高的收益能力的衡量。如果大于零则意味着拥有高于市场的个股选择能力。  
互动收益：在总超额收益中，除去主动配置收益和标的选择收益，也就是超额收益中同时收到主动配置与标的选择影响的部分，就是互动收益。  

因子分析风格分析  

Fama-French 五因子模型，是将超额收益分为5 个因子来解释，具体如下表  

<html><body><table><tr><td>因子</td><td>因子解释</td><td>构造方式</td><td>回归系数解释</td></tr><tr><td>市场因子 (RM)</td><td>受市场走 势变化造 成的不确 定性收益</td><td>市场组合收益 率减去无风险 收益率</td><td>当 βi>0βi>0，说明在样本期间 内，该组合的运行趋势与市场整 体运行趋势是一致的，如果大于</td></tr><tr><td>规模因子</td><td>率 由于上市</td><td>小市值组合的</td><td>1，说明该组合可能偏激进型。</td></tr><tr><td>(SMB)</td><td>公司规模 不同导致 的收益率 差异</td><td>收益率减去大 市值组合的收 益率</td><td>当 Si>Osi>O，说明该组合可能偏 好于配置小盘股</td></tr></table></body></html>  

<html><body><table><tr><td>估值因子 (HML)</td><td>由于上市 公司账面 市值比不 同导致的 收益率差</td><td>较高账面市值 比的公司组合 收益率减去减 低账面市值比 的公司组合收 益率</td><td>当 hi>0hi>0，说明该组合可能 偏好于配置账面市值比高的公 司，也就是价值型的公司</td></tr><tr><td>盈利因子 (RMW)</td><td>异 由于盈利 水平不同 造成的收 益率差异</td><td>高盈利公司组 合收益率减去 低盈利公司组 合收益率</td><td>当 ri>Ori>0，说明该组合可能偏 好于配置盈利高的公司</td></tr><tr><td>投资因子 (CMA)</td><td>由于投资 水平的不 同造成的 收益率差 异</td><td>投资率低的公 司组合收益率 减去投资率高 的公司组合收 益率</td><td>当 ci>0ci>0，说明该组合可能偏 好于配置投资率较低的公司</td></tr></table></body></html>  

风险分析  

说明:  

• 风险因子暴露对比中，基准风险因子暴露度为沪深300 指数股票池中股票风险暴露的市值加权平均；风险暴露的基准都是 hs300 指数，所以只要时间段是一样的，暴露度就是一样的风险因子暴露对比中，风险因子暴露差值代表了策略组合的风险敞口暴露，如果风险因子暴露差值接近0，说明策略组合对该风险因子是风险中性的，即策略组合不暴露与这个风险因子；因子暴露差值就是回测的组合和基准（hs300）组合风险暴露的差，因为这10 个因子是大家公认的风险因子，而基准组合被认为是无风险的；所以大家都认为和基准（hs300）组合风险暴露的差越趋近于0，风险暴露越低，策略收益的稳定性越好；大于或小于基准组合风险，可以参考相应因子的定义，调整对应的持仓，将风险暴露趋近于基准组合风险暴露收益详情中，Backtest 为回测的收益;  

• 收益详情中，国家因子是在巴若风险模型中，横截面线性回归的截距项（一共有10 个风格因子，11 个行业因子(jq_l1)，和1 个国家因子）;国家因子的因子值为常数1，因子收益(线性回归的系数)代表了大盘整体的收益;  
• 收益详情中，特殊收益是指收益中剔除已知可解释收益（因子收益）之外的，其他不可解释的收益；  
• 收益详情中，其他的一些收益的解释，点击页面上的提示即可看到；  

对收益分析的最后一部分就是查看该策略在各个方面和基准相比的偏差，通过10 个风格因子来判别，具体解释如下表。  

解释市值 捕捉大盘股和小盘股之间的收益差异非线性市 描述了无法由规模因子解释的但与规模有限的收益差异，通常代值 表中盘股杠杆 描述了高杠杆股票与低杠杆股票之间的收益差异账面市值 描述了股票估值高低不同而产生的收益差异，即价值因子比成长 描述了对销售或盈利增长预期不同而产生的收益差异动量 描述了过去半年到一年里相对强势的股票与弱势股票之间的差异盈利能力 描述了由盈利收益导致的收益差异贝塔 表征了股票相对于市场的波动敏感程度残差波动 解释了剥离了市场风险后的波动率高低产生的收益率差异率流动性 解释了由股票相对的交易活跃度不同而产生的收益率差异。  

# 策略示例  

当价格高于5 日均线平均价格1.05 时买入，当价格低于5 日平均价格0.95 时卖出。  

# 导入聚宽函数库import jqdata  

# 初始化函数，设定要操作的股票、基准等等def initialize(context):# 定义一个全局变量, 保存要操作的股票# 000001(股票:平安银行)g.security $=$ '000001.XSHE'# 设定沪深300 作为基准set_benchmark('000300.XSHG')# 开启动态复权模式(真实价格)set_option('use_real_price', True)  

# 每个单位时间(如果按天回测,则每天调用一次,如果按分钟,则每分钟调用一次)调用一次  

def handle_data(context, data): security $=$ g.security # 获取股票的收盘价 close_data $=$ attribute_history(security, 5, '1d',   
['close']) # 取得过去五天的平均价格 MA5 $=$ close_data['close'].mean() # 取得上一时间点价格 current_price $=$ close_data['close'][-1] # 取得当前的现金 cash $=$ context.portfolio.available_cash  

# 如果上一时间点价格高出五天平均价 $^{5\%}$ , 则全仓买入if (current_price > 1.05\*MA5) and (cash>0):# 用所有 cash 买入股票order_value(security, cash)# 记录这次买入log.info("Buying %s" % (security))  

elif current_price < 0.95\*MA5 and context.portfolio.positions[security].closeable_amount > 0:  

# 卖出所有股票,使这只股票的最终持有量为0 order_target(security, 0)   
# 记录这次卖出   
log.info("Selling %s" % (security))  

# 画出上一时间点价格record(stock_price=current_price)  

# 多股票持仓示例  

这是一个较简单的多股票操作示例，当价格高于三天平均价1.005 则买入100股，当价格小于三天平均价0.995 则卖出。  

# 导入聚宽函数库import jqdatadef initialize(context):# 初始化此策略# 设置我们要操作的股票池  

g.stocks $=$ ['000001.XSHE','000002.XSHE','000004.XSHE','000005.XSHE']# 设定沪深300 作为基准set_benchmark('000300.XSHG')# 开启动态复权模式(真实价格)set_option('use_real_price', True)  

# 每个单位时间(如果按天回测,则每天调用一次,如果按分钟,则每分钟调用一次)调用一次  

def handle_data(context, data): # 循环每只股票  

for security in g.stocks:# 得到股票之前3 天的平均价vwap $=$ data[security].vwap(3)# 得到上一时间点股票收盘价price $=$ data[security].close# 得到当前资金余额cash $=$ context.portfolio.available_cash  

# 如果上一时间点价格小于三天平均价\*0.995，并且持有该股票，卖出  

if price < vwap \* 0.995 and context.portfolio.positions[security].closeable_amount > 0:  

# 下入卖出单   
order(security,-100)   
# 记录这次卖出   
log.info("Selling %s" % (security))  

# 如果上一时间点价格大于三天平均价\*1.005，并且有现金余额，买入  

elif price > vwap $\star$ 1.005 and cash > 0: # 下入买入单 order(security,100) # 记录这次买入 log.info("Buying %s" % (security))  

# 多股票追涨策略  

当股票在当日收盘30 分钟内涨幅到达 $9.5\%{\sim}9.9\%$ 时间段的时候，我们进行买入，在第二天开盘卖出。注意：请按照分钟进行回测该策略。  
# 导入聚宽函数库  
import jqdata  

# 初始化程序, 整个回测只运行一次def initialize(context):# 开启动态复权模式(真实价格)set_option('use_real_price', True)# 每天买入股票数量g.daily_buy_count  = 5  

# 设置我们要操作的股票池, 这里我们操作多只股票，下列股票选自计算机信息技术相关板块  

g.stocks $=$ get_industry_stocks('I64') + get_industry_stocks('I65')  

# 防止板块之间重复包含某只股票, 排除掉重复的, g.stocks 现在是一个集合(set)g.stocks $=$ set(g.stocks)  

# 让每天早上开盘时执行 morning_sell_all run_daily(morning_sell_all, '09:30')  

def morning_sell_all(context):# 将目前所有的股票卖出for security in context.portfolio.positions:# 全部卖出order_target(security, 0)# 记录这次卖出log.info("Selling %s" % (security))  

def before_trading_start(context): # 今天已经买入的股票 g.today_bought_stocks $=$ set()  

# 得到所有股票昨日收盘价, 每天只需要取一次, 所以放在before_trading_start 中g.last_df = history(1,'1d','close',g.stocks)  

# 在每分钟的第一秒运行, data 是上一分钟的切片数据def handle_data(context, data):  

# 判断是否在当日最后的2 小时，我们只追涨最后2 小时满足追涨条件的股票  

if context.current_dt.hour < 13: return  

# 每天只买这么多个  

if len(g.today_bought_stocks) >= g.daily_buy_count: return  

# 只遍历今天还没有买入的股票 for security in (g.stocks - g.today_bought_stocks):  

# 得到当前价格price $=$ data[security].close# 获取这只股票昨天收盘价last_close $=$ g.last_df[security][0]# 如果上一时间点价格已经涨了9.5%\~9.9%# 今天的涨停价格区间大于1 元，今天没有买入该支股票if price/last_close > 1.095and price/last_close < 1.099and data[security].high_limit# 得到当前资金余额cash $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ context.portfolio.available_cash# 计算今天还需要买入的股票数量need_count $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ g.daily_buy_count  

# 把现金分成几份,  

buy_cash $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ context.portfolio.available_cash / need_count  

# 买入这么多现金的股票 order_value(security, buy_cash)  

# 放入今日已买股票的集合 g.today_bought_stocks.add(security)  

# 记录这次买入  

log.info("Buying %s" % (security))  

# 买够5 个之后就不买了  

if len(g.today_bought_stocks) >= g.daily_buy_count: break  

# 万圣节效应策略  

股市投资中的“万圣节效应”是指在北半球的冬季(11 月至4 月份)，股市回报通常明显高於夏季(5 月至10 月份)。这里我们选取了中国蓝筹股，采用10 月15日后买入，5 月15 日后卖出的简单策略进行示例。  

# 导入聚宽函数库import jqdata# 初始化此策略  

def initialize(context):# 开启动态复权模式(真实价格)set_option('use_real_price', True)  

# 设置我们要操作的股票池，这里我们选择蓝筹股g.stocks $=$  

['000001.XSHE','600000.XSHG','600019.XSHG','600028.XSHG' '600030.XSHG','600036.XSHG','600519.XSHG','601398.XSHG', 601857.XSHG','601988.XSHG']  

def handle_data(context, data):  

# 得到每只股票可以花费的现金，这里我们使用总现金股票数数量  

cash $=$ context.portfolio.available_cash / len(g.stocks)  

# 获取数据  

hist $=$ history(1,'1d','close',g.stocks)  

# 循环股票池  

for security in g.stocks:# 得到当前时间today $=$ context.current_dt# 得到该股票上一时间点价格current_price $=$ hist[security][0]  

# 如果当前为10 月且日期大于15 号，并且现金大于上一时间点价格，并且当前该股票空仓  

if today.month $=~1\textcircled{2}$ and today.day > 15 and cash > current_price and  

context.portfolio.positions[security].closeable_amount == 0:  

order_value(security, cash) # 记录这次买入 log.info("Buying %s" % (security))  

# 如果当前为5 月且日期大于15 号，并且当前有该股票持仓，则卖出  

elif today.month $\mathit{\Theta}=\mathit{\Theta}\;5$ and today.day > 15 and context.portfolio.positions[security].closeable_amount > 0:  

# 全部卖出  

order_target(security, 0) # 记录这次卖出 log.info("Selling %s" % (security))  