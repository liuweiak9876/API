# XtQuant 能提供哪些服务  

XtQuant 是基于迅投MiniQMT 衍生出来的一套完善的Python 策略运行框架，对外以Python 库的形式提供策略交易所需要的行情和交易相关的API 接口。  

# #XtQuant 运行依赖环境  

XtQuant 目前提供的库包括 64 位 Python 3.6、3.7、3.8、3.9、3.10、3.11、3.12版本，不同版本的 Python 导入时会自动切换。 在运行使用 XtQuant 的程序前需要先启动 MiniQMT 客户端。  

# #XtQuant 运行逻辑  

Xtdata 作为行情模块，本模块旨在提供精简直接的数据满足量化交易者的数据需求，主要提供行情数据（历史和实时的K 线和分笔）、财务数据、合约基础信息、板块和行业分类信息等通用的行情数据。  

Xttrader 作为交易模块，封装了策略交易所需要的 Python API 接口，可以和MiniQMT 客户端交互进行报单、撤单、查询资产、查询委托、查询成交、查询持仓以及接收资金、委托、成交和持仓等变动的主推消息。  

# XtQuant.XtData 行情模块  

xtdata 是xtquant 库中提供行情相关数据的模块，本模块旨在提供精简直接的数据满足量化交易者的数据需求，作为python 库的形式可以被灵活添加到各种策略脚本中。  

主要提供行情数据（历史和实时的K 线和分笔）、财务数据、合约基础信息、板块和行业分类信息等通用的行情数据。  

# #版本信息  

2020-09-01 o 初稿  

2020-09-07  

o 添加获取除权数据的接口get_divid_factors，附录添加除权数据字段说明o 获取合约信息、获取合约类型接口完善o 获取交易日列表接口get_trading_dates 支持指定日期范围  

2020-09-13o 添加财务数据接口，调整获取和下载财务数据接口的说明，添加财务数据报表字段列表o  将 “补充” 字样调整为 “下载”，“supply” 接口调整为 “download”  
2020-09-13o  将volumn 拼写错误修正为volume，影响范围：tick 和l2quote 周期行情数据 - 成交量字段■ 合约基础信息 - 总股本、流通股本  
2020-11-23o  合约基础信息CreateDate OpenDate 字段类型由int 调整为stro  添加数据字典部分，添加level2 数据字段枚举值说明  
2021-07-20o 添加新版下载数据接口下载行情数据 download_history_data2■ 下载财务数据 download_financial_data2  
2021-12-30o 数据字典调整▪  委托方向、成交类型添加关于上交所、深交所撤单信息的区分说明  
2022-06-27数据字典调整▪  K 线添加前收价、停牌标记字段  
2022-09-30o 添加交易日历相关接口■ 获取节假日数据 get_holidays获取交易日历 get_trading_calendar■ 获取交易时段 get_trade_times  
2023-01-04o 添加千档行情获取  
2023-01-31o 可转债基础信息的下载 download_cb_datao 可转债基础信息的获取 get_cb_info  

2023-02-06添加连接到指定ip 端口的接口 reconnect  

2023-02-07o 支持QMT 的本地Python 模式o 优化多个QMT 同时存在的场景，自动选择xtdata 连接的端口  

2023-03-27o 新股申购信息获取 get_ipo_info  

2023-04-13本地python 模式下运行VBA 函数  

2023-07-27文档部分描述修改  

2023-08-21o 数据接口支持投研版特色数据参考 接口概述 - 常用类型说明 - 周期 - 投研版 - 特色数据o 获取合约基础信息 get_instrument_detail 返回字段调整增加 ExchangeCode UniCode添加获取可用周期列表的接口 get_period_list  

2023-10-11o get_market_data_ex 支持获取ETF 申赎清单数据数据字典添加 现金替代标志  

2023-11-09o download_history_data 添加增量下载参数，支持指定起始时间的增量下载  
2023-11-22o get_trading_calendar 不再支持tradetimes 参数  

2023-11-27o ETF 申赎清单信息下载 download_etf_infoo ETF 申赎清单信息获取 get_etf_info  

2023-11-28 添加节假日下载download_holiday_data  

2023-12-27o 获取板块成份股列表接口增加北交所板块  

2024-01-19o get_market_data_ex 支持获取期货历史主力合约数据o get_option_detail_data 支持获取商品期权品种的数据o get_market_data_ex 支持获取日线以上周期的K 线数据周线1w、月线1mon、季度线1q、半年线1hy、年线1y  

2024-01-22 o get_trade_times 改名为get_trading_tim $\bigcirc$ get_trading_time 更新实现逻辑  

2024-01-26获取合约基础信息 get_instrument_detail 支持获取全部合约信息字段获取最新交易日k 线数据get_full_kline  

2024-05-27  

o get_stock_list_in_sector 增加real_timetag 参数  

# #接口概述  

# #运行逻辑  

xtdata 提供和MiniQmt 的交互接口，本质是和MiniQmt 建立连接，由  

MiniQmt 处理行情数据请求，再把结果回传返回到python 层。使用的行情服务器以及能获取到的行情数据和MiniQmt 是一致的，要检查数据或者切换连接时直接操作MiniQmt 即可。  

对于数据获取接口，使用时需要先确保MiniQmt 已有所需要的数据，如果不足可以通过补充数据接口补充，再调用数据获取接口获取。  

对于订阅接口，直接设置数据回调，数据到来时会由回调返回。订阅接收到的数据一般会保存下来，同种数据不需要再单独补充。  

# #接口分类  

行情数据（K 线数据、分笔数据，订阅和主动获取的接口）功能划分（接口前缀）subscribe_ / unsubscribe_ 订阅/反订阅get_ 获取数据download_ 下载数据  

常见用法level1 数据的历史部分用download_history_data 补充，实时部分用subscribe_XXX 订阅，使用get_XXX 获取level2 数据实时部分用subscribe_XXX 订阅，用get_l2_XXX 获取。level2 函数无历史数据存储，跨交易日后数据清理  

# 财务数据  

合约基础信息  

基础行情数据板块分类信息等基础信息  

# #常用类型说明  

stock_code - 合约代码  

格式为 code.market，例如000001.SZ 600000.SH 000300.SHperiod - 周期，用于表示要获取的周期和具体数据类型  

level1 数据  

tick - 分笔数据  
■ 1m - 1 分钟线  
■ $5\mathrm{m}\textrm{-}5$ 分钟线$15\mathrm{m}\mathrm{~-~}15$ 分钟线  
■ $30\mathrm{m\cdot30}$ 分钟线  
■ 1h - 1 小时线  
■ 1d - 日线  
■ 1w - 周线  
■ 1mon - 月线1q - 季度线1hy - 半年线1y - 年线  

投研版 - 特色数据  

warehousereceipt - 期货仓单  
futureholderrank - 期货席位  
interactiveqa - 互动问答  
逐笔成交统计transactioncount1m - 逐笔成交统计1 分钟级transactioncount1d - 逐笔成交统计日级  
delistchangebond - 退市可转债信息  
replacechangebond - 待发可转债信息  
specialtreatment - ST 变更历史  
港股通（深港通、沪港通）资金流向northfinancechange1m - 港股通资金流向1 分钟级northfinancechange1d - 港股通资金流向日级  
dividendplaninfo - 红利分配方案信息  
historycontract - 过期合约列表  
optionhistorycontract - 期权历史信息  
historymaincontract - 历史主力合约  
stoppricedata - 涨跌停数据  
snapshotindex - 快照指标数据  

时间范围，用于指定数据请求范围，表示的范围是[start_time, end_time]区间（包含前后边界）中最后不多于count 个数据  

o start_time - 起始时间，为空则认为是最早的起始时间  
o end_time - 结束时间，为空则认为是最新的结束时间  
o count - 数据个数，大于0 为正常限制返回个数，等于0 为不需要返回，-1 为返回全部  
o 通常以[start_time $=$ '', end_time $=$ '', count $=-1]$ 表示完整数据范围，但数据请求范围过大会导致返回时间变长，需要按需裁剪请求范围  

dividend_type - 除权方式，用于K 线数据复权计算，对tick 等其他周期数据无效o none 不复权  

o front 前复权  
o back 后复权  
o front_ratio 等比前复权o back_ratio 等比后复权  

其他依赖库 numpy、pandas 会在数据返回的过程中使用  

本模块会尽可能减少对numpy 和pandas 库的直接依赖，以允许使用者在不同版本的库之间自由切换  
o pandas 库中旧的三维数据结构Panel 没有被使用，而是以dict 嵌套DataFrame 代替（后续可能会考虑使用xarray 等的方案，也欢迎使用者提供改进建议）  
o  后文中会按常用规则分别简写为np、pd，如np.ndarray、pd.DataFrame  

# #请求限制  

全推数据是市场全部合约的切面数据，是高订阅数场景下的有效解决方案。持续订阅全推数据可以获取到每个合约最新分笔数据的推送，且流量和处理效率都优于单股订阅  

单股订阅行情是仅返回单股数据的接口，建议单股订阅数量不超过50。如果订阅数较多，建议直接使用全推数据  

板块分类信息等静态信息更新频率低，无需频繁下载，按周或按日定期下载更新即可  

# #接口说明  

# #行情接口  

# #订阅单股行情  

# subscribe_quote(stock_code, period='1d', start_time='', end_time='', count=0, callback=None)  

释义o 订阅单股的行情数据，返回订阅号o 数据推送从callback 返回，数据类型和period 指定的周期对应o 数据范围代表请求的历史部分的数据范围，数据返回后会进入缓存，用于保证数据连续，通常情况仅订阅数据时传count $=0$ 即可  
参数o stock_code - string 合约代码o period - string 周期o start_time - string 起始时间  

end_time - string 结束时间o count - int 数据个数callback - 数据推送回调回调定义形式为on_data(datas)，回调参数datas 格式为{ stock_code : [data1, data2, ...] }def on_data(datas):for stock_code in datas:print(stock_code, datas[stock_code])  

返回o 订阅号，订阅成功返回大于0，失败返回-1  
备注单股订阅数量不宜过多，详见 接口概述-请求限制  

# #订阅全推行情  

# subscribe_whole_quote(code_list, callback=None)  

释义o 订阅全推行情数据，返回订阅号o 数据推送从callback 返回，数据类型为分笔数据  
参数code_list - 代码列表，支持传入市场代码或合约代码两种方式传入市场代码代表订阅全市场，示例：['SH', 'SZ']传入合约代码代表订阅指定的合约，示例：['600000.SH','000001.SZ']callback - 数据推送回调回调定义形式为on_data(datas)，回调参数datas 格式为 { stock1 :data1, stock2 : data2, ... }def on_data(datas):for stock_code in datas:print(stock_code, datas[stock_code])  
返回o 订阅号，订阅成功返回大于0，失败返回-1  
备注o 订阅后会首先返回当前最新的全推数据  

# #反订阅行情数据  

unsubscribe_quote(seq)  

释义o 反订阅行情数据  
参数o seq - 订阅时返回的订阅号  
返回无  
备注o 无  

# #阻塞线程接收行情回调  

# run()  

释义o 阻塞当前线程来维持运行状态，一般用于订阅数据后维持运行状态持续处理回调  
参数o seq - 订阅时返回的订阅号  
返回o 无  
备注o 实现方式为持续循环sleep，并在唤醒时检查连接状态，若连接断开则抛出异常结束循环  

# #订阅模型  

subscribe_formula(formula_name, stock_code, period, start_time = '', end_time = '', count = -1, dividend_type = None, extend_param = {}, callback = None)  

释义o 订阅vba 模型运行结果，需连接投研端使用  
参数formula_name:str,模型名stock_code:str,模型主图代码形式如'stkcode.market',如'000300.SH'；period:str,K 线周期类型 可选范围： 'tick':分笔线 '1d':日线 '1m':分钟线 '3m':三分钟线 '5m':5 分钟线 '15m':15 分钟线 '30m':30  

分钟线 '1h':小时线 '1w':周线 '1mon':月线 '1q':季线 '1hy':半年线'1y':年线  

start_time:str,模型运行起始时间,形如:'20200101';默认为空视为最早o end_time:str,模型运截止时间,形如:'20200101';默认为空视为最新o count:int,模型运行范围为向前count 根bar,默认为-1 运行所有bardividend_type:str,复权方式,默认为主图除权方式,可选范围：'none':不复权 'front':向前复权 'back':向后复权 'front_ratio':等比向前复权 'back_ratio':等比向后复权extend_param:dict,模型的入参,{参数名:参数值},形如{'a':1,'__basket':{}};__basket:dict,可选参数,组合模型的股票池权重,形如{'600000.SH':0.06,'000001.SZ':0.01}  
返回：o int 订阅成功时为订阅ID，可用于后续反订阅,失败返回-1  
备注:o 使用该函数时需要补充号本地K 线或分笔数据  

# #反订阅模型  

unsubscribe_formula(subID)  

释义o 反订阅模型  
参数o subID:int 模型订阅号  
返回bool ,反订阅成功为True,失败为False  

# #调用模型  

call_formula(formula_name,stock_code,period,start_time="",end_time="",count=- ,dividend_type="none",extend_param={})  

释义  

o  获取vba 模型运行结果，使用前要注意补充本地K 线数据或分笔数据•  参数：o formula_name: str，模型名称名o stock_code: str，模型主图代码形式如'stkcode.market'，如'000300.SH'o period: str，K 线周期类型  

可选范围：  

'tick': 分笔线  
'1d': 日线  
'1m': 分钟线  
'3m': 三分钟线  
'5m': 5 分钟线  
'15m': 15 分钟线  
'30m': 30 分钟线  
'1h': 小时线  
'1w': 周线  
'1mon': 月线  
'1q': 季线  
'1hy': 半年线  
'1y': 年线  

o start_time: str，模型运行起始时间，形如:'20200101'，默认为空视为最早o end_time: str，模型运行截止时间，形如:'20200101'，默认为空视为最新o count: int，模型运行范围为向前 count 根 bar，默认为 -1 运行所有 baro dividend_type: str，复权方式，默认为主图除权方式  

可选范围：  

'none': 不复权  
'front': 向前复权  
'back': 向后复权  
'front_ratio': 等比向前复权  
'back_ratio': 等比向后复权  

o extend_param: dict，模型的入参，例如 {"模型名:参数名": 参数值}，例如在跑模型 MA 时，{'MA:n1': 1}  

入参可以添加 __basket: dict，组合模型的股票池权重，形如 {'__basket': $\{^{\prime}600000.5\mathrm{H}^{\prime}\colon0.06,^{\prime}000001.S{\mathrm{Z}}^{\prime}\colon0.01\}\}$ 如果在跑一个模型1 的时候，模型1 调用了模型2，如果只想修改模型2 的参数可以传 {'模型2: 参数': 参数值}  

