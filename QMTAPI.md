# 逐 K 线驱动 （handlebar） 示例  

回测示例-基于 handlebar  

#coding:gbk  

#导入常用库  
import pandas as pd  
import numpy as np  
import talib  
#示例说明：本策略，通过计算快慢双均线，在金叉时买入，死叉时做卖出 点击回测运行 主  
图选择要交易的股票品种  

def init(C):#init handlebar 函数的入参是ContextInfo 对象 可以缩写为C#设置测试标的为主图品种C.stock $=$ C.stockcode $+$ '.' $+{\mathsf{C}}.$ market#line1 和line2 分别为两条均线期数C.line1 $=\!10$ #快线参数C.line $_{2=20}$ #慢线参数#accountid 为测试的ID 回测模式资金账号可以填任意字符串C.accountid $=$ "testS"  

def handlebar(C):  

#当前k 线日期 bar_date $=$ timetag_to_datetime(C.get_bar_timetag(C.barpos), '%Y%m%d%H%M%S') #回测不需要订阅最新行情使用本地数据速度更快 指定subscribe 参数为否. 如果回测   
多个品种 需要先下载对应周期历史数据 local_data $=$ C.get_market_data_ex(['close'], [C.stock], end_time $=$ bar_date, period $=$   
C.period, count $=$ max(C.line1, C.line2), subscribe $=$ False) close_list $=$ list(local_data[C.stock].iloc[:, 0]) #将获取的历史数据转换为DataFrame 格式方便计算 #如果目前未持仓，同时快线穿过慢线，则买入8 成仓位 if len(close_list) ${<}1$ : print(bar_date, '行情不足 跳过') line1_mean $=$ round(np.mean(close_list[-C.line1:]), 2) line2_mean $=$ round(np.mean(close_list[-C.line2:]), 2) print(f"{bar_date} 短均线{line1_mean} 长均线{line2_mean}") account $=$ get_trade_detail_data('test', 'stock', 'account') account $=$ account[0] available_cash $=$ int(account.m_dAvailable) holdings $=$ get_trade_detail_data('test', 'stock', 'position') holdings $=$ {i.m_strInstrumentID $+$ '.' $^+$ i.m_strExchangeID : i.m_nVolume for i in holdings}   
holding_vol $=$ holdings[C.stock] if C.stock in holdings else 0   
if holding_vol $==0$ and line1_mean $>$ line2_mean: vol $=$ int(available_cash / close_list[-1] / 100) $\star$ 100 #下单开仓 passorder(23, 1101, C.accountid, C.stock, 5, -1, vol, C) print(f"{bar_date} 开仓") C.draw_text(1, 1, '开')   
#如果目前持仓中，同时快线下穿慢线，则全部平仓   
elif holding_vol $>0$ and line1_mean $<$ line2_mean: #状态变更为未持仓 C.holding $=$ False #下单平仓 passorder(24, 1101, C.accountid, C.stock, 5, -1, holding_vol, C) print(f"{bar_date} 平仓") C.draw_text(1, 1, '平')  

# 实盘示例-基于 handlebar  

#coding:gbk # 导入包 import pandas as pd import numpy as np import datetime  

11111I  
示例说明：双均线实盘策略，通过计算快慢双均线，在金叉时买入，死叉时做卖出  
1  
class a():pass  
$\mathsf{A}=\mathsf{a}()$ #创建空的类的实例 用来保存委托状态  

def init(C):A.stock $=$ C.stockcode $^+$ '.' $+$ C.market #品种为模型交易界面选择品种A.acct $\equiv$ account #账号为模型交易界面选择账号A.acct_type $=$ accountType #账号类型为模型交易界面选择账号A.amount $=10000$ #单笔买入金额 触发买入信号后买入指定金额A.line1 $=\!17$ #快线周期A.line $\scriptstyle2=27$ #慢线周期A.waiting_list $=[]$ #未查到委托列表 存在未查到委托情况暂停后续报单 防止超单A.buy_code $=23$ if A.acct_type $==$ 'STOCK' else 33 #买卖代码 区分股票 与 两融账号  

A.sell_code $=24$ if A.acct_type $==$ 'STOCK' else 34print(f'双均线实盘示例{A.stock} {A.acct} {A.acct_type} 单笔买入金额{A.amount}')  

def handlebar(C): #跳过历史k 线 if not C.is_last_bar(): return now $=$ datetime.datetime.now() now_time $=$ now.strftime('%H%M%S') # 跳过非交易时间 if now_time $<\,^{\prime}093000^{\prime}$ or now_time $>$ "150000": return account $=$ get_trade_detail_data(A.acct, A.acct_type, 'account') if len(account) $\scriptstyle{\left|{=}{=}0\right.}$ : print(f'账号{A.acct} 未登录 请检查') return account $=$ account[0] available_cash $=$ int(account.m_dAvailable) #如果有未查到委托 查询委托 if A.waiting_list: found_list $=[]$ orders $=$ get_trade_detail_data(A.acct, A.acct_type, 'order') for order in orders: if order.m_strRemark in A.waiting_list: found_list.append(order.m_strRemark) A.waiting_list $=$ [i for i in A.waiting_list if i not in found_list] if A.waiting_list: print(f"当前有未查到委托 {A.waiting_list} 暂停后续报单") return holdings $=$ get_trade_detail_data(A.acct, A.acct_type, 'position') holdings $=$ {i.m_strInstrumentID $^+$ '.' $+$ i.m_strExchangeID : i.m_nCanUseVolume for i in   
holdings} #获取行情数据 data $=$ C.get_market_data_ex(["close"],[A.stock],period $=$ '1d',count $=$ max(A.line1,   
A.line2) $+1$ ) close_list $=$ data[A.stock].values if len(close_list) $<$ max(A.line1, A.line2) $+1$ : print('行情长度不足(新上市或最近有停牌) 跳过运行') return pre_line1 $=$ np.mean(close_list[-A.line1-1: -1]) pre_line2 $=$ np.mean(close_list[-A.line2-1: -1]) current_line1 $=$ np.mean(close_list[-A.line1:]) current_line2 $=$ np.mean(close_list[-A.line2:]) #如果快线穿过慢线，则买入委托 当前无持仓 买入  

vol $=$ int(A.amount / close_list[-1] $/\,100)\star\,100$ #买入数量 向下取整到100 的整数倍  

if A.amount $<$ available_cash and vol $>=100$ and A.stock not in holdings and pre_line1 $<$ pre_line2 and current_line1 $>$ current_line2:  

#下单开仓 ，参数说明可搜索PY 交易函数 passorder   
msg $=$ f"双均线实盘 {A.stock} 上穿均线 买入 {vol}股"   
passorder(A.buy_code, 1101, A.acct, A.stock, 14, -1, vol, '双均线实盘', 2 , msg, C)   
print(msg)   
A.waiting_list.append(msg)  

#如果快线下穿慢线，则卖出委托  

if A.stock in holdings and holdings[A.stock] $>$ 0 and pre_line1 $>$ pre_line2 and current_line1 $<$ current_line2:  

msg $=$ f"双均线实盘 {A.stock} 下穿均线 卖出 {holdings[A.stock]}股" passorder(A.sell_code, 1101, A.acct, A.stock, 14, -1, holdings[A.stock], '双均线实盘', 2 , msg, C)  

print(msg) A.waiting_list.append(msg)  

# 事件驱动 （subscribe） 示例  

# #实盘示例-基于 subscribe  

#coding:gbk class a():pass $\mathsf{A}=\mathsf{a}()$ A.bought_list $=$ [] account $=$ 'testaccount'  

def init(C):  

#下单函数的参数需要 ContextInfo 对象 在init 中定义行情回调函数 可以用到init 函数的入参 不用手动传入  

def callback_func(data): #print(data) for stock in data: current_price $=$ data[stock]['close'] pre_price $=$ data[stock]['preClose'] ratio $=$ current_price / pre_price - 1 print(stock, C.get_stock_name(stock), '当前涨幅', ratio) if ratio $>0$ and stock not in A.bought_list: msg $=$ f"当前涨幅 {ratio} 大于0 买入100 股" print(msg)  

#下单函数passorder 安全起见处于注释状态 需要实际测试下单交易时  

再放开  

#passorder(23, 1101, account, stock, 5, -1, 100, '订阅下单示例', 2, msg, C) A.bought_list.append(stock)  

for stock in stock_list: C.subscribe_quote(stock, period $=$ '1d', callback $=$ callback_func)  

# 定时任务 （run_time） 示例  

# #实盘示例-基于 run_time  

#coding:gbk import time, datetime  

class a(): pass $\mathsf{A}=\mathsf{a}()$  

def init(C): A.hsa $=$ C.get_stock_list_in_sector('沪深A 股') A.vol_dict $=\{\}$ for stock in A.hsa: A.vol_dict[stock] $=$ C.get_last_volume(stock) A.bought_list $=[]$ C.run_time("f", "1nSecond", "2019-10-14 13:20:00")  

def f(C): t0 = time.time() now $=$ datetime.datetime.now() full_tick $=$ C.get_full_tick(A.hsa) total_market_value $=0$ total_ratio $=0$ count $=0$ for stock in A.hsa: ratio $=$ full_tick[stock]['lastPrice'] / full_tick[stock]['lastClose'] - 1 if ratio $>0.09$ and stock not in A.bought_list: msg $=$ f"{now} {stock} {C.get_stock_name(stock)} 当前涨幅 {ratio} 大于 $5\%$ 买 入100 股" #下单示例 安全起见处于注释状态 需要实际测试下单时可以放开 #passorder(23, 1101, account, stock, 5, -1, 100, '示例策略', 2, msg, C) A.bought_list.append(stock) market_value $=$ full_tick[stock]['lastPrice'] $\star$ A.vol_dict[stock]  

total_ratio $+=$ ratio $\star$ market_value total_market_value $+=$ market_value count $+=1$ total_ratio $/\!=$ total_market_value total_ratio $\star=100$  

print(f'{now}  当前 A 股加权涨幅  {round(total_ratio, 2)}%  函数运行耗时{round(time.time()- t0, 5)}秒')  

# 关于ContextInfo  

由于底层机制的限制，ContextInfo 中存储的变量值将会回滚，即在对ContextInfo中的变量进行修改之后，在下一次handlebar 调用时，这些修改将不会保留。具体细节请参阅常见问题在新窗口打开。因此，在完全理解ContextInfo 机制之前，请避免在其中存储任何变量。  

# #推荐用法  

class $\mathsf{G}()$ : pass  

$\mathtt{g}=\mathsf{G}()$  