o dict{ 'dbt':0,#返回数据类型，0:全部历史数据 'timelist':[...],#返回数据时间范围list, 'outputs':{'var1':[...],'var2':[...]}#输出变量名：变量值list }  

# #批量调用模型  

call_formula_batch(formula_names,stock_codes,period,start_time="",end_time="",count=- 1,dividend_type="none",extend_params=[])  

释义  

o 批量获取vba 模型运行结果，使用前要注意补充本地K 线数据或分笔数据参数：o formula_names: list，包含要批量运行的模型名o stock_codes: list，包含要批量运行的模型主图代码形式'stkcode.market'，如 '000300.SH'o period: str，K 线周期类型  

可选范围：  

'tick': 分笔线  
'1d': 日线  
'1m': 分钟线  
'3m': 三分钟线  
'5m': 5 分钟线  
'15m': 15 分钟线  
'30m': 30 分钟线  
'1h': 小时线  
'1w': 周线  
'1mon': 月线  
'1q': 季线  
'1hy': 半年线  
'1y': 年线  

o start_time: str，模型运行起始时间，形如:'20200101'，默认为空视为最早o end_time: str，模型运行截止时间，形如:'20200101'，默认为空视为最新o count: int，模型运行范围为向前 count 根 bar，默认为 -1 运行所有 baro dividend_type: str，复权方式，默认为主图除权方式  

可选范围：  

'none': 不复权  
'front': 向前复权  
'back': 向后复权  
'front_ratio': 等比向前复权  
'back_ratio': 等比向后复权  

extend_params: list，包含每个模型的入参，形如 [{"模型名:参数名": 参数值}]，例如在跑模型 MA 时，{'MA:n1': 1}  

入参可以添加 __basket: dict，组合模型的股票池权重，形如 {'__basket': $\{^{\prime}600000.5\mathrm{H}^{\prime}\colon0.06,^{\prime}000001.S{\mathrm{Z}}^{\prime}\colon0.01\}\}$ 如果在跑一个模型1 的时候，模型1 调用了模型2，如果只想修改模型2 的参数可以传 {'模型2: 参数': 参数值}  

返回 o list[dict]  

dict 说明:formula:模型名stock:品种代码argument:参数result:dict 参考call_formula 返回结果  

# #生成因子数据  

generate_index_data(formula_name, formula_param = {}, stock_list = [], period = '1d', dividend_type = 'none', start_time = '', end_time = '', fill_mode = 'fixed', fill_value = float('nan'), result_path = None)  

释义  

o 在本地生成因子数据文件，文件格式为feather参数o formula_name:str 模型名称o formula_param:dict 模型参数,例如 {'param1': 1.0, 'param2': 'sym'}o stock_list:list 股票列表o period:str 周期可选范围'1m' '5m' '1d'dividend_type:str 复权方式可选范围'none' - 不复权'front_ratio' - 等比前复权■ 'back_ratio' - 等比后复权o start_time:str 起始时间 格式为'20240101' 或 '20240101000000'o end_time: str 结束时间 格式为'20241231' 或 '20241231235959'fill_mode:str 空缺填充方式可选范围■ 'fixed' - 固定值填充■ 'forward' - 向前延续o fill_value:float 填充数值float('nan') - 以NaN 填充o result_path:str 结果文件路径，feather 格式返回 None  

# #获取行情数据  

get_market_data(field_list=[], stock_list=[], period='1d', start_time='', end_time='', count=-1, dividend_type='none', fill_data=True)  

样o 从缓存获取行情数据，是主动获取行情的主要接口  
参数o field_list - list 数据字段列表，传空则为全部字段o stock_list - list 合约代码列表o period - string 周期o start_time - string 起始时间o end_time - string 结束时间o count - int 数据个数o 默认参数，大于等于0 时，若指定了start_time，end_time，此时以end_time 为基准向前取count 条；若start_time，end_time 缺省，默认取本地数据最新的count 条数据；若start_time，end_time，count 都缺省时，默认取本地全部数据o dividend_type - string 除权方式o fill_data - bool 是否向后填充空缺数据  
返回$\bigcirc$ period 为 $1\mathrm{m}~5\mathrm{m}~1\mathrm{d}$ 等K 线周期时■ 返回dict { field1 : value1, field2 : value2, ... }field1, field2, ... ：数据字段value1, value2, ... ：pd.DataFrame 数据集，index 为stock_list，columns 为time_list各字段对应的DataFrame 维度相同、索引相同period 为tick 分笔周期时返回dict { stock1 : value1, stock2 : value2, ... }stock1, stock2, ... ：合约代码value1, value2, ... ：np.ndarray 数据集，按数据时间戳time 增序排列  
备注o 获取lv2 数据时需要数据终端有lv2 数据权限o 时间范围为闭区间  

# #获取本地行情数据  

# get_local_data(field_list=[], stock_list=[], period='1d', start_time='', end_time='', count=-1, dividend_type='none', fill_data=True, data_dir=data_dir)  

释义o 从本地数据文件获取行情数据，用于快速批量获取历史部分的行情数据  
参数o field_list - list 数据字段列表，传空则为全部字段o stock_list - list 合约代码列表o period - string 周期o start_time - string 起始时间$\bigcirc$ end_time - string 结束时间  

o count - int 数据个数o dividend_type - string 除权方式o fill_data - bool 是否向后填充空缺数据$\bigcirc$ data_dir - string MiniQmt 配套路径的userdata_mini 路径，用于直接读取数据文件。默认情况下xtdata 会通过连接向MiniQmt 直接获取此路径，无需额外设置。如果需要调整，可以将数据路径作为data_dir 传入，也可以直接修改xtdata.data_dir 以改变默认值  

返回o period 为 $1\mathrm{m}~5\mathrm{m}~1\mathrm{dK}$ 线周期时返回dict { field1 : value1, field2 : value2, ... }field1, field2, ... ：数据字段value1, value2, ... ：pd.DataFrame 数据集，index 为stock_list，columns 为time_list各字段对应的DataFrame 维度相同、索引相同period 为tick 分笔周期时■ 返回dict { stock1 : value1, stock2 : value2, ... }■ stock1, stock2, ... ：合约代码value1, value2, ... ：np.ndarray 数据集，按数据时间戳time 增序排列  
备注仅用于获取level1 数据  

# #获取全推数据  

# get_full_tick(code_list)  

释义o 获取全推数据  
参数code_list - 代码列表，支持传入市场代码或合约代码两种方式传入市场代码代表订阅全市场，示例：['SH', 'SZ']传入合约代码代表订阅指定的合约，示例：['600000.SH','000001.SZ']  
返回o dict 数据集 { stock1 : data1, stock2 : data2, ... }  
备注o 无  

# #获取除权数据  

# get_divid_factors(stock_code, start_time='', end_time='  

释义o 获取除权数据  
参数o stock_code - 合约代码o start_time - string 起始时间o end_time - string 结束时间  
返回o pd.DataFrame 数据集  
备注o 无  

# #下载历史行情数据  

download_history_data(stock_code, period, start_time='', end_time='', incrementally = None)  

释义o 补充历史行情数据  
参数o stock_code - string 合约代码o period - string 周期o start_time - string 起始时间o end_time - string 结束时间o incrementally - 是否增量下载■ bool - 是否增量下载■ None - 使用start_time 控制，start_time 为空则增量下载  
返回o 无  
备注o 同步执行，补充数据完成后返回  

download_history_data2(stock_list, period, start_time='', end_time='', callback=None,incrementally = None)  

释义o 补充历史行情数据，批量版本  
参数stock_list - list 合约列表period - string 周期start_time - string 起始时间end_time - string 结束时间callback - func 回调函数参数为进度信息dict  
total - 总下载个数  
finished - 已完成个数  
stockcode - 本地下载完成的合约代码  
message - 本次信息  
返回o 无  
备注o 同步执行，补充数据完成后返回o 有任务完成时通过回调函数返回进度信息  

# #下载过期 （退市） 合约信息  

# download_history_contracts()  

释义o 下载过期（退市）合约信息，过期（退市）标的列表可以通过get_stock_list_in_sector 获取  
参数o None  
返回o 无  
备注o 同步执行，补充数据完成后返回o 过期板块名称可以通过 print([i for i in xtdata.get_sector_list() if "过期" in i]) 查看下载完成后，可以通过 xtdata.get_instrument_detail() 查看过期（退市）合约信息  

# #获取节假日数据  

get_holidays()  

释义o 获取截止到当年的节假日日期  
参数o 无  
返回o list，为8 位的日期字符串格式  
备注o 无  

# #获取交易日历  

# get_trading_calendar(market, start_time = '', end_time = '')  

释义o 获取指定市场交易日历  
参数o market - str 市场o start_time - str 起始时间，8 位字符串。为空表示当前市场首个交易日时间o end_time - str 结束时间，8 位字符串。为空表示当前时间  
返回o 返回list，完整的交易日列表  
备注o 结束时间可以填写未来时间，获取未来交易日。需要下载节假日列表。  

# #获取交易时段  

# get_trading_time(stockcode)  

释义o 返回指定代码的交易时段  
参数o stockcode - str 合约代码（例如600000.SH）  
返回o list，返回交易时段列表，第一位是开始时间，第二位结束时间，第三位交易类型 （2 - 开盘竞价， 3 - 连续交易， 8 - 收盘竞价， 9 - 盘后定价）。时间单位为“秒”  
备注o 股票代码错误时返回空列表o 跨天时以当前天0 点为起始，前一天为负，下一天多86400#需要转换为datetime 时，可以用以下方法转换import datetime as dtdt.datetime.combine(dt.date.today(), dt.time()) + dt.timedelta(seconds = 34200)  

# #可转债基础信息的下载  

download_cb_data()  

释义o 下载全部可转债信息  
参数o 无  
返回  

o 无 备注 o 无  

# #获取可转债基础信息  

# get_cb_info(stockcode)  

释义o 返回指定代码的可转债信息  
参数o stockcode - str 合约代码（例如600000.SH）  
返回o dict，可转债信息  
备注o 需要先下载可转债数据  

# #获取新股申购信息  

# get_ipo_info(start_time, end_time)  

释义o 返回所选时间范围的新股申购信息  
参数o start_time: 开始日期（如：'20230327'）o end_time: 结束日期（如：'20230327'）o start_time 和 end_time 为空则返回全部数据  
返回o list[dict]，新股申购信息o securityCode - string 证券代码codeName - string 代码简称market - string 所属市场o actIssueQty - int 发行总量，单位：股（ onlineIssueQty - int 网上发行量, 单位：股o onlineSubCode - string 申购代码onlineSubMaxQty - int 申购上限, 单位：股o publishPrice - float 发行价格isProfit - int 是否已盈利 0：上市时尚未盈利 1：上市时已盈利industryPe - float 行业市盈率afterPE - float 发行后市盈率o  

#获取可用周期列表  

# get_period_list()  

释义o 返回可用周期列表  
参数o 无  
返回o list 周期列表  

#ETF 申赎清单信息下载  

# download_etf_info()  

释义o 下载所有ETF 申赎清单信息  
参数o 无  
返回o 无  

# #ETF 申赎清单信息获取  

get_etf_info()  

释义o 获取所有ETF 申赎清单信息  
参数o 无  
返回o dict 所有申赎数据  

#节假日下载 download_holiday_data()  

释义o 下载节假日数据  
参数o 无  
返回o 无  

# #获取最新交易日 $\mathbf{k}$ 线数据  

get_full_kline(field_list = [], stock_list = [], period = '1m' , start_time = '', end_time = '', count = 1 dividend_type = 'none', fill_data = True)  

释义o 获取最新交易日k 线全推数据,仅支持最新一个交易日，不包含历史值  
参数o 参考get_market_data 函数  
返回o dict - {field: DataFrame}  

# #财务数据接口  

# #获取财务数据  

get_financial_data(stock_list, table_list=[], start_time='', end_time='', report_type='report_time')  

释义o 获取财务数据  
参数o stock_list - list 合约代码列表o table_list - list 财务数据表名称列表'Balance' #资产负债表'Income' #利润表'CashFlow' #现金流量表'Capital' #股本表'Holdernum' #股东数'Top10holder' #十大股东'Top10flowholder' #十大流通股东'Pershareindex' #每股指标o start_time - string 起始时间o end_time - string 结束时间o report_type - string 报表筛选方式'report_time' #截止日期'announce_time' #披露日期  

返回  

o dict 数据集 { stock1 : datas1, stock2 : data2, ... }o stock1, stock2, ... ：合约代码o datas1, datas2, ... ：dict 数据集 { table1 : table_data1, table2 :table_data2, ... }table1, table2, ... ：财务数据表名table_data1, table_data2, ... ：pd.DataFrame 数据集，数据字段详见附录 - 财务数据字段列表备注  

# #下载财务数据  

download_financial_data(stock_list, table_list=[])  

释义o 下载财务数据  
参数o stock_list - list 合约代码列表o table_list - list 财务数据表名列表  
返回o 无  
备注o 同步执行，补充数据完成后返回  

download_financial_data2(stock_list, table_list=[], start_time='', end_time='', callback=None)  

释义o 下载财务数据  
参数o stock_list - list 合约代码列表table_list - list 财务数据表名列表o start_time - string 起始时间o end_time - string 结束时间以m_anntime 披露日期字段，按[start_time, end_time]范围筛选callback - func 回调函数参数为进度信息dicttotal - 总下载个数finished - 已完成个数stockcode - 本地下载完成的合约代码  
返回o 无  
备注o 同步执行，补充数据完成后返回  

# #基础行情信息  

# #获取合约基础信息  

# get_instrument_detail(stock_code, iscomplete)  

释义o 获取合约基础信息  
参数o stock_code - string 合约代码o iscomplete - bool 是否获取全部字段，默认为False  
返回o dict 数据字典，{ field1 : value1, field2 : value2, ... }，找不到指定合约时返回Noneiscomplete 为False 时，返回以下字段ExchangeID - string 合约市场代码InstrumentID - string 合约代码o InstrumentName - string 合约名称o ProductID - string 合约的品种ID(期货)o ProductName - string 合约的品种名称(期货)ExchangeCode - string 交易所代码UniCode - string 统一规则代码o CreateDate - str 上市日期(期货)o OpenDate - str IPO 日期(股票)o ExpireDate - int 退市日或者到期日PreClose - float 前收盘价格o SettlementPrice - float 前结算价格UpStopPrice - float 当日涨停价DownStopPrice - float 当日跌停价o FloatVolume - float 流通股本TotalVolume - float 总股本LongMarginRatio - float 多头保证金率ShortMarginRatio - float 空头保证金率PriceTick - float 最小价格变动单位VolumeMultiple - int 合约乘数(对期货以外的品种，默认是1)MainContract - int 主力合约标记，1、2、3 分别表示第一主力合约，第二主力合约，第三主力合约LastVolume - int 昨日持仓量  
o InstrumentStatus - int 合约停牌状态  
o IsTrading - bool 合约是否可交易IsRecent - bool 是否是近月合约OpenInterestMultiple - int 交割月持仓倍数  

iscomplete 为True 时，增加会返回更多合约信息字段，例如  

ChargeType - int 期货和期权手续费方式 0 表示未知，1 表示按元/手，2 表示  
按费率，单位为万分比， $\textcircled{1}$   
ChargeOpen - float 开仓手续费(率) 返回-1 时该值无效，其余情况参考  
ChargeType  
ChargeClose - float 平仓手续费(率) 返回-1 时该值无效，其余情况参考  
ChargeType  
ChargeTodayOpen - float 开今仓(日内开仓)手续费(率) 返回-1 时该值无效，其  
余情况参考ChargeType  
ChargeTodayClose - float 平今仓(日内平仓)手续费(率)  返回-1 时该值无效，  
其余情况参考ChargeType  
OptionType - int 期权类型 返回-1 表示合约为非期权 返回0 为期权认购  返  
回1 为期权认沽  

详细合约信息字段见附录-合约信息字段列表  

备注  

可用于检查合约代码是否正确合约基础信息CreateDate OpenDate 字段类型由int 调整为str  

# #获取合约类型  

# get_instrument_type(stock_code)  

释义o 获取合约类型  
参数o stock_code - string 合约代码  
返回o dict 数据字典，{ type1 : value1, type2 : value2, ... }，找不到指定合约时返回Nonetype1, type2, ... ：string 合约类型value1, value2, ... ：bool 是否为该类合约'index' #指数  

备注o  无  

# #获取交易日列表  

get_trading_dates(market, start_time='', end_time='', count=-1)  

释义o 获取交易日列表  
参数o market - string 市场代码o start_time - string 起始时间o end_time - string 结束时间o count - int 数据个数  
返回o list 时间戳列表，[ date1, date2, ... ]  
备注o 无  

# #获取板块列表  

get_sector_list()  

释义o 获取板块列表  
参数o 无  
返回o list 板块列表，[ sector1, sector2, ... ]  
备注o 需要下载板块分类信息  

# #获取板块成分股列表  

get_stock_list_in_sector(sector_name)  

释义o 获取板块成分股列表  
参数o sector_name - string 版块名称  
返回  

o list 成分股列表，[ stock1, stock2, ... ]备注o 需要板块分类信息  

# #下载板块分类信息  

download_sector_data()  

释义o 下载板块分类信息  
参数o 无  
返回o 无  
备注o 同步执行，下载完成后返回  

# #创建板块目录节点  

# create_sector_folder(parent_node, folder_name, overwrite)  

释义o 创建板块目录节点  
参数o parent_node - string 父节点，’ ‘为 '我的‘ （默认目录）o folder_name - string 要创建的板块目录名称o overwrite- bool 是否覆盖，如果目标节点已存在，为True 时跳过，为False 时在folder_name 后增加数字编号，编号为从1 开始自增的第一个不重复的值。 默认为True  
返回o folder_name2 - string 实际创建的板块目录名  
备注o 无  

# #创建板块  

create_sector(parent_node, sector_name, overwrite)  

释义o 创建板块  
参数o parent_node - string 父节点，’ ‘为 '我的‘ （默认目录）o sector_name - string 板块名称o overwrite- bool 是否覆盖，如果目标节点已存在，为True 时跳过，为False 时在sector_name 后增加数字编号，编号为从1 开始自增的第一个不重复的值。 默认为True  
返回o sector_name2 - string 实际创建的板块名  
备注o 无  

# #添加自定义板块  

add_sector(sector_name, stock_list)  

释义o 添加自定义板块  
参数o sector_name - string 板块名称o stock_list - list 成分股列表  
返回o 无  
备注o 无  

# #移除板块成分股  

remove_stock_from_sector(sector_name, stock_list)  

释义o 创建板块  
参数o sector_name - string 板块名称o stock_list- list 成分股列表  
返回o result - bool 操作成功为True，失败为False  
备注o 无  

# #移除自定义板块  

remove_sector(sector_name)  

释义o 移除自定义板块  
参数o sector_name - string 板块名称  
返回  

o 无 备注 o 无  

# #重置板块  

reset_sector(sector_name, stock_list)  

释义o 重置板块  
参数o sector_name - string 板块名称o stock_list- list 成分股列表  
返回o result - bool 操作成功为True，失败为False  
备注o 无  

# #获取指数成分权重信息  

# get_index_weight(index_code)  

释义o 获取指数成分权重信息  
参数o index_code - string 指数代码  
返回o dict 数据字典，{ stock1 : weight1, stock2 : weight2, ... }  
备注o 需要下载指数成分权重信息  

# #下载指数成分权重信息  

download_index_weight()  

释义o 下载指数成分权重信息  
参数o 无  
返回o 无  
备注o 同步执行，下载完成后返回  

# #附录  

# #行情数据字段列表  

# #tick - 分笔数据  

<html><body><table><tr><td>'time' #时间戳</td></tr><tr><td>'lastPrice' #最新价</td></tr><tr><td>'open' #开盘价</td></tr><tr><td>'high' #最高价 'low' #最低价</td></tr><tr><td>'lastClose' #前收盘价</td></tr><tr><td>'amount' #成交总额</td></tr><tr><td>'volume' #成交总量</td></tr><tr><td>'pvolume' #原始成交总量</td></tr><tr><td>'stockStatus' #证券状态 openInt' #持仓量</td></tr><tr><td>lastSettlementPrice' #前结算</td></tr><tr><td>'askPrice' #委卖价</td></tr><tr><td>'bidPrice' #委买价 #委卖量</td></tr><tr><td>'askVol' 'bidVol' #委买量</td></tr><tr><td>transactionNum' #成交笔数</td></tr><tr><td></td></tr></table></body></html>  

# #1m / 5m / 1d - K 线数据  

![](images/ac6dd3f0115d594b7a0787282b333ae0e72127332f8502521fe97e91a7bdf063.jpg)  

#除权数据  


<html><body><table><tr><td>interest #每股股利（税前，元)</td><td></td></tr><tr><td>stockBonus</td><td>#每股红股（股）</td></tr><tr><td>stockGift</td><td>#每股转增股本 （股）</td></tr><tr><td>allotNum</td><td>#每股配股数（股）</td></tr><tr><td>allotPrice</td><td>#配股价格 各（元）</td></tr></table></body></html>  

'gugai' #是否股改, 对于股改，在算复权系数时，系统有特殊算法'dr' #除权系数  

#l2quote - level2 实时行情快照  

![](images/07a11677b68eeaa1d4ca74667b947ac493f1627d9d52919020a61a556aceab01.jpg)  

#l2order - level2 逐笔委托   


<html><body><table><tr><td>time #时间戳</td></tr><tr><td>price' #委托价</td></tr><tr><td>volume #委托量</td></tr><tr><td>entrustNo' #委托号</td></tr><tr><td>entrustType' #委托类型</td></tr><tr><td>entrustDirection #委托方向</td></tr></table></body></html>  

# #l2transaction - level2 逐笔成交  

<html><body><table><tr><td>'time' #时间戳</td></tr><tr><td>price' #成交价</td></tr><tr><td>volume' #成交量</td></tr><tr><td>amount' #成交额</td></tr><tr><td>'tradeIndex' #成交记录号</td></tr><tr><td>'buyNo' #买方委托号</td></tr><tr><td>sellNo' #卖方委托号</td></tr><tr><td>'tradeType' #成交类型</td></tr><tr><td>'tradeFlag' #成交标志</td></tr></table></body></html>  

# #l2quoteaux - level2 实时行情补充 （总买总卖）  

![](images/2ad4bd1e5cccd5c5ff6660991c31cb8cfe1690d4493e0b436f8e5cb47df9c7b5.jpg)  

#l2orderqueue - level2 委买委卖一档委托队列  

![](images/4e6050dffd23fc0bc0a3c084caade86d0547eaadb1ecd53a1775dfd9da30c404.jpg)  

# #数据字典  

#证券状态  

0,10 - 默认为未知  
11 - 开盘前S  
12 - 集合竞价时段C  
13 - 连续交易T  
14 - 休市B  
15 - 闭市E  
16 - 波动性中断V  
17 - 临时停牌P  
18 - 收盘集合竞价U  
19 - 盘中集合竞价M  
20 - 暂停交易至闭市N  
21 - 获取字段异常  
22 - 盘后固定价格行情  
23 - 盘后固定价格行情完毕  

# #委托类型  

level2 逐笔委托 - entrustType 委托类型level2 逐笔成交 - tradeType 成交类型  

# #委托方向  

level2 逐笔委托 - entrustDirection 委托方向o 注：上交所的撤单信息在逐笔委托的委托方向，区分撤买撤卖  

2 - 卖出  
3 - 撤买（上交所）  
4 - 撤卖（上交所）  

# #成交标志  

level2 逐笔成交 - tradeFlag 成交标志o 注：深交所的在逐笔成交的成交标志，只有撤单，没有方向  

0 - 未知  
1 - 外盘  
2 - 内盘  
3 - 撤单（深交所）  

# #现金替代标志  

ETF 申赎清单成份股现金替代标志  

<html><body><table><tr><td>0－禁止现金替代（必须有股票）</td></tr><tr><td>1－允许现金替代（先用股票，股票不足的话用现金替代</td></tr><tr><td>2－必须现金替代 3－非沪市（股票）退补现金替代</td></tr><tr><td>4－非沪市（股票）必须现金替代</td></tr><tr><td>5-非沪深退补现金替代</td></tr><tr><td>6-非沪深必须现金替代</td></tr><tr><td>7－港市退补现金替代（仅适用于跨沪深ETF产品）</td></tr><tr><td>8-港市必须现金替代（仅适用于跨沪深港ETF产品）</td></tr></table></body></html>  

# #Balance - 资产负债表  

<html><body><table><tr><td>'m_anntime' #披露日期 'm_timetag' #截止日期 internal_shoule_recv' #内部应收款</td></tr><tr><td>fixed_capital_clearance' #固定资产清理 'should_pay_money' #应付分保账款 'settlement_payment' #结算备付金</td></tr><tr><td>receivable_premium' #应收保费 accounts_receivable_reinsurance' #应收分保账款 'reinsurance_contract_reserve' #应收分保合同准备金</td></tr><tr><td>'dividends_payable' #应收股利 'tax_rebate_for_export' #应收出口退税 'subsidies_receivable' #应收补贴款</td></tr><tr><td>'deposit_receivable' #应收保证金 apportioned_cost' #待摊费用 profit_and_current_assets_with_deal' #待处理流动资产损益</td></tr><tr><td>current_assets_one_year' #一年内到期的非流动资产 'long_term_receivables' #长期应收款 other_long_term_investments' #其他长期投资</td></tr><tr><td>original_value_of_fixed_assets' #固定资产原值 net_value_of_fixed_assets' #固定资产净值 'depreciation_reserves_of_fixed_assets' #固定资产减值准备</td></tr><tr><td>productive_biological_assets' #生产性生物资产 public_welfare_biological_assets' #公益性生物资产 'oil_and_gas_assets' #油气资产</td></tr><tr><td>development_expenditure' #开发支出 right_of_split_share_distribution' #股权分置流通权</td></tr><tr><td>'other_non_mobile_assets' #其他非流动资产 handling_fee_and_commission' #应付手续费及佣金</td></tr><tr><td>'other_payables' #其他应交款 'margin_payable' #应付保证金 'internal_accounts_payable' #内部应付款</td></tr><tr><td>advance_cost' #预提费用 'insurance_contract_reserve' #保险合同准备金</td></tr><tr><td>'broker_buying_and_selling_securities' #代理买卖证券款 acting_underwriting_securities' #代理承销证券款</td></tr><tr><td>international_ticket_settlement' #国际票证结算 'domestic_ticket_settlement' #国内票证结算 'deferred_income' #递延收益</td></tr><tr><td>'short_term_bonds_payable' #应付短期债券 long_term_deferred_income' #长期递延收益 undetermined_investment_losses' #未确定的投资损失 cash dividends' #拟分配现金股利</td></tr></table></body></html>  

<html><body><table><tr><td>provisions_not' #预计负债</td></tr><tr><td>cust_bank_dep' #吸收存款及同业存放 provisions' #预计流动负债</td></tr><tr><td>'less_tsy_stk' #减：库存股 cash_equivalents' #货币资金 "loans_to_oth_banks' #拆出资金</td></tr><tr><td>'tradable_fin_assets' #交易性金融资产 'derivative_fin_assets' #衍生金融资产 bill_receivable' #应收票据 'account_receivable' #应收账款</td></tr><tr><td>'advance_payment' #预付款项 'int_rcv' #应收利息</td></tr><tr><td>'other_receivable' #其他应收款 'red_monetary_cap_for_sale' #买入返售金融资产 agency_bus_assets' #以公允价值计量且其变动计入当期损益的金融</td></tr><tr><td>资产 inventories' #存货</td></tr><tr><td>'other_current_assets' #其他流动资产 'total_current_assets' #流动资产合计 'loans_and_adv_granted' #发放贷款及垫款</td></tr><tr><td>fin_assets_avail_for_sale' #可供出售金融资产 "held_to_mty_invest' #持有至到期投资</td></tr><tr><td>long_term_eqy_invest' #长期股权投资 'invest_real_estate' #投资性房地产</td></tr><tr><td>accumulated_depreciation' #累计折旧 'fix_assets' #固定资产 'constru_in_process' #在建工程</td></tr><tr><td>construction_materials' #工程物资 long_term_liabilities' #长期负债 'intang_assets' #无形资产</td></tr><tr><td>'goodwill' #商誉 'long_deferred_expense' #长期待摊费用 deferred_tax_assets' #递延所得税资产</td></tr><tr><td>total_non_current_assets' #非流动资产合计 'tot_assets' #资产总计 #短期借款</td></tr><tr><td>'shortterm_loan' 'borrow_central_bank' #向中央银行借款 'loans_oth_banks' #拆入资金 'tradable_fin_liab' #交易性金融负债 'derivative_fin_liab' #衍生金融负债 'notes_payable' #应付票据 'accounts_payable' #应付账款 'advance_peceipts' #预收账款 #卖出回购全融资产款</td></tr></table></body></html>  

'empl_ben_payable'   
'taxes_surcharges_payable'   
'int_payable'   
'dividend_payable'   
'other_payable'   
'non_current_liability_in_one_year   
'other_current_liability'   
'total_current_liability   
'long_term_loans'   
'bonds_payable'   
'longterm_account_payable'   
'grants_received'   
'deferred_tax_liab'   
'other_non_current_liabilities'   
'non_current_liabilities'   
'tot_liab'   
'cap_stk'   
'cap_rsrv'   
'specific_reserves'   
'surplus_rsrv'   
'prov_nom_risks'   
'undistributed_profit'   
'cnvd_diff_foreign_curr_stat'   
'tot_shrhldr_eqy_excl_min_int'   
'minority_int'   
'total_equity'   
'tot_liab_shrhldr_eqy'  

# #Income - 利润表  

![](images/6a7fa95c1757711477c28fb0e289d62b588ba578a5081e4431af7a9c56df1e16.jpg)  

<html><body><table><tr><td>'m_anntime' #披露日期</td></tr><tr><td>'m_timetag' #截止日期</td></tr><tr><td>'revenue_inc' #营业收入</td></tr><tr><td>earned_premium' #已赚保费 'real_estate_sales_income' #房地产销售收入</td></tr><tr><td>'total_operating_cost' #营业总成本</td></tr><tr><td>real_estate_sales_cost' #房地产销售成本</td></tr><tr><td>'research_expenses' #研发费用 'surrender_value' #退保金</td></tr><tr><td>'net_payments' #赔付支出净额 'net_withdrawal_ins_con_res' #提取保险合同准备金净额</td></tr><tr><td>policy_dividend_expenses' #保单红利支出</td></tr><tr><td>'reinsurance_cost' #分保费用 change_income_fair_value' #公允价值变动收益</td></tr><tr><td>futures_loss' #期货损益</td></tr></table></body></html>  

'trust_income'   
'subsidize_revenue'   
'other_business_profits'   
'net_profit_excl_merged_int_inc'   
'int_inc'   
'handling_chrg_comm_inc'   
'less_handling_chrg_comm_exp'   
'other_bus_cost'   
'plus_net_gain_fx_trans'   
'il_net_loss_disp_noncur_asset'   
'inc_tax'   
'unconfirmed_invest_loss'   
'net_profit_excl_min_int_inc'   
'less_int_exp'   
'other_bus_inc'   
'revenue'   
'total_expense'   
'less_taxes_surcharges_ops'   
'sale_expense'   
'less_gerl_admin_exp'   
'financial_expense'   
'less_impair_loss_assets'   
'plus_net_invest_inc'   
'incl_inc_invest_assoc_jv_entp'   
'oper_profit'   
'plus_non_oper_rev'   
'less_non_oper_exp'   
'tot_profit'   
'net_profit_incl_min_int_inc'   
'net_profit_incl_min_int_inc_after'   
'minority_int_inc'   
's_fa_eps_basic'   
's_fa_eps_diluted'   
'total_income'   
'total_income_minority'   
'other_compreh_inc'  

# #CashFlow - 现金流量表  

![](images/ddec4205ce3394e2a9fcdcfd6ecfad5ea8dfd0cca15de48edb5d3223c63e9ae0.jpg)  

'm_anntime'   
'm_timetag'   
'cash_received_ori_ins_contract_pre'   
'net_cash_received_rei_ope'   
'net_increase_insured_funds'  

#披露日期#截止日期#收到原保险合同保费取得的现金#收到再保险业务现金净额#保户储金及投资款净增加额  

#  

'Net'   
increase_in_disposal   
'cash_for_interest'   
'net_increase_in_repurchase_funds'   
'cash_for_payment_original_insurance'   
'cash_payment_policy_dividends'   
'disposal_other_business_units'   
'cash_received_from_pledges'   
'cash_paid_for_investments'   
'net_increase_in_pledged_loans'   
'cash_paid_by_subsidiaries'   
'increase_in_cash_paid'   
'cass_received_sub_abs'   
'cass_received_sub_investments'   
'minority_shareholder_profit_loss'   
'unrecognized_investment_losses'   
'ncrease_deferred_income'   
'projected_liability'   
'increase_operational_payables'   
'reduction_outstanding_amounts_less'   
'reduction_outstanding_amounts_more'   
'goods_sale_and_service_render_cash'   
'net_incr_dep_cob'   
'net_incr_loans_central_bank'   
'net_incr_fund_borr_ofi'   
'net_incr_fund_borr_ofi'   
'tax_levy_refund'   
'cash_paid_invest'   
'other_cash_recp_ral_oper_act'   
'stot_cash_inflows_oper_act'   
'goods_and_services_cash_paid'   
'net_incr_clients_loan_adv'   
'net_incr_dep_cbob'   
'handling_chrg_paid'   
'cash_pay_beh_empl'   
'pay_all_typ_tax'   
'other_cash_pay_ral_oper_act'   
'stot_cash_outflows_oper_act'   
'net_cash_flows_oper_act'   
'cash_recp_disp_withdrwl_invest'   
'cash_recp_return_invest'   
'net_cash_recp_disp_fiolta'   
现金 ther  

#处置交易性金融资产净增加额#收取利息、手续费及佣金的现金#回购业务资金净增加额#支付原保险合同赔付款项的现金#支付保单红利的现金#处置子公司及其他收到的现金#减少质押和定期存款所收到的现金#投资所支付的现金#质押贷款净增加额#取得子公司及其他营业单位支付的现金净额#增加质押和定期存款所支付的现金#其中子公司吸收现金#其中:子公司支付给少数股东的股利、利润#少数股东损益#未确认的投资损失#递延收益增加(减:减少)#预计负债#经营性应付项目的增加#已完工尚未结算款的减少(减:增加)#已结算尚未完工款的增加(减:减少)#销售商品、提供劳务收到的现金#客户存款和同业存放款项净增加额#向中央银行借款净增加额(万元#向其他金融机构拆入资金净增加额#拆入资金净增加额#收到的税费与返还#投资支付的现金#收到的其他与经营活动有关的现金#经营活动现金流入小计#购买商品、接受劳务支付的现金#客户贷款及垫款净增加额#存放中央银行和同业款项净增加额#支付利息、手续费及佣金的现金#支付给职工以及为职工支付的现金#支付的各项税费#支付其他与经营活动有关的现金#经营活动现金流出小计#经营活动产生的现金流量净额#收回投资所收到的现金#取得投资收益所收到的现金#处置固定资产、无形资产和其他长期投资收到的#收到的其他与投资活动有关的现金  

'stot_cash_inflows_inv_act'  
'cash_pay_acq_const_fiolta'  
现金  
'other_cash_pay_ral_oper_act'  
'stot_cash_outflows_inv_act'  
'net_cash_flows_inv_act'  
'cash_recp_cap_contrib'  
'cash_recp_borrow'  
'proc_issue_bonds'  
'other_cash_recp_ral_fnc_act'  
'stot_cash_inflows_fnc_act'  
'cash_prepay_amt_borr'  
'cash_pay_dist_dpcp_int_exp'  
'other_cash_pay_ral_fnc_act'  
'stot_cash_outflows_fnc_act'  
'net_cash_flows_fnc_act'  
'eff_fx_flu_cash'  
'net_incr_cash_cash_equ'  
'cash_cash_equ_beg_period'  
'cash_cash_equ_end_period'  
'net_profit'  
'plus_prov_depr_assets'  
'depr_fa_coga_dpba'  
折旧  
'amort_intang_assets'  
'amort_lt_deferred_exp'  
'decr_deferred_exp'  
'incr_acc_exp'  
'loss_disp_fiolta'  
'loss_scr_fa'  
'loss_fv_chg'  
'fin_exp'  
'invest_loss'  
'decr_deferred_inc_tax_assets'  
'incr_deferred_inc_tax_liab'  
'decr_inventories'  
'decr_oper_payable'  
'others'  
'im_net_cash_flows_oper_act'  
'conv_debt_into_cap'  
'conv_corp_bonds_due_within_1  
'fa_fnc_leases'  
'end_bal_cash'  
'less_beg_bal_cash'  
#投资活动现金流入小计  
#购建固定资产、无形资产和其他长期投资支付的  
#支付其他与投资的现金  
#投资活动现金流出小计#投资活动产生的现金流量净额#吸收投资收到的现金#取得借款收到的现金#发行债券收到的现金  
#收到其他与筹资活动有关的现金  
#筹资活动现金流入小计#偿还债务支付现金#分配股利、利润或偿付利息支付的现金  
#支付其他与筹资的现金  
#筹资活动现金流出小计  
#筹资活动产生的现金流量净额  
#汇率变动对现金的影响#现金及现金等价物净增加额#期初现金及现金等价物余额#期末现金及现金等价物余额#净利润#资产减值准备#固定资产折旧、油气资产折耗、生产性物资#无形资产摊销#长期待摊费用摊销#待摊费用的减少#预提费用的增加  
#处置固定资产、无形资产和其他长期资产的损失#固定资产报废损失#公允价值变动损失#财务费用#投资损失  
#递延所得税资产减少  
#递延所得税负债增加#存货的减少#经营性应收项目的减少#其他#经营活动产生现金流量净额#债务转为资本#一年内到期的可转换公司债券#融资租入固定资产#现金的期末余额#现金的期初余额  

'plus_end_bal_cash_equ' #现金等价物的期末余额 'less_beg_bal_cash_equ' #现金等价物的期初余额 'im_net_incr_cash_cash_equ' #现金及现金等价物的净增加额 'tax_levy_refund' #收到的税费返还  

# #PershareIndex - 主要指标  

![](images/53e31628f5a1ddb5f76da0301f0957bbc0315f1191c4eb879afe24b9428b2413.jpg)  

# #Capital - 股本表  

![](images/f012abd05817e7de02fa7fd5c446ad7e8e39ee86cdc19fe0d75902f23ef7c5ef.jpg)  

# #Top10holder/Top10flowholder - 十大股东/十大流通股东  

'declareDate'  

<html><body><table><tr><td>endDate' #截止日期</td></tr><tr><td>name #股东名称</td></tr><tr><td>'type' #股东类型</td></tr><tr><td>quantity' #持股数量</td></tr><tr><td>reason #变动原因</td></tr><tr><td></td></tr><tr><td>'ratio' #持股比例</td></tr><tr><td>nature #股份性质 'rank' #持股排名</td></tr></table></body></html>  

# #Holdernum - 股东数  

'declareDate' #公告日期'endDate' #截止日期'shareholder' #股东总数'shareholderA' #A 股东户数'shareholderB' #B 股东户数'shareholderH' #H 股东户数'shareholderFloat' #已流通股东户数'shareholderOther' #未流通股东户数  

# #合约信息字段列表  

![](images/f6519f7e5b63eb88d5bd1fa43f92b765e612f0aaf0b62b2b4766f4cae7465db6.jpg)  

'PriceTick' #最小变价单位  
'VolumeMultiple' #合约乘数（对期货以外的品种，默认是1）  
'MainContract' #主力合约标记，1、2、3 分别表示第一主  
力合约，第二主力合约，第三主力合约  
'MaxMarketOrderVolume' #市价单最大下单量  
'MinMarketOrderVolume' #市价单最小下单量  
'MaxLimitOrderVolume' #限价单最大下单量  
'MinLimitOrderVolume' #限价单最小下单量  
'MaxMarginSideAlgorithm' #上期所大单边的处理算法  
'DayCountFromIPO' #自IPO 起经历的交易日总数  
'LastVolume' #昨日持仓量  
'InstrumentStatus' #合约停牌状态  
'IsTrading' #合约是否可交易  
'IsRecent' #是否是近月合约  
'IsContinuous' #是否是连续合约  
'bNotProfitable' #是否非盈利状态  
'bDualClass' #是否同股不同权  
'ContinueType' #连续合约类型  
'secuCategory' #证券分类  
'secuAttri' #证券属性  
'MaxMarketSellOrderVolume' #市价卖单最大单笔下单量  
'MinMarketSellOrderVolume' #市价卖单最小单笔下单量  
'MaxLimitSellOrderVolume' #限价卖单最大单笔下单量  
'MinLimitSellOrderVolume' #限价卖单最小单笔下单量  
'MaxFixedBuyOrderVol' #盘后定价委托数量的上限（买）  
'MinFixedBuyOrderVol' #盘后定价委托数量的下限（买）  
'MaxFixedSellOrderVol' #盘后定价委托数量的上限（卖）  
'MinFixedSellOrderVol' #盘后定价委托数量的下限（卖）  
'HSGTFlag' #标识港股是否为沪港通或深港  
通标的证券。沪港通:0-非标的，1-标的，2-历史标的；深港通:0-非标的，3-标的，4-历史标  
的，5-是沪港通也是深港通  
'BondParValue' #债券面值  
'QualifiedType' #投资者适当性管理分类  
'PriceTickType' #价差类别（港股用），1-股票，3-债券，4-期权，5-  
交易所买卖基金  
'tradingStatus' #交易状态  
'OptUnit' #期权合约单位  
'MarginUnit' #期权单位保证金  
'OptUndlCode' #期权标的证券代码或可转债正股标的证券  
代码  
'OptUndlMarket' #期权标的证券市场或可转债正股标的证券市场  
'OptLotSize' #期权整手数  
'OptExercisePrice' #期权行权价或可转债转股价  

![](images/4f53d3a742e077b99712f39cf97de2435093f391ec29fe726ffb0939c8250b36.jpg)  

# #代码示例  

# #时间戳转换  

![](images/36fcae0236d6a4306dd8b196757491dc6e6bd8343bd67e34c77b68b1ee7686bc.jpg)  

# XtQuant.Xttrade 交易模块  

#版本信息  

2020-09-01 o 初稿  

2020-10-14持仓结构添加字段投资备注相关修正  

2020-10-21  

添加信用交易相关委托类型（order_type）枚举o 调整XtQuant 运行依赖环境说明，更新多版本支持相关说明  

2020-11-13  

o 添加信用交易相关类型定义说明  
o 添加信用交易相关接口说明  
o 添加异步撤单委托反馈结构说明  
o 添加下单失败和撤单失败主推结构说明  
o 添加订阅和反订阅接口  
o 添加创建API 实例，注册回调类，准备API 环境，创建连接，停止运行，阻塞进程接口说明  
o 调整API 接口说明将接口细分为"系统设置接口"，“操作接口”，“查询接口”，"信用相关查询接口"，“回调类”等五类接口返回“None”修改为“无”去掉回调类接口中的示例添加“备注”项  
o 所有“证券账号”改为“资金账号”  
$\bigcirc$ 英文“,”调整为中文“，”  
o 示例代码中增加XtQuant API 实例对象，修正没有实例，直接调用的错误  

添加股票异步撤单接口说明，将原股票撤单修改为股票同步撤单  

2020-11-19  

添加账号状态主推接口添加账号状态数据结构说明o 添加账号状态枚举值回调类接口说明调整将回调函数定义及函数说明标题调整一致补充异步下单回报推送、异步撤单回报推送接口说明  

2021-07-20  

o 修改回调/主推函数实现机制，提升报撤单回报的速度，降低穿透延时波动o XtQuantTrader.run_forever()修改实现，支持 $\mathsf{C t r l+C}$ 跳出  

2022-06-27  

委托查询支持仅查询可撤委托  
添加新股申购相关接口query_new_purchase_limit 查询新股申购额度query_ipo_data 查询新股信息  
添加账号信息查询接口query_account_infos  
2022-11-15o 修复XtQuantTrader.unsubscribe 的实现  
2022-11-17o 交易数据字典格式调整  
2022-11-28o 为主动请求接口的返回增加专用线程以及相关控制，以支持在on_stock_order 等推送接口中调用同步请求XtQuantTrader.set_relaxed_response_order_enabled  
2023-07-17o 持仓结构XtPosition 成本价字段调整open_price - 开仓价■ avg_price - 成本价  
2023-07-26o 添加资金划拨接口 fund_transfer  
2023-08-11o 添加划拨业务查询普通柜台资金接口 query_com_fundo 添加划拨业务查询普通柜台持仓接口 query_com_position  

2023-10-16  

添加期货市价的报价类型■ xtconstant.MARKET_BEST - 市价最优价[郑商所]■ xtconstant.MARKET_CANCEL - 市价即成剩撤[大商所]xtconstant.MARKET_CANCEL_ALL - 市价全额成交或撤[大商所]■ xtconstant.MARKET_CANCEL_1 - 市价最优一档即成剩撤[中金所]xtconstant.MARKET_CANCEL_5 - 市价最优五档即成剩撤[中金所]■ xtconstant.MARKET_CONVERT_1 - 市价最优一档即成剩转[中金所]xtconstant.MARKET_CONVERT_5 - 市价最优五档即成剩转[中金所]  

2023-10-20  

委托结构XtOrder，成交结构XtTrade，持仓结构XtPosition 新增多空字段o  direction - 多空，股票不需要委托结构XtOrder，成交结构XtTrade 新增交易操作字段o offset_flag - 交易操作，用此字段区分股票买卖，期货开、平仓，期权买卖等2023-11-03o 添加券源行情查询接口 smt_query_quotero 添加库存券约券申请接口 smt_negotiate_ordero 添加约券合约查询接口 smt_query_compact2024-01-02o 委托类型增加ETF 申赎2024-02-29o 添加期货持仓统计查询接口query_position_statistics2024-04-25o 数据结构添加stock_code1 字段以适配长代码2024-05-24o 添加通用数据导出接口export_datao 添加通用数据查询接口query_data2024-06-27o  添加外部成交导入接口sync_transaction_from_external  

# #快速入门  

#创建策略  

#coding=utf-8   
from xtquant.xttrader import XtQuantTrader, XtQuantTraderCallback   
from xtquant.xttype import StockAccount   
from xtquant import xtconstant   
class MyXtQuantTraderCallback(XtQuantTraderCallback): def on_disconnected(self): """ 连接断开 :return: """ print("connection lost") def on_stock_order(self, order): """ 委托回报推送 :param order: XtOrder 对象 :return: print("on order callback:") print(order.stock_code, order.order_status, order.order_sysid) def on_stock_trade(self, trade): 成交变动推送 :param trade: XtTrade 对象 :return: """ print("on trade callback") print(trade.account_id, trade.stock_code, trade.order_id) def on_order_error(self, order_error): """ 委托失败推送 :param order_error:XtOrderError 对象 :return: """ print("on order_error callback") print(order_error.order_id, order_error.error_id, order_error.error_msg) def on_cancel_error(self, cancel_error): """ 撤单失败推送 :param cancel_error: XtCancelError 对象 :return: """ print("on cancel_error callback") print(cancel_error.order_id, cancel_error.error_id, cancel_error.error_msg) def on_order_stock_async_response(self, response): """ 异步下单回报推送 :param response: XtOrderResponse 对象 :return: """ print("on_order_stock_async_response") print(response.account_id, response.order_id, response.seq) def on_account_status(self, status): :param response: XtAccountStatus 对象 :return: """ print("on_account_status") print(status.account_id, status.account_type, status.status)   
if __name__ == "__main__": print("demo test") # path 为mini qmt 客户端安装目录下userdata_mini 路径 path = 'D:\\迅投极速交易终端 睿智融科版\\userdata_mini' # session_id 为会话编号，策略使用方对于不同的Python 策略需要使用不同的会话编号 session_id = 123456 xt_trader = XtQuantTrader(path, session_id) # 创建资金账号为1000000365 的证券账号对象 acc = StockAccount('1000000365') # StockAccount 可以用第二个参数指定账号类型，如沪港通传'HUGANGTONG'，深港通传   
'SHENGANGTONG' # acc = StockAccount('1000000365','STOCK') # 创建交易回调类对象，并声明接收回调 callback = MyXtQuantTraderCallback() xt_trader.register_callback(callback) # 启动交易线程 xt_trader.start() # 建立交易连接，返回0 表示连接成功 connect_result = xt_trader.connect() print(connect_result) # 对交易回调进行订阅，订阅后可以收到交易主推，返回0 表示订阅成功 subscribe_result = xt_trader.subscribe(acc) print(subscribe_result) stock_code = '600000.SH' # 使用指定价下单，接口返回订单编号，后续可以用于撤单操作以及查询委托状态 print("order using the fix price:") fix_result_order_id = xt_trader.order_stock(acc, stock_code, xtconstant.STOCK_BUY, 200,   
xtconstant.FIX_PRICE, 10.5, 'strategy_name', 'remark') print(fix_result_order_id) # 使用订单编号撤单 print("cancel order:") cancel_order_result = xt_trader.cancel_order_stock(acc, fix_result_order_id) print(cancel_order_result) # 使用异步下单接口，接口返回下单请求序号seq，seq 可以和   
on_order_stock_async_response 的委托反馈response 对应起来 print("order using async api:") async_seq = xt_trader.order_stock_async(acc, stock_code, xtconstant.STOCK_BUY, 200,   
xtconstant.FIX_PRICE, 10.5, 'strategy_name', 'remark') print(async_seq) # 查询证券资产 print("query asset:") asset = xt_trader.query_stock_asset(acc) if asset: print("asset:") print("cash {0}".format(asset.cash)) # 根据订单编号查询委托 print("query order:") order = xt_trader.query_stock_order(acc, fix_result_order_id) if order: print("order:") print("order {0}".format(order.order_id)) # 查询当日所有的委托 print("query orders:") orders = xt_trader.query_stock_orders(acc) print("orders:", len(orders)) if len(orders) != 0: print("last order:") print("{0} {1} {2}".format(orders[-1].stock_code, orders[-1].order_volume, orders[-   
1].price)) # 查询当日所有的成交 print("query trade:") trades = xt_trader.query_stock_trades(acc) print("trades:", len(trades)) if len(trades) != 0: print("last trade:") print("{0} {1} {2}".format(trades[-1].stock_code, trades[-1].traded_volume, trades[-   
1].traded_price)) # 查询当日所有的持仓 print("query positions:") positions = xt_trader.query_stock_positions(acc)  

# #进阶篇  

# #XtQuant 运行逻辑  

XtQuant 封装了策略交易所需要的Python API 接口，可以和MiniQMT 客户端交互进行报单、撤单、查询资产、查询委托、查询成交、查询持仓以及收到资金、委托、成交和持仓等变动的主推消息。  

# #XtQuant 数据字典  

# #交易市场(market)  

上交所 - xtconstant.SH_MARKET深交所 - xtconstant.SZ_MARKET  

# #账号类型(account_type)  

期货 - xtconstant.FUTURE_ACCOUNT股票 - xtconstant.SECURITY_ACCOUNT信用 - xtconstant.CREDIT_ACCOUNT期货期权 - xtconstant.FUTURE_OPTION_ACCOUNT股票期权 - xtconstant.STOCK_OPTION_ACCOUNT沪港通 - xtconstant.HUGANGTONG_ACCOUNT深港通 - xtconstant.SHENGANGTONG_ACCOUNT  

# #委托类型(order_type)  

股票  

o 买入 - xtconstant.STOCK_BUY卖出 - xtconstant.STOCK_SELL  

信用  

o 担保品买入 - xtconstant.CREDIT_BUY  
o 担保品卖出 - xtconstant.CREDIT_SELL  
o 融资买入 - xtconstant.CREDIT_FIN_BUY  
o 融券卖出 - xtconstant.CREDIT_SLO_SELL  
o 买券还券 - xtconstant.CREDIT_BUY_SECU_REPAY  
o 直接还券 - xtconstant.CREDIT_DIRECT_SECU_REPAY  
o 卖券还款 - xtconstant.CREDIT_SELL_SECU_REPAY  
o 直接还款 - xtconstant.CREDIT_DIRECT_CASH_REPAY  
o 专项融资买入 - xtconstant.CREDIT_FIN_BUY_SPECIAL  
o 专项融券卖出 - xtconstant.CREDIT_SLO_SELL_SPECIAL  
o 专项买券还券 - xtconstant.CREDIT_BUY_SECU_REPAY_SPECIAL  
o 专项直接还券 - xtconstant.CREDIT_DIRECT_SECU_REPAY_SPECIAL  
o 专项卖券还款 - xtconstant.CREDIT_SELL_SECU_REPAY_SPECIAL  
o 专项直接还款 - xtconstant.CREDIT_DIRECT_CASH_REPAY_SPECIAL  

o 开多 - xtconstant.FUTURE_OPEN_LONGo 平昨多 - xtconstant.FUTURE_CLOSE_LONG_HISTORYo 平今多 - xtconstant.FUTURE_CLOSE_LONG_TODAYo 开空 - xtconstant.FUTURE_OPEN_SHORTo 平昨空 - xtconstant.FUTURE_CLOSE_SHORT_HISTORYo 平今空 - xtconstant.FUTURE_CLOSE_SHORT_TODAY  

期货四键风格  

o 平多，优先平今 - xtconstant.FUTURE_CLOSE_LONG_TODAY_FIRSTo 平多，优先平昨 - xtconstant.FUTURE_CLOSE_LONG_HISTORY_FIRSTo 平空，优先平今 - xtconstant.FUTURE_CLOSE_SHORT_TODAY_FIRSTo 平空，优先平昨 - xtconstant.FUTURE_CLOSE_SHORT_HISTORY_FIRST期货两键风格o 卖出，如有多仓，优先平仓，优先平今，如有余量，再开空- xtconstant.FUTURE_CLOSE_LONG_TODAY_HISTORY_THEN_OPEN_SHORT卖出，如有多仓，优先平仓，优先平昨，如有余量，再开空- xtconstant.FUTURE_CLOSE_LONG_HISTORY_TODAY_THEN_OPEN_SHORTo 买入，如有空仓，优先平仓，优先平今，如有余量，再开多- xtconstant.FUTURE_CLOSE_SHORT_TODAY_HISTORY_THEN_OPEN_LONGo 买入，如有空仓，优先平仓，优先平昨，如有余量，再开多- xtconstant.FUTURE_CLOSE_SHORT_HISTORY_TODAY_THEN_OPEN_LONGo 买入，不优先平仓 - xtconstant.FUTURE_OPENo 卖出，不优先平仓 - xtconstant.FUTURE_CLOSE  

期货 - 跨商品套利开仓 - xtconstant.FUTURE_ARBITRAGE_OPENo 平, 优先平昨 - xtconstant.FUTURE_ARBITRAGE_CLOSE_HISTORY_FIRSTC 平, 优先平今 - xtconstant.FUTURE_ARBITRAGE_CLOSE_TODAY_FIRST期货展期o 看多, 优先平昨 - xtconstant.FUTURE_RENEW_LONG_CLOSE_HISTORY_FIRSTo 看多，优先平今 - xtconstant.FUTURE_RENEW_LONG_CLOSE_TODAY_FIRSTo 看空，优先平昨- xtconstant.FUTURE_RENEW_SHORT_CLOSE_HISTORY_FIRST看空，优先平今 - xtconstant.FUTURE_RENEW_SHORT_CLOSE_TODAY_FIRST股票期权o 买入开仓，以下用于个股期权交易业务- xtconstant.STOCK_OPTION_BUY_OPENo 卖出平仓 - xtconstant.STOCK_OPTION_SELL_CLOSEo 卖出开仓 - xtconstant.STOCK_OPTION_SELL_OPENo 买入平仓 - xtconstant.STOCK_OPTION_BUY_CLOSEo 备兑开仓 - xtconstant.STOCK_OPTION_COVERED_OPENo 备兑平仓 - xtconstant.STOCK_OPTION_COVERED_CLOSEo 认购行权 - xtconstant.STOCK_OPTION_CALL_EXERCISEo 认沽行权 - xtconstant.STOCK_OPTION_PUT_EXERCISEo 证券锁定 - xtconstant.STOCK_OPTION_SECU_LOCKo 证券解锁 - xtconstant.STOCK_OPTION_SECU_UNLOCK  

期货期权 o 期货期权行权 - xtconstant.OPTION_FUTURE_OPTION_EXERCISE  

ETF 申赎o 申购 - xtconstant.ETF_PURCHASE赎回 - xtconstant.ETF_REDEMPTION  

# #报价类型(price_type)  

最新价 - xtconstant.LATEST_PRICE• 指定价 - xtconstant.FIX_PRICE郑商所 期货o 市价最优价 - xtconstant.MARKET_BEST大商所 期货o 市价即成剩撤 - xtconstant.MARKET_CANCELo 市价全额成交或撤 - xtconstant.MARKET_CANCEL_ALL中金所 期货o 市价最优一档即成剩撤 - xtconstant.MARKET_CANCEL_1o 市价最优五档即成剩撤 - xtconstant.MARKET_CANCEL_5$\bigcirc$ 市价最优一档即成剩转 - xtconstant.MARKET_CONVERT_1o 市价最优五档即成剩转 - xtconstant.MARKET_CONVERT_5上交所 股票o 最优五档即时成交剩余撤销 - xtconstant.MARKET_SH_CONVERT_5_CANCELo  最优五档即时成交剩转限价 - xtconstant.MARKET_SH_CONVERT_5_LIMITo 对手方最优价格委托 - xtconstant.MARKET_PEER_PRICE_FIRST$\bigcirc$ 本方最优价格委托 - xtconstant.MARKET_MINE_PRICE_FIRST  

深交所 股票 期权o 对手方最优价格委托 - xtconstant.MARKET_PEER_PRICE_FIRST$\bigcirc$ 本方最优价格委托 - xtconstant.MARKET_MINE_PRICE_FIRSTo 即时成交剩余撤销委托 - xtconstant.MARKET_SZ_INSTBUSI_RESTCANCELo 最优五档即时成交剩余撤销 - xtconstant.MARKET_SZ_CONVERT_5_CANCEL$\bigcirc$ 全额成交或撤销委托 - xtconstant.MARKET_SZ_FULL_OR_CANCEL  

# #委托状态(order_status)  

枚举变量名 值 含义xtconstant.ORDER_UNREPORTED 48 未报xtconstant.ORDER_WAIT_REPORTING 49 待报xtconstant.ORDER_REPORTED 50 已报xtconstant.ORDER_REPORTED_CANCEL 51 已报待撤xtconstant.ORDER_PARTSUCC_CANCEL 52 部成待撤部撤（已经有一部分成交，剩下的xtconstant.ORDER_PART_CANCEL 53已经撤单）xtconstant.ORDER_CANCELED 54 已撤部成（已经有一部分成交，剩下的xtconstant.ORDER_PART_SUCC 55待成交）xtconstant.ORDER_SUCCEEDED 56 已成xtconstant.ORDER_JUNK 57 废单xtconstant.ORDER_UNKNOWN 255 未知  

# #账号状态(account_status)  

<html><body><table><tr><td>枚举变量名</td><td>值</td><td></td><td>含义</td></tr><tr><td></td><td></td><td></td><td></td></tr><tr><td>xtconstant.ACCOUNT_STATUSINVALID</td><td>1</td><td>无效</td><td></td></tr></table></body></html>  

<html><body><table><tr><td></td><td></td><td>百入</td></tr><tr><td>xtconstant.ACCOUNT_STATUS_OK</td><td>0</td><td>正常</td></tr><tr><td>xtconstant.ACCOUNT_STATUS_WAITING_LOGIN</td><td>1</td><td>连接中</td></tr><tr><td>xtconstant.ACCOUNT_STATUSING</td><td>2</td><td>登陆中</td></tr><tr><td>xtconstant.ACCOUNT_STATUS_FAIL</td><td>3</td><td>失败</td></tr><tr><td>xtconstant.ACCOUNT_STATUS_INITING</td><td>4</td><td>初始化中</td></tr><tr><td>xtconstant.ACCOUNT_STATUS_CORRECTING</td><td>5</td><td>数据刷新校正中</td></tr><tr><td>xtconstant.ACCOUNT_STATUS_CLOSED</td><td>6</td><td>收盘后</td></tr><tr><td>xtconstant.ACCOUNT_STATUS_ASSIS_FAIL</td><td>7</td><td>穿透副链接断开</td></tr><tr><td>xtconstant.ACCOUNT_STATUS_DISABLEBYSYS</td><td>8</td><td>系统停用（总线使用-密码 错误超限)</td></tr><tr><td>xtconstant.ACCOUNT_STATUS_DISABLEBYUSER</td><td>9</td><td>用户停用 (总线使用)</td></tr></table></body></html>  

# #划拨方向(transfer_direction)  

<html><body><table><tr><td>枚举变量名</td><td>值</td><td>含义</td></tr><tr><td></td><td>510</td><td>资金划拨-普通柜台 到极速柜台</td></tr><tr><td>xtconstant.FUNDS_TRANSFER_SPEED_TO_NORMAL</td><td>511</td><td>资金划拨-极速柜台 到普通柜台</td></tr><tr><td>xtconstant.NODE_FUNDS_TRANSFER_SH_TO_SZ</td><td>512</td><td>节点资金划拨-上海 节点到深圳节点</td></tr><tr><td>xtconstant.NODE_FUNDS_TRANSFER_SZ_TO_SH</td><td>513</td><td>节点资金划拨-深圳 节点到上海节点</td></tr></table></body></html>  

# #多空方向(direction)  

# 枚举变量名 值 含义  

xtconstant.DIRECTION_FLAG_LONG 48 多xtconstant.DIRECTION_FLAG_SHORT 49 空  

# #交易操作(offset_flag)  

枚举变量名 值 含义xtconstant.OFFSET_FLAG_OPEN 48 买入，开仓xtconstant.OFFSET_FLAG_CLOSE 49 卖出，平仓xtconstant.OFFSET_FLAG_FORCECLOSE 50 强平xtconstant.OFFSET_FLAG_CLOSETODAY 51 平今xtconstant.OFFSET_FLAG_ClOSEYESTERDAY 52 平昨xtconstant.OFFSET_FLAG_FORCEOFF 53 强减xtconstant.OFFSET_FLAG_LOCALFORCECLOSE 54 本地强平  

# #XtQuant 数据结构说明  

# #资产XtAsset  

属性 类型 注释account_type int 账号类型，参见数据字典在新窗口打开account_id str 资金账号cash float 可用金额frozen_cash float 冻结金额market_value float 持仓市值total_asset float 总资产  

#委托XtOrder   


<html><body><table><tr><td>属性</td><td>类 型</td><td>注释</td></tr><tr><td>account_type</td><td>int</td><td>账号类型，参见数据字典在新窗口打开</td></tr><tr><td>account_id</td><td>str</td><td>资金账号</td></tr><tr><td>stock_code</td><td>str</td><td>证券代码，例如"600000.SH"</td></tr><tr><td>order_id</td><td>int</td><td>订单编号</td></tr><tr><td>order_sysid</td><td>str</td><td>柜台合同编号</td></tr><tr><td>order_time</td><td>int</td><td>报单时间</td></tr><tr><td>order_type</td><td>int</td><td>委托类型，参见数据字典在新窗口打开</td></tr><tr><td>order_volume</td><td>int</td><td>委托数量</td></tr><tr><td>price_type</td><td>int</td><td>报价类型，该字段在返回时为柜台返回类型，不等价于下 单传入的 price_type，枚举值不一样功能一样，参见数据 字典在新窗口打开</td></tr><tr><td>price</td><td>float</td><td>委托价格</td></tr><tr><td>traded_volume</td><td>int</td><td>成交数量</td></tr><tr><td>traded_price</td><td>float</td><td>成交均价</td></tr><tr><td>order_status</td><td>int</td><td>委托状态，参见数据字典在新窗口打开</td></tr><tr><td>status_msg</td><td>str</td><td>委托状态描述，如废单原因</td></tr><tr><td>strategy_name</td><td>str</td><td>策略名称</td></tr><tr><td>order_remark</td><td>str</td><td>委托备注</td></tr><tr><td>direction</td><td>int</td><td>多空方向，股票不适用；参见数据字典在新窗口打开</td></tr><tr><td>offset_flag</td><td>int</td><td>交易操作，用此字段区分股票买卖，期货开、平仓，期权 买卖等；参见数据字典在新窗口打开</td></tr></table></body></html>  

# #成交XtTrade  

<html><body><table><tr><td>属性</td><td>类 型</td><td>注释</td><td></td></tr><tr><td>account_type</td><td>int</td><td></td><td>账号类型，参见数据字典在新窗口打开</td></tr><tr><td>account_id</td><td>str</td><td>资金账号</td><td></td></tr><tr><td>stock_code</td><td>str</td><td>证券代码</td><td></td></tr><tr><td>order_type</td><td>int</td><td></td><td>委托类型，参见数据字典在新窗口打开</td></tr><tr><td>traded_id</td><td>str</td><td>成交编号</td><td></td></tr><tr><td>traded_time</td><td>int</td><td>成交时间</td><td></td></tr><tr><td>traded_price</td><td>float</td><td>成交均价</td><td></td></tr><tr><td>traded_volume</td><td>int</td><td>成交数量</td><td></td></tr><tr><td>traded_amount</td><td>float</td><td>成交金额</td><td></td></tr><tr><td>order_id</td><td>int</td><td>订单编号</td><td></td></tr><tr><td>order_sysid</td><td>str</td><td>柜台合同编号</td><td></td></tr><tr><td>strategy_name</td><td>str</td><td>策略名称</td><td></td></tr><tr><td>order_remark</td><td>str</td><td>委托备注</td><td></td></tr><tr><td>direction</td><td>int</td><td></td><td>多空方向，股票不适用；参见数据字典在新窗口打开</td></tr><tr><td>offset_flag</td><td>int</td><td></td><td>交易操作，用此字段区分股票买卖，期货开、平仓，期权 买卖等；参见数据字典在新窗口打开</td></tr></table></body></html>  

# #持仓XtPosition  

<html><body><table><tr><td>属性</td><td>类型</td><td></td><td>注释</td></tr><tr><td>account_type</td><td>int</td><td></td><td>账号类型，参见数据字典在新窗口打开</td></tr><tr><td></td><td></td><td>资金账号</td><td></td></tr><tr><td>accountid</td><td>str</td><td></td><td></td></tr></table></body></html>  

属性 类型 注释  
stock_code str 证券代码  
volume int 持仓数量  
can_use_volume int 可用数量  
open_price float 开仓价  
market_value float 市值  
frozen_volume int 冻结数量  
on_road_volume int 在途股份  
yesterday_volume int 昨夜拥股  
avg_price float 成本价  
direction int 多空方向，股票不适用；参见数据字典在新窗口打开  

# #期货持仓统计XtPositionStatistics  

属性 类型 注释  
account_id string 账户  
exchange_id string 市场代码  
exchange_name string 市场名称  
product_id string 品种代码  
instrument_id string 合约代码  
instrument_name string 合约名称多空方向，股票不适用；参见数据字  
direction int典在新窗口打开投保类型；参见投保类型在新窗口  
hedge_flag int打开  

# 属性  

# 类型  

position  
yesterday_position  
today_position  
can_close_vol  
position_cost  
avg_price  
position_profit  
float_profit  
open_price  
open_cost  
used_margin  
used_commission  
frozen_margin  
frozen_commission  
instrument_value  
open_times  
open_volume  
cancel_times  
last_price  
rise_ratio  
product_name  
royalty  
int 持仓数量  
int 昨仓数量  
int 今仓数量  
int 可平数量  
float 持仓成本  
float 持仓均价  
float 持仓盈亏  
float 浮动盈亏  
float 开仓均价  
float 开仓成本  
float 已使用保证金  
float 已使用的手续费  
float 冻结保证金  
float 冻结手续费  
float 市值， 合约价值  
int 开仓次数  
int 总开仓量 中间平仓不减  
int 撤单次数  
float 最新价  
float 当日涨幅  
string 产品名称  
float 权利金市值  

# 属性  

expire_date string 到期日assest_weight float 资产占比increase_by_settlement float 当日涨幅（结）margin_ratio float 保证金占比float_profit_divide_by_used_margin float 浮盈比例（保证金）float_profit_divide_by_balance float 浮盈比例（动态权益）today_profit_loss float 当日盈亏（结）yesterday_init_position int 昨日持仓frozen_royalty float 冻结权利金today_close_profit_loss float 当日盈亏（收）close_profit float 平仓盈亏ft_product_name string 品种名称  

# #异步下单委托反馈XtOrderResponse  

属性 类型 注释account_type int 账号类型，参见数据字典在新窗口打开account_id str 资金账号order_id int 订单编号strategy_name str 策略名称order_remark str 委托备注seq int 异步下单的请求序号  

<html><body><table><tr><td>属性</td><td>类型</td><td>注释</td></tr><tr><td>account_type</td><td>int</td><td>账号类型，参见数据字典在新窗口打开</td></tr><tr><td>account_id</td><td>str</td><td>资金账号</td></tr><tr><td>order_id</td><td>int</td><td>订单编号</td></tr><tr><td>order_sysid</td><td>str</td><td>柜台委托编号</td></tr><tr><td>cancel_result</td><td>int</td><td>撤单结果</td></tr><tr><td>seq</td><td>int</td><td>异步撤单的请求序号</td></tr></table></body></html>  

# #下单失败错误XtOrderError  

<html><body><table><tr><td>属性</td><td>类型</td><td>注释</td></tr><tr><td>account_type</td><td>int</td><td>账号类型，参见数据字典在新窗口打开</td></tr><tr><td>account_id</td><td>str</td><td>资金账号</td></tr><tr><td>order_id</td><td>int</td><td>订单编号</td></tr><tr><td>error_id</td><td>int</td><td>下单失败错误码</td></tr><tr><td>error_msg</td><td>str</td><td>下单失败具体信息</td></tr><tr><td>strategy_name</td><td>str</td><td>策略名称</td></tr><tr><td>order_remark</td><td>str</td><td>委托备注</td></tr></table></body></html>  

# #撤单失败错误XtCancelError  

属性 类型 注释account_type int 账号类型，参见数据字典在新窗口打开account_id str 资金账号order_id int 订单编号market int 交易市场 0:上海 1:深圳  

order_sysid str 柜台委托编号error_id int 下单失败错误码error_msg str 下单失败具体信息  

# #信用账号资产XtCreditDetail  

属性 类型 注释account_type int 账号类型，参见数据字典在新窗口打开account_id str 资金账号m_nStatus int 账号状态m_nUpdateTime int 更新时间m_nCalcConfig int 计算参数m_dFrozenCash float 冻结金额m_dBalance float 总资产m_dAvailable float 可用金额m_dPositionProfit float 持仓盈亏m_dMarketValue float 总市值m_dFetchBalance float 可取金额m_dStockValue float 股票市值m_dFundValue float 基金市值m_dTotalDebt float 总负债m_dEnableBailBalance float 可用保证金m_dPerAssurescaleValue float 维持担保比例  

# 属性  

m_dAssureAsset float 净资产m_dFinDebt float 融资负债m_dFinDealAvl float 融资本金m_dFinFee float 融资息费m_dSloDebt float 融券负债m_dSloMarketValue float 融券市值m_dSloFee float 融券息费m_dOtherFare float 其它费用m_dFinMaxQuota float 融资授信额度m_dFinEnableQuota float 融资可用额度m_dFinUsedQuota float 融资冻结额度m_dSloMaxQuota float 融券授信额度m_dSloEnableQuota float 融券可用额度m_dSloUsedQuota float 融券冻结额度m_dSloSellBalance float 融券卖出资金m_dUsedSloSellBalance float 已用融券卖出资金m_dSurplusSloSellBalance float 剩余融券卖出资金  

# #负债合约StkCompacts  

属性 类型 注释account_type int 账号类型，参见数据字典在新窗口打开account_id str 资金账号  

compact_type int 合约类型cashgroup_prop int 头寸来源exchange_id int 证券市场open_date int 开仓日期business_vol int 合约证券数量real_compact_vol int 未还合约数量ret_end_date int 到期日business_balance float 合约金额businessFare float 合约息费real_compact_balance float 未还合约金额real_compact_fare float 未还合约息费repaid_fare float 已还息费repaid_balance float 已还金额instrument_id str 证券代码compact_id str 合约编号position_str str 定位串  

# #融资融券标的CreditSubjects  

属性 类型 注释account_type int 账号类型，参见数据字典在新窗口打开account_id str 资金账号slo_status int 融券状态  

<html><body><table><tr><td>属性</td><td>类型</td><td>注彩</td></tr><tr><td>fin_status</td><td>int</td><td>融资状态</td></tr><tr><td>exchange_id</td><td>int</td><td>证券市场</td></tr><tr><td>slo_ratio</td><td>float</td><td>融券保证金比例</td></tr><tr><td>fin_ratio</td><td>float</td><td>融资保证金比例</td></tr><tr><td>instrument_id</td><td>str</td><td>证券代码</td></tr></table></body></html>  

# #可融券数据CreditSloCode  

<html><body><table><tr><td>属性</td><td>类型</td><td>注释</td></tr><tr><td>account_type</td><td>int</td><td>账号类型，参见数据字典在新窗口打开</td></tr><tr><td>account_id</td><td>str</td><td>资金账号</td></tr><tr><td>cashgroup_prop</td><td>int</td><td>头寸来源</td></tr><tr><td>exchange_id</td><td>int</td><td>证券市场</td></tr><tr><td>enable_amount</td><td>int</td><td>融券可融数量</td></tr><tr><td>instrument_id</td><td>str</td><td>证券代码</td></tr></table></body></html>  

# #标的担保品CreditAssure  

属性 类型 注释account_type int 账号类型，参见数据字典在新窗口打开account_id str 资金账号assure_status int 是否可做担保exchange_id int 证券市场assure_ratio float 担保品折算比例instrument_id str 证券代码  

# #账号状态XtAccountStatus  

<html><body><table><tr><td>属性</td><td>类型</td><td>注释</td></tr><tr><td>account_type</td><td>int</td><td>账号类型，参见数据字典在新窗口打开</td></tr><tr><td>account_id</td><td>str</td><td>资金账号</td></tr><tr><td>status</td><td>int</td><td>账号状态，参见数据字典在新窗口打开</td></tr></table></body></html>  

# #账号信息XtAccountInfo  

<html><body><table><tr><td>属性</td><td>类型</td><td>注释</td></tr><tr><td>account_type</td><td>int</td><td>账号类型，参见数据字典在新窗口打开</td></tr><tr><td>account_id</td><td>str</td><td>资金账号</td></tr><tr><td>broker_type</td><td>int</td><td>同account_type</td></tr><tr><td>platform_id</td><td>int</td><td>平台号</td></tr><tr><td>account_classification</td><td>int</td><td>账号分类</td></tr><tr><td>login_status</td><td>int</td><td>账号状态，参见数据字典在新窗口打开</td></tr></table></body></html>  

# #约券相关异步接口的反馈XtSmtAppointmentResponse  

<html><body><table><tr><td>属性</td><td>类型</td><td>注释</td></tr><tr><td>seq</td><td>int</td><td>异步请求序号</td></tr><tr><td>success</td><td>bool</td><td>申请是否成功</td></tr><tr><td>msg</td><td>str</td><td>反馈信息</td></tr><tr><td>apply_id</td><td>str</td><td>若申请成功返回资券申请编号，否则返回-1</td></tr></table></body></html>  

# #XtQuant API 说明  

#系统设置接口  

# #创建API 实例  

# XtQuantTrader(path, session_id)  

释义o 创建XtQuant API 的实例  
参数o path - str MiniQMT 客户端userdata_mini 的完整路径o session_id - int 与MiniQMT 通信的会话ID，不同的会话要保证不重  
返回o XtQuant API 实例对象  
备注o 后续对XtQuant API 的操作都需要该实例对象o 通常情况下只需要创建一个XtQuant API 实例  
示例  
path = 'D:\\迅投极速交易终端 睿智融科版\\userdata_mini'  
# session_id 为会话编号，策略使用方对于不同的Python 策略需要使用不同的会话编号  
session_id = 123456  
#后续的所有示例将使用该实例对象  
xt_trader = XtQuantTrader(path, session_id)  

# #注册回调类  

# register_callback(callback)  

释义o 将回调类实例对象注册到API 实例中，用以消息回调和主推  
参数o callback - XtQuantTraderCallback 回调类实例对象  
返回o 无  
备注o 无  
示例  
# 创建交易回调类对象，并声明接收回调  
class MyXtQuantTraderCallback(XtQuantTraderCallback)：pass  
callback = MyXtQuantTraderCallback()  
#xt_trader 为XtQuant API 实例对象  
xt_trader.register_callback(callback)  

# #准备API 环境  

start()  

释义o 启动交易线程，准备交易所需的环境  
参数o 无  
返回o 无  
备注o 无  
示例  

#xt_trader 为XtQuant API 实例对象  

# #创建连接  

connect()  

释义o 连接MiniQMT  
参数o 无  
返回o 连接结果信息，连接成功返回0，失败返回非0  
备注o 该连接为一次性连接，断开连接后不会重连，需要再次主动调用  
示例  

#xt_trader 为XtQuant API 实例对象  

#停止运行  

stop()  

释义o 停止API 接口  
参数o 无  
返回o 无  
备注o 无  
示例  

# xt_trader.stop()  

# #阻塞当前线程进入等待状态  

# run_forever()  

释义o 阻塞当前线程，进入等待状态，直到stop 函数被调用结束阻塞  
参数o 无  
返回o 无  
备注o  无  
示例  

#xt_trader 为XtQuant API 实例对象xt_trader.run_forever()  

# #开启主动请求接口的专用线程  

set_relaxed_response_order_enabled(enabled)  

释义o 控制主动请求接口的返回是否从额外的专用线程返回，以获得宽松的数据时序参数o enabled - bool 是否开启，默认为False 关闭返回o 无备注如果开启，在on_stock_order 等推送回调中调用同步请求不会卡住，但查询和推送的数据在时序上会变得不确定timeline t1 t2 t3 t4callback push1 push2 push3 resp4o do query4 ^例如：分别在t1 t2 t3 时刻到达三条委托数据，在on_push1 中调用同步委托查询接口query_orders()未开启宽松时序时，查询返回resp4 会在t4 时刻排队到push3 完成之后处理，这使得同步等待结果的查询不能返回而卡住执行  

o 开启宽松时序时，查询返回的resp4 由专用线程返回，程序正常执行，但此时查到的resp4 是push3 之后的状态，也就是说resp4 中的委托要比push2 push3 这两个前一时刻推送的数据新，但在更早的t1 时刻就进入了处理  

使用中请根据策略实际情况来开启，通常情况下，推荐在on_stock_order 等推送回调中使用查询接口的异步版本，如query_stock_orders_async  

# #操作接口  

# #订阅账号信息  

# subscribe(account)  

释义o 订阅账号信息，包括资金账号、委托信息、成交信息、持仓信息  
参数o account - StockAccount 资金账号  
返回o 订阅结果信息，订阅成功返回0，订阅失败返回-1  
备注o 无  
示例o 订阅资金账号1000000365  

account = StockAccount('1000000365')  

#xt_trader 为XtQuant API 实例对象 subscribe_result = xt_trader.subscribe(account)  

# #反订阅账号信息  

unsubscribe(account)  

释义o 反订阅账号信息  
参数o account - StockAccount 资金账号  
返回o 反订阅结果信息，订阅成功返回0，订阅失败返回-1  
备注o 无  

示例o 订阅资金账号1000000365  

account = StockAccount('1000000365') #xt_trader 为XtQuant API 实例对象 unsubscribe_result = xt_trader.unsubscribe(account)  

# #股票同步报单  

order_stock(account, stock_code, order_type, order_volume, price_type, price, strategy_name, order_remark)  

释义  

对股票进行下单操作  

o account - StockAccount 资金账号   
o stock_code - str 证券代码，如'600000.SH'   
o order_type - int 委托类型   
o order_volume - int 委托数量，股票以'股'为单位，债券以'张'为单位   
o price_type - int 报价类型   
o price - float 委托价格   
o strategy_name - str 策略名称   
o order_remark - str 委托备注  

返回o 系统生成的订单编号，成功委托后的订单编号为大于0 的正整数，如果为-1 表示委托失败  

例o 股票资金账号1000000365 对浦发银行买入1000 股，使用限价价格10.5元, 委托备注为'order_test'  

account = StockAccount('1000000365')   
#xt_trader 为XtQuant API 实例对象   
order_id = xt_trader.order_stock(account, '600000.SH', xtconstant.STOCK_BUY, 1000,   
xtconstant.FIX_PRICE, 10.5, 'strategy1', 'order_test')  

# #股票异步报单  

order_stock_async(account, stock_code, order_type, order_volume, price_type, price, strategy_name, order_remark)  

释义  

对股票进行异步下单操作，异步下单接口如果正常返回了下单请求序号seq，会收到on_order_stock_async_response 的委托反馈  

参数o account - StockAccount 资金账号  

o stock_code - str 证券代码， 如'600000.SH'  
o order_type - int 委托类型  
o order_volume - int 委托数量，股票以'股'为单位，债券以'张'为单位  
o price_type - int 报价类型  
o price - float 委托价格  
o strategy_name - str 策略名称  
o order_remark - str 委托备注  
返回o 返回下单请求序号seq，成功委托后的下单请求序号为大于0 的正整数，如果为-1 表示委托失败  
备注o 如果失败，则通过下单失败主推接口返回下单失败信息  
示例o 股票资金账号1000000365 对浦发银行买入1000 股，使用限价价格10.5元，委托备注为'order_test'  

# account = StockAccount('1000000365')  

#xt_trader 为XtQuant API 实例对象   
seq = xt_trader.order_stock_async(account, '600000.SH', xtconstant.STOCK_BUY, 1000,   
xtconstant.FIX_PRICE, 10.5, 'strategy1', 'order_test')  

# #股票同步撤单  

cancel_order_stock(account, order_id)  

释义o 根据订单编号对委托进行撤单操作  
参数o account - StockAccount 资金账号o order_id - int 同步下单接口返回的订单编号,对于期货来说，是order 结构中的order_sysid 字段  
返回o 返回是否成功发出撤单指令，0: 成功, -1: 表示撤单失败  
备注o 无  
示例o 股票资金账号1000000365 对订单编号为order_id 的委托进行撤单  
ccount = StockAccount('1000000365')  
rder_id = 100  
xt_trader 为XtQuant API 实例对象  
ancel_result = xt_trader.cancel_order_stock(account, order_id)  

# #股票同步撤单  

释义o 根据券商柜台返回的合同编号对委托进行撤单操作  
参数o account - StockAccount 资金账号o market - int 交易市场o order_sysid - str 券商柜台的合同编号  
返回o 返回是否成功发出撤单指令，0: 成功， -1: 表示撤单失败  
备注o 无  
示例o 股票资金账号1000000365 对柜台合同编号为order_sysid 的上交所委托进行撤单  
market = xtconstant.SH_MARKET  
order_sysid = "100"  
#xt_trader 为XtQuant API 实例对象  
cancel_result = xt_trader.cancel_order_stock_sysid(account, market, order_sysid)  

# #股票异步撤单  

cancel_order_stock_async(account, order_id)  

释义o 根据订单编号对委托进行异步撤单操作  
参数o account - StockAccount 资金账号o order_id - int 下单接口返回的订单编号，对于期货来说，是order 结构中的order_sysid  
返回o 返回撤单请求序号, 成功委托后的撤单请求序号为大于0 的正整数, 如果为-1 表示委托失败  
备注o 如果失败，则通过撤单失败主推接口返回撤单失败信息  
示例o 股票资金账号1000000365 对订单编号为order_id 的委托进行异步撤单  
order_id = 100  
#xt_trader 为XtQuant API 实例对象  
cancel_result = xt_trader.cancel_order_stock_async(account, order_id)  

# #股票异步撤单  

释义o 根据券商柜台返回的合同编号对委托进行异步撤单操作  
参数o account - StockAccount 资金账号o market - int 交易市场o order_sysid - str 券商柜台的合同编号  
返回o 返回撤单请求序号, 成功委托后的撤单请求序号为大于0 的正整数, 如果为-1 表示委托失败  
备注o 如果失败，则通过撤单失败主推接口返回撤单失败信息  
示例o 股票资金账号1000000365 对柜台合同编号为order_sysid 的上交所委托进行异步撤单  
account = StockAccount('1000000365')  
market = xtconstant.SH_MARKET  
order_sysid = "100"  
#xt_trader 为XtQuant API 实例对象  
cancel_result = xt_trader.cancel_order_stock_sysid_async(account, market, order_sysid)  

# #资金划拨  

fund_transfer(account, transfer_direction, price)  

释义 o 资金划拨   
参数 o account - StockAccount 资金账号 o transfer_direction - int 划拨方向，见数据字典划拨方向(transfer_direction) 字段说明 o price - float 划拨金额   
返回 o (success, msg)  

success - bool 划拨操作是否成功msg - str 反馈信息  

# #外部交易数据录入  

sync_transaction_from_external(operation, data_type, account, deal_list)  

释义 o 通用数据导出   
参数 o operation - str 操作类型，有"UPDATE","REPLACE","ADD","DELETE" o data_type - str 数据类型，有"DEAL"   
o account - StockAccount 资金账号   
o deal_list - list 成交列表,每一项是Deal 成交对象的参数字典,键名参考官网 数据字典,大小写保持一致  

返回  

![](images/3646a3441004dfceef3a6319d3294ddcf62958274602ec96f59c408be4486af0.jpg)  

# #股票查询接口  

# #资产查询  

query_stock_asset(account)  

释义o 查询资金账号对应的资产  
参数o account - StockAccount 资金账号  
返回o 该账号对应的资产对象XtAsset 在新窗口打开或者None  
备注o 返回None 表示查询失败  
示例o 查询股票资金账号1000000365 对应的资产数据  

account = StockAccount('1000000365') #xt_trader 为XtQuant API 实例对象 asset = xt_trader.query_stock_asset(account)  

# #委托查询  

query_stock_orders(account, cancelable_only = False)  

释义o 查询资金账号对应的当日所有委托  
参数  

o account - StockAccount 资金账号  

cancelable_only - bool 仅查询可撤委托  
返回o 该账号对应的当日所有委托对象XtOrder 在新窗口打开组成的list 或者None  
备注o None 表示查询失败或者当日委托列表为空  
示例o 查询股票资金账号1000000365 对应的当日所有委托  

account = StockAccount('1000000365') #xt_trader 为XtQuant API 实例对象 orders = xt_trader.query_stock_orders(account, False)  

# #成交查询  

# query_stock_trades(account)  

释义o 查询资金账号对应的当日所有成交  
参数o account - StockAccount 资金账号  
返回o 该账号对应的当日所有成交对象XtTrade 在新窗口打开组成的list 或者None  
备注o None 表示查询失败或者当日成交列表为空  
示例o 查询股票资金账号1000000365 对应的当日所有成交  

# account = StockAccount('1000000365')  

#xt_trader 为XtQuant API 实例对象  

trades = xt_trader.query_stock_trades(account)  

# #持仓查询  

query_stock_positions(account)  

释义o 查询资金账号对应的持仓  
参数o account - StockAccount 资金账号  
返回o 该账号对应的最新持仓对象XtPosition 在新窗口打开组成的list 或者None  
备注o None 表示查询失败或者当日持仓列表为空  
示例  

查询股票资金账号1000000365 对应的最新持仓 account = StockAccount('1000000365') #xt_trader 为XtQuant API 实例对象 positions = xt_trader.query_stock_positions(account)  

# #期货持仓统计查询  

# query_position_statistics(account)  

释义o 查询期货账号的持仓统计  
参数o account - StockAccount 资金账号  
返回o 该账号对应的最新持仓对象XtPositionStatistics 在新窗口打开组成的list 或者None  
备注o None 表示查询失败或者当日持仓列表为空  
示例o 查询期货资金账号1000000365 对应的最新持仓  

account = StockAccount('1000000365', 'FUTURE') #xt_trader 为XtQuant API 实例对象 positions = xt_trader.query_position_statistics(account)  

# #信用查询接口  

# #信用资产查询  

query_credit_detail(account)  

释义o 查询信用资金账号对应的资产  
参数o account - StockAccount 资金账号  
返回o 该信用账户对应的资产对象XtCreditDetail 在新窗口打开组成的list 或者None  
备注None 表示查询失败o 通常情况下一个资金账号只有一个详细信息数据  
示例o 查询信用资金账号1208970161 对应的资产信息  

#xt_trader 为XtQuant API 实例对象 datas = xt_trader.query_credit_detail(account)  

# #负债合约查询  

# query_stk_compacts(account)  

释义o 查询资金账号对应的负债合约  
参数o account - StockAccount 资金账号  
返回o 该账户对应的负债合约对象StkCompacts 在新窗口打开组成的list 或者None  
备注o None 表示查询失败或者负债合约列表为空  
示例o 查询信用资金账号1208970161 对应的负债合约  

account = StockAccount('1208970161', 'CREDIT') #xt_trader 为XtQuant API 实例对象 datas = xt_trader.query_stk_compacts(account)  

# #融资融券标的查询  

query_credit_subjects(account)  

释义o 查询资金账号对应的融资融券标的  
参数o account - StockAccount 资金账号  
返回该账户对应的融资融券标的对象CreditSubjects 在新窗口打开组成的list 或者None  
备注o None 表示查询失败或者融资融券标的列表为空  
示例o 查询信用资金账号1208970161 对应的融资融券标的  

account = StockAccount('1208970161', 'CREDIT')  

#xt_trader 为XtQuant API 实例对象 datas = xt_trader.query_credit_subjects(account)  

# #可融券数据查询  

query_credit_slo_code(account)  

释义  

查询资金账号对应的可融券数据  
参数o account - StockAccount 资金账号  
返回o 该账户对应的可融券数据对象CreditSloCode 在新窗口打开组成的list 或者None  
备注o None 表示查询失败或者可融券数据列表为空  
示例o 查询信用资金账号1208970161 对应的可融券数据  

account = StockAccount('1208970161', 'CREDIT') #xt_trader 为XtQuant API 实例对象 datas = xt_trader.query_credit_slo_code(account)  

# #标的担保品查询  

query_credit_assure(account)  

释义o 查询资金账号对应的标的担保品  
参数o account - StockAccount 资金账号  
返回  
该账户对应的标的担保品对象CreditAssure 在新窗口打开组成的list 或者None  
备注o None 表示查询失败或者标的担保品列表为空  
示例o 查询信用资金账号1208970161 对应的标的担保品  

account = StockAccount('1208970161', 'CREDIT')  

#xt_trader 为XtQuant API 实例对象 datas = xt_trader.query_credit_assure(account)  

# #其他查询接口  

# #新股申购额度查询  

query_new_purchase_limit(account)  

释义o 查询新股申购额度  
参数o account - StockAccount 资金账号  
返回dict 新股申购额度数据集{ type1: number1, type2: number2, ... }type - str 品种类型KCB - 科创板，SH - 上海，SZ - 深圳number - int 可申购股数  
备注o 数据仅代表股票申购额度，债券的申购额度固定10000 张  

# #当日新股信息查询  

query_ipo_data()  

释义o 查询当日新股新债信息  
参数o 无  
返回dict 新股新债信息数据集{ stock1: info1, stock2: info2, ... }stock - str 品种代码，例如 '301208.SZ'info - dict 新股信息name - str 品种名称type - str 品种类型STOCK - 股票，BOND - 债券minPurchaseNum / maxPurchaseNum - int 最小 /最大申购额度单位为股（股票）/ 张（债券）purchaseDate - str 申购日期issuePrice - float 发行价返回值示例{'754810.SH': {'name': '丰山发债', 'type': 'BOND', 'maxPurchaseNum':10000, 'minPurchaseNum': 10, 'purchaseDate': '20220627', 'issuePrice':100.0}, '301208.SZ': {'name': '中亦科技', 'type': 'STOCK','maxPurchaseNum': 16500, 'minPurchaseNum': 500, 'purchaseDate':'20220627', 'issuePrice': 46.06}}  
备注  

o 无  

# #账号信息查询  

释义o 查询所有资金账号  
参数o 无  
返回o list 账号信息列表[ XtAccountInfo ]  
备注o 无  

# #账号状态查询  

query_account_status()  

释义o 查询所有账号状态  
参数o 无  
返回list 账号状态列表[ XtAccountStatus ]  
备注o  无  

# #普通柜台资金查询  

query_com_fund(account)  

释义o 划拨业务查询普通柜台的资金  
参数o account - StockAccount 资金账号  
返回o result - dict 资金信息，包含以下字段success - bool■ erro - strcurrentBalance - double 当前余额enableBalance - double 可用余额fetchBalance - double 可取金额interest - double 待入账利息assetBalance - double 总资产fetchCash - double 可取现金marketValue - double 市值  

debt - double 负债  

# #普通柜台持仓查询  

query_com_position(account)  

释义o 划拨业务查询普通柜台的持仓参数O account - StockAccount 资金账号返回o result - list 持仓信息列表[position1, position2, ...]position - dict 持仓信息，包含以下字段success - bool■ error - strstockAccount - str 股东号exchangeType - str 交易市场口 stockCode - str 证券代码stockName - str 证券名称totalAmt - float 总量enableAmount - float 可用量lastPrice - float 最新价costPrice - float 成本价income - float 盈亏incomeRate - float 盈亏比例marketValue - float 市值costBalance - float 成本总额bsOnTheWayVol - int 买卖在途量prEnableVol - int 申赎可用量  

# #通用数据导出  

export_data(account, result_path, data_type, start_time = None, end_time = None, user_param = {})  

释义o 通用数据导出  
参数o account - StockAccount 资金账号o result_path - str 导出路径，包含文件名及.csv 后缀，如'C:\Users\Desktop\test\deal.csv'o data_type - str 数据类型，如'deal'o start_time - str 开始时间（可缺省）o end_time - str 结束时间（可缺省）o user_param - dict 用户参数（可缺省）  
返回  

o result - dict 结果反馈信息  

示例  

resp = xt_trader.export_data(acc, 'C:\\Users\\Desktop\\test\\deal.csv', 'deal')   
print(resp)   
#成功输出示例：{'msg': 'export success'}   
#失败输出示例：{'error': {'errorMsg': 'can not find account info, accountID:2000449   
accountType:2'}}  

# #通用数据查询  

query_data(account, result_path, data_type, start_time = None, end_time = None, user_param = {})  

释义o 通用数据查询，利用export_data 接口导出数据后再读取其中的数据内容，读取完毕后删除导出的文件  
参数  
同export_data  
返回o result - dict 数据信息  
示例  
data = xt_trader.query_data(acc, 'C:\\Users\\Desktop\\test\\deal.csv', 'deal')  
print(data)  
#成功输出示例：  
# account_id account_Type stock_code order_type  
#0 2003695 2 688488.SH 23  
#1 2003695 2 000096.SZ 23  
#失败输出示例：{'error': {'errorMsg': 'can not find account info, accountID:2000449  
accountType:2'}}  

# #约券相关接口  

# #券源行情查询  

smt_query_quoter(account)  

释义o 券源行情查询  
参数o account - StockAccount 资金账号  
返回o result - list 券源信息列表[quoter1, quoter2, ...]quoter - dict 券源信息，包含以下字段success - bool  
error - str  
finType - str 金融品种  
stockType - str 证券类型  
date - int 期限天数  
code - str 证券代码  
codeName - str 证券代码名称  
exchangeType - str 市场  
fsmpOccupedRate - float 资券占用利率  
fineRate - float 罚息利率  
fsmpreendRate - float 资券提前归还利率  
usedRate - float 资券使用利率  
unUusedRate - float 资券占用未使用利率  
initDate - int 交易日期  
endDate - int 到期日期  
enableSloAmountT0 - float $\mathsf{T}\!+\!0$ 可融券数量  
enableSloAmountT3 - float $\mathsf{T}\!+\!3$ 可融券数量  
srcGroupId - str 来源组编号  
applyMode - str 资券申请方式，"1":库存券，"2":专项券  
lowDate - int 最低期限天数  

# #库存券约券申请  

smt_negotiate_order_async(self, account, src_group_id, order_code, date, amount, apply_rate, dict_param={})  

释义o 库存券约券申请的异步接口，异步接口如果正常返回了请求序号seq，会收到on_smt_appointment_async_response 的反馈  
参数o account - StockAccount 资金账号o src_group_id - str 来源组编号o order_code - str 证券代码，如'600000.SH'o date - int 期限天数o amount - int 委托数量o apply_rate - float 资券申请利率注：目前有如下参数通过一个可缺省的字典传递，键名与参数名称相同o dict_param - dict 可缺省的字典参数■ subFareRate - float 提前归还利率fineRate - float 罚息利率  
返回o 返回请求序号seq，成功发起申请后的请求序号为大于0 的正整数，如果为-1 表示发起申请失败  

示例  

# #约券合约查询  

# smt_query_compact(account)  

释义  

约券合约查询  

account - StockAccount 资金账号result - list 约券合约信息列表[compact1, compact2, ...]compact - dict 券源信息，包含以下字段  

■ success - bool  
■ error - str  
createDate - int 创建日期  
■ cashcompactId - str 头寸合约编号  
■ oriCashcompactId - str 原头寸合约编号  
■ applyId - str 资券申请编号  
■ srcGroupId - str 来源组编号  
■ comGroupId - str 资券组合编号  
■ finType - str 金融品种  
■ exchangeType - str 市场  
■ code - str 证券代码  
■ codeName - str 证券代码名称date - int 期限天数beginCompacAmount - float 期初合约数量beginCompacBalance - float 期初合约金额compacAmount - float 合约数量  
■ compacBalance - float 合约金额  
■ returnAmount - float 返还数量returnBalance - float 返还金额realBuyAmount - float 回报买入数量fsmpOccupedRate - float 资券占用利率compactInterest - float 合约利息金额compactFineInterest - float 合约罚息金额repaidInterest - float 已还利息repaidFineInterest - float 归还罚息  
■ fineRate - float 罚息利率  
■ preendRate - float 资券提前归还利率  
■ compactType - str 资券合约类型postponeTimes - int 展期次数compactStatus - str 资券合约状态，"0":未归还，"1":部分归还，"2":提前了结，"3":到期了结，"4":逾期了结，"5":逾期，"9":已作废lastInterestDate - int 上次结息日期interestEndDate - int 记息结束日期  
■ validDate - int 有效日期  
■ dateClear - int 清算日期  
■ usedAmount - float 已使用数量usedBalance - float 使用金额  
■ usedRate - float 资券使用利率  
■ unUusedRate - float 资券占用未使用利率srcGroupName - str 来源组名称repaidDate - int 归还日期  
■ preOccupedInterest - float 当日实际应收利息  
口 compactInterestx - float 合约总利息enPostponeAmount - float 可展期数量postponeStatus - str 合约展期状态，"0":未审核，"1":审核通过，"2":已撤销，"3":审核不通过applyMode - str 资券申请方式，"1":库存券，"2":专项券  

# #回调类  

![](images/f8051907c86abb3e1daadf65e0a9ed1f15ae7f17b9c11b5c3b73a2b5f71774f6.jpg)  

![](images/a0628f1d2a10a68117cfd6389fa5e5d59a912dc87773e5e4e40bacf100af9867.jpg)  

# #连接状态回调  

on_disconnected()  

释义o 失去连接时推送信息  
参数o 无  
返回o 无  
备注o 无  

# #账号状态信息推送  

# on_account_status(data)  

释义o 账号状态信息变动推送  
参数o data - XtAccountStatus 在新窗口打开 账号状态信息  
返回o 无  
备注o 无  

# #委托信息推送  

# on_stock_order(data)  

释义o 委托信息变动推送,例如已成交数量，委托状态变化等  
参数o data - XtOrder 在新窗口打开 委托信息  
返回o 无  
备注o 无  

# #成交信息推送  

# on_stock_trade(data)  

释义o 成交信息变动推送  
参数o data - XtTrade 在新窗口打开 成交信息  
返回o 无  

备注o 无#下单失败信息推送  

# on_order_error(data)  

释义o 下单失败信息推送  
参数o data - XtOrderError 在新窗口打开 下单失败信息  
返回o 无  
备注o 无  

# #撤单失败信息推送  

# on_cancel_error(data)  

释义o 撤单失败信息的推送  
参数o data - XtCancelError 在新窗口打开 撤单失败信息  
返回o 无  
备注o 无  

# #异步下单回报推送  

# on_order_stock_async_response(data)  

释义o 异步下单回报推送  
参数o data - XtOrderResponse 在新窗口打开 异步下单委托反馈  
返回o 无  
备注o 无  

#约券相关异步接口的回报推送  

释义o 异步约券相关接口回报推送  
参数o data - XtSmtAppointmentResponse 在新窗口打开 约券相关异步接口的反馈  
返回o 无  
备注o 无  

上次更新: 2024/12/2 19:03:47  

# 行情示例  

# #获取行情示例  

新手示例  

# 用前须知  

## xtdata 提供和MiniQmt 的交互接口，本质是和MiniQmt 建立连接，由MiniQmt 处理行情数据请求，再把结果回传返回到python 层。使用的行情服务器以及能获取到的行情数据和MiniQmt 是一致的，要检查数据或者切换连接时直接操作MiniQmt 即可。  

## 对于数据获取接口，使用时需要先确保MiniQmt 已有所需要的数据，如果不足可以通过补充数据接口补充，再调用数据获取接口获取。  

## 对于订阅接口，直接设置数据回调，数据到来时会由回调返回。订阅接收到的数据一般会保存下来，同种数据不需要再单独补充。  

代码讲解  

从本地python 导入xtquant 库，如果出现报错则说明安装失败rom xtquant import xtdata  

import time  

code_list = ["000001.SZ"] 设定获取数据的周期 period = "1d"  

## 为了方便用户进行数据管理，xtquant 的大部分历史数据都是以压缩形式存储在本地的## 比如行情数据，需要通过download_history_data 下载，财务数据需要通过## 所以在取历史数据之前，我们需要调用数据下载接口，将数据下载到本地  

xtdata.download_history_data(i,period=period,incrementally=True) # 增量下载行情数据（开高低收,等等）到本地  

xtdata.download_financial_data(code_list) # 下载财务数据到本地xtdata.download_sector_data() # 下载板块数据到本地# 更多数据的下载方式可以通过数据字典查询  

读取本地历史行情数据  

history_data = xtdata.get_market_data_ex([],code_list,period=period,count=-1) print(history_data)  

print("=" \* 20)  

如果需要盘中的实时行情，需要向服务器进行订阅后才能获取订阅后，get_market_data 函数于get_market_data_ex 函数将会自动拼接本地历史行情与服务器实时行情  

# 向服务器订阅数据  

xtdata.subscribe_quote(i,period=period,count=-1) # 设置count = -1 来取到当天所有实时行  

等待订阅完成time.sleep(1)  

获取订阅后的行情  

kline_data = xtdata.get_market_data_ex([],code_list,period=period) print(kline_data)  

获取订阅后的行情，并以固定间隔进行刷新,预期会循环打印10 次for i in range(10):# 这边做演示，就用for 来循环了，实际使用中可以用while Truekline_data = xtdata.get_market_data_ex([],code_list,period=period)print(kline_data)time.sleep(3) # 三秒后再次获取行情  

# 如果不想用固定间隔触发，可以以用订阅后的回调来执行  
# 这种模式下当订阅的callback 回调函数将会异步的执行，每当订阅的标的tick 发生变化更  
新，callback 回调函数就会被调用一次  
# 本地已有的数据不会触发callback  

![](images/039ae253129b9c08c78b0053155d5a749d67d561b9e5ad0cd386d72c09967712.jpg)  

# #连接VIP 服务器  

![](images/9c3c6c2129214364a0aac16c4d0a69a73932e4c9a7e37ac458e66841d766bea2.jpg)  

![](images/e03f7522c6b1cad5b8001a7884b0a90187c557fbd97777a4138dbd2de92e1026.jpg)  

# #连接指定服务器  

python import time  

from xtquant import xtdata   
#用token 方式连接，不需要账号密码   
#其他连接方式，需要账号密码   
info = {"ip": "218.16.123.122", "port": 55300, "username": '', "pwd": ''}   
connect_success = 0   
def func(d): ip = d.get('ip', '') port = d.get('port') status = d.get('status', 'disconnected') global connect_success if ip == info['ip'] and port == info['port']: if status == 'connected': connect_success = 1 else: connect_success = 2   
# 注册连接回调信息   
xtdata.watch_quote_server_status(func)   
# 行情连接   
qs = xtdata.QuoteServer(info)   
qs.connect()   
# 获取当前数据连接站点   
data_server_info = xtdata.get_quote_server_status() 显示当前数据连接站点   
if 1: for k,v in data_server_info.items(): print(f"data:{k}, connect info:{v.info}")   
# 等待连接状态   
while connect_success == 0: time.sleep(0.3)   
if connect_success == 2: print("连接失败")  

# #指定初始化行情连接范围  

python  

if 1: from xtquant import xtdatacenter as xtdc ## 设置数据目录 xtdc.set_data_home_dir('data') ## 设置token token = "你的token" xtdc.set_token(token) ## 限定行情站点的优选范围 opt_list = [ '115.231.218.73:55310', '115.231.218.79:55310', '42.228.16.210:55300', '42.228.16.211:55300', '36.99.48.20:55300', '36.99.48.21:55300', xtdc.set_allow_optmize_address(opt_list) ## 开启指定市场的K 线全推 xtdc.set_kline_mirror_markets(['SH', 'SZ', 'BJ']) ## 设置要初始化的市场列表 init_markets = [ 'SH', 'SZ', 'BJ', #'DF', 'GF', 'IF', 'SF', 'ZF', 'INE', #'SHO', 'SZO', xtdc.set_init_markets(init_markets) ## 初始化xtdc 模块 xtdc.init(start_local_service = False) ## 监听端口 #xtdc.listen(port = 58620) listen_port = xtdc.listen(port = (58620, 58650)) #import code; code.interact(local = locals())   
import xtquant.xtdata as xtdata  

# #订阅全推数据/下载历史数据  

![](images/03d9d01298fc8671b557af6d82c75d5bfe6328429e30768d0e6c846d35a2d3fd.jpg)  

# #获取对手价  

python 返回值  

import pandas as pd import numpy as np from xtquant import xtdata  

to_do_trade_list = ["000001.SZ"] tick = xtdata.get_full_tick(to_do_trade_list)  

取买一价为对手价，若买一价为0，说明已经跌停，则取最新价 or i in tick:  

fix_price = tick[i]["bidPrice"][0] if tick[i]["bidPrice"][0] != 0 else tick[i]["lastPrice"] print(fix_price)  

# #复权计算方式  

python  

![](images/e8b073e13ff62e9b39f5ef8ba996c346af9490eee4bafecf450d443d68951c45.jpg)  

![](images/5576fa3faf38a464c10bbc58d00c7065b1a56cbe0309f22c6980df0595ea1fca.jpg)  

'002594.SZ'  

#xtdata.download_history_data(s, '1d', '20100101', '  

dd = xtdata.get_divid_factors(s) print(dd)  

等比前复权  

datas_forward_ratio = process_forward_ratio(datas_ori, dd) print('datas_forward_ratio', datas_forward_ratio)  

等比后复权  

datas_backward_ratio = process_backward_ratio(datas_ori, dd) print('datas_backward_ratio', datas_backward_ratio)  

#前复权 datas_forward = process_forward(datas_ori, dd) print('datas_forward', datas_forward)  

datas_backward = process_backward(datas_ori, dd) print('datas_backward', datas_backward)  

# #根据商品期货期权代码获取对应的商品期货合约代码  

python 返回值  

![](images/3b17509c62bc9a65492a99155991c052f04a9d13ae09e3120643d4e782739046.jpg)  

#根据指数代码，返回对应的期货合约  

![](images/92acf219bf4110b44c74beab7843b45eafc08e5ffa1adb62ab5fb7bfeeaf3b23.jpg)  

# #交易示例  

# #简单买卖各一笔示例  

# 需要调整的参数：  

98 行的path 变量需要改为本地客户端路径,券商端指定到 f"{安装目录}\userdata_mini",投研端指定到f"{安装目录}\userdata"107 行的资金账号需要调整为自身资金账号  

# coding:utf-8 import time, datetime, traceback, sys from xtquant import xtdata  

from xtquant.xttrader import XtQuantTrader, XtQuantTraderCallback   
from xtquant.xttype import StockAccount   
from xtquant import xtconstant  

定义一个类 创建类的实例 作为状态的容器class _a():  

A = _a()  

A.bought_list = [ A.hsa = xtdata.get_stock_list_in_sector('沪深A 股')  

def interact(): """执行后进入repl 模式""" code.InteractiveConsole(locals=globals()).interact()  

xtdata.download_sector_data()  

class MyXtQuantTraderCallback(XtQuantTraderCallback): def on_disconnected(self):  

连接断开 :return:  

print(datetime.datetime.now(), '连接断开回调')  

def on_stock_order(self, order):  

委托回报推送   
:param order: XtOrder 对象   
:return:  

:param trade: XtTrade 对象 :return:  

print(datetime.datetime.now(), '成交回调', trade.order_remark, f"委托方向(48 买 49卖) {trade.offset_flag} 成交价格 {trade.traded_price} 成交数量 {trade.traded_volume}")  

def on_order_error(self, order_error):  

委托失败推送   
:param order_error:XtOrderError 对象   
:return:  

def on_cancel_error(self, cancel_error):  

撤单失败推送   
:param cancel_error: XtCancelError 对象   
:return:  

print(datetime.datetime.now(), sys._getframe().f_code.co_name)  

def on_order_stock_async_response(self, response):  

异步下单回报推送   
:param response: XtOrderResponse 对象   
:return:  

print(f"异步委托回调 投资备注: {response.order_remark}")  

def on_cancel_order_stock_async_response(self, response):  

:param response: XtCancelOrderResponse 对象 :return:  

print(datetime.datetime.now(), sys._getframe().f_code.co_name)  

def on_account_status(self, status):  

:param response: XtAccountStatus 对象 :return:  

f __name__ == '__main__':print("start")# 指定客户端所在路径, 券商端指定到 userdata_mini 文件夹# 注意：如果是连接投研端进行交易，文件目录需要指定到f"{安装目录}\userdata"path = r'D:\qmt\投研\迅投极速交易终端睿智融科版\userdata'# 生成session id 整数类型 同时运行的策略不能重复session_id = int(time.time())xt_trader = XtQuantTrader(path, session_id)# 开启主动请求接口的专用线程 开启后在on_stock_xxx 回调函数里调用  
XtQuantTrader.query_xxx 函数不会卡住回调线程，但是查询和推送的数据在时序上会变得不确# 详见: http://docs.thinktrader.net/vip/pages/ee0e9b/#开启主动请求接口的专用线程# xt_trader.set_relaxed_response_order_enabled(True)# 创建资金账号为 800068 的证券账号对象 股票账号为STOCK 信用CREDIT 期货  
FUTUREacc = StockAccount('2000128', 'STOCK')# 创建交易回调类对象，并声明接收回调callback = MyXtQuantTraderCallback()xt_trader.register_callback(callback)# 启动交易线程xt_trader.start()# 建立交易连接，返回0 表示连接成功connect_result = xt_trader.connect()print('建立交易连接，返回0 表示连接成功', connect_result)# 对交易回调进行订阅，订阅后可以收到交易主推，返回0 表示订阅成功subscribe_result = xt_trader.subscribe(acc)print('对交易回调进行订阅，订阅后可以收到交易主推，返回0 表示订阅成功',  
subscribe_result)#取账号信息account_info = xt_trader.query_stock_asset(acc)#取可用资金available_cash = account_info.m_dCashprint(acc.account_id, '可用资金', available_cash)#查账号持仓positions = xt_trader.query_stock_positions(acc)#取各品种 总持仓 可用持仓position_total_dict = {i.stock_code : i.m_nVolume for i in positions}position_available_dict = {i.stock_code : i.m_nCanUseVolume for i in positions}print(acc.account_id, '持仓字典', position_total_dict)print(acc.account_id, '可用持仓字典', position_available_dict)#买入 浦发银行 最新价 两万元stock = '600000.SH'target_amount = 20000full_tick = xtdata.get_full_tick([stock])print(f"{stock} 全推行情： {full_tick}")current_price = full_tick[stock]['lastPrice']#买入金额 取目标金额 与 可用金额中较小的buy_amount = min(target_amount, available_cash)#买入数量 取整为100 的整数倍buy_vol = int(buy_amount / current_price / 100) \* 100print(f"当前可用资金 {available_cash} 目标买入金额 {target_amount} 买入股数  
{buy_vol}股")async_seq = xt_trader.order_stock_async(acc, stock, xtconstant.STOCK_BUY, buy_vol,  
xtconstant.FIX_PRICE, current_price,#卖出 500 股stock = '513130.SH'#目标数量target_vol = 500#可用数量available_vol = position_available_dict[stock] if stock in position_available_dict else 0#卖出量取目标量与可用量中较小的sell_vol = min(target_vol, available_vol)print(f"{stock} 目标卖出量 {target_vol} 可用数量 {available_vol} 卖出 {sell_vol}股")if sell_vol > 0:async_seq = xt_trader.order_stock_async(acc, stock, xtconstant.STOCK_SELL, sell_vol,  
xtconstant.LATEST_PRICE,-1,'strategy_name', stock)print(f"下单完成 等待回调")# 阻塞主线程退出xt_trader.run_forever()# 如果使用vscode pycharm 等本地编辑器 可以进入交互模式 方便调试 （把上一行的  
run_forever 注释掉 否则不会执行到这里）interact()  

# #单股订阅实盘示例  

# 需要调整的参数：  

113 行的path 变量需要改为本地客户端路径,券商端指定到 f"{安装目录}\userdata_mini",投研端指定到f"{安装目录}\userdata"122 行的资金账号需要调整为自身资金账号  

python  

# coding:utf-8   
import time, datetime, traceback, sys   
from xtquant import xtdata   
from xtquant.xttrader import XtQuantTrader, XtQuantTraderCallback   
from xtquant.xttype import StockAccount   
from xtquant import xtconstant  

定义一个类 创建类的实例 作为状态的容器class _a():  

A = _a()   
A.bought_list = []   
A.hsa = xtdata.get_stock_list_in_sector('沪深A 股')  

def interact():"""执行后进入repl 模式"""import codecode.InteractiveConsole(locals=globals()).interact()  

xtdata.download_sector_data()  

def f(data):  

print(data) now = datetime.datetime.now()  

for stock in data: if stock not in A.hsa: continue cuurent_price = data[stock][0]['close'] pre_price = data[stock][0]['preClose'] ratio = cuurent_price / pre_price - 1 if pre_price > 0 else 0 if ratio > 0.09 and stock not in A.bought_list: print(f"{now} 最新价 买入 {stock} 100 股")  

async_seq = xt_trader.order_stock_async(acc, stock, xtconstant.STOCK_BUY, 100,   
xtconstant.LATEST_PRICE, -1, 'strategy_name', stock) A.bought_list.append(stock)   
class MyXtQuantTraderCallback(XtQuantTraderCallback): def on_disconnected(self): 连接断开 :return: """ print(datetime.datetime.now(), '连接断开回调') def on_stock_order(self, order): 委托回报推送 :param order: XtOrder 对象 :return: print(datetime.datetime.now(), '委托回调', order.order_remark) def on_stock_trade(self, trade): """ 成交变动推送 :param trade: XtTrade 对象 :return: """ print(datetime.datetime.now(), '成交回调', trade.order_remark) def on_order_error(self, order_error): """ 委托失败推送 :param order_error:XtOrderError 对象 :return: """ # print("on order_error callback") # print(order_error.order_id, order_error.error_id, order_error.error_msg) print(f"委托报错回调 {order_error.order_remark} {order_error.error_msg}") def on_cancel_error(self, cancel_error): """ 撤单失败推送  

print(datetime.datetime.now(), sys._getframe().f_code.co_name)  

异步下单回报推送   
:param response: XtOrderResponse 对象   
:return:  

print(f"异步委托回调 {response.order_remark}")  

def on_cancel_order_stock_async_response(self, response): """ :param response: XtCancelOrderResponse 对象 :return:  

print(datetime.datetime.now(), sys._getframe().f_code.co_name)  

def on_account_status(self, status):  

:param response: XtAccountStatus 对象 :return:  

print(datetime.datetime.now(), sys._getframe().f_code.co_name)  

name__ == ' _main__':  

# print("start"  

# 指定客户端所在路径, 券商端指定到 userdata_mini 文件夹  
# 注意：如果是连接投研端进行交易，文件目录需要指定到f"{安装目录}\userdata"  
path = r'D:\qmt\投研\迅投极速交易终端睿智融科版\userdata'  
# 生成session id 整数类型 同时运行的策略不能重复  

session_id = int(time.time())  

xt_trader = XtQuantTrader(path, session_id)  

# 开启主动请求接口的专用线程 开启后在on_stock_xxx 回调函数里调用tQuantTrader.query_xxx 函数不会卡住回调线程，但是查询和推送的数据在时序上会变得不确# 详见: http://docs.thinktrader.net/vip/pages/ee0e9b/#开启主动请求接口的专用线程# xt_trader.set_relaxed_response_order_enabled(True)  

# 创建资金账号为 800068 的证券账号对象 股票账号为STOCK 信用CREDIT 期货UTURE  

acc = StockAccount('2000128', 'STOCK')  

![](images/92a42f766b47ee90991a1625d89af55cc9ee24b76b031d8cd6b87fab0453e6dd.jpg)  

# #全推订阅实盘示例  

本示例用于展示如何订阅上海及深圳市场全推，对于沪深A 股品种策略进行判断当前涨幅超过 9 个点的买入 200 股  

# 需要调整的参数：  

111 行的path 变量需要改为本地客户端路径  
116 行的资金账号需要调整为自身资金账号  

# 注意  

本策略只用于提供策略写法及参考，若您直接进行实盘下单，造成损失本网站不负担责任。  

python  

#coding:utf-8   
import time, datetime, traceback, sys   
from xtquant import xtdata   
from xtquant.xttrader import XtQuantTrader, XtQuantTraderCallback   
from xtquant.xttype import StockAccount   
from xtquant import xtconstant   
#定义一个类 创建类的实例 作为状态的容器   
class _a(): pass   
A = _a()   
A.bought_list = []   
A.hsa = xtdata.get_stock_list_in_sector('沪深A 股')   
def interact(): """执行后进入repl 模式""" import code code.InteractiveConsole(locals=globals()).interact()   
xtdata.download_sector_data()   
def f(data): now = datetime.datetime.now() for stock in data: if stock not in A.hsa: continue cuurent_price = data[stock][0]['lastPrice'] pre_price = data[stock][0]['lastClose'] ratio = cuurent_price / pre_price - 1 if pre_price > 0 else 0 if ratio > 0.09 and stock not in A.bought_list: print(f"{now} 最新价 买入 {stock} 200 股") async_seq = xt_trader.order_stock_async(acc, stock, xtconstant.STOCK_BUY, 200,   
xtconstant.LATEST_PRICE, -1, 'strategy_name', stock) A.bought_list.append(stock)   
class MyXtQuantTraderCallback(XtQuantTraderCallback): def on_disconnected(self): """ 连接断开 :return: """ print(datetime.datetime.now(),'连接断开回调') def on_stock_order(self, order):   
委托回报推送   
:param order: XtOrder 对象   
:return:   
成交变动推送   
:param trade: XtTrade 对象   
:return:  

print(datetime.datetime.now(), '成交回调', trade.order_remark)  

def on_order_error(self, order_error):  

委托失败推送   
:param order_error:XtOrderError 对象   
:return:  

def on_cancel_error(self, cancel_error):  

撤单失败推送   
:param cancel_error: XtCancelError 对象   
:return:  

print(datetime.datetime.now(), sys._getframe().f_code.co_name)  

def on_order_stock_async_response(self, response):  

异步下单回报推送   
:param response: XtOrderResponse 对象   
:return:  

print(f"异步委托回调 {response.order_remark}")  

:param response: XtCancelOrderResponse 对象 :return:  

print(datetime.datetime.now(), sys._getframe().f_code.co_name)  

def on_account_status(self, status):""":param response: XtAccountStatus 对象:return:"""print(datetime.datetime.now(), sys._getframe().f_code.co_name)if __name__ == '__main__':print("start")#指定客户端所在路径,# 注意：如果是连接投研端进行交易，文件目录需要指定到f"{安装目录}\userdata"path = r'D:\qmt\sp3\迅投极速交易终端 睿智融科版\userdata_mini'# 生成session id 整数类型 同时运行的策略不能重复session_id = int(time.time())xt_trader = XtQuantTrader(path, session_id)# 开启主动请求接口的专用线程 开启后在on_stock_xxx 回调函数里调用XtQuantTrader.query_xxx 函数不会卡住回调线程，但是查询和推送的数据在时序上会变得不确定# 详见: http://docs.thinktrader.net/vip/pages/ee0e9b/#开启主动请求接口的专用线程# xt_trader.set_relaxed_response_order_enabled(True)# 创建资金账号为 800068 的证券账号对象acc = StockAccount('800068', 'STOCK')# 创建交易回调类对象，并声明接收回调callback = MyXtQuantTraderCallback()xt_trader.register_callback(callback)# 启动交易线程xt_trader.start()# 建立交易连接，返回0 表示连接成功connect_result = xt_trader.connect()print('建立交易连接，返回0 表示连接成功', connect_result)# 对交易回调进行订阅，订阅后可以收到交易主推，返回0 表示订阅成功subscribe_result = xt_trader.subscribe(acc)print('对交易回调进行订阅，订阅后可以收到交易主推，返回0 表示订阅成功',subscribe_result)  

# #定时判断实盘示例  

![](images/1522f86965861a1e1c343be57ca7b90d91edf7971fb4de856a57ad23eb6d598d.jpg)  

![](images/b4ab033063e80fca23e030ef8ab00516d44b964d03666265b76bd12acd143bf6.jpg)  

def on_cancel_error(self, cancel_error):  

撤单失败推送   
:param cancel_error: XtCancelError 对象   
:return:  

print(datetime.datetime.now(), sys._getframe().f_code.co_name)  

def on_order_stock_async_response(self, response):  

异步下单回报推送   
:param response: XtOrderResponse 对象   
:return:  

print(f"异步委托回调 {response.order_remark}")  

def on_cancel_order_stock_async_response(self, response): :param response: XtCancelOrderResponse 对象 :return:  

print(datetime.datetime.now(), sys._getframe().f_code.co_name)  

def on_account_status(self, status): :param response: XtAccountStatus 对象 :return:  

print(datetime.datetime.now(), sys._getframe().f_code.co_name)  

_name__ == main  

# print("start"  

# 指定客户端所在路径, 券商端指定到 userdata_mini 文件夹# 注意：如果是连接投研端进行交易，文件目录需要指定到f"{安装目录}\userdata"path = r'D:\qmt\投研\迅投极速交易终端睿智融科版\userdata'# 生成session id 整数类型 同时运行的策略不能重复session_id = int(time.time())xt_trader = XtQuantTrader(path, session_id)# 开启主动请求接口的专用线程 开启后在on_stock_xxx 回调函数里调用tQuantTrader.query_xxx 函数不会卡住回调线程，但是查询和推送的数据在时序上会变得不确  

![](images/9c6e813c5f6973244917e2d38499368aac2666bd3e353f38448d5e557b15fbc7.jpg)  

# 如果使用vscode pycharm 等本地编辑器 可以进入交互模式 方便调试 （把上一行的run_forever 注释掉 否则不会执行到这里）interact()  

# #交易接口重连  

该示例演示交易连接断开时重连的代码处理。  

# 提示  

1. 该示例不是线程安全的，仅演示断开连接时应该怎么处理重连代码，实际使用时请注意避免潜在的问题  
2. 本策略只用于提供策略写法及参考，若您直接进行实盘下单，造成损失本网站不负担责任。  

# python  

#本文用一个均线策略演示交易连接断开时怎么处理交易接口重连策略本身不严谨，不能作为实盘策略或者参考策略，本策略仅是演示重连用法  

mport time   
from xtquant.xttrader import XtQuantTrader, XtQuantTraderCallback   
rom xtquant.xttype import StockAccount   
rom xtquant import xtconstant   
rom xtquant import xtdata  

class MyXtQuantTraderCallback(XtQuantTraderCallback): # 更多说明见  

http://dict.thinktrader.net/nativeApi/xttrader.html?id=I3DJ97#%E5%A7%94%E6%89%98xtor der  

def on_disconnected(self):  

连接断开 :return:  

print("connection lost, 交易接口断开，即将重连")   
global xt_trader   
xt_trader = None  

def on_stock_order(self, order): print(f'委托回报: 股票代码:{order.stock_code} 账号:{order.account_id}, 订单编 号:{order.order_id} 柜台合同编号:{order.order_sysid} \  

成交编号:{trade.traded_id} 成交数量:{trade.traded_volume} 委托数量:{trade.direction} ')  

def on_order_error(self, order_error):print(f"报单失败： 订单编号：{order_error.order_id} 下单失败具体信息:{order_error.error_msg} 委托备注:{order_error.order_remark}")  

def on_cancel_error(self, cancel_error):print(f"撤单失败: 订单编号：{cancel_error.order_id} 失败具体信息:{cancel_error.error_msg} 市场：{cancel_error.market}")  

def on_order_stock_async_response(self, response): print(f"异步下单的请求序号:{response.seq}, 订单编号：{response.order_id} ")  

def on_account_status(self, status): print(f"账号状态发生变化， 账号:{status.account_id} 最新状态：{status.status}")  

trader = XtQuantTrader(path, session_id,callback=MyXtQuantTraderCallback())   
trader.start()   
connect_result = trader.connect()   
trader.subscribe(xt_acc)   
return trader if connect_result == 0 else None  

def try_connect(xt_acc,path): session_id_range = [i for i in range(100, 120)] import random random.shuffle(session_id_range)  

# 遍历尝试session_id 列表尝试连接  

# print('连接失败，session_id:{}，继续尝试下一个id', session_id)continue  

print('所有id 都尝试后仍失败，放弃连接')return None  

ef get_xttrader(xt_acc,path): global xt_trader if xt_trader is None: xt_trader = try_connect(xt_acc,path) return xt_trader  

name_ == _main_  

# 注意实际连接XtQuantTrader 时不要写类似while True 这种无限循环的尝试，因为每次连接都会用session_id 创建一个对接文件，这样就会占满硬盘导致电脑运行异常# 要控制session_id 在有限的范围内尝试，这里提供10 个session_id 供重连尝试# 当所有session_id 都尝试后，程序会抛出异常。实际使用过程中当session_id 用完时，可以增加邮件等通知方式提醒人工处理  

path = 'E:\qmt\\userdata_mini'   
xt_trader = None   
xt_acc = StockAccount('2000204')   
xt_trader = get_xttrader(xt_acc,path)   
if not xt_trader: raise Exception('交易接口连接失败')   
print('交易接口连接成功， 策略开始')   
stock = '513050.SH'   
xtdata.subscribe_quote(stock, '5m','','',count=-1)   
time.sleep(1)   
order_record = []   
while '093000'<=time.strftime('%H%M%S')<'150000': time.sleep(3) xt_trader = get_xttrader(xt_acc,path) price = xtdata.get_market_data_ex(['close'],[stock],period='5m',)[stock] #计算均线 ma5 = price['close'].rolling(5).mean() ma10 = price['close'].rolling(10).mean()  

![](images/f5b65cf1ed937a4b16a04eeb4d4b6d3c6e98694512da7670eaebe28f957a587e.jpg)  

# #指定session id 范围连接交易  

该示例演示指定session 重试连接次数的代码处理。  

python  

![](images/af79f470a7aa23fa5163b3059bf79e9e0acb162f501d1a4f0b518f8ecbd9bdab.jpg)  

![](images/1b0a374daac7b108e59c00af146a9db7dfd1be67aaa3c73f28cd6033ce4d78bd.jpg)  

# #信用账号执行还款  

本示例用于展示如何使用xtquant 库对信用账号执行还款的操作  

# 提示  

本策略只用于提供策略写法及参考，若您直接进行实盘下单，造成损失本网站不负担责任。  

![](images/6d751199bbada12683490005d5f7fb6b0457dda1e3d2857dee3ea3f1e671628a.jpg)  

成交变动推送 :param trade: XtTrade 对象 :return: """ print("on trade callback") print(trade.account_id, trade.stock_code, trade.order_id) def on_order_error(self, order_error): """ 委托失败推送 :param order_error:XtOrderError 对象 :return: """ print("on order_error callback") print(order_error.order_id, order_error.error_id, order_error.error_msg) def on_cancel_error(self, cancel_error): 撤单失败推送 :param cancel_error: XtCancelError 对象 :return: """ print("on cancel_error callback") print(cancel_error.order_id, cancel_error.error_id, cancel_error.error_msg) def on_order_stock_async_response(self, response): """ 异步下单回报推送 :param response: XtOrderResponse 对象 :return: """ print("on_order_stock_async_response") print(response.account_id, response.order_id, response.seq) def on_account_status(self, status): :param response: XtAccountStatus 对象 :return: """ print("on_account_status") print(status.account_id, status.account_type, status.status) __name__ == "__main__": print("demo test")  

![](images/a300e7548746efa34c913f3371c528d14e3a6d658177067815ca34854bac2382.jpg)  

# #下单后通过回调撤单  

![](images/979de8600ce2bdf1237e0d3ba22411c32f20d0b96fd4b5d4e5c86180604e21b1.jpg)  

![](images/8cae5ba706d7ef7f7e56c4444c91443f26f4167580badf8c02e53bc469e05ef4.jpg)  

委托信息 ===== ===== 账号类型: {order.account_type}, 资金账号: {order.account_id}, 证券代码: {order.stock_code}, 订单编号: {order.order_id}, 柜台合同编号: {order.order_sysid}, 报单时间: {order.order_time}, 委托类型: {order.order_type}, 委托数量: {order.order_volume}, 报价类型: {order.price_type}, 委托价格: {order.price}, 成交数量: {order.traded_volume}, 成交均价: {order.traded_price}, 委托状态: {order.order_status}, 委托状态描述: {order.status_msg}, 策略名称: {order.strategy_name}, 委托备注: {order.order_remark}, 多空方向: {order.direction}, 交易操作: {order.offset_flag} """) if order.strategy_name == strategy_name: # 该委托是由本策略发出 ssid = order.order_sysid status = order.order_status market = order.stock_code.split(".")[1] # print(ssid) if ssid and status in [50,55]: ## 使用cancel_order_stock_sysid_async 时，投研端market 参数可以填写为   
0，券商端按实际情况填写 print(xt_trade.cancel_order_stock_sysid_async(account,0,ssid)) def on_stock_trade(self, trade): """ 成交变动推送 :param trade: XtTrade 对象 :return: """ print(datetime.datetime.now(), '成交回调',   
trade.order_remark,trade.stock_code,trade.traded_volume,trade.offset_flag) def on_order_stock_async_response(self, response): 异步下单回报推送   
# 填投研端的userdata 路径,miniqmt 指定到userdata_mini   
xt_trade = xttrader.XtQuantTrader(r"C:\Program Files\测试1\迅投极速交易终端睿智融科版   
\userdata",int(time.time()))   
# 注册接受回调   
xt_trade.register_callback(callback)   
# 启动交易线程   
xt_trade.start()  

![](images/416f7b46266e9f0d6e2a764a3c4bf459b41514988ed5b6fdf5d6000edd6bd263.jpg)  

![](images/d567ca3c149739edbd7272d155513fc96599762b960e43fce257e41b149af11d.jpg)  

上次更新: 2024/12/30 17:24:22  

1、目前xtquant 支持的python 版本为 64 位python3.6----3.11，请使用支持的python 版本重试  

#连接 xtquant 时失败，返回-1 及解决方法  

1. 客户端是否以极简模式登录（登录qmt 系统时需要勾选极简模式）  

2. 检查路径是否正确  

miniqmt：路径指定到安装目录下\userdata_mini 文件夹投研端：路径指定到安装目录下\userdata 文件夹  

3. 客户端安装在C 盘的话，每次都需要用管理员权限运行策略，才能正常连接，否则有权限问题。  

# 提示  

不建议安装在C 盘。  

可以通过以下测试来验证是否有写入权限  

ile_path = r"d:\qmt\userdata_mini\example.txt"  # 设置文件路径和名称使用open 函数创建文件，并指定写入模式("w"表示写入模式)  
with open(file_path, "w") as file:file.write("123")  # 向文件写入内容  

如果出现PermissionError，则说明存在文件权限问题  

4. 路径正确时换个session（任意整数即可）  

提示  

由于机制限制，同一个session 的两次python 进程 connect 之间必须超过3秒钟  

5. 以上方法都不行，就是QMT 用户权限问题#执行xtdatacenter.init 时提示监听58609 端口失败说明当前环境的58609 端口被其他程序占用,通常是启动了两个xtdc 服务导致的  

方法1. 可用通过指定xtdc.init(False)后,使用xtdc.listen(port)指定自己需要的端口  

from xtquant import xtdatacenter as xtdc   
xtdc.set_token("这里输入token")   
xtdc.init(False)   
port = 58601   
xtdc.listen(port=port)   
print(f"服务启动,开放端口：{port}")  

方法2. 关闭所有py 程序，或重启电脑，再执行xtdc.init  

# #下单后，查询委托的投资备注只有前半部分  

极简客户端的order_remark 字段有长度限制，最大 24 个英文字符(一个中文占3个)， 超出的部分会丢弃。大qmt 没有长度限制。  