def init(ContextInfo): g.stock_list $=\lceil^{\prime}($ 00001.SZ']  

def handlebar(ContextInfo): g.stock_list.append('600000.SH')  

# 函数命名规则  

函数名以 get_ 开头的，表示数据来源于客户端内存函数名以 query_ 开头的，表示数据是向服务查询  

# #账号类型说明  

'FUTURE' - 期货账号  

'STOCK' - 股票账号  

'CREDIT' - 信用账号  

'FUTURE_OPTION' - 期货期权  

'STOCK_OPTION' - 股票期权  

'HUGANGTONG' - 沪港通'SHENGANGTONG' - 深港通  

# #symbol_code - 代码表示  

迅投代码(symbol_code)是迅投平台统一用于表示交易标的的代码 其格式为:交易标的代码.交易所代码,例如深圳证券交易所的平安银行,迅投代码为000001.SZ(不区分大小写)。代码表示可以在迅投研终端的行情列表或者按键精灵中查询。  

# 交易所代码  

目前迅投研支持国内12 个交易所,12 个交易所的代码缩写如下:  

# 交易所名称 迅投简称 显示后缀  

上海证券交易所 SH SH深圳证券交易所 SZ SZ北京证券交易所 BJ BJ香港证券交易所 HK HK沪港通 HGT HGT深港通 SGT SGT中国金融期货交易所 IF CFFEX上海期货交易所 SF SHFE大连商品交易所 DF DCE郑州商品交易所 ZF CZCE上海国际能源交易中心 INE INE广州期货交易所 GF GFEX  

# symbol 示例  

<html><body><table><tr><td>市场中文 名</td><td>市场 代码</td><td>示例代码</td><td>显示后 缀</td><td>证券简称</td></tr><tr><td>上交所</td><td>SH</td><td>600000.SH</td><td>SH</td><td>浦发银行</td></tr><tr><td>深交所</td><td>SZ</td><td>000001.SZ</td><td>SZ</td><td>平安银行</td></tr><tr><td>北交所</td><td>BJ</td><td>830779.BJ</td><td>BJ</td><td>武汉蓝电</td></tr><tr><td>中金所</td><td>IF</td><td>IC2311.IF</td><td>CFFEX</td><td>中证 500 指数 2023年11月期</td></tr><tr><td>上期所</td><td>SF</td><td>rb2311.SF</td><td>SHFE</td><td>货合约 螺纹钢 2023 年</td></tr><tr><td>大商所</td><td>DF</td><td>m2311.DF</td><td>DCE</td><td>11月期货合约 豆粕2023年11</td></tr><tr><td>郑商所</td><td></td><td></td><td>CZCE</td><td>月期货合约 玻璃 2023 年 5</td></tr><tr><td>上海国际</td><td>ZF</td><td>FG305.ZF</td><td></td><td>月期货合约 原油 2023 年11</td></tr><tr><td>能源交易 中心</td><td>INE</td><td>sc2311.INE</td><td>INE</td><td>月期货合约</td></tr><tr><td>广期所</td><td>GF</td><td>lc2405.GF</td><td>GFEX</td><td>碳酸锂2024年 05 月期货合约</td></tr></table></body></html>  

<html><body><table><tr><td>市场中文 名</td><td>市场 代码</td><td>示例代码</td><td>显示后 缀</td><td>证券简称</td></tr><tr><td rowspan="2">上证期权</td><td rowspan="2">SHO</td><td rowspan="2">10005334.SHO</td><td rowspan="2">SH</td><td>50ETF购12月</td></tr><tr><td>2650</td></tr><tr><td rowspan="2">深证期权</td><td rowspan="2">SZO</td><td rowspan="2">90002114.SZO</td><td rowspan="2">SZ</td><td>深证 100ETF 沽12</td></tr><tr><td>月2700</td></tr><tr><td>板块指数</td><td>BKZS</td><td>290001.BKZS</td><td>BKZS</td><td>工业品期货板块指 数</td></tr></table></body></html>  

# Tick - Tick 对象  

行情快照数据  

#get_market_data_ex/get_full_tick 返回对象：  

数据类字段名 含义型time int 时间戳stime string 时间戳字符串形式lastPrice float 最新价open float 开盘价high float 最高价low float 最低价lastClose float 前收盘价amount float 成交总额  

数据类字段名 含义型volume int 成交总量（手）原始成交总量(未经过股手转换的成交总量)【不pvolume int推荐使用】stockStatus int 证券状态若是股票，则openInt 含义为股票状态，非股票openInterest int 则是持仓量openInt 字段说明在新窗口打开  
transactionNum float 成交笔数(期货没有，单独计算)  
lastSettlementPrice float 前结算(股票为0)  
settlementPrice float 今结算(股票为0)askPrice list[float] 多档委卖价askVol list[int] 多档委卖量bidPrice list[float] 多档委买价bidVol list[int] 多档委买量  

# 交易类  

# #Account - 账户对象  

字段名 数据类 解释型m_strAccountID str 资金账号，用于识别不同的资金账户m_nBrokerType int 账号类型，表示账号的具体种类m_dMaxMarginRate float 保证金比率，通常用于期货账号  

# 字段名  

<html><body><table><tr><td></td><td>型</td><td>冻结保证金，指投资者在交易中被冻结的保</td></tr><tr><td>m_dFrozenMargin</td><td>float</td><td>证金金额</td></tr><tr><td>m_dFrozenCash</td><td>float</td><td>冻结金额，指投资者在交易中被冻结的资金 金额</td></tr><tr><td>m_dFrozenCommission</td><td>float</td><td>冻结手续费，指投资者在交易中被冻结的手 续费金额</td></tr><tr><td>m_dRisk</td><td>float</td><td>风险度，指投资者账户的风险程度</td></tr><tr><td>m_dNav</td><td>float</td><td>单位净值，用于表示基金的净值</td></tr><tr><td>m_dPreBalance</td><td>float</td><td>期初权益，指期初时账户的资金金额</td></tr><tr><td>m_dBalance</td><td>float</td><td>总资产，表示账户的总资金金额</td></tr><tr><td>m_dAvailable</td><td>float</td><td>可用金额，指账户中可用于交易和提取的资 金金额</td></tr><tr><td>m_dCommission</td><td>float</td><td>手续费 (I旧版本为 m_dComission)</td></tr><tr><td>m_dPositionProfit</td><td>float</td><td>持仓盈亏，指当前持有的证券或期货合约的 盈亏金额</td></tr><tr><td>m_dCloseProfit</td><td>float</td><td>平仓盈亏,在期货交易中表示已经平仓的交 易的盈亏金额</td></tr><tr><td>m_dCashln</td><td>float</td><td>出入金净值，表示账户中出入金的净额</td></tr><tr><td>m_dCurrMargin</td><td>float</td><td>当前使用的保证金金额</td></tr><tr><td>m_dlnitBalance</td><td>float</td><td>初始权益，指账户初始时的权益金额</td></tr><tr><td>m_strStatus</td><td>str</td><td>状态，表示账户的当前状态</td></tr><tr><td>m_dlnitCloseMoney</td><td>float</td><td>期初平仓盈亏，指账户初始时的平仓盈亏金 额</td></tr><tr><td>m_dlnstrumentValue</td><td>float</td><td>总市值，表示持有的证券或期货合约的总市 值</td></tr></table></body></html>  

# 字段名  

m_dDeposit  
m_dWithdraw  
m_dPreCredit  
m_dPreMortgage  
m_dMortgage  
m_dCredit  
m_dAssetBalance  
m_strOpenDate  
m_dFetchBalance  
m_strTradingDate  
m_dStockValue  
m_dLoanValue  
m_dFundValue  
m_dRepurchaseValue  
m_dLongValue  
m_dShortValue  
m_dNetValue  
float 入金，指账户中的入金金额  
float 出金，指账户中的出金金额  
float 上次信用额度，用于表示上次的信用额度  
float 上次质押，指上次的质押金额  
float 质押，指当前的质押金额  
float 信用额度，表示账户的信用额度  
float 证券初始资金，表示股票账户的初始资金  
str 起始日期，表示账户的起始日期  
float 可取金额，指账户中可取出的金额  
str 交易日，表示当前的交易日期股票总市值，表示股票账户中持有的股票的  
float总市值债券总市值，表示账户中持有的债券的总市  
float值基金总市值，包括ETF 和封闭式基金在内的  
float基金的总市值回购总市值，表示账户中持有的所有回购交  
float易的总市值多单总市值，指现货账户中多单持仓的总市  
float值空单总市值，指现货账户中空单持仓的总市  
float值净持仓总市值，指现货账户中多单总市值减  
float去空单总市值的差额  
float 净资产，表示账户的净资产金额  

#  

字段名 解释型  
m_dTotalDebit float 总负债，表示账户的总负债金额  
m_dEntrustAsset float 可信资产，用于校对账户资金的准确性总市值（人民币），指沪港通账户中的持仓  
m_dInstrumentValueRMB float证券的总市值  
m_dSubscribeFee float 申购费，指申购基金时支付的费用库存市值，表示黄金现货账户中黄金库存的  
m_dGoldValue float市值现货冻结，表示黄金现货账户中被冻结的黄  
m_dGoldFrozen float金金额  
m_dMargin float 占用保证金，用于维持保证金  
m_strMoneyType str 币种，表示账户的资金所使用的货币种类  
m_dPurchasingPower float 购买力，指账户可用于购买投资品的金额原始保证金，指期货账户中的原始保证金金  
m_dRawMargin float额买入待交收金额（元），指账户中买入股票  
m_dBuyWaitMoney float但尚未交收的金额卖出待交收金额（元），指账户中卖出股票  
m_dSellWaitMoney float但尚未交收的金额本期间应计利息，指账户本期间内应计的利  
m_dReceiveInterestTotal float息金额权利金收支，指期货期权交易中的权利金收  
m_dRoyalty float支金额冻结权利金，指期货期权交易中被冻结的权  
m_dFrozenRoyalty float 利金金额实时占用保证金，用于股票期权交易中表示  
m_dRealUsedMargin float实时占用的保证金金额  

<html><body><table><tr><td>字段名</td><td>数据类 型</td><td>解释</td></tr><tr><td></td><td></td><td>实时风险度，用于股票期权交易中表示实时</td></tr><tr><td>m_dRealRiskDegree</td><td>float</td><td>的风险度</td></tr><tr><td></td><td></td><td></td></tr></table></body></html>  

# #Order - 委托对象  

<html><body><table><tr><td>字段</td><td>类型</td><td>解释</td></tr><tr><td>m_strAccountID</td><td>str</td><td>资金账号，账号，账号，资金账号</td></tr><tr><td>m_strExchangeID</td><td>str</td><td>证券市场</td></tr><tr><td>m_strExchangeName</td><td>str</td><td>交易市场</td></tr><tr><td>m_strProductID</td><td>str</td><td>品种代码</td></tr><tr><td>m_strProductName</td><td>str</td><td>品种名称</td></tr><tr><td>m_strlnstrumentID</td><td>str</td><td>证券代码</td></tr><tr><td>m_strlnstrumentName</td><td>str</td><td>证券名称，合约名称</td></tr><tr><td>m_strOrderRef</td><td>str</td><td>内部委托号，下单引用等于股票的内部委托 号</td></tr><tr><td>m_nOrderPriceType</td><td>int</td><td>EBrokerPriceType 类型，例如市价单、限价 单在新窗口打开</td></tr><tr><td>m_nDirection</td><td>int</td><td>EEntrustBS 类型，操作，多空，期货多空 股票买卖永远是 48，其他的dir同理</td></tr><tr><td>m_nOffsetFlag</td><td>int</td><td>EOffset_Flag_Type 类型，买卖/开平，用此字 段区分股票买卖，期货开、平仓，期权买卖 等</td></tr><tr><td>m_nHedgeFlag</td><td>int</td><td>EHedge_Flag_Type 类型，投保</td></tr><tr><td>m_dLimitPrice</td><td>float</td><td>委托价格，限价单的限价，即报价</td></tr><tr><td>m_nVolumeTotalOriginal</td><td>int</td><td>委托数量，最初的委托数量</td></tr><tr><td>m_nOrderSubmitStatus</td><td>int</td><td>EEntrustSubmitStatus 类型，报单状态，提</td></tr></table></body></html>  

# 字段  

# 交状态，股票中不需要报单状态  

m_strOrderSysID str 合同编号，委托号  
m_nOrderStatus int EEntrustStatus，委托状态  
m_nVolumeTraded int 成交数量，已成交量委托剩余量，当前总委托量，股票中表示总  
m_nVolumeTotal int委托量减去成交量  
m_nErrorID int 状态ID  
m_strErrorMsg str 状态信息  
m_nTaskId int 任务号  
m_dFrozenMargin float 冻结金额，冻结保证金  
m_dFrozenCommission float 冻结手续费  
m_strInsertDate str 委托日期，报单日期  
m_strInsertTime str 委托时间  
m_dTradedPrice float 成交均价（股票）  
m_dCancelAmount float 已撤数量  
m_strOptName str 买卖标记，展示委托属性的中文成交金额，期货的计算方式为均价乘以数量  
m_dTradeAmount float乘以合约乘数  
m_eEntrustType int EEntrustTypes，委托类别  
m_strCancelInfo str 废单原因  
m_strUnderCode str 标的证券代码  
m_eCoveredFlag int 备兑标记，'0’表示非备兑，'1’表示备兑  

# 字段  

m_dOrderPriceRMB float 委托价格（人民币），目前用于港股通  
m_dTradeAmountRMB float 成交金额（人民币），目前用于港股通  
m_dReferenceRate float 汇率，目前用于港股通  
m_strCompactNo str 合约编号  
m_eCashgroupProp int EXTCompactBrushSource 类型，头寸来源  
m_dShortOccupedMargin float 预估在途占用保证金，用于期权  
m_strXTTrade str 是否是迅投交易  
m_strAccountKey str 账号key，唯一区别不同账号的key  
m_strRemark str 投资备注  

# #Deal - 成交对象  

字段 数据 解释类型m_strAccountID str 资金账号m_strExchangeID str 证券市场m_strExchangeName str 交易市场m_strProductID str 品种代码m_strProductName str 品种名称m_strInstrumentID str 证券代码m_strInstrumentName str 证券名称m_strTradeID str 成交编号m_strOrderRef str 下单引用，等于股票的内部委托号m_strOrderSysID str 合同编号，报单编号，委托号  

# 字段  

# 解释  

EEntrustBS，买卖方向 对于股票该值始终是m_nDirection int48 在新窗口打开EOffset_Flag_Type，买卖/开平，用此字段区分m_nOffsetFlag int 股票买卖，期货开、平仓，期权买卖等在新窗口打开m_nHedgeFlag int EHedge_Flag_Type 类型，投保在新窗口打开m_dPrice float 成交均价m_nVolume int 成交量，期货单位手，股票做到股m_strTradeDate str 成交日期m_strTradeTime str 成交时间m_dCommission float 手续费 (旧版本为 m_dComission)m_dTradeAmount float 成交额，期货 $=$ 均价 \* 量 \* 合约乘数m_nTaskId int 任务号EBrokerPriceType 类型，例如市价单、限价单m_nOrderPriceType int 在新窗口打开m_strOptName str 买卖标记，展示委托属性的中文m_eEntrustType int EEntrustTypes，委托类别在新窗口打开EFutureTradeType 类型，成交类型在新窗口打m_eFutureTradeType int开EOffset_Flag_Type 类型，实际开平，主要是区m_nRealOffsetFlag int 分平今和平昨在新窗口打开ECoveredFlag 类型，备兑标记 '0' - 非备兑，m_eCoveredFlag int'1' - 备兑m_nCloseTodayVolume int 平今量，不显示m_dOrderPriceRMB float 委托价格（人民币），目前用于港股通  

类型m_dPriceRMB float 成交价格（人民币），目前用于港股通m_dTradeAmountRMB float 成交金额（人民币），目前用于港股通m_dReferenceRate float 汇率，目前用于港股通m_strXTTrade str 是否是迅投交易m_strCompactNo str 合约编号m_dCloseProfit float 平仓盈亏，目前用于外盘m_strRemark str 投资备注m_strAccountKey str 账号key，唯一区别不同账号的keym_nRef int 订单编号  

# #Position - 持仓对象  

# 字段名  

型 含义  
m_strAccountID string 资金账号  
m_strExchangeID string 证券市场  
m_strExchangeName string 市场名称  
m_strProductID string 品种代码  
m_strProductName string 品种名称  
m_strInstrumentID string 证券代码  
m_strInstrumentName string 证券名称EHedge_Flag_Type 类  
m_nHedgeFlag int适用在新窗口打开EEntrustBS，买卖方向  
m_nDirection int是48 在新窗口打开  

# 字段名  

# 数据类型  

string 开仓日期 股票此字段无效  
string 成交号，最初开仓位的成交  
int 当前拥股/持仓量持仓成本 ；持仓成本 $=$ (总买入金额  
float总卖出金额) / 剩余数量在实盘运行中是当前交易日，在回测中是  
string 股票最后交易过的日期使用的保证金，历史的直接用ctp 的，新  
float的自己用成本价存量系数算，股票不适用开仓成本，等于成本价\*第一次建仓的量，  
float 后续减持会影响，不算手续费，股票不适用  
float 最新结算价/当前价  
int 平仓量（对于股票不适用）  
float 平仓额（对于股票不适用）  
float 浮动盈亏  
float 平仓盈亏（对于股票不适用）  
float 市值/合约价值  
float 持仓成本（对于股票不适用）  
float 持仓盈亏（对于股票不适用）  
float 最新结算价（对于股票不适用）  
float 合约价值（对于股票不适用）  
bool 是否今仓  
string 股东账号  
m_strOpenDate  
m_strTradeID  
m_nVolume  
m_dOpenPrice  
m_strTradingDay  
m_dMargin  
m_dOpenCost  
m_dSettlementPrice  
m_nCloseVolume  
m_dCloseAmount  
m_dFloatProfit  
m_dCloseProfit  
m_dMarketValue  
m_dPositionCost  
m_dPositionProfit  
m_dLastSettlementPrice  
m_dInstrumentValue  
m_bIsToday  
m_strStockHolder  

# 字段名  

# 数据类型  

m_nFrozenVolume int 冻结数量  
m_nCanUseVolume int 可用余额  
m_nOnRoadVolume int 在途股份  
m_nYesterdayVolume int 昨夜拥股  
m_dLastPrice float 最新价/当前价  
m_dAvgOpenPrice float 开仓均价（对于股票不适用）  
m_dProfitRate float 盈亏比例EFutureTradeType 类型，成交类型在新窗  
m_eFutureTradeType int口打开  
m_strExpireDate string 到期日（针对逆回购）  
m_strComTradeID string 组合成交号  
m_nLegId int 组合序号  
m_dTotalCost float 累计成本（自定义，股票信用用到）  
m_dSingleCost float 单股成本（自定义，股票信用用  
m_nCoveredVolume int 备兑数量，用于个股期权持仓类型 ，用于个股期权，标记 '0' - 权  
m_eSideFlag int 利，'1' - 义务，'2' - '备兑'  
m_dReferenceRate float 汇率，目前用于港股通  
m_dStructFundVol float 分级基金可用（可分拆或可合并）  
m_dRedemptionVolume float 分级基金可赎回量申赎可用量（记录当日申购赎回的股票或  
m_nPREnableVolume int 基金数量）  
m_dRealUsedMargin float 实时占用保证金，用于期权  

段名 型 百Xm_dRoyalty float 权利金m_dStockLastPrice float 标的证券最新价，用于期权m_dStaticHoldMargin float 静态持仓占用保证金，用于期权m_nOptCombUsedVolume int 期权组合占用数量m_nEnableExerciseVolume int 能够行使的数量，用于个股期权m_strAccountKey string 账号key，唯一区别不同账号的key  

# #PositionStatistics - 持仓统计对象  

字段名 数据类型 描述m_strAccountID string 账号m_strExchangeID string 市场代码m_strExchangeName string 市场名称m_strProductID string 品种代码m_strInstrumentID string 合约代码m_strInstrumentName string 合约名称m_nDirection int 多空m_nHedgeFlag int 投保m_nPosition int 持仓m_nYestodayPosition int 昨仓m_nTodayPosition int 今仓m_nCanCloseVol int 可平m_dPositionCost float 持仓成本  

# 字段名  

# 数据类型  

m_dAvgPrice  
m_dPositionProfit  
m_dFloatProfit  
m_dOpenPrice  
m_dUsedMargin  
m_dUsedCommission  
m_dFrozenMargin  
m_dFrozenCommission  
m_dInstrumentValue  
m_nOpenTimes  
m_nOpenVolume  
m_nCancelTimes  
m_dLastPrice  
m_dRiseRatio  
m_strProductName  
m_dRoyalty  
m_strExpireDate  
m_dAssestWeight  
m_dIncreaseBySettlement  
m_dMarginRatio  
m_dFloatProfitDivideByUsedMar  
m_dFloatProfitDivideByBalance  
float 持仓均价  
float 持仓盈亏  
float 浮动盈亏  
float 开仓均价  
float 已使用保证金  
float 已使用的手续费  
float 冻结保证金  
float 冻结手续费  
float 市值，合约价值  
int 开仓次数  
int 总开仓量 中间平仓不减  
int 撤单次数  
float 最新价  
float 当日涨幅  
string 产品名称  
float 权利金市值  
string 到期日  
float 资产占比  
float 当日涨幅（结）  
float 保证金占比  
float 浮盈比例（保证金）  
float 浮盈比例（动态权益）  

字段名 数据类型 描述m_dTodayProfitLoss float 当日盈亏（结）m_nYestodayInitPosition int 昨日持仓m_dFrozenRoyalty float 冻结权利金m_dTodayCloseProfitLoss float 当日盈亏（收）m_dCloseProfit float 平仓盈亏m_strFtProductName string 品种名称m_dOpenCost float 开仓成本  

# PassorderArguments - 下单函数参数对象  

字段名 数据类型 解释opType int passorder 的opType 参数orderType int passorder 的orderType 参数accountID string 资金账号orderCode string 交易代码prType int passorder 的prType，价格类型  
modelPrice float 下单价格  
modelVolume int 下单量（手数或股数）  
strategyName string 策略名 _ &&& _ 投资备注  

# openInt - 证券状态  

状态  
码  
0,10 默认为未知  
1 停牌  
11 开盘前S  
12 集合竞价时段C  
13 连续交易T  
14 休市B  
15 闭市E  
波动性中断V,例如(10006742.SHO)50ETF 沽9 月2300 在2024/08/28  
16  
10:15:34 - 2024/08/28 10:18:34 触发熔断临时停牌，此时的openInt 值为16  
17 临时停牌P  
18 收盘集合竞价U  
19 盘中集合竞价M  
20 暂停交易至闭市N  
21 获取字段异常  
22 盘后固定价格行情  
23 盘后固定价格行情完毕  

# ContextInfo 对象  

ContextInfo 是策略运行环境对象，是 init, after_init, handlebar 等基本方法的入参，里面包括了终端自带的属性和方法。一般情况下不建议对ContextInfo  

添加自定义属性，ContextInfo 会随着bar 的切换而重置到上一根bar 的结束状态，建议用自建的全局变量来存储。详细说明请看这里在新窗口打开  

# #init - 初始化函数  

初始化函数，只在整个策略开始时调用运行到一次。用于初始订阅行情，订阅账号信息使用。init 函数执行完成前部分接口无法使用，如交易日获取函数get_trading_dates。  

系统函数 不可被手动调用  
参数：  


<html><body><table><tr><td>名称</td><td>类型</td><td>描述</td></tr><tr><td>Contextlnfo</td><td>object</td><td>策略运行环境对象，可以用于存储自定义的全局变量</td></tr></table></body></html>  

返回： 无  

# 示例：  

def init(ContextInfo): ContextInfo.initProfit $=0$  

# 在init 函数中订阅行情示例：  

python  

# #coding:gbk  

print(data) stock = '600000.SH' C.subscribe_quote(stock, period = '5m', callback = my_callback_function) #init 函数执行完成后 print('init 函数执行完成')  

# #after_init - 初始化后函数  

后初始化函数，在初始化函数执行完成后被调用一次。可以用于放置一次性触发的下单，取数据操作代码。  

系统会在init 函数执行完后和执行handlebar 之前调用after_init, 有些init 里不支持的函数比如ContextInfo.get_trading_dates 可以在after_init 里调用。  

参数：  

名称 类型 描述ContextInfo object 策略运行环境对象，可以用于存储自定义的全局变量  

返回： 无  

# 示例：  

python  

def init(ContextInfo): print('init')  

def after_init(ContextInfo):print('系统会在init 函数执行完后和执行handlebar 之前调用after_init')  

ef handlebar(ContextInfo): if ContextInfo.is_last_bar(): print('handlebar')  

after_init 函数中立刻下单示例：  

python  

![](images/a3142a02e8f703de0ca70555e981fcbc417bcfc8d39e872c05f293171810687e.jpg)  

# #handlebar - 行情事件函数  

系统函数 不可被手动调用  

释义： 行情事件函数，每根 K 线运行一次；实时行情获取状态下，先每根历史 K 线运行一次，再在每个 tick 数据来后驱动运行一次  

历史k 线上，按时间顺序每根K 线触发一次调用；盘中，每个新到达的TICK 数据驱动运行一次。可以作为行情驱动的函数，实现指标计算，回测，实盘下单的效果。  

# 参数：  

名称 类型 描述  

ContextInfo object 策略运行环境对象，可以用于存储自定义的全局变量  

返回： 无  

示例：  

def handlebar(ContextInfo):# 输出当前运行到的 K 线的位置print(ContextInfo.barpos)  

# #ContextInfo.schedule_run - 设置定时器  

# 说明  

1. 该函数是新版设置定时器函数，相比旧版run_time，新版schedule_run 新增了任务分组,任务取消等多种功能  

# 原型:  

python  

ContextInfo.schedule_run(func:Callable, # 回调函数，到达定时器预定时间时触发调用，参数为ContextInfo 类型，  
无需返回值，定义示例def on_timer(C:ContextInfo):time_point:Union[dt.datetime,str], # 表示预定的第一次触发时间，如果设置定时器时已经  
过了预定时间，会立即执行func 以及后续逻辑；当使用str 类型时，格式为  
'yyyymmddHHMMSS'如'20231231235959'，需要满足转换  
dt.datetime.strptime('20231231235959','%Y%m%d%H%M%S')repeat_times:int=0, # 表示在预定时间触发后按interval 间隔再触发多少次interval:datetime.timedelta=None, # 表示预定时间触发后的后续重复执行的时间间隔name:str='' # 定时器任务组名，可用于定时器分组，多次设置同名定时任务不会互相覆  
盖，会计入同一个任务组，按任务组名取消时会全部取消  

参数：  


<html><body><table><tr><td>名称</td><td>类型</td><td>描述</td></tr><tr><td>func</td><td>Callable</td><td>回调函数，到达定时器预定时间时触发调用， 参数为Contextlnfo类型，无需返回值，定义示 例 def on_timer(C:Contextlnfo): pass</td></tr><tr><td>time_poi</td><td>Union[datetime.date</td><td>表示预定的第一次触发时间，如果设置定时器 时已经过了预定时间，会立即执行func以及后 续逻辑；当使用str类型时，格式为 'yyyymmddHHMMSS'如'20231231235959'，需</td></tr><tr><td>nt</td><td>time,str]</td><td>要 满 足 转 换 datetime.datetime.strptime('20231231235959',' %Y%m%d%H%M%S)</td></tr><tr><td></td><td></td><td></td></tr><tr><td>repeat_ti mes</td><td>int</td><td>表示在预定时间触发后按interval间隔再触发 多少次，传-1表示不限制次数</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>描述</td></tr><tr><td>interval</td><td>datetime.timedelta</td><td>表示预定时间触发后的后续重复执行的时间间 隔</td></tr><tr><td></td><td></td><td>定时器任务组名，可用于定时器分组，多次设</td></tr><tr><td>name</td><td>str</td><td>置同名定时任务不会互相覆盖，会计入同一个 任务组，按任务组名取消时会全部取消</td></tr></table></body></html>  

回调函数参数： ContextInfo：策略模型全局对象  

# 返回值：  

int 类型，表示本次调用后生成的定时任务号，可用于取消本次定时任务，全局唯一不重复  

示例：  

python  

import datetime as dt   
def on_timer(C:ContextInfo): print('hello world')   
def init(ContextInfo): tid=ContextInfo.schedule_run(on_timer,'20231231235959',-   
1,dt.timedelta(minutes=1),'my_timer')   
def handlebar(ContextInfo): pass   
#此例为自2023-12-31 23:59:59 后每60s 运行一次on_timer  

#ContextInfo.cancel_schedule_run 取 消 由schedule_run 产生的定时任务  

原型：  

python  

ContextInfo.cancel_schedule_run( key:Union[seq:int,name:str] # 定时任务号或定时任务组名称  

参数：  

<html><body><table><tr><td>名称</td><td>类型</td><td>描述</td></tr><tr><td>key:</td><td>Union[seq:int,name:str]</td><td>类型为int时，表示按任务号取消;类型为str时 表示按任务组取消，会取消组内所有定时任务</td></tr></table></body></html>  

# 返回值：  

bool 类型，表示是否取消成功，即是否能按key 找到目标定时任务  

示例：  

示例  

ContextInfo.cancel_schedule_run('my_timer') #取消my_timer 任务组所有定时任务ContextInfo.cancel_schedule_run(1) #取消任务号为1 的定时任务  

# #ContextInfo.run_time - 设置定时器  

设置定时器函数，可以指定时间间隔，定时触发用户定义的回调函数。适用与在盘中，持续判断交易信号的模型。  

用法： ContextInfo.run_time(funcName,period,startTime) 定时触发指定的  

funcName 函数, funcName 函数由用户定义, 入参为ContextInfo 对象。  

# 参数：  

funcName：回调函数名  

period：重复调用的时间间隔,'5nSecond'表示每5 秒运行1 次回调函数,'5nDay'表示每5 天运行一次回调函数,'500nMilliSecond'表示每500 毫秒运行1 次回调函数  

startTime：表示定时器第一次启动的时间,如果要定时器立刻启动,可以设置历史的时间  

回调函数参数： ContextInfo：策略模型全局对象  

示例：  

python  

def init(ContextInfo):  

# 注意  

1. 模型回测时无效  

2. 定时器没有结束方法，会随着策略的结束而结束。  
3.  period 有nMilliSecond、nSecond 和Day 三个周期单元，部分周期下定时器函数在第一次运行之前会先等待一个period  

# #stop - 停止处理函数  

# 系统函数 不可被手动调用  

释义： PY 策略模型关闭停止前运行到的函数，复杂策略模型，如中间有起线程可通过在该函数内实现停止线程操作。注意, 当前版本stop 函数被调用时交易连接已断开, 不能在stop 函数中做报单 / 撤单操作.  

# 参数：  

<html><body><table><tr><td>名称</td><td>类型</td><td>描述</td></tr><tr><td></td><td></td><td></td></tr><tr><td>Contextlnfo</td><td>object</td><td>策略运行环境对象，可以用于存储自定义的全局变量</td></tr><tr><td></td><td></td><td></td></tr></table></body></html>  

示例：  

python  

def stop(ContextInfo): print( 'strategy is stop !')  

#ContextInfo.is_last_bar - 是否为最后一根K 线  

用法： ContextInfo.is_last_bar()  

释义： 判定是否为最后一根 K 线  

参数： 无  

返回： bool，返回值含义：True 是右侧最新k 线 False 不是最新k 线True：是False：否  

示例：  

pythonresult  

def handlebar(ContextInfo): print(ContextInfo.is_last_bar())  

#ContextInfo.is_new_bar - 判定是否为新的 K 线  

用法： ContextInfo.is_new_bar()  

释义： 某根 K 线的第一个 tick 数据到来时，判定该 K 线为新的 K线，其后的tick 不会认为是新的 K 线  

# 参数： 无  

返回： bool，返回值含义：  

True：是 False：否  

示例：  

pythonresult  

def handlebar(ContextInfo):print(ContextInfo.is_new_bar()) #历史k 线每根都是新k 线 盘中 每根新k 线第一个分笔返  
回True 其他分笔返回False  

# #ContextInfo.get_stock_name - 根据代码获取名称  

注意  
我们计划后续版本抛弃这个函数，不建议继续使用，可以用  
ContextInfo.get_instrument_detail("stockcode")["InstrumentName"]来实现同样  
功能  

用法： ContextInfo.get_stock_name('stockcode')  

释义： 根据代码获取名称  

参数： stockcode：股票代码，如'000001.SZ'，缺省值 ' ' 默认为当前图代码  

返回： string（GBK 编码）  

示例：  

示例返回值  

def handlebar(ContextInfo): print(ContextInfo.get_stock_name('000001.SZ'))  

#ContextInfo.get_open_date - 根据代码返回对应股票的上市时间  

用法： ContextInfo.get_open_date('stockcode')  

释义： 根据代码返回对应股票的上市时间  

参数： stockcode：股票代码，如'000001.SZ'，缺省值 ' ' 默认为当前图代码  

返回： number  

示例：  

pythonresult  

def init(ContextInfo): print(ContextInfo.get_open_date('000001.SZ'))  

# #ContextInfo.set_output_index_property - 设定指标绘制的属性  

# 用  

法： ContextInfo.set_output_index_property(index_name,draw_style $=$ 0,color='white',noaxis $=$ False,nodraw $\equiv$ False,noshow $\equiv$ False)  

释义： 设定指标绘制的属性，会最终覆盖掉指标对应的属性字段  

# 参数：  

index_name:string,指标名称，不可缺省draw_style,同paint 函数的drawstyle，可缺省默认为0color,同paint 函数的color，可缺省默认为'white'noaxis:bool,是否无坐标，可缺省默认为Falsenodraw:bool,是否不画线，可缺省默认为Falsenoshow:bool,是否不展示，可缺省默认为False  

返回： 无示例：  

pythonpythonresult  

def init(ContextInfo): ContextInfo.set_output_index_property('单位净值', nodraw = True)#使回测指标'单位净值'   
不画线  

# #create_sector - 创建板块  

用法： create_sector(parent_node,sector_name,overwrite)  

释义： 创建板块  

# 参数：  

parent_node：str，父节点，''为'我的'（默认目录）  
sector_name：str，要创建的板块名  
overwrite：bool，是否覆盖。如果目标节点已存在，为True 时跳过，为False 时在sector_name 后增加数字编号，编号为从1 开始自增的第一个不重复的值。  

返回： sector_name2：实际创建的板块名  

示例：  

# #create_sector_folder - 创建板块目录节点  

用法： create_sector_folder(parent_node,folder_name,overwrite)  

释义： 创建板块目录节点  

# 参数：  

parent_node：str，父节点，''为'我的'（默认目录）  
sector_name：str，要创建的节点名  
overwrite：bool，是否覆盖。如果目标节点已存在，为True 时跳过，为False 时在folder_name 后增加数字编号，编号为从1 开始自增的第一个不重复的值。返回： sector_name2：实际创建的节点名  

示例：  

pythonresult  

folder=create_sector_folder('我的','新建分类',False)  

#get_sector_list - 获取板块目录信息用法： get_sector_list(node)  

释义： 获取板块目录信息  

参数：  

node：str，板块节点名，''为顶层目录  

返回： info_list：[[s1,s2,...],[f1,f2,...]]s 为板块名，f 为目录节点名，例如[['我的自选'],['新建分类1']]  

# 示例：  

pythonresult  

get_sector_list('我的')  

#reset_sector_stock_list - 设置板块成分股  

用法： reset_sector_stock_list(sector,stock_list)  

释义： 设置板块成分股  

# 参数：  

sector：板块名 stock_list：list，品种代码列表，例如['000001.SZ','600000.SH']  

返回： result：bool，操作成功为True，失败为False  

示例：  

pythonresult  

reset_sector_stock_list('我的自选',['000001.SZ','600000.SH'])  

#remove_stock_from_sector - 移除板块成分股  

用法： remove_stock_from_sector(sector,stock_code)  

释义： 移除板块成分股  

# 参数：  

sector：板块名  

stock_code：品种代码，例如'000001.SZ'  

返回： result：bool，操作成功为True，失败为False  

示例：  

pythonresult  

remove_stock_from_sector('我的自选','000001.SZ')  

#add_stock_to_sector - 添加板块成分股  

用法： add_stock_to_sector(sector,stock_code)  

释义： 添加板块成分股  

# 参数：  

sector：板块名stock_code：品种代码，例如'000001.SZ'  

返回： result：bool，操作成功为True，失败为False  

示例：  

pythonresult  

add_stock_to_sector('我的自选','000001.SZ')  

# 数据下载  

#download_history_data - 下载指定合约代码指定周期对应时间范围的行情数据  

# 提示  

QMT 提供的行情数据中，基础周期包含 tick 1m 5m 1d，这些是实际用于存储的周期 其他周期为合成周期，以基础周期合成得到  

合成周期  

15m, 30m, $60\mathsf{m}$ 由5 分钟线合成  
1w（周线）, 1mon（月线）, 1y（年线） 由日线数据合成  

获取合成周期时  

如果取历史，需要下载历史的基础周期（如取15m 需要下载 $5\mathsf{m}$ ）如果取实时，可以直接订阅原始周期（如直接订阅 $15\mathsf{m}$ ）  

如果同时用到基础周期和合成周期，只需要下载基础周期,例如同时使用5m 和$15\mathsf{m}$ ，因为 $15\mathsf{m}$ 也是由5m 合成，所以只需要下载一次5m 的数据即可  

# 原型  

内置python  

download_history_data(stockcode,period,startTime,endTime)  

# 释义  

下载指定合约代码指定周期对应时间范围的行情数据  

# 参数  

<html><body><table><tr><td>字段名</td><td>数据类 型</td><td>解释</td></tr><tr><td>stockcode</td><td>string</td><td>股票代码，格式为'stkcode.market'，例如‘600000.SH'</td></tr><tr><td rowspan="4">period</td><td></td><td>K线周期类型，包括：</td></tr><tr><td>'tick'：分笔线 '1d'：日线</td><td></td></tr><tr><td>string</td><td>'1m'：分钟线</td></tr><tr><td>'5m'：5分钟线</td><td></td></tr><tr><td>startTime</td><td>string</td><td>可以为空</td><td></td></tr><tr><td>endTime</td><td>string</td><td>可以为空</td><td>结束时间，格式为“20200101”或“20200101093000"</td></tr></table></body></html>  

none  

# 示例  

示例  

# coding:gbk   
def init(C): download_history_data("000001.SZ","1d","20230101","") # 下载000001.SZ,从   
20230101 至今的日线数据   
def handlebar(C): return  

# #获取行情数据  

该目录下的函数用于获取实时行情,历史行情  

# #ContextInfo.get_market_data_ex - 获取行情数据  

# 注意  

1. 该函数不建议在init 中运行,在init 中运行时仅能取到本地数据  

2. 关于获取行情函数之间的区别与注意事项可在 - 常见问题-行情相关在新窗口打开 查看  
3. 除实时行情外，该函数还可用于获取特色数据，如资金流向数据,订单流数据等，获取方式见数据字典在新窗口打开  

原型  

内置python  

![](images/8ac3df29385fbba2c2115cd709f6a3a05adab7290563abf18d221be59502ff89.jpg)  

释义  

获取实时行情与历史行情数据  

field list 数据字段，详情见下方field 字段表  
stock_list list 合约代码列表数据周期，可选字段为:"tick""1m"：1 分钟线"5m"：5 分钟线； $"15\mathrm{m}"$ ：15 分钟线； $"30\mathrm{m}"$ ：30 分钟线"1h"小时线"1d"：日线"1w"：周线"1mon"：月线  
period str "1q"：季线"1hy"：半年线"1y"：年线'l2quote'：Level2 行情快照'l2quoteaux'：Level2 行情快照补充'l2order'：Level2 逐笔委托'l2transaction'：Level2 逐笔成交'l2transactioncount'：Level2 大单统计'l2orderqueue'：Level2 委买委卖队列数 据 起 始 时 间 ， 格 式 为 $\%\mathrm{Y}\%\mathrm{m}\%\mathrm{d}$   
start_time str或 $9/0\mathrm{Y}^{0}\!/\!0\mathrm{m}^{0}\!/\!0\mathrm{d}^{0}\!/\!0\mathrm{H}^{0}\!/\!0\mathrm{M}^{0}\!/\!0\mathrm{S}$ ，填""为获取历史最早一天数 据 结 束 时 间 ， 格 式 为 $\%\mathrm{Y}\%\mathrm{m}\%\mathrm{d}$   
end_time str 或 $9/0\mathrm{Y}^{0}\!/\!0\mathrm{m}^{0}\!/\!0\mathrm{d}^{0}\!/\!0\mathrm{H}^{0}\!/\!0\mathrm{M}^{0}\!/\!0\mathrm{S}$ ，填""为截止到最新一天  
count int 数据个数除权方式,可选值为'none'：不复权'front':前复权  
dividend_type str'back':后复权'front_ratio': 等比前复权'back_ratio': 等比后复权  
fill_data bool 是否填充数据  

<html><body><table><tr><td>名称</td><td>类型</td><td>描述</td></tr><tr><td></td><td></td><td>订阅数据开关，默认为True， 设置为False时不做数据订阅，</td></tr><tr><td>subscribe</td><td>bool</td><td>只读取本地已有数据。</td></tr></table></body></html>  

field 字段可选：  

field 数据类型 含义  

time int 时间  
open float 开盘价  
high float 最高价  
low float 最低价  
close float 收盘价  
volume float 成交量  
amount float 成交额  
settle float 今结算  
openInterest float 持仓量  
preClose float 前收盘价  
suspendFlag int 停牌 1 停牌，0 不停牌  

period 周期为tick 时，field 字段可选:  

# field 数据类型 含义  

time int 时间lastPrice float 最新价lastClose float 前收盘价open float 开盘价field 数据类型 含义  

high float 最高价  
low float 最低价  
close float 收盘价  
volume float 成交量  
amount float 成交额  
settle float 今结算  
openInterest float 持仓量  
stockStatus int 停牌 1 停牌，0 不停牌  

period 周期为Level2 数据时，字段参考数据结构  

# 返回值  

返回dict { stock_code1 $:$ value1, stock_code2 : value2, ... }  
value1, value2, ... ：pd.DataFrame 数据集，index 为time_list，columns 为fields,  
可参考Bar 字段在新窗口打开  
各标的对应的DataFrame 维度相同、索引相同  

# 示例  

示例data1 返回值data2 返回值data3 返回值data4 返回值历史tick 期货五档盘口  

import pandas as pd import numpy as np  

def init(C):  

C.stock_list = ["000001.SZ","600519.SH", "510050.SH"]# 指定获取的标的C.start_time = "20230901"# 指定获取数据的开始时间C.end_time = "20231101"# 指定获取数据的结束时间  

def handlebar(C):  

# 获取多只股票，多个字段，一条数据 data1 = C.get_market_data_ex([],C.stock_list, period = "1d",count = 1) # 获取多只股票，多个字段，指定时间数据  

data2 = C.get_market_data_ex([],C.stock_list, period = "1d", start_time = C.start_time,  

![](images/816ad4b8323c5e446cc3ae4da2338e1ae2637aa8242400d12b485320f16d9765.jpg)  

# #ContextInfo.get_full_tick - 获取全推数据  

# 提示  

不能用于回测 只能取最新的分笔，不能取历史分笔  

# 原型  

内置python  

ContextInfo.get_full_tick(stock_code=[])  

# 释义  

获取最新分笔数据  

# 参数  

<html><body><table><tr><td>名称</td><td>类型</td><td>描述</td></tr><tr><td></td><td></td><td>合约代码列表，如[600000.SH"600036.SH]，不指定时为当前</td></tr><tr><td>stock_code</td><td>list[str]</td><td></td></tr><tr><td></td><td></td><td>主图合约。</td></tr></table></body></html>  

返回值 根据stock_code 返回一个dict，该字典的key 值是股票代码，其值仍然是一个dict，在该dict 中存放股票代码对应的最新的数据。该字典数据key 值参考tick 字段在新窗口打开  

示例  

示例返回值  

# coding:gbk   
import pandas as pd   
import numpy as np   
def init(C): C.stock_list = ["000001.SZ","600519.SH", "510050.SH"]   
def handlebar(C): tick = C.get_full_tick(C.stock_list) print(tick["510050.SH"])  

#ContextInfo.subscribe_quote - 订阅行情数据  

提示  

1. 该函数属于订阅函数，非VIP 用户限制订阅数量  

2. VIP 用户支持全推市场指定周期K 线  
3. VIP 用户权限请参考vip-行情用户优势对比  

原型  

内置python  

ContextInfo.subscribe_quote( stock_code, period='follow', dividend_type='follow', result_type='', callback=None)  

释义  

订阅行情数据,关于订阅机制请参考运行机制对比在新窗口打开  

<html><body><table><tr><td>字段名</td><td>数据类 型</td><td>解释</td></tr><tr><td>stockcode</td><td>string</td><td>股票代码，'stkcode.market'，如'600000.SH'</td></tr><tr><td>period</td><td>string</td><td>K线周期类型</td></tr><tr><td>dividend_type</td><td></td><td>除权方式,可选值为</td></tr><tr><td rowspan="6"></td><td rowspan="6">string</td><td>'none'：不复权</td></tr><tr><td>'front':前复权</td></tr><tr><td>'back':后复权</td></tr><tr><td>'front_ratio'：等比前复权</td></tr><tr><td>'back_ratio'：等比后复权</td></tr><tr><td>注意：分笔周期返回数据均为不复权</td></tr><tr><td rowspan="5">result_type</td><td></td><td>返回数据格式,可选范围：<br>'DataFrame'或”（默认）：</td></tr><tr><td></td><td>返回{code:data}，data 为 pd.DataFrame 数据集，index</td></tr><tr><td></td><td>为字符串格式的时间序列，columns为数据字段</td></tr><tr><td>string</td><td><br>'dict'：返回{code:{k1:v1,k2:v2,.)}，k为数据字段</td></tr><tr><td></td><td>名，v为字段值<br>'list'：返回 {code:{k1:[v1],k2:[v2]..)}，k为数据字段名，v为字段值</td></tr><tr><td></td><td>function</td><td></td></tr><tr><td>callback</td><td></td><td>指定推送行情的回调函数</td></tr></table></body></html>  

# 返回值  

int：订阅号，用于反订阅  

# 示例  

示例返回值  

conding = gbk  

def call_back(data):  

print(data)  

def init(C): C.subID = C.subscribe_quote("000001.SZ","1d", callback = call_back)   
def handlebar(C):  

# #ContextInfo.subscribe_whole_quote - 订阅全推数据  

提示  

内置python  

ContextInfo.subscribe_whole_quote(code_list,callback=None)  

释义订阅全推数据，全推数据只有分笔周期，每次增量推送数据有变化的品种  

参数  

<html><body><table><tr><td>字段名</td><td>数据类 型</td><td>解释</td></tr><tr><td>code_list</td><td>list[str..]</td><td>市场代码列表/品种代码列表，如 ['SH','SZ'] 或 '600000.SH' 000001.SZ'</td></tr><tr><td>callback</td><td>function</td><td>数据推送回调</td></tr></table></body></html>  

返回值int，订阅号，可用ContextInfo.unsubscribe_quote 做反订阅  

示例返回值  

![](images/db9b7e33915838ffef38a08ba8db7a2355cf308f2ea57ae7d60e45ef8288d4a3.jpg)  

# #ContextInfo.unsubscribe_quote - 反订阅行情数据  

原型  

内置pythonContextInfo.unsubscribe_quote(subId)  

释义  

反订阅行情数据，配合ContextInfo.subscribe_quote()或ContextInfo.subscribe_whole_quote()使用  

参数  

字段名 数据类型 解释subId int 行情订阅返回的订阅号  

# 示例  

示例  

# conding = gbk   
def call_back(data): print(data)   
def init(C): C.stock_list = ["000001.SZ","600519.SH", "510050.SH"] C.subID = C.subscribe_whole_quote(C.stock_list,callback=call_back)   
def handlebar(C): print("====== ===== print("C.subID: ",C.subID) if C.subID > 0: C.unsubscribe_quote(C.subID) # 取消行情订阅  

# #subscribe_formula - 订阅模型  

原型  

内置python  

subscribe_formula( formula_name,stock_code,period ,start_time="",end_time="",count=-1 ,dividend_type="none" ,extend_param={} ,callback=None)  

释义 订阅vba 模型运行结果，使用前要注意补充本地K 线数据或分笔数据  

参数  

<html><body><table><tr><td>字段名</td><td>类 型</td><td>描述</td></tr><tr><td>formula_name</td><td>str</td><td>模型名称名</td></tr><tr><td>stock_code</td><td>str</td><td>模型主图代码形式如'stkcode.market'，如'000300.SH'</td></tr><tr><td rowspan="2">period</td><td rowspan="2">str</td><td>K线周期类型，可选范围：'tick':分笔线，‘1d:日线，‘1m': 分钟线，'3m'三分钟线，‘5m'5分钟线，‘15m':15分钟线，</td></tr><tr><td>'30m*:30分钟线，‘1h':小时线，‘1w':周线，‘1mon':月线,</td></tr><tr><td>start_time</td><td>str</td><td>'1q':季线，‘1hy:半年线，‘1y:年线 模型运行起始时间，形如：20200101，默认为空视为最早</td></tr><tr><td>end_time</td><td>str</td><td>模型运行截止时间，形如：20200101'，默认为空视为最新</td></tr><tr><td>count</td><td>int</td><td>模型运行范围为向前count 根bar，默认为-1运行所 有bar</td></tr><tr><td>dividend_type</td><td>str</td><td>复权方式，默认为主图除权方式，可选范围：'none':不复 权，‘front':向前复权，‘back':向后复权，‘front_ratio'等比 向前复权，‘back_ratio':等比向后复权</td></tr><tr><td>extend_param</td><td>dict</td><td>模型的入参，形如{'a':1，'__basket':{0}</td></tr><tr><td>basket</td><td>dict</td><td>可选参数，组合模型的股票池权重，形如{600000.SH: 0.06, '000001.SZ': 0.01}</td></tr></table></body></html>  

# 返回值 分两块，  

subscribe_formula 返回模型的订阅号,可用于后续反订阅，失败返回 -1  
callback:o timelist： 数据时间戳o outputs：模型的输出值，结构为{变量名:值}  

# 示例  

示例  

def callback(data): print(data)  

![](images/faa3ad0532a46d2985d217715fb00bc896926c1107c21fb561209e4c10700e09.jpg)  

# #unsubscribe_formula - 反订阅模型  

原型  

内置python unsubscribe_formula(subID)  

释义 反订阅模型  

参数  

字段名 类型 描述subID int 模型订阅号  

返回值  

bool:反订阅成功为True，失败为False  

示例  

示例  

<html><body><table><tr><td>#encoding=gbk def callback(data):</td></tr><tr><td>print(data)</td></tr><tr><td></td></tr><tr><td>def init(ContextInfo): basket={</td></tr><tr><td></td></tr><tr><td></td></tr></table></body></html>  

![](images/686d418941feb51c69fc899379676a0ea823f5927962e8c813c2d5bc2a71fcf5.jpg)  

# #call_formula - 调用模型  

原型  

内置python  

call_formula(formula_name,stock_code,period,start_time="",end_time="",count=- 1,dividend_type="none",extend_param={})  

释义 获取vba 模型运行结果，使用前要注意补充本地K 线数据或分笔数据  

参数  

<html><body><table><tr><td>字段名</td><td>类 型</td><td>描述</td></tr><tr><td>formula_name</td><td>str</td><td>模型名称名</td></tr><tr><td>stock_code</td><td>str</td><td>模型主图代码形式如'stkcode.market'，如'000300.SH'</td></tr><tr><td rowspan="3">period</td><td rowspan="3">str</td><td>K线周期类型，可选范围：'tick':分笔线，‘1d:日线，'1m':</td></tr><tr><td>分钟线，'3m：三分钟线，'5m'5分钟线，‘15m:15分钟线，</td></tr><tr><td>'30m*:30分钟线，‘1h':小时线，'1w':周线，'1mon':月线， '1q':季线，‘1hy:半年线，‘1y:年线</td></tr><tr><td>start_time</td><td>str</td><td>模型运行起始时间，形如：20200101＇，默认为空视为最早</td></tr><tr><td>end_time</td><td>str</td><td>模型运行截止时间，形如:20200101'，默认为空视为最新</td></tr><tr><td>count</td><td>int</td><td>模型运行范围为向前count 根 bar，默认为-1 运行所</td></tr></table></body></html>  

<html><body><table><tr><td>字段名</td><td>类 型</td><td>描述</td></tr><tr><td rowspan="2">dividend_type</td><td rowspan="2">str</td><td>有bar 复权方式，默认为主图除权方式，可选范围：‘none:不复</td></tr><tr><td>权，‘front':向前复权，‘back':向后复权，‘front_ratio':等比 向前复权，back_ratio:：等比向后复权</td></tr><tr><td>extend_param</td><td>票 dict</td><td>模型的入参，{"模型名：参数名":参数值}例如在跑模型MA 时，{MA:n1:1};入参可以添加_basket:dict,组合模型的股 池 权 重 形 如 {'_basket':['600000.SH':0.06,'000001.SZ':0.01}，如果在跑 一个模型1的时候，模型1调用了模型2，如果只想修改 模型2的参数可以传{模型2:参数'参数值}</td></tr></table></body></html>  

返回值 返回：dict{ 'dbt':0,#返回数据类型，0:全部历史数据 'timelist':[...],#返回数据时间范围list, 'outputs':{'var1':[...],'var2':[...]}#输出变量名：变量值list }  

# 示例  

示例  

def handlebar(ContextInfo): basket={'600000.SH':0.06,'000001.SZ':0.01} argsDict={'a':100,'__basket':basket} modelRet=call_formula('单股模型示范','000300.SH','1d','20240101','20240201',-   
,"none",argsDict) print(modelRet)  

# #call_formula_batch - 批量调用模型  

原型  

内置python   
call_formula_batch(formula_names,stock_codes,period,start_time="",end_time="",count=-   
1,dividend_type="none",extend_params=[])  

释义 批量获取vba 模型运行结果，使用前要注意补充本地K 线数据或分笔数据  

参数  

<html><body><table><tr><td>字段名</td><td>类 型</td><td>描述</td></tr><tr><td>formula_names</td><td>list</td><td>包含要批量运行的模型名</td></tr><tr><td>stock_codes</td><td>list</td><td>包含要批量运行的模型主图代码形式'stkcode.market'，如 '000300.SH'</td></tr><tr><td>period</td><td>str</td><td>K线周期类型，可选范围：'tick':分笔线，'1d:日线，‘1m': 分钟线，'3m'三分钟线，'5m*:5分钟线，‘15m:15分钟线， '30m':30分钟线，‘1h':小时线，‘1w"周线，‘1mon':月线 '1q':季线，‘1hy:半年线，‘1y':年线</td></tr><tr><td>start_time</td><td>str</td><td>模型运行起始时间，形如：20200101，默认为空视为最早</td></tr><tr><td>end_time</td><td>str</td><td>模型运行截止时间，形如：20200101'，默认为空视为最新</td></tr><tr><td>count</td><td>int</td><td>模型运行范围为向前count 根 bar，默认为-1运行所 有bar</td></tr><tr><td>dividend_type</td><td>str</td><td>复权方式，默认为主图除权方式，可选范围：‘none'不复 权，‘front':向前复权，‘back':向后复权，‘front_ratio:等比 向前复权，‘back_ratio':等比向后复权</td></tr><tr><td>extend_params</td><td>list</td><td>包含每个模型的入参,{"模型名：参数名":参数值],例如在 跑模型MA时，{MA:n1:1};入参可以添加_basket:dict,组 合模型的股票池权重，形如 {'_basket':{'600000.SH':0.06,000001.SZ':0.01}}，如果在跑 一个模型1的时候，模型1调用了模型2，如果只想修改 模型2的参数可以传{模型2:参数：参数值}</td></tr></table></body></html>  

# 返回值  

dict 说明:formula:模型名stock:品种代码argument:参数result:dict 参考call_formula 返回结果  

示例  

def handlebar(ContextInfo): formulas=['testModel1','testModel2'] codes=['600000.SH','000001.SZ'] basket={'600000.SH':0.06,'000001.SZ':0.01} args=[{'a':100,'__basket':basket},{'a':200,'__basket':basket}] modelRet=call_formula_batch(formulas,codes,'1d',extend_params=args); print(modelRet)  

#ContextInfo.get_svol - 根据代码获取对应股票的内盘成交量  

原型  

内置pythonContextInfo.get_svol(stockcode)  

释义  

根据代码获取对应股票的内盘成交量  

参数  

<html><body><table><tr><td>字段名</td><td>数据类 型</td><td>解释</td></tr><tr><td></td><td></td><td>股票代码，如‘000001.SZ"，年 缺省值"，黑 默认为当前图代</td></tr><tr><td>stockcode</td><td>string</td><td>码</td></tr></table></body></html>  

返回值int:内盘成交量  

示例  

示例返回值  

<html><body><table><tr><td>#coding:gbk def init(C): pass</td></tr><tr><td>def handlebar(C): data = C.get_svol('000001.SZ')</td></tr></table></body></html>  

![](images/a0dd6e2e63db1aefc62730d8e27bb73b206a38cb69c4be0d4d30b1c70ba8aee5.jpg)  

释义根据代码获取对应股票的外盘成交量  

# 参数  

<html><body><table><tr><td>字段名</td><td>数据类 型</td><td>解释</td></tr><tr><td>stockcode</td><td>string</td><td>股票代码，如 ‘000001.SZ"，缺省值"，黑 默认为当前图代 码</td></tr></table></body></html>  

# 返回值  

int:外盘成交量  

示例 示例返回值 coding:gbk def init(C):  

def handlebar(C): data = C.get_bvol('000001.SZ') print(data)  

#ContextInfo.get_turnover_rate - 获取换手率  

提示  

使用之前需要下载财务数据(在财务数据下载中)以及日线数据如果不补充股本数据,将使用最新流通股本计算历史换手率,可能会造成历史换手率不正确  

原型  

内置python  

ContextInfo.get_turnover_rate(stock_list,startTime,endTime)  

释义获取换手率  

参数  

字段名 数据类型 解释stock_list list 股票列表，如['600000.SH','000001.SZ']startTime string 起始时间，如'20170101'endTime string 结束时间，如'20180101'  

返回值 pandas.Dataframe  

示例  

示例返回值 coding:gbk def init(C):  

def handlebar(C): data = C.get_turnover_rate(['000002.SZ'],'20170101','20170301') print(data)  

# #ContextInfo.get_longhubang - 获取龙虎榜数据  

原型  

内置pythonContextInfo.get_longhubang(stock_list, startTime, endTime)  

释义获取龙虎榜数据  

参数  

参数名称 类型 描述stock_list list 股票列表，如 ['600000.SH', '600036.SH']startTime str 起始时间，如 '20170101'endTime str 结束时间，如 '20180101'  

返回值  

格式为pandas.DataFrame:  

参数名称 数据类型 描述  
reason str 上榜原因  
close float 收盘价  
spreadRate float 涨跌幅  
TurnoverVolune float 成交量  
Turnover_Amount float 成交金额  
buyTraderBooth pandas.DataFrame 买方席位  
sellTraderBooth pandas.DataFrame 卖方席位buyTraderBooth 或 sellTraderBooth 包含字段：  

参数名称 数据类型 描述traderName str 交易营业部名称buyAmount float 买入金额buyPercent float 买入金额占总成交占比  

# 参数名称 数据类型 描述  

sellAmount float 卖出金额sellPercent float 卖出金额占总成交占比totalAmount float 该席位总成交金额rank int 席位排行direction int 买卖方向  

# 示例  

示例返回值  

![](images/6104ac3586c8cefc7fd2012ec0d279045d0e74230655d998ea046155d29ea1e4.jpg)  

# 获取财务数据  

获取财务数据前，请先通过界面端数据管理 - 财务数据下载  

![](images/7a4408834977bfe6d6347007b382dc9996478aa39f27c19ee66cc68303e77c98.jpg)  

# 提示  

财务数据接口通过读取下载本地的数据取数，使用前需要补充本地数据。除公告日期和报表截止日期为时间戳毫秒格式其他单位为元或 $\%$ ，数据主要包括资产负债表(ASHAREBALANCESHEET)、利润表（ASHAREINCOME）、现金流量表（ASHARECASHFLOW）、股本表（CAPITALSTRUCTURE）的主要字段数据以及经过计算的主要财务指标数据（PERSHAREINDEX）。建议使用本文档对照表中的英文表名和迅投英文字段，表名不区分大小写。  

# #ContextInfo.get_financial_data - 获取财务数据  

财务数据接口有两种用法，入参和返回值不同，具体如下  

#用法1  

原型  

内置python  

ContextInfo.get_financial_data(fieldList, stockList, startDate, enDate, report_type = 'announce_time')  

# 释义  

获取财务数据，方法1  

参数  


<html><body><table><tr><td>字段名</td><td>类型</td><td>释义与用例</td></tr><tr><td>fieldList</td><td>List （必</td><td>财报字段列表：「'ASHAREBALANCESHEET.fix_aSSets'，'利润表 净利润]</td></tr><tr><td>stockList</td><td>须) List （必</td><td>股票列表：['600000.SH'，'000001.SZ']</td></tr><tr><td></td><td>须)</td><td></td></tr><tr><td>startDate</td><td>Str(必</td><td>开始时间：'20171209＇</td></tr></table></body></html>  

<html><body><table><tr><td>字段名</td><td>类型</td><td>释义与用例</td></tr><tr><td rowspan="2">endDate</td><td>须)</td><td></td></tr><tr><td>Str(必 须)</td><td>结束时间：'20171212"</td></tr><tr><td rowspan="2">report_type</td><td>Str(可</td><td>报表时间类型，可缺省，默认是按照数据的公告期为区分取数</td></tr><tr><td>选)</td><td>据，设置为 'report_time'为按照报告期取数据， announce_time'为按照公告日期取数据</td></tr></table></body></html>  

# 提示  

选择按照公告期取数和按照报告期取数的区别：  

报告日期是指财务报告所覆盖的会计时间段，而公告日期是指公司向外界公布该报告的具体时间点  

若指定report_type 为report_time，则不会考虑财报的公告日期，可能会取到未  

# 来数据  

若指定report_type 为announce_time，则会按财报实际发布日期返回数据，不会  

# 取到未来数据  

例：  

# 返回值  

函数根据stockList 代码列表,startDate,endDate 时间范围，返回不同的的数据类型。如下：  

代码数 时间范返回类型量 围  
$\begin{array}{r l r}&{}&{=\mathsf{T}}\\ &{}&{=\mathsf{T}}\\ &{}&{\phantom{\Rightarrow}\mathsf{T}}\\ &{}&{\phantom{\Rightarrow}\mathsf{T}}\\ &{}&{\phantom{\Rightarrow}\mathsf{T}}\end{array}$ =1 pandas.Series (index $=$ 字段)$>1$ pandas.DataFrame (index $=$ 时间, columns $=$ 字段)$=1$ pandas.DataFrame (index $=$ 代码, columns $=$ 字段)>1 pandas.Panel (items $=$ 代码, major_axis $=$ 时间,  

minor_axis $=$ 字段)  

示例  

示例返回值   
# coding:gbk   
def init(C): pass   
def handlebar(C): #取总股本和净利润 fieldList = ['CAPITALSTRUCTURE.total_capital', '利润表.净利润'] stockList = ["000001.SZ","000002.SZ","430017.BJ"] startDate = '20171209' endDate = '20231204' data = C.get_financial_data(fieldList, stockList, startDate, endDate, report_type = 'report_time') print(data)  

#用法2原型  

内置python  

ContextInfo.get_financial_data(tabname, colname, market, code, report_type = 'report_time', barpos)  

与用法 1 可同时使用释义获取财务数据，方法2  

参数  

字段名 类型 释义与用例tabname Str （必 表名：'ASHAREBALANCESHEET'  

<html><body><table><tr><td>字段名</td><td colspan="2">类型</td><td>释义与用例</td></tr><tr><td></td><td>须) Str（必</td><td>字段名：'fix_assets'</td><td></td></tr><tr><td>colname</td><td>须)</td><td>Str（必</td><td></td></tr><tr><td>market</td><td>须)</td><td>Str（必</td><td>市场：'SH'</td></tr><tr><td>code</td><td>须)</td><td></td><td>代码：'600000＇ 报表时间类型，可缺省，默认是按照数据的公告期为区分取</td></tr><tr><td>report_type</td><td>Str（可 选）</td><td></td><td>数据，设置为'report_time’为按照报告期取数据，‘ announce_time’为按照公告日期取数据</td></tr><tr><td>barpos</td><td>number</td><td></td><td>当前bar 的索引</td></tr></table></body></html>  

# 返回值  

float ：所取字段的数值  

# 示例  

示例返回值  

def init(C):  

index = C.barpos   
data = C.get_financial_data('ASHAREBALANCESHEET', 'fix_assets', 'SH', '600000', index)   
print(data)  

#ContextInfo.get_raw_financial_data - 获取原始财务数 据  

# 提示  

取原始财务数据,与get_financial_data 相比不填充每个交易日的数据  

原型  

内置python   
ContextInfo.get_raw_financial_data(fieldList,stockList,startDate,endDate,report_type='announce_t   
ime')  

释义  

取原始财务数据,与get_financial_data 相比不填充每个交易日的数据  

# 参数  

<html><body><table><tr><td>字段名</td><td>类型</td><td>释义与用例</td></tr><tr><td>fieldList</td><td>List （必 须)</td><td>字段列表：例如【资产负债表.固定资产，利润表.净利润]</td></tr><tr><td>stockList</td><td>List （必 须)</td><td>股票列表：例如['600000.SH',000001.SZ’]</td></tr><tr><td>startDate</td><td>Str(必 须)</td><td>开始时间：例如'20171209'</td></tr><tr><td>endDate</td><td>Str(必 须)</td><td>结束时间：例如'20171212'</td></tr><tr><td>report_type</td><td>Str（可 选）</td><td>时间类型，可缺省，默认是按照数据的公告期为区分取数 据，设置为‘report_time’为按照报告期取数据，可选 值:announce_time','report_time'</td></tr></table></body></html>  

# 返回值  

函数根据stockList 代码列表,startDate,endDate 时间范围，返回不同的的数据类型。如下：  

代码数 时间范返回类型量 围=1 $=1$ pandas.Series (index $=$ 字段)  

=1 $>1$ pandas.DataFrame (index $=$ 时间, columns $=$ 字段)   
$>\,1$ $=1$ pandas.DataFrame (index $=$ 代码, columns $=$ 字段) pandas.Panel (items $=$ 代码, major_axis $=$ 时间, >1 minor_axis $=$ 字段)  

# 示例  

# 示例返回值  

![](images/6910627533f3e193ae2fe028b42dc49f1a7c46a4556aefcc57741726af379485.jpg)  

# #ContextInfo.get_last_volume - 获取最新流通股本  

原型  

内置pythonContextInfo.get_last_volume(stockcode)  

# 释义  

获取最新流通股本  

参数  

字段名 数据类型 解释stockcode string 标的名称，必须是 'stock.market' 形式  

# 返回值  

int 类型值,代表流通股本数量  

# 示例  

示例返回值  

# coding:gbk   
def init(C): pass   
def handlebar(C): data = C.get_last_volume("000001.SZ") print(data)  

# #ContextInfo.get_total_share - 获取总股数  

获取总股数  

<html><body><table><tr><td>字段名</td><td>数据类 型</td><td>解释</td></tr><tr><td></td><td></td><td>股票代码， 缺省值 默认为当前图代码，如：</td></tr><tr><td>stockcode</td><td>string</td><td>600000.SH</td></tr><tr><td></td><td></td><td></td></tr></table></body></html>  

返回值  

示例返回值  

#财务数据字段表  

# 中文字段  

# 迅投字段  

可供出售金融资产   
持有至到期投资   
长期股权投资   
固定资产   
无形资产   
递延所得税资产   
资产总计   
交易性金融负债   
应付职工薪酬   
应交税费   
应付利息   
应付债券   
递延所得税负债   
负债合计   
实收资本(或股本)   
资本公积金   
盈余公积金   
未分配利润   
归属于母公司股东权益合   
少数股东权益   
负债和股东权益总计   
所有者权益合计   
fin_assets_avail_for_sale   
held_to_mty_invest   
long_term_eqy_invest   
fix_assets   
intang_assets   
deferred_tax_assets   
tot_assets   
tradable_fin_liab   
empl_ben_payable   
taxes_surcharges_payable   
int_payable   
bonds_payable   
deferred_tax_liab   
tot_liab   
cap_stk   
cap_rsrv   
surplus_rsrv   
undistributed_profit   
tot_shrhldr_eqy_excl_min_int   
minority_int   
tot_liab_shrhldr_eqy   
total_equity  

# 中文字段  

# 迅投字段  

货币资金   
应收票据   
应收账款   
预付账款   
其他应收款   
其他流动资产   
流动资产合计   
存货   
在建工程   
工程物资   
长期待摊费用   
非流动资产合计   
短期借款   
应付股利   
其他应付款   
一年内到期的非流动负债   
其他流动负债   
长期应付款   
应付账款   
预收账款   
流动负债合计   
应付票据   
cash_equivalents   
bill_receivable   
account_receivable   
advance_payment   
other_receivable   
other_current_assets   
total_current_assets   
inventories   
constru_in_process   
construction_materials   
long_deferred_expense   
total_non_current_assets   
shortterm_loan   
dividend_payable   
other_payable   
non_current_liability_in_one_year   
other_current_liability   
longterm_account_payable   
accounts_payable   
advance_peceipts   
total_current_liability   
notes_payable  

# 中文字段  

# 迅投字段  

长期借款 long_term_loans 专项应付款 grants_received 其他非流动负债 other_non_current_liabilities 非流动负债合计 non_current_liabilities 专项储备 specific_reserves 商誉 goodwill 报告截止日 m_timetag 公告日 m_anntime  

# #利润表 (ASHAREINCOME)  

# 中文字段  

# 迅投字段  

投资收益 plus_net_invest_inc 联营企业和合营企业的投资收益 incl_inc_invest_assoc_jv_entp 营业税金及附加 less_taxes_surcharges_ops 营业总收入 revenue 营业总成本 total_operating_cost 营业收入 revenue_inc 营业成本 total_expense 资产减值损失 less_impair_loss_assets 营业利润 oper_profit 营业外收入 plus_non_oper_rev 营业外支出 less_non_oper_exp  

# 中文字段  

# 迅投字段  

利润总额 tot_profit所得税 inc_tax净利润 net_profit_incl_min_int_inc归母净利润 net_profit_excl_min_int_inc管理费用 less_gerl_admin_exp销售费用 sale_expense财务费用 financial_expense综合收益总额 total_income归属于少数股东的综合收益总额 total_income_minority公允价值变动收益 change_income_fair_value已赚保费 earned_premium报告截止日 m_timetag公告日 m_anntime  

# #现金流量表 (ASHARECASHFLOW)  

# 中文字段  

# 迅投字段  

收到其他与经营活动有关的现金经营活动现金流入小计  
支付给职工以及为职工支付的现金支付的各项税费  
支付其他与经营活动有关的现金经营活动现金流出小计  

other_cash_recp_ral_oper_act stot_cash_inflows_oper_act cash_pay_beh_empl pay_all_typ_tax other_cash_pay_ral_oper_act stot_cash_outflows_oper_act  

# 中文字段  

# 迅投字段  

经营活动产生的现金流量净额  
取得投资收益所收到的现金  
处置固定资产、无形资产和其他长期投资收  
到的现金  
投资活动现金流入小计  
投资支付的现金  
购建固定资产、无形资产和其他长期投资支  
付的现金  
支付其他与投资的现金  
投资活动产生的现金流出小计  
投资活动产生的现金流量净额  
吸收投资收到的现金  
取得借款收到的现金  
收到其他与筹资活动有关的现金  
筹资活动现金流入小计  
偿还债务支付现金  
分配股利、利润或偿付利息支付的现金  
支付其他与筹资的现金  
筹资活动现金流出小计  
筹资活动产生的现金流量净额  
汇率变动对现金的影响  
现金及现金等价物净增加额  
销售商品、提供劳务收到的现金  
net_cash_flows_oper_act  
cash_recp_return_invest  
net_cash_recp_disp_fiolta  
stot_cash_inflows_inv_act  
cash_paid_invest  
cash_pay_acq_const_fiolta  
other_cash_pay_ral_inv_act  
stot_cash_outflows_inv_act  
net_cash_flows_inv_act  
cash_recp_cap_contrib  
cash_recp_borrow  
other_cash_recp_ral_fnc_act  
stot_cash_inflows_fnc_act  
cash_prepay_amt_borr  
cash_pay_dist_dpcp_int_exp  
other_cash_pay_ral_fnc_act  
stot_cash_outflows_fnc_act  
net_cash_flows_fnc_act  
eff_fx_flu_cash  
net_incr_cash_cash_equ  
goods_sale_and_service_render_cash  

# 中文字段  

# 迅投字段  

购买商品、接受劳务支付的现金处置子公司及其他收到的现金其中子公司吸收现金  

tax_levy_refund   
goods_and_services_cash_paid   
net_cash_deal_subcompany   
cash_from_mino_s_invest_sub   
fix_intan_other_asset_dispo_cash_payment   
m_timetag   
m_anntime  

处置固定资产、无形资产和其他长期资产支付的现金净额  

报告截止日公告日  

# #股本表 (CAPITALSTRUCTURE)  

迅投字段  

总股本 total_capital  
已上市流通A 股 circulating_capital  
自由流通股本 free_float_capital（旧版本为freeFloatCapital）  
限售流通股份 restrict_circulating_capital  
变动日期 m_timetag  
公告日 m_anntime  

# #主要指标 (PERSHAREINDEX)  

# 中文字段  

每股经营活动现金流量 s_fa_ocfps每股净资产 s_fa_bps基本每股收益 s_fa_eps_basic  

# 中文字段  

# 迅投字段  

稀释每股收益  
每股未分配利润  
每股资本公积金  
扣非每股收益  
净资产收益率  
销售毛利率  
主营收入同比增长  
净利润同比增长  
归属于母公司所有者的净利润同比增长  
扣非净利润同比增长  
营业总收入滚动环比增长  
归属净利润滚动环比增长  
扣非净利润滚动环比增长  
加权净资产收益率  
摊薄净资产收益率  
摊薄总资产收益率  
毛利率  
净利率  
实际税率  
预收款营业收入  
销售现金流营业收入  
资产负债比率  
s_fa_eps_diluted  
s_fa_undistributedps  
s_fa_surpluscapitalps  
adjusted_earnings_per_share  
du_return_on_equity  
sales_gross_profit  
inc_revenue_rate  
du_profit_rate  
inc_net_profit_rate  
adjusted_net_profit_rate  
inc_total_revenue_annual  
inc_net_profit_to_shareholders_annual  
adjusted_profit_to_profit_annual  
equity_roe  
net_roe  
total_roe  
gross_profit  
net_profit  
actual_tax_rate  
pre_pay_operate_income  
sales_cash_flow  
gear_ratio  

中文字段迅投字段  

# #十大股东/十大流通股东 (TOP10HOLDER/TOP10FLOWHOLDER)  

# 提示  

对于公告内披露的十大股东数量大于10 条的，我们会保留原始数据，以保持和公司公告信息一致  

中文字段 迅投字段公告日期 declareDate截止日期 endDate股东名称 name股东类型 type持股数量 quantity变动原因 reason持股比例 ratio股份性质 nature持股排名 rank  

# #股东数 (SHAREHOLDER)  

中文字段 迅投字段公告日期 declareDate截止日期 endDate股东总数 shareholder  

中文字段 迅投字段A 股东户数 shareholderAB 股东户数 shareholderBH 股东户数 shareholderH已流通股东户数 shareholderFloat未流通股东户数 shareholderOther  

# #获取合约信息  

#ContextInfo.get_instrument_detail - 根据代码获取合约详细信息  

# 提示  

旧版本客户端中，函数名为ContextInfo.get_instrumentdetail；不支持iscomplete 参数  

# 原型  

内置python  

ContextInfo.get_instrument_detail(stockcode,iscomplete = Fasle)  

释义根据代码获取合约详细信息  

参数  

字段名 数据类型 解释stockcode string 标的名称，必须是 'stock.market' 形式iscomplete bool 是否获取全部字段，默认为False  

# 返回值  

根据stockcode 返回一个dict。该字典数据key 值有：  

名称 类型 描述ExchangeID string 合约市场代码InstrumentID string 合约代码InstrumentName string 合约名称ProductID string 合约的品种ID(期货)ProductName string 合约的品种名称(期货)ProductType int 合约的类型, 默认-1,枚举值可参考下方说明ExchangeCode string 交易所代码UniCode string 统一规则代码CreateDate str 创建日期OpenDate str 上市日期（特殊值情况见表末）ExpireDate int 退市日或者到期日（特殊值情况见表末）PreClose float 前收盘价格SettlementPrice float 前结算价格UpStopPrice float 当日涨停价DownStopPrice float 当日跌停价流通股本（注意，部分低等级客户端中此字段为FloatVolume floatFloatVolumn）总股本（注意，部分低等级客户端中此字段为TotalVolume floatFloatVolumn）LongMarginRatio float 多头保证金率  

名称 类型 描述ShortMarginRatio float 空头保证金率PriceTick float 最小价格变动单位VolumeMultiple int 合约乘数(对期货以外的品种，默认是1)主力合约标记，1、2、3 分别表示第一主力合约，MainContract int第二主力合约，第三主力合约LastVolume int 昨日持仓量合约停牌状态( $<=\!0$ :正常交易（-1:复牌）; $\prime>=1$ 停InstrumentStatus int牌天数;)IsTrading bool 合约是否可交易IsRecent bool 是否是近月合约ChargeType int 期货和期权手续费方式ChargeOpen float 开仓手续费(率)ChargeClose float 平仓手续费(率)ChargeTodayOpen float 开今仓(日内开仓)手续费(率)ChargeTodayClose float 平今仓(日内平仓)手续费(率)OptionType int 期权类型OpenInterestMultiple int 交割月持仓倍数  

# 提示  

字段OpenDate 有以下几种特殊值： 19700101 $=$ 新股, 19700102 $=$ 老股东增发,19700103=新债, 19700104=可转债, 19700105=配股， 19700106=配号 字段ExpireDate 为0 或 99999999 时，表示该标的暂无退市日或到期日  

字段ProductType 对于股票以外的品种，有以下几种值国内期货市场： 1-期货 2-期权(DF SF ZF INE GF) 3-组合套利 4-即期 5-期转现6-期权(IF) 7-结算价交易(tas)  

\*\*沪深股票期权市场： $^{**}0.$ 认购 1-认沽  

外盘： 1-100：期货， 101-200：现货, 201-300:股票相关 1：股指期货 2：能源期货 3：农业期货 4：金属期货 5：利率期货 6：汇率期货 7：数字货币期货 99：自定义合约期货 107：数字货币现货 201：股票 202：GDR 203：ETF204：ETN 300：其他  

示例  

示例返回值  

def handlebar(C): data = C.get_instrumentdetail("000001.SZ") print(data)  

# #get_st_status - 获取历史st 状态  

提示  

本函数需要下载历史ST 数据(过期合约K 线),可通过界面端数据管理 - 过期合约数据下载  

原型  

内置python  

get_st_status(stockcode)  

释义  

获取历史st 状态  

# 参数  

<html><body><table><tr><td>字段名</td><td>数据类 型</td><td>解释</td></tr><tr><td>stockcode</td><td></td><td>股票代码，如000004.SZ 可为空，为空时取主图代</td></tr><tr><td></td><td>string</td><td>码)</td></tr></table></body></html>  

返回值  

st 范围字典 格式 {'ST': [['20210520', '20380119']], '\*ST': [['20070427','20080618'], ['20200611', '20210520']]}  

示例：  

示例  

示例返回值  

coding:gbk  

def init(C):  

#ContextInfo.get_his_st_data - 获取某只股票ST 的历史  

提示  

本函数需要下载历史ST 数据(过期合约K 线),可通过界面端数据管理 - 过期合约数据下载  

原型  

内置pythonContextInfo.get_his_st_data(stockcode)  

释义  

获取某只股票ST 的历史  

参数  

字段名 数据类型 解释  

stockcode string 股票代码，'stkcode.market'，如'000004.SZ'  

# 返回值  

dict,st 历史，key 为ST,\*ST,PT,历史未ST 会返回{}  

示例  

示例返回值  

coding:gbk  

def init(C):  

def handlebar(C):  

#ContextInfo.get_main_contract - 获取期货主力合约  

提示  

1. 该函数支持实盘/回测两种模式  
2. 若要使用该函数获取历史主力合约，必须要先下载历史主力合约数据  
3. 历史主力合约数据目前通过界面端数据管理 - 过期合约数据 - 历史主力合约下载  

# 原型  

内置python  

ContextInfo.get_main_contract(codemarket)  

ContextInfo.get_main_contract(codemarket,date="") ContextInfo.get_main_contract(codemarket,startDate="",endDate  

释义  

获取当前期货主力合约  

参数  

<html><body><table><tr><td>字段名</td><td>数据类 型</td><td>解释</td></tr><tr><td>codemarket</td><td>string</td><td>合约和市场，合约格式为品种名加OO，如IF00.IF znOo.SF</td></tr><tr><td>startDate</td><td>string</td><td>开始日期（可以不写）如20180608</td></tr><tr><td>endDate</td><td>string</td><td>结束日期(可以不写),如20190608</td></tr></table></body></html>  

# 返回值  

str，合约代码  

# 示例  

示例返回值  

# coding:gbk   
def init(C): pass   
def handlebar(C): symbol1 = C.get_main_contract('IF00.IF')# 获取当前主力合约 symbol2 = C.get_main_contract('IF00.IF',"20190101")# 获取指定日期主力合约 symbol3 = C.get_main_contract('IF00.IF',"20181101","20190101") # 获取时间段内全   
部主力合约 print(symbol1, symbol2) print("="\*10) print(symbol3)  

# #ContextInfo.get_contract_multiplier - 获取合约乘数  

原型  

内置pythonContextInfo.get_contract_multiplier(contractcode)  

释义  

获取合约乘数  

参数  

<html><body><table><tr><td>字段名</td><td>数据类型</td><td>解释</td></tr><tr><td>contractcode</td><td>string</td><td>合约代码，格式为 'code.market'，例如 IF1707.IF</td></tr></table></body></html>  

返回值int,表示合约乘数  

示例  

示例返回值  

# coding:gbk   
def init(C): pass   
def handlebar(C): multiplier = C.get_contract_multiplier("rb2401.SF") print(multiplier)  

#ContextInfo.get_contract_expire_date - 获取期货合约到期日  

释义获取期货合约到期日  

参数  

字段名 数据类型 解释Codemarket string 合约和市场,如IF00.IF,zn00.SF  

返回值str，合约到期日  

示例  

示例返回值  

# #ContextInfo.get_his_contract_list - 获取市场已退市合约  

原型  

内置python  

ContextInfo.get_his_contract_list(market)  

# 释义  

获取市场已退市合约，需要手动补充过期合约列表  

参数  

字段名 数据类型 解释market string 市场,SH,SZ,SHO,SZO,IF 等  

# 返回值  

list,合约代码列表  

# 示例  

示例返回值  

# coding:gbk   
def init(C): pass   
def handlebar(C): print(C.get_his_contract_list('SHO')[:30])  

# #获取期权信息  

# #ContextInfo.get_option_detail_data - 获取指定期权品种的详细信息  

原型  

内置python  

ContextInfo.get_option_detail_data(optioncode)  

# 释义  

获取指定期权品种的详细信息  

# 参数  

<html><body><table><tr><td>字段名</td><td>数据类 型</td><td>解释</td></tr><tr><td></td><td></td><td>期权代码，如'10001506.SHO，当填写空字符串时候默认为</td></tr><tr><td>optioncode</td><td>string</td><td>当前主图的期权品种</td></tr></table></body></html>  

返回值dict,字段如下：  

字段 类型 说明ExchangeID str 期权市场代码InstrumentID str 期权代码ProductID str 期权标的的产品IDOpenDate int 发行日期ExpireDate int 到期日PreClose float 前收价格SettlementPrice float 前结算价格UpStopPrice float 当日涨停价  

字段 类型 说明DownStopPrice float 当日跌停价LongMarginRatio float 多头保证金率ShortMarginRatio float 空头保证金率PriceTick float 最小变价单位VolumeMultiple int 合约乘数MaxMarketOrderVolume int 涨跌停价最大下单量MinMarketOrderVolume int 涨跌停价最小下单量MaxLimitOrderVolume int 限价单最大下单量MinLimitOrderVolume int 限价单最小下单量OptUnit int 期权合约单位MarginUnit float 期权单位保证金OptUndlCode str 期权标的证券代码OptUndlMarket str 期权标的证券市场OptExercisePrice float 期权行权价NeeqExeType str 全国股转转让类型OptUndlRiskFreeRate float 期权标的无风险利率OptUndlHistoryRate float 期权标的历史波动率EndDelivDate int 期权行权终止日optType str 期权类型  

# 示例  

示例返回值  

# #ContextInfo.get_option_list - 获取指定期权列表  

原型  

内置python  

ContextInfo.get_option_list(undl_code,dedate,opttype,isavailable)  

# 释义  

获取指定期权列表。如获取历史期权，需先下载过期合约列表  

# 参数  

<html><body><table><tr><td>字段名</td><td>数据 类型</td><td>解释</td></tr><tr><td>undl_code</td><td>string</td><td>期权标的代码，如'510300.SH</td></tr><tr><td>dedate</td><td>string</td><td>期权到期月或当前交易日期，"YYYYMM"格式为期权到期 月，"YYYYMMDD"格式为获取当前日期交易的期权</td></tr><tr><td>opttype</td><td>string</td><td>期权类型，默认值为空，"CALL"，"PUT"，为空时认购认 沽都取</td></tr><tr><td rowspan="2">isavailable</td><td rowspan="2">bool</td><td>是否可交易，当dedate 的格式为"YYYYMMDD"格式为获取</td></tr><tr><td>当前日期交易的期权时，isavailable为True时返回当前可 用，为False时返回当前和历史可用</td></tr></table></body></html>  

# 返回值  

list，期权合约列表  

# 示例  

示例data1 返回值data2 返回值data3 返回值# 获取到期月份为202101 的上交所510300ETF 认购合约data1=C.get_option_list('510300.SH','202101',"CALL")# 获取20210104 当天上交所510300ETF 可交易的认购合约data2=C.get_option_list('510300.SH','20210104',"CALL",True)# 获取20210104 当天上交所510300ETF 已经上市的认购合约(包括退市)data3=C.get_option_list('510300.SH','20210104',"CALL",False)  

# #ContextInfo.get_option_undl_data - 获取指定期权标的对应的期权品种列表  

# 原型  

内置pythonContextInfo.get_option_undl_data(undl_code_ref)  

# 释义  

获取指定期权标的对应的期权品种列表  

# 参数  

<html><body><table><tr><td>字段名</td><td>数据类 型</td><td>解释</td><td></td></tr><tr><td></td><td></td><td>期权标的代码,如'510300.SH'，传空字符串时获取全部</td><td></td></tr><tr><td>undl_code_ref</td><td>string</td><td>标的数据</td><td></td></tr></table></body></html>  

# 返回值  

指定期权标的代码时返回对应该标的的期权合约列表list  

期权标的代码为空字符串时返回全部标的对应的品种列表的字典dict  

# 示例  

示例返回值  

<html><body><table><tr><td>小例返回值</td></tr><tr><td>#coding:gbk def init(C):</td></tr><tr><td>pass</td></tr><tr><td></td></tr><tr><td>def handlebar(C):</td></tr><tr><td></td></tr></table></body></html>  

#ContextInfo.bsm_price - 基于BS 模型计算欧式期权理论价格  

# 原型  

内置python  

ContextInfo.bsm_price(optionType,objectPrices,strikePrice,riskFree,sigma,days,dividend)  

# 释义  

基于Black-Scholes-Merton 模型，输入期权标的价格、期权行权价、无风险利率、期权标的年化波动率、剩余天数、标的分红率、计算期权的理论价格  

# 参数  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>optionType</td><td>str</td><td>期权类型，认购：'C'，认沽：'P'</td></tr><tr><td>objectPrices</td><td>float</td><td>期权标的价格，可以是价格列表或者单个价格</td></tr><tr><td>strikePrice</td><td>float</td><td>期权行权价</td></tr><tr><td>riskFree</td><td>float</td><td>无风险收益率</td></tr><tr><td>sigma</td><td>float</td><td>标的波动率</td></tr><tr><td>days</td><td>int</td><td>剩余天数</td></tr><tr><td>dividend</td><td>float</td><td>分红率</td></tr></table></body></html>  

# 返回  

# 提示  

objectPrices 为float 时，返回float  
objectPrices 为list 时，返回list  
计算结果最小值0.0001，结果保留4 位小数,输入非法参数返回nan  

示例返回值  

# #ContextInfo.bsm_iv - 基于BS 模型计算欧式期权隐含波动率  

# 原型  

内置pythonContextInfo.bsm_iv(optionType,objectPrices,strikePrice,optionPrice,riskFree,days,dividend)  

释义 基于Black-Scholes-Merton 模型,输入期权标的价格、期权行权价、期权现价、无风险利率、剩余天数、标的分红率,计算期权的隐含波动率  

# 参数  

字段 类型 说明optionType str 期权类型，认购：'C'，认沽：'P'objectPrices float 期权标的价格，可以是价格列表或者单个价格strikePrice float 期权行权价riskFree float 无风险收益率  

字段 类型 说明sigma float 标的波动率days int 剩余天数dividend float 分红率  

返回 double 示例返回值  

#encoding:gbk   
import numpy as np   
def init(ContextInfo): pass   
def after_init(ContextInfo): # 计算剩余15 天的行权价3.5 的认购期权,在无风险利率3%,分红率为0 时,标的现价3.51   
元,期权价格0.0725 元时的隐含波动率 iv=ContextInfo.bsm_iv('C',3.51,3.5,0.0725,0.03,15) print(iv)  

#获取除复权信息  

#ContextInfo.get_divid_factors - 获取除权除息日和复权因子  

原型  
内置python  
ContextInfo.get_divid_factors(stock.market)  

释义  

获取除权除息日和复权因子  

参数  

字段名 数据类型 解释  

stock.market string 股票代码.市场代码，如 '600000.SH'  

返回值  

dict  

key:时间戳，  

value:list[每股红利,每股送转,每股转赠,配股,配股价,是否股改,复权系数]输入除权除息日非法时候返回空dict，合法时返回输入日期的对应的dict，不输入时返回查询股票的所有除权除息日及对应dict  

示例  

示例返回值  

def handlebar(C): Result = C.get_divid_factors('600000.SH') print(Result)  

# #获取指数权重  

#ContextInfo.get_weight_in_index - 获取某只股票在某指数中的绝对权重  

原型  

内置pythonContextInfo.get_weight_in_index(indexcode, stockcode)  

释义  

获取某只股票在某指数中的绝对权重  

# 参数  

<html><body><table><tr><td>字段名</td><td>数据类 型</td><td>解释</td><td rowspan="2">'stockcode.market'，例如</td></tr><tr><td>indexcode</td><td>string</td><td>指数代码，格式为 000300.SH</td></tr><tr><td></td><td></td><td></td><td>'stockcode.market'，例如</td></tr><tr><td>stockcode</td><td>string</td><td>股票代码，格式为 600004.SH</td><td></td></tr></table></body></html>  

返回值  

float：返回的数值单位是 %，如 1.6134 表示权重是 $1.6134\%$  

示例  

示例返回值  

def handlebar(C): data = C.get_weight_in_index('000300.SH', '000002.SZ') print(data)  

#获取成分股信息  

#ContextInfo.get_stock_list_in_sector - 获取板块成份股  

原型  

内置python  

释义获取板块成份股，支持客户端左侧板块列表中任意的板块，包括自定义板块  

参数返回值  

<html><body><table><tr><td>字段名</td><td>数据类型</td><td>解释</td></tr><tr><td>sectorname</td><td>string</td><td>板块名，如‘沪深300'，‘中证500'，‘上证50'，‘我 的自选等</td></tr><tr><td></td><td>毫秒级时间</td><td></td></tr><tr><td>realtime</td><td></td><td>实时数据的毫秒级时间戳</td></tr><tr><td></td><td>戳</td><td></td></tr></table></body></html>  

list：内含成份股代码，代码形式为 'stockcode.market'，如 '000002.SZ'  

示例  

示例返回值  

# coding:gbk   
def init(C): pass   
def handlebar(C): print(C.get_stock_list_in_sector('上证50'))  

# #获取交易日信息  

注意  

1.  该函数只能在after_init;handlebar 运行  

# #ContextInfo.get_trading_dates - 获取交易日信息  

原型  
内置python  
ContextInfo.get_trading_dates(stockcode,start_date,end_date,count,period='1d')  

释义  

ContextInfo.get_trading_dates(stockcode,start_date,end_date,count,period $\qquad\qquad\qquad\qquad\qquad\qquad\qquad\qquad=^{\prime}\,\daleth$ d')  

参数  

<html><body><table><tr><td>stockcode</td><td>string</td><td>股票代码，缺省值"默认为当前图代码，如：600000.SH"</td></tr><tr><td>start_date</td><td>string</td><td>开始时间，缺省值"为空时不使用， 如：20170101,20170101000000</td></tr><tr><td>end_date</td><td>string</td><td>结束时间，缺省值"默认为当前bar的时间， 如：20170102',20170102000000'</td></tr><tr><td>count</td><td>int</td><td>K线个数，必须大于O，取包括end_date往前的count个 K线，start_date 不为空时此值无效，写为1即可</td></tr><tr><td>period</td><td>string</td><td>k线类型，1d：日线，1m：分钟线，3m*三分钟线，5m*：5分钟 线，15m*：15分钟线，30m：30分钟线，1h：小时线，1w：周 线，1mon*月线，1g*季线，1hy半年线，1y年线</td></tr></table></body></html>  

# 返回值  

list:K 线周期（交易日）列表 period 为日线时返回如['20170101','20170102',...]样式 其它返回如['20170101010000','20170102020000',...]样式  

# 示例  

示例返回值  

coding:gbk  

def init(C):  

def after_init(C): print(C.get_trading_dates('600000.SH','','',30,'1d'))   
def handlebar(C):  

# 交易下单函数  

# #passorder - 综合下单函数  

综合下单函数，用于股票、期货、期权等下单和新股、新债申购、融资融券等交易操作推荐使用  

# 提示  

1. 推荐使用  
2. 可覆盖多品种下单  
3. 注意参数的变化  

# 调用方法：  

python 示例  

![](images/1cae788297844b5cd6278903c55ae44dfc7de38cb26327dacc2d7479a860fdc9.jpg)  

参数：  

<html><body><table><tr><td>参数名</td><td>类型</td><td>说明</td><td>提示</td></tr><tr><td rowspan="4">opType</td><td rowspan="4">int</td><td rowspan="4">交易 类型</td><td>可选买、买，期货开仓、平仓等</td></tr><tr><td>可选值参考opType-操作类型在新窗口打开</td></tr><tr><td>可选值参考orderType-下单方式在新窗口打 开</td></tr><tr><td>可选按股票数量买卖或按照金额等方式买卖</td></tr><tr><td rowspan="4">orderType</td><td rowspan="4">int</td><td rowspan="4">下单 方式</td><td>一、期货不支持1102和1202;</td></tr><tr><td></td></tr><tr><td>二、对所有账号组的操作相当于对账号组里的 每个账号做一样的操作，如passorder（23,</td></tr><tr><td>1202,'testS'，'000001.SZ'，5,-1，50000, ContextInfo)，意思就是对账号组testS里的所 有账号都以最新价开仓买入50000元市值 的0ooo01.sZ平安银行；passorder (60,1101,"test",'510050. SH', 5,-1,1, ContextInfo)</td></tr><tr><td>accountID</td><td>string</td><td>资金 账号</td><td>意思就是账号test申购1个单位 (900000股) 的华夏上证50ETF (只申购不买入成分股)。 下单的账号ID（可多个）或账号组名或套利组 名（一个篮子一个套利账号，如accountlD： 股票账户名，期货账号) 1．如果是单股或单期货、港股，则该参数填合</td></tr><tr><td>orderCode</td><td>string</td><td>下单 代码</td><td>约代码; 2.如果是组合交易，则该参数填篮子名称，参 考组合交易在新窗口打开; 3．如果是组合套利，则填一个篮子名和一个 期货合约名（如 orderCode='篮子名，期货合 约名)，请参考组合套利交易在新窗口打开</td></tr><tr><td>prType</td><td>int</td><td>下单 开 选价 类型</td><td>可选值参考 prType-下单选价类型在新窗口打 特别的对于套利，这个 prType只对篮子起作 用，期货的采用默认的方式)</td></tr></table></body></html>  

参数名 类型 说明 提示一、单股下单时，prType 是模型价/科创板盘后定价时 price 有效；其它情况无效；1.1 即单股时， prType 参数为 11，49 时被使用。下单  
price float 价格1.2 prType 参数不为 11，49 时也需填写，填写的内容可为 -1，0，2，100 等任意数字；二、组合下单时，是组合利利时，price 作利利比例有效，其它情况无效。下单数量根据 orderType 值最后一位确定 volume 的（股  
volume int 单位，可选值参考volume - 下单在新窗口打/  手开/  元/ %）  

一、用来区分 order 委托和deal 成交来自不同的策略。  

根据该策略名，get_trade_detail_data ，自定strategyName string 义策 get_last_order_id 函数可以获取相应策略名对略名 应的委托或成交集合。  

strategyName 只对同账号本地客户端有效，即 strategyName 只对当前客户端下的单进行策略区分，且该策略区分只能当前客户端使用。  

设定可选值参考quicktrade - 快速下单在新窗口是否打开quickTrade int 立即触发passorder 是对最后一根K 线完全走完后生成下单的模型信号在下一根K 线的第一个tick 数据来时触发下单交易；  

参数名 类型 说明  

<html><body><table><tr><td></td><td></td><td>采用quickTrade参数设置为1时，非历史bar 上执行时（ContextInfo.is_last_barO为True）, 只要策略模型中调用到就触发下单交易。 quickTrade参数设置为2时，不判断bar状态， 只要策略模型中调用到就触发下单交易，历史</td></tr><tr><td>userOrderld string class</td><td>用户 自设 的 委托</td><td>bar上也能触发下单，请谨慎使用。 如果传入该参数 则 strategyName 和quickTrade 参数也填写。 对应order委托对象和deal成交对象中 m_strRemark 属性， 通</td></tr><tr><td>Contextlnfo</td><td>ID 系统 参数</td><td>过get_trade_detail_data函数或委托主推函 数order_callback和成交主推函 数deal_callback可拿到这两个对象信息。 含有k线信息和接口的上下文对象</td></tr></table></body></html>  

返回：  

无  

# 更多示例：  

1. 股票在新窗口打开  
2. 基金在新窗口打开  
3. 两融在新窗口打开  
4. 期货在新窗口打开  
5. 期权在新窗口打开  
6. 新股申购在新窗口打开  
7. 债券在新窗口打开  
8. ETF 在新窗口打开  
9. 组合交易在新窗口打开  
10. 组合利利交易在新窗口打开  

# #algo_passorder - 算法下单 （拆单） 函数  

用于按固定时间间隔和固定规则把目标交易数量拆分成多次下单的交易函数  

# 调用用法：  

algo_passorder(opType,orderType,accountid,orderCode,prType,price,volume,[strategyName,qui ckTrade,userOrderId,userOrderParam],ContextInfo)\`  

# 提示  

算法交易下单，此时使用交易面板-程序交易-函数交易-函数交易参数中设置的下单类型(普通交易,算法交易,随机量交易) 如果函数交易参数使用未修改的默认值,此函数和passorder 函数一致， 设置了函数交易参数后，将会使用函数交易参数的超价等拆单参数，algo_passorder 内的prType 若赋值,则优先使用该参数，若algo_passorder 内的prType $\cdot{=}{-}1,$ 将会使用userOrderParam 内的opType，若userOrderParam 未赋值，则使用界面上的函数交易参数的报价方式  

# 参数：  

其他参数同passorder，详细解释可参考passorder 的说明  
userOrderParam dict[str:value] 是用户自定义交易参数,主要用于修改算法交易的参  
数 其中Key Value 定义如下  

注：所有参数均为非必选  

<html><body><table><tr><td>Key</td><td colspan="2">Value类 型</td><td rowspan="2">Value</td></tr><tr><td>OrderType</td><td>int</td><td>普通交易:0 算法交易:1</td></tr><tr><td rowspan="2">PriceType</td><td></td><td>随机量交易:2</td></tr><tr><td></td><td>报价方式:数值同passordeprType</td></tr><tr><td>MaxOrderCount</td><td>int int</td><td>最大下单次数</td></tr><tr><td rowspan="2">SinglePriceRange</td><td>int</td><td>波动区间是否单向：</td></tr><tr><td>是:1</td><td>否:0,</td></tr></table></body></html>  

<html><body><table><tr><td>Key</td><td>Value类 型</td><td>Value</td></tr><tr><td>PriceRangeType</td><td>int</td><td>波动区间类型按比例：0,按数值1</td></tr><tr><td>PriceRangeValue</td><td>float</td><td>波动区间(按数值)</td></tr><tr><td>PriceRangeRate</td><td>float</td><td>波动区间(按比例)[0-1]</td></tr><tr><td></td><td></td><td>单笔超价类型:</td></tr><tr><td>SuperPriceType</td><td>int</td><td>按比例:0</td></tr><tr><td></td><td></td><td>按数值 1</td></tr><tr><td>SuperPriceRate</td><td>float</td><td>单笔超价(按比例)[0-1]</td></tr><tr><td>SuperPriceValue</td><td>float</td><td>单笔超价(按数值)</td></tr><tr><td></td><td></td><td>单笔基准量类型卖1+2+3+4+5量:0</td></tr><tr><td></td><td></td><td>卖 1+2+3+4量:1</td></tr><tr><td></td><td></td><td>卖1量:4</td></tr><tr><td>VolumeType</td><td></td><td>买1量:5</td></tr><tr><td></td><td>int</td><td></td></tr><tr><td></td><td></td><td>买1+2+3+4+5量:9</td></tr><tr><td></td><td></td><td>目标量：10</td></tr><tr><td></td><td></td><td>目标剩余量:11</td></tr><tr><td></td><td></td><td>持仓数量:12</td></tr><tr><td>VolumeRate</td><td>float</td><td>单笔下单比率[0-1]</td></tr><tr><td>SingleNumMin</td><td>float</td><td>单笔下单量最小值</td></tr><tr><td>SingleNumMax</td><td>float</td><td>单笔下单量最大值</td></tr><tr><td></td><td></td><td></td></tr><tr><td>ValidTimeType</td><td>int</td><td>有效时间类型: 0:按持续时间</td></tr><tr><td></td><td></td><td>1 按时间区间，默认为0</td></tr><tr><td>ValidTimeElapse</td><td>int</td><td>有效持续时间,ValidTimeType设置为O时生效</td></tr><tr><td>ValidTimeStart</td><td>int</td><td>有效开始时间偏移，ValidTimeType 设置为1时</td></tr><tr><td></td><td></td><td>生效</td></tr><tr><td>ValidTimeEnd</td><td>int</td><td>有效结束时间偏移，ValidTimeType 设置为1时</td></tr></table></body></html>  

<html><body><table><tr><td>Key</td><td>Value类 型</td><td>Value</td></tr><tr><td rowspan="2">UndealtEntrustRule</td><td colspan="2">生效</td></tr><tr><td>int</td><td>未成委托处理数值同 prType</td></tr><tr><td>PlaceOrderlnterval</td><td>int</td><td>下撤单时间间隔</td></tr><tr><td rowspan="3">UseTrigger</td><td rowspan="3">int</td><td>是否触价：</td></tr><tr><td>否：0</td></tr><tr><td>是:1</td></tr><tr><td>TriggerType</td><td>int</td><td>触价类型: 最新价大于:1 最新价小于:2</td></tr><tr><td>TriggerPrice</td><td>float</td><td>触价价格</td></tr><tr><td>SuperPriceEnable</td><td>int</td><td>超价启用笔数</td></tr></table></body></html>  

返回无示例  

# 调用方法一：  

python   
smart_algo_passorder(opType,orderType,accountid,orderCode,prType,price,volume,strageName, quickTrade,userOrderId,smartAlgoType,limitOverRate,minAmountPerOrder,[targetPriceLevel,st artTime,endTime,limitControl],ContextInfo)  

# 提示  

可选参数可缺省  

参数：其他参数同passorder，详细解释可参考passorder 的说明在新窗口打开  

<html><body><table><tr><td>参数名</td><td>类 型</td><td>说明</td><td>提示</td></tr><tr><td>prType</td><td>in t</td><td>可选值： 11:限价（只对单股情况支持，对 组合交易不支持) 12:市价 特别的对于套利：这个prType只 对篮子起作用，期货的采用默认</td><td></td></tr><tr><td>smartAlgoType</td><td>str</td><td>的方式 智能算法类型 [enum_constants#smartAlgoTyp e 智能算法类型在新窗口打开]</td><td>网格算法无此</td></tr><tr><td>limitOverRate</td><td>in t</td><td>量比数据范围0-100</td><td>项 若 在 algoParam中 填写量比,则填 写范围0-1 的 小数。</td></tr><tr><td>minAmountPerOrde r</td><td>in t</td><td>智能算法最小委托金额，数据范 围0-100000</td><td></td></tr><tr><td rowspan="2">targetPriceLevel</td><td>in</td><td>智能算法目标价格，可选值：</td><td>一、输入无效值</td></tr><tr><td>t</td><td>1：己方盘口1 2：己方盘口2</td><td>则 targetPriceLeve</td></tr></table></body></html>  

<html><body><table><tr><td>startTime</td><td>型 3：己方盘口3 4: 己方盘口4 5: 己方盘口5 6：最新价 7：对方盘口 str 智能算法开始时间</td><td></td><td>1为1 二、本项只针对 冰山算法,其他 算法可缺省。 格 式 "HH:MM:SS", 如"10:30:00"。</td></tr><tr><td>endTime</td><td>str</td><td>智能算法截止时间</td><td>如果缺省值，则 默 认 为 "09:30:00" 格 式 "HH:MM:SS", 如"14:30:00"。 如果缺省值，则</td></tr><tr><td>limitControl</td><td>in t</td><td>涨跌停控制</td><td>默认 为 "15:30:00" 默认值为 1 1：涨停不卖跌 停不卖</td></tr><tr><td>返回 无</td><td></td><td></td><td>0：无限制</td></tr></table></body></html>  

示例：  

![](images/06fb747b2928ccada17bf9ebd4b06bb8f1b663c0901ae62eabe3c3a5a74b7394.jpg)  

![](images/251d83dc7a5068d8982d63f906e869457f353134c3ccb4fbdbd24ffccfa52b0c.jpg)  

# 调用方法二：  

当时用algoParam 时，函数声明为：  

smart_algo_passorder(opType,orderType,accountid,orderCode,prType,modelprice,volume,strage Name,quickTrade,userid,smartAlgoType,startTime,endTime,algoParam,ContextInfo)参数均不 可缺省  

smartAlgoType,startTime,endTime 含义同上，algoParam 请使用下面的方法获取：  

# #获取algoParam 具体字段  

# 释义  

获取智能算法参数配置信息  

用法 python  

get_smart_algo_param(algoList)  

参数返回  

<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>algoList</td><td>list</td><td>需要查询参数配置信息的算法名称列表，若传空则查询全部有</td></tr><tr><td></td><td></td><td>权限的算法参数配置信息</td></tr><tr><td></td><td></td><td></td></tr></table></body></html>  

返回一个字典，键为算法名称，值为参数字典列表。  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>key</td><td>string</td><td>参数名称 key 值,即 smart_algo_order 中 algoList 字 典需要传的键值</td></tr><tr><td>name</td><td>string</td><td>参数名称</td></tr><tr><td>dataType</td><td>string</td><td>参数类型</td></tr><tr><td>valueRange</td><td>string</td><td>参数范围</td></tr><tr><td>defaultValue</td><td>string</td><td>参数默认值</td></tr><tr><td>enumName</td><td>string</td><td>参数枚举值的名称</td></tr><tr><td>enumValue</td><td>string</td><td>参数实际的枚举值</td></tr><tr><td>unit</td><td>string</td><td>参数的单位，当单位为%时，值要填写小数而非参 数范围所示的百分数值</td></tr><tr><td>valueRangeByName</td><td>string</td><td>不同算法参数范围</td></tr><tr><td>defaultValueByName</td><td>string</td><td>不同算法参数默认值</td></tr></table></body></html>  

示例  

# algoParam# 先获取所有需要传入的参数  

print(get_smart_algo_param(['VWAP'])) 输出：[2024-01-30 11:21:10][智能算法1][SH000300][日线] {'VWAP': [ {'key': 'm_dLimitOverRate', 'name': '量比比例', 'dataType': '浮点数', 'valueRange': '0.00- 100.00', 'defaultValue': '20.00', 'enumName': '', 'enumValue': '', 'unit': '%', 'valueRangByName': '', defaultValueByName': ''}, {'key': 'm_dMinAmountPerOrder', 'name': '委托最小金额', 'dataType': '整数', valueRange': '0-100000', 'defaultValue': '0', 'enumName': '', 'enumValue': '', 'unit': '', valueRangByName': '', 'defaultValueByName': ''}, {'key': 'm_dMaxAmountPerOrder', 'name': '委托最大金额', 'dataType': '浮点数', valueRange': '0.00-100000000.00', 'defaultValue': '0', 'enumName': '', 'enumValue': '', 'unit': '' 'valueRangByName': '', 'defaultValueByName': ''}, {'key': 'm_nStopTradeForOwnHiLow', 'name': '涨跌停控制', 'dataType': '整数', 'valueRange': '', 'defaultValue': '涨停不卖跌停不买', 'enumName': '无,涨停不卖跌停不买', enumValue': '0,1', 'unit': '', 'valueRangByName': '', 'defaultValueByName': ''}, {'key': 'm_dMulitAccountRate', 'name': '多账号总量比', 'dataType': '浮点数', valueRange': '0.00-100.00', 'defaultValue': '0', 'enumName': '', 'enumValue': '', 'unit': '%', valueRangByName': '', 'defaultValueByName': ''}, {'key': 'm_strCmdRemark', 'name': '投资备注', 'dataType': '字符串', 'valueRange': '', defaultValue': '', 'enumName': '', 'enumValue': '', 'unit': '', 'valueRangByName': '', defaultValueByName': ''}]}  

algoParam=  
'm_dLimitOverRate': 0.25, # 量比 25%  
'm_dMinAmountPerOrder':0, # 委托最小金额  
'm_dMaxAmountPerOrder':10000, # 委托最大金额  
'm_nStopTradeForOwnHiLow': 1, # 涨跌停控制  
'm_dMulitAccountRate':0.30, # 多账号总量比  
'm_strCmdRemark':  '投资备注1' # 投资备注  
}  
smart_algo_passorder(23,1101,account,'600000.SH',12,0,10000,  

# #cancel-撤销委托  

调用方法cancel(orderId, accountId, accountType, ContextInfo)  

参数  

<html><body><table><tr><td>参数名</td><td>类型</td><td>含义</td><td>说明</td></tr><tr><td>orderld</td><td>string</td><td>委托号</td><td>必填</td></tr><tr><td>accountID</td><td>string</td><td>资金账号</td><td>必填</td></tr><tr><td rowspan="6">AccountType</td><td></td><td>账号类型可选：</td><td></td></tr><tr><td></td><td>'FUTURE'：期货</td><td></td></tr><tr><td></td><td>'STOCK'：股票</td><td></td></tr><tr><td>string</td><td>'CREDIT'：信用</td><td>必填</td></tr><tr><td></td><td>'HUGANGTONG'：沪港通</td><td></td></tr><tr><td></td><td>SHENGANGTONG'：深港通 'STOCK_OPTION':期权</td><td></td></tr><tr><td>Contextlnfo</td><td>class</td><td>含有k线信息和接口的上下文对象</td><td>必填</td></tr></table></body></html>  

返回 bool，是否发出了取消委托信号，返回值含义：  

True：是 False：否  

python 返回值  

![](images/20b33093e40fae78d7625d758a1518b832537a55ed2f238dd718e4edf1542d3e.jpg)  

# #cancel_task - 撤销任务  

调用方法cancel_task(taskId,accountId,accountType,ContextInfo)  

参数  

<html><body><table><tr><td>参数名</td><td>类型</td><td>含义</td><td>说明</td></tr><tr><td>taskld</td><td>string</td><td>委托号</td><td>必填</td></tr><tr><td>accountID</td><td>string</td><td>资金账号</td><td>必填</td></tr><tr><td rowspan="6">AccountType</td><td></td><td>账号类型可选：</td><td></td></tr><tr><td></td><td>'FUTURE'：期货</td><td></td></tr><tr><td></td><td>'STOCK':月 股票</td><td></td></tr><tr><td>string</td><td>'CREDIT'：信用</td><td>必填</td></tr><tr><td></td><td>'HUGANGTONG'：沪港通</td><td></td></tr><tr><td></td><td>'SHENGANGTONG'：深港通</td><td></td></tr><tr><td></td><td></td><td>STOCK_OPTION':期权</td><td></td></tr></table></body></html>  

<html><body><table><tr><td>参数名</td><td>类型</td><td>含义</td><td>说明</td></tr><tr><td>Contextlnfo</td><td>class</td><td>含有k线信息和接口的上下文对象</td><td>必填</td></tr></table></body></html>  

返回 bool，是否发出了撤销任务信号，返回值含义：  

True：是  

False：否  

示例  

python  

![](images/bc8474da299a71d3aec3f09f167bd5925902034cdb16c0cc2ad7fa31bd627234.jpg)  

# #pause_task - 暂停任务  

暂停智能算法任务  

调用方法 pause_task(taskId,accountId,accountType,ContextInfo)  

参数  

<html><body><table><tr><td>参数名</td><td>类型</td><td>含义</td><td>说明</td></tr><tr><td>taskld</td><td>string</td><td>委托号</td><td>必填</td></tr><tr><td>accountID</td><td>string</td><td>资金账号</td><td>必填</td></tr><tr><td rowspan="6">AccountType</td><td></td><td>账号类型可选：</td><td></td></tr><tr><td></td><td>'FUTURE'：期货</td><td></td></tr><tr><td></td><td>'STOCK：股票</td><td>必填</td></tr><tr><td>string</td><td>'CREDIT'：信用</td><td></td></tr><tr><td></td><td>'HUGANGTONG'：沪港通 SHENGANGTONG'：深港通</td><td></td></tr><tr><td></td><td>STOCK_OPTION'：期权</td><td></td></tr><tr><td>Contextlnfo</td><td>class</td><td>含有k线信息和接口的上下文对象</td><td>必填</td></tr></table></body></html>  

返回 bool，是否发出了暂停任务信号，返回值含义：  

True：是 False：否  

示例  

python  

![](images/f2055d9f1927bd1c59d0c1511b56b6545deee1a3d42ca4c6485dd785ba261ceb.jpg)  

# #resume_task - 继续任务  

继续智能算法任务  

调用方法resume_task(taskId,accountId,accountType,ContextInfo)  

参数  

<html><body><table><tr><td>参数名</td><td>类型</td><td>含义</td><td>说明</td></tr><tr><td>taskld</td><td>string</td><td>委托号</td><td>必填</td></tr><tr><td>accountID</td><td>string</td><td>资金账号</td><td>必填</td></tr><tr><td rowspan="6">AccountType</td><td></td><td>账号类型可选：</td><td></td></tr><tr><td></td><td>'FUTURE'：期货</td><td></td></tr><tr><td></td><td>'STOCK'：股票</td><td></td></tr><tr><td>string</td><td>'CREDIT'：信用</td><td>必填</td></tr><tr><td></td><td>'HUGANGTONG'：沪港通</td><td></td></tr><tr><td></td><td>'SHENGANGTONG'：深港通 STOCK_OPTION':期权</td><td></td></tr><tr><td>Contextlnfo</td><td>class</td><td>含有k线信息和接口的上下文对象</td><td>必填</td></tr></table></body></html>  

返回 bool，是否发出了重启任务信号，返回值含义：  

True：是  

False：否  

示例  

python  

# #get_basket-获取股票篮子  

用法： get_basket(basketName)  

释义： 获取股票篮子  

# 参数：  

basketName：股票篮子名称  

示例：  

print( get_basket('basket1') )  

#set_basket-设置股票篮子  

用法： set_basket(basketDict)  

释义： 设置passorder 的股票篮子,仅用于passorder 进行篮子交易,设置成功后,用get_basket 可以取出后即可进行passorder 组合交易下单  

# 参数：  

basketDict：股票篮子 {'name':股票篮子名称,'stocks':[{'stock':股票名称,'weight',权重,'quantity':数量,'optType':交易类型}]} 。  

# 示例：  

# #get_trade_detail_data-查询账号资金信息、委托记录等  

调用方法 get_trade_detail_data(accountID, strAccountType, strDatatype, strategyName)  
或不区分策略  
get_trade_detail_data(accountID, strAccountType, strDatatype)  

参数  


<html><body><table><tr><td>参数名</td><td>类型</td><td>说明</td><td>备注</td></tr><tr><td>accountID</td><td>string</td><td>资金账号</td><td>必填</td></tr><tr><td rowspan="8">strAccountType</td><td></td><td>账号类型可选：</td><td rowspan="8">必填</td></tr><tr><td></td><td>'FUTURE'：期货</td></tr><tr><td>'STOCK'：股票</td><td></td></tr><tr><td>string</td><td>'CREDIT'：信用</td></tr><tr><td>'HUGANGTONG'：沪港通</td><td></td></tr><tr><td></td><td>SHENGANGTONG'：深港通</td></tr><tr><td></td><td>STOCK_OPTION':期权</td></tr><tr><td>要查询数据类型 可选： ACCOUNT：账号对象在新窗口打开 或信用账号对象在新窗口打开 在新窗口打开</td><td></td></tr><tr><td>strDatatype</td><td>string</td><td>POSITION：持仓在新窗口打开 POSITION_STATISTICS：持仓统计 ORDER: 委托在新窗口打开 DEAL：成交在新窗口打开 TASK: 任务在新窗口打开</td><td>必填</td></tr><tr><td></td><td></td><td></td><td></td></tr><tr><td></td><td></td><td></td><td></td></tr><tr><td></td><td></td><td></td><td></td></tr><tr><td></td><td></td><td></td><td></td></tr><tr><td></td><td></td><td></td><td></td></tr><tr><td></td><td></td><td></td><td></td></tr><tr><td></td><td></td><td></td><td></td></tr><tr><td></td><td></td><td></td><td></td></tr><tr><td></td><td></td><td></td><td></td></tr><tr><td></td><td></td><td>策略 当用passorder下单时指定</td><td></td></tr><tr><td></td><td></td><td>了 strategyName 参数时，当查询</td><td></td></tr><tr><td></td><td></td><td></td><td>strategyName</td></tr><tr><td></td><td></td><td></td><td></td></tr><tr><td></td><td></td><td>成交和委托时传入同样的</td><td>参数只对成交</td></tr><tr><td>strategyName</td><td>string</td><td></td><td></td></tr><tr><td></td><td></td><td></td><td></td></tr><tr><td></td><td></td><td>strageName，则可以只返回包含</td><td>和委托有效,选</td></tr><tr><td></td><td></td><td></td><td></td></tr><tr><td></td><td></td><td></td><td></td></tr><tr><td></td><td></td><td></td><td></td></tr><tr><td></td><td></td><td></td><td></td></tr><tr><td></td><td></td><td></td><td>填</td></tr><tr><td></td><td></td><td>strategyName的委托子集或成交</td><td></td></tr><tr><td></td><td></td><td>子集</td><td></td></tr></table></body></html>  

返回 list，list 中放的是对应strDatatype 的 Python 对象，通过 dir(pythonobj)可返回某个对象的属性列表。  

有五种交易相关信息，包括：  

ACCOUNT：账号对象在新窗口打开或信用账号对象在新窗口打开  

POSITION：持仓明细在新窗口打开  

POSITION_STATISTICS: 持仓统计在新窗口打开  

ORDER： 委托在新窗口打开  

DEAL： 成交在新窗口打开  

TASK： 任务在新窗口打开  

# 示例：  

python 返回值  

#coding:gbk  

account = '800174' # 在策略交易界面运行时，account 的值会被赋值为策略配置中的账号，编辑器界面运行时，需要手动赋值；编译器环境里执行的下单函数不会产生实际委托  

def init(ContextInfo):  

pass  

ef handlebar(ContextInfo): if not ContextInfo.is_last_bar():  

return  

positions = get_trade_detail_data(account, 'stock', 'position') print('查询持仓结果：')  

accounts = get_trade_detail_data(account, 'stock', 'account') print('查询账号结果：')  

print(f'总资产: {dt.m_dBalance:.2f}, 净资产: {dt.m_dAssureAsset:.2f}, 总市值: {dt.m_dInstrumentValue:.2f}',  

f'总负债: {dt.m_dTotalDebit:.2f}, 可用金额: {dt.m_dAvailable:.2f}, 盈亏:{dt.m_dPositionProfit:.2f}')  

position_statistics = get_trade_detail_data(account,"FUTURE",'POSITION_STATISTICS') for obj in position_statistics:  

# #get_history_trade_detail_data - 查询历史交易明细  

用  
法： get_history_trade_detail_data(accountID,strAccountType,strDatatype,strStratDate,strEndDate);  

释义： 获取历史成交明细数据，返回结果为一个([timetag,obj...])的元组  

# 参数：  

accountID：string,账号； strAccountType：string,账号类型,有 "FUTURE","STOCK","CREDIT","HUGANGTONG","SHENGANGTONG","STOCK_O PTION"； strDatatype：string,交易明细数据类型,有：持仓"POSITION"、委托 "ORDER"、成交"DEAL"； strStratDate：string,开始时间,如'20240513'； strEndDate：string,结束时间,如'20240514'；  

\*\*返回：\*\*list,list 中放的是PythonObj,通过dir(pythonobj)可返回某个对象的属性列表 示例：  

示例  

def handlebar(ContextInfo):  

obj_list = get_history_trade_detail_data('6000000248','stock','position','20240513','20240514') for time,data in obj_list: for obj in data: print(obj.m_strInstrumentID) print(dir(obj))#查看有哪些属性字段  

# #get_ipo_data-获取当日新股新债信息  

用法： get_ipo_data([,type])  

释义： 获取当日新股新债信息，返回结果为一个字典,包括新股申购代码,申购名称,最大申购数量,最小申购数量等数据  

参数：  

type：为空时返回新股新债信息，type $=$ "STOCK"时只返回新股申购信息，type $=$ "BOND"时只返回新债申购信息  

示例：  

def init(ContextInfo):ipoData=get_ipo_data()# 返回新股新债信息ipoStock=get_ipo_data("STOCK")# 返回新股信息ipoCB=get_ipo_data("BOND")# 返回新债申购信息#get_new_purchase_limit-获取账户新股申购额度用法： get_new_purchase_limit(accid)  

释义： 获取账户新股申购额度，返回结果为一个字典,包括上海主板,深圳市场,上海科创版的申购额度  

# 参数：  

accid：资金账号，必须时股票账号或者信用账号  

# 示例：  

def init(ContextInfo):ContextInfo.accid="10000001"# 返回新股新债信息purchase_limit=get_new_purchase_limit(ContextInfo.accid)  

#get_value_by_order_id-根据委托号获取委托或成交信息  

调用方法get_value_by_order_id(orderId, accountID, strAccountType, strDatatype)  

参数  

<html><body><table><tr><td>参数名</td><td>类型</td><td>含义</td><td>说明</td></tr><tr><td>orderld</td><td>string</td><td>委托号</td><td>必填</td></tr><tr><td>accountID</td><td>string</td><td>资金账号</td><td>必填</td></tr><tr><td rowspan="5">strAccountType</td><td rowspan="5">string</td><td>账号类型可选： 'FUTURE'：期货</td><td></td></tr><tr><td>'STOCK：股票</td><td></td></tr><tr><td>'CREDIT'：信用</td><td>必填</td></tr><tr><td></td><td>'HUGANGTONG'：沪港通</td></tr><tr><td>'SHENGANGTONG'：深港通 'STOCK_OPTION':期权</td><td></td></tr><tr><td>strDatatype</td><td>string</td><td>要查询数据类型可选： 'ORDER'：委托 'DEAL＇：成交</td><td>必填</td></tr></table></body></html>  

# 返回  

# 委托对象 或 成交对象  

示例  

python 返回值  

def init(ContextInfo): ContextInfo.accid = '6000000248' def handlebar(ContextInfo): orderid = get_last_order_id(ContextInfo.accid, 'stock', 'order') print(orderid) obj = get_value_by_order_id(orderid,ContextInfo.accid, 'stock', 'order') print(obj.m_strInstrumentID)  

调用方法  

python 区分策略，添加策略名称参数 strategyName   
get_last_order_id(accountID, strAccountType, strDatatype, strategyName) 不区分策略   
get_last_order_id(accountID, strAccountType, strDatatype)  

<html><body><table><tr><td>参数名</td><td>类型</td><td>含义</td><td>说 明</td></tr><tr><td>accountID</td><td>string</td><td>资金账号</td><td>必 填</td></tr><tr><td rowspan="6">strAccountType</td><td rowspan="6">string</td><td>账号类型可选：</td><td></td></tr><tr><td></td><td></td></tr><tr><td>'FUTURE'：期货 'STOCK'：股票</td><td>必</td></tr><tr><td>'CREDIT'：信用</td><td></td></tr><tr><td>'HUGANGTONG'：沪港通</td><td>填</td></tr><tr><td>'SHENGANGTONG'：深港通</td><td></td></tr><tr><td rowspan="4">strDatatype</td><td rowspan="4">string</td><td>STOCK_OPTION':期权</td><td></td></tr><tr><td>要查询数据类型 可选:</td><td></td></tr><tr><td>'ORDER'：委托</td><td>必 填</td></tr><tr><td>'DEAL＇：成交</td><td></td></tr><tr><td>strategyName</td><td>string</td><td>策略 strategyName 参数时，当查询成交和委托时传 入同样的strageName，则可以只返回包含 strategyName的委托子集或成交子集</td><td>当用passorder下单时指定了 选 填</td></tr></table></body></html>  

返回  

String，委托号，如果没找到返回 '-1'。  

示例  

def init(ContextInfo): ContextInfo.accid = '6000000248'   
def handlebar(ContextInfo): orderid = get_last_order_id(ContextInfo.accid, 'stock', 'order') print(orderid) obj = get_value_by_order_id(orderid,ContextInfo.accid, 'stock', 'order') print(obj.m_strInstrumentID)  

# #get_assure_contract-获取两融担保标的明细  

用法： get_assure_contract(accId)  

释义： 获取信用账户担保合约明细  

参数：  

accId：信用账户  

返回： list，list 中放的是 StkSubjects 在新窗口打开，通过 dir(pythonobj) 可返回某个对象的属性列表。  

# 示例：  

python  

![](images/9d0f443d64c5356b86f8fd2a0023a244af80837f6b650fde1939754162a5ed29.jpg)  

# #get_enable_short_contract-获取可融券明细  

# 提示  

注:由于字段m_dSloRatio、m_dSloStatus 提供来源和取担保品明细  

(get_assure_contract)重复，字段在2021 年9 月移除，后续用担保品明细接口获取,具体见 担保标的对象字段说明在新窗口打开  

用法： get_enable_short_contract(accId)  

释义： 获取信用账户当前可融券的明细  

# 参数：  

accId：信用账户  

返回： list，list 中放的是 CreditSloEnableAmount 在新窗口打开，通过dir(pythonobj) 可返回某个对象的属性列表。  

示例：  

python  

![](images/c0ea648971b19882f51e00f07cb4b5b9bb00510d93f9efaaaa62ffc0c4d96ca6.jpg)  

# #query_credit_account - 查询信用账户明细  

# 注意  

1. 本函数一次最多查询200 只股票的两融最大下单量，且同时只能有一个查询,如果前面的查询正在进行中,后面的查询将会提前返回。本函数从服务器查询数据,建议平均查询时间间隔180s 一次,不可频繁调用。  
2. 该函数必须配合credit_account_callback 回调才能使用，关于此回调的说明请看credit_account_callback 在新窗口打开  
3.  callback 返回的对象是CCreditAccountDetail 在新窗口打开  

调用query_credit_account，该接口的查询结果将会推送给credit_account_callback，所以程序里需要按照函数参数实现函数credit_account_callback,callback 返回的对象是CCreditAccountDetail 在新窗口打开用法： query_credit_account(accountId,seq,ContextInfo)  

释义： 查询信用账户明细。本函数只能有一个查询，如果前面的查询正在进行中，后面的查询将会提前返回。  

参数：  

accountId：string，查询的两融账号 seq：int，查询序列号，建议输入唯一值以便对应结果回调  

示例：  

![](images/850dd8c4c7f4d11467837a64986cceea88c388bd540e394418bad443a7a24541.jpg)  

回调示例 见query_credit_account 在新窗口打开  

# #query_credit_opvolume - 查询两融最大可下单量  

# 注意  

1. 本函数一次最多查询200 只股票的两融最大下单量，且同时只能有一个查询,如果前面的查询正在进行中,后面的查询将会提前返回。本函数从服务器查询数据,建议平均查询时间间隔180s 一次,不可频繁调用。  

2. 该函数必须配合credit_opvolume_callback 回调才能使用,关于此回调的说明请看credit_account_callback 在新窗口打开  

调用query_credit_opvolume，该接口的查询结果将会推送给  

credit_opvolume_callback，所以必须配合credit_opvolume_callback 回调才能使用  

用  

法： query_credit_opvolume(accountId,stockCode,opType,prType,price,seq,ContextInfo)  

释义： 查询两融最大可下单量。  

# 参数：  

accountId:查询的两融账号  
• stockCode:需要查询的股票代码,stockCode 为List 的类型,可以查询多只股票opType:两融下单类型,同passorder 的下单类型  
• prType:报单价格类型,同passorder 的报价类型  
• seq:查询序列号,int 型，建议输入唯一值以便对应结果回调price:报价(非限价单可以填任意值),如果stockCode 为List 类型,报价也需要为长度相同的ListContextInfo:ContextInfo 类  

# 示例：  

python 返回值  

#coding:gbk  

mport time  

def init(ContextInfo): ContextInfo.accid='200133  

if ContextInfo.is_last_bar():#查询accid 账号担保品买入600000,SH 限价10 元的最大可下单量  

query_credit_opvolume(ContextInfo.accid,'600000.SH',33,11,10,int(time.time()),C) #查询两融最大可下单量。  

#查询accid 账号担保品买入600000,SH 限价10 元,000001.SZ 担保品买入限价20 元的最大可下单量  

query_credit_opvolume(ContextInfo.accid,["600000.SH","000001.SZ"],33,11,[10,20],int(time.time()),C) # 查询两融最大可下单量。  

# #get_option_subject_position-取期权标的持仓  

用法： get_option_subject_position(accountID)  

释义： 取期权标的持仓  

参数：  

accountID：string,账号  

返回： list,list 中放的是CLockPosition 在新窗口打开,通过dir(pythonobj)可返回某个对象的属性列表  

示例：  

data=get_option_subject_position('880399990383')   
print(len(data));   
forobjindata: print(obj.m_strInstrumentName,obj.m_lockVol,obj.m_coveredVol);  

#get_comb_option-取期权组合持仓用法： get_comb_option(accountID)  

释义： 取期权组合持仓  

参数：  

accountID：string,账号  

返回： list,list 中放的是CStkOptCombPositionDetail 在新窗口打开,通过dir(pythonobj)可返回某个对象的属性列表  

# 示例：  

obj_list=get_comb_option('880399990383')   
print(len(obj_list));   
forobjinobj_list: print(obj.m_strCombCodeName,obj.m_strCombID,obj.m_nVolume,obj.m_nFrozenVolume)  

# #get_unclosed_compacts-获取未了结负债合约明细  

用法： get_unclosed_compacts(accountID,accountType)  

释义： 获取未了结负债合约明细  

# 参数：  

accountID：str，资金账号accountType：str，账号类型，这里应该填'CREDIT'  

返回：  

list([ CStkUnclosedCompacts, ... ]) 负债列表，CStkUnclosedCompacts 属性如下：  

<html><body><table><tr><td>字段名称</td><td>类型</td><td>说明</td></tr><tr><td>m_strAccountID</td><td>string</td><td>账号ID 账号类型</td></tr><tr><td>m_nBrokerType</td><td>int</td><td>1-期货账号 2-股票账号 3-信用账号 5-期货期权账号 6-股票期权账号</td></tr><tr><td></td><td></td><td>7-沪港通账号 11-深港通账号</td></tr><tr><td>m_strExchangeID</td><td>string</td><td>市场</td></tr><tr><td></td><td></td><td></td></tr><tr><td>m_strInstrumentID m_eCompactType</td><td>string int</td><td>证券代码 合约类型 32-不限制</td></tr></table></body></html>  

# 字段名称  

m_nOpenDate  
m_nBusinessVol  
m_nRealCompactVol  
m_nRetEndDate  
m_dBusinessBalance  
m_dBusinessFare  
m_dRealCompactBalance  
m_dRealCompactFare  
m_dRepaidFare  
m_dRepaidBalance  
m_strCompactId  
m_strEntrustNo  
m_nRepayPriority  
m_strPositionStr48-融资49-融券头寸来源32-不限制  
int48-普通头寸49-专项头寸  
int 开仓日期(如'20201231')  
int 合约证券数量  
int 未还合约数量  
int 到期日(如'20201231')  
float 合约金额  
float 合约息费  
float 未还合约金额  
float 未还合约息费  
float 已还息费  
float 已还金额  
string 合约编号  
string 委托编号  
int 偿还优先级  
string 定位串合约展期状态48-可申请49-已申请  
int 50-审批通过51-审批不通过52-不可申请53-已执行  

m_eCompactRenewalStatus  

示例：  


<html><body><table><tr><td>字段名称</td><td>类型</td><td>说明</td></tr><tr><td></td><td></td><td>54-已取消</td></tr><tr><td>m_nDeferTimes</td><td></td><td></td></tr><tr><td></td><td>int</td><td>展期次数</td></tr></table></body></html>  

get_unclosed_compacts('6000000248', 'CREDIT') #get_closed_compacts-获取已了结负债合约明细 用法： get_closed_compacts(accountID,accountType)  

释义： 获取已了结负债合约明细  

# 参数：  

accountID：str，资金账号accountType：str，账号类型，这里应该填'CREDIT'  

返回：  

list([ CStkUnclosedCompacts, ... ]) 负债列表，CStkUnclosedCompacts 属性如下：  

<html><body><table><tr><td>字段名</td><td>类型</td><td>描述</td></tr><tr><td>m_strAccountID</td><td>string</td><td>账号ID</td></tr><tr><td rowspan="6">m_nBrokerType</td><td></td><td>账号类型</td></tr><tr><td></td><td>1-期货账号</td></tr><tr><td></td><td>2-股票账号</td></tr><tr><td></td><td>3-信用账号</td></tr><tr><td>int</td><td>5-期货期权账号</td></tr><tr><td></td><td>6-股票期权账号</td></tr><tr><td></td><td></td><td>7-沪港通账号</td></tr><tr><td></td><td></td><td>11-深港通账号</td></tr><tr><td></td><td></td><td></td></tr></table></body></html>  

m_strExchangeID string 市场  

<html><body><table><tr><td>字段名</td><td>类型</td><td>描述</td></tr><tr><td>m_strInstrumentID</td><td>string</td><td>证券代码</td></tr><tr><td></td><td></td><td>合约类型</td></tr><tr><td>m_eCompactType</td><td></td><td>32-不限制</td></tr><tr><td></td><td>int</td><td>48-融资</td></tr><tr><td></td><td></td><td>49-融券</td></tr><tr><td></td><td></td><td>头寸来源</td></tr><tr><td>m_eCashgroupProp</td><td></td><td>32-不限制</td></tr><tr><td></td><td>int</td><td>48-普通头寸</td></tr><tr><td></td><td></td><td>49-专项头寸</td></tr><tr><td>m_nOpenDate</td><td>int</td><td>开仓日期(如'20201231")</td></tr><tr><td>m_nBusinessVol</td><td>int</td><td>合约证券数量</td></tr><tr><td>m_nRetEndDate</td><td>int</td><td>到期日(如'20201231")</td></tr><tr><td>m_nDateClear</td><td>int</td><td>了结日期(如'20201231")</td></tr><tr><td>m_nEntrustVol</td><td>int</td><td>委托数量</td></tr><tr><td>m_dEntrustBalance</td><td>float</td><td>委托金额</td></tr><tr><td>m_dBusinessBalance</td><td>float</td><td>合约金额</td></tr><tr><td>m_dBusinessFare</td><td>float</td><td>合约息费</td></tr><tr><td>m_dRepaidFare</td><td>float</td><td>已还息费</td></tr><tr><td>m_dRepaidBalance</td><td>float</td><td>已还金额</td></tr><tr><td>m_strCompactId</td><td>string</td><td>合约编号</td></tr><tr><td>m_strEntrustNo</td><td>string</td><td>委托编号</td></tr><tr><td>m_strPositionStr</td><td>string</td><td>定位串</td></tr></table></body></html>  

# #其他交易函数 （仅回测可用）  

警告以下函数仅回测生效，实盘和模拟盘交易均不可用  

# #order_lots-指定手数交易  

用法： order_lots(stockcode, lots[, style, price], ContextInfo[, accId])  

释义： 指定手数交易，指定手数发送买/卖单。如有需要落单类型当做一个参量传入，如果忽略掉落单类型，那么默认以最新价下单。  

参数：  

stockcode：代码，string，如 '000002.SZ'  
lots：手数，int  
style：下单选价类型，string，默认为最新价 'LATEST'，可选值：  
'LATEST'：最新  
'FIX'：指定 选此参数时必须指定有效的price 参数，其他style 值可不用  
传入price 参数  
'HANG'：挂单 用己方盘口挂单，即买入时用盘口买一价下单，卖出时  
用卖一价挂单，  
'COMPETE'：对手  
'MARKET'：市价  
'SALE5', 'SALE4', 'SALE3', 'SALE2', 'SALE1'：卖5-1 价  
'BUY1', 'BUY2', 'BUY3', 'BUY4', 'BUY5'：买1-5 价  
price：价格，double  

ContextInfo：PythonObj，Python 对象，这里必须是 ContextInfo accId：账号，string  

返回： 无  

# 示例：  

def handlebar(ContextInfo):# 按最新价下 1 手买入order_lots('000002.SZ', 1, ContextInfo, '600000248')# 用对手价下 1 手卖出order_lots('000002.SZ', -1, 'COMPETE', ContextInfo, '600000248')# 用指定价 37.5 下 2 手卖出order_lots('000002.SZ', -2, 'fix', 37.5, ContextInfo, '600000248')  

# #order_value-指定价值交易  

用法： order_value(stockcode, value[, style, price], ContextInfo[, accId])  

释义： 指定价值交易，使用想要花费的金钱买入 / 卖出股票，而不是买入 /卖出想要的股数，正数代表买入，负数代表卖出。股票的股数总是会被调整成对应的 100 的倍数（在中国 A 股市场 1 手是 100 股）。当您提交一个卖单时，该方法代表的意义是您希望通过卖出该股票套现的金额，如果金额超出了您所持有股票的价值，那么您将卖出所有股票。需要注意，如果资金不足，该API 将不会创建发送订单。  

# 参数：  

stockcode：代码，string，如 '000002.SZ'  
value：金额（元），double  
style：下单选价类型，string，默认为最新价 'LATEST'，可选值：  
'LATEST'：最新  
'FIX'：指定  
'HANG'：挂单  
'COMPETE'：对手  
'MARKET'：市价  
'SALE5', 'SALE4', 'SALE3', 'SALE2', 'SALE1'：卖5-1 价  
'BUY1', 'BUY2', 'BUY3', 'BUY4', 'BUY5'：买1-5 价  
price：价格，double  
ContextInfo：PythonObj，Python 对象，这里必须是 ContextInfo  
accId：账号，string  

返回： 无  

# 示例：  

def handlebar(ContextInfo):# 按最新价下 10000 元买入order_value('000002.SZ', 10000, ContextInfo, '600000248')# 用对手价下 10000 元卖出order_value('000002.SZ', -10000, 'COMPETE', ContextInfo, '600000248')# 用指定价 37.5 下 20000 元卖出order_value('000002.SZ', -20000, 'fix', 37.5, ContextInfo, '600000248')  

# #order_percent-指定比例交易  

用法： order_percent(stockcode, percent[, style, price], ContextInfo[, accId])  

释义： 指定比例交易，发送一个等于目前投资组合价值（市场价值和目前现金的总和）一定百分比的买 / 卖单，正数代表买，负数代表卖。股票的股数总是  

会被调整成对应的一手的股票数的倍数（1 手是 100 股）。百分比是一个小数，并且小于或等于1（小于等于 $100\%$ ），0.5 表示的是 $50\%$ 。需要注意，如果资金不足，该 API 将不会创建发送订单。  

# 参数：  

stockcode：代码，string，如 '000002.SZ'  
percent：比例，double  
style：下单选价类型，string，默认为最新价 'LATEST'，可选值：  
'LATEST'：最新  
'FIX'：指定  
'HANG'：挂单  
'COMPETE'：对手  
'MARKET'：市价  
'SALE5', 'SALE4', 'SALE3', 'SALE2', 'SALE1'：卖5-1 价  
'BUY1', 'BUY2', 'BUY3', 'BUY4', 'BUY5'：买1-5 价  
price：价格，double  
ContextInfo：PythonObj，Python 对象，这里必须是 ContextInfo  
accId：账号，string  

返回： 无  

# 示例：  

def handlebar(ContextInfo):  

# 按最新价下 5.1% 价  

# #order_target_value-指定目标价值交易  

用法： order_target_value(stockcode, tar_value[, style, price], ContextInfo[,accId])  

释义： 指定目标价值交易，买入 / 卖出并且自动调整该证券的仓位到一个目标价值。如果还没有任何该证券的仓位，那么会买入全部目标价值的证券；如果已经有了该证券的仓位，则会买入 / 卖出调整该证券的现在仓位和目标仓位的价值差值的数目的证券。需要注意，如果资金不足，该API 将不会创建发送订单。  

# 参数：  

stockcode：代码，string，如 '000002.SZ'tar_value：目标金额（元），double，非负数  

style：下单选价类型，string，默认为最新价 'LATEST'，可选值：  
'LATEST'：最新  
'FIX'：指定  
'HANG'：挂单  
'COMPETE'：对手  
'MARKET'：市价  
'SALE5', 'SALE4', 'SALE3', 'SALE2', 'SALE1'：卖5-1 价  

'BUY1', 'BUY2', 'BUY3', 'BUY4', 'BUY5'：买1-5 价  

price：价格，double   
ContextInfo：PythonObj，Python 对象，这里必须是 ContextInfo   
accId：账号，string  

返回： 无  

# 示例：  

def handlebar(ContextInfo):# 按最新价下调仓到 10000 元持仓order_target_value('000002.SZ', 10000, ContextInfo, '600000248')# 用对手价调仓到 10000 元持仓order_target_value('000002.SZ', 10000, 'COMPETE', ContextInfo, '600000248')# 用指定价 37.5 下调仓到 20000 元持仓order_target_value('000002.SZ', 20000, 'fix', 37.5, ContextInfo, '600000248')  

# #order_target_percent-指定目标比例交易  

用法： order_target_percent(stockcode, tar_percent[, style, price],ContextInfo[, accId])  

释义： 指定目标比例交易，买入 / 卖出证券以自动调整该证券的仓位到占有一个指定的投资组合的目标百分比。投资组合价值等于所有已有仓位的价值和剩余现金的总和。买 / 卖单会被下舍入一手股数（A 股是 100 的倍数）的倍数。目标百分比应该是一个小数，并且最大值应该小于等于1，比如 0.5 表示$50\%$ ，需要注意，如果资金不足，该API 将不会创建发送订单。  

# 参数：  

stockcode：代码，string，如 '000002.SZ'tar_percent：目标百分比 $[0\sim1]$ ，double  

style：下单选价类型，string，默认为最新价 'LATEST'，可选值：'LATEST'：最新'FIX'：指定'HANG'：挂单'COMPETE'：对手'MARKET'：市价'SALE5', 'SALE4', 'SALE3', 'SALE2', 'SALE1'：卖5-1 价'BUY1', 'BUY2', 'BUY3', 'BUY4', 'BUY5'：买1-5 价  
price：价格，doubleContextInfo：PythonObj，Python 对象，这里必须是 ContextInfo  
accId：账号，string  

返回： 无  

# 示例：  

def handlebar(ContextInfo):# 按最新价下买入调仓到 5.1% 持仓order_target_percent('000002.SZ', 0.051, ContextInfo, '600000248')# 用对手价调仓到 5.1% 持仓order_target_percent('000002.SZ', 0.051, 'COMPETE', ContextInfo, '600000248')# 用指定价 37.5 调仓到 10.2% 持仓order_target_percent('000002.SZ', 0.102, 'fix', 37.5, ContextInfo, '600000248')  

# #order_shares-指定股数交易  

用法： order_shares(stockcode, shares[, style, price], ContextInfo[, accId])  

释义： 指定股数交易，指定股数的买 / 卖单,最常见的落单方式之一。如有需要落单类型当做一个参量传入，如果忽略掉落单类型，那么默认以最新价下单。  

# 参数：  

stockcode：代码，string，如 '000002.SZ'  
shares：股数，int  
style：下单选价类型，string，默认为最新价 'LATEST'，可选值：  
'LATEST'：最新  
'FIX'：指定  
'HANG'：挂单  
'COMPETE'：对手  
'MARKET'：市价  
'SALE5', 'SALE4', 'SALE3', 'SALE2', 'SALE1'：卖5-1 价  
'BUY1', 'BUY2', 'BUY3', 'BUY4', 'BUY5'：买1-5 价  
price：价格，double  
ContextInfo：PythonObj，Python 对象，这里必须是 ContextInfo  
accId：账号，string  

返回： 无  

# 示例：  

![](images/b15ef2d5303d78d5db22b7bb064a265318184b63cf2468a3737957252f72216b.jpg)  

# #buy_open-期货买入开仓  

用法： buy_open(stockcode, amount[, style, price], ContextInfo[, accId])  

释义： 期货买入开仓  

# 参数：  

stockcode：代码，string，如 'IF1805.IF'  
amount：手数，int  
style：下单选价类型，string，默认为最新价 'LATEST'，可选值：  
'LATEST'：最新  
'FIX'：指定  
'HANG'：挂单  
'COMPETE'：对手  
'MARKET'：市价  
'SALE1'：卖一价  
'BUY1'：买一价  
price：价格，double  
ContextInfo：PythonObj，Python 对象，这里必须是 ContextInfo  
accId：账号，string  

返回： 无示例：  

def handlebar(ContextInfo):# 按最新价 1 手买入开仓buy_open('IF1805.IF', 1, ContextInfo, '110476')# 用对手价 1 手买入开仓buy_open('IF1805.IF', 1, 'COMPETE', ContextInfo, '110476')# 用指定价 3750 元 2 手买入开仓buy_open('IF1805.IF', 2, 'fix', 3750, ContextInfo, '110476')  

# #buy_close_tdayfirst-期货买入平仓 （平今优先）  

用法： buy_close_tdayfirst(stockcode, amount[, style, price], ContextInfo[,accId])  

释义： 期货买入平仓，平今优先  

# 参数：  

stockcode：代码，string，如 'IF1805.IF'  
amount：手数，int  
style：下单选价类型，string，默认为最新价 'LATEST'，可选值：  
'LATEST'：最新  
'FIX'：指定  

'HANG'：挂单'COMPETE'：对手'MARKET'：市价'SALE1'：卖一价'BUY1'：买一价  

price：价格，double   
ContextInfo：PythonObj，Python 对象，这里必须是 ContextInfo   
accId：账号，string  

返回： 无  

# 示例：  

![](images/242c261de9330da9c9d21efe4be081099cfeb53bf7a3e7871924b4564c807042.jpg)  

# #buy_close_ydayfirst-期货买入平仓（平昨优先）  

用法： buy_close_ydayfirst(stockcode, amount[, style, price], ContextInfo[,accId])  

释义： 期货买入开仓，平昨优先  

参数：  

stockcode：代码，string，如 'IF1805.IF' amount：手数，int  

style：下单选价类型，string，默认为最新价 'LATEST'，可选值：  
'LATEST'：最新  
'FIX'：指定  
'HANG'：挂单  
'COMPETE'：对手  
'MARKET'：市价  
'SALE1'：卖一价  
'BUY1'：买一价  

price：价格，double  

ContextInfo：PythonObj，Python 对象，这里必须是 ContextInfo  

accId：账号，string  

返回： 无  

# 示例：  

# #sell_open-期货卖出开仓  

用法： sell_open(stockcode, amount[, style, price], ContextInfo[, accId])  

释义： 期货卖出开仓  

参数：  

stockcode：代码，string，如 'IF1805.IF'  
amount：手数，int  
style：下单选价类型，string，默认为最新价 'LATEST'，可选值：  
'LATEST'：最新  
'FIX'：指定  
'HANG'：挂单  
'COMPETE'：对手  
'MARKET'：市价  
'SALE1'：卖一价  
'BUY1'：买一价  
price：价格，double  
ContextInfo：PythonObj，Python 对象，这里必须是 ContextInfo  
accId：账号，string  

返回： 无示例：  

# #sell_close_tdayfirst-期货卖出平仓（平今优先）  

用法： sell_close_tdayfirst(stockcode, amount[, style, price], ContextInfo[,accId])  

释义： 期货卖出平仓，平今优先  

# 参数：  

stockcode：代码，string，如 'IF1805.IF'  
amount：手数，int  
style：下单选价类型，string，默认为最新价 'LATEST'，可选值：  
'LATEST'：最新  
'FIX'：指定  
'HANG'：挂单  
'COMPETE'：对手  
'MARKET'：市价  
'SALE1'：卖一价  
'BUY1'：买一价  
price：价格，double  
ContextInfo：PythonObj，Python 对象，这里必须是 ContextInfo  
accId：账号，string  

返回： 无示例：  

def handlebar(ContextInfo):# 按最新价下 1 手卖出平仓，平今优先sell_close_tdayfirst('IF1805.IF', 1, ContextInfo, '110476')# 用对手价 1 手卖出平仓，平今优先sell_close_tdayfirst('IF1805.IF', 1, 'COMPETE', ContextInfo, '110476')# 用指定价 3750 元 2 手卖出平仓，平今优先sell_close_tdayfirst('IF1805.IF', 1, 'fix', 3750, ContextInfo, '110476')  

# #sell_close_ydayfirst-期货卖出平仓 （平昨优先）  

用法： sell_close_ydayfirst(stockcode, amount[, style, price], ContextInfo[,accId])  

释义： 期货卖出平仓，平昨优先  

# 参数：  

stockcode：代码，string，如 'IF1805.IF'  
amount：手数，int  
style：下单选价类型，string，默认为最新价 'LATEST'，可选值：  
'LATEST'：最新  
'FIX'：指定  

'HANG'：挂单'COMPETE'：对手'MARKET'：市价'SALE1'：卖一价'BUY1'：买一价  

price：价格，double   
ContextInfo：PythonObj，Python 对象，这里必须是 ContextInfo   
accId：账号，string  

返回： 无  

# 示例：  

def handlebar(ContextInfo):# 按最新价 1 手卖出平仓，平昨优先sell_close_ydayfirst('IF1805.IF', 1, ContextInfo, '110476')# 用对手价 1 手卖出平仓，平昨优先sell_close_ydayfirst('IF1805.IF', 1, 'COMPETE', ContextInfo, '110476')# 用指定价 3750 元 2 手卖出平仓，平昨优先sell_close_ydayfirst('IF1805.IF', 2, 'fix', 3750, ContextInfo, '110476')  

# #[已弃用] get_debt_contract-获取两融负债合约明细  

用法： get_debt_contract(accId)释义： 获取信用账户负债合约明细  

此接口已弃用，替代接口为get_unclosed_compacts（获取未了结负债）和get_closed_compacts（获取已了结负债）  

# 参数：  

accId：信用账户  

返回： list，list 中放的是 PythonObj，通过 dir(pythonobj) 可返回某个对象的属性列表。  

示例：  

def handlebar(ContextInfo): obj_list = get_debt_contract('6000000248') for obj in obj_list: # 输出负债合约名 print(obj.m_strInstrumentName)  

# #get_hkt_exchange_rate-获取沪深港通汇率数据  

用法： get_hkt_exchange_rate(accountID,accountType)  

释义： 获取沪深港通汇率数据  

参数：  

accountID：string,账号；accountType:string,账号类型,必须填HUGANGTONG 或者SHENGANGTONG返回：  

dict,字段释义：  

bidReferenceRate:买入参考汇率 askReferenceRate:卖出参考汇率 dayBuyRiseRate:日间买入参考汇率浮动比例 daySaleRiseRate:日间卖出参考汇率浮动比例  

示例：  

# 实时主推函数  

# #account_callback - 资金账号状态变化主推  

# 提示  

1. 仅在实盘运行模式下生效。  
2.  需要先在init 里调用ContextInfo.set_account 后生效。  

用法： account_callback(ContextInfo, accountInfo)  

释义： 当资金账号状态有变化时，这个函数被客户端调用  

# 参数：  

ContextInfo：特定对象 accountInfo：账号对象在新窗口打开或信用账号对象在新窗口打开  

返回： 无  

# 示例：  

示例返回值  

# #task_callback - 账号任务状态变化主推  

# 提示  

1. 仅在实盘运行模式下生效。  
2.  需要先在init 里调用ContextInfo.set_account 后生效。  

用法： task_callback(ContextInfo, taskInfo)  

释义： 当账号任务状态有变化时，这个函数被客户端调用  

参数：  

ContextInfo：特定对象taskInfo 任务对象在新窗口打开  

返回： 无  

# 示例：  

示例返回值  

#coding:gbk   
def show_data(data): tdata = {} for ar in dir(data): if ar[:2] != 'm_':continue try: tdata[ar] = data.__getattribute__(ar)  

![](images/199b094b5269f142680af23ab0e710555fa69bed451c9ac9545c2d04c2f59ea0.jpg)  

# #order_callback - 账号委托状态变化主推  

# 提示  

1. 仅在实盘运行模式下生效。  
2.  需要先在init 里调用ContextInfo.set_account 后生效。  

用法： order_callback(ContextInfo, orderInfo)  

释义： 当账号委托状态有变化时，这个函数被客户端调用  

# 参数：  

ContextInfo：特定对象 orderInfo：委托在新窗口打开  

返回： 无  

# 示例：  

示例返回值  

def show_data(data):  

![](images/7329bfcd717ba9263006e82eea041e903207b9f20a3f1c1630342524bbad9bdd.jpg)  

# #deal_callback - 账号成交状态变化主推  

提示  

1. 仅在实盘运行模式下生效。  
2.  需要先在init 里调用ContextInfo.set_account 后生效。  

用法： deal_callback(ContextInfo, dealInfo)  

释义： 当账号成交状态有变化时，这个函数被客户端调用  

参数：  

ContextInfo：特定对象 dealInfo：成交在新窗口打开  

返回： 无  

# 示例：  

示例返回值  

![](images/c5f92c47c4892742442b165d6c9597a37dee7f56465eb3d0c170b1da46db9c57.jpg)  

# #position_callback - 账号持仓状态变化主推  

# 提示  

1. 仅在实盘运行模式下生效。  
2. 需要先在init 里调用ContextInfo.set_account 后生效。  

用法： position_callback(ContextInfo, positonInfo)  

释义： 当账号持仓状态有变化时，这个函数被客户端调用  

参数：  

ContextInfo：特定对象  

positonInfo：持仓在新窗口打开  

返回： 无  

示例：  

示例返回值  

![](images/3d3eb76a3d740a15acd7d6856b754ad05a536451cd496a647cca5c3d9eb9c9f0.jpg)  

# #orderError_callback - 账号异常下单主推  

提示  

1. 仅在实盘运行模式下生效。  
2.  需要先在init 里调用ContextInfo.set_account 后生效。  

用法： orderError_callback(ContextInfo,orderArgs,errMsg)  

释义： 当账号下单异常时，这个函数被客户端调用  

参数：  

ContextInfo：特定对象  
orderArgs：下单参数在新窗口打开  
errMsg：错误信息  

返回： 无  

# 示例：  

# 示例返回值  

def show_data(data): tdata = {} for ar in dir(data): if ar[:2] != 'm_':continue try: tdata[ar] = data.__getattribute__(ar) except: tdata[ar] = '<CanNotConvert>' return tdata  

def init(ContextInfo): # 设置对应的资金账号 # 示例需要在策略交易界面运行 ContextInfo.set_account(account)  

def after_init(ContextInfo):# 在策略交易界面运行时，account 的值会被赋值为策略配置中的账号，编辑器界面运行  
时，需要手动赋值# 编译器界面里执行的下单函数不会产生实际委托passorder(23, 1101, account, "000001.SZ", 11, 0, 100, "示例", 2, "投资备注",ContextInfo)  

# #其他主推函数  

# #credit_account_callback - 查询信用账户明细回调  

用法： credit_account_callback(ContextInfo,seq,result)  

释义： 查询信用账户明细回调  

# 参数：  

ContextInfo：策略模型全局对象  

seq:query_credit_account 时输入查询seq result: 信用账户明细在新窗口打开  

# #credit_opvolume_callback - 查询两融最大可下单量的回 调  

用法： credit_opvolume_callback(ContextInfo,accid,seq,ret,result)  

释义： 查询两融最大可下单量的回调。  

# 参数：  

ContextInfo：策略模型全局对象  

accid:查询的账号  
seq:query_credit_opvolume 时输入查询seq  
ret:查询结果状态。正常返回:1,正在查询中-1,输入账号非法:-2,输入查询参数非法:-3,  
超时等服务器返回报错:-4  
result:查询到的结果  

示例 见query_credit_opvolume  

# ext_data - 获取扩展数据  

获取扩展数据  

调用方法：ext_data(extdataname, stockcode, deviation, ContextInfo)  

# 参数：  

<html><body><table><tr><td>参数名</td><td>类型</td><td>说明</td><td>提示</td></tr><tr><td>extdataname</td><td>string</td><td>扩展数据 名</td><td></td></tr><tr><td>stockcode</td><td>string</td><td>证券代码</td><td>形式如‘600000.SH'</td></tr><tr><td>deviation</td><td>number</td><td>K 线偏移</td><td>0:不偏移，N:向右偏移N，-N:向 左偏移 N</td></tr><tr><td>ContextInfo</td><td>pythonObj</td><td>Python对 象</td><td>ython 对象，这里必须是 Contextlnfo</td></tr><tr><td></td><td></td><td></td><td></td></tr><tr><td>返回：</td><td>number</td><td></td><td></td></tr><tr><td></td><td></td><td></td><td></td></tr></table></body></html>  

\*\* 示例：\*\*  

#coding:gbk  

def init(ContextInfo): print(ext_data('CR', '600000.SH', 0, ContextInfo))  

#ext_data_rank - 获取引用的扩展数据的数值在所有品种中的排名  

获取引用的扩展数据的数值在所有品种中的排名  

调用方法：ext_data_rank(extdataname, stockcode, deviation, ContextInfo)  

参数：  

<html><body><table><tr><td>参数名</td><td>类型</td><td>说明</td><td>提示</td></tr><tr><td>extdataname</td><td>string</td><td>扩展数据 名</td><td></td></tr><tr><td>stockcode</td><td>string</td><td>证券代码</td><td>形式如‘600000.SH'</td></tr><tr><td>deviation</td><td>number</td><td>K 线偏移</td><td>0：不偏移，N:向右偏移N，-N:向 左偏移 N</td></tr></table></body></html>  

返回： number  


<html><body><table><tr><td>参数名</td><td>类型</td><td>说明</td><td>提示</td></tr><tr><td></td><td></td><td>Python 对</td><td>ython 对象 这里必须是</td></tr><tr><td>ContextInfo</td><td>pythonObj</td><td>象</td><td></td></tr><tr><td></td><td></td><td></td><td>Contextlnfo</td></tr></table></body></html>  

\*\* 示例：\*\*  

def init(ContextInfo): print(ext_data_rank('mycci', '600000.SH', 0, ContextInfo))  

#ext_data_rank_range - 获取引用的扩展数据的数值在指定时间区间内所有品种中的排名  

获取引用的扩展数据的数值在指定时间区间内所有品种中的排名  

\*\* 调用方法： \*\*ext_data_rank_range(extdataname, stockcode, begintime, endtime,ContextInfo)  

参数：  
返回： pythonDict  


<html><body><table><tr><td>参数名</td><td>类型</td><td>说明</td><td>提示</td></tr><tr><td>extdataname</td><td>string</td><td>扩展数据名</td><td></td></tr><tr><td>stockcode</td><td>string</td><td>证券代码</td><td>形式如'600000.SH'</td></tr><tr><td>begintime</td><td>string</td><td>区间的起始 时间</td><td>格式为'2016-08-0212:12:30'（包括 该时间点在内)</td></tr><tr><td>endtime</td><td>string</td><td>区间的结束 时间</td><td>格式为'2017-08-0212:12:30' （包 括该时间点在内)</td></tr><tr><td>ContextInfo</td><td>pythonObj</td><td>Python 对象</td><td>Python对象，这里必须是 Contextlnfo</td></tr></table></body></html>  

\*\* 示例：\*\*  

# #coding:gbk  

def init(ContextInfo): print(ext_data_rank_range('mycci', '600000.SH','2022-08-02 12:12:30', '2023-08-02   
12:12:30', ContextInfo))  

# #ext_data_range - 获取扩展数据在指定时间区间内的值  

获取扩展数据在指定时间区间内的值  

调用方法：ext_data_range(extdataname, stockcode, begintime, endtime, ContextInfo)参数：  

<html><body><table><tr><td>参数名</td><td>类型</td><td>说明</td><td>提示</td></tr><tr><td>extdataname</td><td>string</td><td>扩展数据名</td><td></td></tr><tr><td>stockcode</td><td>string</td><td>证券代码</td><td>形式如'600000.SH'</td></tr><tr><td>begintime</td><td>string</td><td>区间的起始 时间</td><td>格式为'2016-08-0212:12:30'（包括 该时间点在内)</td></tr><tr><td>endtime</td><td>string</td><td>区间的结束 时间</td><td>格式为'2017-08-0212:12:30' （包 括该时间点在内)</td></tr><tr><td>ContextInfo</td><td>pythonObj</td><td>Python 对象</td><td>Python对象，这里必须是 Contextlnfo</td></tr><tr><td></td><td>返回：pythonDict</td><td></td><td></td></tr></table></body></html>  

# 示例：  

# #coding:gbk  

def init(ContextInfo): print(ext_data_range('mycci', '600000.SH','2022-08-02 12:12:30', '2023-08-02   
12:12:30', ContextInfo))  

# #get_factor_value - 获取因子数据  

获取因子数据  

调用方法：get_factor_value(factorname, stockcode, deviation, ContextInfo)  

参数：  

<html><body><table><tr><td>参数名</td><td>类型</td><td>说明</td><td>提示</td></tr><tr><td>factorname</td><td>string</td><td>因子名称</td><td></td></tr><tr><td>stockcode</td><td>string</td><td>证券代码</td><td>形式如'600000.SH'</td></tr><tr><td>deviation</td><td>number</td><td>K 线偏移</td><td>0不偏移，N 向右偏移 N，-N 向左偏 移N</td></tr><tr><td>ContextInfo</td><td>pythonObj</td><td>Python对 象</td><td>Python 对象，这里必须是 Contextlnfo</td></tr><tr><td></td><td></td><td></td><td></td></tr><tr><td>返回：</td><td></td><td></td><td></td></tr><tr><td></td><td>number</td><td></td><td></td></tr></table></body></html>  

# #coding:gbk  

ef init(ContextInfo):  

print(get_factor_value('zzz', '600000.SH', 0, ContextInfo))  

#get_factor_rank - 获取引用的因子数据的数值在所有品种中排名  

获取引用的因子数据的数值在所有品种中排名  

调用方法：get_factor_rank(factorname, stockcode, deviation, ContextInfo)  

参数：  

<html><body><table><tr><td>参数名</td><td>类型</td><td>说明</td><td>提示</td></tr><tr><td>factorname</td><td>string</td><td>因子名称</td><td></td></tr><tr><td>stockcode</td><td>string</td><td>证券代码</td><td>形式如 600000.SH</td></tr><tr><td>deviation</td><td>number</td><td>K 线偏移</td><td>0不偏移，N向右偏移 N，-N 向左偏 移N</td></tr></table></body></html>  

示例：  


<html><body><table><tr><td>参数名</td><td>类型</td><td>说明</td><td>提示</td></tr><tr><td></td><td></td><td>Python 对</td><td>Python 对象 这里必须是</td></tr><tr><td>ContextInfo</td><td>pythonObj</td><td>象</td><td></td></tr><tr><td></td><td></td><td></td><td>Contextlnfo</td></tr></table></body></html>  

def init(ContextInfo): print(get_factor_rank('zzz', '600000.SH', 0, ContextInfo))  

# #call_vba - 获取引用的 VBA 模型运行的结果  

获取引用的 VBA 模型运行的结果  

# 提示  

注意  

1. 使用该函数时需补充好本地 K 线或分笔数据  

调用方法： call_vba(factorname, stockcode,[period, dividend_type,  

barpos],ContextInfo)  

# 参数：  

<html><body><table><tr><td>参数名</td><td>类型</td><td>说明</td><td>提示</td></tr><tr><td>factorname</td><td>string</td><td>因子名称</td><td></td></tr><tr><td>stockcode</td><td>string</td><td>证券代码</td><td>形式如‘600000.SH'</td></tr><tr><td>period</td><td>string</td><td>K 线偏移</td><td>可缺省，默认为当前主图周期线型</td></tr><tr><td>dividend_type</td><td>string</td><td>复权方式</td><td>可缺省，默认当前图复权方式，具体 可选值如下</td></tr><tr><td>barpos</td><td>number</td><td>对应 bar 下标</td><td>可缺省，默认当前主图调用到的 bar 的对应下标xtlnfo</td></tr><tr><td>ContextInfo</td><td>pythonObj</td><td>Python对 象</td><td>Python对象，这里必须是 Contextlnfo</td></tr></table></body></html>  

• period 可选值：  

'tick'：分笔线 '1d'：日线 '1m'：1 分钟线 '3m'：3 分钟线 '5m'：5 分钟线 '15m'：15 分钟线 '30m'：30 分钟线 '1h'：小时线 '1w'：周线'1mon'：月线 '1q'：季线 '1hy'：半年线 '1y'：年线  

• dividend_type 可选值：  

'none'：不复权 'front'：向前复权 'back'：向后复权 'front_ratio'：等比向前复权 'back_ratio'：等比向后复权  

返回： number  

示例：  

python  

def init(ContextInfo): print(call_vba('MA.ma1', '600036.SH', ContextInfo))  

$@$ tab 返回值  

# opType - 操作类型  

#期货/股指期权/商品期权 - 六键  

数值 描述  

# 数值 描述  

3 开空  
4 平昨空  
5 平今空  

# #期货/股指期权/商品期权 - 四键  

数值 描述  
6 平多, 优先平今  
7 平多, 优先平昨  
8 平空, 优先平今  
9 平空, 优先平昨  

# #期货/股指期权/商品期权 - 两键  

10 卖出, 如有多仓, 优先平仓, 优先平今, 如有余量, 再开空  
11 卖出, 如有多仓, 优先平仓, 优先平昨, 如有余量, 再开空  
12 买入, 如有空仓, 优先平仓, 优先平今, 如有余量, 再开多  
13 买入, 如有空仓, 优先平仓, 优先平昨, 如有余量, 再开多  
14 买入, 不优先平仓  
15 卖出, 不优先平仓  

# #股票/ETF/可转债买卖  

# 数值  

# 描述  

23 股票/ETF/可转债买入，或沪港通、深港通股票买入   
24 股票/ETF/可转债卖出，或沪港通、深港通股票卖出  

# #融资融券  

数值 描述  
27 融资买入  
28 融券卖出  
29 买券还券  
30 直接还券  
31 卖券还款  
32 直接还款  
33 担保品买入  
34 担保品卖出  

# #组合交易  

#  

数值 描述  
25 组合买入，或沪港通、深港通的组合买入  
26 组合卖出，或沪港通、深港通的组合卖出  
27 融资买入  
28 融券卖出  
29 买券还券  
31 卖券还款  
33 担保品买入  
34 担保品卖出  
35 普通账号一键买卖  
36 信用账号一键买卖  
40 期货组合开多  

# 数值 描述  

43 期货组合开空  
46 期货组合平多, 优先平今  
47 期货组合平多, 优先平昨  
48 期货组合平空, 优先平今  
49 期货组合平空, 优先平昨  

# #ETF 期权交易  

# 数值 描述  

50 买入开仓  
51 卖出平仓  
52 卖出开仓  
53 买入平仓  
54 备兑开仓  
55 备兑平仓  
56 认购行权  
57 认沽行权  
58 证券锁定  
59 证券解锁  

# #ETF 申赎交易  

# 数值 描述  

60 申购   
61 赎回  

# #专项两融  

数值 描述  
70 专项融资买入  
71 专项融券卖出  
72 专项买券还券  
73 专项直接还券  
74 专项卖券还款  
75 专项直接还款  

# #可转债转股/回售  

数值 描述  
80 普通账户转股  
81 普通账户回售  
82 信用账户转股  
83 信用账户回售  

# #orderType - 下单方式  

提示  

注意  

一、期货不支持 1102 和 1202  

二、对所有账号组的操作相当于对账号组里的每个账号做一样的操作，如：  

1.  passorder(23, 1202, 'testS', '000001.SZ', 5, -1, 50000, ContextInfo)，意思就是对账号组testS 里的所有账号都以最新价开仓买入 50000 元市值的 000001.SZ 平安银行；  

2.  passorder (60,1101,"test",'510050. SH', 5,-1,1, ContextInfo)意思就是账号test 申购1 个 单位 (900000 股)的华夏上证50ETF (只申购不买入成分股)。  

# #单股交易  

# 数值  

# 描述  

1101 单股、单账号、普通、股/手方式下单  
1102 单股、单账号、普通、金额（元）方式下单（只支持股票）  
1113 单股、单账号、总资产、比例 [0 \~ 1] 方式下单  
1123 单股、单账号、可用、比例[0 \~ 1]方式下单  

# #单股交易 （账号组）  

# 数值  

# 描述  

1201 单股、账号组（无权重）、普通、股/手方式下单  
1202 单股、账号组（无权重）、普通、金额（元）方式下单（只支持股票）  
1213 单股、账号组（无权重）、总资产、比例 [0 \~ 1] 方式下单  
1223 单股、账号组（无权重）、可用、比例 [0 \~ 1] 方式下单  

# #组合交易 （单账号）  

# 数值  

# 描述  

组合、单账号、普通、按组合股票数量（篮子中股票设定的数量）方式下单 >  
2101对应 volume 的单位为篮子的份组合、单账号、普通、按组合股票权重（篮子中股票设定的权重）方式下单 $>$   
2102对应 volume 的单位为元组合、单账号、普通、按账号可用方式下单 $>$ （底层篮子股票怎么分配？  
2103 答：按可用资金比例后按篮子中股票权重分配，如用户没填权重则按相等权重分配）只对股票篮子支持  

# #组合交易 （账号组）  

# 数值  

# 描述  

2201 组合、账号组（无权重）、普通、按组合股票数量方式下单  
2202 组合、账号组（无权重）、普通、按组合股票权重方式下单  

# 数值  

2203 组合、账号组（无权重）、普通、按账号可用方式下单只对股票篮子支持  

# #prType - 下单选价类型  

关于使用市价指令的说明  

1. 对于上交所（42,43,44,45）  

1. 当prType 选择市价类型时时，price 为保护限价，范围为（0 - 9999）表示投资者能够接受的最高买入价或最低卖出价，即买入申报的成交价格和转限价的价格不高于保护限价，卖出申报的成交价格和转限价的价格不低于保护限价，当price 指定为 0 时，保护限价为对应的涨跌停价  
2. 融券卖出不允许使用市价指令  
3. 集合竞价阶段不允许使用市价指令  

2. 对于深交所（44,45,46,47,48）  

1. 市价申报只适用于有价格涨跌幅限制证券。  
2. 集合竞价阶段不允许使用市价指令  

3. 对于北交所(42,43,44,45)  

1. 当prType 选择市价类型时时，price 为保护限价，范围为（0 - 9999）表示投资者能够接受的最高买入价或最低卖出价，即买入申报的成交价格和转限价的价格不高于保护限价，卖出申报的成交价格和转限价的价格不低于保护限价，当price 指定为 0 时，保护限价为对应的涨跌停价  

2. 融券卖出不允许使用市价指令  
3. 集合竞价阶段不允许使用市价指令  

# 数值  

# 描述  

-1 无效(只对于algo_passorder 起作用)  

0 卖5 价   
1 卖4 价   
2 卖3 价   
3 卖2 价   
4 卖1 价  

# 数值  

描述  

5 最新价  
6 买1 价  
7 买2 价(组合不支持)  
8 买3 价(组合不支持)  
9 买4 价(组合不支持)  
10 买5 价(组合不支持)  
11 指定价（只对单股情况支持,对组合交易不支持）  
12 涨跌停价(对手方最远端价格)  
13 挂单价(本方一档价格)  
14 对手价(对方一档价格)  
18 市价最优价[郑商所][期货]  
19 市价即成剩撤[大商所][期货]  
20 市价全额成交或撤[大商所][期货]  
21 市价最优一档即成剩撤[中金所][期货]  
22 市价最优五档即成剩撤[中金所][期货]  
23 市价最优一档即成剩转[中金所][期货]  
24 市价最优五档即成剩转[中金所][期货]  
26 限价即时全部成交否则撤单[上交所[期权]] [深交所[期权]]  
27 市价即成剩撤[上交所][期权]  
28 市价即全成否则撤[上交所][期权]  
29 市价剩转限价[上交所][期权]  
42 最优五档即时成交剩余撤销申报[上交所[股票]][北交所[股票]]  

# 描述  

43 最优五档即时成交剩转限价申报[上交所[股票]][北交所[股票]]  
44 对手方最优价格委托[上交所[股票]][深交所[股票][北交所[股票]][期权]]  
45 本方最优价格委托[上交所[股票]][深交所[股票][北交所[股票]][期权]]  
46 即时成交剩余撤销委托[深交所][股票][期权]  
47 最优五档即时成交剩余撤销委托[深交所][股票][期权]  
48 全额成交或撤销委托[深交所][股票][期权]  
49 盘后定价  

# #volume - 下单数量  

提示根据 orderType 值最后一位确定 volume 的单位  

# #单股下单时  

# 数值  

# 描述  

1 股 / 手 （股票: 股，股票期权: 张，期货: 手，可转债: 张，基金：份）  
2 金额（元）  
3 比例（%）  

# #组合下单时  

数值 描述  

1 按组合股票数量（份）  
2 按组合股票权重（元）  
3 按账号可用（%）  

# #quicktrade - 快速下单  

数值 描述0 否1 是2 是  

提示  

passorder 是对最后一根K 线完全走完后生成的模型信号在下一根K 线的第一个tick 数据来时触发下单交易；  

采用quickTrade 参数设置为1 时，非历史 bar 上执行时（ContextInfo.is_last_bar()为True），只要策略模型中调用到就触发下单交易。  

quickTrade 参数设置为2 时，不判断 bar 状态，只要策略模型中调用到就触发下单交易，历史 bar 上也能触发下单，请谨慎使用。  

# #enum_ - 对象属性状态字段释义  

# #enum EEntrustBS - 买卖方向  

<html><body><table><tr><td>变量</td><td>数值</td><td>描述</td></tr><tr><td>ENTRUST_BUY</td><td>48</td><td>买入，多</td></tr><tr><td>ENTRUST_SELL</td><td>49</td><td>卖出，空</td></tr><tr><td>ENTRUST_PLEDGE_IN</td><td>81</td><td>质押入库</td></tr><tr><td>ENTRUST_PLEDGE_OUT</td><td>66</td><td>质押出库</td></tr></table></body></html>  

# #EEntrustSubmitStatus - 报单状态  

数值 描述  
48 已经提交  
49 撤单已经提交  
50 修改已经提交  
51 已经接受  
52 报单已经被拒绝  
53 撤单已经被拒绝  
54 改单已经被拒绝  

# #enum_EEntrustTypes - 委托类型  

变量名称 数 描述 值 ENTRUST_BUY_SELL 48 买卖 ENTRUST_QUERY 49 查询 ENTRUST_CANCE 50 撤单 ENTRUST_APPEND 51 补单 ENTRUST_COMFIRM 52 确认 ENTRUST_BIG 53 大宗 ENTRUST_FIN 54 融资委托 ENTRUST_SLO 55 融券委托 ENTRUST_CLOSE 56 信用平仓 ENTRUST_CREDIT_NORMAL 57 信用普通委托 ENTRUST_CANCEL_OPEN 58 撤单补单  

<html><body><table><tr><td>变量名称</td><td>值</td><td>描述</td></tr><tr><td>ENTRUST_TYPE_OPTION_EXERCISE</td><td>59</td><td>行权</td></tr><tr><td>ENTRUST_TYPE_OPTION_SECU_LOCK</td><td>60</td><td>锁定</td></tr><tr><td>ENTRUST_TYPE_OPTION_SECU_UNLOCK</td><td>61</td><td>解锁</td></tr><tr><td>ENTRUST_QUOTATION_REPURCHASE</td><td>62</td><td>报价回购</td></tr><tr><td>ENTRUST_TYPE_OPTION_ABANDON</td><td>63</td><td>放弃行权</td></tr><tr><td>ENTRUST_AGREEMENT_REPURCHASE</td><td>64</td><td>协议回购</td></tr><tr><td>ENTRUST_TYPE_OPTION_COMB_EXERCISE</td><td>65</td><td>组合行权</td></tr><tr><td>ENTRUST_TYPE_OPTION_BUILD_COMB_STRATEGY</td><td>66</td><td>构建组合策略持仓</td></tr><tr><td>ENTRUST_TYPE_OPTION_RELEASE_COMB_STRATEGY</td><td>67</td><td>解除组合策略持仓</td></tr><tr><td>ENTRUST_TYPE_LMT_LOAN</td><td>68</td><td>转融通出借</td></tr><tr><td>ENTRUST_TYPE_LMT_LOAN_DEFER</td><td>69</td><td>转融通出借展期</td></tr><tr><td>ENTRUST_TYPE_LMT_LOAN_FINISH_AHEAD</td><td>70</td><td>转融通出借提前了 结</td></tr><tr><td>ENTRUST_CROSS_MARKET_IN</td><td>71</td><td>跨市场场内</td></tr><tr><td>ENTRUST_CROSS_MARKET_OUT</td><td>72</td><td>跨市场场外</td></tr></table></body></html>  

# #enum_EEntrustStatus - 委托状态  

ENTRUST_STATUS_WAIT_REPORTING 49 待报  
ENTRUST_STATUS_REPORTED 50 已报（已报出到柜台，待成交）已报待撤（对已报状态的委托撤单  
ENTRUST_STATUS_REPORTED_CANCEL 51吗，等待柜台处理撤单请求）  
ENTRUST_STATUS_PARTSUCC_CANCEL 52 部成待撤（已报到柜台，已有部分  

# 变量名称  

ENTRUST_STATUS_PART_CANCEL ENTRUST_STATUS_CANCELED ENTRUST_STATUS_PART_SUCC ENTRUST_STATUS_SUCCEEDED  

成交，已发出对剩余部分的撤单，待柜台处理撤单请求）部撤（已报到柜台，已有部分成交，  
53剩余部分已撤）  
54 已撤  
55 部成（已报到柜台，已有部分成交）  
56 已成废单（不符合报单条件，委托被打  
57 回，相关信息再委托的废单原因字段查看）  

ENTRUST_STATUS_JUNK  

![](images/f7968ea302b9b84f81d7cd9fefdc84ab74d75a61e66aeea3dac523974fc305c6.jpg)  

# #enum_ EHedge_Flag_Type - 投保类型  

变量名称 数值 描述  

HEDGE_FLAG_SPECULATION 49 投机HEDGE_FLAG_ARBITRAGE 50 利利HEDGE_FLAG_HEDGE 51 利保  

# #enum_EFutureTradeType - 成交类型  

变量名称 数值 描述FUTRUE_TRADE_TYPE_COMMON 48 普通成交FUTURE_TRADE_TYPE_OPTIONSEXECUTION 49 期权成交FUTURE_TRADE_TYPE_OTC 50 OTC 成交FUTURE_TRADE_TYPE_EFPDIRVED 51 期转现衍生成交FUTURE_TRADE_TYPE_COMBINATION_DERIVED 52 组合衍生成交  

# #enum_EBrokerPriceType - 价格类型  

<html><body><table><tr><td>变量名称</td><td>值</td><td>描述</td></tr><tr><td>BROKER_PRICE_ANY</td><td>49</td><td>市价</td></tr><tr><td>BROKER_PRICE_LIMIT</td><td>50</td><td>限价</td></tr><tr><td>BROKER_PRICE_BEST</td><td>51</td><td>最优价</td></tr><tr><td>BROKER_PRICE_PROP_ALLOTMENT</td><td>52</td><td>配股</td></tr><tr><td>BROKER_PRICE_PROP_REFER</td><td>53</td><td>转托</td></tr><tr><td>BROKER_PRICE_PROP_SUBSCRIBE</td><td>54</td><td>申购</td></tr><tr><td>BROKER_PRICE_PROP_BUYBACK</td><td>55</td><td>回购</td></tr><tr><td>BROKER_PRICE_PROP_PLACING</td><td>56</td><td>配售</td></tr><tr><td>BROKER_PRICE_PROP_DECIDE</td><td>57</td><td>指定</td></tr><tr><td>BROKER_PRICE_PROP_EQUITY</td><td>58</td><td>转股</td></tr><tr><td>BROKER_PRICE_PROP_SELLBACK</td><td>59</td><td>回售</td></tr><tr><td>BROKER_PRICE_PROP_DIVIDEND</td><td>60</td><td>股息</td></tr><tr><td>BROKER_PRICE_PROP_SHENZHEN_PLACING</td><td>68</td><td>深圳配售确认</td></tr></table></body></html>  

# 变量名称  

# 数 值  

BROKER_PRICE_PROP_CANCEL_PLACING  
BROKER_PRICE_PROP_WDZY  
BROKER_PRICE_PROP_DJZY  
BROKER_PRICE_PROP_WDJY  
BROKER_PRICE_PROP_JDJY  
BROKER_PRICE_PROP_ETF  
BROKER_PRICE_PROP_VOTE  
BROKER_PRICE_PROP_YYSGYS  
BROKER_PRICE_PROP_YSYYJC  
BROKER_PRICE_PROP_FUND_DEVIDEND  
BROKER_PRICE_PROP_FUND_ENTRUST  
BROKER_PRICE_PROP_CROSS_MARKET  
BROKER_PRICE_PROP_EXERCIS  
BROKER_PRICE_PROP_PEER_PRICE_FIRST  
BROKER_PRICE_PROP_L5_FIRST_LIMITPX  
BROKER_PRICE_PROP_MIME_PRICE_FIRST  
BROKER_PRICE_PROP_INSTBUSI_RESTCANCEL  
BROKER_PRICE_PROP_L5_FIRST_CANCEL  
BROKER_PRICE_PROP_FULL_REAL_CANCEL  
BROKER_PRICE_PROP_DIRECT_SECU_REPAY  
值  
69 配售放弃  
70 无冻质押  
71 冻结质押  
72 无冻解押  
73 解冻解押  
81 ETF 申购  
75 投票  
92 要约收购预售  
77 预售要约解除  
78 基金设红  
79 基金申赎  
80 跨市转托  
83 权证行权  
84 对手方最优价格最优五档即时成  
85 交剩余转限价  
86 本方最优价格即时成交剩余撤  
87销最优五档即时成  
88交剩余撤销  
89 全额成交并撤单  
101 直接还券  

<html><body><table><tr><td>变量名称</td><td>数 值</td><td>描述</td></tr><tr><td>BROKER_PRICE_PROP_FUND_CHAIHE</td><td>90</td><td>基金拆合</td></tr><tr><td>BROKER_PRICE_PROP_DEBT_CONVERSION</td><td>91</td><td>债转股</td></tr><tr><td>BROKER_PRICE_BID_LIMIT</td><td>92</td><td>港股通竞价限价</td></tr><tr><td>BROKER_PRICE_ENHANCED_LIMIT</td><td>93</td><td>港股通增强限价</td></tr><tr><td>BROKER_PRICE_RETAIL_LIMIT</td><td>94</td><td>港股通零股限价</td></tr><tr><td>BROKER_PRICE_PROP_INCREASE_SHARE</td><td></td><td>增发</td></tr><tr><td>BROKER_PRICE_PROP_COLLATERAL_TRANSFER</td><td>107</td><td>担保品划转</td></tr><tr><td>BROKER_PRICE_PROP_NEEQ_PRICING</td><td>'w'</td><td>定价(全国股转- 挂牌公司交易- 协议转让)</td></tr><tr><td>BROKER_PRICE_PROP_NEEQ_MATCH_CONFIRM</td><td>'x'</td><td>成交确认(全国股 转－挂牌公司交 易 － 协议转让)</td></tr><tr><td>BROKER_PRICE_PROP_NEEQ_MUTUAL_MATCH_CONFIRM</td><td></td><td>互报成交确认(全 国股转－挂牌公 司交易－协议转 让)</td></tr><tr><td>BROKER_PRICE_PROP_NEEQ_LIMIT</td><td>'z'</td><td>限价（用于挂牌公 司交易－做市转 让－限价买卖和 两网及退市交易- 限价买卖)</td></tr><tr><td>enum_Eoffset_Flag_Type－操作类型</td><td></td><td></td></tr></table></body></html>  

EOFF_THOST_FTDC_OF_INVALID -1 无效操作EOFF_THOST_FTDC_OF_Open 48 买入，开仓  

EOFF_THOST_FTDC_OF_Close 49 卖出，平仓EOFF_THOST_FTDC_OF_ForceClose 50 强平EOFF_THOST_FTDC_OF_CloseToday 51 平今EOFF_THOST_FTDC_OF_CloseYesterday 52 平昨EOFF_THOST_FTDC_OF_ForceOff 53 强减EOFF_THOST_FTDC_OF_LocalForceClose 54 本地强平EOFF_THOST_FTDC_OF_PLEDGE_IN 81 质押入库EOFF_THOST_FTDC_OF_PLEDGE_OUT 66 质押出库EOFF_THOST_FTDC_OF_ALLOTMENT 67 股票配股  

# #enum_EXTSubjectsStatus - 融资融券状态  

SUBJECTS_STATUS_NORMAL 48 正常SUBJECTS_STATUS_PAUSE 49 暂停SUBJECTS_STATUS_NOT 50 作废  

# #enum_EXTCreditFundCtl - 融资交易控制  

变量名称 数 描述值  
FUND_CTL_ONLY_FIN_BUY 48 只允许融资买入  
FUND_CTL_ONLY_SELL_CASH_REPAY 49 只允许卖券还款  
FUND_CTL_ALL 50 既允许融资买入又允许卖券还款既不允许融资买入又不允许卖券还  
FUND_CTL_NONE 51款  

# #enum_EXTCreditStkCtl - 融券交易控制  

变量名称 数值 描述STK_CTL_ONLY_SLO_SELL 48 只允许融券卖出STK_CTL_ONLY_BUY_SECU_REPAY 49 只允许买券还券STK_CTL_ALL 50 既允许融券卖出又允许买券还券STK_CTL_NONE 51 既不允许融券卖出又不允许买券还券  

# #enum_EXTSloTypeQueryMode - 查询类型  

XT_SLOTYPE_QUERYMODE_NOMARL 48 普通XT_SLOTYPE_QUERYMODE_SPECIAL 49 专项  

# #enum_EXTCompactType - 合约类型  

# 变量名称 数值 描述  

COMPACT_TYPE_ALL 32 不限制COMPACT_TYPE_FIN 48 融资COMPACT_TYPE_SLO 49 融券  

# #enum_EXTCompactStatus - 合约状态  

变量名称 数值 描述COMPACT_STATUS_ALL 32 不限制COMPACT_STATUS_UNDONE 48 未归还COMPACT_STATUS_PART_DONE 49 部分归还COMPACT_STATUS_DONE 50 已归还COMPACT_STATUS_DONE_BY_SELF 51 自行了结COMPACT_STATUS_DONE_BY_HAND 52 手工了结  

变量名称 数值 描述COMPACT_STATUS_NOT_DEBT 53 未形成负债COMPACT_STATUS_EXPIRY 54 合约已过期  

# #enum_EXTCompactBrushSource - 头寸来源  

# 变量名称 数值 描述  

XT_COMPACT_BRUSH_SOURCE_ALL 32 不限制XT_COMPACT_BRUSH_SOURCE_NORMAL 48 普通头寸XT_COMPACT_BRUSH_SOURCE_SPECIAL 49 专项头寸  

# #enum_EXTSpecialAssure - 是否可以用融券资金买入  

ASSURE_USE_SLO_CASH_DISABLE 48 担保品买入不允许使用融券资金ASSURE_USE_SLO_CASH_ENABLE 49 担保品买入允许使用融券资金  

# #enum_EOperationType - 下单操作类型/主要交易类型  

#  

变量名称 数值 述开  
OPT_OPEN_LONG 0多平  
OPT_CLOSE_LONG_HISTORY 昨多平  
OPT_CLOSE_LONG_TODAY 2 今多开  
OPT_OPEN_SHORT 3空  
OPT_CLOSE_SHORT_HISTORY 4 平  

# 变量名称  

述昨空平  
OPT_CLOSE_SHORT_TODAY 5 今空优先  
OPT_CLOSE_LONG_TODAY_FIRST 6 平今多优先  
OPT_CLOSE_LONG_HISTORY_FIRST 7 平昨多平空优  
OPT_CLOSE_SHORT_TODAY_FIRST 8先平今平空优  
OPT_CLOSE_SHORT_HISTORY_FIRST 9先平昨卖出优  
OPT_CLOSE_LONG_TODAY_HISTORY_THEN_OPEN_SHORT 10先平今  
OPT_CLOSE_LONG_HISTORY_TODAY_THEN_OPEN_SHORT 11 卖  

# 变量名称  

出优先平昨买入优  
OPT_CLOSE_SHORT_TODAY_HISTORY_THEN_OPEN_LONG 12 先平今买入优  
OPT_CLOSE_SHORT_HISTORY_TODAY_THEN_OPEN_LONG 13 先平昨平  
OPT_CLOSE_LONG 14多平  
OPT_CLOSE_SHORT 15空开  
OPT_OPEN 16仓平  
OPT_CLOSE 17仓买  
OPT_BUY 18入卖  
OPT_SELL 19出融  
OPT_FIN_BUY 20 资买描变量名称 数值述入融券  
OPT_SLO_SELL 21卖出买券  
OPT_BUY_SECU_REPAY 22还券直接  
OPT_DIRECT_SECU_REPAY 23还券卖券  
OPT_SELL_CASH_REPAY 24还款直  
OPT_DIRECT_CASH_REPAY 25 接还款基金  
OPT_FUND_SUBSCRIBE 26申购基金  
OPT_FUND_REDEMPTION 27赎回基  
OPT_FUND_MERGE 28 金 合并描变量名称 数值述基金  
OPT_FUND_SPLIT 29 分拆质押  
OPT_PLEDGE_IN 30入库质押  
OPT_PLEDGE_OUT 31出库买入开仓（  
OPT_OPTION_BUY_OPEN 32 个股期权交易）卖出平仓（  
OPT_OPTION_SELL_CLOSE 33 个股期权交易）卖  
OPT_OPTION_SELL_OPEN 34出描  
数值述证券解锁（  
41 个股期权交易）协议转让  
42定价买入协议转让  
43 定价卖出协议转让-成  
44交确认买  

# OPT_N3B_CONFIRM_BUY  

描  
数值述协议转让-成  
45交确认卖出协议转让-互报  
6成交确认买入协议转让-互报  
7成交确认卖出全国  
48股  

# 变量名称  

限价买入全国股  
OPT_N3B_LIMIT_PRICE_SELL 49 转-限价卖出期货期  
OPT_FUTURE_OPTION_EXERCISE 50权行权可转  
OPT_CONVERT_BONDS 51 债转股可转  
OPT_SELL_BACK_BONDS 52 债回售股票  
OPT_STK_ALLOTMENT 53配股股  
OPT_STK_INCREASE_SHARE 54 票增  

#  

变量名称 数值述发担保  
OPT_COLLATERAL_TRANSFER_IN 55 品划入担保  
OPT_COLLATERAL_TRANSFER_OUT 56 品划出意向申  
OPT_BLOCK_INTENTION_BUY 57报买入意向申  
OPT_BLOCK_INTENTION_SELL 58报卖出定价申  
OPT_BLOCK_PRICE_BUY 59 报买入定价申  
OPT_BLOCK_PRICE_SELL 60报卖出数值述成交申  
OPT_BLOCK_CONFIRM_BUY 61报买入成交申  
OPT_BLOCK_CONFIRM_SELL 62报卖出盘后定  
OPT_BLOCK_CLOSE_PRICE_BUY 63价买入盘后定  
OPT_BLOCK_CLOSE_PRICE_SELL 64价卖出黄金  
OPT_GOLD_PRICE_DELIVERY_BUY 65 交割买黄金  
OPT_GOLD_PRICE_DELIVERY_SELL 66 交割卖  
OPT_GOLD_PRICE_MIDDLE_BUY 67 黄描变量名称述金中立仓买黄金  
OPT_GOLD_PRICE_MIDDLE_SELL 68 中 立仓卖组合交易  
OPT_COMPOSE_ONEKEY_BUYSELL 69一键买卖组合交易  
OPT_COMPOSE_GGT_BUY 70 港股通买入组合交易  
OPT_COMPOSE_GGT_SELL 71 港股通卖出描变量名称 数值述零股  
OPT_ODD_SELL 72卖出成份  
OPT_ETF_STOCK_BUY 73 股买入成份  
OPT_ETF_STOCK_SELL 74 股卖出场外基  
OPT_OTC_FUND_SUBSCRIBE 200金认购场外基  
OPT_OTC_FUND_PURCHASE 201金申购场外基  
OPT_OTC_FUND_REDEMPTION 202金赎回场  
OPT_OTC_FUND_CONVERT 203 外基  

# 变量名称  

# 数值  

金转换场外基金分  
OPT_OTC_FUND_BONUS_TYPE_UPDATE 204红方式变更场外协  
OPT_OTC_CONTRACTUAL_DEPOSIT 205 议存款场外非  
OPT_OTC_NON_CONTRACTUAL_DEPOSIT 206 协议存款场外协议  
OPT_OTC_CONTRACTUAL_DEPOSIT_ASK 207存款询价场  
OPT_OTC_NON_CONTRACTUAL_DEPOSIT_ASK 208外述非协议存款询价场外非协  
OPT_OTC_NON_CONTRACTUAL_DEPOSIT_CUR 209 议活期存款场外存  
OPT_OTC_DRAW_DEPOSIT 210单支取网下  
OPT_OTC_STOCK_INQUIRY 230询价网下  
OPT_OTC_STOCK_PURCHASE 231申购场外100 转  
OPT_OPTION_NS_DEPOSIT1 账入金描变量名称 数值述场外100 转  
OPT_OPTION_NS_WITHDRAW2 账出金场100 外  
OPT_OPTION_NS_INOUT3 互转ETF100  
OPT_ETF_PURCHASE 申4购ETF100  
OPT_ETF_REDEMPTION 赎5回外100 盘  
OPT_OUTER_BUY6 买入外100 盘  
OPT_OUTER_SELL7 卖出外盘100 可  
OPT_OUTER_CAN_CLOSE_BUY8 平买仓外100 盘  
OPT_OUTER_CAN_CLOSE_SELL9 可平描变量名称 数值述卖仓专项101 融  
OPT_SLO_SELL_SPECIAL0 券卖出专项101 买  
OPT_BUY_SECU_REPAY_SPECIAL 1 券还券专项101 直  
OPT_DIRECT_SECU_REPAY_SPECIAL 2 接还券全国股转-两网及101  
OPT_NEEQ_O3B_LIMIT_PRICE_BUY 退3市交易-限价买入  
OPT_NEEQ_O3B_LIMIT_PRICE_SELL 101 全描  
数值述  
4 国股转-两网及退市交易-限价卖出投行  
101 债  
5 券买入投行  
101 债  
6 券卖出质押式  
101融  
7资回购质  
101 押  
8 式融描数值述券回购质押式101  
OPT_IBANK_BOND_REPAY 融9资购回质押式102  
OPT_IBANK_FUND_RETRIEVE 融0 券购回融102 券  
OPT_INTEREST_FEE1 息费专项102 融  
OPT_FIN_BUY_SPECIAL2 资买入专项102 卖  
OPT_SELL_CASH_REPAY_SPECIAL 3 券还款102 专  
OPT_DIRECT_CASH_REPAY_SPECIAL4 项  

OPT_FUND_PRICE_SELL  

描  
数值述直接还款货币  
102 基  
5 金申购货币  
102 基  
6 金赎回协议转让-  
102 集  
7 合竞价买入协议转让-  
102 集  
8 合竞价卖出  

OPT_N3B_CALL_AUCTION_BUY  

# OPT_N3B_CALL_AUCTION_SELL  

描  
数值述全国股转-  
102 盘  
9 后协议买入全国股转-  
103 盘  
0 后协议卖出ETF  
103利  
1利报价  
103 回  
2 购买入报价回  
103 购  
3 终止续做描变量名称 数值述报价回103 购  
OPT_QUOTATION_REPURCHASE_BEFORE4 提前购回报价回103 购  
OPT_QUOTATION_REPURCHASE_RESERVATION5 购回预约报价回103 购  
OPT_QUOTATION_REPURCHASE_CANCEL6 取消预约成交申103 报  
OPT_BLOCK_CONFIRM_MATCH_BUY7 配对买入成交103  
OPT_BLOCK_CONFIRM_MATCH_SELL 申8报配数值 述对卖出期货期103 权  
OPT_FUTURE_OPTION_ABANDON9 放弃行权一104 键  
OPT_ONEKEY_TRANSFER0 划转一104 键  
OPT_ONEKEY_TRANSFER_IN1 划入一104 键  
OPT_ONEKEY_TRANSFER_OUT 2 划出盘后104 定  
OPT_AFTER_FIX_BUY 3 价买入盘后104  
OPT_AFTER_FIX_SELL 定4 价卖描数值述成交申104  
OPT_AGREEMENT_REPURCHASE_TRANSACTION_DEC_FORWARD 报5正回购成交申104  
OPT_AGREEMENT_REPURCHASE_TRANSACTION_DEC_REVERSE 报6逆回购到104 期  
OPT_AGREEMENT_REPURCHASE_EXPIRE_CONFIRM7 确认提前购104  
OPT_AGREEMENT_REPURCHASE_ADVANCE_REPURCHASE 回8正回购提前购104  
OPT_AGREEMENT_REPURCHASE_ADVANCE_REVERSE 回9逆回购到105 期  
OPT_AGREEMENT_REPURCHASE_EXPIRE_RENEW0 续做  

# 变量名称  

还正回购到期续105  
OPT_AGREEMENT_REPURCHASE_EXPIRE_REVERSE 做1逆回购现105 券  
OPT_TRANSACTION_IN_CASH_BUY2 买入现105 券  
OPT_TRANSACTION_IN_CASH_SELL 3 卖出买断式  
OPT_OUTRIGHT_REPO_FUND_REPURCHASE 105 融4资回购买断式  
OPT_OUTRIGHT_REPO_BOND_REPURCHASE 105 融5券回购买105  
OPT_OUTRIGHT_REPO_BOND_REPAY 断6式描变量名称 数值述融资购回买断式105  
OPT_OUTRIGHT_REPO_FUND_RETRIEVE 融7券购回分105 销  
OPT_DISTRIBUTION_BUYING8 买入固定利率105  
OPT_FIXRATE_TO_FLOATINGRATE 换9 浮动利率浮动利率106  
OPT_FLOATINGRATE_TO_FIXRATE 换0固定利率银106  
OPT_IBANK_TRANSFER_OUT 行1间  

#  

变量名称 数值述转出托管银行间106  
OPT_IBANK_TRANSFER_IN 转2入托管意向申报106  
OPT_AGREEMENT_REPURCHASE_INTENTION_BUY 正3回购买入意向申报106  
OPT_AGREEMENT_REPURCHASE_INTENTION_SELL 正4回购卖出协议回106 购  
OPT_AGREEMENT_REPURCHASE_BIZ_APPLY_CONFIRM5 成交申报描变量名称 数值 述确认协议回购106 成  
OPT_AGREEMENT_REPURCHASE_BIZ_APPLY_REJECT6 交申报拒绝协议回购到106 期  
OPT_AGREEMENT_REPURCHASE_CONTINUE_CONFIRM7 续做申报确认协议回购到106 期  
OPT_AGREEMENT_REPURCHASE_CONTINUE_REJECT8 续做申报拒绝  
OPT_AGREEMENT_REPURCHASE_INTENTION_CHANGE_BONDS 106 协  

# 变量名称  

# 变量名称  

# 变量名称  

描变量名称 数值述优先股107  
OPT_PREFERENCE_SHARES_BIDDING_BUY 竞9 价买入优先股108  
OPT_PREFERENCE_SHARES_BIDDING_SELL 竞0价卖出债券108  
OPT_TOC_BOND 转1 托管基金108  
OPT_TOC_FUND 转2 托管同108 业  
OPT_IBANK_BORROW 3 拆入同108 业  
OPT_IBANK_LOAN 4 拆出拆108  
OPT_IBANK_BORROW_REPAY 入5还  

#  

变量名称 数值 抽述款拆108 出  
OPT_IBANK_LOAN_REPAY6 还款理财108 产  
OPT_FINANCIAL_PRODUCT_BUY7 品申购理财108 产  
OPT_FINANCIAL_PRODUCT_SELL8 品赎回组108 合  
OPT_OPTION_COMB_EXERCISE9 行权构建109 组  
OPT_OPTION_BUILD_COMB_STRATEGY0 合策略解除109 组  
OPT_OPTION_RELEASE_COMB_STRATEGY 1 合策略  
OPT_AGREEMENT_REPURCHASE_REVERSE_STOP_AHEAD_CONFIRM 109 协  

# 变量名称  

# 变量名称  

OPT_AGREEMENT_REPURCHASE_REVERSE_RELEASE_PLEDGE_CONFI 109   
RM 5  

# 变量名称  

描  
数值述理财  
109 产  
8 品认购全国股转-  
109北  
9交所买入全国股转-  
110北  
0交所卖出全国股转-  
110 申  
1 购-询价申报全  
110国  
2股  

# 变量名称  

描  
数值述转-申购-申购申报全国股转-  
110 大  
3 宗交易买入全国股转-  
110 大  
4 宗交易卖出转融通非  
110 约  
5 定出借申报  

# 变量名称  

描  
数值述转融通约  
110定  
6出借申报转融通  
110出  
7 借展期转融通出  
110借  
8提前了结跨市场  
110 ETF  
9 场内申购跨  
111 市  
0 场ETF描变量名称 数值述场内赎回跨市场111 ETF  
OPT_CROSS_MARKET_OUT_ETF_PURCHASE1 场外申购跨市场111 ETF  
OPT_CROSS_MARKET_OUT_ETF_REDEMPTION2 场外赎回券111 源  
OPT_CREDIT_APPOINTMENT3 预约网下申购-111 公  
OPT_OFF_IPO_PUB_PRICE4 开发行询价111 网  
OPT_OFF_IPO_PUB_PURCHASE5 下描  
数值述申购-公开发行申购网下申购-非  
111公  
6开发行询价网下申购-非  
111  
7 7 公开发行申购债  
111 券  
8 回售债  
111券  
9借  

# 变量名称  

描  
数值述贷融入债券  
112 借  
0 贷融出债券借  
112 贷  
1 融入购回债券借  
112 贷  
2 融出购回债券借贷-  
112质  
3 押券置换  
112 融  
4 券  

# 变量名称  

描  
数值 述通-预约融券融入融券通-预  
112约  
5融券融出固收业务-点击  
112 成  
6 交-报价申报买入固收业  
112 务-  
7 点击成交-描  
数值述报价申报卖出固收业务点击成  
12 交-报价确认-买入-确认固收业务点击成  
12 交报价确认-买入-拒绝  

# 变量名称  

描  
数值述固收业务-点击成  
113 交-  
0 报价确认-卖出-确认固收业务-点击成  
113 交-  
1 报价确认-卖出-拒绝固收业  
113务-  
2协商成  

# OPT_FICC_CONSULT_DECLARE_BUY  

描  
数值述交-协商申报买入固收业务-协商  
113 成  
3 交-协商申报卖出固收业务-协商成  
113 交-  
4 协商确认-买入-确认  
113 固描  
数值述  
5 收业务-协商成交-协商确认-买入-拒绝固收业务-协商成  
113 交-  
6 协商确认-卖出-确认固收业  
113 务-  
7 协商成交-描  
数值述协商确认-卖出-拒绝固收业务-询价  
113 成  
8 交-询价申报买入固收业务-询价  
113 成  
9 交-询价申报卖出  
114 固收描  
数值述业务-询价成交-报价回复-买入-确认固收业务-询价成交-报  
114 价  
L 回复-买入-拒绝-- 预留字段固收  
114业  
2 务-询描  
数值述价成交-报价回复-卖出-确认固收业务-询价成交-报  
14 价回复-卖出-拒绝-- 预留字段固收业  
14 务-询价成交描  
数值述询价成交-买入-确认固收业务-询价成交-询  
114 价  
5 成交-买入-拒绝-- 预留字段固收业务-竞  
114  
6 买成交-询价成描  
数值述交-卖出确认固收业务竞买成交询  
114 价  
7 成交卖出-拒绝-- 预留字段固收业务竞买  
114 成  
8 交竞买预约买入  

# OPT_FICC_BINDDING_RESERVE_BUY  

描  
数值述固收业务-竞买  
114 成  
9 交-竞买预约卖出固收业务-竞买  
115 成  
0 交-竞买申报买入固收业务-竞  
115买  
1成交-竞买申  

# OPT_FICC_BINDDING_DECLARE_SELL  

# 变量名称  

描  
数值述报卖出固收业务-竞买  
115 成  
2 交-应价申报买入固收业务-竞买  
115 成  
3 交-应价申报卖出买入优  
115先  
4平仓，个描  
数值述股期权交易业务补充类型卖出  
115 优  
5 先平仓资  
115 金  
6 划入资  
115 金  
7 划出  

# #enum_EOrderType - 算法交易、普通交易类型  

# 变量名称  

OTP_ORDINARY 0 常规 OTP_ALGORITHM 1 算法交易 OTP_RANDVOLUME 2 随机量交易 OTP_ALGORITHM3 3 算法交易3  

#  

<html><body><table><tr><td>变量名称</td><td>值</td><td>描述</td></tr><tr><td>OTP_ZXJT</td><td>4</td><td>中信建投算法</td></tr><tr><td>OTP_ZSGS</td><td>5</td><td>隔时交易</td></tr><tr><td>OTP_ORDINARY_BASKET_TRIGGER_SINGLE_ORDER</td><td>6</td><td>普通交易的触价单笔 委托方式</td></tr><tr><td>OTP_ALGORITHM_BASKET_TRIGGER_SINGLE_ORDER</td><td>7</td><td>算法交易的触价单笔 委托方式</td></tr><tr><td>OTP_ZXZQ</td><td>8</td><td>中信证券算法</td></tr><tr><td>OTP_GENUS</td><td>9</td><td>金纳算法</td></tr><tr><td>OTP_JAZZ</td><td>10</td><td>爵士算法</td></tr><tr><td>OTP_VWAP</td><td>11</td><td>智能VWAP</td></tr><tr><td>OTP_TWAP</td><td>12</td><td>智能TWAP</td></tr><tr><td>OTP_XTALGO</td><td>13</td><td>智能算法</td></tr><tr><td>OTP_HUACHUANG</td><td>14</td><td>华创算法</td></tr><tr><td>OTP_HUARUN</td><td>15</td><td>华润算法</td></tr><tr><td>OTP_CUSTOM</td><td>16</td><td>回转算法</td></tr><tr><td>OPT_EXTERN</td><td>17</td><td>主动算法</td></tr><tr><td>OTP_GUANGFA</td><td>18</td><td>广发算法</td></tr></table></body></html>  

# #enum_EPriceType - 价格类型  

值 PRTP_SALE5 0 卖5 PRTP_SALE4 1 卖4 PRTP_SALE3 2 卖3  

# 变量名称  

# 数 值  

PRTP_SALE2   
PRTP_SALE1   
PRTP_LATEST   
PRTP_BUY1   
PRTP_BUY2   
PRTP_BUY3   
PRTP_BUY4   
PRTP_BUY5   
PRTP_FIX   
PRTP_MARKET   
PRTP_HANG   
PRTP_COMPETE   
PRTP_AUTO   
PRTP_CLOSE   
PRTP_AVERAGE   
PRTP_MARKET_BEST   
PRTP_MARKET_CANCEL   
PRTP_MARKET_CANCEL_ALL   
PRTP_MARKET_CANCEL_1   
PRTP_MARKET_CANCEL_5   
PRTP_MARKET_CONVERT_1  

值  
3 卖2  
4 卖1  
5 最新价  
6 买1  
7 买2  
8 买3  
9 买4  
10 买5  
11 指定价  
12 市价_涨跌停价  
13 挂单价  
14 对手价  
15 自动盘口  
16 昨收价  
17 大宗加权平均价  
18 市价_最优价  
19 市价_即成剩撤  
20 市价_全额成交或撤  
21 市价_最优1 档即成剩撤  
22 市价_最优5 档即成剩撤  
23 市价_最优1 档即成剩转  

# 变量名称  

# 数 值  

PRTP_MARKET_CONVERT_5   
PRTP_STK_OPTION_ASK   
PRTP_STK_OPTION_FIX_CANCEL_ALL   
PRTP_STK_OPTION_MARKET_CACEL_LEFT   
PRTP_STK_OPTION_MARKET_CANCEL_ALL   
PRTP_STK_OPTION_MARKET_CONVERT_FIX   
PRTP_SALE6   
PRTP_SALE7   
PRTP_SALE8   
PRTP_SALE9   
PRTP_SALE10   
PRTP_BUY6   
PRTP_BUY7   
PRTP_BUY8   
PRTP_BUY9   
PRTP_BUY10   
PRTP_UPPER_LIMIT_PRICE   
PRTP_LOWER_LIMIT_PRICE   
PRTP_MARKET_SH_CONVERT_5_CANCEL   
PRTP_MARKET_SH_CONVERT_5_LIMIT   
PRTP_MARKET_PEER_PRICE_FIRST  

24 市价_最优5 档即成剩转  
25 询价  
26 限价即时全部成交否则撤单  
27 市价即时成交剩余撤单  
28 市价即时全部成交否则撤单  
29 市价剩余转限价  
30 卖6  
31 卖7  
32 卖8  
33 卖9  
34 卖10  
35 买6  
36 买7  
37 买8  
38 买9  
39 买10  
40 涨停价  
41 跌停价  
42 最优五档即时成交剩余撤销  
43 最优五档即时成交剩转限价  
44 对手方最优价格委托  

<html><body><table><tr><td>变量名称</td><td>数 值</td><td>描述</td></tr><tr><td>PRTP_MARKET_MINE_PRICE_FIRST</td><td>45</td><td>本方最优价格委托</td></tr><tr><td>PRTP_MARKET_SZ_INSTBUSI_RESTCANCEL</td><td>46</td><td>即时成交剩余撤销委托</td></tr><tr><td>PRTP_MARKET_SZ_CONVERT_5_CANCEL</td><td>47</td><td>最优五档即时成交剩余撤销 委托</td></tr><tr><td>PRTP_MARKET_SZ_FULL_REAL_CANCEL</td><td>48</td><td>全额成交或撤销委托</td></tr><tr><td>PRTP_AFTER_FIX_PRICE</td><td>49</td><td>盘后定价申报</td></tr></table></body></html>  

# #enum_ETaskStatus - 任务状态  

<html><body><table><tr><td>变量名称</td><td>值</td><td>描述</td></tr><tr><td>TASK_STATUS_UNKNOWN</td><td>0</td><td>未知</td></tr><tr><td>TASK_STATUS_WAITING</td><td>1</td><td>等待</td></tr><tr><td>TASK_STATUS_COMMITING</td><td>2</td><td>提交中</td></tr><tr><td>TASK_STATUS_RUNNING</td><td>3</td><td>执行中</td></tr><tr><td>TASK_STATUS_PAUSE</td><td>4</td><td>暂停</td></tr><tr><td>TASK_STATUS_CANCELING_DEPRECATED</td><td>5</td><td>撤销中 (已弃用)</td></tr><tr><td>TASK_STATUS_EXCEPTION_CANCELING_DEPRECATED</td><td>6</td><td>异常撤销中 (已弃用)</td></tr><tr><td>TASK_STATUS_COMPLETED</td><td>7</td><td>完成</td></tr><tr><td>TASK_STATUS_CANCELED</td><td>8</td><td>已撤</td></tr><tr><td>TASK_STATUS_REJECTED</td><td>9</td><td>打回</td></tr><tr><td>TASK_STATUS_EXCEPTION_CANCELED</td><td>10</td><td>异常终止</td></tr><tr><td>TASK_STATUS_DROPPED</td><td>11</td><td>放弃（用于组合交易 中，放弃补单)</td></tr><tr><td>TASK_STATUS_FORCE_CANCELED_DEPRECATED</td><td>12</td><td>强制终止 (已弃用)</td></tr></table></body></html>  

# 获取行情示例  

# #按品种划分  

#两融  

# #获取融资融券账户可融资买入标的  

python  

#coding:gbk   
def init(C): r = get_assure_contract('123456789') if len(r) == 0: print('未取到担保明细') else: finable = [o.m_strInstrumentID+'.'+o.m_strExchangeID for o in r if   
o.m_eFinStatus==48] print('可融资买入标的:', finable)  

# #按功能划分  

#订阅K 线全推  

提示  

1. K 线全推需要VIP 权限在新窗口打开，非VIP 用户请勿使用此功能  

订阅全市场1m 周期K 线  

python  

![](images/bf9109542fb1999776a1978487cb01cfd7cdaa7c2b01d8777a88b27d5e6a68e8.jpg)  

# #获取N 分钟周期K 线数据  

# 提示  

1. 获取历史N 分钟数据前，需要先下载历史数据  
2. 1m 以上，5m 以下的数据，是通过1m 数据合成的  
3. 5m 以上，1d 以下的数据，是通过5m 数据合成的  
4. 1d 以上的数据，是通过1d 的数据合成的  

![](images/7da463cb16bfb9eb86653e3081e1330f1a5f45d29b508b6e0f77da324e208e01.jpg)  

![](images/3ebd6a8006b6374ade408ddd8447271c3719865c7d26bbb3fa46c3e2edbdf731.jpg)  

# #获取 Lv1 行情数据  

本示例用于说明如何通过函数获取行情数据。  

python  

#coding:gbk # get_market_data_ex(subscribe=True)有订阅股票数量限制 # 即stock_list 参数的数量不能超过500  

![](images/ad38682034d08500a32df2df834b3ce491087363847265a727a7822d7adf949f.jpg)  

# #获取 Lv2 数据（需要数据源支持）  

# #方法1 - 查询LV2 数据  

使用该函数后，会定期查询最新数据，并进行数据返回。  

python 返回值  

#coding:gbk  

# def init(C):  

C.sub_nums =  

for field in ['l2transaction', 'l2order', 'l2transactioncount', 'l2quote']: num = C.subscribe_quote(C.stock, period=field,  

dividend_type='follow'  

C.sub_nums.append(num)  

def handlebar(C):  

return   
price = C.get_market_data_ex([],[C.stock],period='l2transaction',count=10)[C.stock]   
price_dict = price.to_dict('index')   
print(price_dict)   
for pos, t in enumerate(price_dict): print(f" 逐笔成交:{pos+1} 时间:{price_dict[t]['stime']}, 时间  

戳:{price_dict[t]['time']}, 成交价:{price_dict[t]['price']}, \ 成交量:{price_dict[t]['volume']}, 成交额:{price_dict[t]['amount']} \ 成交记录号:{price_dict[t]['tradeIndex']}, 买方委托号:{price_dict[t]['buyNo']},\ 卖方委托号:{price_dict[t]['sellNo']}, 成交类型:{price_dict[t]['tradeType']}, \ 成交标志:{price_dict[t]['tradeFlag']}, ")  

price = C.get_market_data_ex([],[C.stock],period='l2quote',count=10)[C.stock]   
price_dict = price.to_dict('index')   
print(price_dict)   
for pos, t in enumerate(price_dict): print(f" 十档快照:{pos+1} 时间:{price_dict[t]['stime']}, 时间   
戳:{price_dict[t]['time']}, 最新价:{price_dict[t]['lastPrice']}, \   
开盘价:{price_dict[t]['open']}, 最高价:{price_dict[t]['high']} 最低价:{price_dict[t]['low']}, 成交   
额:{price_dict[t]['amount']},\   
成交总量:{price_dict[t]['volume']}, 原始成交总量:{price_dict[t]['pvolume']}, 证券状   
态:{price_dict[t]['stockStatus']}, 持仓量:{price_dict[t]['openInt']},\   
成交笔数:{price_dict[t]['transactionNum']},前收盘价:{price_dict[t]['lastClose']},多档委卖   
价:{price_dict[t]['askPrice']},多档委卖量:{price_dict[t]['askVol']},\   
多档委买价:{price_dict[t]['bidPrice']},多档委买量:{price_dict[t]['bidVol']}")   
price = C.get_market_data_ex([],[C.stock],period='l2order',count=10)[C.stock]   
price_dict = price.to_dict('index')   
for pos, t in enumerate(price_dict):  

![](images/2a1c63cd84bac84b5fea7079ead222927b1c1d2f5b5cb9db19dd0bae18f9ca1c.jpg)  

# #方法2 - 订阅LV2 数据  

此方法在发起订阅后，会自动收到所订阅数据，订阅方需要记录订阅函数返回的订阅号，并在不需要订阅时调用unsubscribe_quote 反订阅数据，释放资源。  

python 返回值  

![](images/4f9ce9cd0c2c053bd6538086460bb7a6d8cc79527e400b1f6dc1f68e87673f90.jpg)  

![](images/8fda171a30cb60307f708f5a8e551df97a833ed56a488a40ed18a8190955623c.jpg)  

# #使用 Lv1 全推数据计算全市场涨幅  

python  

# lass a():pass  

A = a()  

A.hsa = C.get_stock_list_in_sector('沪深A 股') + C.get_stock_list_in_sector('京市A 股')   
print('股票池大小', len(A.hsa))   
A.vol_dict = {}   
for stock in A.hsa: A.vol_dict[stock] = C.get_last_volume(stock)   
C.run_time("f","3nSecond","2019-10-14 13:20:00")   
import numpy as np   
if np.isnan(a): return '问题数据'   
if abs(a) < 1000: print(a, str(round(int(a) / 1000.0, 2)) + "千") return str(round(int(a) / 1000.0, 2)) + "千"   
if abs(a) < 10000: return str(int(a))[0] + "千"   
if abs(a) < 100000000: return str(int(a))[:-4] + "万" + str(int(a))[-4]   
return f"{int(a / 100000000)}亿"  

def f(C):  

![](images/ac23eafd4aa21a7d5fd5f2202df61aebac84d551e6fdf95dc535513034c8707d.jpg)  

![](images/fde91b7cb515d15357bec79775607c007dd48c871e805386e2d90a0af4cd5b76.jpg)  

# #在行情回调函数里处理动态行情  

ContextInfo.subscribe_quote - 订阅行情函数说明行情回调函数字段说明  

![](images/9bf69927646c77999f86dd1b9e72572b928d290e34fa46764d800711a0aaf33b.jpg)  

![](images/9466a6dd23bccec13ef17b15a7f72ec2f3c368ec1dddcc9c18753482551d6464.jpg)  

# #python 写入扩展数据  

python  

coding:gbk  

python 写扩展数据，投研接口  

def init(C):# 创建扩展数据  

extencd_name  = 'test' # 创建名为test 的扩展数据create_extend_data# (父节点, 扩展数据名称, 是否覆盖)C.extencd_name = create_extend_data('扩展数据', extencd_name, True)  

# def handlebar(C):  

if C.is_last_bar():  

data = {'SH600177': 0.43, 'SZ000767': 0.18, 'SH600362': 0.27, 'SH600171': 0.25, 'SH600170': 0.18, 'SH600073': 0.13, 'SZ000768': 0.17, 'SH600282': 0.19, 'SH600601': 0.42, SH600569': 0.26, 'SZ000401': 0.21, 'SH600602': 0.17, 'SZ000806': 0.13, 'SZ000807': 0.15, SH600608': 0.08, 'SH600874': 0.09, 'SZ000825': 0.44, 'SZ000652': 0.19, 'SH600078': 0.11, 'SH600871': 0.1, 'SZ000573': 0.1, 'SZ000520': 0.14, 'SH600879': 0.43, 'SZ000960': 0.2, 'SH600597': 0.21, 'SZ000550': 0.1, 'SH600591': 0.14, 'SZ000059': 0.13, 'SH600215': 0.12, 'SZ000968': 0.11, 'SZ000969': 0.14, 'SZ000568': 0.22, 'SH600598': 0.22, 'SH600028': 1.85, 'SH600270': 0.27, 'SH600060': 0.22, 'SH600062': 0.15, 'SH600779': 0.14, 'SH600997': 0.2, 'SZ000707': 0.12, 'SH600068': 0.16, 'SH600770': 0.14, 'SZ000680': 0.14, 'SH600674': 0.1, SH600675': 0.25, 'SZ000488': 0.28, 'SZ000012': 0.11, 'SH600863': 0.17, 'SZ000429': 0.17, 'SH600027': 0.32, 'SH600866': 0.13, 'SH600001': 0.43, 'SZ000636': 0.11, 'SH600900': 2.73, 'SH600600': 0.31, 'SH600895': 0.26, 'SH600029': 0.43, 'SH600020': 0.24, 'SH600205': 0.39, 'SH600688': 0.76, 'SH600207': 0.1, 'SZ000970': 0.3, 'SZ000601': 0.19, 'SH600200': 0.35, 'SZ000975': 0.08, 'SZ000538': 0.39, 'SZ000422': 0.14, 'SZ000858': 0.88, 'SZ000651': 0.44, 'SH600780': 0.21, 'SH600007': 0.11, 'SH600016': 2.36, 'SZ000866': 0.84, 'SH600267': 0.12, 'SH600266': 0.16, 'SH600786': 0.27, 'SZ000406': 0.39, 'SH600269': 0.47, 'SZ000528': 0.19, 'SH600694': 0.51, 'SZ000786': 0.14, 'SH600004': 0.4, 'SH600663': 0.25, 'SH600662': 0.21, 'SH600548': 0.11, 'SH600383': 0.42, 'SH600357': 0.12, 'SH600705': 0.13, 'SH600812': 0.18, 'SH600707': 0.06, 'SZ000895': 0.49, 'SZ000898': 0.68, 'SZ000400': 0.17, 'SZ000607': 0.1, 'SH600894': 0.1, 'SH600418': 0.4, 'SZ000061': 0.15, 'SH600653': 0.31, 'SZ000682': 0.17, 'SZ000543': 0.07, 'SZ000541': 0.25, 'SH600377': 0.12, 'SZ000949': 0.06, 'SH600256': 0.17, 'SH600006': 0.23, 'SH600005': 1.13, 'SH600790': 0.1, 'SH600797': 0.2, 'SH600002': 0.51, 'SH600795': 0.49, 'SH600000': 1.64, 'SH600652': 0.17, 'SH600121': 0.13, 'SH600123': 0.3, 'SH600125': 0.27, 'SH600126': 0.12, 'SH600008': 0.51, 'SZ000016': 0.14, 'SH600550': 0.24, 'SH600718': 0.16, 'SH600654': 0.2, 'SZ000157': 0.2, 'SH600808': 0.42, 'SZ000666': 0.1, 'SH600805': 0.11, 'SZ000527': 0.39, 'SH600717': 0.5, 'SH600399': 0.07, 'SZ000828': 0.14, 'SZ000959': 0.17, 'SZ000729': 0.29, 'SH600098': 0.43, 'SZ000886': 0.09, 'SZ000099': 0.13, 'SZ000800': 0.29, 'SH600096': 0.29, 'SZ001872': 0.17, 'SH600091': 0.12, 'SZ000956': 0.41, 'SH600887': 0.63, 'SH600886': 0.2, 'SH600884': 0.12, 'SH600308': 0.32, 'SH600309': 0.64, 'SH600881': 0.21, 'SH600307': 0.14, 'SZ000069': 0.8, 'SZ000068': 0.1, 'SH600153': 0.19, 'SZ000792': 0.55, 'SZ000060': 0.38, 'SZ000002': 2.25, 'SZ000001': 1.25, 'SH600138': 0.1, 'SH600649': 0.44, 'SH600015': 0.99, 'SZ000533': 0.07, 'SZ000009': 0.24, 'SH600408': 0.09, 'SZ000778': 0.23, 'SH600643': 0.17, 'SH600642': 0.71, 'SH600832': 0.71, 'SZ000089': 0.36, 'SZ000088': 0.44, 'SZ000539': 0.3, 'SH600835': 0.19, 'SH600726': 0.09, 'SH600010': 0.42, 'SH600724': 0.16, 'SH600839': 0.61, 'SH600011': 0.38, 'SH600012': 0.27, 'SH600089': 0.23, 'SH600088': 0.12, 'SH600087': 0.12, 'SH600085': 0.38, 'SZ000927': 0.2, 'SZ000920': 0.11, 'SZ000962': 0.13, 'SZ000559': 0.16, 'SH600050': 2.98, 'SZ000708': 0.09, 'SZ000503': 0.36, 'SZ000839': 0.44, 'SZ000717': 0.28, 'SZ000100': 0.31, 'SZ000036': 0.18, 'SZ000878': 0.24, 'SZ000511': 0.09, 'SZ000410': 0.19, 'SH600033': 0.24, 'SH600108': 0.13, 'SZ000031': 0.21, 'SZ000507': 0.09, 'SH600104': 0.78, 'SZ002024': 0.45, 'SH600102': 0.18, 'SH600103': 0.14, 'SH600100': 0.41, 'SH600019': 2.84, 'SH600009': 1.5, 'SH600639': 0.19, 'SZ000709': 0.34, 'SH600820': 0.14, 'SZ000571': 0.1, 'SH600739': 0.13, 'SH600631': 0.25, 'SH600021': 0.24, 'SH600635': 0.22, 'SH600637': 0.15, 'SZ000733': 0.09, 'SZ000780': 0.09, 'SH600210': 0.25, 'SZ000939': 0.12, 'SZ000937': 0.26, 'SZ000875': 0.15, 'SZ000933': 0.22, 'SZ000932': 0.51, 'SZ000659': 0.15, 'SZ000930': 0.38, 'SH600320': 0.8, 'SZ000822': 0.17, 'SZ000726': 0.14, 'SZ000727': 0.1, 'SZ000725': 0.13, 'SH600380': 0.14, 'SH600030': 0.63, 'SH600031': 0.16, 'SH600036': 3.93, 'SH600037': 0.62, 'SH600035': 0.16, 'SH600058': 0.2, 'SH600110': 0.13, 'SH600508': 0.19, 'SZ000402': 0.62, 'SH600115': 0.1, 'SH600117': 0.13, 'SZ000423': 0.22, 'SH600348': 0.34, 'SZ000518': 0.14, 'SH600500': 0.26, 'SH600660': 0.37, 'SH600057': 0.09, 'SH600744': 0.12, 'SH600747': 0.11, 'SH600740': 0.09, 'SH600741': 0.17, 'SH600621': 0.11, 'SZ000698': 0.14, 'SH600851': 0.19, 'SZ000900': 0.28, 'SH600854': 0.1, 'SH600868': 0.25, 'SH600428': 0.3, 'SZ000630': 0.36, 'SH600811': 0.3, 'SZ000735': 0.1, 'SZ000737': 0.09, 'SZ000066': 0.19, 'SH600331': 0.25, 'SH600183': 0.27, 'SH600333': 0.1, 'SZ000581': 0.25, 'SZ000425': 0.11, 'SZ000983': 0.49, 'SH600236': 0.25, 'SH600026': 0.45, 'SH600339': 0.08, 'SH600231': 0.16, 'SH600188': 0.27, 'SH600022': 0.2, 'SH600166': 0.08, 'SH600350': 0.37, 'SH600519': 1.14, 'SZ000063': 1.49, 'SH600690': 0.44, 'SZ000758': 0.24, 'SH600296': 0.26, 'SH601607': 0.17, 'SHT00018': 0.8, 'SZ000039': 0.78, 'SZ000599': 0.1, 'SH600198': 0.21, 'SZ000917': 0.15, 'SZ000916': 0.22, 'SZ000912': 0.21, 'SH600190': 0.11, 'SH600196': 0.25,  

# #扩展数据展示  

![](images/d094c1198eebe8feb7c9f8d5b04d1ef4110f313b15653a15b4b27f6d08a3ac22.jpg)  

# #每1 分钟统计一次市场涨跌情况  

示例  

# coding:gbk   
import datetime as dt   
def on_timer(ContextInfo): ls = globals().get("stock_list") now_time = dt.datetime.now().strftime("%Y%m%d %H:%M:%S") # 取tick 数据 ticks = ContextInfo.get_full_tick(ls)  

![](images/bc2baa3480f68db6137d9f987434d05e58242ab8ba0b46053805e6e318f02f38.jpg)  

# #交易下单示例  

# #按品种划分  

# #股票  

python  

#coding:gbk  
def handlebar(ContextInfo):if not ContextInfo.is_last_bar():return# 单股单账号股票最新价买入 100 股（1 手）passorder(23, 1101, 'test', '600000.SH', 5, 0, 100, '',1,'',ContextInfo)# 单股单账号股票最新价卖出 100 股（1 手）passorder(24, 1101, 'test', '600000.SH', 5, 0, 100, '',1,'',ContextInfo)# 单股单账号沪市股票市价买入 100 股（1 手），沪市市价存在保护限价，Price 参数为  
保护限价，买入为投资者能够接受的最高买价，填0 会自动填为涨停价passorder(23, 1101, 'test', '600000.SH', 42, 0, 100, '',1,'',ContextInfo)# 单股单账号沪市股票市价卖出 100 股（1 手），沪市市价存在保护限价，Price 参数为  
保护限价，卖出为投资者能够接受的最低卖价，填0 会自动填为跌停价passorder(24, 1101, 'test', '600000.SH', 42, 0, 100, '',1,'',ContextInfo)# 单股单账号京市股票最新价买入 101 股（1 手零 1 股）passorder(23, 1101, 'test', '430047.BJ', 5, 0, 101, '',1,'',ContextInfo)# 单股单账号京市股票最新价卖出 101 股（1 手零 1 股）  

passorder(24, 1101, 'test', '430047.BJ', 5, 0, 101, '',1,'',ContextInfo)  

#基金 python  

def handlebar(ContextInfo):if not ContextInfo.is_last_bar():return# 申购 中证500 指数ETFpassorder(60, 1101, 'test', '510030.SH', 5, 0, 1, 2, ContextInfo)# 赎回 中证500 指数ETFpassorder(61, 1101, 'test', '510030.SH', 5, 0, 1, 2, ContextInfo)  

# #两融  

python  

#coding:gbk  
def handlebar(ContextInfo):if not ContextInfo.is_last_bar():returntarget = '000001.SZ'# 单股单账号股票指定价担保品买入 100 股（1 手）passorder(33, 1101, 'test', target, 11, 7, 100, ContextInfo)# 单股单账号股票指定价融资买入 100 股（1 手）passorder(27, 1101, 'test', target, 11, 7, 100, ContextInfo)  

#期货 python  

![](images/be15310c9a976cd46d7deed75d331abf184b551988abf04dbe8c62c0f65b2a43.jpg)  

target = 'IF2311.IF' passorder(6, 1101, 'test', target, 5, -1, 2, 1, ContextInfo)  

# #期权  

python  

#coding:gbk  
def handlebar(ContextInfo):if not ContextInfo.is_last_bar():returntarget = '10005330.SHO' # 50ETF 购12 月2450 合约# 单股单账号用最新价买入开仓期权合约target 2 张passorder(50, 1101, 'test', target, 5, -1, 2, 1, ContextInfo)# 单股单账号用最新价卖出平仓期权合约target 2 张passorder(51, 1101, 'test', target, 5, -1, 2, 1, ContextInfo)  

# #新股申购  

#coding:gbk   
def init(ContextInfo): ipoStock=get_ipo_data("BOND")#返回新股信息 print(ipoStock) accont = '123456789' for stock in ipoStock: ipo_price = ipoStock[stock]['issuePrice'] # 发行价 maxPurchaseNum = ipoStock[stock]['maxPurchaseNum'] # 可申购额度 passorder(23,1101, accont, stock,11,ipo_price, maxPurchaseNum,'新股申购   
',2,stock,C)  

# #债券  

python  

#coding:gbk  
def handlebar(ContextInfo):if not ContextInfo.is_last_bar():return# 单股单账号最新价可转债买入 20 张passorder(23, 1101, 'test', '128123.SZ', 5, -1, 10, 1, ContextInfo)  

# #ETF  

python  

ef handlebar(ContextInfo):if not ContextInfo.is_last_bar():return# 单股单账号 最新价买入上证etf 2000 份passorder(23, 1101, 'test', '510050.SH', 5, -1, 2000, ContextInfo)  

# #组合交易  

一键买卖（一篮子下单）  

功能描述： 该示例演示如何用python 进行一揽子股票买卖的交易操作  

代码示例：  

python  

![](images/5c5aebb9da21a66e4b2b49f7528f5e117e5fab6351efb81cd9a9cad4d827c24c.jpg)  

#组合套利交易  

提示  

（accountID、orderType 特殊设置）  

用法  

释义：  

参数  

# 参数名称  

# 描述  

accountID 'stockAccountID, futureAccountID'  
orderCode 'basketName, futureName'  
hedgeRatio 利利比例（0 \~ 2 之间值，相当于 %0 至 $200\%$ 利利）  
volume 份数 \ 资金 \ 比例  
orderType 参考下方orderType-下单方式（特殊设置）  
rderType - 下单方式（特殊设置）  

# 编号  

# 项目  

2331 组合、利利、合约价值自动利利、按组合股票数量方式下单  
2332 组合、利利、按合约价值自动利利、按组合股票权重方式下单  

2333 组合、利利、按合约价值自动利利、按账号可用方式下单  

示例  

python 返回值  

# #按功能划分  

#passorder 下单函数  

本示例用于演示K 线走完下单及立即下单的参数写法差异，旨在帮助您了解如何快速实现下单操作。  

# python  

![](images/542656c23ca54a31e7bdb504ac7e00b83d02f4e507f70e9e7a7451072476ef5d.jpg)  

# #集合竞价下单  

本示例演示了利用定时器函数和passorder 下单函数在集合竞价期间以指定价买入平安银行100 股。  

python #coding:gbk  

import time  
c = 0  
s = '000001.SZ'  
def init(ContextInfo):# 设置定时器，历史时间表示会在一次间隔时间后开始调用回调函数 比如本例中 5  
秒后会后第一次触发myHandlebar 调用 之后五秒触发一次ContextInfo.run_time("myHandlebar","5nSecond","2019-10-14 13:20:00")  
def myHandlebar(ContextInfo):global cnow = time.strftime('%H%M%S')if c ==0 and '092500' >= now >= '091500':c += 1passorder(23,1101,account,s,11,14.00,100,2,ContextInfo) # 立即下单  
def handlebar(ContextInfo):return  

# #止盈止损示例  

python  

#coding:gbk  

.账户内所有股票，当股价低于买入价10%止损卖出。  
2.账户内所有股票，当股价高于前一天的收盘价10%时，开始监控一旦股价炸板（开板），以买三价卖出  

def init(C):  

![](images/68313de8160c1923f5d55b7a574deac52cbfc186601efe8fc0c61d72f106b8b8.jpg)  

# #passorder 下算法单函数  

本示例由于演示如何下达算法单，具体算法参数请参考迅投投研平台客户端参数说明。  

python  

![](images/8d7832283350fa51d1110f39ad0c324c230d00808a34a351a8a35353deacdff1.jpg)  

# #如何使用投资备注  

投资备注功能是模型下单时指定的任意字符串(长度小于24)，即passorder 的userOrderId 参数，可以用于匹配委托或成交。有且只有passorder，algo_passorder, smart_algo_passorder 下单函数支持投资备注功能。  

![](images/6a7ebda0975868dce97b93c7a3bbd351afcdf2c75ffad4f4986205d1ddd8c260.jpg)  

#如何获取委托持仓及资金数据  

本示例用于演示如何通过函数获取指定账户的委托、持仓、资金数据。  

python #coding:gbk def init(C):  

pass #orders, deals, positions, accounts = query_info(C)  

def handlebar(C):  

if not C.is_last_bar(): return   
orders, deals, positions, accounts = query_info(C)  

def query_info(C): orders = get_trade_detail_data('8000000213', 'stock', 'order') for o in orders:  

print(f'股票代码: {o.m_strInstrumentID}, 市场类型: {o.m_strExchangeID},证券名称: {o.m_strInstrumentName}, 买卖方向: {o.m_nOffsetFlag}',  

f'委托数量: {o.m_nVolumeTotalOriginal}, 成交均价: {o.m_dTradedPrice}, positions = get_trade_detail_data('8000000213', 'stock', 'position') for dt in positions:  

print(f'股票代码: {dt.m_strInstrumentID}, 市场类型: {dt.m_strExchangeID}   
证券名称: {dt.m_strInstrumentName}, 持仓量: {dt.m_nVolume}, 可用数量:   
{dt.m_nCanUseVolume}', f'成本价: {dt.m_dOpenPrice:.2f}, 市值: {dt.m_dInstrumentValue:.2f}, 持仓   
成本: {dt.m_dPositionCost:.2f}, 盈亏: {dt.m_dPositionProfit:.2f}') accounts = get_trade_detail_data('8000000213', 'stock', 'account') for dt in accounts: print(f'总资产: {dt.m_dBalance:.2f}, 净资产: {dt.m_dAssureAsset:.2f}, 总市   
值: {dt.m_dInstrumentValue:.2f}', f'总负债: {dt.m_dTotalDebit:.2f}, 可用金额: {dt.m_dAvailable:.2f}, 盈亏:   
{dt.m_dPositionProfit:.2f}') return orders, deals, positions, accounts  

# #使用快速交易参数委托  

本例展示如何使用快速交易参数(quickTrade)立刻进行委托。  

python  

#coding:gbk  
def after_init(C):#account 变量是模型交易界面 添加策略时选择的资金账号 不需要手动填写#快速交易参数(quickTrade )填2 passorder 函数执行后立刻下单 不会等待k 线走完  
再委托。 可以在after_init 函数 run_time 函数注册的回调函数里进行委托msg = f"投资备注字符串 用来区分不同委托"passorder(23, 1101, account, '600000.SH', 5, -1, 200, '测试下单', 2, msg, C)  

# #调整至目标持仓  

本示例由于演示如何调仓。  

python  

![](images/9888e535ec522dd344ce9dbad5a9f9e585401fbae7194403a80b32405c112b18.jpg)  

def init(C): '''读取目标仓位 字典格式 品种代码:持仓股数, 可以读本地文件/数据库，当前在代   
码里写死''' A.final_dict = {"600000.SH" :10000, '000001.SZ' : 20000} '''设置交易账号 acount accountType 是界面上选的账号 账号类型''' A.acct = account A.acct_type = accountType #定时器 定时触发指定函数 C.run_time("f","1nSecond","2019-10-14 13:20:00","SH") #获取持仓信息 position_list = get_trade_detail_data(A.acct, A.acct_type, 'position') #持仓数据 组合为字典 position_dict = {i.m_strInstrumentID + '.' + i.m_strExchangeID : int(i.m_nVolume) for i   
in position_list} position_dict_available = {i.m_strInstrumentID + '.' + i.m_strExchangeID :   
int(i.m_nCanUseVolume) for i in position_list} #未持有的品种填充持股数0 not_in_position_stock_dict = {i : 0 for i in final_dict if i not in position_dict} position_dict.update(not_in_position_stock_dict) #print(position_dict) stock_list = list(position_dict.keys()) # print(stock_list) #获取全推行情 full_tick = C.get_full_tick(stock_list) #print('fulltick', full_tick) #更新持仓状态记录 refresh_waiting_dict(C) #撤超时委托 order_list = get_trade_detail_data(A.acct, 'stock', 'order') if '091500'<= now_timestr <= '093000':#指定的范围內不撤单 pass else: for order in order_list: #非本策略 本次运行记录的委托 不撤 if order.m_strRemark not in A.all_order_ref_dict: continue #委托后 时间不到撤单等待时间的 不撤 if time.time() - A.all_order_ref_dict[order.m_strRemark] <   
A.withdraw_secs: continue #对所有可撤状态的委托 撤单 if order.m_nOrderStatus in [48,49,50,51,52,55,86,255]: print(f"超时撤单 停止等待 {order.m_strRemark}") cancel(order.m_strOrderSysID,A.acct,'stock',C) #下单判断 for stock in position_dict: #有未查到的委托的品种 跳过下单 防止超单 if stock in A.waiting_dict: print(f"{stock} 未查到或存在未撤回委托   
{A.waiting_dict[stock]} 暂停后续报单") continue if stock in position_dict.keys():   
target_vol = final_dict[stock] if stock in final_dict else 0   
if int(abs(position_dict[stock] - target_vol)) == 0: print(stock, C.get_stock_name(stock), '与目标一致') continue  

![](images/bfd1a434c26df3000068b2947ca322dea847cfbcb6984b539766f839b2ffcc1f.jpg)  

if position_dict[stock]>target_vol: vol = int((position_dict[stock] - target_vol)/100)\*100 if stock not in position_dict_available:  

取到的价格{buy_one_price}无效，跳过此次推送")  

print(f"{stock} {C.get_stock_name(stock)} 目标股数 {target_vol} 当前股数{position_dict[stock]}")  

msg  

"{now.strftime('%Y%m%d%H%M%S')}_{stock}_sell_{vol}股"  

#对手价卖出 passorder(24,1101,A.acct,stock,14,-1,vol,'调仓策略  

# ,2,msg,C)  

A.waiting_dict[stock] = msg A.all_order_ref_dict[msg] = time.time()  

#持仓小于目标持仓 买入  

position_dict[stock]<target_vol: vol = int((target_vol-position_dict[stock])/100)\*100 #获取卖一价 sell_one_price = full_tick[stock]['askPrice'][0] #卖一价无效时 跳过委托 if not sell_one_price > 0: print(f"{stock} {C.get_stock_name(stock)} 取到的价格{sell_one_price}无效，跳过此次推送")  

# target_value = sell_one_price \* vol  

if target_value > available_cash:print(f"{stock} 目标市值{target_value} 大  

于 可用资金{available_cash} 跳过委托")  

continue  

{target_vol} 当前股数{position_dict[stock]}")  

print(f"{stock} {C.get_stock_name(stock)} 目标股数  

msg  

{now.strftime('%Y%m%d%H%M%S')}_{stock}_buy_{vol}股"  

print(msg)  

#对手价买  

passorder(23,1101,A.acct,stock,14,-1,vol,'调仓策略  

,2,msg,C)  

A.waiting_dict[stock] = msg A.all_order_ref_dict[msg] = time.time() available_cash -= target_value  

#打印函数运行耗时 定时器间隔应大于该值print(f"下单判断函数运行完成 耗时{time.time() - t0}秒")  

def refresh_waiting_dict(C):  

{ref_dict[A.waiting_dict[stock]]} (56 已成 53 部撤 54 已撤)从等待等待字典中删除')del_list.append(stock)  

if A.waiting_dict[stock] in ref_dict and ref_dict[A.waiting_dict[stock]] == 57:#委托状态是废单的 也停止等待 从等待字典中删除print(f"投资备注为{A.waiting_dict[stock]}的委托状态为废单 停  

# #获取融资融券账户可融资买入标的  

python  

#coding:gbk   
def init(C): r = get_assure_contract('123456789') if len(r) == 0: print('未取到担保明细') else: finable = [o.m_strInstrumentID+'.'+o.m_strExchangeID for o in r if   
o.m_eFinStatus==48] print('可融资买入标的:', finable)  

# #获取两融账号信息示例  

python  

![](images/68f9fe86ad68f7a42babbf6d3f6157fbe250f4feacd07ea263d1daa1b2430133.jpg)  

# #直接还款示例  

该示例演示使用python 进行融资融券账户的还款操作。  

![](images/4f31dbaad23219acd8bbffb7321201f873f43905a4ecaa83e05b5835a8a99811.jpg)  

# #交易数据查询示例  

python #coding:gbk  

for attr in dir(obj): try: if attr[:2] == 'm_': attr_dict[attr] = getattr(obj, attr) except: pass return attr_dict def init(C): pass #orders, deals, positions, accounts = query_info(C) def handlebar(C): if not C.is_last_bar(): return orders, deals, positions, accounts = query_info(C) def query_info(C): orders = get_trade_detail_data('8000000213', 'stock', 'order') for o in orders: print(f'股票代码: {o.m_strInstrumentID}, 市场类型: {o.m_strExchangeID}, 证券名称: {o.m_strInstrumentName}, 买卖方向: {o.m_nOffsetFlag}', f'委托数量: {o.m_nVolumeTotalOriginal}, 成交均价: {o.m_dTradedPrice}, 成交数量: {o.m_nVolumeTraded}, 成交金额:{o.m_dTradeAmount}') deals = get_trade_detail_data('8000000213', 'stock', 'deal') for dt in deals: print(f'股票代码: {dt.m_strInstrumentID}, 市场类型: {dt.m_strExchangeID}, 证券名称: {dt.m_strInstrumentName}, 买卖方向: {dt.m_nOffsetFlag}', f'成交价格: {dt.m_dPrice}, 成交数量: {dt.m_nVolume}, 成交金额: {dt.m_dTradeAmount}') positions = get_trade_detail_data('8000000213', 'stock', 'position') for dt in positions: print(f'股票代码: {dt.m_strInstrumentID}, 市场类型: {dt.m_strExchangeID}, 证券名称: {dt.m_strInstrumentName}, 持仓量: {dt.m_nVolume}, 可用数量:  

# Python 环境相关  

# #安装第三方 Python 库报错  

# 问题描述：  

"ImportError:Forbidden:Moduleopenpyxl not in whitelist!"  

# 问题解答：  

该报错是由于券商后台开启了 Python 库白名单，若您使用的是券商提供的QMT 终端，请联系您的所属券商开通对应 Python 库白名单权限即可。  

# #启动策略时pandas 库报错  

报错信息1 ：NameError: name 'pandas' is not defined  

# 解答：  

该报错是指当前环境下没有找到pandas 库  

# 解决方法  

1. 请在设置-模型设置中检查正确设置了路径,正确路径应指向{安装目录}\bin.x64  

![](images/c7e821f29f9533117fa75213af903d1c4998df7dd46b1d60e1e96523b9353bf7.jpg)  

2. 请检查是否已经下载了python 环境  

![](images/f7891cc1e2db568690f67606754dae34848bfb7fcb167d75bda9a45e5bfb6916.jpg)  

报错信息2 ：AttributeError: module 'pandas' has no attribute 'core'  

# 解答：  

该报错是由于在pandas 导入中被强行中断导致的  

# 解决方法  

重启客户端  

# #对第三方库的支持  

QMT Python API 提供基于 Python 3.6 规范的标准量化投资策略应用程序接口，本文档示例代码基于 Python 3.6 规范。我司主要通过以下两种方式对外提供：  

# #系统自带的 Python 环境  

QMT 系统的安装包默认自带 Python 运行环境。用户安装完迅投客户端后，默认可以直接使用Python。在这个打包的Python 环境中，迅投除了提供标准的 Python api 带的库外，还集成了如下一些第三方库：  

名称  
说明  


<html><body><table><tr><td>NumPy</td><td>NumPy（NumericPython）提供了许多高级的数值编程工具，如：矩 阵数据类型、矢量处理，以及精密的运算库。专为进行严格的数字处 理而产生。</td></tr><tr><td>Pandas</td><td>Python Data Analysis Library 或 Pandas 是基于 NumPy 的一种工 具，该工具是为了解决数据分析任务而创建的。Pandas 纳入了大量 库和一些标准的数据模型，提供了高效地操作大型数据集所需的工 具。Pandas提供了大量能使我们快速便捷地处理数据的函数和方法。</td></tr><tr><td>Patsy</td><td>一个线性模型分析和构建工具库。</td></tr><tr><td>SciPy</td><td>SciPy函数库在NumPy库的基础上增加了众多的数学、科学以及工 程计算中常用的库函数。例如线性代数、常微分方程数值求解、信号 处理、图像处理、稀疏矩阵等等。</td></tr><tr><td>Statsmodels</td><td>Python的统计建模和计量经济学工具包，包括一些描述统计、统计 模型估计和推断。</td></tr><tr><td>TA_Lib</td><td>称作技术分析库，是一种广泛用在程序化交易中进行金融市场数据的 技术分析的函数库。它提供了多种技术分析的函数，可以大大方便我 们量化投资中编程工作，内容包括：多种指标，如ADX,MACD,RSI, 布林轨道等；K 线形态识别，如黄昏之星，锤形线等等。</td></tr></table></body></html>  

# #第三方库导入指引  

除迅投提供的标准 Python api 和集成的部分第三方库，用户也可自己在 Python 官网下载其他所需第三方库，使用方式如下：  

（1）本地安装Python 环境，下载python3.6，Python 官网：https://www.python.org/downloads/release/python-360/  

# （2）安装位置：C:\Python36  

新增环境变量：我的电脑--属性--高级系统设置--高级--环境变量---path：C:\Python36;C:\Python36\Scripts  

![](images/a701bdc6e40552810dae85a9a10047bd173f8aa82890dcbcd639bb2412accc81.jpg)  

# （3）Python 环境检查  

Win $+\mathsf{R}$ 打开运行,输入 cmd  

![](images/4626fcf0b23f17f8a5978359ee85e60ad88026076ffeca2a8f1826e8b5de0cee.jpg)  

检查Python 变量  

# （4）安装第三方库  

安装前先确认客户端安装目录，根据个人电脑进行调整。  

安装时若遇到下面错误提示，请执行 pip 更新命令 python -m pip install --upgradepip  

C:\Users\wang>pip instal1 -t E:\ 正券QMT交易端20962\bin.x64\Lib\site-packages You must give at least one requirement to install (see "pip help install") You are using pip version 9.0.1, however version 2l.0.1 is available. You should consider upgrading via the 'python -m pip install --upgrade pip' command. C:\Users\wang>python -m pip instal1 --upgrade pip  

安装三方库命令 pip install openpyxl -t E:\QMT 交易端20962\bin.x64\Lib\site-packages  

![](images/3e87f7705fbbf37564c399e108237412026fbbd767446a801c6850d19a539c82.jpg)  

# （5）检查安装结果  

安装位置\bin.x64\Lib\site-packages 检查安装库  

名称 修改日期 类型 大小 ecos.py 2019/11/25 11:18 Python File 3 KB pvectorc.cp36-win_amd64.pyd 2019/11/25 11:18 Python Extensio.. 33 KB   
jupyter.py 2019/11/25 11:18 Python File 1KB kiwisolver.cp36-win_amd64.pyd 2019/11/25 11:18 Python Extensio... 140 KB entrypoints.py 2019/11/25 11:18 Python File 9 KB pandocfilters.py 2019/11/25 11:18 Python File 9 KB mssql.cp36-win_amd64.pyd 2019/11/25 11:17 Python Extensio.... 2,178 KB six.py 2019/11/25 11:17 Python File 32 KB pylab.py 2019/11/25 11:16 Python File 1KB README.txt 2019/11/25 11:16 文本文档 1 KB pickleshare.py 2019/11/25 11:16 Python File 10 KB setuputils.py 2019/11/25 11:16 Python File 1KB termcolor.py 2019/11/25 11:16 Python File 5 KB openpyxl-3.0.6.dist-info 2021/3/4 14:24 文件夹 et xmlfile 2021/3/4 14:24 文件夹 et_xmlfle-1.0.1-py3.6.egg-info 2021/3/4 14:24 文件夹  

# #业务规则相关  

# #交易所委托数量规则  

1. 科创板，连续交易时段限价单笔最大是10 万股，市价单笔最大是5 万股，盘后定价交易单笔最大量是100 万股，200 股起，1 股递增。  

2. 创业板，连续交易时段限价单笔最大30 万股，市价单笔最大15 万股，100 股起，100 股递增。  

3. 主板，6 和0 开头的，连续交易时段单笔最大100 万股，100 股起，100 股递增。  

# #策略运行相关  

# #在策略没有勾选终端启动后自动运行的情况下，策略自动启动运行  

# 情况一  

策略被运行于行情界面的副图上，随客户端启动被启动  

解决方法  

在右上角的页面布局中选择恢复默认布局，并重启客户端  

![](images/86acab5aeb93e5cb67587613bec43fdc148d0846804d1360bc92e2597e928a76.jpg)  

# 情况二  

交易日切换/行情断线重连时，所有挂着的模型会被重新运行，这是正常的  

# #策略回测相关  

# #QMT 在回测时如何选择复权方式  

# 解答  

回测是为了更贴近历史数据，但实际中各类配股、增发的动作，会造成价格的异常波动，为了避免这样的波动对回测的影响，我们推荐用户在回测中使用等比前复权价，这样在回测过程中，无需考虑配股、增发带来的变化，始终以统一标准的价格进行买卖，方便的同时也能得到更贴合历史数据的回测收益和表现。  

# #交易相关  

# #系统对象 ContextInfo 逐 k 线保存的机制  

# 机制说明  

ContextInfo 是由底层维护并传递给init、handlebar 等系统函数的参数，同一个bar（不是 bar 里面的 tick，下同）内ContextInfo 本质上是同一个变量且对其进行的修改只会对本次handlebar 调用的下文所起作用。handlebar 里对ContextInfo做的修改在该 bar 结束后才会进行保存，也就是说，对ContextInfo 做的修改会在下一个 bar 体现出来。  

具体来说，ContextInfo 不同于一般 python 对象，做了逐 k 线更新设计，盘中主图品种每个 Level 1 分笔到达会触发handlebar 函数调用，但只有 k 线结束时最后一个分笔触发的handlebar 调用，对ContextInfo 的修改才有效。  

每次handlebar 函数调用前会对ContextInfo 对象进行深拷贝, 下一次分笔行情到来时，如果新的分笔不是新 k 线 bar 第一个分笔，则判断上一个分笔不是k 线最后分笔，ContextInfo 对象被回退为之前深拷贝的那个。  

ContextInfo 对象逐k 线更新机制设计的目的，是为了在盘中时模拟k 线的效果，只在k 线结束的分笔触发的handlebar 函数运行时生效一次，丢弃所有其他分笔的修改。  

# 影响  

该机制有两个影响，一是在ContextInfo 对象中存数据每次分笔到达时会被深拷贝，拖慢策略运行；二是ContextInfo 适用于记录逐k 线生效的交易信号（quickTrade 参数传0），不适宜立刻下单的情况。  

如不需要模拟k 线效果，希望调用交易函数后立刻下单，quickTrade 参数可以传2， 下单记录可以用普通的全局变量保存, 不能存在ContextInfo 对象的属性里(实现可以参考实盘示例7-调整至目标持仓Demo)。  

# #快速交易参数 quickTrade  

下单函数passorder 有可选参数快速交易quickTrade， 默认为0。  

传0，只在k 线结束分笔时调用passorder 产生有效信号，其他情况调用不产生信号。  
传1，在当前k 线为最新k 线时调用passorder 函数产生有效信号, 历史k 线调用不产生信号。  
传2，任何情况下调用passorder 都产生有效信号，不会丢弃任何一次调用的信号。  
如果在定时器注册的回调函数，行情回调函数, after_init 函数中调用下单函数，需要传2，确保不会漏单。  

passorder 以外的下单函数不能指定快速交易参数，效果与传0 的passorder 一致。  

# #下单与回报相关  

1. 为保证以尽快的速度执行交易信号, qmt 客户端提供的交易接口是异步的, 以快速交易参数填2 的passorder 函数为例，调用后会立刻发出委托,然后返回。不会等待委托回报, 也不会阻塞python 线程的运行。  

2. 委托/成交/持仓/账号信息的更新, 是在客户端后台进行的, python 策略中无法手动控制。python 提供的取账号信息接口 get_trade_detail_data，与四种交易回调函数, 都是从客户端本地缓存中读取数据 / 触发调用，不是调用时查询柜台再返回。客户端本地缓存状态定期接收柜台推送刷新，有交易主推的柜台50ms 一次，没有交易主推的柜台1-6 秒一次。不能认为get_trade_detail_data 查到的状态是与柜台完全一致的, 比如卖出委托后立刻查询, 不会查到对应委托, 可用资金也不会变多。  

3. 实盘策略需要设计盘中保存/更新委托状态的机制。常见的做法是用全局变量字典保存委托状态, 给每一笔委托独立的投资备注作为字典的key，委托状态作为字典的value, 下单后默认设置为待报, 之后查到委托后更新状态。如果某品种股票存在待报状态委托, 暂停该品种后续报单, 防止发生超单的情况。(实现可以参考实盘示例7-调整至目标持仓Demo)  

4. QMT 所有策略是在同一个线程中被调用的，任意一个策略阻塞线程(死循环 sleep 加锁等操作)会导致所有策略的执行被阻塞，所以不能在策略里写等待操作。如需要多线程 / 多进程的用法，可以使用极简模式配合xtquant 库使用  

# #QMT 下单失败  

1. 检查是否是在模型交易界面，实盘模式运行的策略。模拟模式只显示策略信号，不发出委托。  
2. 如运行到交易函数，未看到策略信号，检查交易函数是否使用了快速下单参数(quickTrade)，默认为0，只会在k 线结束发出委托，日线及以上周期等于全天不会委托。传1 时，非历史bar 上执行时（ContextInfo.is_last_bar()为True），只要策略模型中调用到就触发下单交易。传2，无论是否是历史bar，运行到交易函数时立刻发出委托。  

如果希望盘中出现信号立即下单，建议传1，这种情况下会有策略信号闪烁的风险，需要自己处理；如果希望K 线结束下单（信号不闪烁），建议传0，通常情况下不建议传2  

# 提示  

具体到场景：  

1.  handlebar 逐k 线下单, 每次k 线结束的分笔生效一次, 传 $0;$   
2.  需要在handlebar 盘中触发立刻下单, 传1;  
3.  定时器/init/after_init 与交易回调函数, 行情回调函数内下单, 传2.  
3. 如看到实盘的策略信号，未找到对应委托，检查客户端左下角消息提示是否有报  
错，如有，请根据消息提示的描述修改下单参数  

# #行情相关  

# #QMT 行情数据基础概念  

QMT 行情数据主要分为三种，包括本地数据，全推数据，订阅数据。  

1. 本地数据： 指下载到本地的行情数据加密文件。包括历史数据，适合回测模式使用，对应python 接口为get_market_data_ex(subscribe=False) 在新窗口打开  

2. 全推数据： 指客户端启动后, 自动接收，更新的全市场最新数据快照，包括日线的开高低收,成交量成交额，与五档盘口（在行情界面选择了五档行情时可用五档 具体见行情常规问题3）。支持取全市场品种, 只有最新值，没有历史值，服务器对交易所下发的数据即时转发，打包增量部分发送给下游客户端。可以用get_full_tick 一次性取出当前最新值，也可以用subscribe_whole_quote 注册回调函数，每次处理增量的部分。 对应python 接口为get_full_tick 在新窗口打开，subscribe_whole_quote 在新窗口打开  

3. 订阅：指向行情服务器订阅指定品种行情, 共有四种周期(分笔 1 分钟5 分钟 日线)，可以订阅当日数据，当天以前的需要用 down_history_data下. 订阅有最大数量限制(例如：假设最大数量限制为300 个，则可以单独订阅日线300 个，若同时订阅日线和五分钟 则各150 个)，如需订阅超过300 个限额，可以在页面右上角，选购行情vip 服务。对应  

python 接口为subscribe_quote 在新窗口打开和get_market_data_ex(subscribe $=$ True,)在新窗口打开其中，使用get_market_data 或get_market_data_ex(subscribe $:=$ True,)时客户端会自动订阅传入的品种，不需要额外调用subscibe_quote,但这种方式订阅的品种没有订阅号，无法手动反订阅，只能通过停止策略释放可订阅数。  

# 警告  

如果超出订阅数量限制，则返回的行情数据会使用前值填充，出现重复值，非正确行情数据。  

# #QMT 行情调用函数对比说明  

down_history_data 下载指定区间的行情数据到本地，存放在硬盘上。效果和界面,点击行情数据下载一致。 开始时间不填时，为增量下载(以本地数据最后一天为开始时间), 填写的话按填写值下载。  
get_local_data 取本地数据函数，盘中不会更新，速度快，回测可以用这个函数取。get_full_tick 取客户端缓存中的最新全推数据。全推数据不包括历史，不用订阅，没有品种数量限制，盘中50ms 更新一次，速度快。  
subscribe_quote 向服务器订阅股票行情 盘中实时更新 初次订阅耗时长，最大订阅品种数受限. 订阅超过一定数量的品种k 线行情不会更新.可订阅四种基本周期(分笔 一分钟 五分钟 日线)行情（如果有 Level-2 行情权限 也可以订 Level-2 的）,同一品种订阅了不同周期累加计数(如订阅浦发银行 1 分钟 5 分钟 日线行情 算订阅3 次). 复数策略订阅同一品种计数不会累加. Level-2 的订阅也会受限，但是和Level 1 的互不影响。  
unsubscribe_quote 按订阅号反订阅行情, 释放可订阅数.  
get_market_data_ex 取订阅/本地数据接口。用subscribe_quote 在init 函数中先订阅后subscribe 参数为True 时，取本地数据和订阅的最新行情。subscribe 参数传False 时,可以用来取本地数据，不会订阅。 如股票池超过一定数量，可  
用 down_history_data $^+$ get_local_data $^+$ get_full_tick 拼接历史和最新数据替代get_market_data_ex。  

# 注意  

gmd 系列函数在init 中运行时，只能读取到本地数据，不会取到最新行情数据，因子，不建议在init 中调用使用gmd 系列函数  

# 警告  

不再推荐使用!  

set_universe, get_history_data, get_market_data 是早期订阅股票池, 取订阅的行情数据接口. 因为set_universe 订阅的品种没有订阅号 无法在策略中反订阅, 只能通过停止策略释放订阅数。  

#全推接口和订阅接口的分笔行情没有5 档行情，只有最新价  

问题描述  

get_full_tick, subscribe_while_quote 函数中获取分笔行情没有5 档行情，只有最新价。  

# 解决办法  

修改行情源对应的全推行情级别，见下图  

![](images/ab8752cd0180952824a602e3d29fd2b68acd57b10fb34ee6ec82a962c7071f0e.jpg)  
或者  

![](images/291c0d2b512dbc8117e1aae5c427360eac0edf177ecf23b1ab25ba03f5366dd4.jpg)  

# #行情中心和交易中心到底有啥区别？  

行情中心控制单支订阅，例如subscribe_quote交易中心影响全推数据，例如get_full_tick,subscribe_whole_quote  

# #passorder 使用对手价下单报错/有误  

# 问题描述  

passorder 参数prType 填写14(对手价下单)时，委托价格有误，或信息提示对手价无效，无法下单!  

# 解决办法  

修改行情源对应的全推行情级别，见下图  

![](images/d7abd7dca605403d2182b71350d41346829878f61243599d3c5de4309c9bf0ed.jpg)  
或者  

![](images/692a02af40968c0302ec0c2f2b9fbc9f242dce202b65c4f488ca4e92cf7f31b1.jpg)  

# #为什么在handlebar 中获取期货tick 时，tick 是3S 一个而非0.5s 一个？  

这是由于handlebar 函数是逐K 线驱动在新窗口打开的，在实时行情中，  

handlebar 会随着主图标的tick 的更新被调用。  

在这个问题场景中，主图的标的通常被设置为股票，而股票的tick 通常是3s 一个，这就导致handlebar 函数3s 才被调用一次  

# 解决方法  

1. 使用定时器(run_time)在新窗口打开进行计算  
2. 使用订阅推送(subscribe)在新窗口打开,在回调函数中进行计算  
3. 如果需要在handlebar 中进行期货策略编写，建议将主图设置为期货品种，来保证handlebar 调用频率  

# #为什么在非交易时间段handlebar 也会被调用  

handlebar 受行情数据推送驱动，在非交易时段，行情服务会做一系列准备工作，其中可能伴随着服务重启，在重启后为了保证数据齐全，客户端会重新订阅数据，这时服务会推送最新的数据，客户端会把推送的最新数据更新至缓存，并向上层策略推送更新，也就是触发handlebar 执行  

这个合并数据的驱动执行只会在最新一根bar 而不会在历史范围，策略可以根据需要处理这次推送或直接根据交易时间跳过这个驱动，例如判断time 小于09:15 则直接return  

# #关于证券状态openint 值的详细说明  

沪市  

<html><body><table><tr><td>时间段</td><td>状态</td><td>编码</td></tr><tr><td>9:15 -9:25</td><td>盘前集合竞价</td><td>12</td></tr><tr><td>9:25 -14:57</td><td>盘中连续竞价</td><td>13</td></tr><tr><td>14:57 - 15:00</td><td>盘后集合竞价</td><td>18</td></tr><tr><td>15:00</td><td>收盘状态</td><td>15</td></tr><tr><td>15:05-15:30</td><td>盘后定价</td><td>22</td></tr><tr><td>15:30</td><td>盘后定价结束</td><td>23</td></tr><tr><td>上一状态后</td><td>收盘状态</td><td>15</td></tr></table></body></html>  

时间段 状态 编码9:15 - 9:25 盘前集合竞价 129:25 - 9:30 休市 14  

时间段 状态 编码  
9:30 - 11:30 盘中连续竞价 13  
11:30 - 13:00 休市 14  
13:00 - 14:57 盘中连续竞价 13  
14:57 - 15:00 盘后集合竞价 18  
15:00 发收盘状态 15  
15:05 - 15:30 盘后定价 22  
15:30 盘后定价结束 23  
上一状态后 收盘状态 15  

# #静态数据问题  

# #报错：[系统]ERROR：\*\*\*\*\*\*.\*\*获取合约乘数和最小变动价 位失败，跳过  

点击右下角【行情】按钮，选择【智能下载】，数据选项下拉框勾选【过期合约列表】点击该面板右下角【开始】，待过期合约数据补充完毕后，即可正常获取过期合约数据。  

# #软件运行日志相关  

# #如何找到软件运行日志  

Log 文件通常在安装目录下的.\userdata\log 文件夹中，在 .\userdata\log 文件夹中，你可能会看到一个或者多个 log 文件，通常以 '.log' 作为扩展名。这些文件将包含软件运行时的详细情况。  

投研：{安装目录}\userdata\log  

说明  

XtClient_20210922.log - 客户端常规日志  

XtClient_datasource_20210922.log - 行情数据日志  

XtClient_Formula_20210922.log - 策略运行日志  

XtClient_FormulaOutput.log - 策略输出日志  

QMT：{安装目录}\userdata\log  

# 说明  

XtClient_20210922.log - 客户端常规日志  

XtClient_Formula_20210922.log - 策略运行日志  

XtClient_FormulaOutput.log - 策略输出日志  

XtClient_PerformanceFile_20210922.log - 客户端流程节点日志  

极简模式：{安装目录}\userdata_mini\log  

# 说明  

XtMiniQuote_20210917.log - 行情策略模块日志  

XtMiniQmt_20210917.log - 客户端常规日志  

XtMiniQmt_perform_20210917.log - 客户端流程节点日志  