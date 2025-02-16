基础信息  

接口：stock_basic，可以通过数据工具调试和查看数据  

描述：获取基础信息数据，包括股票代码、名称、上市日期、退市日期等  

权限：2000 积分起。此接口是基础信息，调取一次就可以拉取完，建议保存倒本地存储后使用  

输入参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>必选</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td>N</td><td>TS股票代码</td></tr><tr><td>name</td><td>str</td><td>N</td><td>名称</td></tr><tr><td>market</td><td>str</td><td>N</td><td>市场类别 （主板/创业板/科创板/CDR/北交所）</td></tr><tr><td>list_status</td><td>str</td><td>N</td><td>上市状态L上市D退市P暂停上市，默认是L</td></tr><tr><td>exchange</td><td>str</td><td>N</td><td>交易所 SSE上交所 SZSE深交所 BSE 北交所</td></tr><tr><td>is_hs</td><td>str</td><td>N</td><td>是否沪深港通标的，N否H沪股通S深股通</td></tr></table></body></html>  

输出参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td>Y</td><td>TS代码</td></tr><tr><td>symbol</td><td>str</td><td>Y</td><td>股票代码</td></tr><tr><td>name</td><td>str</td><td>Y</td><td>股票名称</td></tr><tr><td>area</td><td>str</td><td>Y</td><td>地域</td></tr><tr><td>industry</td><td>str</td><td>Y</td><td>所属行业</td></tr><tr><td>fullname</td><td>str</td><td>N</td><td>股票全称</td></tr><tr><td>enname</td><td>str</td><td>N</td><td>英文全称</td></tr><tr><td>cnspell</td><td>str</td><td>Y</td><td>拼音缩写</td></tr><tr><td>market</td><td>str</td><td>Y</td><td>市场类型 (主板/创业板/科创板/CDR)</td></tr><tr><td>exchange</td><td>str</td><td>N</td><td>交易所代码</td></tr><tr><td>curr_type</td><td>str</td><td>N</td><td>交易货币</td></tr><tr><td>list_status</td><td>str</td><td>N</td><td>上市状态L上市 D退市 P暂停上市</td></tr><tr><td>list_date</td><td>str</td><td>Y</td><td>上市日期</td></tr><tr><td>delist_date</td><td>str</td><td>N</td><td>退市日期</td></tr><tr><td>is_hs</td><td>str</td><td>N</td><td>是否沪深港通标的，N 否 H 沪股通 S 深股通</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>act_name</td><td>str</td><td>Y</td><td>实控人名称</td></tr><tr><td>act_ent_type</td><td>str</td><td>Y</td><td>实控人企业性质</td></tr></table></body></html>  

说明：旧版上的PE/PB/股本等字段，请在行情接口“每日指标”中获取。  

# 接口示例  

pro $=$ ts.pro_api()  

#查询当前所有正常上市交易的股票列表  

data pro.stock_basic(exchange $=$ '', list_status $=$ 'L', fields $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ 'ts_code,symbol,name,area,industry,list_date')  

或者：  

#查询当前所有正常上市交易的股票列表  

data = pro.query('stock_basic', exchange $:=$ '', list_status $=$ 'L', fields $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ 'ts_code,symbol,name,area,industry,list_date')  

# 数据样例  

ts_code symbol name area industry list_date  
0 000001.SZ 000001 平安银行 深圳 银行 19910403  
1 000002.SZ 000002 万科A 深圳 全国地产 19910129  
2 000004.SZ 000004 国农科技 深圳 生物制药 19910114  
3 000005.SZ 000005 世纪星源 深圳 房产服务 19901210  
4 000006.SZ 000006 深振业A 深圳 区域地产 19920427  
5 000007.SZ 000007 全新好 深圳 酒店餐饮 19920413  
6 000008.SZ 000008 神州高铁 北京 运输设备 19920507  
7 000009.SZ 000009 中国宝安 深圳 综合类 19910625  
8 000010.SZ 000010 美丽生态 深圳 建筑施工 19951027  
9 000011.SZ 000011 深物业A 深圳 区域地产 19920330  
10 000012.SZ 000012 南玻A 深圳 玻璃 19920228  
11 000014.SZ 000014 沙河股份 深圳 全国地产 19920602  
12 000016.SZ 000016 深康佳A 深圳 家用电器 19920327  
13 000017.SZ 000017 深中华A 深圳 文教休闲 19920331  
14 000018.SZ 000018 神州长城 深圳 装修装饰 19920616  
15 000019.SZ 000019 深深宝A 深圳 软饮料 19921012  
16 000020.SZ 000020 深华发A 深圳 元器件 19920428  
17 000021.SZ 000021 深科技 深圳 电脑设备 19940202  
18 000022.SZ 000022 深赤湾A 深圳 港口 19930505  
19 000023.SZ 000023 深天地A 深圳 其他建材 19930429  
20 000025.SZ 000025 特力A 深圳 汽车服务 19930621  

# 股本情况（盘前）  

接口：stk_premarket  

描述：每日开盘前获取当日股票的股本情况，包括总股本和流通股本，涨跌停价格等。  

限量：单次最大8000 条数据，可循环提取  

权限：与积分无关，需单独开权限  

输入参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>必选</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td>N</td><td>股票代码</td></tr><tr><td>trade_date</td><td>str</td><td>N</td><td>交易日期(YYYYMMDD 格式，下同)</td></tr><tr><td>start_date</td><td>str</td><td>N</td><td>开始日期</td></tr><tr><td>end_date</td><td>str</td><td>N</td><td>结束日期</td></tr></table></body></html>  

# 输出参数  

<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>trade_date</td><td>str</td><td>V</td><td>交易日期</td></tr><tr><td>ts_code</td><td>str</td><td>Y</td><td>TS股票代码</td></tr><tr><td>total_share</td><td>float</td><td>Y</td><td>总股本 (万股)</td></tr><tr><td>float_share</td><td>float</td><td>Y</td><td>流通股本 (万股)</td></tr><tr><td>pre_close</td><td>float</td><td>Y</td><td>昨日收盘价</td></tr><tr><td>up_limit</td><td>float</td><td>Y</td><td>今日涨停价</td></tr><tr><td>down_limit</td><td>float</td><td>Y</td><td>今日跌停价</td></tr></table></body></html>  

# 接口示例  

pro $=$ ts.pro_api()  

#获取某一日盘前所有股票当日的最新股本 df $=$ pro.stk_premarket(trade_date $=$ '20240603')  

# 数据示例  

trade_date ts_code total_share  float_share pre_close up _limit down_limit  

0 20240603  001387.SZ 17778.8000 4355.7297 17.000   
18.700 15.300   
1 20240603  600460.SH 166407.1845  166407.1845 18.790   
20.670 16.910   
2 20240603 603052.SH 13484.8000 4096.4000 30.270   
33.300 27.240   
3 20240603 603269.SH 22053.6977 22053.6977 10.140   
11.150 9.130   
4 20240603 001339.SZ 24974.4000 7157.2575 29.210   
32.130 26.290   
5335 20240603 603567.SH 94196.3592 93954.0524 12.340   
13.570 11.110   
5336 20240603  301188.SZ 23245.0244 15044.4508 17.740   
21.290 14.190   
5337 20240603  603939.SH 101057.9797 100811.6102 45.060   
49.570 40.550   
5338 20240603  300441.SZ 65225.6868 63480.0236 6.460   
7.750 5.170   
5339 20240603  920002.BJ 3175.2120 475.0000 None   
77.840 41.920  

# 交易日历  

接口：trade_cal，可以通过数据工具调试和查看数据。  

描述：获取各大交易所交易日历数据,默认提取的是上交所  

积分：需2000 积分  

<html><body><table><tr><td>名称</td><td>类 型</td><td>必 选</td><td>描述</td></tr><tr><td>exchange</td><td>str</td><td>N</td><td>交易所 SSE上交所,SZSE深交所,CFFEX 中金所,SHFE上期所,CZCE 所,INE上能源</td></tr><tr><td>start_date</td><td>str</td><td>N</td><td>开始日期（格式：YYYYMMDD下同）</td></tr><tr><td>end_date</td><td>str</td><td>N</td><td>结束日期</td></tr><tr><td>is_open</td><td>str</td><td>N</td><td>是否交易'0'休市'1交易</td></tr></table></body></html>  

输出参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>exchange</td><td>str</td><td></td><td>交易所 SSE上交所 SZSE深交所</td></tr><tr><td>cal_date</td><td>str</td><td></td><td>日历日期</td></tr><tr><td>is_open</td><td>str</td><td></td><td>是否交易0休市1交易</td></tr><tr><td>pretrade_date</td><td>str</td><td></td><td>上一个交易日</td></tr></table></body></html>  

# 接口示例  

pro $=$ ts.pro_api()  

df $=$ pro.trade_cal(exchange $^{1=}$ '', start_date $=$ '20180101', end_date $=`26181231`$ )  

或者  

df $=$ pro.query('trade_cal', start_date $=$ '20180101', end_date='20 181231')  

# 数据样例  

<html><body><table><tr><td>exchange</td><td>cal_date</td><td></td><td>is_open</td></tr><tr><td>0</td><td>SSE</td><td>20180101</td><td>0</td></tr><tr><td>1</td><td>SSE</td><td>20180102</td><td>1</td></tr><tr><td>2</td><td>SSE</td><td>20180103</td><td>1</td></tr><tr><td>3</td><td>SSE</td><td>20180104</td><td>1</td></tr><tr><td>4</td><td>SSE</td><td>20180105</td><td>1</td></tr><tr><td>5</td><td>SSE</td><td>20180106</td><td>0</td></tr><tr><td>6</td><td>SSE</td><td>20180107</td><td></td></tr><tr><td>7</td><td>SSE</td><td>20180108</td><td>1</td></tr><tr><td>8</td><td>SSE</td><td>20180109</td><td>1</td></tr><tr><td>9</td><td>SSE</td><td>20180110</td><td>1</td></tr><tr><td>10</td><td>SSE</td><td>20180111</td><td>1</td></tr><tr><td>11</td><td>SSE</td><td>20180112</td><td>1</td></tr><tr><td>12</td><td>SSE</td><td>20180113</td><td></td></tr><tr><td>13</td><td>SSE</td><td>20180114</td><td>0</td></tr><tr><td>14</td><td>SSE</td><td>20180115</td><td>1</td></tr><tr><td>15</td><td>SSE</td><td>20180116</td><td>1</td></tr><tr><td>16</td><td>SSE</td><td>20180117</td><td>1</td></tr><tr><td>17</td><td>SSE</td><td>20180118</td><td>1</td></tr><tr><td>18</td><td>SSE</td><td>20180119</td><td>1</td></tr><tr><td>19</td><td>SSE</td><td>20180120</td><td>0</td></tr><tr><td>20</td><td>SSE</td><td>20180121</td><td>0</td></tr></table></body></html>  

# 股票曾用名  

描述：历史名称变更记录  

输入参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>必选</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td>N</td><td>TS代码</td></tr><tr><td>start_date</td><td>str</td><td>N</td><td>公告开始日期</td></tr><tr><td>end_date</td><td>str</td><td>N</td><td>公告结束日期</td></tr></table></body></html>  

输出参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>默认输出</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td>Y</td><td>TS代</td></tr><tr><td>name</td><td>str</td><td>Y</td><td>证券名</td></tr><tr><td>start_date</td><td>str</td><td>Y</td><td>开始日</td></tr><tr><td>end_date</td><td>str</td><td>Y</td><td>结束日</td></tr><tr><td>ann_date</td><td>str</td><td>Y</td><td>公告日</td></tr><tr><td>change_reason</td><td>str</td><td>Y</td><td>变更原</td></tr></table></body></html>  

# 接口示例  

pro $=$ ts.pro_api()  

df $=$ pro.namechange(ts_code $=$ '600848.SH', fields $=$ 'ts_code,name,s tart_date,end_date,change_reason')  

# 数据样例  

ts_code name start_date end_date change_reason  
0 600848.SH 上海临港 20151118 None 改名  
1 600848.SH 自仪股份 20070514 20151117 撤销ST  
2 600848.SH ST 自仪 20061026 20070513 完成股改  
3 600848.SH SST 自仪 20061009 20061025 未股改加S  
4 600848.SH ST 自仪 20010508 20061008 ST  
5 600848.SH 自仪股份 19940324 20010507 其他  

# 沪深股通成份股  

# 接口：hs_const  

描述：获取沪股通、深股通成分数据  

输入参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>必选</td><td>描述</td></tr><tr><td>hs_type</td><td>str</td><td>Y</td><td>类型SH沪股通SZ深股通</td></tr><tr><td>is_new</td><td>str</td><td>N</td><td>是否最新 1 是 0 否 (默认 1)</td></tr></table></body></html>  

输出参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td>V</td><td>TS代码</td></tr><tr><td>hs_type</td><td>str</td><td></td><td>沪深港通类型SH沪SZ深</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>in_date</td><td>str</td><td></td><td>纳入日期</td></tr><tr><td>out_date</td><td>str</td><td></td><td>剔除日期</td></tr><tr><td>is_new</td><td>str</td><td></td><td>是否最新1是0否</td></tr></table></body></html>  

# 接口使用  

pro $=$ ts.pro_api()  

#获取沪股通成分 df $=$ pro.hs_const(hs_type $=$ 'SH')  

#获取深股通成分 df $=$ pro.hs_const(hs_type='SZ')  

# 数据样例  

ts_code hs_type in_date out_date is_new   
0 603818.SH SH 20160613 None 1   
1 603108.SH SH 20161212 None 1   
2 600507.SH SH 20141117 None 1   
3 601377.SH SH 20141117 None 1   
4 600309.SH SH 20141117 None 1   
5 600298.SH SH 20141117 None 1   
6 600018.SH SH 20141117 None 1   
7 600483.SH SH 20151214 None 1   
8 600068.SH SH 20141117 None 1   
9 600594.SH SH 20141117 None 1   
10 603806.SH SH 20160613 None 1   
11 600867.SH SH 20141117 None 1   
12 601012.SH SH 20141117 None 1   
13 601231.SH SH 20141117 None 1   
14 601888.SH SH 20151214 None 1   
15 601099.SH SH 20141117 None 1   
16 603025.SH SH 20151214 None 1  

# 上市公司基本信息  

接口：stock_company，可以通过数据工具调试和查看数据。  

描述：获取上市公司基础信息，单次提取4500 条，可以根据交易所分批提取  

积分：用户需要至少120 积分才可以调取，具体请参阅积分获取办法  

输入参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>必须</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td>N</td><td>股票代码</td></tr><tr><td>exchange</td><td>str</td><td>N</td><td>交易所代码，SSE上交所 SZSE深交所 BSE北交所</td></tr></table></body></html>  

输出参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td>Y</td><td>股票代码</td></tr><tr><td>com_name</td><td>str</td><td>Y</td><td>公司全称</td></tr><tr><td>com_id</td><td>str</td><td>Y</td><td>统一社会信用代码</td></tr><tr><td>exchange</td><td>str</td><td>Y</td><td>交易所代码</td></tr><tr><td>chairman</td><td>str</td><td></td><td>法人代表</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>manager</td><td>str</td><td>Y</td><td>总经理</td></tr><tr><td>secretary</td><td>str</td><td>Y</td><td>董秘</td></tr><tr><td>reg_capital</td><td>float</td><td>Y</td><td>注册资本(万元)</td></tr><tr><td>setup_date</td><td>str</td><td>Y</td><td>注册日期</td></tr><tr><td>province</td><td>str</td><td>Y</td><td>所在省份</td></tr><tr><td>city</td><td>str</td><td>Y</td><td>所在城市</td></tr><tr><td>introduction</td><td>str</td><td>N</td><td>公司介绍</td></tr><tr><td>website</td><td>str</td><td>Y</td><td>公司主页</td></tr><tr><td>email</td><td>str</td><td>Y</td><td>电子邮件</td></tr><tr><td>office</td><td>str</td><td>N</td><td>办公室</td></tr><tr><td>employees</td><td>int</td><td>Y</td><td>员工人数</td></tr><tr><td>main_business</td><td>str</td><td>N</td><td>主要业务及产品</td></tr><tr><td>business_scope</td><td>str</td><td>N</td><td>经营范围</td></tr></table></body></html>  

# 接口示例  

pro $=$ ts.pro_api()  

#或者 #pro $=$ ts.pro_api('your token')  

df $=$ pro.stock_company(exchange $=$ 'SZSE', fields $=$ 'ts_code,chairma n,manager,secretary,reg_capital,setup_date,province')  

# 数据示例  

ts_code chairman manager secretary reg_capital setup_date province  

0 000001.SZ 谢永林 胡跃飞 周强 1.717041e+06  
19871222 广东  
1 000002.SZ 郁亮 祝九胜 朱旭 1.103915e+06  
19840530 广东  
2 000003.SZ 马钟鸿 马钟鸿 安汪 3.334336e+04  
19880208 广东  
3 000004.SZ 李林琳 李林琳 徐文苏 8.397668e+03  
19860505 广东  
4 000005.SZ 丁芃 郑列列 罗晓春  1.058537e+05  
19870730 广东  
5 000006.SZ 赵宏伟 朱新宏 杜汛  1.349995e+05  
19850525 广东  
6 000007.SZ 智德宇 智德宇 陈伟彬 3.464480e+04  
19830311 广东  
7 000008.SZ 王志全 钟岩 王志刚 2.818330e+05  
19891011 北京  
8 000009.SZ 陈政立 陈政立 郭山清 2.149345e+05  
19830706 广东  
9 000010.SZ 曾嵘 李德友 金小刚 8.198547e+04  
19881231 广东  
10 000011.SZ 刘声向 王航军 范维平 5.959791e+04  
19830117 广东  
11 000012.SZ 陈琳 王健 杨昕宇  2.863277e+05  
19840910 广东  
12 000013.SZ 厉怒江 阮克竖 刘渝敏  3.033550e+04  
19920114 广东  
13 000014.SZ 陈勇 温毅 王凡  2.017052e+04 1  
9870727 广东  
14 000015.SZ 宿南南 马骧 蒋孝安 1.598761e+05  
19880408 广东  
15 000016.SZ 刘凤喜 周彬 吴勇军  2.407945e+05  
19801001 广东  

# IPO 新股列表  

接口：new_share  
描述：获取新股上市列表数据  
限量：单次最大2000 条，总量不限制  
积分：用户需要至少120 积分才可以调取，具体请参阅积分获取办法  

输入参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>必选</td><td>描述</td></tr><tr><td>start_date</td><td>str</td><td>N</td><td>上网发行开始日期</td></tr><tr><td>end_date</td><td>str</td><td>N</td><td>上网发行结束日期</td></tr></table></body></html>  

输出参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td>Y</td><td>TS股票代码</td></tr><tr><td>sub_code</td><td>str</td><td>Y</td><td>申购代码</td></tr><tr><td>name</td><td>str</td><td>Y</td><td>名称</td></tr><tr><td>ipo_date</td><td>str</td><td>Y</td><td>上网发行日期</td></tr><tr><td>issue_date</td><td>str</td><td>Y</td><td>上市日期</td></tr><tr><td>amount</td><td>float</td><td>Y</td><td>发行总量 (万股)</td></tr><tr><td>market_amount</td><td>float</td><td>V</td><td>上网发行总量 (万股)</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>price</td><td>float</td><td></td><td>发行价格</td></tr><tr><td>pe</td><td>float</td><td></td><td>市盈率</td></tr><tr><td>limit_amount</td><td>float</td><td></td><td>个人申购上限 (万股)</td></tr><tr><td>funds</td><td>float</td><td></td><td>募集资金 (亿元)</td></tr><tr><td>ballot</td><td>float</td><td></td><td>中签率</td></tr></table></body></html>  

# 接口示例  

pro $=$ ts.pro_api()  

df $=$ pro.new_share(start_date $^{1=}$ '20180901', end_date $=$ '20181018')  

# 数据示例  

ts_code sub_code  name  ipo_date issue_date amount market_amount \  

0 002939.SZ 002939 长城证券 20181017 None 31034.0 27931.0   
1 002940.SZ 002940 昂利康 20181011 20181023 2250.0 2025.0   
2 601162.SH 780162 天风证券 20181009 20181019 51800.0 46620.0   
3 300694.SZ 300694 蠡湖股份 20180927 20181015 5383.0 4845.0   
4 300760.SZ 300760 迈瑞医疗 20180927 20181016 12160.0 10944.0   
5 300749.SZ 300749 顶固集创 20180913 20180925 2850.0 2565.0   
6 002937.SZ 002937 兴瑞科技 20180912 20180926 4600.0 4140.0 601577.SH 780577 长沙银行 20180912 20180926 34216.0  

30794.0  

8 603583.SH 732583 捷昌驱动 20180911 20180921 3020.0 2718.0   
9 002936.SZ 002936 郑州银行 20180907 20180919 60000.0 54000.0   
10 300748.SZ 300748 金力永磁 20180906 20180921 4160.0 3744.0   
11 603810.SH 732810 丰山集团 20180906 20180917 2000.0 2000.0   
12 002938.SZ 002938 鹏鼎控股 20180905 20180918 23114.0 20803.0 price pe limit_amount funds ballot   
0 6.31 22.98 9.30 19.582 0.16   
1 23.07 22.99 0.90 5.191 0.03   
2 1.79 22.86 15.50 0.000 0.25   
3 9.89 22.98 2.15 5.324 0.04   
4 48.80 22.99 3.60 59.341 0.08   
5 12.22 22.99 1.10 3.483 0.03   
6 9.94 22.99 1.80 4.572 0.04   
7 7.99 6.97 10.20 27.338 0.17   
8 29.17 22.99 1.20 8.809 0.03   
9 4.59 6.50 18.00 27.540 0.25   
10 5.39 22.98 1.20 2.242 0.05   
11 25.43 20.39 2.00 5.086 0.02   
12 16.07 22.99 6.90 37.145 0.12  

# 股票历史列表（历史每天股票列表）  

# 接口：bak_basic  

描述：获取备用基础列表，数据从2016 年开始  

限量：单次最大7000 条，可以根据日期参数循环获取历史，正式权限需  

要5000 积分。  

输入参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>必选</td><td>描述</td></tr><tr><td>trade_date</td><td>str</td><td>N</td><td>交易日期</td></tr><tr><td>ts_code</td><td>str</td><td>N</td><td>股票代码</td></tr></table></body></html>  

输出参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>trade_date</td><td>str</td><td>Y</td><td>交易日期</td></tr><tr><td>ts_code</td><td>str</td><td>Y</td><td>TS 股票代码</td></tr><tr><td>name</td><td>str</td><td>Y</td><td>股票名称</td></tr><tr><td>industry</td><td>str</td><td>Y</td><td>行业</td></tr><tr><td>area</td><td>str</td><td>V</td><td>地域</td></tr><tr><td>pe</td><td>float</td><td>Y</td><td>市盈率 (动)</td></tr><tr><td>float_share</td><td>float</td><td>Y</td><td>流通股本（亿</td></tr><tr><td>total_share</td><td>float</td><td>Y</td><td>总股本 (亿)</td></tr><tr><td>total_assets</td><td>float</td><td>V</td><td>总资产 (亿)</td></tr><tr><td>liquid_assets</td><td>float</td><td>Y</td><td>流动资产（亿</td></tr><tr><td>fixed_assets</td><td>float</td><td>Y</td><td>固定资产（亿</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>reserved</td><td>float</td><td>Y</td><td>公积金</td></tr><tr><td>reserved_pershare</td><td>float</td><td>Y</td><td>每股公积金</td></tr><tr><td>eps</td><td>float</td><td>Y</td><td>每股收益</td></tr><tr><td>bvps</td><td>float</td><td>Y</td><td>每股净资产</td></tr><tr><td>pb</td><td>float</td><td>Y</td><td>市净率</td></tr><tr><td>list_date</td><td>str</td><td>Y</td><td>上市日期</td></tr><tr><td>undp</td><td>float</td><td>Y</td><td>未分配利润</td></tr><tr><td>per_undp</td><td>float</td><td>Y</td><td>每股未分配利</td></tr><tr><td>rev_yoy</td><td>float</td><td>Y</td><td>收入同比 (%)</td></tr><tr><td>profit_yoy</td><td>float</td><td>Y</td><td>利润同比 (%)</td></tr><tr><td>gpr</td><td>float</td><td>Y</td><td>毛利率（%)</td></tr><tr><td>npr</td><td>float</td><td>Y</td><td>净利润率 (%)</td></tr><tr><td>holder_num</td><td>int</td><td></td><td>股东人数</td></tr></table></body></html>  

# 接口示例  

pro $=$ ts.pro_api()  

df $=$ pro.bak_basic(trade_date $^{1=}$ '20211012', fields $=$ 'trade_date,ts _code,name,industry,pe')  

# 数据样例  

<html><body><table><tr><td colspan="2">trade date</td><td colspan="2">ts_code name industry</td><td colspan="2">pe</td></tr><tr><td>0</td><td>20211012</td><td>300605.SZ</td><td>恒锋信息</td><td>软件服务</td><td>56.4400</td></tr><tr><td>1</td><td>20211012</td><td>301017.SZ</td><td>漱玉平民</td><td>医药商业</td><td>58.7600</td></tr><tr><td>2</td><td>20211012</td><td>300755.SZ</td><td>华致酒行</td><td>其他商业</td><td>23.0000</td></tr><tr><td>3</td><td>20211012</td><td>300255.SZ</td><td>常山药业</td><td>生物制药</td><td>24.9900</td></tr><tr><td>4</td><td>20211012</td><td>688378.SH</td><td>奥来德</td><td>专用机械</td><td>24.9600</td></tr><tr><td></td><td></td><td></td><td></td><td></td><td></td></tr><tr><td>4529</td><td>20211012</td><td>688257.SH</td><td>新锐股份</td><td>机械基件</td><td>0.0000</td></tr><tr><td>4530</td><td>20211012</td><td>688255.SH</td><td>凯尔达</td><td>机械基件</td><td>0.0000</td></tr><tr><td>4531</td><td>20211012</td><td>688211.SH</td><td>中科微至</td><td>专用机械</td><td>0.0000</td></tr><tr><td>4532</td><td>20211012</td><td>605567.SH</td><td>春雪食品</td><td>食品</td><td>0.0000</td></tr><tr><td>4533</td><td>20211012</td><td>605566.SH</td><td>福莱蒽特</td><td>染料涂料</td><td>0.0000</td></tr></table></body></html>  

# A 股日线行情  

接口：daily，可以通过数据工具调试和查看数据  

数据说明：交易日每天15 点～16 点之间入库。本接口是未复权行情，  

停牌期间不提供数据  

调取说明：120 积分每分钟内最多调取500 次，每次6000 条数据，相当于单次提取23 年历史  

描述：获取股票行情数据，或通过通用行情接口获取数据，包含了前后复权数据  

# 输入参数  

<html><body><table><tr><td>名称</td><td>类型</td><td>必选</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td>N</td><td>股票代码（支持多个股票同时提取，逗号分隔)</td></tr><tr><td>trade_date</td><td>str</td><td>N</td><td>交易日期（YYYYMMDD）</td></tr><tr><td>start_date</td><td>str</td><td>N</td><td>开始日期(YYYYMMDD)</td></tr><tr><td>end_date</td><td>str</td><td>N</td><td>结束日期(YYYYMMDD)</td></tr></table></body></html>

注：日期都填YYYYMMDD 格式，比如20181010  

输出参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td>股票代码</td></tr><tr><td>trade_date</td><td>str</td><td>交易日期</td></tr><tr><td>open</td><td>float</td><td>开盘价</td></tr><tr><td>high</td><td>float</td><td>最高价</td></tr><tr><td>low</td><td>float</td><td>最低价</td></tr><tr><td>close</td><td>float</td><td>收盘价</td></tr><tr><td>pre_close</td><td>float</td><td>昨收价【除权价，前复权】</td></tr><tr><td>change</td><td>float</td><td>涨跌额</td></tr><tr><td>pct_chg</td><td>float</td><td>涨跌幅【基于除权后的昨收计算的涨跌幅：（今收-除权昨收）/除权昨</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>描述</td></tr><tr><td>vol</td><td>float</td><td>成交量 （手）</td></tr><tr><td>amount</td><td>float</td><td>成交额 （千元)</td></tr></table></body></html>  

# 接口示例  

pro $=$ ts.pro_api()  

df $=$ pro.daily(ts_code $=$ '000001.SZ', start_date $=$ '20180701', end date $^{1=}$ '20180718')  

#多个股票  

df $=$ pro.daily(ts_code $=$ '000001.SZ,600000.SH', start_date $=$ '20180 701', end_date $=$ '20180718')  

或者  

df $=$ pro.query('daily', ts_code $=$ '000001.SZ', start_date $=$ '201807 $\mathsf{01}^{\prime}$ , end_date $=$ '20180718')  

也可以通过日期取历史某一天的全部历史  

df $=$ pro.daily(trade_date $=$ '20180810')  

# 数据样例  

ts_code trade_date open  high low close pre_close cha nge pct_chg  vol amount  

0 000001.SZ 20180718  8.75  8.85  8.69 8.70 8.72 -0.   
02 -0.23 525152.77 460697.377   
1 000001.SZ 20180717  8.74  8.75  8.66 8.72 8.73 -0.   
01 -0.11 375356.33 326396.994   
2 000001.SZ 20180716  8.85  8.90  8.69 8.73 8.88 -0.   
15 -1.69 689845.58 603427.713   
3 000001.SZ 20180713  8.92  8.94  8.82 8.88 8.88 0.   
00 0.00 603378.21 535401.175   
4 000001.SZ 20180712 8.60 8.97  8.58 8.88 8.64 0.   
24 2.78 1140492.31 1008658.828   
5 000001.SZ 20180711 8.76  8.83  8.68 8.78 8.98 -0.   
20 -2.23 851296.70 744765.824   
6 000001.SZ 20180710 9.02 9.02  8.89 8.98 9.03 -0.   
05 -0.55 896862.02 803038.965   
7 000001.SZ 20180709 8.69 9.03 8.68 9.03 8.66 0.   
37 4.27 1409954.60 1255007.609   
8 000001.SZ 20180706 8.61 8.78 8.45 8.66 8.60 0.   
06 0.70 988282.69 852071.526   
9 000001.SZ 20180705  8.62  8.73  8.55 8.60 8.61 -0.   
01 -0.12 835768.77 722169.579  

# 周线行情  

# 接口：weekly  

描述：获取A 股周线行情  

限量：单次最大4500 行，总量不限制  

积分：用户需要至少2000 积分才可以调取，具体请参阅积分获取办法  

输入参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>必选</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td>N</td><td>TS代码 (ts_code,trade_date 两个参数任选一)</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>必选</td><td>描述</td></tr><tr><td>trade_date</td><td>str</td><td>N</td><td>交易日期 （每周最后一个交易日期，YYYYMMDD格式）</td></tr><tr><td>start_date</td><td>str</td><td>N</td><td>开始日期</td></tr><tr><td>end_date</td><td>str</td><td>N</td><td>结束日期</td></tr></table></body></html>  

输出参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td>Y</td><td>股票代码</td></tr><tr><td>trade_date</td><td>str</td><td>Y</td><td>交易日期</td></tr><tr><td>close</td><td>float</td><td>Y</td><td>周收盘价</td></tr><tr><td>open</td><td>float</td><td>Y</td><td>周开盘价</td></tr><tr><td>high</td><td>float</td><td>Y</td><td>周最高价</td></tr><tr><td>low</td><td>float</td><td>Y</td><td>周最低价</td></tr><tr><td>pre_close</td><td>float</td><td>Y</td><td>上一周收盘价</td></tr><tr><td>change</td><td>float</td><td>Y</td><td>周涨跌额</td></tr><tr><td>pct_chg</td><td>float</td><td>Y</td><td>周涨跌幅 （未复权，如果是复权请用通用行情接口</td></tr><tr><td>vol</td><td>float</td><td>Y</td><td>周成交量</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>amount</td><td>float</td><td>Y</td><td>周成交额</td></tr></table></body></html>  

# 接口用法  

pro $=$ ts.pro_api()  

df $=$ pro.weekly(ts_code $^{1=}$ '000001.SZ', start_date $=$ '20180101', end _date $=$ '20181101', fields $=$ 'ts_code,trade_date,open,high,low,clos e,vol,amount')  

或者  

df $=$ pro.weekly(trade_date $=$ '20181123', fields $=$ 'ts_code,trade_da te,open,high,low,close,vol,amount')  

# 数据样例  

ts_code trade_date close open high low vol   
\   
0 000001.SZ 20181026 11.18 10.81 11.46 10.71 9062500.1   
4   
1 000001.SZ 20181019 10.76 10.39 10.78 9.92 7235319.5   
5   
2 000001.SZ 20181012 10.30 10.70 10.79 9.70 7257596.9   
7   
3 000001.SZ 20180928 11.05 10.52 11.27 10.48 5458134.1   
3   
4 000001.SZ 20180921 10.67 9.80 10.70 9.68 5120305.2   
9   
5 000001.SZ 20180914 9.84 10.01 10.10 9.81 3534261.7   
6   
6 000001.SZ 20180907 10.01 10.09 10.55 9.93 4708303.8   
1   
7 000001.SZ 20180831 10.13 10.02 10.43 9.97 6715867.9   
2   
8 000001.SZ 20180824 10.03 8.90 10.28 8.87 6697713.5   
2   
9 000001.SZ 20180817 8.81 9.12 9.16 8.64 3206923.4   
4   
10 000001.SZ 20180810 9.23 8.94 9.35 8.88 3054338.5   
6   
11 000001.SZ 20180803 8.91 9.32 9.50 8.88 3648566.3   
5   
12 000001.SZ 20180727 9.25 9.04 9.59 9.00 5170189.4   
1   
13 000001.SZ 20180720 9.11 8.85 9.20 8.61 3806004.4   
7   
14 000001.SZ 20180713 8.88 8.69 9.03 8.58 4901983.8   
4   
15 000001.SZ 20180706 8.66 9.05 9.05 8.45 5125563.5   
3   
16 000001.SZ 20180629 9.09 9.91 9.92 8.87 5150575.9   
3   
amount   
0 1.002282e+07   
1 7.482596e+06   
2 7.483906e+06   
3 5.904901e+06   
4 5.225262e+06   
5 3.501724e+06   
6 4.796533e+06   
7 6.858804e+06   
8 6.358840e+06   
9 2.854248e+06   
10 2.787629e+06   
11 3.363448e+06   
12 4.826484e+06   
13 3.371040e+06   
14 4.346872e+06   
15 4.446723e+06   
16 4.764107e+06  

# A 股复权行情  

接口名称 ：pro_bar  

接口说明 ：复权行情通过通用行情接口实现，利用Tushare Pro 提供的复权因子进行动态计算，因此http 方式无法调取。若需要静态复权行情（支持http），请访问股票技术因子接口。  

# Python SDK 版本要求： >= 1.2.26  

复权说明  


<html><body><table><tr><td>类型</td><td>算法</td></tr><tr><td>不复权</td><td>无</td></tr><tr><td>前复权</td><td>当日收盘价×当日复权因子／最新复权因子</td></tr><tr><td>后复权</td><td>当日收盘价×当日复权因子</td></tr></table></body></html>

注：目前支持A 股的日线复权，分钟复权稍后支持  

# 接口参数  

<html><body><table><tr><td>名称</td><td>类型</td><td>必选</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td>Y</td><td>证券代码</td></tr><tr><td>start_date</td><td>str</td><td>N</td><td>开始日期（格式：YYYYMMDD)</td></tr><tr><td>end_date</td><td>str</td><td>N</td><td>结束日期 (格式：YYYYMMDD)</td></tr><tr><td>asset</td><td>str</td><td>Y</td><td>资产类别：E股票「沪深指数C 数字货币FT期货FD 基金O期</td></tr><tr><td>adj</td><td>str</td><td>N</td><td>复权类型(只针对股票)：None 未复权 qfq 前复权 hfq 后复权，默</td></tr><tr><td>freq</td><td>str</td><td>Y</td><td>数据频度：1MIN表示1分钟（1/5/15/30/60分钟）D日线，黑</td></tr><tr><td>ma</td><td>list</td><td>N</td><td>均线，支持任意周期的均价和均量，输入任意合理int数值</td></tr></table></body></html>  

# 接口用例  

日线复权  

#取000001 的前复权行情   
df $=$ ts.pro_bar(ts_code $^{1=}$ '000001.SZ', adj $=$ 'qfq', start_date $^{1=}$ '201   
80101', end_date $=$ '20181011')   
#取000001 的后复权行情   
df $=$ ts.pro_bar(ts_code $^{1=}$ '000001.SZ', adj $=$ 'hfq', start_date $=$ '201   
80101', end_date $=$ '20181011')  

周线复权  

#取000001 的周线前复权行情  

df $=$ ts.pro_bar( ts_code='000001.SZ', freq='W', adj $=$ 'qfq', star t_date $=$ '20180101', end_date $=$ '20181011')  

#取000001 的周线后复权行情   
df $=$ ts.pro_bar(ts_code $=$ '000001.SZ', freq $=$ 'W', adj $=$ 'hfq', start   
_date='20180101', end_date $=$ '20181011')  

# 月线复权  

#取000001 的月线前复权行情   
df $=$ ts.pro_bar(ts_code $^{1=}$ '000001.SZ', freq $=$ 'M', adj $=$ 'qfq', start   
_date $=$ '20180101', end_date $=$ '20181011')   
#取000001 的月线后复权行情   
df $=$ ts.pro_bar(ts_code $^{1=}$ '000001.SZ', freq $=$ 'M', adj $=$ 'hfq', start   
_date $=$ '20180101', end_date $=$ '20181011')  

# 复权因子  

接口：adj_factor，可以通过数据工具调试和查看数据。  

更新时间：早上9 点30 分  

描述：获取股票复权因子，可提取单只股票全部历史复权因子，也可以提取单日全部股票的复权因子。  

积分要求：2000 积分起，5000 以上可高频调取  

# 输入参数  

<html><body><table><tr><td>名称</td><td>类型</td><td>必选</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td>N</td><td>股票代码</td></tr><tr><td>trade_date</td><td>str</td><td>N</td><td>交易日期(YYYYMMDD，下同)</td></tr><tr><td>start_date</td><td>str</td><td>N</td><td>开始日期</td></tr><tr><td>end_date</td><td>str</td><td>N</td><td>结束日期</td></tr></table></body></html>

注：日期都填YYYYMMDD 格式，比如20181010  

输出参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td>股票代码</td></tr><tr><td>trade_date</td><td>str</td><td>交易日期</td></tr><tr><td>adj_factor</td><td>float</td><td>复权因子</td></tr></table></body></html>  

# 接口示例  

pro $=$ ts.pro_api()  

#提取000001 全部复权因子df $=$ pro.adj_factor(ts_code $=$ '000001.SZ', trade_date $=$ '')  

#提取2018 年7 月18 日复权因子df $=$ pro.adj_factor(ts_code $=$ '', trade_date $:=$ '20180718')  

或者  

df $=$ pro.query('adj_factor',  trade_date $=$ '20180718')  

# 数据样例  

<html><body><table><tr><td></td><td>ts_code trade_date</td><td>adj_factor</td></tr><tr><td></td><td>000001.SZ 20180809</td><td>108.031</td></tr><tr><td>1</td><td>000001.SZ 20180808</td><td>108.031</td></tr><tr><td>2</td><td>000001.SZ 20180807</td><td>108.031</td></tr><tr><td>3</td><td>000001.SZ 20180806</td><td>108.031</td></tr><tr><td>4</td><td>000001.SZ 20180803</td><td>108.031</td></tr><tr><td>5</td><td>000001.SZ 20180802</td><td>108.031</td></tr><tr><td>6</td><td>000001.SZ 20180801</td><td>108.031</td></tr><tr><td>7</td><td>000001.SZ 20180731</td><td>108.031</td></tr><tr><td>8</td><td>000001.SZ 20180730</td><td>108.031</td></tr><tr><td>9</td><td>000001.SZ 20180727</td><td>108.031</td></tr><tr><td>10</td><td>000001.SZ 20180726</td><td>108.031</td></tr><tr><td>11</td><td>000001.SZ 20180725</td><td>108.031</td></tr><tr><td>12</td><td>000001.SZ 20180724</td><td>108.031</td></tr><tr><td>13</td><td>000001.SZ 20180723</td><td>108.031</td></tr><tr><td>14</td><td>000001.SZ 20180720</td><td>108.031</td></tr><tr><td>15</td><td>000001.SZ 20180719</td><td>108.031</td></tr><tr><td>16</td><td>000001.SZ 20180718</td><td>108.031</td></tr><tr><td>17</td><td>000001.SZ 20180717</td><td>108.031</td></tr><tr><td>18</td><td>000001.SZ</td><td>20180716 108.031</td></tr><tr><td>19</td><td>000001.SZ</td><td>20180713 108.031</td></tr><tr><td>20</td><td>000001.SZ</td><td>20180712 108.031</td></tr></table></body></html>  

# 每日指标  

接口：daily_basic，可以通过数据工具调试和查看数据。  

更新时间：交易日每日15 点～17 点之间  

描述：获取全部股票每日重要的基本面指标，可用于选股分析、报表展  

积分：至少2000 积分才可以调取，5000 积分无总量限制，具体请参阅  

# 积分获取办法  

输入参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>必选</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td></td><td>股票代码 （二选一)</td></tr><tr><td>trade_date</td><td>str</td><td>N</td><td>交易日期 （二选一）</td></tr><tr><td>start_date</td><td>str</td><td>N</td><td>开始日期(YYYYMMDD)</td></tr><tr><td>end_date</td><td>str</td><td>N</td><td>结束日期(YYYYMMDD)</td></tr></table></body></html>  

# 注：日期都填YYYYMMDD 格式，比如20181010  

输出参数  

<html><body><table><tr><td>名称</td><td>类型</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td>TS股票代码</td></tr><tr><td>trade_date</td><td>str</td><td>交易日期</td></tr><tr><td>close</td><td>float</td><td>当日收盘价</td></tr><tr><td>turnover_rate</td><td>float</td><td>换手率(%)</td></tr><tr><td>turnover_rate_f</td><td>float</td><td>换手率 (自由流通股)</td></tr><tr><td>volume_ratio</td><td>float</td><td>量比</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>描述</td></tr><tr><td>pe</td><td>float</td><td>市盈率（总市值/净利润，亏损的PE为空)</td></tr><tr><td>pe_ttm</td><td>float</td><td>市盈率（TTM，亏损的PE为空)</td></tr><tr><td>pb</td><td>float</td><td>市净率 (总市值/净资产)</td></tr><tr><td>ps</td><td>float</td><td>市销率</td></tr><tr><td>w-sd</td><td>float</td><td>市销率 (TTM)</td></tr><tr><td>dv_ratio</td><td>float</td><td>股息率 (%)</td></tr><tr><td>dv_ttm</td><td>float</td><td>股息率（TTM） (%)</td></tr><tr><td>total_share</td><td>float</td><td>总股本 （万股）</td></tr><tr><td>float_share</td><td>float</td><td>流通股本 （万股)</td></tr><tr><td>free_share</td><td>float</td><td>自由流通股本 （万）</td></tr><tr><td>total_mv</td><td>float</td><td>总市值 （万元)</td></tr><tr><td>circ_mv</td><td>float</td><td>流通市值 (万元)</td></tr></table></body></html>  

# 接口用法  

pro $=$ ts.pro_api()  

df $=$ pro.daily_basic(ts_code $=$ '', trade_date $=$ '20180726', fields $=$ 'ts_code,trade_date,turnover_rate,volume_ratio,pe,pb')  

或者  

df $=$ pro.query('daily_basic', ts_code $=$ '', trade_date $=$ '20180726 ',fields $=$ 'ts_code,trade_date,turnover_rate,volume_ratio,pe,pb  

# 数据样例  

ts_code trade_date turnover_rate volume_ratio e pb  

0 600230.SH 20180726 2.4584 0.72 8.69283.7203  
1 600237.SH 20180726 1.4737 0.88 166.40011.8868  
2 002465.SZ 20180726 0.7489 0.72 71.89432.6391  
3 300732.SZ 20180726 6.7083 0.77 21.81013.2513  
4 600007.SH 20180726 0.0381 0.61 23.76962.3774  
5 300068.SZ 20180726 1.4583 0.52 27.81661.7549  
6 300552.SZ 20180726 2.0728 0.95 56.80042.9279  
7 601369.SH 20180726 0.2088 0.95 44.11631.8001  
8 002518.SZ 20180726 0.5814 0.76 15.10042.5626  
9 002913.SZ 20180726 12.1096 1.03 33.12792.9217  
10 601818.SH 20180726 0.1893 0.86 6.30640.7209  
11 600926.SH 20180726 0.6065 0.46 9.17720.9808  
12 002166.SZ 20180726 0.7582 0.82 16.98683.3452  
13 600841.SH 20180726 0.3754 1.02 66.26472.2302  
14 300634.SZ 20180726 23.1127 1.26 120.305314.3168  
15 300126.SZ 20180726 1.2304 1.11 348.43061.5171  
16 300718.SZ 20180726 17.6612 0.92 32.02393.8661  
17 000708.SZ 20180726 0.5575 0.70 10.36741.0276  
18 002626.SZ 20180726 0.6187 0.83 22.75804.2446  
19 600816.SH 20180726 0.6745 0.65 11.07783.2214  

# 通用行情接口  

接口名称：pro_bar，可以通过数据工具调试和查看数据。  

更新时间：股票和指数通常在15 点～17 点之间，数字货币实时更新，具体请参考各接口文档明细。  

描述：目前整合了股票（未复权、前复权、后复权）、指数、数字货币、ETF 基金、期货、期权的行情数据，未来还将整合包括外汇在内的所有交易行情数据，同时提供分钟数据。不同数据对应不同的积分要求，具体请参阅每类数据的文档说明。  

其它：由于本接口是集成接口，在SDK 层做了一些逻辑处理，目前暂时没法用http 的方式调取通用行情接口。用户可以访问Tushare 的Github，查看源代码完成类似功能。  

输入参数  

<html><body><table><tr><td>名称</td><td>类 型</td><td>必</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td>Y</td><td>证券代码，不支持多值输入，多值输入获取结果会有重复记录</td></tr><tr><td>start_date</td><td>str</td><td>N</td><td>开始日期（日线格式：YYYYMMDD，提取分钟数据请用2019-09-0109:0</td></tr><tr><td>end_date</td><td>str</td><td>N</td><td>结束日期（日线格式：YYYYMMDD)</td></tr><tr><td>asset</td><td>str</td><td>V</td><td>资产类别：E股票I沪深指数C数字货币FT期货FD基金O期权CB 默认E</td></tr><tr><td>adj</td><td>str</td><td>N</td><td>复权类型(只针对股票)：None未复权qfq 前复权hfq 后复权，默认 Non 复权，同时复权机制是根据设定的end_date参数动态复权，采用分红再 常见问题列表里的说明，如果获取跟行情软件一致的复权行情，可以参阅</td></tr><tr><td>freq</td><td>str</td><td>Y</td><td>数据频度 ：支持分钟(min)/日(D)/周(W)/月(M)K线，其中 1min表示1分 1/5/15/30/60分钟），默认D。对于分钟数据有600积分用户可以试用 权限可以参考权限列表说明，使用方法请参考股票分钟使用方法。</td></tr><tr><td>ma</td><td>list</td><td>N</td><td>均线，支持任意合理int数值。注：均线是动态计算，要设置一定时间范 线，比如5日均线，开始和结束日期参数跨度必须要超过5日。目前只支 均线，即需要输入ts_code 参数。é.g:ma_5 表示5日均价，ma_v_5表示</td></tr><tr><td>factors</td><td>list</td><td>N</td><td>股票因子（asset='E'有效）支持tor换手率vr量比</td></tr><tr><td>adjfactor</td><td>str</td><td>N</td><td>复权因子，在复权数据时，如果此参数为True，返回的数据中则带复权因 该功能从1.2.33版本开始生效</td></tr></table></body></html>  

# 输出指标  

具体输出的数据指标可参考各行情具体指标：  

股票Daily：https://tushare.pro/document/2?doc_id=27  

基金Daily：https://tushare.pro/document/2?doc_id=127  

期货Daily：https://tushare.pro/document/2?doc_id=138  

期权Daily：https://tushare.pro/document/2?doc_id=159  

指数Daily：https://tushare.pro/document/2?doc_id=95  

# 接口用例  

#取000001 的前复权行情   
df $=$ ts.pro_bar(ts_code $^{1=}$ '000001.SZ', adj $=$ 'qfq', start_date $=$ '201   
80101', end_date $=$ '20181011')  

ts_code trade_date open high low clo se trade_date 20181011 000001.SZ 20181011 1085.71 1097.59 1047.90 106 5.19 20181010 000001.SZ 20181010 1138.65 1151.61 1121.36 112 8.92 20181009 000001.SZ 20181009 1130.00 1155.93 1122.44 114 0.81 20181008 000001.SZ 20181008 1155.93 1165.65 1128.92 112 8.92 20180928 000001.SZ 20180928  1164.57  1217.51 1164.57 119 3.74  

#取上证指数行情数据  

df $=$ ts.pro_bar(ts_code $^{1=}$ '000001.SH', asset $=$ 'I', start_date $=$ '201 80101', end_date $=$ '20181011')  

In [10]: df.head() Out[10]:  

code trade_date close open high lo   
w \   
0 000001.SH 20181011 2583.4575 2643.0740 2661.2859 2560.3   
164   
1 000001.SH 20181010 2725.8367 2723.7242 2743.5480 2703.0   
626   
2 000001.SH 20181009 2721.0130 2713.7319 2734.3142 2711.1   
971   
3 000001.SH 20181008 2716.5104  2768.2075 2771.9384 2710.1   
781   
4 000001.SH 20180928  2821.3501  2794.2644  2821.7553 2791.8   
363   
pre_close change pct_chg vol amount   
0 2725.8367 -142.3792 -5.2233 197150702.0 170057762.5   
1 2721.0130 4.8237 0.1773 113485736.0 111312455.3   
2 2716.5104 4.5026 0.1657 116771899.0 110292457.8   
3 2821.3501 -104.8397 -3.7159 149501388.0 141531551.8   
4 2791.7748 29.5753 1.0594 134290456.0 125369989.4  

# #均线  

df $=$ ts.pro_bar(ts_code $=$ '000001.SZ', start_date='20180101', end _date $=$ '20181011', ma=[5, 20, 50])  

注：Tushare pro_bar 接口的均价和均量数据是动态计算，想要获取某个时间段的均线，必须要设置start_date 日期大于最大均线的日期数，然后自行截取想要日期段。例如，想要获取20190801 开始的3 日均线，  

必须设置start_date='20190729'，然后剔除20190801 之前的日期记录。  

#换手率tor，量比vr  

df $=$ ts.pro_bar(ts_code $=$ '000001.SZ', start_date $=$ '20180101', end _date $=$ '20181011', factors $=$ ['tor', 'vr'])  

# 说明  

对于pro_api 参数，如果在一开始就通过 ts.set_token('xxxx') 设置过token 的情况，这个参数就不是必需的。  

例如：  

df $=$ ts.pro_bar(ts_code $=$ '000001.SH', asset='I', start_date $=$ '201 80101', end_date $=$ '20181011')  

# 每日涨跌停价格  

接口：stk_limit  

描述：获取全市场（包含A/B 股和基金）每日涨跌停价格，包括涨停价格，跌停价格等，每个交易日8 点40 左右更新当日股票涨跌停价格。限量：单次最多提取5800 条记录，可循环调取，总量不限制积分：用户积2000 积分可调取，单位分钟有流控，积分越高流量越大，请自行提高积分，具体请参阅积分获取办法  

输入参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>必选</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td>N</td><td>股票代码</td></tr><tr><td>trade_date</td><td>str</td><td>N</td><td>交易日期</td></tr><tr><td>start_date</td><td>str</td><td>N</td><td>开始日期</td></tr><tr><td>end_date</td><td>str</td><td>N</td><td>结束日期</td></tr></table></body></html>  

输出参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>trade_date</td><td>str</td><td></td><td>交易日期</td></tr><tr><td>ts_code</td><td>str</td><td></td><td>TS股票代码</td></tr><tr><td>pre_close</td><td>float</td><td>N</td><td>昨日收盘价</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>up_limit</td><td>float</td><td>Y</td><td>涨停价</td></tr><tr><td>down_limit</td><td>float</td><td>V</td><td>跌停价</td></tr></table></body></html>  

# 接口示例  

pro $=$ ts.pro_api()  

#获取单日全部股票数据涨跌停价格 df $=$ pro.stk_limit(trade_date $^{1=}$ '20190625')  

#获取单个股票数据   
df $=$ pro.stk_limit(ts_code $=$ '002149.SZ', start_date $=$ '20190115',   
end_date $=$ '20190615')  

# 数据示例  

trade_date ts_code up_limit down_limit   
0 20190625 000001.SZ 15.06 12.32   
1 20190625 000002.SZ 30.94 25.32   
2 20190625 000004.SZ 25.15 20.57   
3 20190625 000005.SZ 3.49 2.85   
4 20190625 000006.SZ 6.14 5.02   
5 20190625 000007.SZ 7.74 6.34   
6 20190625 000008.SZ 4.28 3.50   
7 20190625 000009.SZ 6.36 5.20   
8 20190625 000010.SZ 3.51 3.17   
9 20190625 000011.SZ 10.58 8.66   
10 20190625 000012.SZ 5.16 4.22   
11 20190625 000014.SZ 10.98 8.98   
12 20190625 000016.SZ 4.81 3.93   
13 20190625 000017.SZ 5.15 4.21   
14 20190625 000018.SZ 1.44 1.30   
15 20190625 000019.SZ 8.09 6.62   
16 20190625 000020.SZ 12.21 9.99   
17 20190625 000021.SZ 9.30 7.61   
18 20190625 000023.SZ 14.61 11.95   
19 20190625 000025.SZ 23.08 18.88   
20 20190625 000026.SZ 8.66 7.08  

# 每日停复牌信息  

接口：suspend_d  

更新时间：不定期  

描述：按日期方式获取股票每日停复牌信息  

输入参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>必选</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td>N</td><td>股票代码(可输入多值)</td></tr><tr><td>trade_date</td><td>str</td><td>N</td><td>交易日日期</td></tr><tr><td>start_date</td><td>str</td><td>N</td><td>停复牌查询开始日期</td></tr><tr><td>end_date</td><td>str</td><td>N</td><td>停复牌查询结束日期</td></tr><tr><td>suspend_type</td><td>str</td><td>N</td><td>停复牌类型：S-停牌,R-复牌</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td></td><td>TS代码</td></tr><tr><td>trade_date</td><td>str</td><td></td><td>停复牌日期</td></tr><tr><td>suspend_timing</td><td>str</td><td></td><td>日内停牌时间段</td></tr><tr><td>suspend_type</td><td>str</td><td></td><td>停复牌类型：S-停牌，R-复牌</td></tr></table></body></html>  

# 接口用法  

pro $=$ ts.pro_api()  

#提取2020-03-12 的停牌股票df $=$ pro.suspend_d(suspend_type $=$ 'S', trade_date $=$ '20200312')  

# 数据样例  

ts_code suspend_type trade_date suspend_timing   
0 000029.SZ S 20200312 None   
1 000502.SZ S 20200312 None   
2 000939.SZ S 20200312 None   
3 000977.SZ S 20200312 None   
4 000995.SZ S 20200312 None   
5 002260.SZ S 20200312 None   
6 002450.SZ S 20200312 None   
7 002604.SZ S 20200312 None   
8 300028.SZ S 20200312 None   
9 300104.SZ S 20200312 None   
10 300216.SZ S 20200312 None   
11 300592.SZ S 20200312 None   
12 300819.SZ S 20200312 09:30-10:00   
13 300821.SZ S 20200312 09:30-10:00   
14 600074.SH S 20200312 None   
15 600145.SH S 20200312 None   
16 600228.SH S 20200312 None   
17 600310.SH S 20200312 None   
18 600610.SH S 20200312 None   
19 600745.SH S 20200312 None   
20 600766.SH S 20200312 None   
21 600891.SH S 20200312 None   
22 601127.SH S 20200312 None   
23 601162.SH S 20200312 None   
24 603002.SH S 20200312 None   
25 603399.SH S 20200312 None  

# 备用行情  

接口：bak_daily  

描述：获取备用行情，包括特定的行情指标(数据从2017 年中左右开  

始，早期有几天数据缺失，近期正常)  

限量：单次最大7000 行数据，可以根据日期参数循环获取，正式权限需  

要5000 积分。  

输入参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>必选</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td>N</td><td>股票代码</td></tr><tr><td>trade_date</td><td>str</td><td>N</td><td>交易日期</td></tr><tr><td>start_date</td><td>str</td><td>N</td><td>开始日期</td></tr><tr><td>end_date</td><td>str</td><td>N</td><td>结束日期</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>必选</td><td>描述</td></tr><tr><td>offset</td><td>str</td><td>N</td><td>开始行数</td></tr><tr><td>limit</td><td>str</td><td>N</td><td>最大行数</td></tr></table></body></html>  

输出参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td>V</td><td>股票代码</td></tr><tr><td>trade_date</td><td>str</td><td>Y</td><td>交易日期</td></tr><tr><td>name</td><td>str</td><td>Y</td><td>股票名称</td></tr><tr><td>pct_change</td><td>float</td><td>Y</td><td>涨跌幅</td></tr><tr><td>close</td><td>float</td><td>Y</td><td>收盘价</td></tr><tr><td>change</td><td>float</td><td>Y</td><td>涨跌额</td></tr><tr><td>open</td><td>float</td><td>Y</td><td>开盘价</td></tr><tr><td>high</td><td>float</td><td>Y</td><td>最高价</td></tr><tr><td>low</td><td>float</td><td>Y</td><td>最低价</td></tr><tr><td>pre_close</td><td>float</td><td>Y</td><td>昨收价</td></tr><tr><td>vol_ratio</td><td>float</td><td>Y</td><td>量比</td></tr><tr><td>turn_over</td><td>float</td><td></td><td>换手率</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>swing</td><td>float Y</td><td></td><td>振幅</td></tr><tr><td>vol</td><td>float Y</td><td></td><td>成交量</td></tr><tr><td>amount</td><td>float Y</td><td></td><td>成交额</td></tr><tr><td>selling</td><td>float Y</td><td></td><td>内盘 (主动卖，手)</td></tr><tr><td>buying</td><td>float Y</td><td></td><td>外盘 (主动买，手)</td></tr><tr><td>total_share</td><td>float Y</td><td></td><td>总股本(亿)</td></tr><tr><td>float_share</td><td>float Y</td><td></td><td>流通股本(亿)</td></tr><tr><td>pe</td><td>float Y</td><td></td><td>市盈(动)</td></tr><tr><td>industry</td><td>str Y</td><td></td><td>所属行业</td></tr><tr><td>area</td><td>str Y</td><td></td><td>所属地域</td></tr><tr><td>float_mv</td><td>float Y</td><td></td><td>流通市值</td></tr><tr><td>total_mv</td><td>float Y</td><td></td><td>总市值</td></tr><tr><td>avg_price</td><td>float Y</td><td></td><td>平均价</td></tr><tr><td>strength</td><td>float</td><td></td><td>强弱度(%)</td></tr><tr><td>activity</td><td>float Y</td><td></td><td>活跃度(%)</td></tr><tr><td>avg_turnover</td><td>float</td><td></td><td>笔换手</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>attack</td><td>float</td><td></td><td>攻击波(%)</td></tr><tr><td>interval_3</td><td>float</td><td></td><td>近3月涨幅</td></tr><tr><td>interval_6</td><td>float</td><td></td><td>近6月涨幅</td></tr></table></body></html>  

# 接口示例  

pro $=$ ts.pro_api()  

df $=$ pro.bak_daily(trade_date $^{1=}$ '20211012', fields $=$ 'trade_date,ts _code,name,close,open')  

# 数据样例  

ts_code trade_date name close open   
0 300605.SZ 20211012 恒锋信息 14.86 12.65   
1 301017.SZ 20211012 漱玉平民 25.21 20.82   
2 300755.SZ 20211012 华致酒行 40.45 37.01   
3 300255.SZ 20211012 常山药业 8.39 7.26   
4 688378.SH 20211012 奥来德 68.62 67.00   
4529 688257.SH 20211012 新锐股份 0.00 0.00   
4530 688255.SH 20211012 凯尔达 0.00 0.00   
4531 688211.SH 20211012 中科微至 0.00 0.00   
4532 605567.SH 20211012 春雪食品 0.00 0.00   
4533 605566.SH 20211012 福莱蒽特 0.00 0.00  

# 利润表  

接口：income，可以通过数据工具调试和查看数据。  

描述：获取上市公司财务利润表数据  

积分：用户需要至少2000 积分才可以调取，具体请参阅积分获取办法  

提示：当前接口只能按单只股票获取其历史数据，如果需要获取某一季度全部上市公司数据，请使用income_vip 接口（参数一致），需积攒5000 积分。  

# 输入参数  

<html><body><table><tr><td>名称</td><td>类 型</td><td>必 选</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td>Y</td><td>股票代码</td></tr><tr><td>ann_date</td><td>str</td><td>N</td><td>公告日期（YYYYMMDD格式，下同）</td></tr><tr><td>f_ann_date</td><td>str</td><td>N</td><td>实际公告日期</td></tr><tr><td>start_date</td><td>str</td><td>N</td><td>公告开始日期</td></tr><tr><td>end_date</td><td>str</td><td>N</td><td>公告结束日期</td></tr><tr><td>period</td><td>str</td><td>N</td><td>报告期(每个季度最后一天的日期，比如20171231表示年报，20170 20170930三季报)</td></tr><tr><td>report_type</td><td>str</td><td>N</td><td>报告类型，参考文档最下方说明</td></tr><tr><td>comp_type</td><td>str</td><td>N</td><td>公司类型（1一般工商业2银行3保险4证券)</td></tr></table></body></html>  

输出参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td>Y</td><td>TS代码</td></tr><tr><td>ann_date</td><td>str</td><td>Y</td><td>公告日期</td></tr><tr><td>f_ann_date</td><td>str</td><td>Y</td><td>实际公告日期</td></tr><tr><td>end_date</td><td>str</td><td>Y</td><td>报告期</td></tr><tr><td>report_type</td><td>str</td><td>Y</td><td>报告类型见底部表</td></tr><tr><td>comp_type</td><td>str</td><td>Y</td><td>公司类型(1一般工商业 2 银行 3保</td></tr><tr><td>end_type</td><td>str</td><td>Y</td><td>报告期类型</td></tr><tr><td>basic_eps</td><td>float</td><td>Y</td><td>基本每股收益</td></tr><tr><td>diluted_eps</td><td>float</td><td>Y</td><td>稀释每股收益</td></tr><tr><td>total_revenue</td><td>float</td><td>Y</td><td>营业总收入</td></tr><tr><td>revenue</td><td>float</td><td>Y</td><td>营业收入</td></tr><tr><td>int_income</td><td>float</td><td>Y</td><td>利息收入</td></tr><tr><td>prem_earned</td><td>float</td><td>Y</td><td>已赚保费</td></tr><tr><td>comm_income</td><td>float</td><td>Y</td><td>手续费及佣金收入</td></tr><tr><td>n_commis_income</td><td>float</td><td>Y</td><td>手续费及佣金净收入</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>n_oth_income</td><td>float</td><td>Y</td><td>其他经营净收益</td></tr><tr><td>n_oth_b_income</td><td>float</td><td>Y</td><td>加:其他业务净收益</td></tr><tr><td>prem_income</td><td>float</td><td>Y</td><td>保险业务收入</td></tr><tr><td>out_prem</td><td>float</td><td>Y</td><td>减:分出保费</td></tr><tr><td>une_prem_reser</td><td>float</td><td>Y</td><td>提取未到期责任准备金</td></tr><tr><td>reins_income</td><td>float</td><td>V</td><td>其中:分保费收入</td></tr><tr><td>n_sec_tb_income</td><td>float</td><td>Y</td><td>代理买卖证券业务净收入</td></tr><tr><td>n_sec_uw_income</td><td>float</td><td>Y</td><td>证券承销业务净收入</td></tr><tr><td>n_asset_mg_income</td><td>float</td><td>Y</td><td>受托客户资产管理业务净收入</td></tr><tr><td>oth_b_income</td><td>float</td><td>Y</td><td>其他业务收入</td></tr><tr><td>fv_value_chg-gain</td><td>float</td><td>Y</td><td>加:公允价值变动净收益</td></tr><tr><td>invest_income</td><td>float</td><td>Y</td><td>加:投资净收益</td></tr><tr><td>ass_invest_income</td><td>float</td><td>Y</td><td>其中:对联营企业和合营企业的投资</td></tr><tr><td>forex_gain</td><td>float</td><td>Y</td><td>加:汇兑净收益</td></tr><tr><td>total_cogs</td><td>float</td><td>V</td><td>营业总成本</td></tr><tr><td>oper_cost</td><td>float</td><td>V</td><td>减:营业成本</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>int_exp</td><td>float</td><td>Y</td><td>减:利息支出</td></tr><tr><td>comm_exp</td><td>float</td><td>Y</td><td>减:手续费及佣金支出</td></tr><tr><td>biz_tax_surchg</td><td>float</td><td>Y</td><td>减:营业税金及附加</td></tr><tr><td>sell_exp</td><td>float</td><td>Y</td><td>减:销售费用</td></tr><tr><td>admin_exp</td><td>float</td><td>Y</td><td>减:管理费用</td></tr><tr><td>fin_exp</td><td>float</td><td>Y</td><td>减:财务费用</td></tr><tr><td>assets_impair_loss</td><td>float</td><td>Y</td><td>减:资产减值损失</td></tr><tr><td>prem_refund</td><td>float</td><td>Y</td><td>退保金</td></tr><tr><td>compens_payout</td><td>float</td><td>Y</td><td>赔付总支出</td></tr><tr><td>reser_insur_liab</td><td>float</td><td>Y</td><td>提取保险责任准备金</td></tr><tr><td>div_payt</td><td>float</td><td>Y</td><td>保户红利支出</td></tr><tr><td>reins_exp</td><td>float</td><td>Y</td><td>分保费用</td></tr><tr><td>oper_exp</td><td>float</td><td>Y</td><td>营业支出</td></tr><tr><td>compens_payout_refu</td><td>float</td><td>Y</td><td>减:摊回赔付支出</td></tr><tr><td>insur_reser_refu</td><td>float</td><td>Y</td><td>减:摊回保险责任准备金</td></tr><tr><td>reins_cost_refund</td><td>float</td><td>Y</td><td>减:摊回分保费用</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>other_bus_cost</td><td>float</td><td>Y</td><td>其他业务成本</td></tr><tr><td>operate_profit</td><td>float</td><td>Y</td><td>营业利润</td></tr><tr><td>non_oper_income</td><td>float</td><td>Y</td><td>加:营业外收入</td></tr><tr><td>non_oper_exp</td><td>float</td><td>Y</td><td>减:营业外支出</td></tr><tr><td>nca_disploss</td><td>float</td><td>Y</td><td>其中:减:非流动资产处置净损失</td></tr><tr><td>total_profit</td><td>float</td><td>Y</td><td>利润总额</td></tr><tr><td>income_tax</td><td>float</td><td>Y</td><td>所得税费用</td></tr><tr><td>n_income</td><td>float</td><td>Y</td><td>净利润(含少数股东损益)</td></tr><tr><td>n_income_attr_p</td><td>float</td><td>Y</td><td>净利润(不含少数股东损益)</td></tr><tr><td>minority_gain</td><td>float</td><td>Y</td><td>少数股东损益</td></tr><tr><td>oth_compr_income</td><td>float</td><td>Y</td><td>其他综合收益</td></tr><tr><td>t_compr_income</td><td>float</td><td>Y</td><td>综合收益总额</td></tr><tr><td>compr_inc_attr_p</td><td>float</td><td>Y</td><td>归属于母公司(或股东)的综合收益总</td></tr><tr><td>compr_inc_attr_m_s</td><td>float</td><td>Y</td><td>归属于少数股东的综合收益总额</td></tr><tr><td>ebit</td><td>float</td><td>Y</td><td>息税前利润</td></tr><tr><td>ebitda</td><td>float</td><td>Y</td><td>息税折旧摊销前利润</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>insurance_exp</td><td>float</td><td>Y</td><td>保险业务支出</td></tr><tr><td>undist_profit</td><td>float</td><td>Y</td><td>年初未分配利润</td></tr><tr><td>distable_profit</td><td>float</td><td>Y</td><td>可分配利润</td></tr><tr><td>rd_exp</td><td>float</td><td>Y</td><td>研发费用</td></tr><tr><td>fin_exp_int_exp</td><td>float</td><td>Y</td><td>财务费用:利息费用</td></tr><tr><td>fin_exp_int_inc</td><td>float</td><td>Y</td><td>财务费用:利息收入</td></tr><tr><td>transfer_surplus_rese</td><td>float</td><td>Y</td><td>盈余公积转入</td></tr><tr><td>transfer_housing_imprest</td><td>float</td><td>Y</td><td>住房周转金转入</td></tr><tr><td>transfer_oth</td><td>float</td><td>Y</td><td>其他转入</td></tr><tr><td>adj_lossgain</td><td>float</td><td>Y</td><td>调整以前年度损益</td></tr><tr><td>withdra_legal_surplus</td><td>float</td><td>Y</td><td>提取法定盈余公积</td></tr><tr><td>withdra_legal_pubfund</td><td>float</td><td>Y</td><td>提取法定公益金</td></tr><tr><td>withdra_biz_devfund</td><td>float</td><td>Y</td><td>提取企业发展基金</td></tr><tr><td>withdra_rese_fund</td><td>float</td><td>Y</td><td>提取储备基金</td></tr><tr><td>withdra_oth_ersu</td><td>float</td><td>Y</td><td>提取任意盈余公积金</td></tr><tr><td>workers_welfare</td><td>float</td><td>Y</td><td>职工奖金福利</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>distr_profit_shrhder</td><td>float</td><td>Y</td><td>可供股东分配的利润</td></tr><tr><td>prfshare_payable_dvd</td><td>float</td><td>Y</td><td>应付优先股股利</td></tr><tr><td>comshare_payable_dvd</td><td>float</td><td>Y</td><td>应付普通股股利</td></tr><tr><td>capit_comstock_div</td><td>float</td><td>V</td><td>转作股本的普通股股利</td></tr><tr><td>net_after_nr_lp_correct</td><td>float</td><td>N</td><td>扣除非经常性损益后的净利润（更</td></tr><tr><td>credit_impa_loss</td><td>float</td><td>N</td><td>信用减值损失</td></tr><tr><td>net_expo_hedging_benefits</td><td>float</td><td>N</td><td>净口套期收益</td></tr><tr><td>oth_impair_loss_assets</td><td>float</td><td>N</td><td>其他资产减值损失</td></tr><tr><td>total_opcost</td><td>float</td><td>N</td><td>营业总成本 (二)</td></tr><tr><td>amodcost_fin_assets</td><td>float</td><td>N</td><td>以摊余成本计量的金融资产终止确</td></tr><tr><td>oth_income</td><td>float</td><td>N</td><td>其他收益</td></tr><tr><td>asset_disp_income</td><td>float</td><td>N</td><td>资产处置收益</td></tr><tr><td>continued_net_profit</td><td>float</td><td>N</td><td>持续经营净利润</td></tr><tr><td>end_net_profit</td><td>float</td><td>N</td><td>终止经营净利润</td></tr><tr><td>update_flag</td><td>str</td><td>V</td><td>更新标识</td></tr><tr><td></td><td></td><td></td><td></td></tr></table></body></html>  

pro $=$ ts.pro_api()  

df $=$ pro.income(ts_code $=$ '600000.SH', start_date $=$ '20180101', end _date $=$ '20180730', fields $=$ 'ts_code,ann_date,f_ann_date,end_date, report_type,comp_type,basic_eps,diluted_eps')  

获取某一季度全部股票数据  

df $=$ pro.income_vip(period $=$ '20181231',fields $=$ 'ts_code,ann_date, f_ann_date,end_date,report_type,comp_type,basic_eps,diluted_ep s')  

# 数据样例  

ts_code  ann_date f_ann_date end_date report_type comp_typ e basic_eps  diluted_eps  

0 600000.SH 20180428 20180428 20180331 1 2 0.46 0.46  

1 600000.SH 20180428 20180428 20180331 1 2 0.46 0.46  

2 600000.SH 20180428 20180428 20171231 1.84 1.84  

# 主要报表类型说明  

<html><body><table><tr><td>代码</td><td>类型</td><td>说明</td></tr><tr><td>1</td><td>合并报表</td><td>上市公司最新报表 （默认）</td></tr><tr><td>2</td><td>单季合并</td><td>单一季度的合并报表</td></tr><tr><td>3</td><td>调整单季合并表</td><td>调整后的单季合并报表（如果有）</td></tr><tr><td>4</td><td>调整合并报表</td><td>本年度公布上年同期的财务报表数据，报告期为上年度</td></tr></table></body></html>  

<html><body><table><tr><td>代码</td><td>类型</td><td>说明</td></tr><tr><td>5</td><td>调整前合并报表</td><td>数据发生变更，将原数据进行保留，即调整前的原数据</td></tr><tr><td>6</td><td>母公司报表</td><td>该公司母公司的财务报表数据</td></tr><tr><td>7</td><td>母公司单季表</td><td>母公司的单季度表</td></tr><tr><td>8</td><td>母公司调整单季 表</td><td>母公司调整后的单季表</td></tr><tr><td>9</td><td>母公司调整表</td><td>该公司母公司的本年度公布上年同期的财务报表数据</td></tr><tr><td>10</td><td>母公司调整前报 表</td><td>母公司调整之前的原始财务报表数据</td></tr><tr><td>11</td><td>母公司调整前合 并报表</td><td>母公司调整之前合并报表原数据</td></tr><tr><td>12</td><td>母公司调整前报 表</td><td>母公司报表发生变更前保留的原数据</td></tr></table></body></html>  

# 资产负债表  

接口：balancesheet，可以通过数据工具调试和查看数据。  

描述：获取上市公司资产负债表  

积分：用户需要至少2000 积分才可以调取，具体请参阅积分获取办法  

提示：当前接口只能按单只股票获取其历史数据，如果需要获取某一季度全部上市公司数据，请使用balancesheet_vip 接口（参数一致），需积攒5000 积分。  

输入参数  


<html><body><table><tr><td>名称</td><td>类 型</td><td>必 选</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td>Y</td><td>股票代码</td></tr><tr><td>ann_date</td><td>str</td><td>N</td><td>公告日期(YYYYMMDD格式，下同)</td></tr><tr><td>start_date</td><td>str</td><td>N</td><td>公告开始日期</td></tr><tr><td>end_date</td><td>str</td><td>N</td><td>公告结束日期</td></tr><tr><td>period</td><td>str</td><td>N</td><td>报告期(每个季度最后一天的日期，比如 20171231表示年报，20170 20170930三季报)</td></tr><tr><td>report_type</td><td>str</td><td>N</td><td>报告类型：见下方详细说明</td></tr><tr><td>comp_type</td><td>str</td><td>N</td><td>公司类型：1一般工商业 2银行3保险4证券</td></tr></table></body></html>  

# 输出参数  

<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td>Y</td><td>TS股票代码</td></tr><tr><td>ann_date</td><td>str</td><td>Y</td><td>公告日期</td></tr><tr><td>f_ann_date</td><td>str</td><td>Y</td><td>实际公告日期</td></tr><tr><td>end_date</td><td>str</td><td>Y</td><td>报告期</td></tr><tr><td>report_type</td><td>str</td><td>Y</td><td>报表类型</td></tr><tr><td>comp_type</td><td>str</td><td>Y</td><td>公司类型(1一般工商业 2 银行 3 保险 4 证</td></tr><tr><td>end_type</td><td>str</td><td>Y</td><td>报告期类型</td></tr><tr><td>total_share</td><td>float</td><td>Y</td><td>期末总股本</td></tr><tr><td>cap_rese</td><td>float</td><td>Y</td><td>资本公积金</td></tr><tr><td>undistr_porfit</td><td>float</td><td>Y</td><td>未分配利润</td></tr><tr><td>surplus_rese</td><td>float</td><td>Y</td><td>盈余公积金</td></tr><tr><td>special_rese</td><td>float</td><td>Y</td><td>专项储备</td></tr><tr><td>money_cap</td><td>float</td><td>Y</td><td>货币资金</td></tr><tr><td>trad_asset</td><td>float</td><td>Y</td><td>交易性金融资产</td></tr><tr><td>notes_receiv</td><td>float</td><td>Y</td><td>应收票据</td></tr><tr><td>accounts_receiv</td><td>float</td><td>Y</td><td>应收账款</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示 描述</td><td></td></tr><tr><td>oth_receiv</td><td>float Y</td><td></td><td>其他应收款</td></tr><tr><td>prepayment</td><td>float Y</td><td></td><td>预付款项</td></tr><tr><td>div_receiv</td><td>float Y</td><td></td><td>应收股利</td></tr><tr><td>int_receiv</td><td>float Y</td><td></td><td>应收利息</td></tr><tr><td>inventories</td><td>float Y</td><td></td><td>存货</td></tr><tr><td>amor_exp</td><td>float Y</td><td></td><td>待摊费用</td></tr><tr><td>nca_within_1y</td><td>float Y</td><td></td><td>一年内到期的非流动资产</td></tr><tr><td>sett_rsrv</td><td>float Y</td><td></td><td>结算备付金</td></tr><tr><td>loanto_oth_bank_fi</td><td>float Y</td><td></td><td>拆出资金</td></tr><tr><td>premium_receiv</td><td>float Y</td><td></td><td>应收保费</td></tr><tr><td>reinsur_receiv</td><td>float Y</td><td></td><td>应收分保账款</td></tr><tr><td>reinsur_res_receiv</td><td>float Y</td><td></td><td>应收分保合同准备金</td></tr><tr><td>pur_resale_fa</td><td>float Y</td><td></td><td>买入返售金融资产</td></tr><tr><td>oth_cur_assets</td><td>float Y</td><td></td><td>其他流动资产</td></tr><tr><td>total_cur_assets</td><td>float Y</td><td></td><td>流动资产合计</td></tr><tr><td>fa_avail_for_sale</td><td>float Y</td><td></td><td>可供出售金融资产</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>htm_invest</td><td>float</td><td>Y</td><td>持有至到期投资</td></tr><tr><td>It_eqt_invest</td><td>float</td><td>Y</td><td>长期股权投资</td></tr><tr><td>invest_real_estate</td><td>float</td><td>Y</td><td>投资性房地产</td></tr><tr><td>time_deposits</td><td>float Y</td><td></td><td>定期存款</td></tr><tr><td>oth_assets</td><td>float Y</td><td></td><td>其他资产</td></tr><tr><td>It_rec</td><td>float Y</td><td></td><td>长期应收款</td></tr><tr><td>fix_assets</td><td>float Y</td><td></td><td>固定资产</td></tr><tr><td>cip</td><td>float Y</td><td></td><td>在建工程</td></tr><tr><td>const_materials</td><td>float Y</td><td></td><td>工程物资</td></tr><tr><td>fixed_assets_disp</td><td>float Y</td><td></td><td>固定资产清理</td></tr><tr><td>produc_bio_assets</td><td>float Y</td><td></td><td>生产性生物资产</td></tr><tr><td>oil_and_gas_assets</td><td>float Y</td><td></td><td>油气资产</td></tr><tr><td>intan_assets</td><td>float Y</td><td></td><td>无形资产</td></tr><tr><td>r_and_d</td><td>float Y</td><td></td><td>研发支出</td></tr><tr><td>goodwill</td><td>float Y</td><td></td><td>商誉</td></tr><tr><td>It_amor_exp</td><td>float Y</td><td></td><td>长期待摊费用</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>defer_tax_assets</td><td>float</td><td>Y</td><td>递延所得税资产</td></tr><tr><td>decr_in_disbur</td><td>float</td><td>Y</td><td>发放贷款及垫款</td></tr><tr><td>oth_nca</td><td>float</td><td>Y</td><td>其他非流动资产</td></tr><tr><td>total_nca</td><td>float</td><td>Y</td><td>非流动资产合计</td></tr><tr><td>cash_reser_cb</td><td>float</td><td>Y</td><td>现金及存放中央银行款项</td></tr><tr><td>depos_in_oth_bfi</td><td>float</td><td>Y</td><td>存放同业和其它金融机构款项</td></tr><tr><td>prec_metals</td><td>float</td><td>Y</td><td>贵金属</td></tr><tr><td>deriv_assets</td><td>float</td><td>Y</td><td>衍生金融资产</td></tr><tr><td>rr_reins_une_prem</td><td>float</td><td>Y</td><td>应收分保未到期责任准备金</td></tr><tr><td>rr_reins_outstd_cla</td><td>float</td><td>Y</td><td>应收分保未决赔款准备金</td></tr><tr><td>rr_reins_lins_liab</td><td>float</td><td>Y</td><td>应收分保寿险责任准备金</td></tr><tr><td>rr_reins_Ithins_liab</td><td>float</td><td>Y</td><td>应收分保长期健康险责任准备金</td></tr><tr><td>refund_depos</td><td>float</td><td>Y</td><td>存出保证金</td></tr><tr><td>ph_pledge_loans</td><td>float</td><td>Y</td><td>保户质押贷款</td></tr><tr><td>refund_cap_depos</td><td>float</td><td>Y</td><td>存出资本保证金</td></tr><tr><td>indep_acct_assets</td><td>float</td><td>Y</td><td>独立账户资产</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>client_depos</td><td>float</td><td>Y</td><td>其中：客户资金存款</td></tr><tr><td>client_prov</td><td>float</td><td>Y</td><td>其中：客户备付金</td></tr><tr><td>transac_seat_fee</td><td>float</td><td>Y</td><td>其中:交易席位费</td></tr><tr><td>invest_as_receiv</td><td>float</td><td>Y</td><td>应收款项类投资</td></tr><tr><td>total_assets</td><td>float</td><td>Y</td><td>资产总计</td></tr><tr><td>It_borr</td><td>float</td><td>Y</td><td>长期借款</td></tr><tr><td>st_borr</td><td>float</td><td>Y</td><td>短期借款</td></tr><tr><td>cb_borr</td><td>float</td><td>Y</td><td>向中央银行借款</td></tr><tr><td>depos_ib_deposits</td><td>float</td><td>Y</td><td>吸收存款及同业存放</td></tr><tr><td>loan_oth_bank</td><td>float</td><td>Y</td><td>拆入资金</td></tr><tr><td>trading_fl</td><td>float</td><td>Y</td><td>交易性金融负债</td></tr><tr><td>notes_payable</td><td>float</td><td>Y</td><td>应付票据</td></tr><tr><td>acct_payable</td><td>float</td><td>Y</td><td>应付账款</td></tr><tr><td>adv_receipts</td><td>float</td><td>Y</td><td>预收款项</td></tr><tr><td>sold_for_repur_fa</td><td>float</td><td>Y</td><td>卖出回购金融资产款</td></tr><tr><td>comm_payable</td><td>float</td><td></td><td>应付手续费及佣金</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>payroll_payable</td><td>float</td><td>Y</td><td>应付职工薪酬</td></tr><tr><td>taxes_payable</td><td>float</td><td>Y</td><td>应交税费</td></tr><tr><td>int_payable</td><td>float</td><td>Y</td><td>应付利息</td></tr><tr><td>div_payable</td><td>float</td><td>Y</td><td>应付股利</td></tr><tr><td>oth_payable</td><td>float</td><td>Y</td><td>其他应付款</td></tr><tr><td>acc_exp</td><td>float</td><td>Y</td><td>预提费用</td></tr><tr><td>deferred_inc</td><td>float</td><td>Y</td><td>递延收益</td></tr><tr><td>st_bonds_payable</td><td>float</td><td>Y</td><td>应付短期债券</td></tr><tr><td>payable_to_reinsurer</td><td>float</td><td>Y</td><td>应付分保账款</td></tr><tr><td>rsrv_insur_cont</td><td>float</td><td>Y</td><td>保险合同准备金</td></tr><tr><td>acting_trading_sec</td><td>float</td><td>Y</td><td>代理买卖证券款</td></tr><tr><td>acting_uw_sec</td><td>float</td><td>Y</td><td>代理承销证券款</td></tr><tr><td>non_cur_liab_due_1y</td><td>float</td><td>Y</td><td>一年内到期的非流动负债</td></tr><tr><td>oth_cur_liab</td><td>float</td><td>Y</td><td>其他流动负债</td></tr><tr><td>total_cur_liab</td><td>float</td><td>Y</td><td>流动负债合计</td></tr><tr><td>bond_payable</td><td>float</td><td>Y</td><td>应付债券</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>It_payable</td><td>float</td><td>Y</td><td>长期应付款</td></tr><tr><td>specific_payables</td><td>float</td><td>Y</td><td>专项应付款</td></tr><tr><td>estimated_liab</td><td>float</td><td>Y</td><td>预计负债</td></tr><tr><td>defer_tax_liab</td><td>float</td><td>Y</td><td>递延所得税负债</td></tr><tr><td>defer_inc_non_cur_liab</td><td>float</td><td>Y</td><td>递延收益-非流动负债</td></tr><tr><td>oth_ncl</td><td>float</td><td>Y</td><td>其他非流动负债</td></tr><tr><td>total_ncl</td><td>float</td><td>Y</td><td>非流动负债合计</td></tr><tr><td>depos_oth_bfi</td><td>float</td><td>Y</td><td>同业和其它金融机构存放款项</td></tr><tr><td>deriv_liab</td><td>float</td><td>Y</td><td>衍生金融负债</td></tr><tr><td>depos</td><td>float</td><td>Y</td><td>吸收存款</td></tr><tr><td>agency_bus_liab</td><td>float</td><td>Y</td><td>代理业务负债</td></tr><tr><td>oth_liab</td><td>float</td><td>Y</td><td>其他负债</td></tr><tr><td>prem_receiv_adva</td><td>float</td><td>Y</td><td>预收保费</td></tr><tr><td>depos_received</td><td>float</td><td>Y</td><td>存入保证金</td></tr><tr><td>ph_invest</td><td>float</td><td>Y</td><td>保户储金及投资款</td></tr><tr><td>reser_une_prem</td><td>float</td><td>Y</td><td>未到期责任准备金</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>reser_outstd_claims</td><td>float</td><td>Y</td><td>未决赔款准备金</td></tr><tr><td>reser_lins_liab</td><td>float</td><td>Y</td><td>寿险责任准备金</td></tr><tr><td>reser_lthins_liab</td><td>float</td><td>Y</td><td>长期健康险责任准备金</td></tr><tr><td>indept_acc_liab</td><td>float</td><td>Y</td><td>独立账户负债</td></tr><tr><td>pledge_borr</td><td>float</td><td>Y</td><td>其中:质押借款</td></tr><tr><td>indem_payable</td><td>float</td><td>Y</td><td>应付赔付款</td></tr><tr><td>policy_div_payable</td><td>float</td><td>Y</td><td>应付保单红利</td></tr><tr><td>total_liab</td><td>float</td><td>Y</td><td>负债合计</td></tr><tr><td>treasury_share</td><td>float</td><td>Y</td><td>减:库存股</td></tr><tr><td>ordin_risk_reser</td><td>float</td><td>Y</td><td>一般风险准备</td></tr><tr><td>forex_differ</td><td>float</td><td>Y</td><td>外币报表折算差额</td></tr><tr><td>invest_loss_unconf</td><td>float</td><td>Y</td><td>未确认的投资损失</td></tr><tr><td>minority_int</td><td>float</td><td>Y</td><td>少数股东权益</td></tr><tr><td>total_hldr_eqy_exc_min_int</td><td>float</td><td>Y</td><td>股东权益合计(不含少数股东权益)</td></tr><tr><td>total_hldr_eqy_inc_min_int</td><td>float</td><td>Y</td><td>股东权益合计(含少数股东权益)</td></tr><tr><td>total_liab_hldr_eqy</td><td>float</td><td>Y</td><td>负债及股东权益总计</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>It_payroll_payable</td><td>float</td><td>Y</td><td>长期应付职工薪酬</td></tr><tr><td>oth_comp_income</td><td>float</td><td>Y</td><td>其他综合收益</td></tr><tr><td>oth_eqt_tools</td><td>float</td><td>Y</td><td>其他权益工具</td></tr><tr><td>oth_eqt_tools_p_shr</td><td>float</td><td>Y</td><td>其他权益工具(优先股)</td></tr><tr><td>lending_funds</td><td>float</td><td>Y</td><td>融出资金</td></tr><tr><td>acc_receivable</td><td>float</td><td>Y</td><td>应收款项</td></tr><tr><td>st_fin_payable</td><td>float</td><td>Y</td><td>应付短期融资款</td></tr><tr><td>payables</td><td>float</td><td>V</td><td>应付款项</td></tr><tr><td>hfs_assets</td><td>float</td><td>Y</td><td>持有待售的资产</td></tr><tr><td>hfs_sales</td><td>float</td><td>Y</td><td>持有待售的负债</td></tr><tr><td>cost_fin_assets</td><td>float</td><td>Y</td><td>以摊余成本计量的金融资产</td></tr><tr><td>fair_value_fin_assets</td><td>float</td><td>Y</td><td>以公允价值计量且其变动计入其他综合收</td></tr><tr><td>cip_total</td><td>float</td><td>Y</td><td>在建工程(合计)(元)</td></tr><tr><td>oth_pay_total</td><td>float</td><td>Y</td><td>其他应付款(合计)(元)</td></tr><tr><td>long-pay_total</td><td>float</td><td>Y</td><td>长期应付款(合计)(元)</td></tr><tr><td>debt_invest</td><td>float</td><td>Y</td><td>债权投资(元)</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>oth_debt_invest</td><td>float</td><td>Y</td><td>其他债权投资(元)</td></tr><tr><td>oth_eq_invest</td><td>float</td><td>N</td><td>其他权益工具投资(元)</td></tr><tr><td>oth_illiq_fin_assets</td><td>float</td><td>N</td><td>其他非流动金融资产(元)</td></tr><tr><td>oth_eq_ppbond</td><td>float</td><td>N</td><td>其他权益工具:永续债(元)</td></tr><tr><td>receiv_financing</td><td>float</td><td>N</td><td>应收款项融资</td></tr><tr><td>use_right_assets</td><td>float</td><td>N</td><td>使用权资产</td></tr><tr><td>lease_liab</td><td>float</td><td>N</td><td>租赁负债</td></tr><tr><td>contract_assets</td><td>float</td><td>Y</td><td>合同资产</td></tr><tr><td>contract_liab</td><td>float</td><td>Y</td><td>合同负债</td></tr><tr><td>accounts_receiv_bill</td><td>float</td><td>Y</td><td>应收票据及应收账款</td></tr><tr><td>accounts_pay</td><td>float</td><td>Y</td><td>应付票据及应付账款</td></tr><tr><td>oth_rcv_total</td><td>float</td><td>Y</td><td>其他应收款(合计） (元)</td></tr><tr><td>fix_assets_total</td><td>float</td><td>Y</td><td>固定资产(合计)(元)</td></tr><tr><td>update_flag</td><td>str</td><td>Y</td><td>更新标识</td></tr><tr><td>接口使用说明</td><td></td><td></td><td></td></tr></table></body></html>  

df $=$ pro.balancesheet(ts_code $^{1=}$ '600000.SH', start_date $=$ '20180101 ', end_date $=$ '20180730', fields $=$ 'ts_code,ann_date,f_ann_date,end _date,report_type,comp_type,cap_rese')  

获取某一季度全部股票数据  

$\mathsf{d}\mathsf{f}2\mathsf{\Omega}=\mathsf{\Omega}$ pro.balancesheet_vip(period $=$ '20181231',fields $=$ 'ts_code,an n_date,f_ann_date,end_date,report_type,comp_type,cap_rese')  

# 数据样例  

ts_code ann_date f_ann_date end_date report_type comp _type  

0 600000.SH 20180830 20180830 20180630 1 2  

1 600000.SH 20180428 20180428 20180331  

0 8.176000e+10   
1 8.176000e+10  

# 主要报表类型说明  

<html><body><table><tr><td>代码</td><td>类型</td><td>说明</td></tr><tr><td>1</td><td>合并报表</td><td>上市公司最新报表 (默认)</td></tr><tr><td>2</td><td>单季合并</td><td>单一季度的合并报表</td></tr><tr><td>3</td><td>调整单季合并表</td><td>调整后的单季合并报表（如果有）</td></tr><tr><td>4</td><td>调整合并报表</td><td>本年度公布上年同期的财务报表数据，报告期为上年度</td></tr><tr><td>5</td><td>调整前合并报表</td><td>数据发生变更，将原数据进行保留，即调整前的原数据</td></tr><tr><td>6</td><td>母公司报表</td><td>该公司母公司的财务报表数据</td></tr></table></body></html>  

<html><body><table><tr><td>代码</td><td>类型</td><td>说明</td></tr><tr><td>7</td><td>母公司单季表</td><td>母公司的单季度表</td></tr><tr><td>8</td><td>母公司调整单季表</td><td>母公司调整后的单季表</td></tr><tr><td>9</td><td>母公司调整表</td><td>该公司母公司的本年度公布上年同期的财务报表数据</td></tr><tr><td>10</td><td>母公司调整前报表</td><td>母公司调整之前的原始财务报表数据</td></tr><tr><td>11</td><td>母公司调整前合并报表</td><td>母公司调整之前合并报表原数据</td></tr><tr><td>12</td><td>母公司调整前报表</td><td>母公司报表发生变更前保留的原数据</td></tr></table></body></html>  

# 现金流量表  

接口：cashflow，可以通过数据工具调试和查看数据。描述：获取上市公司现金流量表积分：用户需要至少2000 积分才可以调取，具体请参阅积分获取办法  

提示：当前接口只能按单只股票获取其历史数据，如果需要获取某一季度全部上市公司数据，请使用cashflow_vip 接口（参数一致），需积攒5000 积分。  

# 输入参数  

<html><body><table><tr><td>名称</td><td>类 型</td><td>必 选</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td>Y</td><td>股票代码</td></tr><tr><td>ann_date</td><td>str</td><td>N</td><td>公告日期（YYYYMMDD格式，下同)</td></tr><tr><td>f_ann_date</td><td>str</td><td>N</td><td>实际公告日期</td></tr><tr><td>start_date</td><td>str</td><td>N</td><td>公告开始日期</td></tr><tr><td>end_date</td><td>str</td><td>N</td><td>公告结束日期</td></tr><tr><td>period</td><td>str</td><td>N</td><td>报告期(每个季度最后一天的日期，比如20171231表示年报，201706 20170930三季报)</td></tr><tr><td>report_type</td><td>str</td><td>N</td><td>报告类型：见下方详细说明</td></tr><tr><td>comp_type</td><td>str</td><td>N</td><td>公司类型：1一般工商业 2 银行 3 保险4证券</td></tr><tr><td>is_calc</td><td>int</td><td>N</td><td>是否计算报表</td></tr></table></body></html>  

输出参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td></td><td>TS股票代码</td></tr><tr><td>ann_date</td><td>str</td><td></td><td>公告日期</td></tr><tr><td>f_ann_date</td><td>str</td><td></td><td>实际公告日期</td></tr><tr><td>end_date</td><td>str</td><td></td><td>报告期</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>comp_type</td><td>str</td><td>Y</td><td>公司类型(1一般工商业 2 银行 3 保险 4</td></tr><tr><td>report_type</td><td>str</td><td>Y</td><td>报表类型</td></tr><tr><td>end_type</td><td>str</td><td>Y</td><td>报告期类型</td></tr><tr><td>net_profit</td><td>float</td><td>Y</td><td>净利润</td></tr><tr><td>finan_exp</td><td>float</td><td>Y</td><td>财务费用</td></tr><tr><td>c_fr_sale_sg</td><td>float</td><td>Y</td><td>销售商品、提供劳务收到的现金</td></tr><tr><td>recp_tax_rends</td><td>float</td><td>Y</td><td>收到的税费返还</td></tr><tr><td>n_depos_incr_fi</td><td>float</td><td>Y</td><td>客户存款和同业存放款项净增加额</td></tr><tr><td>n_incr_loans_cb</td><td>float</td><td>Y</td><td>向中央银行借款净增加额</td></tr><tr><td>n_inc_borr_oth_fi</td><td>float</td><td>Y</td><td>向其他金融机构拆入资金净增加额</td></tr><tr><td>prem_fr_orig_contr</td><td>float</td><td>Y</td><td>收到原保险合同保费取得的现金</td></tr><tr><td>n_incr_insured_dep</td><td>float</td><td>Y</td><td>保户储金净增加额</td></tr><tr><td>n_reinsur_prem</td><td>float</td><td>Y</td><td>收到再保业务现金净额</td></tr><tr><td>n_incr_disp_tfa</td><td>float</td><td>Y</td><td>处置交易性金融资产净增加额</td></tr><tr><td>ifc_cash_incr</td><td>float</td><td>Y</td><td>收取利息和手续费净增加额</td></tr><tr><td>n_incr_disp_faas</td><td>float</td><td>Y</td><td>处置可供出售金融资产净增加额</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>n_incr_loans_oth_bank</td><td>float</td><td>Y</td><td>拆入资金净增加额</td></tr><tr><td>n_cap_incr_repur</td><td>float</td><td>Y</td><td>回购业务资金净增加额</td></tr><tr><td>c_fr_oth_operate_a</td><td>float</td><td>Y</td><td>收到其他与经营活动有关的现金</td></tr><tr><td>c_inf_fr_operate_a</td><td>float</td><td>Y</td><td>经营活动现金流入小计</td></tr><tr><td>c_paid_goods_s</td><td>float</td><td>Y</td><td>购买商品、接受劳务支付的现金</td></tr><tr><td>c_paid_to_for_empl</td><td>float</td><td>Y</td><td>支付给职工以及为职工支付的现金</td></tr><tr><td>c_paid_for_taxes</td><td>float</td><td>Y</td><td>支付的各项税费</td></tr><tr><td>n_incr_clt_loan_adv</td><td>float</td><td>Y</td><td>客户贷款及垫款净增加额</td></tr><tr><td>n_incr_dep_cbob</td><td>float</td><td>Y</td><td>存放央行和同业款项净增加额</td></tr><tr><td>c_pay_claims_orig_inco</td><td>float</td><td>Y</td><td>支付原保险合同赔付款项的现金</td></tr><tr><td>pay_handling_chrg</td><td>float</td><td>Y</td><td>支付手续费的现金</td></tr><tr><td>pay_comm_insur_plcy</td><td>float</td><td>Y</td><td>支付保单红利的现金</td></tr><tr><td>oth_cash_pay_oper_act</td><td>float</td><td>Y</td><td>支付其他与经营活动有关的现金</td></tr><tr><td>st_cash_out_act</td><td>float</td><td>Y</td><td>经营活动现金流出小计</td></tr><tr><td>n_cashflow_act</td><td>float</td><td>Y</td><td>经营活动产生的现金流量净额</td></tr><tr><td>oth_recp_ral_inv_act</td><td>float</td><td>Y</td><td>收到其他与投资活动有关的现金</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>c_disp_withdrwl_invest</td><td>float</td><td>Y</td><td>收回投资收到的现金</td></tr><tr><td>c_recp_return_invest</td><td>float</td><td>Y</td><td>取得投资收益收到的现金</td></tr><tr><td>n_recp_disp_fiolta</td><td>float</td><td>Y</td><td>处置固定资产、无形资产和其他长期资产</td></tr><tr><td>n_recp_disp_sobu</td><td>float</td><td>Y</td><td>处置子公司及其他营业单位收到的现金净</td></tr><tr><td>stot_inflows_inv_act</td><td>float</td><td>Y</td><td>投资活动现金流入小计</td></tr><tr><td>c_pay_acq_const_fiolta</td><td>float</td><td>Y</td><td>购建固定资产、无形资产和其他长期资产</td></tr><tr><td>c_paid_invest</td><td>float</td><td>Y</td><td>投资支付的现金</td></tr><tr><td>n_disp_subs_oth_biz</td><td>float</td><td>Y</td><td>取得子公司及其他营业单位支付的现金净</td></tr><tr><td>oth_pay_ral_inv_act</td><td>float</td><td>Y</td><td>支付其他与投资活动有关的现金</td></tr><tr><td>n_incr_pledge_loan</td><td>float</td><td>Y</td><td>质押贷款净增加额</td></tr><tr><td>stot_out_inv_act</td><td>float</td><td>Y</td><td>投资活动现金流出小计</td></tr><tr><td>n_cashflow_inv_act</td><td>float</td><td>Y</td><td>投资活动产生的现金流量净额</td></tr><tr><td>c_recp_borrow</td><td>float</td><td>Y</td><td>取得借款收到的现金</td></tr><tr><td>proc_issue_bonds</td><td>float</td><td>Y</td><td>发行债券收到的现金</td></tr><tr><td>oth_cash_recp_ral_fnc_act</td><td>float</td><td>Y</td><td>收到其他与筹资活动有关的现金</td></tr><tr><td>stot_cash_in_fnc_act</td><td>float</td><td>Y</td><td>筹资活动现金流入小计</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>free_cashflow</td><td>float</td><td>Y</td><td>企业自由现金流量</td></tr><tr><td>c_prepay_amt_borr</td><td>float</td><td>Y</td><td>偿还债务支付的现金</td></tr><tr><td>c_pay_dist_dpcp_int_exp</td><td>float</td><td>Y</td><td>分配股利、利润或偿付利息支付的现金</td></tr><tr><td>incl_dvd_profit_paid_sc_ms</td><td>float</td><td>Y</td><td>其中:子公司支付给少数股东的股利、利</td></tr><tr><td>oth_cashpay_ral_fnc_act</td><td>float</td><td>Y</td><td>支付其他与筹资活动有关的现金</td></tr><tr><td>stot_cashout_fnc_act</td><td>float</td><td>Y</td><td>筹资活动现金流出小计</td></tr><tr><td>n_cash_flows_fnc_act</td><td>float</td><td>Y</td><td>筹资活动产生的现金流量净额</td></tr><tr><td>eff_fx_flu_cash</td><td>float</td><td>Y</td><td>汇率变动对现金的影响</td></tr><tr><td>n_incr_cash_cash_equ</td><td>float</td><td>Y</td><td>现金及现金等价物净增加额</td></tr><tr><td>c_cash_equ_beg_period</td><td>float</td><td>Y</td><td>期初现金及现金等价物余额</td></tr><tr><td>c_cash_equ_end_period</td><td>float</td><td>Y</td><td>期末现金及现金等价物余额</td></tr><tr><td>c_recp_cap_contrib</td><td>float</td><td>Y</td><td>吸收投资收到的现金</td></tr><tr><td>incl_cash_rec_saims</td><td>float</td><td>Y</td><td>其中:子公司吸收少数股东投资收到的现</td></tr><tr><td>uncon_invest_loss</td><td>float</td><td>Y</td><td>未确认投资损失</td></tr><tr><td>prov_depr_assets</td><td>float</td><td>Y</td><td>加:资产减值准备</td></tr><tr><td>depr_fa_coga_dpba</td><td>float</td><td>Y</td><td>固定资产折旧、油气资产折耗、生产性生</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>amort_intang_assets</td><td>float</td><td>Y</td><td>无形资产摊销</td></tr><tr><td>It_amort_deferred_exp</td><td>float</td><td>Y</td><td>长期待摊费用摊销</td></tr><tr><td>decr_deferred_exp</td><td>float</td><td>Y</td><td>待摊费用减少</td></tr><tr><td>incr_acc_exp</td><td>float</td><td>Y</td><td>预提费用增加</td></tr><tr><td>loss_disp_fiolta</td><td>float</td><td>Y</td><td>处置固定、无形资产和其他长期资产的</td></tr><tr><td>loss_scr_fa</td><td>float</td><td>V</td><td>固定资产报废损失</td></tr><tr><td>loss_fv_chg</td><td>float</td><td>Y</td><td>公允价值变动损失</td></tr><tr><td>invest_loss</td><td>float</td><td>Y</td><td>投资损失</td></tr><tr><td>decr_def_inc_tax_assets</td><td>float</td><td>Y</td><td>递延所得税资产减少</td></tr><tr><td>incr_def_inc_tax_liab</td><td>float</td><td>Y</td><td>递延所得税负债增加</td></tr><tr><td>decr_inventories</td><td>float</td><td>Y</td><td>存货的减少</td></tr><tr><td>decr_oper_payable</td><td>float</td><td>Y</td><td>经营性应收项目的减少</td></tr><tr><td>incr_oper_payable</td><td>float</td><td>Y</td><td>经营性应付项目的增加</td></tr><tr><td>others</td><td>float</td><td>Y</td><td>其他</td></tr><tr><td>im_net_cashflow_oper_act</td><td>float</td><td>Y</td><td>经营活动产生的现金流量净额(间接法)</td></tr><tr><td>conv_debt_into_cap</td><td>float</td><td></td><td>债务转为资本</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>conv_copbonds_due_within_1y</td><td>float</td><td>Y</td><td>一年内到期的可转换公司债券</td></tr><tr><td>fa_fnc_leases</td><td>float</td><td>Y</td><td>融资租入固定资产</td></tr><tr><td>im_n_incr_cash_equ</td><td>float</td><td>Y</td><td>现金及现金等价物净增加额(间接法)</td></tr><tr><td>net_dism_capital_add</td><td>float</td><td>Y</td><td>拆出资金净增加额</td></tr><tr><td>net_cash_rece_sec</td><td>float</td><td>Y</td><td>代理买卖证券收到的现金净额(元)</td></tr><tr><td>credit_impa_loss</td><td>float</td><td>Y</td><td>信用减值损失</td></tr><tr><td>use_right_asset_dep</td><td>float</td><td>Y</td><td>使用权资产折旧</td></tr><tr><td>oth_loss_asset</td><td>float</td><td>V</td><td>其他资产减值损失</td></tr><tr><td>end_bal_cash</td><td>float</td><td>Y</td><td>现金的期末余额</td></tr><tr><td>beg_bal_cash</td><td>float</td><td>Y</td><td>减:现金的期初余额</td></tr><tr><td>end_bal_cash_equ</td><td>float</td><td>Y</td><td>加:现金等价物的期末余额</td></tr><tr><td>beg_bal_cash_equ</td><td>float</td><td>Y</td><td>减:现金等价物的期初余额</td></tr><tr><td>update_flag</td><td>str</td><td>Y</td><td>更新标志(1 最新)</td></tr></table></body></html>  

# 输出参数  

# 接口使用说明  

pro $=$ ts.pro_api()  

df $=$ pro.cashflow(ts_code $=$ '600000.SH', start_date $=$ '20180101', e nd_date $=$ '20180730')  

获取某一季度全部股票数据  

$\mathsf{d}\mathsf{f}2\mathsf{\Omega}=\mathsf{\Omega}$ pro.cashflow_vip(period $=$ '20181231',fields='')  

# 数据样例  

ts_code  ann_date f_ann_date  end_date comp_type report_typ   
e net_profit finan_exp \   
0 600000.SH  20180428 20180428 20180331 2 1 NaN None   
1 600000.SH  20180428 20180428 20171231 2 1 5.500200e+10 None   
2 600000.SH  20180428 20180428 20171231 2 5.500200e+10 None  

# 主要报表类型说明  

<html><body><table><tr><td>代码</td><td>类型</td><td>说明</td></tr><tr><td>1</td><td>合并报表</td><td>上市公司最新报表 (默认)</td></tr><tr><td>2</td><td>单季合并</td><td>单一季度的合并报表</td></tr><tr><td>3</td><td>调整单季合并表</td><td>调整后的单季合并报表 （如果有)</td></tr><tr><td>4</td><td>调整合并报表</td><td>本年度公布上年同期的财务报表数据，报告期为上年度</td></tr><tr><td>5</td><td>调整前合并报表</td><td>数据发生变更，将原数据进行保留，即调整前的原数据</td></tr><tr><td>6</td><td>母公司报表</td><td>该公司母公司的财务报表数据</td></tr><tr><td>7</td><td>母公司单季表</td><td>母公司的单季度表</td></tr></table></body></html>  

<html><body><table><tr><td>代码</td><td>类型</td><td>说明</td></tr><tr><td>8</td><td>母公司调整单季表</td><td>母公司调整后的单季表</td></tr><tr><td>9</td><td>母公司调整表</td><td>该公司母公司的本年度公布上年同期的财务报表数据</td></tr><tr><td>10</td><td>母公司调整前报表</td><td>母公司调整之前的原始财务报表数据</td></tr><tr><td>11</td><td>目公司调整前合并报表</td><td>母公司调整之前合并报表原数据</td></tr><tr><td>12</td><td>母公司调整前报表</td><td>母公司报表发生变更前保留的原数据</td></tr></table></body></html>  

# 业绩预告  

接口：forecast，可以通过数据工具调试和查看数据。  

描述：获取业绩预告数据权限：用户需要至少2000 积分才可以调取，具体请参阅积分获取办法  

提示：当前接口只能按单只股票获取其历史数据，如果需要获取某一季度全部上市公司数据，请使用forecast_vip 接口（参数一致），需积攒5000 积分。  

# 输入参数  

<html><body><table><tr><td>名称</td><td>类 型</td><td>必 选</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td>N</td><td>股票代码(二选一)</td></tr><tr><td>ann_date</td><td>str</td><td>N</td><td>公告日期 (二选一)</td></tr><tr><td>start_date</td><td>str</td><td>N</td><td>公告开始日期</td></tr><tr><td>end_date</td><td>str</td><td>N</td><td>公告结束日期</td></tr><tr><td>period</td><td>str</td><td>N</td><td>20170930三季报)</td></tr><tr><td>type</td><td>str</td><td>N</td><td>预告类型(预增/预减/扭亏/首亏/续亏/续盈/略增/略减)</td></tr></table></body></html>  

# 输出参数  

<html><body><table><tr><td>名称</td><td>类型</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td>TS 股票代码</td></tr><tr><td>ann_date</td><td>str</td><td>公告日期</td></tr><tr><td>end_date</td><td>str</td><td>报告期</td></tr><tr><td>type</td><td>str</td><td>业绩预告类型(预增/预减/扭亏/首亏/续亏/续盈/略增/略减)</td></tr><tr><td>p_change_min</td><td>float</td><td>预告净利润变动幅度下限 （%)</td></tr><tr><td>p_change_max</td><td>float</td><td>预告净利润变动幅度上限 (%)</td></tr><tr><td>net_profit_min</td><td>float</td><td>预告净利润下限 (万元)</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>描述</td></tr><tr><td>net_profit_max</td><td>float</td><td>预告净利润上限 (万元)</td></tr><tr><td>last_parent_net</td><td>float</td><td>上年同期归属母公司净利润</td></tr><tr><td>first_ann_date</td><td>str</td><td>首次公告日</td></tr><tr><td>summary</td><td>str</td><td>业绩预告摘要</td></tr><tr><td>change_reason</td><td>str</td><td>业绩变动原因</td></tr></table></body></html>  

# 接口用法  

pro $=$ ts.pro_api()  

pro.forecast(ann_date $=$ '20190131', fields $=$ 'ts_code,ann_date,end_ date,type,p_change_min,p_change_max,net_profit_min')  

获取某一季度全部股票数据  

df $=$ pro.forecast_vip(period $=$ '20181231',fields $=$ 'ts_code,ann_dat e,end_date,type,p_change_min,p_change_max,net_profit_min')  

# 数据样例  

ts_code  ann_date  end_date type  p_change_min  p_change_   
max \   
0 000005.SZ 20190131 20181231 预增 618.5600 945.   
1800   
1 000825.SZ 20190131 20181231 略增 3.8500 12.   
5100   
2 000566.SZ 20190131 20181231 预增 50.0000 100.   
0000   
3 000932.SZ 20190131 20181231 预增 60.8864 68.   
1664   
4 000557.SZ 20190131 20181231 预增 66.6800 66.   
6800   
5 600127.SH 20190131 20181231 首亏 -601.5517 -510.   
3604   
6 600159.SH 20190131 20181231 预增 315.0000 315.   
0000   
7 600963.SH 20190131 20181231 略增 2.3800 11.   
5800   
8 002336.SZ 20190131 20181231 续亏 33.1367 47.   
9952   
9 601608.SH 20190131 20181231 预增 228.5900 274.   
5700   
10 600531.SH 20190131 20181231 预减 -61.8800 -54.   
3200   
11 300200.SZ 20190131 20181231 预增 82.4000 112.   
4000   
12 300441.SZ 20190131 20181231 略减 -20.5100 -0.   
6400   
13 300157.SZ 20190131 20181231 扭亏 107.3969 108.   
5176   
14 300052.SZ 20190131 20181231 略减 -30.0000 0.   
0000   
15 002328.SZ 20190131 20181231 略增 0.0000 20.   
0000   
16 300420.SZ 20190131 20181231 预增 61.1500 90.   
8000   
17 300109.SZ 20190131 20181231 续盈 -13.8100 7.   
7300   
18 300479.SZ 20190131 20181231 略减 -35.8400 -6.   
6700   
19 000402.SZ 20190131 20181231 略增 1.0000 10.   
0000   
20 002626.SZ 20190131  20181231 略增 37.1200 47.   
6600  

接口：express描述：获取上市公司业绩快报  

权限：用户需要至少2000 积分才可以调取，具体请参阅积分获取办法提示：当前接口只能按单只股票获取其历史数据，如果需要获取某一季度全部上市公司数据，请使用express_vip 接口（参数一致），需积攒5000 积分。  

# 输入参数  

<html><body><table><tr><td>名称</td><td>类 型</td><td>必 选</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td>Y</td><td>股票代码</td></tr><tr><td>ann_date</td><td>str</td><td>N</td><td>公告日期</td></tr><tr><td>start_date</td><td>str</td><td>N</td><td>公告开始日期</td></tr><tr><td>end_date</td><td>str</td><td>N</td><td>公告结束日期</td></tr><tr><td>period</td><td>str</td><td>N</td><td>报告期(每个季度最后一天的日期,比如20171231表示年报，20170630 三季报)</td></tr></table></body></html>  

# 输出参数  

<html><body><table><tr><td>名称</td><td>类型</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td>TS股票代码</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>描述</td></tr><tr><td>ann_date</td><td>str</td><td>公告日期</td></tr><tr><td>end_date</td><td>str</td><td>报告期</td></tr><tr><td>revenue</td><td>float</td><td>营业收入(元)</td></tr><tr><td>operate_profit</td><td>float</td><td>营业利润(元)</td></tr><tr><td>total_profit</td><td>float</td><td>利润总额(元)</td></tr><tr><td>n_income</td><td>float</td><td>净利润(元)</td></tr><tr><td>total_assets</td><td>float</td><td>总资产(元)</td></tr><tr><td>total_hldr_eqy_exc_min_int</td><td>float</td><td>股东权益合计(不含少数股东权益)(元)</td></tr><tr><td>diluted_eps</td><td>float</td><td>每股收益(摊薄)(元)</td></tr><tr><td>diluted_roe</td><td>float</td><td>净资产收益率(摊薄)(%)</td></tr><tr><td>yoy_net_profit</td><td>float</td><td>去年同期修正后净利润</td></tr><tr><td>bps</td><td>float</td><td>每股净资产</td></tr><tr><td>yoy_sales</td><td>float</td><td>同比增长率:营业收入</td></tr><tr><td>yoy_op</td><td>float</td><td>同比增长率:营业利润</td></tr><tr><td>yoy_tp</td><td>float</td><td>同比增长率:利润总额</td></tr><tr><td>yoy_dedu_np</td><td>float</td><td>同比增长率:归属母公司股东的净利润</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型 描述</td><td></td></tr><tr><td>yoy_eps</td><td>float</td><td>同比增长率:基本每股收益</td></tr><tr><td>yoy_roe</td><td>float</td><td>同比增减:加权平均净资产收益率</td></tr><tr><td>growth_assets</td><td>float</td><td>比年初增长率:总资产</td></tr><tr><td>yoy_equity</td><td>float</td><td>比年初增长率:归属母公司的股东权益</td></tr><tr><td>growth_bps</td><td>float</td><td>比年初增长率:归属于母公司股东的每股净资</td></tr><tr><td>or_last_year</td><td>float</td><td>去年同期营业收入</td></tr><tr><td>op_last_year</td><td>float</td><td>去年同期营业利润</td></tr><tr><td>tp_last_year</td><td>float</td><td>去年同期利润总额</td></tr><tr><td>np_last_year</td><td>float</td><td>去年同期净利润</td></tr><tr><td>eps_last_year</td><td>float</td><td>去年同期每股收益</td></tr><tr><td>open_net_assets</td><td>float</td><td>期初净资产</td></tr><tr><td>open_bps</td><td>float</td><td>期初每股净资产</td></tr><tr><td>perf_summary</td><td>str</td><td>业绩简要说明</td></tr><tr><td>is_audit</td><td>int</td><td>是否审计：1是0否</td></tr><tr><td>remark</td><td>str</td><td>备注</td></tr><tr><td></td><td></td><td></td></tr></table></body></html>  

# 接口用法  

pro $=$ ts.pro_api()  

pro.express(ts_code $=$ '600000.SH', start_date $=$ '20180101', end_dat e='20180701', fields $=$ 'ts_code,ann_date,end_date,revenue,operate _profit,total_profit,n_income,total_assets')  

获取某一季度全部股票数据  

df $=$ pro.express_vip(period $=$ '20181231',fields $=$ 'ts_code,ann_dat e,end_date,revenue,operate_profit,total_profit,n_income,total_ assets')  

# 数据样例  

ts_code ann_date  end_date revenue operate_profit total_profit n_income  total_assets  \ 0 603535.SH 20180411  20180331  2.064659e+08 3.345047e+07 3.340047e+07 2.672643e+07  1.682111e+09 1 603535.SH 20180208  20171231  1.034262e+09 1.323373e+08 1.440493e+08 1.188325e+08  1.710466e+09 2 603535.SH 20171016  20170930  7.064117e+08 9.509520e+07 9.931530e+07 8.202480e+07  1.672986e+09  

# 分红送股  

接口：dividend  

描述：分红送股数据  

权限：用户需要至少2000 积分才可以调取，具体请参阅积分获取办法  

# 输入参数  

以上参数至少有一个不能为空  


<html><body><table><tr><td>名称</td><td>类型</td><td>必选</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td>N</td><td>TS代码</td></tr><tr><td>ann_date</td><td>str</td><td>N</td><td>公告日</td></tr><tr><td>record_date</td><td>str</td><td>N</td><td>股权登记日期</td></tr><tr><td>ex_date</td><td>str</td><td>N</td><td>除权除息日</td></tr><tr><td>imp_ann_date</td><td>str</td><td>N</td><td>实施公告日</td></tr></table></body></html>  

输出参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td>Y</td><td>TS代码</td></tr><tr><td>end_date</td><td>str</td><td>Y</td><td>分红年度</td></tr><tr><td>ann_date</td><td>str</td><td>Y</td><td>预案公告日</td></tr><tr><td>div_proc</td><td>str</td><td>Y</td><td>实施进度</td></tr><tr><td>stk_div</td><td>float</td><td>Y</td><td>每股送转</td></tr><tr><td>stk_bo_rate</td><td>float</td><td></td><td>每股送股比例</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>stk_co_rate</td><td>float</td><td>Y</td><td>每股转增比例</td></tr><tr><td>cash_div</td><td>float</td><td>Y</td><td>每股分红 (税后)</td></tr><tr><td>cash_div_tax</td><td>float</td><td>Y</td><td>每股分红 (税前)</td></tr><tr><td>record_date</td><td>str</td><td></td><td>股权登记日</td></tr><tr><td>ex_date</td><td>str</td><td>Y</td><td>除权除息日</td></tr><tr><td>pay_date</td><td>str</td><td></td><td>派息日</td></tr><tr><td>div_listdate</td><td>str</td><td></td><td>红股上市日</td></tr><tr><td>imp_ann_date</td><td>str</td><td>Y</td><td>实施公告日</td></tr><tr><td>base_date</td><td>str</td><td>N</td><td>基准日</td></tr><tr><td>base_share</td><td>float</td><td>N</td><td>基准股本 (万)</td></tr></table></body></html>  

# 接口示例  

pro $=$ ts.pro_api()  

df $=$ pro.dividend(ts_code $=$ '600848.SH', fields $=$ 'ts_code,div_pro c,stk_div,record_date,ex_date')  

# 数据样例  

ts_code div_proc stk_div record_date ex_date 0 600848.SH 实施 0.10 19950606 19950607 1 600848.SH 实施 0.10 19970707 19970708 2 600848.SH 实施 0.15 19960701 19960702  

# 财务指标数据  

接口：fina_indicator，可以通过数据工具调试和查看数据。  

描述：获取上市公司财务指标数据，为避免服务器压力，现阶段每次请求最多返回60 条记录，可通过设置日期多次请求获取更多数据。  

权限：用户需要至少2000 积分才可以调取，具体请参阅积分获取办法  

提示：当前接口只能按单只股票获取其历史数据，如果需要获取某一季度全部上市公司数据，请使用fina_indicator_vip 接口（参数一致），需积攒5000 积分。  

输入参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>必选</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td></td><td>TS 股票代码,e.g.600001.SH/000001.SZ</td></tr><tr><td>ann_date</td><td>str</td><td>N</td><td>公告日期</td></tr><tr><td>start_date</td><td>str</td><td>N</td><td>报告期开始日期</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>必选</td><td>描述</td></tr><tr><td>end_date</td><td>str</td><td>N</td><td>报告期结束日期</td></tr><tr><td>period</td><td>str</td><td>N</td><td>报告期(每个季度最后一天的日期,比如 20171231表示年报)</td></tr></table></body></html>  

输出参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td>Y</td><td>TS代码</td></tr><tr><td>ann_date</td><td>str</td><td>Y</td><td>公告日期</td></tr><tr><td>end_date</td><td>str</td><td>Y</td><td>报告期</td></tr><tr><td>eps</td><td>float</td><td>Y</td><td>基本每股收益</td></tr><tr><td>dt_eps</td><td>float</td><td>Y</td><td>稀释每股收益</td></tr><tr><td>total_revenue_ps</td><td>float</td><td>Y</td><td>每股营业总收入</td></tr><tr><td>revenue_ps</td><td>float</td><td>Y</td><td>每股营业收入</td></tr><tr><td>capital_rese_ps</td><td>float</td><td>Y</td><td>每股资本公积</td></tr><tr><td>surplus_rese_ps</td><td>float</td><td>Y</td><td>每股盈余公积</td></tr><tr><td>undist_profit_ps</td><td>float</td><td>Y</td><td>每股未分配利润</td></tr><tr><td>extra_item</td><td>float</td><td>Y</td><td>非经常性损益</td></tr><tr><td>profit_dedt</td><td>float</td><td>Y</td><td>扣除非经常性损益后的净利润（扣非净利</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>gross_margin</td><td>float</td><td>Y</td><td>毛利</td></tr><tr><td>current_ratio</td><td>float</td><td>Y</td><td>流动比率</td></tr><tr><td>quick_ratio</td><td>float</td><td>Y</td><td>速动比率</td></tr><tr><td>cash_ratio</td><td>float</td><td>Y</td><td>保守速动比率</td></tr><tr><td>invturn_days</td><td>float</td><td>N</td><td>存货周转天数</td></tr><tr><td>arturn_days</td><td>float</td><td>N</td><td>应收账款周转天数</td></tr><tr><td>inv_turn</td><td>float</td><td>N</td><td>存货周转率</td></tr><tr><td>ar_turn</td><td>float</td><td>Y</td><td>应收账款周转率</td></tr><tr><td>ca_turn</td><td>float</td><td>Y</td><td>流动资产周转率</td></tr><tr><td>fa_turn</td><td>float</td><td>Y</td><td>固定资产周转率</td></tr><tr><td>assets_turn</td><td>float</td><td>Y</td><td>总资产周转率</td></tr><tr><td>op_income</td><td>float</td><td>Y</td><td>经营活动净收益</td></tr><tr><td>valuechange_income</td><td>float</td><td>N</td><td>价值变动净收益</td></tr><tr><td>interst_income</td><td>float</td><td>N</td><td>利息费用</td></tr><tr><td>daa</td><td>float</td><td>N</td><td>折旧与摊销</td></tr><tr><td>ebit</td><td>float</td><td>Y</td><td>息税前利润</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>ebitda</td><td>float</td><td>Y</td><td>息税折旧摊销前利润</td></tr><tr><td>fcff</td><td>float</td><td>Y</td><td>企业自由现金流量</td></tr><tr><td>fcfe</td><td>float</td><td>Y</td><td>股权自由现金流量</td></tr><tr><td>current_exint</td><td>float</td><td>Y</td><td>无息流动负债</td></tr><tr><td>noncurrent_exint</td><td>float</td><td>Y</td><td>无息非流动负债</td></tr><tr><td>interestdebt</td><td>float</td><td>Y</td><td>带息债务</td></tr><tr><td>netdebt</td><td>float</td><td>Y</td><td>净债务</td></tr><tr><td>tangible_asset</td><td>float</td><td>Y</td><td>有形资产</td></tr><tr><td>working_capital</td><td>float</td><td>Y</td><td>营运资金</td></tr><tr><td>networking_capital</td><td>float</td><td></td><td>营运流动资本</td></tr><tr><td>invest_capital</td><td>float</td><td>Y</td><td>全部投入资本</td></tr><tr><td>retained_earnings</td><td>float</td><td>Y</td><td>留存收益</td></tr><tr><td>diluted2_eps</td><td>float</td><td>Y</td><td>期末摊薄每股收益</td></tr><tr><td>bps</td><td>float</td><td>Y</td><td>每股净资产</td></tr><tr><td>ocfps</td><td>float</td><td>V</td><td>每股经营活动产生的现金流量净额</td></tr><tr><td>retainedps</td><td>float</td><td>Y</td><td>每股留存收益</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>cfps</td><td>float</td><td>Y</td><td>每股现金流量净额</td></tr><tr><td>ebit_ps</td><td>float</td><td>Y</td><td>每股息税前利润</td></tr><tr><td>fcff_ps</td><td>float</td><td>Y</td><td>每股企业自由现金流量</td></tr><tr><td>fcfe_ps</td><td>float</td><td>Y</td><td>每股股东自由现金流量</td></tr><tr><td>netprofit_margin</td><td>float</td><td>Y</td><td>销售净利率</td></tr><tr><td>grossprofit_margin</td><td>float</td><td>Y</td><td>销售毛利率</td></tr><tr><td>cogs_of_sales</td><td>float</td><td>Y</td><td>销售成本率</td></tr><tr><td>expense_of_sales</td><td>float</td><td>Y</td><td>销售期间费用率</td></tr><tr><td>profit_to_gr</td><td>float</td><td>Y</td><td>净利润/营业总收入</td></tr><tr><td>saleexp_to_gr</td><td>float</td><td>Y</td><td>销售费用/营业总收入</td></tr><tr><td>adminexp_of-gr</td><td>float</td><td>Y</td><td>管理费用/营业总收入</td></tr><tr><td>finaexp_of-gr</td><td>float</td><td>Y</td><td>财务费用/营业总收入</td></tr><tr><td>impai_ttm</td><td>float</td><td>Y</td><td>资产减值损失/营业总收入</td></tr><tr><td>16-10-56</td><td>float</td><td>Y</td><td>营业总成本/营业总收入</td></tr><tr><td>op_of_gr</td><td>float</td><td>Y</td><td>营业利润/营业总收入</td></tr><tr><td>ebit_of_gr</td><td>float</td><td>Y</td><td>息税前利润/营业总收入</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>roe</td><td>float</td><td>Y</td><td>净资产收益率</td></tr><tr><td>roe_waa</td><td>float</td><td>Y</td><td>加权平均净资产收益率</td></tr><tr><td>roe_dt</td><td>float</td><td>Y</td><td>净资产收益率(扣除非经常损益)</td></tr><tr><td>roa</td><td>float</td><td>Y</td><td>总资产报酬率</td></tr><tr><td>npta</td><td>float</td><td>Y</td><td>总资产净利润</td></tr><tr><td>roic</td><td>float</td><td></td><td>投入资本回报率</td></tr><tr><td>roe_yearly</td><td>float</td><td>Y</td><td>年化净资产收益率</td></tr><tr><td>roa2_yearly</td><td>float</td><td>Y</td><td>年化总资产报酬率</td></tr><tr><td>roe_avg</td><td>float</td><td>N</td><td>平均净资产收益率(增发条件)</td></tr><tr><td>opincome_of_ebt</td><td>float</td><td>N</td><td>经营活动净收益/利润总额</td></tr><tr><td>investincome_of_ebt</td><td>float</td><td>N</td><td>价值变动净收益/利润总额</td></tr><tr><td>n_op_profit_of_ebt</td><td>float</td><td>N</td><td>营业外收支净额/利润总额</td></tr><tr><td>tax_to_ebt</td><td>float</td><td>N</td><td>所得税/利润总额</td></tr><tr><td>dtprofit_to_profit</td><td>float</td><td>N</td><td>扣除非经常损益后的净利润/净利润</td></tr><tr><td>salescash_to_or</td><td>float</td><td>N</td><td>销售商品提供劳务收到的现金/营业收入</td></tr><tr><td>ocf_to_or</td><td>float</td><td>N</td><td>经营活动产生的现金流量净额/营业收入</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>ocf_to_opincome</td><td>float</td><td>N</td><td>经营活动产生的现金流量净额/经营活动净</td></tr><tr><td>capitalized_to_da</td><td>float</td><td>N</td><td>资本支出/折旧和摊销</td></tr><tr><td>debt_to_assets</td><td>float</td><td>Y</td><td>资产负债率</td></tr><tr><td>assets_to_eqt</td><td>float</td><td>Y</td><td>权益乘数</td></tr><tr><td>dp_assets_to_eqt</td><td>float</td><td>Y</td><td>权益乘数(杜邦分析)</td></tr><tr><td>ca_to_assets</td><td>float</td><td>Y</td><td>流动资产/总资产</td></tr><tr><td>nca_to_assets</td><td>float</td><td>Y</td><td>非流动资产/总资产</td></tr><tr><td>tbassets_to_totalassets</td><td>float</td><td>Y</td><td>有形资产/总资产</td></tr><tr><td>int_to_talcap</td><td>float</td><td>Y</td><td>带息债务/全部投入资本</td></tr><tr><td>eqt_to_talcapital</td><td>float</td><td>Y</td><td>归属于母公司的股东权益/全部投入资本</td></tr><tr><td>currentdebt_to_debt</td><td>float</td><td>Y</td><td>流动负债/负债合计</td></tr><tr><td>longdeb_to_debt</td><td>float</td><td>Y</td><td>非流动负债/负债合计</td></tr><tr><td>ocf_to_shortdebt</td><td>float</td><td>Y</td><td>经营活动产生的现金流量净额/流动负债</td></tr><tr><td>debt_to_eqt</td><td>float</td><td>Y</td><td>产权比率</td></tr><tr><td>eqt_to_debt</td><td>float</td><td>Y</td><td>归属于母公司的股东权益/负债合计</td></tr><tr><td>eqt_to_interestdebt</td><td>float</td><td>Y</td><td>归属于母公司的股东权益/带息债务</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>tangibleasset_to_debt</td><td>float</td><td>Y</td><td>有形资产/负债合计</td></tr><tr><td>tangasset_to_intdebt</td><td>float</td><td>Y</td><td>有形资产/带息债务</td></tr><tr><td>tangibleasset_to_netdebt</td><td>float</td><td>Y</td><td>有形资产/净债务</td></tr><tr><td>ocf_to_debt</td><td>float</td><td>Y</td><td>经营活动产生的现金流量净额/负债合计</td></tr><tr><td>ocf_to_interestdebt</td><td>float</td><td>N</td><td>经营活动产生的现金流量净额/带息债务</td></tr><tr><td>ocf_to_netdebt</td><td>float</td><td>N</td><td>经营活动产生的现金流量净额/净债务</td></tr><tr><td>ebit_to_interest</td><td>float</td><td>N</td><td>已获利息倍数(EBIT/利息费用)</td></tr><tr><td>longdebt_to_workingcapital</td><td>float</td><td>N</td><td>长期债务与营运资金比率</td></tr><tr><td>ebitda_to_debt</td><td>float</td><td>N</td><td>息税折旧摊销前利润/负债合计</td></tr><tr><td>turn_days</td><td>float</td><td>Y</td><td>营业周期</td></tr><tr><td>roa_yearly</td><td>float</td><td>Y</td><td>年化总资产净利率</td></tr><tr><td>roa_dp</td><td>float</td><td>Y</td><td>总资产净利率(杜邦分析)</td></tr><tr><td>fixed_assets</td><td>float</td><td>Y</td><td>固定资产合计</td></tr><tr><td>profit_prefin_exp</td><td>float</td><td>N</td><td>扣除财务费用前营业利润</td></tr><tr><td>non_op_profit</td><td>float</td><td>N</td><td>非营业利润</td></tr><tr><td>op_to_ebt</td><td>float</td><td>N</td><td>营业利润／利润总额</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>nop_to_ebt</td><td>float</td><td>N</td><td>非营业利润／利润总额</td></tr><tr><td>ocf_to_profit</td><td>float</td><td>N</td><td>经营活动产生的现金流量净额／营业利润</td></tr><tr><td>cash_to_liqdebt</td><td>float</td><td>N</td><td>货币资金／流动负债</td></tr><tr><td>cash_to_liqdebt_withinterest</td><td>float</td><td>N</td><td>货币资金／带息流动负债</td></tr><tr><td>op_to_liqdebt</td><td>float</td><td>N</td><td>营业利润／流动负债</td></tr><tr><td>op_to_debt</td><td>float</td><td>N</td><td>营业利润／负债合计</td></tr><tr><td>roic_yearly</td><td>float</td><td>N</td><td>年化投入资本回报率</td></tr><tr><td>total_fa_trun</td><td>float</td><td>N</td><td>固定资产合计周转率</td></tr><tr><td>profit_to_op</td><td>float</td><td>Y</td><td>利润总额／营业收入</td></tr><tr><td>q_opincome</td><td>float</td><td>N</td><td>经营活动单季度净收益</td></tr><tr><td>q_investincome</td><td>float</td><td>N</td><td>价值变动单季度净收益</td></tr><tr><td>q_dtprofit</td><td>float</td><td>N</td><td>扣除非经常损益后的单季度净利润</td></tr><tr><td>q-eps</td><td>float</td><td>N</td><td>每股收益(单季度)</td></tr><tr><td>q_netprofit_margin</td><td>float</td><td>N</td><td>销售净利率(单季度)</td></tr><tr><td>q-gsprofit_margin</td><td>float</td><td>N</td><td>销售毛利率(单季度)</td></tr><tr><td>q_exp_to_sales</td><td>float</td><td>N</td><td>销售期间费用率(单季度)</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>q_profit_to_gr</td><td>float</td><td>N</td><td>净利润 ／营业总收入(单季度)</td></tr><tr><td>q_saleexp_to_gr</td><td>float Y</td><td></td><td>销售费用 ／营业总收入 (单季度)</td></tr><tr><td>q_adminexp_to_gr</td><td>float</td><td>N</td><td>管理费用 ／营业总收入 (单季度)</td></tr><tr><td>q_finaexp_to_gr</td><td>float N</td><td></td><td>财务费用 ／营业总收入 (单季度)</td></tr><tr><td>q_impair_to_gr_ttm</td><td>float N</td><td></td><td>资产减值损失 ／营业总收入(单季度)</td></tr><tr><td>q-gc_to_gr</td><td>float Y</td><td></td><td>营业总成本／营业总收入 (单季度)</td></tr><tr><td>u6-o-do-b</td><td>float N</td><td></td><td>营业利润 ／营业总收入(单季度)</td></tr><tr><td>q_roe</td><td>float Y</td><td></td><td>净资产收益率(单季度)</td></tr><tr><td>q_dt_roe</td><td>float Y</td><td></td><td>净资产单季度收益率(扣除非经常损益)</td></tr><tr><td>q_npta</td><td>float Y</td><td></td><td>总资产净利润(单季度)</td></tr><tr><td>q_opincome_to_ebt</td><td>float N</td><td></td><td>经营活动净收益 ／利润总额(单季度)</td></tr><tr><td>q_investincome_to_ebt</td><td>float N</td><td></td><td>价值变动净收益 /利润总额(单季度)</td></tr><tr><td>q_dtprofit_to_profit</td><td>float N</td><td></td><td>扣除非经常损益后的净利润／净利润(单季</td></tr><tr><td>q_salescash_to_or</td><td>float N</td><td></td><td>销售商品提供劳务收到的现金／营业收入(</td></tr><tr><td>q_ocf_to_sales</td><td>float Y</td><td></td><td>经营活动产生的现金流量净额／营业收入</td></tr><tr><td>q-ocf_to_or</td><td>float</td><td>N</td><td>经营活动产生的现金流量净额／经营活动</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>basic_eps_yoy</td><td>float</td><td>Y</td><td>基本每股收益同比增长率(%)</td></tr><tr><td>dt_eps_yoy</td><td>float</td><td>Y</td><td>稀释每股收益同比增长率(%)</td></tr><tr><td>cfps_yoy</td><td>float</td><td>Y</td><td>每股经营活动产生的现金流量净额同比增</td></tr><tr><td>op-yoy</td><td>float</td><td>Y</td><td>营业利润同比增长率(%)</td></tr><tr><td>ebt_yoy</td><td>float</td><td>Y</td><td>利润总额同比增长率(%)</td></tr><tr><td>netprofit_yoy</td><td>float</td><td>Y</td><td>归属母公司股东的净利润同比增长率(%)</td></tr><tr><td>dt_netprofit_yoy</td><td>float</td><td>Y</td><td>归属母公司股东的净利润-扣除非经常损益</td></tr><tr><td>ocf_yoy</td><td>float</td><td>Y</td><td>经营活动产生的现金流量净额同比增长率</td></tr><tr><td>roe_yoy</td><td>float</td><td>Y</td><td>净资产收益率(摊薄)同比增长率(%)</td></tr><tr><td>bps_yoy</td><td>float</td><td>Y</td><td>每股净资产相对年初增长率(%)</td></tr><tr><td>assets_yoy</td><td>float</td><td>Y</td><td>资产总计相对年初增长率(%)</td></tr><tr><td>eqt_yoy</td><td>float</td><td>Y</td><td>归属母公司的股东权益相对年初增长率(%</td></tr><tr><td>tr_yoy</td><td>float</td><td>Y</td><td>营业总收入同比增长率(%)</td></tr><tr><td>or_yoy</td><td>float</td><td>Y</td><td>营业收入同比增长率(%)</td></tr><tr><td>q-gr_yoy</td><td>float</td><td>N</td><td>营业总收入同比增长率(%)(单季度)</td></tr><tr><td>bob-6-b</td><td>float</td><td>N</td><td>营业总收入环比增长率(%)(单季度)</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>q_sales_yoy</td><td>float</td><td>Y</td><td>营业收入同比增长率(%)(单季度)</td></tr><tr><td>q_sales_qoq</td><td>float</td><td>N</td><td>营业收入环比增长率(%)(单季度)</td></tr><tr><td>q_op_yoy</td><td>float</td><td>N</td><td>营业利润同比增长率(%)(单季度)</td></tr><tr><td>bob-do-b</td><td>float</td><td>Y</td><td>营业利润环比增长率(%)(单季度)</td></tr><tr><td>q_profit_yoy</td><td>float</td><td>N</td><td>净利润同比增长率(%)(单季度)</td></tr><tr><td>bob-od-b</td><td>float</td><td>N</td><td>净利润环比增长率(%)(单季度)</td></tr><tr><td>q_netprofit_yoy</td><td>float</td><td>N</td><td>归属母公司股东的净利润同比增长率(%)(</td></tr><tr><td>q_netprofit_qoq</td><td>float</td><td>N</td><td>归属母公司股东的净利润环比增长率(%)(</td></tr><tr><td>equity-yoy</td><td>float</td><td>Y</td><td>净资产同比增长率</td></tr><tr><td>rd_exp</td><td>float</td><td>N</td><td>研发费用</td></tr><tr><td>update_flag</td><td>str</td><td>N</td><td>更新标识</td></tr></table></body></html>  

# 接口用法  

pro $=$ ts.pro_api()  

df $=$ pro.fina_indicator(ts_code $=$ '600000.SH')  

或者  

df $=$ pro.query('fina_indicator', ts_code $=$ '600000.SH', start_dat $\mathrm{e}=^{1}28176161^{\prime}$ , end_date $=$ '20180801')  

# 数据样例  

ts_code ann_date end_date eps dt_eps  total_revenue_ps rev enue_ps \  

0 600000.SH 20180830 20180630 0.95 0.95 2.8024 2.8024   
1 600000.SH 20180428 20180331 0.46 0.46 1.3501 1.3501   
2 600000.SH 20180428 20171231 1.84 1.84 5.7447 5.7447   
3 600000.SH 20180428 20171231 1.84 1.84 5.7447 5.7447   
4 600000.SH 20171028 20170930  1.45 1.45 4.2507 4.2507   
5 600000.SH 20171028 20170930  1.45 1.45 4.2507 4.2507   
6 600000.SH 20170830 20170630 0.97 0.97 2.9659 2.9659   
7 600000.SH 20170427 20170331 0.63 0.63 1.9595 1.9595   
8 600000.SH 20170427 20170331 0.63 0.63 1.9595 1.9595  

# 主营业务构成  

# 接口：fina_mainbz  

描述：获得上市公司主营业务构成，分地区和产品两种方式  

权限：用户需要至少2000 积分才可以调取，具体请参阅积分获取办  

法 ，单次最大提取100 行，总量不限制，可循环获取。  

提示：当前接口只能按单只股票获取其历史数据，如果需要获取某一季度全部上市公司数据，请使用fina_mainbz_vip 接口（参数一致），需积攒5000 积分。  

输入参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>必选</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td>Y</td><td>股票代码</td></tr><tr><td>period</td><td>str</td><td>N</td><td>报告期(每个季度最后一天的日期,比如 20171231表示年报)</td></tr><tr><td>type</td><td>str</td><td>N</td><td>类型：P按产品D按地区「按行业（请输入大写字母P或者</td></tr><tr><td>start_date</td><td>str</td><td>N</td><td>报告期开始日期</td></tr><tr><td>end_date</td><td>str</td><td>N</td><td>报告期结束日期</td></tr></table></body></html>  

输出参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td>TS代码</td></tr><tr><td>end_date</td><td>str</td><td>报告期</td></tr><tr><td>bz_item</td><td>str</td><td>主营业务来源</td></tr><tr><td>bz_sales</td><td>float</td><td>主营业务收入(元)</td></tr><tr><td>bz_profit</td><td>float</td><td>主营业务利润(元)</td></tr><tr><td>bz_cost</td><td>float</td><td>主营业务成本(元)</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>描述</td></tr><tr><td>curr_type</td><td>str</td><td>货币代码</td></tr><tr><td>update_flag</td><td>str</td><td>是否更新</td></tr></table></body></html>  

# 代码示例  

pro $=$ ts.pro_api()  

df $=$ pro.fina_mainbz(ts_code $=$ '000627.SZ', type='P')  

获取某一季度全部股票数据  

df $=$ pro.fina_mainbz_vip(period $=$ '20181231', type $=$ 'P' ,fields='t s_code,end_date,bz_item,bz_sales')  

# 数据样例  

ts_code  end_date bz_item bz_sales bz_profit bz_cost curr_type 0 000627.SZ  20171231 其他产品 1.847507e+08 None None CNY 1 000627.SZ  20171231 其他主营业务 1.847507e+08 None None CNY 2 000627.SZ  20171231 聚丙烯 6.629111e+07 None None CNY 3 000627.SZ 20171231 原料药产品 2.685909e+08 None None CNY 4 000627.SZ  20171231 保险业务 5.288595e+10 None None CNY  

接口：disclosure_date  
描述：获取财报披露计划日期  
限量：单次最大3000，总量不限制  
积分：用户需要至少500 积分才可以调取，积分越多权限越大，具体请  
参阅积分获取办法  

# 输入参数  

<html><body><table><tr><td>名称</td><td>类 型</td><td>必 选</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td>N</td><td>TS股票代码</td></tr><tr><td>end_date</td><td>str</td><td>N</td><td>财报周期（每个季度最后一天的日期，比如20181231表示2018年1 示中报)</td></tr><tr><td>pre_date</td><td>str</td><td>N</td><td>计划披露日期</td></tr><tr><td>actual_date</td><td>str</td><td>N</td><td>实际披露日期</td></tr></table></body></html>  

输出参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td></td><td>TS代码</td></tr><tr><td>ann_date</td><td>str</td><td></td><td>最新披露公告日</td></tr><tr><td>end_date</td><td>str</td><td></td><td>报告期</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>pre_date</td><td>str</td><td></td><td>预计披露日期</td></tr><tr><td>actual_date</td><td>str</td><td></td><td>实际披露日期</td></tr><tr><td>modify_date</td><td>str</td><td>N</td><td>披露日期修正记录</td></tr></table></body></html>  

# 接口使用  

pro $=$ ts.pro_api()  

df $=$ pro.disclosure_date(end_date $=$ '20181231')  

# 数据示例  

ts_code  ann_date end_date  pre_date actual_date modify _date 0 300619.SZ 20181228 20181231 20190122 20190122 None 1 300125.SZ 20181228 20181231 20190129 20190129 None 2 601619.SH 20181227 20181231 20190129 20190129 None 3 000055.SZ 20181228 20181231 20190130 20190130 None 4 002910.SZ 20181228 20181231 20190131 None None 5 002188.SZ 20181228 20181231 20190131 None None 6 600738.SH 20190124  20181231 20190131 None None 7 002107.SZ 20181228  20181231 20190201 None None 8 300748.SZ 20181228 20181231 20190201 None None 9 002675.SZ 20181228 20181231 20190201 None None  

10 002167.SZ  20181228 20181231 20190201 None None   
11 002211.SZ 20190125 20181231 20190201 None None   
12 002240.SZ 20181228 20181231 20190201 None None   
13 002245.SZ  20181228 20181231 20190201 None None   
14 002552.SZ 20181228 20181231 20190201 None None   
15 002825.SZ 20181228 20181231 20190201 None None  

# 前十大股东  

# 接口：top10_holders  

描述：获取上市公司前十大股东数据，包括持有数量和比例等信息  

积分：需2000 积分以上才可以调取本接口，5000 积分以上频次会更高  

输入参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>必选</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td></td><td>TS代码</td></tr><tr><td>period</td><td>str</td><td>N</td><td>报告期 月（YYYYMMDD格式，一般为每个季度最后一天）</td></tr><tr><td>ann_date</td><td>str</td><td>N</td><td>公告日期</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>必选</td><td>描述</td></tr><tr><td>start_date</td><td>str</td><td>N</td><td>报告期开始日期</td></tr><tr><td>end_date</td><td>str</td><td>N</td><td>报告期结束日期</td></tr></table></body></html>  

输出参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td>TS股票代码</td></tr><tr><td>ann_date</td><td>str</td><td>公告日期</td></tr><tr><td>end_date</td><td>str</td><td>报告期</td></tr><tr><td>holder_name</td><td>str</td><td>股东名称</td></tr><tr><td>hold_amount</td><td>float</td><td>持有数量 (股)</td></tr><tr><td>hold_ratio</td><td>float</td><td>占总股本比例(%)</td></tr><tr><td>hold_float_ratio</td><td>float</td><td>占流通股本比例(%)</td></tr><tr><td>hold_change</td><td>float</td><td>持股变动</td></tr><tr><td>holder_type</td><td>str</td><td>股东类型</td></tr></table></body></html>  

# 接口用法  

pro $=$ ts.pro_api()  

df $=$ pro.top10_holders(ts_code $=$ '600000.SH', start_date $=$ '2017010 1', end_date $=$ '20171231')  

或者  

df $=$ pro.query('top10_holders', ts_code $=$ '600000.SH', start_date $=^{\prime}26176161^{\prime}$ , end_date $=$ '20171231')  

# 数据样例  

holder_na  

ts_code ann_date end_date   
me hold_amount hold_ratio   
0 600000.SH 20180428 20171231   
统 2.779437e+09 9.47   
1 600000.SH 20180428 20171231   
9.455690e+08 3.22   
2 600000.SH 20180428 20171231   
能H  1.270429e+09 4.33   
3 600000.SH 20180428 20171231   
本金 1.763232e+09 6.01   
4 600000.SH 20180428 20171231   
331323e+09 21.57   
5 600000.SH 20180428 20171231   
5.334893e+09 18.18   
6 600000.SH 20180428 20171231   
1.216979e+09 4.15   
7 600000.SH 20180428 20171231   
8.861313e+08 3.02   
8 600000.SH 20180428 20171231   
3.985214e+08 1.36   
9 600000.SH 20180428 20171231   
1.395571e+09 4.75  

富德生命人寿保险股份有限公司-传上海国鑫投资发展有限公司  
富德生命人寿保险股份有限公司-万  
富德生命人寿保险股份有限公司-资上海国际集团有限公司  6.中国移动通信集团广东有限公司中国证券金融股份有限公司梧桐树投资平台有限责任公司中央汇金资产管理有限责任公司上海上国投资产管理有限公司  

# 前十大流通股东  

接口：top10_floatholders  

描述：获取上市公司前十大流通股东数据  

积分：需2000 积分以上才可以调取本接口，5000 积分以上频次会更高  

输入参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>必选</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td>Y</td><td>TS代码</td></tr><tr><td>period</td><td>str</td><td>N</td><td>报告期（YYYYMMDD格式，一般为每个季度最后一天)</td></tr><tr><td>ann_date</td><td>str</td><td>N</td><td>公告日期</td></tr><tr><td>start_date</td><td>str</td><td>N</td><td>报告期开始日期</td></tr><tr><td>end_date</td><td>str</td><td>N</td><td>报告期结束日期</td></tr></table></body></html>  

输出参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td>TS股票代码</td></tr><tr><td>ann_date</td><td>str</td><td>公告日期</td></tr><tr><td>end_date</td><td>str</td><td>报告期</td></tr><tr><td>holder_name</td><td>str</td><td>股东名称</td></tr><tr><td>hold_amount</td><td>float</td><td>持有数量 (股)</td></tr><tr><td>hold_ratio</td><td>float</td><td>占总股本比例(%)</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>描述</td></tr><tr><td>hold_float_ratio</td><td>float</td><td>占流通股本比例(%)</td></tr><tr><td>hold_change</td><td>float</td><td>持股变动</td></tr><tr><td>holder_type</td><td>str</td><td>股东类型</td></tr></table></body></html>  

# 接口用法  

pro $=$ ts.pro_api()  

df $=$ pro.top10_floatholders(ts_code $^{1=}$ '600000.SH', start_date='20 170101', end_date $=$ '20171231')  

或者  

df $=$ pro.query('top10_floatholders', ts_code $=$ '600000.SH', start _date $=$ '20170101', end_date $=$ '20171231')  

# 数据样例  

ts_code  ann_date  end_date holder_name hold_amount0 600000.SH  20180428 20171231 富德生命人寿保险股份有限公司-资本金 1.763232e+091 600000.SH  20180428 20171231 上海国际集团有限公司  5.489319e+092 600000.SH  20180428 20171231 富德生命人寿保险股份有限公司-传统 2.779437e+093 600000.SH  20180428 20171231 中国证券金融股份有限公司1.216979e+094 600000.SH 20180428 20171231 梧桐树投资平台有限责任公司8.861313e+085 600000.SH 20180428 20171231 上海上国投资产管理有限公司1.395571e+09  

6  600000.SH  20180428 20171231 富德生命人寿保险股份有限公司-万能H  1.270429e+09  

7 600000.SH  20180428 20171231 上海国鑫投资发展有限公司  
5.392559e+08  
8 600000.SH  20180428 20171231 中央汇金资产管理有限责任公司3.985214e+08  
9 600000.SH  20180428 20171231 中国移动通信集团广东有限公司5.334893e+09  

# 概念股分类  

接口：concept  

描述：获取概念股分类，目前只有ts 一个来源，未来将逐步增加来源  

积分：用户需要至少300 积分才可以调取，具体请参阅积分获取办法  

注意：本接口数据已停止更新，请转移到同花顺概念接口  

# 输入参数  

<html><body><table><tr><td>名称</td><td>类型</td><td>必选</td><td>描述</td></tr><tr><td>src</td><td>str</td><td>N</td><td>来源，默认为ts</td></tr></table></body></html>  

输出参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>code</td><td>str</td><td>Y</td><td>概念分类ID</td></tr><tr><td>name</td><td>str</td><td>Y</td><td>概念分类名称</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>src</td><td>str</td><td>Y</td><td>来源</td></tr></table></body></html>  

# 接口使用  

pro $=$ ts.pro_api()  

df $=$ pro.concept()  

#或者 # df $=$ pro.concept(src='ts')  

# 数据示例  

code name src  
2 TS2 5G  ts  
3 TS3 机场 ts  
4 TS4 高价股 ts  
5 TS5 烧碱  ts  
6 TS6 AH 溢价股 ts  
7 TS7 保险  ts  
8 TS8 PVC  ts  
9 TS9 啤酒 ts  
10 TS10 火电 ts  
11 TS11 银行 ts  
12 TS12 碳纤维 ts  
13 TS13 安邦系 ts  
14 TS14 特高压 ts  
15 TS15 高股息 ts  
16 TS16 光通信 ts  
17 TS17 草甘膦 ts  
18 TS18 高速公路 ts  
19 TS19 有色-铝 ts  
20 TS20 有色-锆 ts  

# 概念股列表  

接口：concept_detail  

描述：获取概念股分类明细数据  

积分：用户需要至少300 积分才可以调取，具体请参阅积分获取办法  

注意：本接口数据已停止更新，请转移到同花顺概念接口  

输入参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>必选</td><td>描述</td></tr><tr><td>id</td><td>str</td><td>N</td><td>概念分类ID (id来自概念股分类接口）</td></tr><tr><td>ts_code</td><td>str</td><td>N</td><td>股票代码 （以上参数二选一）</td></tr></table></body></html>  

输出参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>id</td><td>str</td><td>Y</td><td>概念代</td></tr><tr><td>concept_name</td><td>str</td><td>Y</td><td>概念名</td></tr><tr><td>ts_code</td><td>str</td><td></td><td>股票代</td></tr><tr><td>name</td><td>str</td><td>Y</td><td>股票名</td></tr><tr><td>in_date</td><td>str</td><td>N</td><td>纳入日</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>out_date</td><td>str</td><td>N</td><td>剔除</td></tr></table></body></html>  

# 接口使用  

pro $=$ ts.pro_api()  

#取5G 概念明细 df $=$ pro.concept_detail( $\dot{\mathsf{1}}\mathsf{d}=$ 'TS2', fields $=$ 'ts_code,name')  

#或者查询某个股票的概念  

df $=$ pro.concept_detail(ts_code $=$ '600848.SH')  

# 数据示例  

ts_code name  
0 000008.SZ 神州高铁  
1 000063.SZ 中兴通讯  
2 000070.SZ 特发信息  
3 000586.SZ 汇源通信  
4 000636.SZ 风华高科  
5 000810.SZ 创维数字  
6 000836.SZ 富通鑫茂  
7 000938.SZ 紫光股份  
8 000988.SZ 华工科技  
9 002023.SZ 海特高新  
10 002089.SZ 新海宜  
11 002115.SZ 三维通信  
12 002138.SZ 顺络电子  
13 002179.SZ 中航光电  
14 002194.SZ \*ST 凡谷  
15 002217.SZ 合力泰  
16 002229.SZ 鸿博股份  
17 002231.SZ 奥维通信  
18 002281.SZ 光迅科技  
19 002309.SZ 中利集团  
20 002313.SZ 日海智能  
21 002384.SZ 东山精密  
22 002396.SZ 星网锐捷  
23 002402.SZ 和而泰  
24 002446.SZ 盛路通信  
25 002475.SZ 立讯精密  
26 002491.SZ 通鼎互联  
27 002544.SZ 杰赛科技  
28 002547.SZ 春兴精工  
29 002725.SZ 跃岭股份  

# 数据调取场景  

1、先通过概念股分类接口获取具体分类df $=$ pro.concept(src='ts')  

print(df)  

code name src  
0 TS0 密集调研 ts  
1 TS1 南北船合并 ts  
2 TS2 5G  ts  
3 TS3 机场 ts  
4 TS4 高价股 ts  
5 TS5 烧碱 ts  
6 TS6 AH 溢价股 ts  
7 TS7 保险  ts  
8 TS8 PVC  ts  
9 TS9 啤酒 ts  
10 TS10 火电 ts  
11 TS11 银行 ts  
12 TS12 碳纤维 ts  
13 TS13 安邦系 ts  
14 TS14 特高压 ts  
15 TS15 高股息 ts  
16 TS16 光通信 ts  
17 TS17 草甘膦 ts  
18 TS18 高速公路 ts  

上面的code 即概念股明细接口里的id 参数  

2、用上面接口示例的方法调取数据  

# 限售股解禁  

接口：share_float  

描述：获取限售股解禁  

限量：单次最大5000 条，总量不限制  

积分：120 分可调取，每分钟内限制次数，超过5000 积分频次相对较  

高，具体请参阅积分获取办法  

输入参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>必选</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td>N</td><td>TS股票代码（至少输入一个参数)</td></tr><tr><td>ann_date</td><td>str</td><td>N</td><td>公告日期（日期格式：YYYYMMDD，下同）</td></tr><tr><td>float_date</td><td>str</td><td>N</td><td>解禁日期</td></tr><tr><td>start_date</td><td>str</td><td>N</td><td>解禁开始日期</td></tr><tr><td>end_date</td><td>str</td><td>N</td><td>解禁结束日期</td></tr></table></body></html>  

# 输出参数  

<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td>Y</td><td>TS代码</td></tr><tr><td>ann_date</td><td>str</td><td>Y</td><td>公告日期</td></tr><tr><td>float_date</td><td>str</td><td>Y</td><td>解禁日期</td></tr><tr><td>float_share</td><td>float</td><td>Y</td><td>流通股份(股)</td></tr><tr><td>float_ratio</td><td>float</td><td>Y</td><td>流通股份占总股本比率</td></tr><tr><td>holder_name</td><td>str</td><td>Y</td><td>股东名称</td></tr><tr><td>share_type</td><td>str</td><td>Y</td><td>股份类型</td></tr></table></body></html>  

# 接口使用  

pro $=$ ts.pro_api()  

df $=$ pro.share_float(ann_date $^{1=}$ '20181220')  

# 数据示例  

ts_code ann_date float_date  float_share  float_ratio holder_name  

0 000998.SZ  20181220 20211221 25076106.0 1.9041王义波  

1 000998.SZ  20181220 20211221 11265340.0 0.8554彭泽斌  
2 000998.SZ  20181220 20211221 10820446.0 0.8216杨蔚  
3 000998.SZ  20181220 20211221 2704317.0 0.2053王宏  
4 000998.SZ 20181220 20211221 2704317.0 0.2053姜书贤  
5 000998.SZ 20181220 20211221 2952186.0 0.2242谢玉迁  
6 000998.SZ 20181220 20211221 3022098.0 0.2295陆利行000998.SZ 20181220 20211221 190668.0 0.0145史泽琪  
8 000998.SZ 20181220 20211221 190668.0 0.0145张林  
9 000998.SZ  20181220 20211221 95334.0 0.0072孙继明  
10 000998.SZ  20181220 20211221 95334.0 0.0072王青才  
11 000998.SZ 20181220 20211221 95334.0 0.0072刘榜  
12 000998.SZ 20181220 20211221 63556.0 0.0048朱静  
13 000998.SZ 20181220 20211221 63556.0 0.0048陈亮亮000998.SZ 20181220 20211221 63556.0 0.0048杜培林  
15 000998.SZ 20181220 20211221 63556.0 0.0048高飞  
16  000998.SZ  20181220 20211221 63556.0 0.0048胡素华  
17 000998.SZ 20181220 20211221 63556.0 0.0048王明磊  
18 000998.SZ 20181220 20211221 63556.0 0.0048刘占才  
19 000998.SZ 20181220 20211221 63556.0 0.0048傅兆作  
20 000998.SZ 20181220 20211221 63556.0 0.0048应银链share_type  
0 定增股份  
1 定增股份  

2 定增股份  
3 定增股份  
4 定增股份  
5 定增股份  
6 定增股份  
7 定增股份  
8 定增股份  
9 定增股份  
10 定增股份  
11 定增股份  
12 定增股份  
13 定增股份  
14 定增股份  
15 定增股份  
16 定增股份  
17 定增股份  
18 定增股份  
19 定增股份  
20 定增股份  

# 个股资金流向  

接口：moneyflow，可以通过数据工具调试和查看数据。  

描述：获取沪深A 股票资金流向数据，分析大单小单成交情况，用于判别资金动向，数据开始于2010 年。  

限量：单次最大提取6000 行记录，总量不限制  

积分：用户需要至少2000 积分才可以调取，基础积分有流量控制，积分越多权限越大，请自行提高积分，具体请参阅积分获取办法  

输入参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>必选</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td>N</td><td>股票代码 (股票和时间参数至少输入一个)</td></tr><tr><td>trade_date</td><td>str</td><td>N</td><td>交易日期</td></tr><tr><td>start_date</td><td>str</td><td>N</td><td>开始日期</td></tr><tr><td>end_date</td><td>str</td><td>N</td><td>结束日期</td></tr></table></body></html>  

输出参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td>Y</td><td>TS代码</td></tr><tr><td>trade_date</td><td>str</td><td></td><td>交易日期</td></tr><tr><td>buy_sm_vol</td><td>int</td><td></td><td>小单买入量 (手)</td></tr><tr><td>buy_sm_amount</td><td>float</td><td>Y</td><td>小单买入金额 (万元)</td></tr><tr><td>sell_sm_vol</td><td>int</td><td>Y</td><td>小单卖出量 (手)</td></tr><tr><td>sell_sm_amount</td><td>float</td><td>Y</td><td>小单卖出金额 (万元)</td></tr><tr><td>buy_md_vol</td><td>int</td><td></td><td>中单买入量 (手)</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>buy_md_amount</td><td>float</td><td>Y</td><td>中单买入金额 (万元)</td></tr><tr><td>sell_md_vol</td><td>int</td><td>Y</td><td>中单卖出量 (手)</td></tr><tr><td>sell_md_amount</td><td>float</td><td>Y</td><td>中单卖出金额 (万元)</td></tr><tr><td>buy_lg_vol</td><td>int</td><td></td><td>大单买入量 (手)</td></tr><tr><td>buy_lg_amount</td><td>float</td><td>Y</td><td>大单买入金额 (万元)</td></tr><tr><td>sell_lg_vol</td><td>int</td><td></td><td>大单卖出量 (手)</td></tr><tr><td>sell_lg_amount</td><td>float</td><td>Y</td><td>大单卖出金额 (万元)</td></tr><tr><td>buy_elg_vol</td><td>int</td><td>Y</td><td>特大单买入量 (手)</td></tr><tr><td>buy_elg_amount</td><td>float</td><td></td><td>特大单买入金额 (万元)</td></tr><tr><td>sell_elg_vol</td><td>int</td><td>Y</td><td>特大单卖出量 (手)</td></tr><tr><td>sell_elg_amount</td><td>float</td><td>Y</td><td>特大单卖出金额 (万元)</td></tr><tr><td>net_mf_vol</td><td>int</td><td>Y</td><td>净流入量 (手)</td></tr><tr><td>net_mf_amount</td><td>float</td><td>Y</td><td>净流入额 (万元)</td></tr></table></body></html>

各类别统计规则如下：  

小单：5 万以下 中单：5 万 ${\sim}20$ 万 大单：20 万 $\sim\!100$ 万 特大单：成交  

额 $>=\uparrow00$ 万 ，数据基于主动买卖单统计  

# 接口示例  

pro $=$ ts.pro_api('your token')  

#获取单日全部股票数据 df $=$ pro.moneyflow(trade_date $^{1=}$ '20190315')  

#获取单个股票数据   
df $=$ pro.moneyflow(ts_code $=$ '002149.SZ', start_date $=$ '20190115',   
end_date $=$ '20190315')  

# 数据示例  

ts_code trade_date  buy_sm_vol  buy_sm_amount sell_sm_v   
ol   
0 000779.SZ 20190315 11377 1150.17 1110   
0   
1 000933.SZ 20190315 94220 4803.22 10592   
4   
2 002270.SZ 20190315 43979 2330.96 4589   
3   
3 002319.SZ 20190315 21502 2952.88 1715   
5   
4 002604.SZ 20190315 31944 607.35 5866   
7   
5 300065.SZ 20190315 16048 2294.71 1642   
5   
6 600062.SH 20190315 55439 7432.13 6576   
5   
7 002735.SZ 20190315 3220 797.10 4598   
8 300196.SZ 20190315 12534 1286.02 834   
0   
9 300350.SZ 20190315 15346 1120.12 1885   
3   
10 600193.SH 20190315 12183 503.73 1957   
6   
11 002866.SZ 20190315 16932 2213.68 1603   
7   
12 300481.SZ 20190315 21386 4275.33 2186   
3   
13 600527.SH 20190315 115462 2975.44 7927   
2   
14 603980.SH 20190315 13957 1924.69 1171   
8   
15 600658.SH 20190315 71767 4826.73 6953   
5   
16 600812.SH 20190315 26140 1247.47 3492   
3   
17 002013.SZ 20190315 170234 12286.02 14850   
9   
18 600789.SH 20190315 211012 21644.56 15059   
8   
19 601636.SH 20190315 70737 3117.43 6807   
3   
20 000807.SZ 20190315 129668 6361.06 12207   
7  

sell_sm_amount  buy_md_vol  buy_md_amount  sell_md_vol  sel l_md_amount  

0 1122.97 13012 1316.72 14812  

1498.90   
1 5411.72 135976 6935.40 154023 7863.00   
2 2435.98 57679 3059.15 47279 2507.55   
3 2358.68 27245 3742.52 26708 3670.05   
4 1114.40 69897 1327.41 41108 781.19   
5 2353.34 31232 4472.05 26771 3834.95   
6 8817.75 86617 11615.40 79551 10676.99   
7 1140.61 4602 1141.61 2730 676.72   
8 855.45 9401 963.72 10478 1074.32   
9 1380.31 24224 1770.90 21588 1577.92   
10 812.58 28696 1185.17 31087 1286.11   
11 2100.70 19197 2511.62 20269 2650.56   
12 4379.14 31692 6345.72 32873 6578.36   
13 2046.54 107103 2763.00 84883 2191.24   
14 1619.33 14621 2019.41 14528 2005.69   
15 4691.29 92788 6232.80 93273 6280.13   
16 1669.97 38812 1855.78 39211 1874.05   
17 10726.22 154979 11190.69 164090 11855.76   
18 15479.08 269470 27660.18 236958 24338.36   
19 3000.73 90416 3984.68 115162 5075.50   
20 5999.66 175692 8627.77 178044 8751.08  

# 个股资金流向（THS）  

# 接口：moneyflow_ths  

描述：获取同花顺个股资金流向数据，每日盘后更新  

限量：单次最大6000，可根据日期或股票代码循环提取数据  

积分：用户需要至少5000 积分才可以调取，具体请参阅积分获取办法  

输入参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>必选</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td>N</td><td>股票代码</td></tr><tr><td>trade_date</td><td>str</td><td>N</td><td>交易日期（YYYYMMDD 格式，下同）</td></tr><tr><td>start_date</td><td>str</td><td>N</td><td>开始日期</td></tr><tr><td>end_date</td><td>str</td><td>N</td><td>结束日期</td></tr></table></body></html>  

输出参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>trade_date</td><td>str</td><td>Y</td><td>交易日期</td></tr><tr><td>ts_code</td><td>str</td><td></td><td>股票代码</td></tr><tr><td>name</td><td>str</td><td></td><td>股票名称</td></tr><tr><td>pct_change</td><td>float</td><td>Y</td><td>涨跌幅</td></tr><tr><td>latest</td><td>float</td><td></td><td>最新价</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>net_amount</td><td>float</td><td>Y</td><td>资金净流入(万元)</td></tr><tr><td>net_d5_amount</td><td>float</td><td>Y</td><td>5日主力净额(万元)</td></tr><tr><td>buy_lg-amount</td><td>float</td><td>Y</td><td>今日大单净流入额(万元</td></tr><tr><td>buy_lg_amount_rate</td><td>float</td><td>Y</td><td>今日大单净流入占比(%</td></tr><tr><td>buy_md_amount</td><td>float</td><td>Y</td><td>今日中单净流入额(万元</td></tr><tr><td>buy_md_amount_rate</td><td>float</td><td>Y</td><td>今日中单净流入占比(%</td></tr><tr><td>buy_sm_amount</td><td>float</td><td>Y</td><td>今日小单净流入额(万元</td></tr><tr><td>buy_sm_amount_rate</td><td>float</td><td>Y</td><td>今日小单净流入占比(%</td></tr></table></body></html>  

# 接口示例  

pro $=$ ts.pro_api()  

#获取单日全部股票数据 df $=$ pro.moneyflow_ths(trade_date $=$ '20241011')  

#获取单个股票数据   
df $=$ pro.moneyflow_ths(ts_code $=$ '002149.SZ', start_date $=$ '2024100   
1', end_date $=$ '20241011') trade_date ts_code  name  pct_change  ... buy_md_amount  bu   
y_md_amount_rate  buy_sm_amount  buy_sm_amount_rate  

0 20241011 002149.SZ 西部材料 2.47 -589.0 5.43 -191.0 1.76  

<html><body><table><tr><td rowspan="2">1</td><td rowspan="2">20241010</td><td rowspan="2">002149.SZ</td><td rowspan="2">西部材料</td><td rowspan="2">1.22</td><td colspan="2">-2732.0</td></tr><tr><td>5.81</td><td></td></tr><tr><td rowspan="2">2</td><td>20241009</td><td>15.38 002149.SZ</td><td>-1031.0 西部材料</td><td>7.00</td><td></td><td>-1941.0</td></tr><tr><td></td><td>9.25</td><td>-2079.0</td><td></td><td>9.90</td><td></td></tr><tr><td rowspan="2">3</td><td>20241008</td><td>002149.SZ</td><td>西部材料</td><td>5.17</td><td></td><td>-2985.0</td></tr><tr><td></td><td>7.93</td><td>-2507.0</td><td></td><td>6.66</td><td></td></tr></table></body></html>  

# 个股资金流向（DC）  

接口：moneyflow_dc  

描述：获取东方财富个股资金流向数据，每日盘后更新，数据开始于  

# 20230911  

限量：单次最大获取6000 条数据，可根据日期或股票代码循环提取数据积分：用户需要至少5000 积分才可以调取，具体请参阅积分获取办法  

输入参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>必选</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td>N</td><td>股票代码</td></tr><tr><td>trade_date</td><td>str</td><td>N</td><td>交易日期（YYYYMMDD格式，下同）</td></tr><tr><td>start_date</td><td>str</td><td>N</td><td>开始日期</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>必选</td><td>描述</td></tr><tr><td>end_date</td><td>str</td><td>N</td><td>结束日期</td></tr></table></body></html>  

输出参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>trade_date</td><td>str</td><td>Y</td><td>交易日期</td></tr><tr><td>ts_code</td><td>str</td><td>Y</td><td>股票代码</td></tr><tr><td>name</td><td>str</td><td>Y</td><td>股票名称</td></tr><tr><td>pct_change</td><td>float</td><td>Y</td><td>涨跌幅</td></tr><tr><td>close</td><td>float</td><td>Y</td><td>最新价</td></tr><tr><td>net_amount</td><td>float</td><td>Y</td><td>今日主力净流入额 (万元)</td></tr><tr><td>net_amount_rate</td><td>float</td><td>Y</td><td>今日主力净流入净占比 (%)</td></tr><tr><td>buy_elg_amount</td><td>float</td><td>Y</td><td>今日超大单净流入额（万元</td></tr><tr><td>buy_elg_amount_rate</td><td>float</td><td>Y</td><td>今日超大单净流入占比 (%)</td></tr><tr><td>buy_lg_amount</td><td>float</td><td>Y</td><td>今日大单净流入额 (万元)</td></tr><tr><td>buy_lg_amount_rate</td><td>float</td><td>Y</td><td>今日大单净流入占比 (%)</td></tr><tr><td>buy_md_amount</td><td>float</td><td>Y</td><td>今日中单净流入额 (万元)</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>buy_md_amount_rate</td><td>float</td><td></td><td>今日中单净流入占比 (%)</td></tr><tr><td>buy_sm_amount</td><td>float</td><td></td><td>今日小单净流入额 (万元)</td></tr><tr><td>buy_sm_amount_rate</td><td>float</td><td></td><td>今日小单净流入占比 (%)</td></tr></table></body></html>  

# 接口示例  

pro $=$ ts.pro_api()  

#获取单日全部股票数据 df $=$ pro.moneyflow_dc(trade_date $=$ '20241011')  

#获取单个股票数据   
df $=$ pro.moneyflow_dc(ts_code $=$ '002149.SZ', start_date $=$ '20240901   
, end_date='20240913')  

trade_date ts_code  name  pct_change ... buy_md_amount  bu y_md_amount_rate  buy_sm_amount  buy_sm_amount_rate  

0 20240913 002149.SZ 西部材料 -1.34 -12.65-0.35 -62.43 -1.72  
1 20240912 002149.SZ 西部材料 1.43 13.710.33 -388.43 -9.25  
2 20240911 002149.SZ 西部材料 -0.79 -26.10-1.68 95.69 6.15  
3 20240910 002149.SZ 西部材料 -0.08 -199.50-7.26 -69.29 -2.52  
4 20240909 002149.SZ 西部材料 1.12 66.762.48 -198.12 -7.37  
5 20240906 002149.SZ 西部材料 -2.49 -104.57-2.74 769.65 20.19  

<html><body><table><tr><td>6</td><td>20240905</td><td>002149.SZ</td><td>西部材料</td><td>-0.70</td><td></td><td>-307.62</td></tr><tr><td rowspan="3">7</td><td></td><td>-8.11</td><td>346.51</td><td></td><td>9.14</td><td></td></tr><tr><td>20240904</td><td>002149.SZ</td><td>西部材料</td><td>-0.92</td><td></td><td>370.98</td></tr><tr><td></td><td>9.56</td><td>-23.25</td><td></td><td>-0.60</td><td></td></tr><tr><td rowspan="2">8</td><td>20240903</td><td>002149.SZ</td><td>西部材料</td><td>0.93</td><td></td><td>-195.45</td></tr><tr><td></td><td>-3.87</td><td>643.41</td><td></td><td>12.75</td><td></td></tr><tr><td rowspan="2">9</td><td>20240902</td><td>002149.SZ</td><td>西部材料</td><td>-3.44</td><td></td><td>195.50</td></tr><tr><td></td><td>2.32</td><td>988.69</td><td></td><td>11.71</td><td></td></tr></table></body></html>  

# 板块资金流向（THS）  

接口：moneyflow_ind_ths  

描述：获取同花顺行业板块资金流向，每日盘后更新  

限量：单次最大可调取5000 条数据，可以根据日期和代码循环提取全部数据  

积分：5000 积分可以调取，具体请参阅积分获取办法  

# 输入参数  

<html><body><table><tr><td>名称</td><td>类型</td><td>必选</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td>N</td><td>代码</td></tr><tr><td>trade_date</td><td>str</td><td>N</td><td>交易日期(YYYYMMDD 格式，下同)</td></tr><tr><td>start_date</td><td>str</td><td>N</td><td>开始日期</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>必选</td><td>描述</td></tr><tr><td>end_date</td><td>str</td><td>N</td><td>结束日期</td></tr></table></body></html>  

输出参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>trade_date</td><td>str</td><td>Y</td><td>交易日期</td></tr><tr><td>ts_code</td><td>str</td><td>Y</td><td>板块代码</td></tr><tr><td>industry</td><td>str</td><td>Y</td><td>板块名称</td></tr><tr><td>lead_stock</td><td>str</td><td>Y</td><td>领涨股票名称</td></tr><tr><td>close</td><td>float</td><td>Y</td><td>收盘指数</td></tr><tr><td>pct_change</td><td>float</td><td>Y</td><td>指数涨跌幅</td></tr><tr><td>company_num</td><td>int</td><td>Y</td><td>公司数量</td></tr><tr><td>pct_change_stock</td><td>float</td><td>Y</td><td>领涨股涨跌幅</td></tr><tr><td>close_price</td><td>float</td><td>Y</td><td>领涨股最新价</td></tr><tr><td>net_buy_amount</td><td>float</td><td>Y</td><td>流入资金(亿元</td></tr><tr><td>net_sell_amount</td><td>float</td><td>Y</td><td>流出资金(亿元</td></tr><tr><td>net_amount</td><td>float</td><td>Y</td><td>净额(元)</td></tr></table></body></html>  

# 接口示例  

#获取当日所有板块资金流向df $=$ pro.moneyflow_ind_ths(trade_date $=$ '20240927')  

# 数据示例  

trade_date ts_code industry close company_num net_buy_a mount net_sell_amount net_amount  

0 20240927 881267.TI 能源金属 15021.70 16 490.00 46.00 3.00   
1 20240927 881273.TI 白酒 3251.85 20   
1890.00 179.00 10.00   
2 20240927 881279.TI 光伏设备 5940.19 70 1120.00 94.00 17.00   
3 20240927 881157.TI 证券 1407.41 50   
3680.00 319.00 49.00   
4 20240927 877137.TI 软件开发 1375.49 137 2260.00 204.00 22.00   
85 20240927 881148.TI 港口航运 901.87 37 190.00 20.00 -1.00   
86 20240927 881105.TI 煤炭开采加工 2271.57 34 220.00 26.00 -4.00   
87 20240927 881169.TI 贵金属 2141.46 12 240.00 32.00 -8.00   
88 20240927 881149.TI 公路铁路运输 1224.59 31 210.00 29.00 -7.00   
89 20240927 877035.TI 银行 1080.14 84   
1190.00 159.00 -40.00  

[90 rows x 8 columns]  

# 板块资金流向（DC）  

接口：moneyflow_ind_dc  

描述：获取东方财富板块资金流向，每天盘后更新  

限量：单次最大可调取5000 条数据，可以根据日期和代码循环提取全部数据  

积分：5000 积分可以调取，具体请参阅积分获取办法  

输入参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>必选</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td>N</td><td>代码</td></tr><tr><td>trade_date</td><td>str</td><td>N</td><td>交易日期（YYYYMMDD格式，下同）</td></tr><tr><td>start_date</td><td>str</td><td>N</td><td>开始日期</td></tr><tr><td>end_date</td><td>str</td><td>N</td><td>结束日期</td></tr></table></body></html>  

# 输出参数  

<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>trade_date</td><td>str</td><td>Y</td><td>交易日期</td></tr><tr><td>ts_code</td><td>str</td><td>Y</td><td>DC 板块代码</td></tr><tr><td>name</td><td>str</td><td>Y</td><td>板块名称</td></tr><tr><td>pct_change</td><td>float</td><td>Y</td><td>板块涨跌幅 （%)</td></tr><tr><td>close</td><td>float</td><td>Y</td><td>板块最新指数</td></tr><tr><td>net_amount</td><td>float</td><td>Y</td><td>今日主力净流入 净额 (元)</td></tr><tr><td>net_amount_rate</td><td>float</td><td>Y</td><td>今日主力净流入净占比%</td></tr><tr><td>buy_elg_amount</td><td>float</td><td>Y</td><td>今日超大单净流入净额（元</td></tr><tr><td>buy_elg_amount_rate</td><td>float</td><td>Y</td><td>今日超大单净流入 净占比%</td></tr><tr><td>buy_lg_amount</td><td>float</td><td>Y</td><td>今日大单净流入 净额 (元)</td></tr><tr><td>buy_lg_amount_rate</td><td>float</td><td>Y</td><td>今日大单净流入 净占比%</td></tr><tr><td>buy_md_amount</td><td>float</td><td>Y</td><td>今日中单净流入 净额 (元)</td></tr><tr><td>buy_md_amount_rate</td><td>float</td><td>Y</td><td>今日中单净流入 净占比%</td></tr><tr><td>buy_sm_amount</td><td>float</td><td>Y</td><td>今日小单净流入 净额 (元)</td></tr><tr><td>buy_sm_amount_rate</td><td>float</td><td>Y</td><td>今日小单净流入净占比%</td></tr><tr><td>buy_sm_amount_stock</td><td>str</td><td>Y</td><td>今日主力净流入最大股</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>rank</td><td>int</td><td>Y</td><td>序号</td></tr></table></body></html>  

# 接口示例  

#获取当日所有板块资金流向  

df $=$ pro.moneyflow_ind_dc(trade_date $=$ '20240927', fields $=$ 'trade_ date,name,pct_change, close, net_amount,net_amount_rate,rank')  

# 数据示例  

trade_date name pct_change close net_amount n et_amount_rate  rank  

0 20240927 互联网服务 6.28 16883.55 3056382208.003.93 1  
1 20240927 证券 8.23  135249.80 2875528704.004.64 2  
2 20240927 软件开发 8.28 721.35 2733378816.003.18 3  
3 20240927 酿酒行业 6.47 49330.63 2568183040.005.24 4  
4 20240927 电池 8.37 731.85 1328346624.003.05 5  
81 20240927 石油行业 2.31 4654.40 -611530368.00-9.39 82  
82 20240927 汽车整车 4.05 1386.22 -629528064.00-2.42 83  
83 20240927 综合行业 3.06 7437.08 -667341600.00-7.28 84  
84 20240927 家电行业 3.95 15815.68 -670035968.00-2.37 85  

# 大盘资金流向（DC）  

接口：moneyflow_mkt_dc  

描述：获取东方财富大盘资金流向数据，每日盘后更新  

限量：单次最大3000 条，可根据日期或日期区间循环获取  

积分：120 积分可试用，5000 积分可正式调取，具体请参阅积分获取办法  

\*\*输入参数\*\*   


<html><body><table><tr><td>名称</td><td>类型</td><td>必选</td><td>描述</td></tr><tr><td>trade_date</td><td>str</td><td>N</td><td>交易日期(YYYYMMDD格式，下同)</td></tr><tr><td>start_date</td><td>str</td><td>N</td><td>开始日期</td></tr><tr><td>end_date</td><td>str</td><td>N</td><td>结束日期</td></tr></table></body></html>  

# 输出参数  

<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>trade_date</td><td>str</td><td>Y</td><td>交易日期</td></tr><tr><td>close_sh</td><td>float</td><td>Y</td><td>上证收盘价 (点)</td></tr><tr><td>pct_change_sh</td><td>float</td><td>Y</td><td>上证涨跌幅(%)</td></tr><tr><td>close_sz</td><td>float</td><td>Y</td><td>深证收盘价 (点)</td></tr><tr><td>pct_change_sz</td><td>float</td><td>Y</td><td>深证涨跌幅(%)</td></tr><tr><td>net_amount</td><td>float</td><td>Y</td><td>今日主力净流入 净额 (元)</td></tr><tr><td>net_amount_rate</td><td>float</td><td>Y</td><td>今日主力净流入净占比%</td></tr><tr><td>buy_elg_amount</td><td>float</td><td>Y</td><td>今日超大单净流入净额（元</td></tr><tr><td>buy_elg_amount_rate</td><td>float</td><td>Y</td><td>今日超大单净流入 净占比%</td></tr><tr><td>buy_lg-amount</td><td>float</td><td>Y</td><td>今日大单净流入 净额 (元)</td></tr><tr><td>buy_lg_amount_rate</td><td>float</td><td>Y</td><td>今日大单净流入 净占比%</td></tr><tr><td>buy_md_amount</td><td>float</td><td>Y</td><td>今日中单净流入 净额 (元)</td></tr><tr><td>buy_md_amount_rate</td><td>float</td><td>Y</td><td>今日中单净流入 净占比%</td></tr><tr><td>buy_sm_amount</td><td>float</td><td>Y</td><td>今日小单净流入 净额 (元)</td></tr><tr><td>buy_sm_amount_rate</td><td>float</td><td>Y</td><td>今日小单净流入净占比%</td></tr></table></body></html>  

# 接口示例  

#获取当日所有板块资金流向  

df $=$ pro.moneyflow_mkt_dc(start_date $=$ '20240901', end_date $=$ '2024 0930')  

# 数据示例  

trade_date close_sh ptc_change_sh  close_sz pct_change_sz buy_elg_amount buy_lg_amount  

0 20240930 3336.50 8.06 10529.76 10.67 -6   
500884480.00 -29199228928.00   
1 20240927 3087.53 2.89 9514.86 6.71 17   
175101440.00 -3564773376.00   
2 20240926 3000.95 3.61 8916.65 4.44 18   
894807552.00 -2446319616.00   
3 20240925 2896.31 1.16 8537.73 1.21 -4   
010342144.00 -10390331392.00   
4 20240924 2863.13 4.15 8435.70 4.36 22   
524846080.00 5433212928.00   
5 20240923 2748.92 0.44 8083.38 0.10   
926530816.00 -5776028928.00   
6 20240920 2736.81 0.03 8075.14 -0.15 -4   
991644160.00 -6899648256.00   
7 20240919 2736.02 0.69 8087.60 1.19 3   
472006400.00 1882220032.00   
8 20240918 2717.28 0.49 7992.25 0.11 -5   
056087040.00 -7836610048.00   
9 20240913 2704.09 -0.48 7983.55 -0.88 -5   
527845376.00 -9092720640.00   
10 20240912 2717.12 -0.17 8054.24 -0.63 -3   
747197184.00 -5645509632.00   
11 20240911 2721.80 -0.82 8105.38 0.39 -3   
585276416.00 -6461025792.00   
12 20240910 2744.19 0.28 8073.83 0.13 -2   
726709504.00 -3818158336.00   
13 20240909 2736.49 -1.06 8063.27 -0.83 -7   
874987776.00 -8608827904.00   
14 20240906 2765.81 -0.81 8130.77 -1.44 -5   
892936960.00 -13908542976.00   
15 20240905 2788.31 0.14 8249.66 0.28 1   
211718400.00 -3910650112.00   
16 20240904 2784.28 -0.67 8226.24 -0.51 -7   
008298240.00 -11212970496.00   
17 20240903 2802.98 -0.29 8268.05 1.17   
263304192.00 -3680828928.00   
18 20240902 2811.04 -1.10 8172.21 -2.11 -18   
689678336.00 -20967354368.00  

# 开盘啦题材库  

# 接口：kpl_concept  

描述：获取开盘啦概念题材列表，每天盘后更新  

限量：单次最大5000 条，可根据日期循环获取历史数据  

积分：5000 积分可提取数据，具体请参阅积分获取办法  

输入参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>必选</td><td>描述</td></tr><tr><td>trade_date</td><td>str</td><td>N</td><td>交易日期 月（YYYYMMDD格式）</td></tr><tr><td>ts_code</td><td>str</td><td>N</td><td>题材代码 （xXxxxx.KP格式）</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>必选</td><td>描述</td></tr><tr><td>name</td><td>str</td><td>N</td><td>题材名称</td></tr></table></body></html>  

输出参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>trade_date</td><td>str</td><td>Y</td><td>交易日期</td></tr><tr><td>ts_code</td><td>str</td><td>Y</td><td>题材代码</td></tr><tr><td>name</td><td>str</td><td>Y</td><td>题材名称</td></tr><tr><td>z_t_num</td><td>None</td><td>Y</td><td>涨停数量</td></tr><tr><td>up_num</td><td>str</td><td>Y</td><td>排名上升位数</td></tr></table></body></html>  

# 接口用法  

pro $=$ ts.pro_api()  

df $=$ pro.kpl_concept(trade_date $=$ '20241014')  

# 数据样例  

trade_date ts_code name z_t_num up_num 0 20241014 000111.KP 化债概念 15 0  

1 20241014 000262.KP 跨境支付 2 0   
2 20241014 000039.KP 华为鸿蒙 8 0   
3 20241014 000259.KP 墨脱水电概念 3 68   
4 20241014 000276.KP 神经网络概念 1 0   
160 20241014 000267.KP 乙游概念 0 0   
161 20241014 000203.KP 碳纤维 0 0   
162 20241014 000167.KP 冷锻工艺概念 0 0   
163 20241014 000059.KP 一体化压铸 0 0   
164 20241014 000266.KP 集换式卡牌概念 0 0  

# 开盘啦题材成分  

接口：kpl_concept_cons  

描述：获取开盘啦概念题材的成分股  

限量：单次最大3000 条，可根据代码和日期循环获取全部数据  

积分：5000 积分可提取数据，具体请参阅积分获取办法  

输入参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>必选</td><td>描述</td></tr><tr><td>trade_date</td><td>str</td><td>N</td><td>交易日期（YYYYMMDD格式）</td></tr><tr><td>ts_code</td><td>str</td><td>N</td><td>题材代码 马（xXXxXx.KP格式）</td></tr><tr><td>con_code</td><td>str</td><td>N</td><td>成分代码 （xXXXXX.SH格式）</td></tr></table></body></html>  

输出参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td></td><td>题材ID</td></tr><tr><td>name</td><td>str</td><td>Y</td><td>题材名称</td></tr><tr><td>con_name</td><td>str</td><td>Y</td><td>股票名称</td></tr><tr><td>con_code</td><td>str</td><td>Y</td><td>股票代码</td></tr><tr><td>trade_date</td><td>str</td><td>Y</td><td>交易日其</td></tr><tr><td>desc</td><td>str</td><td>Y</td><td>描述</td></tr><tr><td>hot_num</td><td>None</td><td></td><td>人气值</td></tr></table></body></html>  

# 接口用法  

pro $=$ ts.pro_api() df $=$ pro.kpl_concept_cons(trade_date $=$ '20241014')  

# 数据样例  

ts_code name ts_name con_code trade_date 0 000111.KP 化债概念 信达地产 600657.SH 20241014  

1 000111.KP 化债概念 银宝山新 002786.SZ 20241014   
2 000111.KP 化债概念 摩恩电气 002451.SZ 20241014   
3 000111.KP 化债概念 光大嘉宝 600622.SH 20241014   
4 000111.KP 化债概念 海德股份 000567.SZ 20241014   
..   
2995 000229.KP 电力 特变电工 600089.SH 20241014   
2996 000229.KP 电力 中国西电 601179.SH 20241014   
2997 000229.KP 电力 金盘科技 688676.SH 20241014   
2998 000229.KP 电力 思源电气 002028.SZ 20241014   
2999 000229.KP 电力 明阳电气 301291.SZ 20241014  

# 开盘啦榜单数据  

# 接口：kpl_list  

描述：获取开盘啦涨停、跌停、炸板等榜单数据  

限量：单次最大8000 条数据，可根据日期循环获取历史数据  

积分：5000 积分每分钟可以请求200 次每天总量1 万次，8000 积分以  

上每分钟500 次每天总量不限制，具体请参阅积分获取办法  

输入参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>必选</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td>N</td><td>股票代码</td></tr><tr><td>trade_date</td><td>str</td><td>N</td><td>交易日期</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>必选</td><td>描述</td></tr><tr><td>tag</td><td>str</td><td>N</td><td>板单类型 (涨停/炸板/跌停/自然涨停/竞价)</td></tr><tr><td>start_date</td><td>str</td><td>N</td><td>开始日期</td></tr><tr><td>end_date</td><td>str</td><td>N</td><td>结束日期</td></tr></table></body></html>  

输出参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td>Y</td><td>代码</td></tr><tr><td>name</td><td>str</td><td>Y</td><td>名称</td></tr><tr><td>trade_date</td><td>str</td><td>Y</td><td>交易时间</td></tr><tr><td>lu_time</td><td>str</td><td>Y</td><td>涨停时间</td></tr><tr><td>Id_time</td><td>str</td><td>Y</td><td>跌停时间</td></tr><tr><td>open_time</td><td>str</td><td>Y</td><td>开板时间</td></tr><tr><td>last_time</td><td>str</td><td>Y</td><td>最后涨停时间</td></tr><tr><td>lu_desc</td><td>str</td><td>Y</td><td>涨停原因</td></tr><tr><td>tag</td><td>str</td><td>Y</td><td>标签</td></tr><tr><td>theme</td><td>str</td><td>Y</td><td>板块</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>net_change</td><td>float</td><td>Y</td><td>主力净额(元)</td></tr><tr><td>bid_amount</td><td>float</td><td>Y</td><td>竞价成交额(元)</td></tr><tr><td>status</td><td>str</td><td>Y</td><td>状态 (N连板)</td></tr><tr><td>bid_change</td><td>float</td><td>Y</td><td>竞价净额</td></tr><tr><td>bid_turnover</td><td>float</td><td>Y</td><td>竞价换手%</td></tr><tr><td>lu_bid_vol</td><td>float</td><td>Y</td><td>涨停委买额</td></tr><tr><td>pct_chg</td><td>float</td><td>Y</td><td>涨跌幅%</td></tr><tr><td>bid_pct_chg</td><td>float</td><td>Y</td><td>竞价涨幅%</td></tr><tr><td>rt_pct_chg</td><td>float</td><td>Y</td><td>实时涨幅%</td></tr><tr><td>limit_order</td><td>float</td><td>Y</td><td>封单</td></tr><tr><td>amount</td><td>float</td><td>Y</td><td>成交额</td></tr><tr><td>turnover_rate</td><td>float</td><td>Y</td><td>换手率%</td></tr><tr><td>free_float</td><td>float</td><td>Y</td><td>实际流通</td></tr><tr><td>lu_limit_order</td><td>float</td><td>Y</td><td>最大封单</td></tr></table></body></html>  

# 接口用法  

pro $=$ ts.pro_api()  

df $=$ pro.kpl_list(trade_date $=$ '20240927', tag='涨停', fields $=$ 'ts _code,name,trade_date,tag,theme,status')  

# 数据样例  

<html><body><table><tr><td>tus</td><td>ts_code</td><td>name</td><td>trade_date tag</td><td></td><td>theme</td><td>sta</td></tr><tr><td>0</td><td>000762.SZ</td><td>西藏矿业</td><td>20240927</td><td>涨停</td><td>锂矿、盐湖提锂</td><td></td></tr><tr><td>首板 1</td><td>300399.SZ</td><td>天利科技</td><td>20240927</td><td>涨停</td><td>互联网金融、金融概念</td><td></td></tr><tr><td>2</td><td>首板 002673.SZ</td><td>西部证券</td><td>20240927</td><td>涨停</td><td>证券、控参股基金</td><td></td></tr><tr><td>首板 3</td><td>002050.SZ</td><td>三花智控</td><td>20240927</td><td>涨停</td><td>汽车热管理、比亚迪产业链</td><td></td></tr><tr><td>4</td><td>首板 600801.SH</td><td>华新水泥</td><td>20240927</td><td>涨停</td><td>水泥、地产链</td><td></td></tr><tr><td>首板</td><td></td><td></td><td></td><td></td><td></td><td></td></tr><tr><td>126</td><td>600696.SH</td><td>岩石股份</td><td>20240927</td><td>涨停</td><td>白酒、酿酒</td><td>2</td></tr><tr><td>连板</td><td></td><td></td><td></td><td></td><td></td><td></td></tr><tr><td>127 连板</td><td>600606.SH</td><td>绿地控股</td><td>20240927</td><td>涨停</td><td>房地产、地产链</td><td>2</td></tr><tr><td>128 2连板</td><td>000882.SZ</td><td>华联股份</td><td>20240927</td><td>涨停</td><td>零售、互联网金融</td><td></td></tr><tr><td>129 连板 130 首板</td><td>000069.SZ 002570.SZ</td><td>华侨城A 贝因美</td><td>20240927 20240927</td><td>涨停 涨停</td><td>房地产、地产链 多胎概念、乳业</td><td>2</td></tr></table></body></html>  

# 龙虎榜每日明细  

接口：top_list  

描述：龙虎榜每日交易明细  

数据历史： 2005 年至今  

限量：单次请求返回最大10000 行数据，可通过参数循环获取全部历史  

积分：用户需要至少2000 积分才可以调取，具体请参阅积分获取办法  

输入参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>必选</td><td>描述</td></tr><tr><td>trade_date</td><td>str</td><td>Y</td><td>交易日期</td></tr><tr><td>ts_code</td><td>str</td><td>N</td><td>股票代码</td></tr></table></body></html>  

输出参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>trade_date</td><td>str</td><td>Y</td><td>交易日期</td></tr><tr><td>ts_code</td><td>str</td><td>Y</td><td>TS代码</td></tr><tr><td>name</td><td>str</td><td>Y</td><td>名称</td></tr><tr><td>close</td><td>float</td><td>Y</td><td>收盘价</td></tr><tr><td>pct_change</td><td>float</td><td></td><td>涨跌幅</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>turnover_rate</td><td>float</td><td>Y</td><td>换手率</td></tr><tr><td>amount</td><td>float</td><td>Y</td><td>总成交额</td></tr><tr><td>I_sell</td><td>float</td><td>Y</td><td>龙虎榜卖出额</td></tr><tr><td>I_buy</td><td>float</td><td>Y</td><td>龙虎榜买入额</td></tr><tr><td>I_amount</td><td>float</td><td>Y</td><td>龙虎榜成交额</td></tr><tr><td>net_amount</td><td>float</td><td>Y</td><td>龙虎榜净买入额</td></tr><tr><td>net_rate</td><td>float</td><td>Y</td><td>龙虎榜净买额占比</td></tr><tr><td>amount_rate</td><td>float</td><td>Y</td><td>龙虎榜成交额占比</td></tr><tr><td>float_values</td><td>float</td><td>Y</td><td>当日流通市值</td></tr><tr><td>reason</td><td>str</td><td>Y</td><td>上榜理由</td></tr></table></body></html>  

# 接口用户  

pro $=$ ts.pro_api()  

df $=$ pro.top_list(trade_date $=$ '20180928')  

# 数据样例  

trade_date ts_code name close pct_change turnover_ra  
te \  
0 20180928  000007.SZ 全新好 7.830 -10.0000  
0.24  
1 20180928 000017.SZ 深中华A 4.660 9.9057  
7.44  
2 20180928 000505.SZ 京粮控股 5.750 9.9426  
3.61  
3 20180928 000566.SZ 海南海药 6.120 10.0719  
2.51  
4 20180928 000593.SZ 大通燃气 7.990 -8.0552 1  
3.37  
5 20180928 000971.SZ 高升控股 3.990 -9.9323  
0.94  
6 20180928 002219.SZ 恒康医疗 4.360 10.1010  
7.11  
7 20180928 002219.SZ 恒康医疗 4.360 10.1010  
7.11  
8 20180928 002333.SZ 罗普斯金 9.500 -9.9526  
0.24  
9 20180928 002445.SZ 中南文化 3.140 -6.5476 1  
1.66  
10 20180928 002813.SZ 路畅科技 25.500 10.0086 1  
8.48  
11 20180928 002892.SZ 科力尔 29.970 2.8130 2  
5.67  
12 20180928 002917.SZ 金奥博 29.120 6.1611 2  
8.33  
13 20180928 002923.SZ 润都股份 26.700 0.0000 2  
5.56  
14 20180928 002930.SZ 宏川智慧 30.990 10.0106 1  
2.22  
15 20180928 002931.SZ  锋龙股份 35.310 10.0000 2  
0.39  

amount l_sell l_buy l_amount net_a mount  

0 13736952.0  1.373695e+07  9.071055e+06  2.280801e+07 -4.66   
5897e+06   
1 101054192.0  7.329639e+06  2.836120e+07  3.569084e+07  2.10   
3156e+07   
2 74555564.0  8.547019e+06  2.143432e+07  2.998134e+07  1.288   
731e+07   
3 165464131.0  2.555165e+07  2.192522e+07  4.747687e+07 -3.62   
6437e+06   
4 307769383.0  4.250203e+07  1.169383e+07  5.419587e+07 -3.08   
0820e+07   
5 22255422.0  5.998390e+06  3.371550e+06  9.369940e+06 -2.62   
6840e+06   
6 550236631.0  4.180139e+07  3.942085e+07  8.122223e+07 -2.38   
0538e+06   
7 800737935.0  6.724486e+07  5.763500e+07  1.248799e+08 -9.60   
9865e+06   
8 10943050.0  1.094305e+07  2.862350e+06  1.380540e+07 -8.08   
0700e+06   
9 477766761.0  3.059160e+07  7.482957e+07  1.054212e+08  4.42   
3796e+07   
10  138607013.0  1.219620e+07  2.408786e+07  3.628407e+07  1.18   
9166e+07   
11  199046728.0  5.973278e+07  3.066344e+07  9.039623e+07 -2.90   
6934e+07   
12  229118953.0  1.285196e+07  1.632610e+07  2.917805e+07  3.47   
4138e+06   
13  203570158.0  4.148259e+07  2.583138e+07  6.731397e+07 -1.56   
5121e+07   
14  226882184.0  1.456010e+07  6.502630e+07  7.958640e+07  5.04   
6621e+07   
15  151875439.0  2.016411e+07  2.434384e+07  4.450795e+07  4.17   
9725e+06  

net_rate amount_rate float_values  

0 -33.97 166.03 2.419063e+09   
1 20.81 35.32 1.411891e+09   
2 17.29 40.21 2.072708e+09   
3 -2.19 28.69 6.751556e+09   
4 -10.01 17.61 2.235541e+09   
5 -11.80 42.10 2.359132e+09   
6 -0.43 14.76 8.132328e+09   
7 -1.20 15.60 8.132328e+09   
8 -73.84 126.16 4.607212e+09   
9 9.26 22.07 4.078696e+09   
10 8.58 26.18 7.650000e+08   
11 -14.60 45.41 7.892899e+08   
12 1.52 12.73 8.232224e+08   
13 -7.69 33.07 8.010000e+08   
14 22.24 35.08 1.885122e+09   
15 2.75 29.31 7.845882e+08  

# reason  

0 日跌幅偏离值达到7%的前五只证券  
1 日涨幅偏离值达到7%的前五只证券  
2 日涨幅偏离值达到7%的前五只证券  
3 日涨幅偏离值达到7%的前五只证券  
4 日跌幅偏离值达到7%的前五只证券  
5 日跌幅偏离值达到7%的前五只证券  
6 日涨幅偏离值达到7%的前五只证券  
7 连续三个交易日内，涨幅偏离值累计达到20%的证券  
8 日跌幅偏离值达到7%的前五只证券  
9 日跌幅偏离值达到7%的前五只证券  
10 日涨幅偏离值达到7%的前五只证券  
11 日换手率达到20%的前五只证券  
12 日换手率达到20%的前五只证券  
13 日换手率达到20%的前五只证券  
14 日涨幅偏离值达到7%的前五只证券  
15 日涨幅偏离值达到7%的前五只证券  

# 涨跌停榜单（同花顺）  

# 接口：limit_list_ths  

描述：获取同花顺每日涨跌停榜单数据，历史数据从20231101 开始提供，增量每天16 点左右更新  

限量：单次最大4000 条，可根据日期或股票代码循环提取  

积分：8000 积分以上每分钟500 次，每天总量不限制，具体请参阅积分  

# 获取办法  

输入参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>必选</td><td>描述</td></tr><tr><td>trade_date</td><td>str</td><td>N</td><td>交易日期</td></tr><tr><td>ts_code</td><td>str</td><td>N</td><td>股票代码</td></tr><tr><td>limit_type</td><td>str</td><td>N</td><td>涨停池、连扳池、冲刺涨停、炸板池、跌停池，默认：涨停氵</td></tr><tr><td>market</td><td>str</td><td>N</td><td>HS-沪深主板GEM-创业板STAR-科创板</td></tr><tr><td>start_date</td><td>str</td><td>N</td><td>开始日期</td></tr><tr><td>end_date</td><td>str</td><td>N</td><td>结束日期</td></tr></table></body></html>  

输出参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>trade_date</td><td>str</td><td>Y</td><td>交易日期</td></tr><tr><td>ts_code</td><td>str</td><td>V</td><td>股票代码</td></tr><tr><td>name</td><td>str</td><td>Y</td><td>股票名称</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>price</td><td>float</td><td>Y</td><td>收盘价(元)</td></tr><tr><td>pct_chg</td><td>float</td><td>Y</td><td>涨跌幅%</td></tr><tr><td>open_num</td><td>int</td><td>Y</td><td>打开次数</td></tr><tr><td>lu_desc</td><td>str</td><td>Y</td><td>涨停原因</td></tr><tr><td>limit_type</td><td>str</td><td>Y</td><td>板单类别</td></tr><tr><td>tag</td><td>str</td><td>Y</td><td>涨停标签</td></tr><tr><td>status</td><td>str</td><td>Y</td><td>涨停状态（N连板、一字板)</td></tr><tr><td>first_lu_time</td><td>str</td><td>N</td><td>首次涨停时间</td></tr><tr><td>last_lu_time</td><td>str</td><td>N</td><td>最后涨停时间</td></tr><tr><td>first_ld_time</td><td>str</td><td>N</td><td>首次跌停时间</td></tr><tr><td>last_ld_time</td><td>str</td><td>N</td><td>最后涨停时间</td></tr><tr><td>limit_order</td><td>float</td><td>Y</td><td>封单量(元</td></tr><tr><td>limit_amount</td><td>float</td><td>Y</td><td>封单额(元</td></tr><tr><td>turnover_rate</td><td>float</td><td>Y</td><td>换手率%</td></tr><tr><td>free_float</td><td>float</td><td>Y</td><td>实际流通(元</td></tr><tr><td>lu_limit_order</td><td>float</td><td>Y</td><td>最大封单(元</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>limit_up_suc_rate</td><td>float</td><td>Y</td><td>近一年涨停封板率</td></tr><tr><td>turnover</td><td>float</td><td>Y</td><td>成交额</td></tr><tr><td>rise_rate</td><td>float</td><td>N</td><td>涨速</td></tr><tr><td>sum_float</td><td>float</td><td>N</td><td>总市值 （亿元）</td></tr><tr><td>market_type</td><td>str</td><td>Y</td><td>股票类型：HS 沪深主板、GEM 创业板、STAR</td></tr></table></body></html>  

# 接口用法  

pro $=$ ts.pro_api()  

df $=$ pro.limit_list_ths(trade_date $=$ '20241125', limit_type $=$ '涨停 池', fields $=$ 'ts_code,trade_date,tag,status,lu_desc')  

# 数据样例  

trade_date ts_code lu_desc tagstatus0 20241125 603518.SH 服装家纺 $^+$ 电商 首板 换手板1 20241125 003036.SZ 高端纺织机械设备 $^{+}$ 近年来收购了2 家公司 4天4 板 T 字板2 20241125 301268.SZ 精密结构件 $^{+}$ 华为 $^{\downarrow}$ 光伏 $^+$ 一体化压铸 首板 换手板3 20241125 603655.SH 橡胶 $^+$ 汽车零部件 $^+$ 间接供货特斯拉  2 天2板 换手板4 20241125 600119.SH 上海国资 $^+.$ 产业投资 $^+$ 物流 $^+$ 跨境电商  4 天2 板 换手板  

149 20241125 002348.SZ 固态电池 $^+$ 玩具 $^+$ 互联网教育  4 天2 板一字板  
150 20241125 002175.SZ “东方系”+芯片 $^+$ 智能制造 $^+$ 物业管理  4 天4  
板 一字板  
151 20241125 002155.SZ 湖南万古金矿田探矿获重大突破  3 天3  
板 一字板  
152 20241125 002117.SZ 智能机器人 $^{+}$ 拟向子公司增资 $+\mathsf{A I}$ 应用  2 天  
2 板 一字板  
153 20241125 002103.SZ IP 产品 $^+.$ 广告营销 $^+$ 跨境电商  7 天5 板一字板  

# 涨跌停列表（新）  

接口：limit_list_d  

描述：获取沪深A 股每日涨跌停、炸板数据情况，数据从2020 年开始（不提供ST 股票的统计）  

限量：单次最大可以获取1000 条数据，可通过日期或者股票循环提取积分：5000 积分每分钟可以请求200 次每天总量1 万次，8000 积分以上每分钟500 次每天总量不限制，具体请参阅积分获取办法  

输入参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>必选</td><td>描述</td></tr><tr><td>trade_date</td><td>str</td><td>N</td><td>交易日期</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>必选</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td>N</td><td>股票代码</td></tr><tr><td>limit_type</td><td>str</td><td>N</td><td>涨跌停类型（U 涨停 D 跌停 Z炸板)</td></tr><tr><td>exchange</td><td>str</td><td>N</td><td>交易所（SH上交所 SZ深交所 BJ北交所)</td></tr><tr><td>start_date</td><td>str</td><td>N</td><td>开始日期</td></tr><tr><td>end_date</td><td>str</td><td>N</td><td>结束日期</td></tr></table></body></html>  

输出参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>trade_date</td><td>str</td><td>Y</td><td>交易日期</td></tr><tr><td>ts_code</td><td>str</td><td>Y</td><td>股票代码</td></tr><tr><td>industry</td><td>str</td><td>Y</td><td>所属行业</td></tr><tr><td>name</td><td>str</td><td>Y</td><td>股票名称</td></tr><tr><td>close</td><td>float</td><td>Y</td><td>收盘价</td></tr><tr><td>pct_chg</td><td>float</td><td>Y</td><td>涨跌幅</td></tr><tr><td>amount</td><td>float</td><td>Y</td><td>成交额</td></tr><tr><td>limit_amount</td><td>float</td><td>Y</td><td>板上成交金额(涨停无此数据)</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>float_mv</td><td>float</td><td>Y</td><td>流通市值</td></tr><tr><td>total_mv</td><td>float</td><td>Y</td><td>总市值</td></tr><tr><td>turnover_ratio</td><td>float</td><td>Y</td><td>换手率</td></tr><tr><td>fd_amount</td><td>float</td><td>Y</td><td>封单金额</td></tr><tr><td>first_time</td><td>str</td><td>Y</td><td>首次封板时间 (跌停无此数据)</td></tr><tr><td>last_time</td><td>str</td><td>Y</td><td>最后封板时间</td></tr><tr><td>open_times</td><td>int</td><td>Y</td><td>炸板次数(跌停为开板次数)</td></tr><tr><td>up_stat</td><td>str</td><td>Y</td><td>涨停统计（N/TT天有N次涨停）</td></tr><tr><td>limit_times</td><td>int</td><td>Y</td><td>连板数</td></tr><tr><td>limit</td><td>str</td><td>Y</td><td>D 跌停U涨停 Z炸板</td></tr></table></body></html>  

# 接口用法  

pro $=$ ts.pro_api()  

df $=$ pro.limit_list_d(trade_date $=$ '20220615', limit_type $^{1=}$ 'U', fi elds $=$ 'ts_code,trade_date,industry,name,close,pct_chg,open_time s,up_stat,limit_times')  

# 数据样例  

trade_date ts_code industry name close pct_chg ope  
n_times up_stat  limit_times  
0 20220615  000017.SZ 交运设备 深中华A 3.65 9.940 1/1 1  
1 20220615 000025.SZ 汽车服务 特  力Ａ 29.54 10.025 12/23 1  
2 20220615 000498.SZ 工程建设 山东路桥 10.41 10.043 1/1 1  
3 20220615 000502.SZ 房地产服 绿景退 0.69 9.522 3/3 3  
4 20220615 000532.SZ 综合行业 华金资本 12.69 9.970 1/1 1  
56 20220615 603633.SH 消费电子 徕木股份 14.58 10.043 2/4 1  
57 20220615 603668.SH 农牧饲渔 天马科技 18.22 10.020 2/2 2  
58 20220615 603918.SH 互联网服 金桥信息 9.49 9.976 1/1 1  
59 20220615 603963.SH 中药 大理药业  14.78 9.971 1/1 1  
60 20220615 605068.SH 汽车零部 明新旭腾  29.03 10.001 2/2 2  

# 连板天梯  

# 接口：limit_step  

描述：获取每天连板个数晋级的股票，可以分析出每天连续涨停进阶个数，判断强势热度  

限量：单次最大2000 行数据，可根据股票代码或者日期循环提取全部  

积分：8000 积分以上每分钟500 次，每天总量不限制，具体请参阅积分  

# 获取办法  

输入参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>必选</td><td>描述</td></tr><tr><td>trade_date</td><td>str</td><td>N</td><td>交易日期（格式：YYYYMMDD，下同)</td></tr><tr><td>ts_code</td><td>str</td><td>N</td><td>股票代码</td></tr><tr><td>start_date</td><td>str</td><td>N</td><td>开始日期</td></tr><tr><td>end_date</td><td>str</td><td>N</td><td>结束日期</td></tr><tr><td>nums</td><td>str</td><td>N</td><td>连板次数，支持多个输入，例如 nums='2,3</td></tr></table></body></html>  

输出参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td></td><td>代码</td></tr><tr><td>name</td><td>str</td><td></td><td>名称</td></tr><tr><td>trade_date</td><td>str</td><td></td><td>交易日期</td></tr><tr><td>nums</td><td>str</td><td>Y</td><td>连板次数</td></tr></table></body></html>  

# 接口用法  

pro $=$ ts.pro_api()  

df $=$ pro.limit_step(trade_date $=$ '20241125')  

# 数据样例  

ts_code name trade_date nums  
0 000833.SZ 粤桂股份 20241125 11  
1 002611.SZ 东方精工 20241125 8  
2 600800.SH 渤海化学 20241125 7  
3 000801.SZ 四川九洲 20241125 6  
4 600889.SH 南京化纤 20241125 6  
5 000615.SZ ST 美谷 20241125 5  
6 001229.SZ 魅视科技 20241125 5  
7 002095.SZ 生意宝 20241125 5  
8 002403.SZ 爱仕达 20241125 5  
9 600470.SH 六国化工 20241125 5  
10 603015.SH 弘讯科技 20241125 5  
11 603527.SH 众源新材 20241125 5  
12 002103.SZ 广博股份 20241125 4  
13 002175.SZ 东方智造 20241125 4  
14 002467.SZ 二六三 20241125 4  
15 002741.SZ 光华科技 20241125 4  
16 002862.SZ 实丰文化 20241125 4  
17 003036.SZ 泰坦股份 20241125 4  
18 603377.SH ST 东时 20241125 4  
19 000573.SZ 粤宏远A 20241125 3  
20 002155.SZ 湖南黄金 20241125 3  
21 300822.SZ 贝仕达克 20241125 3  
22 600105.SH 永鼎股份 20241125 3  
23 600405.SH 动力源 20241125 3  
24 600410.SH 华胜天成 20241125 3  
25 600979.SH 广安爱众 20241125 3  
26 000548.SZ 湖南投资 20241125 2  
27 000695.SZ 滨海能源 20241125 2  
28 000803.SZ 山高环能 20241125 2  
29 002045.SZ 国光电器 20241125 2  
30 002054.SZ 德美化工 20241125 2  
31 002117.SZ 东港股份 20241125 2  
32 002638.SZ 勤上股份 20241125 2  
33 002640.SZ 跨境通 20241125 2  
34 002658.SZ 雪迪龙 20241125 2  
35 002820.SZ 桂发祥 20241125 2  
36 002877.SZ 智能自控 20241125 2  
37 003005.SZ 竞业达 20241125 2  
38 300220.SZ 金运激光 20241125 2  
39 600228.SH 返利科技 20241125 2  
40 600333.SH 长春燃气 20241125 2  
41 600615.SH 丰华股份 20241125 2  
42 600775.SH 南京熊猫 20241125 2  
43 601133.SH 柏诚股份 20241125 2  
44 603026.SH 石大胜华 20241125 2  
45 603359.SH 东珠生态 20241125 2  
46 603585.SH 苏利股份 20241125 2  
47 603655.SH 朗博科技 20241125 2  
48 603843.SH 正平股份 20241125 2  

# 最强板块统计  

接口：limit_cpt_list  

描述：获取每天涨停股票最多最强的概念板块，可以分析强势板块的轮  

动，判断资金动向  

限量：单次最大2000 行数据，可根据股票代码或者日期循环提取全部积分：8000 积分以上每分钟500 次，每天总量不限制，具体请参阅积分  

输入参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>必选</td><td>描述</td></tr><tr><td>trade_date</td><td>str</td><td>N</td><td>交易日期（格式：YYYYMMDD，下同）</td></tr><tr><td>ts_code</td><td>str</td><td>N</td><td>板块代码</td></tr><tr><td>start_date</td><td>str</td><td>N</td><td>开始日期</td></tr><tr><td>end_date</td><td>str</td><td>N</td><td>结束日期</td></tr></table></body></html>  

输出参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td>Y</td><td>板块代码</td></tr><tr><td>name</td><td>str</td><td>Y</td><td>板块名称</td></tr><tr><td>trade_date</td><td>str</td><td></td><td>交易日期</td></tr><tr><td>days</td><td>int</td><td>Y</td><td>上榜天数</td></tr><tr><td>up_stat</td><td>str</td><td>Y</td><td>连板高度</td></tr><tr><td>cons_nums</td><td>int</td><td>Y</td><td>连板家数</td></tr><tr><td>swnu-dn</td><td>str</td><td></td><td>涨停家数</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>pct_chg</td><td>float</td><td>Y</td><td>涨跌幅%</td></tr><tr><td>rank</td><td>str</td><td>Y</td><td>板块热点排名</td></tr></table></body></html>  

# 接口用法  

pro $=$ ts.pro_api()  

df $=$ pro.limit_cpt_list(trade_date $=$ '20241127')  

# 数据样例  

ts_code name trade_date  days up_stat cons_nums p_nums pct_chg rank  

0 885728.TI 人工智能 20241127 18 9 天7 板 927  2.8608 1  

1 885420.TI 电子商务 20241127 6 9 天7 板 1125  1.8973 2  

2 885806.TI 华为概念 20241127 34  18 天14 板 621  2.4648 3  

3 885418.TI  文化传媒概念 20241127 2 9 天7 板 618  3.5207 4  

4 885976.TI 数字经济 20241127 4 9 天7 板 617  2.8993 5  

5 885788.TI 网络直播 20241127 6 9 天7 板 917  2.5367 6  

6 886019.TI AIGC 概念 20241127 1 9 天7 板 516  4.3615 7  

885756.TI 芯片概念 20241127 1 7 天7 板  
16  2.4840 8  

8 885642.TI 跨境电商 20241127 6 9 天7 板 1016  2.1974 9  

9 885517.TI 机器人概念 20241127 14 6 天6 板16  2.1272 10  

10 885929.TI 专精特新 20241127 8 7 天7 板 416  2.0335 11  
11 885709.TI 虚拟现实 20241127 1 9 天7 板 415  3.4553 12  
12 885934.TI 元宇宙 20241127 1 9 天7 板 414  3.9264 13  
13 885757.TI 区块链 20241127 1  18 天14 板 514  3.1271 14  
14  885413.TI 创投 20241127 3  18 天14 板 714  1.7311 15  
15 885779.TI 腾讯概念 20241127 1 9 天7 板 413  3.3722 16  
16 885876.TI 网红经济 20241127 1 9 天7 板 512  2.9002 17  
17 885494.TI 一带一路 20241127 2 9 天7 板 112  1.3427 18  
18 885950.TI 虚拟数字人 20241127 1 9 天7 板 311  4.1545 19  
19 886013.TI 信创 20241127 2 9 天7 板 611  3.2298 20  

# 同花顺概念和行业指数  

# 接口：ths_index  

描述：获取同花顺板块指数。注：数据版权归属同花顺，如做商业用途，请主动联系同花顺，如需帮助请联系微信：waditu_a限量：本接口需获得5000 积分，单次最大5000，一次可提取全部数据，请勿循环提取。  

# 输入参数  

<html><body><table><tr><td>名称</td><td>类 型</td><td>必 选</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td>N</td><td>指数代码</td></tr><tr><td>exchange</td><td>str</td><td>N</td><td>市场类型A-a 股HK-港股US-美股</td></tr><tr><td>type</td><td>str</td><td>N</td><td>指数类型N-概念指数I-行业指数R-地域指数S-同花顺特色指数ST-同 花顺主题指数BB-同花顺宽基指数</td></tr></table></body></html>  

输出参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td>Y</td><td>代码</td></tr><tr><td>name</td><td>str</td><td>Y</td><td>名称</td></tr><tr><td>count</td><td>int</td><td>Y</td><td>成分个数</td></tr><tr><td>exchange</td><td>str</td><td>Y</td><td>交易所</td></tr><tr><td>list_date</td><td>str</td><td>Y</td><td>上市日期</td></tr><tr><td>type</td><td>str</td><td>Y</td><td>N概念指数S特色指数</td></tr></table></body></html>  

# 接口示例  

pro $=$ ts.pro_api() df $=$ pro.ths_index()  

# 数据样例  

<html><body><table><tr><td rowspan="2"></td><td rowspan="2">ts code name</td><td colspan="5">count exchange list_date type</td></tr><tr><td>参股银行</td><td>126</td><td>A</td><td>20190416</td><td>N</td></tr><tr><td>0 1</td><td>885835.TI 885472.TI</td><td>上海自贸区</td><td>51</td><td>A</td><td>20130813</td><td>N</td></tr><tr><td>2</td><td>885788.TI</td><td>网络直播</td><td>63</td><td>A</td><td>20180312</td><td>N</td></tr><tr><td>3</td><td>885881.TI</td><td>云办公</td><td>29</td><td>A</td><td>20200203</td><td>N</td></tr><tr><td>4</td><td>885785.TI</td><td>小米概念</td><td>91</td><td>A</td><td>20180306</td><td>N</td></tr><tr><td></td><td></td><td></td><td></td><td></td><td></td><td></td></tr><tr><td>266</td><td>885566.TI</td><td>大飞机</td><td>58</td><td>A</td><td>20140519</td><td>N</td></tr><tr><td>267</td><td>885841.TI</td><td>草地贪夜蛾防治</td><td>18</td><td></td><td>A 20190517</td><td></td></tr><tr><td>268</td><td>885760.TI</td><td>装配式建筑</td><td>50</td><td>A</td><td>20170918</td><td>N N</td></tr><tr><td>269</td><td>885909.TI</td><td>辅助生殖</td><td>15</td><td>A</td><td>20201023</td><td>N</td></tr><tr><td>270</td><td>885883.TI</td><td>医疗废物处理</td><td>25</td><td></td><td>A 20200207</td><td>N</td></tr></table></body></html>  

# 同花顺概念板块成分  

# 接口：ths_member  

描述：获取同花顺概念板块成分列表注：数据版权归属同花顺，如做商业用途，请主动联系同花顺。  

限量：用户积累5000 积分可调取，每分钟可调取200 次，可按概念板块代码循环提取所有成分  

输入参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>必选</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td>N</td><td>板块指数代码</td></tr><tr><td>con_code</td><td>str</td><td>N</td><td>股票代码</td></tr></table></body></html>  

输出参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td>Y</td><td>指数代码</td></tr><tr><td>con_code</td><td>str</td><td>Y</td><td>股票代码</td></tr><tr><td>con_name</td><td>str</td><td>Y</td><td>股票名称</td></tr><tr><td>weight</td><td>float</td><td>N</td><td>权重(暂无)</td></tr><tr><td>in_date</td><td>str</td><td>N</td><td>纳入日期(暂无)</td></tr><tr><td>out_date</td><td>str</td><td>N</td><td>剔除日期(暂无)</td></tr><tr><td>is_new</td><td>str</td><td>N</td><td>是否最新Y是N否</td></tr></table></body></html>  

# 接口示例  

pro $=$ ts.pro_api() df $=$ pro.ths_member(ts_code $=$ '885800.TI')  

# 数据样例  

ts_code con_code con_name  
0 885800.TI 000016.SZ 深康佳A  
1 885800.TI 000049.SZ 德赛电池  
2 885800.TI 002008.SZ 大族激光  
3 885800.TI 002036.SZ 联创电子  
4 885800.TI 002055.SZ 得润电子  
87 885800.TI 688127.SH 蓝特光学  
88 885800.TI 688157.SH 松井股份  
89 885800.TI 688286.SH 敏芯股份  
90 885800.TI 688312.SH 燕麦科技  
91 885800.TI 688386.SH 泛亚微透  

[92 rows x 3 columns]  

# 东方财富概念板块  

# 接口：dc_index  

描述：获取东方财富每个交易日的概念板块数据，支持按日期查询限量：单次最大可获取5000 条数据，历史数据可根据日期循环获取权限：用户积累5000 积分可调取，具体请参阅积分获取办法  

输入参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>必选</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td>N</td><td>指数代码（支持多个代码同时输入，用逗号分隔)</td></tr><tr><td>name</td><td>str</td><td>N</td><td>板块名称（例如：人形机器人)</td></tr><tr><td>trade_date</td><td>str</td><td>N</td><td>交易日期（YYYYMMDD格式，下同)</td></tr><tr><td>start_date</td><td>str</td><td>N</td><td>开始日期</td></tr><tr><td>end_date</td><td>str</td><td>N</td><td>结束日期</td></tr></table></body></html>  

输出参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td></td><td>概念代码</td></tr><tr><td>trade_date</td><td>str</td><td></td><td>交易日期</td></tr><tr><td>name</td><td>str</td><td></td><td>概念名称</td></tr><tr><td>leading</td><td>str</td><td>Y</td><td>领涨股票名称</td></tr><tr><td>leading_code</td><td>str</td><td>Y</td><td>领涨股票代码</td></tr><tr><td>pct_change</td><td>float</td><td></td><td>涨跌幅</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>leading_pct</td><td>float</td><td>Y</td><td>领涨股票涨跌幅</td></tr><tr><td>total_mv</td><td>float</td><td>Y</td><td>总市值 (万元)</td></tr><tr><td>turnover_rate</td><td>float</td><td></td><td>换手率</td></tr><tr><td>wnu-dn</td><td>int</td><td>Y</td><td>上涨家数</td></tr><tr><td>down_num</td><td>int</td><td>Y</td><td>下降家数</td></tr></table></body></html>  

# 接口示例  

#获取东方财富2025 年1 月3 日的概念板块列表  
df $=$ pro.dc_index(trade_date $=$ '20250103', fields $=$ 'ts_code,name,t  
urnover_rate,up_num,down_num')  

# 数据示例  

ts_code name turnover_rate up_num down_num  
0 BK1186.DC 首发经济 8.3700 4 31  
1 BK1185.DC 冰雪经济 4.0800 2 32  
2 BK1184.DC 人形机器人 4.0800 2 62  
3 BK1183.DC 谷子经济 4.6300 2 55  
4 BK1182.DC 智谱AI 5.4000 0 33  
453 BK0498.DC AB 股 1.7300 4 67  
454 BK0494.DC 节能环保 2.1600 32 378  
455 BK0493.DC 新能源 1.4800 19 184  
456 BK0492.DC 煤化工 1.7000 16 56  

# 东方财富板块成分  

# 接口：dc_member  

描述：获取东方财富板块每日成分数据，可以根据概念板块代码和交易日期，获取历史成分  

限量：单次最大获取5000 条数据，可以通过日期和代码循环获取  

权限：用户积累5000 积分可调取，具体请参阅积分获取办法  

输入参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>必选</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td>N</td><td>板块指数代码</td></tr><tr><td>con_code</td><td>str</td><td>N</td><td>成分股票代码</td></tr><tr><td>trade_date</td><td>str</td><td>N</td><td>交易日期（YYYYMMDD格式）</td></tr></table></body></html>  

# 输出参数  

<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>trade_date</td><td>str</td><td>Y</td><td>交易日期</td></tr><tr><td>ts_code</td><td>str</td><td>Y</td><td>概念代码</td></tr><tr><td>con_code</td><td>str</td><td>Y</td><td>成分代码</td></tr><tr><td>name</td><td>str</td><td>Y</td><td>成分股名称</td></tr></table></body></html>  

# 接口示例  

#获取东方财富2025 年1 月2 日的人形机器人概念板块成分列表df $=$ pro.dc_index(trade_date='20250102', ts_code $=$ 'BK1184.DC')  

# 数据示例  

trade_date ts_code con_code name  
0 20250102 BK1184.DC 002117.SZ 东港股份  
1 20250102 BK1184.DC 603662.SH 柯力传感  
2 20250102 BK1184.DC 688165.SH 埃夫特-U  
3 20250102 BK1184.DC 300660.SZ 江苏雷利  
4 20250102 BK1184.DC 873593.BJ 鼎智科技  
59 20250102 BK1184.DC 002139.SZ 拓邦股份  
60 20250102 BK1184.DC 301236.SZ 软通动力  
61 20250102 BK1184.DC 601727.SH 上海电气  
62 20250102 BK1184.DC 300432.SZ 富临精工  
63 20250102 BK1184.DC 300843.SZ 胜蓝股份  

# 同花顺热榜  

接口：ths_hot  

描述：获取同花顺App 热榜数据，包括热股、概念板块、ETF、可转债、港美股等等，每日盘中提取4 次，收盘后4 次，最晚22 点提取一次。  

限量：单次最大2000 条，可根据日期等参数循环获取全部数据  

积分：用户积5000 积分可调取使用，积分获取办法请参阅积分获取办法  

# 输入参数  

<html><body><table><tr><td>名称</td><td>类 型</td><td>必 选</td><td>描述</td></tr><tr><td>trade_date</td><td>str</td><td>N</td><td>交易日期</td></tr><tr><td>ts_code</td><td>str</td><td>N</td><td>TS代码</td></tr><tr><td>market</td><td>str</td><td>N</td><td>热榜类型(热股、ETF、可转债、行业板块、概念板块、期货、港股、</td></tr><tr><td>is_new</td><td>str</td><td>N</td><td>是否最新（默认Y，如果为N则为盘中和盘后阶段采集，具体时间可参 段)</td></tr></table></body></html>  

输出参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>trade_date</td><td>str</td><td>Y</td><td>交易日期</td></tr><tr><td>data_type</td><td>str</td><td>Y</td><td>数据类型</td></tr><tr><td>ts_code</td><td>str</td><td>Y</td><td>股票代码</td></tr><tr><td>ts_name</td><td>str</td><td>Y</td><td>股票名称</td></tr><tr><td>rank</td><td>int</td><td>Y</td><td>排行</td></tr><tr><td>pct_change</td><td>float</td><td>Y</td><td>涨跌幅%</td></tr><tr><td>current_price</td><td>float</td><td>Y</td><td>当前价格</td></tr><tr><td>concept</td><td>str</td><td>Y</td><td>标签</td></tr><tr><td>rank_reason</td><td>str</td><td>Y</td><td>上榜解读</td></tr><tr><td>hot</td><td>float</td><td>Y</td><td>热度值</td></tr><tr><td>rank_time</td><td>str</td><td>Y</td><td>排行榜获取时间</td></tr></table></body></html>  

# 接口示例  

df $=$ pro.ths_hot(trade_date $=$ '20240315', market $=$ '热股', fields=' ts_code,ts_name,hot,concept')  

# 数据示例  

ts_code ts_name hot concept 0 300750.SZ 宁德时代 214462.0 ["钠离子电池", "同花顺漂亮1 00"] 1 603580.SH 艾艾精工 185431.0 ["人民币贬值受益", "台湾概 念股"] 2 002085.SZ 万丰奥威 180332.0  ["飞行汽车(eVTOL)", "低空经济 "] 3 600733.SH 北汽蓝谷 156000.0 ["一体化压铸", "华为汽 车"] 4 603259.SH 药明康德 154360.0 ["CRO 概念", "创新药"] 95 300735.SZ 光弘科技 28528.0 ["智能穿戴", "EDR 概念 "] 96 002632.SZ 道明光学 28101.0 ["AI 手机", "消费电子概念 "] 97 601086.SH 国芳集团 28006.0 ["新零售", "网络直播 "] 98 002406.SZ 远东传动 28003.0 ["工业互联网", "智能制 造"] 99 600160.SH 巨化股份 27979.0 ["PVDF 概念", "氟化工概念 "]  

# 东方财富热板  

接口：dc_hot  

描述：获取东方财富App 热榜数据，包括A 股市场、ETF 基金、港股市  

场、美股市场等等，每日盘中提取4 次，收盘后4 次，最晚22 点提取一次。  

限量：单次最大2000 条，可根据日期等参数循环获取全部数据  

积分：用户积8000 积分可调取使用，积分获取办法请参阅积分获取办法  

# 输入参数  

<html><body><table><tr><td>名称</td><td>类 型</td><td>必 选</td><td>描述</td></tr><tr><td>trade_date</td><td>str</td><td>N</td><td>交易日期</td></tr><tr><td>ts_code</td><td>str</td><td>N</td><td>TS代码</td></tr><tr><td>market</td><td>str</td><td>N</td><td>类型(A 股市场、ETF 基金、港股市场、美股市场)</td></tr><tr><td>hot_type</td><td>str</td><td>N</td><td>热点类型(人气榜、飙升榜)</td></tr><tr><td>is_new</td><td>str</td><td>N</td><td>是否最新（默认Y，如果为N则为盘中和盘后阶段采集，具体时间可 段)</td></tr></table></body></html>  

输出参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>trade_date</td><td>str</td><td>Y</td><td>交易日期</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>data_type</td><td>str</td><td></td><td>数据类型</td></tr><tr><td>ts_code</td><td>str</td><td>Y</td><td>股票代码</td></tr><tr><td>ts_name</td><td>str</td><td>Y</td><td>股票名称</td></tr><tr><td>rank</td><td>int</td><td>Y</td><td>排行或者热度</td></tr><tr><td>pct_change</td><td>float</td><td>Y</td><td>涨跌幅%</td></tr><tr><td>current_price</td><td>float</td><td>Y</td><td>当前价</td></tr><tr><td>rank_time</td><td>str</td><td></td><td>排行榜获取时间</td></tr></table></body></html>  

# 接口示例  

#获取查询月份券商金股   
df $=$ pro.dc_hot(trade_date $^{1=}$ '20240315', market='A 股市场',hot_typ   
$\e{=}^{\prime}$ 人气榜',  fields $=$ 'ts_code,ts_name,rank')  

# 数据示例  

ts_code ts_name rank  
0 601099.SH 太平洋 1  
1 601995.SH 中金公司 2  
2 002235.SZ 安妮股份 3  
3 601136.SH 首创证券 4  
4 600127.SH 金健米业 5  
95 300675.SZ 建科院 96  
96 601900.SH 南方传媒 97  
97 600280.SH 中央商场 98  
98 300898.SZ 熊猫乳品 99  
99 600519.SH 贵州茅台 100  

# 指数基本信息  

接口：index_basic，可以通过数据工具调试和查看数据。  

描述：获取指数基础信息。  

输入参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>必选</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td>N</td><td>指数代码</td></tr><tr><td>name</td><td>str</td><td>N</td><td>指数简称</td></tr><tr><td>market</td><td>str</td><td>N</td><td>交易所或服务商(默认 SSE)</td></tr><tr><td>publisher</td><td>str</td><td>N</td><td>发布商</td></tr><tr><td>category</td><td>str</td><td>N</td><td>指数类别</td></tr></table></body></html>  

# 输出参数  

<html><body><table><tr><td>名称</td><td>类型</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td>TS代码</td></tr><tr><td>name</td><td>str</td><td>简称</td></tr><tr><td>fullname</td><td>str</td><td>指数全称</td></tr><tr><td>market</td><td>str</td><td>市场</td></tr><tr><td>publisher</td><td>str</td><td>发布方</td></tr><tr><td>index_type</td><td>str</td><td>指数风格</td></tr><tr><td>category</td><td>str</td><td>指数类别</td></tr><tr><td>base_date</td><td>str</td><td>基期</td></tr><tr><td>base_point</td><td>float</td><td>基点</td></tr><tr><td>list_date</td><td>str</td><td>发布日期</td></tr><tr><td>weight_rule</td><td>str</td><td>加权方式</td></tr><tr><td>desc</td><td>str</td><td>描述</td></tr><tr><td>exp_date 市场说明(market)</td><td>str</td><td>终止日期</td></tr><tr><td colspan="3"></td></tr><tr><td>市场代码</td><td colspan="2">说明</td></tr><tr><td>MSCI</td><td colspan="2">MSCI指数</td></tr></table></body></html>  

<html><body><table><tr><td>市场代码</td><td>说明</td></tr><tr><td>CSI</td><td>中证指数</td></tr><tr><td>SSE</td><td>上交所指数</td></tr><tr><td>SZSE</td><td>深交所指数</td></tr><tr><td>CICC</td><td>中金指数</td></tr><tr><td>SW</td><td>申万指数</td></tr><tr><td>OTH</td><td>其他指数</td></tr></table></body></html>  

# 指数列表  

• 主题指数  
• 规模指数  
• 策略指数  
• 风格指数  
• 综合指数  
• 成长指数  
• 价值指数  
• 有色指数  
• 化工指数  
• 能源指数  
• 其他指数  
• 外汇指数  
• 基金指数  
• 商品指数  
• 债券指数  
• 行业指数  
• 贵金属指数  
• 农副产品指数  
• 软商品指数  
• 油脂油料指数  
• 非金属建材指数  
• 煤焦钢矿指数  
• 谷物指数  

# 接口使用  

pro $=$ ts.pro_api()  

df $=$ pro.index_basic(market $=$ 'SW')  

# 数据样例  

ts_code name market publisher catego  
ry base_date base_point  
5 801010.SI 农林牧渔 SW 申万 一级行业指数  
19991230 1000.0  
6 801011.SI 林业Ⅱ SW 申万 二级行业指数 1  
9991230 1000.0  
7 801012.SI 农产品加工 SW 申万 二级行业指数  
19991230 1000.0  
8 801013.SI 农业综合Ⅱ SW 申万 二级行业指数  
19991230 1000.0  
9 801014.SI 饲料Ⅱ SW 申万 二级行业指数  1  
9991230 1000.0  
10 801015.SI 渔业 SW 申万 二级行业指数  
19991230 1000.0  
11 801016.SI 种植业 SW 申万 二级行业指数  
19991230 1000.0  
12 801017.SI 畜禽养殖Ⅱ SW 申万 二级行业指数  
20111010 1000.0  
13 801018.SI 动物保健Ⅱ SW 申万研 二级行业指数  
19991230 1000.0  
14 801020.SI 采掘 SW 申万 一级行业指数  
19991230 1000.0  
15 801021.SI 煤炭开采Ⅱ SW 申万 二级行业指数  
19991230 1000.0  
16 801022.SI 其他采掘Ⅱ SW 申万 二级行业指数  
19991230 1000.0  
17 801023.SI 石油开采Ⅱ SW 申万 二级行业指数  
19991230 1000.0  

# 指数日线行情  

接口：index_daily，可以通过数据工具调试和查看数据。  

描述：获取指数每日行情，还可以通过bar 接口获取。由于服务器压力，目前规则是单次调取最多取8000 行记录，可以设置start 和end 日期补全。指数行情也可以通过通用行情接口获取数据  

权限：用户累积2000 积分可调取，5000 积分以上频次相对较高。本接口不包括申万行情数据，申万等行业指数行情需5000 积分以上，具体请参阅积分获取办法  

输入参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>必选</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td></td><td>指数代码，来源指数基础信息接口</td></tr><tr><td>trade_date</td><td>str</td><td>N</td><td>交易日期 （日期格式：YYYYMMDD，下同）</td></tr><tr><td>start_date</td><td>str</td><td>N</td><td>开始日期</td></tr><tr><td>end_date</td><td>str</td><td>N</td><td>结束日期</td></tr></table></body></html>  

输出参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td>TS指数代码</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>描述</td></tr><tr><td>trade_date</td><td>str</td><td>交易日</td></tr><tr><td>close</td><td>float</td><td>收盘点位</td></tr><tr><td>open</td><td>float</td><td>开盘点位</td></tr><tr><td>high</td><td>float</td><td>最高点位</td></tr><tr><td>low</td><td>float</td><td>最低点位</td></tr><tr><td>pre_close</td><td>float</td><td>昨日收盘点</td></tr><tr><td>change</td><td>float</td><td>涨跌点</td></tr><tr><td>pct_chg</td><td>float</td><td>涨跌幅（%)</td></tr><tr><td>vol</td><td>float</td><td>成交量 (手)</td></tr><tr><td>amount</td><td>float</td><td>成交额 (千元)</td></tr></table></body></html>  

# 接口使用  

pro $=$ ts.pro_api()  

df $=$ pro.index_daily(ts_code $=$ '399300.SZ')  

#或者按日期取  

df $=$ pro.index_daily(ts_code $=$ '399300.SZ', start_date $^{1=}$ '20180101 ', end_date $=$ '20181010')  

# 数据样例  

ts_code trade_date close open high   
low \   
0 399300.SZ 20180903  3321.8248 3320.6898 3325.6070 329   
1.7842   
1 399300.SZ 20180831 3334.5036  3333.3801 3356.5757 331   
0.8726   
2 399300.SZ 20180830  3351.0942  3385.8052  3402.5626 334   
9.4688   
3 399300.SZ 20180829  3386.5736  3393.0527  3398.7139 337   
7.1231   
4 399300.SZ 20180828 3400.1705  3408.1502 3416.5929 338   
8.8143   
5 399300.SZ 20180827 3406.5735 3339.3894 3406.5735 333   
9.2646   
6 399300.SZ 20180824 3325.3347 3308.4778 3353.0445 329   
1.8654   
7 399300.SZ 20180823 3320.0257 3308.4589 3336.1123 328   
5.8141   
8 399300.SZ 20180822 3307.9545  3328.9693  3328.9693 329   
9.3938   
9 399300.SZ 20180821 3326.6489  3271.8402 3331.7077 327   
0.0302   
10 399300.SZ 20180820  3267.2498  3238.2150  3267.2498 320   
9.0115   
11 399300.SZ 20180817  3229.6198  3305.8954  3311.5729 322   
4.0999   
12 399300.SZ 20180816  3276.7276  3251.8556  3315.2031 323   
1.5561   
13 399300.SZ 20180815 3291.9760  3371.9590 3372.1369 328   
8.7088   
14 399300.SZ 20180814 3372.9137 3386.4832 3391.7290 335   
6.6142   
15 399300.SZ 20180813 3390.3441 3369.9812 3396.1883 333   
6.6956   
16 399300.SZ 20180810 3405.0191  3398.4139 3424.0411 338   
0.5731  

接口：index_weight  

描述：获取各类指数成分和权重，月度数据 ，建议输入参数里开始日期和结束日分别输入当月第一天和最后一天的日期。  

来源：指数公司网站公开数据  

积分：用户需要至少2000 积分才可以调取，具体请参阅积分获取办法  

输入参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>必选</td><td>描述</td></tr><tr><td>index_code</td><td>str</td><td></td><td>指数代码，来源指数基础信息接口</td></tr><tr><td>trade_date</td><td>str</td><td>N</td><td>交易日期（格式YYYYMMDD，下同）</td></tr><tr><td>start_date</td><td>str</td><td>N</td><td>开始日期</td></tr><tr><td>end_date</td><td>None</td><td>N</td><td>结束日期</td></tr></table></body></html>  

输出参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>描述</td></tr><tr><td>index_code</td><td>str</td><td>指数代码</td></tr><tr><td>con_code</td><td>str</td><td>成分代码</td></tr><tr><td>trade_date</td><td>str</td><td>交易日期</td></tr><tr><td>weight</td><td>float</td><td>权重</td></tr></table></body></html>  

# 接口调用  

pro $=$ ts.pro_api()  

#提取沪深300 指数2018 年9 月成分和权重   
df $=$ pro.index_weight(index_code='399300.SZ', start_date $=$ '20180   
901', end_date $=$ '20180930')  

# 数据样例  

index_code con_code trade_date weight   
0 399300.SZ 000001.SZ 20180903 0.8656   
1 399300.SZ 000002.SZ 20180903 1.1330   
2 399300.SZ 000060.SZ 20180903 0.1125   
3 399300.SZ 000063.SZ 20180903 0.4273   
4 399300.SZ 000069.SZ 20180903 0.2010   
5 399300.SZ 000157.SZ 20180903 0.1699   
6 399300.SZ 000402.SZ 20180903 0.0816   
7 399300.SZ 000413.SZ 20180903 0.2023   
8 399300.SZ 000415.SZ 20180903 0.0648   
9 399300.SZ 000423.SZ 20180903 0.2100   
10 399300.SZ 000425.SZ 20180903 0.1884  

# 大盘指数每日指标  

接口：index_dailybasic，可以通过数据工具调试和查看数据。  

描述：目前只提供上证综指，深证成指，上证50，中证500，中小板  

指，创业板指的每日指标数据  

数据来源：Tushare 社区统计计算  

数据历史：从2004 年1 月开始提供  

数据权限：用户需要至少400 积分才可以调取，具体请参阅积分获取办  

法  

# 输入参数  

<html><body><table><tr><td>名称</td><td>类型</td><td>必选</td><td>描述</td></tr><tr><td>trade_date</td><td>str</td><td>N</td><td>交易日期 」（格式：YYYYMMDD，比如20181018，下同）</td></tr><tr><td>ts_code</td><td>str</td><td>N</td><td>TS代码</td></tr><tr><td>start_date</td><td>str</td><td>N</td><td>开始日期</td></tr><tr><td>end_date</td><td>str</td><td>N</td><td>结束日期</td></tr></table></body></html>  

注：trade_date，ts_code 至少要输入一个参数，单次限量3000 条  

（即，单一指数单次可提取超过12 年历史），总量不限制。  

# 输出参数  

<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td>Y</td><td>TS代码</td></tr><tr><td>trade_date</td><td>str</td><td>Y</td><td>交易日期</td></tr><tr><td>total_mv</td><td>float</td><td>Y</td><td>当日总市值 (元)</td></tr><tr><td>float_mv</td><td>float</td><td>Y</td><td>当日流通市值 (元)</td></tr><tr><td>total_share</td><td>float</td><td>Y</td><td>当日总股本 (股)</td></tr><tr><td>float_share</td><td>float</td><td>V</td><td>当日流通股本 (股)</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>free_share</td><td>float</td><td>Y</td><td>当日自由流通股本 (股)</td></tr><tr><td>turnover_rate</td><td>float</td><td>Y</td><td>换手率</td></tr><tr><td>turnover_rate_f</td><td>float</td><td>Y</td><td>换手率(基于自由流通股本)</td></tr><tr><td>pe</td><td>float</td><td>Y</td><td>市盈率</td></tr><tr><td>pe_ttm</td><td>float</td><td>Y</td><td>市盈率TTM</td></tr><tr><td>pb</td><td>float</td><td>Y</td><td>市净率</td></tr></table></body></html>  

# 接口示例  

pro $=$ ts.pro_api()  

df $=$ pro.index_dailybasic(trade_date $=$ '20181018', fields $=$ 'ts_cod e,trade_date,turnover_rate,pe')  

# 数据示例  

ts_code trade_date turnover_rate pe   
0 000001.SH 20181018 0.38 11.92   
1 000300.SH 20181018 0.27 11.17   
2 000905.SH 20181018 0.82 18.03   
3 399001.SZ 20181018 0.88 17.48   
4 399005.SZ 20181018 0.85 21.43   
5 399006.SZ 20181018 1.50 29.56   
6 399016.SZ 20181018 1.06 18.86   
7 399300.SZ 20181018 0.27 11.17  

# 申万行业分类  

接口：index_classify  

描述：获取申万行业分类，可以获取申万2014 年版本（28 个一级分类，104 个二级分类，227 个三级分类）和2021 年本版（31 个一级分类，134 个二级分类，346 个三级分类）列表信息  

权限：用户需2000 积分可以调取，具体请参阅积分获取办法  

# 申万行业指数分类标准2021 版  

注：指数成分股小于5 条该指数行情不发布  

<html><body><table><tr><td>行业代</td><td>指数代</td><td>一级</td><td>二级行业</td><td>三级行业</td><td>指数 类别</td><td>是否 发布</td><td>变动原因</td></tr><tr><td>码 110000</td><td>码 801010</td><td>行业 农林</td><td></td><td></td><td>一级</td><td>1</td><td>2021保留</td></tr><tr><td>110100</td><td>801016</td><td>牧渔 农林</td><td>种植业</td><td></td><td>行业 二级</td><td></td><td>2021保留</td></tr><tr><td></td><td></td><td>牧渔 农林</td><td></td><td></td><td>行业 三级</td><td></td><td></td></tr><tr><td>110101</td><td>850111</td><td>牧渔</td><td>种植业</td><td>种子</td><td>行业</td><td>1</td><td>2021改名</td></tr></table></body></html>  

<html><body><table><tr><td>行业代</td><td>指数代</td><td>一级 行业</td><td rowspan="2">二级行业</td><td rowspan="2">三级行业</td><td rowspan="2">指数 类别</td><td rowspan="2">是否 发布</td><td rowspan="2">变动原因</td></tr><tr><td>码</td><td>码</td><td></td></tr><tr><td>110102</td><td>850112</td><td>农林 牧渔</td><td>种植业</td><td>粮食种植</td><td>三级 行业</td><td>0</td><td>2021保留</td></tr><tr><td>110103</td><td>850113</td><td>农林 牧渔</td><td>种植业</td><td>其他种植业</td><td>三级 行业</td><td></td><td>2021保留</td></tr><tr><td>110104</td><td>850114</td><td>农林 牧渔</td><td>种植业</td><td>食用菌</td><td>三级 行业</td><td>0</td><td>2021新增</td></tr><tr><td>110200</td><td>801015</td><td>农林 牧渔</td><td>渔业</td><td></td><td>二级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>110201</td><td>850121</td><td>农林 牧渔</td><td>渔业</td><td>海洋捕捞</td><td>三级 行业</td><td>0</td><td>2021保留</td></tr><tr><td>110202</td><td>850122</td><td>农林 牧渔</td><td>渔业</td><td>水产养殖</td><td>三级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>110300</td><td>801011</td><td>农林 牧渔</td><td>林业II</td><td></td><td>二级 行业</td><td>0</td><td>2021保留</td></tr><tr><td>110301</td><td>850131</td><td>农林 牧渔</td><td>林业II</td><td>林业川I</td><td>三级 行业</td><td>0</td><td>2021保留</td></tr></table></body></html>  

<html><body><table><tr><td>行业代</td><td>指数代</td><td>一级 行业</td><td rowspan="2">二级行业</td><td rowspan="2">三级行业</td><td rowspan="2">指数 类别</td><td rowspan="2">是否 发布</td><td rowspan="2">变动原因</td></tr><tr><td>码</td><td>码</td><td></td></tr><tr><td>110400</td><td>801014</td><td>农林 牧渔</td><td>饲料</td><td></td><td>二级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>110402</td><td>850142</td><td>农林 牧渔</td><td>饲料</td><td>畜禽饲料</td><td>三级 行业</td><td></td><td>2021新增</td></tr><tr><td>110403</td><td>850143</td><td>农林 牧渔</td><td>饲料</td><td>水产饲料</td><td>三级 行业</td><td>0</td><td>2021新增</td></tr><tr><td>110404</td><td>850144</td><td>农林 牧渔</td><td>饲料</td><td>宠物食品</td><td>三级 行业</td><td>0</td><td>2021新增</td></tr><tr><td>110500</td><td>801012</td><td>农林 牧渔</td><td>农产品加 工</td><td></td><td>二级 行业</td><td></td><td>2021保留</td></tr><tr><td>110501</td><td>850151</td><td>农林 牧渔</td><td>农产品加 工</td><td>果蔬加工</td><td>三级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>110502</td><td>850152</td><td>农林 牧渔</td><td>农产品加 工</td><td>粮油加工</td><td>三级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>110504</td><td>850154</td><td>农林 牧渔</td><td>农产品加 工</td><td>其他农产品加工</td><td>三级 行业</td><td></td><td>2021保留</td></tr></table></body></html>  

<html><body><table><tr><td>行业代</td><td>指数代</td><td>一级 行业</td><td rowspan="2">二级行业</td><td rowspan="2">三级行业</td><td rowspan="2">指数 类别</td><td rowspan="2">是否 发布</td><td rowspan="2">变动原因</td></tr><tr><td>码</td><td>码</td></tr><tr><td>110700</td><td>801017</td><td>农林 牧渔</td><td>养殖业</td><td></td><td>二级 行业</td><td>1</td><td>2021改名</td></tr><tr><td>110702</td><td>850172</td><td>农林 牧渔</td><td>养殖业</td><td>生猪养殖</td><td>三级 行业</td><td></td><td>2021新增</td></tr><tr><td>110703</td><td>850173</td><td>农林 牧渔</td><td>养殖业</td><td>肉鸡养殖</td><td>三级 行业</td><td></td><td>2021新增</td></tr><tr><td>110704</td><td>850174</td><td>农林 牧渔</td><td>养殖业</td><td>其他养殖</td><td>三级 行业</td><td>0</td><td>2021新增</td></tr><tr><td>110800</td><td>801018</td><td>农林 牧渔</td><td>动物保健</td><td></td><td>二级 行业</td><td></td><td>2021保留</td></tr><tr><td>110801</td><td>850181</td><td>农林 牧渔</td><td>动物保健</td><td>动物保健川</td><td>三级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>110900</td><td>801019</td><td>农林 牧渔</td><td>农业综合</td><td></td><td>二级 行业</td><td>0</td><td>2021新增</td></tr><tr><td>110901</td><td>850191</td><td>农林 牧渔</td><td>农业综合</td><td>农业综合川</td><td>三级 行业</td><td>0</td><td>2021新增</td></tr></table></body></html>  

<html><body><table><tr><td>行业代</td><td>指数代</td><td>一级</td><td rowspan="2">二级行业</td><td rowspan="2">三级行业</td><td rowspan="2">指数 类别</td><td rowspan="2">是否 发布</td><td rowspan="2">变动原因</td></tr><tr><td>码</td><td>码</td><td>行业</td></tr><tr><td>220000</td><td>801030</td><td>基础 化工</td><td></td><td></td><td>一级 行业</td><td>1</td><td>2021改名</td></tr><tr><td>220200</td><td>801033</td><td>基础 化工</td><td>化学原料</td><td></td><td>二级 行业</td><td></td><td>2021保留</td></tr><tr><td>220201</td><td>850321</td><td>基础 化工</td><td>化学原料</td><td>纯碱</td><td>三级 行业</td><td>0</td><td>2021保留</td></tr><tr><td>220202</td><td>850322</td><td>基础 化工</td><td>化学原料</td><td>氯碱</td><td>三级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>220203</td><td>850323</td><td>基础 化工</td><td>化学原料</td><td>无机盐</td><td>三级 行业</td><td></td><td>2021保留</td></tr><tr><td>220204</td><td>850324</td><td>基础 化工</td><td>化学原料</td><td>其他化学原料</td><td>三级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>220205</td><td>850325</td><td>基础 化工</td><td>化学原料</td><td>煤化工</td><td>三级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>220206</td><td>850326</td><td>基础 化工</td><td>化学原料</td><td>钛白粉</td><td>三级 行业</td><td></td><td>2021新增</td></tr></table></body></html>  

<html><body><table><tr><td>行业代</td><td>指数代</td><td>一级 行业</td><td rowspan="2">二级行业</td><td rowspan="2">三级行业</td><td rowspan="2">指数 类别</td><td rowspan="2">是否 发布</td><td rowspan="2">变动原因</td></tr><tr><td>码</td><td>码</td><td></td></tr><tr><td>220300</td><td>801034</td><td>基础 化工</td><td>化学制品</td><td></td><td>二级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>220305</td><td>850335</td><td>基础 化工</td><td>化学制品</td><td>涂料油墨</td><td>三级 行业</td><td></td><td>2021改名</td></tr><tr><td>220307</td><td>850337</td><td>基础 化工</td><td>化学制品</td><td>民爆制品</td><td>三级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>220308</td><td>850338</td><td>基础 化工</td><td>化学制品</td><td>纺织化学制品</td><td>三级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>220309</td><td>850339</td><td>基础 化工</td><td>化学制品</td><td>其他化学制品</td><td>三级 行业</td><td></td><td>2021保留</td></tr><tr><td>220311</td><td>850382</td><td>基础 化工</td><td>化学制品</td><td>氟化工</td><td>三级 行业</td><td>1</td><td>2021改名</td></tr><tr><td>220313</td><td>850372</td><td>基础 化工</td><td>化学制品</td><td>聚氨酯</td><td>三级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>220315</td><td>850135</td><td>基础 化工</td><td>化学制品</td><td>食品及饲料添加剂</td><td>三级 行业</td><td></td><td>2021新增</td></tr></table></body></html>  

<html><body><table><tr><td>行业代</td><td>指数代</td><td>一级 行业</td><td rowspan="2">二级行业</td><td rowspan="2">三级行业</td><td rowspan="2">指数 类别</td><td rowspan="2">是否 发布</td><td rowspan="2">变动原因</td></tr><tr><td>码</td><td>码</td></tr><tr><td>220316</td><td>850136</td><td>基础 化工</td><td>化学制品</td><td>有机硅</td><td>三级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>220317</td><td>850137</td><td>基础 化工</td><td>化学制品</td><td>胶黏剂及胶带</td><td>三级 行业</td><td>0</td><td>2021新增</td></tr><tr><td>220400</td><td>801032</td><td>基础 化工</td><td>化学纤维</td><td></td><td>二级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>220401</td><td>850341</td><td>基础 化工</td><td>化学纤维</td><td>涤纶</td><td>三级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>220403</td><td>850343</td><td>基础 化工</td><td>化学纤维</td><td>粘胶</td><td>三级 行业</td><td></td><td>2021保留</td></tr><tr><td>220404</td><td>850344</td><td>基础 化工</td><td>化学纤维</td><td>其他化学纤维</td><td>三级 行业</td><td>0</td><td>2021改名</td></tr><tr><td>220405</td><td>850345</td><td>基础 化工</td><td>化学纤维</td><td>氨纶</td><td>三级 行业</td><td>0</td><td>2021保留</td></tr><tr><td>220406</td><td>850346</td><td>基础 化工</td><td>化学纤维</td><td>锦纶</td><td>三级 行业</td><td>0</td><td>2021新增</td></tr></table></body></html>  

<html><body><table><tr><td>行业代</td><td>指数代</td><td>一级 行业</td><td rowspan="2">二级行业</td><td rowspan="2">三级行业</td><td rowspan="2">指数 类别</td><td rowspan="2">是否 发布</td><td rowspan="2">变动原因</td></tr><tr><td>码</td><td>码</td><td></td></tr><tr><td>220500</td><td>801036</td><td>基础 化工</td><td>塑料</td><td></td><td>二级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>220501</td><td>850351</td><td>基础 化工</td><td>塑料</td><td>其他塑料制品</td><td>三级 行业</td><td></td><td>2021保留</td></tr><tr><td>220503</td><td>850353</td><td>基础 化工</td><td>塑料</td><td>改性塑料</td><td>三级 行业</td><td></td><td>2021保留</td></tr><tr><td>220504</td><td>850354</td><td>基础 化工</td><td>塑料</td><td>合成树脂</td><td>三级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>220505</td><td>850355</td><td>基础 化工</td><td>塑料</td><td>膜材料</td><td>三级 行业</td><td></td><td>2021新增</td></tr><tr><td>220600</td><td>801037</td><td>基础 化工</td><td>橡胶</td><td></td><td>二级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>220602</td><td>850362</td><td>基础 化工</td><td>橡胶</td><td>其他橡胶制品</td><td>三级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>220603</td><td>850363</td><td>基础 化工</td><td>橡胶</td><td>炭黑</td><td>三级 行业</td><td></td><td>2021保留</td></tr></table></body></html>  

<html><body><table><tr><td>行业代</td><td>指数代</td><td>一级 行业</td><td rowspan="2">二级行业</td><td rowspan="2">三级行业</td><td rowspan="2">指数 类别</td><td rowspan="2">是否 发布</td><td rowspan="2">变动原因</td></tr><tr><td>码</td><td>码</td></tr><tr><td>220604</td><td>850364</td><td>基础 化工</td><td>橡胶</td><td>橡胶助剂</td><td>三级 行业</td><td>0</td><td>2021新增</td></tr><tr><td>220800</td><td>801038</td><td>基础 化工</td><td>农化制品</td><td></td><td>二级 行业</td><td></td><td>2021新增</td></tr><tr><td>220801</td><td>850331</td><td>基础 化工</td><td>农化制品</td><td>氮肥</td><td>三级 行业</td><td>1</td><td>2021替换 220301</td></tr><tr><td>220802</td><td>850332</td><td>基础 化工</td><td>农化制品</td><td>磷肥及磷化工</td><td>三级 行业</td><td>1</td><td>2021替换 220302</td></tr><tr><td>220803</td><td>850333</td><td>基础 化工</td><td>农化制品</td><td>农药</td><td>三级 行业</td><td></td><td>2021替换 220303</td></tr><tr><td>220804</td><td>850336</td><td>基础 化工</td><td>农化制品</td><td>钾肥</td><td>三级 行业</td><td>0</td><td>2021替换 220306</td></tr><tr><td>220805</td><td>850381</td><td>基础 化工</td><td>农化制品</td><td>复合肥</td><td>三级 行业</td><td>1</td><td>2021替换 220310</td></tr><tr><td>220900</td><td>801039</td><td>基础 化工</td><td>非金属材 料II</td><td></td><td>二级 行业</td><td></td><td>2021新增</td></tr></table></body></html>  

<html><body><table><tr><td>行业代</td><td>指数代</td><td>一级</td><td rowspan="2">二级行业</td><td rowspan="2">三级行业</td><td rowspan="2">指数 类别</td><td rowspan="2">是否 发布</td><td rowspan="2">变动原因</td></tr><tr><td>码</td><td>码</td><td>行业</td></tr><tr><td>220901</td><td>850523</td><td>基础 化工</td><td>非金属材 料II</td><td>非金属材料II</td><td>三级 行业</td><td>1</td><td>2021替换 240203</td></tr><tr><td>230000</td><td>801040</td><td>钢铁</td><td></td><td></td><td>一级 行业</td><td></td><td>2021保留</td></tr><tr><td>230300</td><td>801043</td><td>钢铁</td><td>治钢原料</td><td></td><td>二级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>230301</td><td>850431</td><td>钢铁</td><td>治钢原料</td><td>铁矿石</td><td>三级 行业</td><td>0</td><td>2021新增</td></tr><tr><td>230302</td><td>850432</td><td>钢铁</td><td>治钢原料</td><td>治钢辅料</td><td>三级 行业</td><td>0</td><td>2021新增</td></tr><tr><td>230400</td><td>801044</td><td>钢铁</td><td>普钢</td><td></td><td>二级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>230401</td><td>850441</td><td>钢铁</td><td>普钢</td><td>长材</td><td>三级 行业</td><td>0</td><td>2021新增</td></tr><tr><td>230402</td><td>850442</td><td>钢铁</td><td>普钢</td><td>板材</td><td>三级 行业</td><td></td><td>2021新增</td></tr></table></body></html>  

<html><body><table><tr><td>行业代</td><td>指数代</td><td>一级</td><td rowspan="2">二级行业</td><td rowspan="2">三级行业</td><td rowspan="2">指数 类别</td><td rowspan="2">是否 发布</td><td rowspan="2">变动原因</td></tr><tr><td>码</td><td>码</td><td>行业</td></tr><tr><td>230403</td><td>850443</td><td>钢铁</td><td>普钢</td><td>钢铁管材</td><td>三级 行业</td><td>0</td><td>2021新增</td></tr><tr><td>230500</td><td>801045</td><td>钢铁</td><td>特钢II</td><td></td><td>二级 行业</td><td></td><td>2021新增</td></tr><tr><td>230501</td><td>850412</td><td>钢铁</td><td>特钢II</td><td>特钢II</td><td>三级 行业</td><td>1</td><td>2021替换 230102</td></tr><tr><td>240000</td><td>801050</td><td>有色 金属</td><td></td><td></td><td>一级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>240200</td><td>801051</td><td>有色 金属</td><td>金属新材 料</td><td></td><td>二级 行业</td><td></td><td>2021改名</td></tr><tr><td>240201</td><td>850521</td><td>有色 金属</td><td>金属新材 料</td><td>其他金属新材料</td><td>三级 行业</td><td>1</td><td>2021改名</td></tr><tr><td>240202</td><td>850522</td><td>有色 金属</td><td>金属新材 料</td><td>磁性材料</td><td>三级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>240300</td><td>801055</td><td>有色 金属</td><td>工业金属</td><td></td><td>二级 行业</td><td></td><td>2021保留</td></tr></table></body></html>  

<html><body><table><tr><td>行业代</td><td>指数代</td><td>一级 行业</td><td rowspan="2">二级行业</td><td rowspan="2">三级行业</td><td rowspan="2">指数 类别</td><td rowspan="2">是否 发布</td><td rowspan="2">变动原因</td></tr><tr><td>码</td><td>码</td></tr><tr><td>240301</td><td>850551</td><td>有色 金属</td><td>工业金属</td><td>铝</td><td>三级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>240302</td><td>850552</td><td>有色 金属</td><td>工业金属</td><td>铜</td><td>三级 行业</td><td></td><td>2021保留</td></tr><tr><td>240303</td><td>850553</td><td>有色 金属</td><td>工业金属</td><td>铅锌</td><td>三级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>240400</td><td>801053</td><td>有色 金属</td><td>贵金属</td><td></td><td>二级 行业</td><td>1</td><td>2021改名</td></tr><tr><td>240401</td><td>850531</td><td>有色 金属</td><td>贵金属</td><td>黄金</td><td>三级 行业</td><td></td><td>2021保留</td></tr><tr><td>240402</td><td>850532</td><td>有色 金属</td><td>贵金属</td><td>白银</td><td>三级 行业</td><td>0</td><td>2021新增</td></tr><tr><td>240500</td><td>801054</td><td>有色 金属</td><td>小金属</td><td></td><td>二级 行业</td><td>1</td><td>2021改名</td></tr><tr><td>240501</td><td>850541</td><td>有色 金属</td><td>小金属</td><td>稀土</td><td>三级 行业</td><td>0</td><td>2021保留</td></tr></table></body></html>  

<html><body><table><tr><td>行业代</td><td>指数代</td><td>一级 行业</td><td rowspan="2">二级行业</td><td rowspan="2">三级行业</td><td rowspan="2">指数 类别</td><td rowspan="2">是否 发布</td><td rowspan="2">变动原因</td></tr><tr><td>码</td><td>码</td><td></td></tr><tr><td>240502</td><td>850542</td><td>有色 金属</td><td>小金属</td><td>钨</td><td>三级 行业</td><td>0</td><td>2021保留</td></tr><tr><td>240504</td><td>850544</td><td>有色 金属</td><td>小金属</td><td>其他小金属</td><td>三级 行业</td><td></td><td>2021保留</td></tr><tr><td>240505</td><td>850545</td><td>有色 金属</td><td>小金属</td><td>钼</td><td>三级 行业</td><td>0</td><td>2021新增</td></tr><tr><td>240600</td><td>801056</td><td>有色 金属</td><td>能源金属</td><td></td><td>二级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>240601</td><td>850561</td><td>有色 金属</td><td>能源金属</td><td>钴</td><td>三级 行业</td><td>0</td><td>2021新增</td></tr><tr><td>240602</td><td>850562</td><td>有色 金属</td><td>能源金属</td><td>镍</td><td>三级 行业</td><td>0</td><td>2021新增</td></tr><tr><td>240603</td><td>850543</td><td>有色 金属</td><td>能源金属</td><td>锂</td><td>三级 行业</td><td>0</td><td>2021替换 240503</td></tr><tr><td>270000</td><td>801080</td><td>电子</td><td></td><td></td><td>一级 行业</td><td></td><td>2021保留</td></tr></table></body></html>  

<html><body><table><tr><td>行业代</td><td>指数代</td><td>一级</td><td rowspan="2">二级行业</td><td rowspan="2">三级行业</td><td rowspan="2">指数 类别</td><td rowspan="2">是否 发布</td><td rowspan="2">变动原因</td></tr><tr><td>码</td><td>码</td><td>行业</td></tr><tr><td>270100</td><td>801081</td><td>电子</td><td>半导体</td><td></td><td>二级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>270102</td><td>850812</td><td>电子</td><td>半导体</td><td>分立器件</td><td>三级 行业</td><td></td><td>2021保留</td></tr><tr><td>270103</td><td>850813</td><td>电子</td><td>半导体</td><td>半导体材料</td><td>三级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>270104</td><td>850814</td><td>电子</td><td>半导体</td><td>数字芯片设计</td><td>三级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>270105</td><td>850815</td><td>电子</td><td>半导体</td><td>模拟芯片设计</td><td>三级 行业</td><td></td><td>2021新增</td></tr><tr><td>270106</td><td>850816</td><td>电子</td><td>半导体</td><td>集成电路制造</td><td>三级 行业</td><td>0</td><td>2021新增</td></tr><tr><td>270107</td><td>850817</td><td>电子</td><td>半导体</td><td>集成电路封测</td><td>三级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>270108</td><td>850818</td><td>电子</td><td>半导体</td><td>半导体设备</td><td>三级 行业</td><td></td><td>2021新增</td></tr></table></body></html>  

<html><body><table><tr><td>行业代</td><td>指数代</td><td>一级</td><td rowspan="2">二级行业</td><td rowspan="2">三级行业</td><td rowspan="2">指数 类别</td><td rowspan="2">是否 发布</td><td rowspan="2">变动原因</td></tr><tr><td>码</td><td>码</td><td>行业</td></tr><tr><td>270200</td><td>801083</td><td>电子</td><td>元件</td><td></td><td>二级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>270202</td><td>850822</td><td>电子</td><td>元件</td><td>印制电路板</td><td>三级 行业</td><td></td><td>2021保留</td></tr><tr><td>270203</td><td>850823</td><td>电子</td><td>元件</td><td>被动元件</td><td>三级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>270300</td><td>801084</td><td>电子</td><td>光学光电 子</td><td></td><td>二级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>270301</td><td>850831</td><td>电子</td><td>光学光电 子</td><td>面板</td><td>三级 行业</td><td></td><td>2021改名</td></tr><tr><td>270302</td><td>850832</td><td>电子</td><td>光学光电 子</td><td>LED</td><td>三级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>270303</td><td>850833</td><td>电子</td><td>光学光电 子</td><td>光学元件</td><td>三级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>270400</td><td>801082</td><td>电子</td><td>其他电子</td><td></td><td>二级 行业</td><td></td><td>2021保留</td></tr></table></body></html>  

<html><body><table><tr><td>行业代</td><td>指数代</td><td>一级 行业</td><td>二级行业</td><td>三级行业</td><td>指数 类别</td><td>是否 发布</td><td>变动原因</td></tr><tr><td>码 270401</td><td>码 850841</td><td>电子</td><td>其他电子</td><td>其他电子川</td><td>三级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>270500</td><td>801085</td><td>电子</td><td>消费电子</td><td></td><td>二级 行业</td><td></td><td>2021改名</td></tr><tr><td>270503</td><td>850853</td><td>电子</td><td>消费电子</td><td>品牌消费电子</td><td>三级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>270504</td><td>850854</td><td>电子</td><td>消费电子</td><td>消费电子零部件及 组装</td><td>三级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>270600</td><td>801086</td><td>电子</td><td>电子化学 品I</td><td></td><td>二级 行业</td><td></td><td>2021新增</td></tr><tr><td>270601</td><td>850861</td><td>电子</td><td>电子化学 品I</td><td>电子化学品川I</td><td>三级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>280000</td><td>801880</td><td>汽车</td><td></td><td></td><td>一级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>280200</td><td>801093</td><td>汽车</td><td>汽车零部 件</td><td></td><td>二级 行业</td><td></td><td>2021保留</td></tr></table></body></html>  

<html><body><table><tr><td>行业代</td><td>指数代</td><td>一级</td><td>二级行业</td><td>三级行业</td><td>指数 类别</td><td>是否 发布</td><td>变动原因</td></tr><tr><td>码 280202</td><td>码 850922</td><td>行业 汽车</td><td>汽车零部</td><td>车身附件及饰件</td><td>三级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>280203</td><td>850923</td><td>汽车</td><td>件 汽车零部 件</td><td>底盘与发动机系统</td><td>三级 行业</td><td></td><td>2021新增</td></tr><tr><td>280204</td><td>850924</td><td>汽车</td><td>汽车零部 件</td><td>轮胎轮毂</td><td>三级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>280205</td><td>850925</td><td>汽车</td><td>汽车零部 件</td><td>其他汽车零部件</td><td>三级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>280206</td><td>850926</td><td>汽车</td><td>汽车零部 件</td><td>汽车电子电气系统</td><td>三级 行业</td><td></td><td>2021新增</td></tr><tr><td>280300</td><td>801092</td><td>汽车</td><td>汽车服务</td><td></td><td>二级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>280302</td><td>850232</td><td>汽车</td><td>汽车服务</td><td>汽车经销商</td><td>三级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>280303</td><td>850233</td><td>汽车</td><td>汽车服务</td><td>汽车综合服务</td><td>三级 行业</td><td></td><td>2021新增</td></tr></table></body></html>  

<html><body><table><tr><td>行业代</td><td>指数代</td><td>一级 行业</td><td>二级行业</td><td>三级行业</td><td>指数 类别</td><td>是否 发布</td><td>变动原因</td></tr><tr><td>码 280400</td><td>码 801881</td><td>汽车</td><td>摩托车及 其他</td><td></td><td>二级 行业</td><td>1</td><td>2021改名</td></tr><tr><td>280401</td><td>858811</td><td>汽车</td><td>摩托车及 其他</td><td>其他运输设备</td><td>三级 行业</td><td></td><td>2021保留</td></tr><tr><td>280402</td><td>858812</td><td>汽车</td><td>摩托车及 其他</td><td>摩托车</td><td>三级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>280500</td><td>801095</td><td>汽车</td><td>乘用车</td><td></td><td>二级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>280501</td><td>850951</td><td>汽车</td><td>乘用车</td><td>电动乘用车</td><td>三级 行业</td><td>0</td><td>2021新增</td></tr><tr><td>280502</td><td>850952</td><td>汽车</td><td>乘用车</td><td>综合乘用车</td><td>三级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>280600</td><td>801096</td><td>汽车</td><td>商用车</td><td></td><td>二级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>280601</td><td>850912</td><td>汽车</td><td>商用车</td><td>商用载货车</td><td>三级 行业</td><td></td><td>2021替换 280102</td></tr></table></body></html>  

<html><body><table><tr><td>行业代</td><td>指数代</td><td>一级</td><td rowspan="2">二级行业</td><td rowspan="2">三级行业</td><td rowspan="2">指数 类别</td><td rowspan="2">是否 发布</td><td rowspan="2">变动原因</td></tr><tr><td>码</td><td>码</td><td>行业</td></tr><tr><td>280602</td><td>850913</td><td>汽车</td><td>商用车</td><td>商用载客车</td><td>三级 行业</td><td>1</td><td>2021替换 280103</td></tr><tr><td>330000</td><td>801110</td><td>家用 电器</td><td></td><td></td><td>一级 行业</td><td></td><td>2021保留</td></tr><tr><td>330100</td><td>801111</td><td>家用 电器</td><td>白色家电</td><td></td><td>二级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>330102</td><td>851112</td><td>家用 电器</td><td>白色家电</td><td>空调</td><td>三级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>330106</td><td>851116</td><td>家用 电器</td><td>白色家电</td><td>冰洗</td><td>三级 行业</td><td></td><td>2021新增</td></tr><tr><td>330200</td><td>801112</td><td>家用 电器</td><td>黑色家电</td><td></td><td>二级 行业</td><td>1</td><td>2021改名</td></tr><tr><td>330201</td><td>851121</td><td>家用 电器</td><td>黑色家电</td><td>彩电</td><td>三级 行业</td><td>0</td><td>2021保留</td></tr><tr><td>330202</td><td>851122</td><td>家用 电器</td><td>黑色家电</td><td>其他黑色家电</td><td>三级 行业</td><td></td><td>2021改名</td></tr></table></body></html>  

<html><body><table><tr><td>行业代</td><td>指数代</td><td>一级 行业</td><td rowspan="2">二级行业</td><td rowspan="2">三级行业</td><td>指数 类别</td><td rowspan="2">是否 发布</td><td rowspan="2">变动原因</td></tr><tr><td>码</td><td>码</td><td></td></tr><tr><td rowspan="2">330300</td><td rowspan="2">801113</td><td>家用 电器</td><td rowspan="2">小家电</td><td rowspan="2"></td><td>二级</td><td rowspan="2">1</td><td rowspan="2">2021新增</td></tr><tr><td></td><td>行业</td></tr><tr><td>330301</td><td>851131</td><td>家用 电器</td><td>小家电</td><td>厨房小家电</td><td>三级 行业</td><td></td><td>2021新增</td></tr><tr><td>330302</td><td>851132</td><td>家用 电器</td><td>小家电</td><td>清洁小家电</td><td>三级 行业</td><td>0</td><td>2021新增</td></tr><tr><td>330303</td><td>851133</td><td>家用 电器</td><td>小家电</td><td>个护小家电</td><td>三级 行业</td><td>0</td><td>2021新增</td></tr><tr><td>330400</td><td>801114</td><td>家用 电器</td><td>厨卫电器</td><td></td><td>二级 行业</td><td></td><td>2021新增</td></tr><tr><td>330401</td><td>851141</td><td>家用 电器</td><td>厨卫电器</td><td>厨房电器</td><td>三级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>330402</td><td>851142</td><td>家用 电器</td><td>厨卫电器</td><td>卫浴电器</td><td>三级 行业</td><td>0</td><td>2021新增</td></tr><tr><td></td><td></td><td>家用</td><td>照明设备</td><td></td><td>二级</td><td></td><td></td></tr><tr><td>330500</td><td>801115</td><td>电器</td><td></td><td></td><td>行业</td><td></td><td>2021新增</td></tr></table></body></html>  

<html><body><table><tr><td>行业代</td><td>指数代 码</td><td>一级 行业</td><td rowspan="2">二级行业</td><td rowspan="2">三级行业</td><td>指数 类别</td><td rowspan="2">是否 发布</td><td rowspan="2">变动原因</td></tr><tr><td>码</td><td></td><td></td></tr><tr><td rowspan="2">330501</td><td rowspan="2">851151</td><td>家用</td><td rowspan="2">照明设备</td><td rowspan="2">照明设备川</td><td>三级 行业</td><td rowspan="2">1</td><td rowspan="2">2021新增</td></tr><tr><td>电器</td><td></td></tr><tr><td rowspan="2">330600</td><td rowspan="2">801116</td><td>家用</td><td rowspan="2">家电零部</td><td rowspan="2"></td><td>二级</td><td rowspan="2"></td><td rowspan="2">2021新增</td></tr><tr><td>电器 件I</td><td>行业</td></tr><tr><td rowspan="2">330601</td><td rowspan="2">851161</td><td>家用</td><td rowspan="2">家电零部 件I</td><td rowspan="2">家电零部件II</td><td>三级 行业</td><td rowspan="2">1</td><td rowspan="2">2021新增</td></tr><tr><td>电器</td><td></td></tr><tr><td rowspan="2">330700</td><td rowspan="2">801117</td><td>家用</td><td rowspan="2">其他家电</td><td rowspan="2"></td><td>二级 行业</td><td rowspan="2">0</td><td rowspan="2">2021新增</td></tr><tr><td>电器</td><td></td></tr><tr><td rowspan="2">330701</td><td rowspan="2">851171</td><td>家用</td><td rowspan="2">其他家电</td><td rowspan="2">其他家电川</td><td>三级 行业</td><td rowspan="2">0</td><td rowspan="2">2021新增</td></tr><tr><td>电器</td><td></td></tr><tr><td rowspan="2">340000</td><td rowspan="2">801120</td><td>食品</td><td rowspan="2"></td><td rowspan="2"></td><td>一级</td><td rowspan="2">1</td><td rowspan="2">2021保留</td></tr><tr><td>饮料</td><td>行业</td></tr><tr><td rowspan="2">340400</td><td rowspan="2">801124</td><td>食品 饮料</td><td rowspan="2">食品加工</td><td rowspan="2"></td><td>二级</td><td rowspan="2">1</td><td rowspan="2">2021保留</td></tr><tr><td></td><td>行业</td></tr><tr><td>340401</td><td>851241</td><td>食品 饮料</td><td>食品加工</td><td>肉制品</td><td>三级 行业</td><td></td><td>2021保留</td></tr></table></body></html>  

<html><body><table><tr><td>行业代</td><td>指数代</td><td>一级 行业</td><td>二级行业</td><td>三级行业</td><td>指数 类别</td><td>是否 发布</td><td>变动原因</td></tr><tr><td>码 340404</td><td>码 851244</td><td>食品 饮料</td><td>食品加工</td><td>其他食品</td><td>三级 行业</td><td>0</td><td>2021改名</td></tr><tr><td>340406</td><td>851246</td><td>食品 饮料</td><td>食品加工</td><td>预加工食品</td><td>三级 行业</td><td></td><td>2021新增</td></tr><tr><td>340407</td><td>851247</td><td>食品 饮料</td><td>食品加工</td><td>保健品</td><td>三级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>340500</td><td>801125</td><td>食品 饮料</td><td>白酒II</td><td></td><td>二级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>340501</td><td>851251</td><td>食品 饮料</td><td>白酒II</td><td>白酒川I</td><td>三级 行业</td><td></td><td>2021新增</td></tr><tr><td>340600</td><td>801126</td><td>食品 饮料</td><td>非白酒</td><td></td><td>二级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>340601</td><td>851232</td><td>食品 饮料</td><td>非白酒</td><td>啤酒</td><td>三级 行业</td><td>1</td><td>2021替换 340302</td></tr><tr><td>340602</td><td>851233</td><td>食品 饮料</td><td>非白酒</td><td>其他酒类</td><td>三级 行业</td><td></td><td>2021替换 340303</td></tr></table></body></html>  

<html><body><table><tr><td>行业代</td><td>指数代</td><td>一级 行业</td><td rowspan="2">二级行业</td><td rowspan="2">三级行业</td><td>指数 类别</td><td rowspan="2">是否 发布</td><td rowspan="2">变动原因</td></tr><tr><td>码</td><td>码</td><td></td></tr><tr><td>340700</td><td>801127</td><td>食品 饮料</td><td>饮料乳品</td><td></td><td>二级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>340701</td><td>851271</td><td>食品 饮料</td><td>饮料乳品</td><td>软饮料</td><td>三级 行业</td><td></td><td>2021新增</td></tr><tr><td>340702</td><td>851243</td><td>食品 饮料</td><td>饮料乳品</td><td>乳品</td><td>三级 行业</td><td>1</td><td>2021替换 340403</td></tr><tr><td>340800</td><td>801128</td><td>食品 饮料</td><td>休闲食品</td><td></td><td>二级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>340801</td><td>851281</td><td>食品 饮料</td><td>休闲食品</td><td>零食</td><td>三级 行业</td><td></td><td>2021新增</td></tr><tr><td>340802</td><td>851282</td><td>食品 饮料</td><td>休闲食品</td><td>烘焙食品</td><td>三级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>340803</td><td>851283</td><td>食品 饮料</td><td>休闲食品</td><td>熟食</td><td>三级 行业</td><td>0</td><td>2021新增</td></tr><tr><td>340900</td><td>801129</td><td>食品 饮料</td><td>调味发酵 品I</td><td></td><td>二级 行业</td><td></td><td>2021新增</td></tr></table></body></html>  

<html><body><table><tr><td>行业代</td><td>指数代</td><td>一级 行业</td><td>二级行业</td><td>三级行业</td><td>指数 类别</td><td>是否 发布</td><td>变动原因</td></tr><tr><td>码 340901</td><td>码 851242</td><td>食品</td><td>调味发酵</td><td>调味发酵品III</td><td>三级</td><td>1</td><td>2021替换</td></tr><tr><td>350000</td><td>801130</td><td>饮料 纺织</td><td>品I</td><td></td><td>行业 一级</td><td></td><td>340402 2021改名</td></tr><tr><td>350100</td><td>801131</td><td>服饰 纺织</td><td>纺织制造</td><td></td><td>行业 二级</td><td>1</td><td></td></tr><tr><td>350102</td><td>851312</td><td>服饰 纺织</td><td></td><td></td><td>行业 三级</td><td></td><td>2021保留</td></tr><tr><td></td><td></td><td>服饰 纺织</td><td>纺织制造</td><td>棉纺</td><td>行业 三级</td><td>1</td><td>2021保留</td></tr><tr><td>350104</td><td>851314</td><td>服饰 纺织</td><td>纺织制造</td><td>印染</td><td>行业</td><td></td><td>2021保留</td></tr><tr><td>350105</td><td>851315</td><td>服饰</td><td>纺织制造</td><td>辅料</td><td>三级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>350106</td><td>851316</td><td>纺织 服饰</td><td>纺织制造</td><td>其他纺织</td><td>三级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>350107</td><td>851317</td><td>纺织 服饰</td><td>纺织制造</td><td>纺织鞋类制造</td><td>三级 行业</td><td>0</td><td>2021新增</td></tr></table></body></html>  

<html><body><table><tr><td>行业代</td><td>指数代</td><td>一级 行业</td><td rowspan="2">二级行业</td><td rowspan="2">三级行业</td><td rowspan="2">指数 类别</td><td rowspan="2">是否 发布</td><td rowspan="2">变动原因</td></tr><tr><td>码</td><td>码</td></tr><tr><td>350200</td><td>801132</td><td>纺织 服饰</td><td>服装家纺</td><td></td><td>二级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>350205</td><td>851325</td><td>纺织 服饰</td><td>服装家纺</td><td>鞋帽及其他</td><td>三级 行业</td><td>1</td><td>2021改名</td></tr><tr><td>350206</td><td>851326</td><td>纺织 服饰</td><td>服装家纺</td><td>家纺</td><td>三级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>350208</td><td>851328</td><td>纺织 服饰</td><td>服装家纺</td><td>运动服装</td><td>三级 行业</td><td>0</td><td>2021新增</td></tr><tr><td>350209</td><td>851329</td><td>纺织 服饰</td><td>服装家纺</td><td>非运动服装</td><td>三级 行业</td><td></td><td>2021新增</td></tr><tr><td>350300</td><td>801133</td><td>纺织 服饰</td><td>饰品</td><td></td><td>二级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>350301</td><td>851331</td><td>纺织 服饰</td><td>饰品</td><td>钟表珠宝</td><td>三级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>350302</td><td>851332</td><td>纺织 服饰</td><td>饰品</td><td>多品类奢侈品</td><td>三级 行业</td><td>0</td><td>2021新增</td></tr></table></body></html>  

<html><body><table><tr><td>行业代</td><td>指数代</td><td>一级 行业</td><td rowspan="2">二级行业</td><td rowspan="2">三级行业</td><td rowspan="2">指数 类别</td><td rowspan="2">是否 发布</td><td rowspan="2">变动原因</td></tr><tr><td>码</td><td>码</td><td></td></tr><tr><td>350303</td><td>851333</td><td>纺织 服饰</td><td>饰品</td><td>其他饰品</td><td>三级 行业</td><td>0</td><td>2021新增</td></tr><tr><td>360000</td><td>801140</td><td>轻工 制造</td><td></td><td></td><td>一级 行业</td><td></td><td>2021保留</td></tr><tr><td>360100</td><td>801143</td><td>轻工 制造</td><td>造纸</td><td></td><td>二级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>360102</td><td>851412</td><td>轻工 制造</td><td>造纸</td><td>大宗用纸</td><td>三级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>360103</td><td>851413</td><td>轻工 制造</td><td>造纸</td><td>特种纸</td><td>三级 行业</td><td></td><td>2021新增</td></tr><tr><td>360200</td><td>801141</td><td>轻工 制造</td><td>包装印刷</td><td></td><td>二级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>360202</td><td>851422</td><td>轻工 制造</td><td>包装印刷</td><td>印刷</td><td>三级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>360203</td><td>851423</td><td>轻工 制造</td><td>包装印刷</td><td>金属包装</td><td>三级 行业</td><td></td><td>2021新增</td></tr></table></body></html>  

<html><body><table><tr><td>行业代</td><td>指数代</td><td>一级 行业</td><td rowspan="2">二级行业</td><td rowspan="2">三级行业</td><td rowspan="2">指数 类别</td><td rowspan="2">是否 发布</td><td rowspan="2">变动原因</td></tr><tr><td>码</td><td>码</td><td></td></tr><tr><td>360204</td><td>851424</td><td>轻工 制造</td><td>包装印刷</td><td>塑料包装</td><td>三级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>360205</td><td>851425</td><td>轻工 制造</td><td>包装印刷</td><td>纸包装</td><td>三级 行业</td><td></td><td>2021新增</td></tr><tr><td>360206</td><td>851426</td><td>轻工 制造</td><td>包装印刷</td><td>综合包装</td><td>三级 行业</td><td>0</td><td>2021新增</td></tr><tr><td>360300</td><td>801142</td><td>轻工 制造</td><td>家居用品</td><td></td><td>二级 行业</td><td>1</td><td>2021改名</td></tr><tr><td>360306</td><td>851436</td><td>轻工 制造</td><td>家居用品</td><td>瓷砖地板</td><td>三级 行业</td><td></td><td>2021新增</td></tr><tr><td>360307</td><td>851437</td><td>轻工 制造</td><td>家居用品</td><td>成品家居</td><td>三级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>360308</td><td>851438</td><td>轻工 制造</td><td>家居用品</td><td>定制家居</td><td>三级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>360309</td><td>851439</td><td>轻工 制造</td><td>家居用品</td><td>卫浴制品</td><td>三级 行业</td><td></td><td>2021新增</td></tr></table></body></html>  

<html><body><table><tr><td>行业代</td><td>指数代</td><td>一级 行业</td><td rowspan="2">二级行业</td><td rowspan="2">三级行业</td><td rowspan="2">指数 类别</td><td rowspan="2">是否 发布</td><td rowspan="2">变动原因</td></tr><tr><td>码</td><td>码</td><td></td></tr><tr><td>360311</td><td>851491</td><td>轻工 制造</td><td>家居用品</td><td>其他家居用品</td><td>三级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>360500</td><td>801145</td><td>轻工 制造</td><td>文娱用品</td><td></td><td>二级 行业</td><td></td><td>2021新增</td></tr><tr><td>360501</td><td>851451</td><td>轻工 制造</td><td>文娱用品</td><td>文化用品</td><td>三级 行业</td><td>0</td><td>2021新增</td></tr><tr><td>360502</td><td>851452</td><td>轻工 制造</td><td>文娱用品</td><td>娱乐用品</td><td>三级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>370000</td><td>801150</td><td>医药 生物</td><td></td><td></td><td>一级 行业</td><td></td><td>2021保留</td></tr><tr><td>370100</td><td>801151</td><td>医药 生物</td><td>化学制药</td><td></td><td>二级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>370101</td><td>851511</td><td>医药 生物</td><td>化学制药</td><td>原料药</td><td>三级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>370102</td><td>851512</td><td>医药 生物</td><td>化学制药</td><td>化学制剂</td><td>三级 行业</td><td></td><td>2021保留</td></tr></table></body></html>  

<html><body><table><tr><td>行业代</td><td>指数代</td><td>一级 行业</td><td rowspan="2">二级行业</td><td rowspan="2">三级行业</td><td rowspan="2">指数 类别</td><td rowspan="2">是否 发布</td><td rowspan="2">变动原因</td></tr><tr><td>码</td><td>码</td></tr><tr><td>370200</td><td>801155</td><td>医药 生物</td><td>中药II</td><td></td><td>二级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>370201</td><td>851521</td><td>医药 生物</td><td>中药II</td><td>中药III</td><td>三级 行业</td><td></td><td>2021保留</td></tr><tr><td>370300</td><td>801152</td><td>医药 生物</td><td>生物制品</td><td></td><td>二级 行业</td><td></td><td>2021保留</td></tr><tr><td>370302</td><td>851522</td><td>医药 生物</td><td>生物制品</td><td>血液制品</td><td>三级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>370303</td><td>851523</td><td>医药 生物</td><td>生物制品</td><td>疫苗</td><td>三级 行业</td><td></td><td>2021新增</td></tr><tr><td>370304</td><td>851524</td><td>医药 生物</td><td>生物制品</td><td>其他生物制品</td><td>三级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>370400</td><td>801154</td><td>医药 生物</td><td>医药商业</td><td></td><td>二级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>370402</td><td>851542</td><td>医药 生物</td><td>医药商业</td><td>医药流通</td><td>三级 行业</td><td></td><td>2021新增</td></tr></table></body></html>  

<html><body><table><tr><td>行业代</td><td>指数代</td><td>一级 行业</td><td rowspan="2">二级行业</td><td rowspan="2">三级行业</td><td rowspan="2">指数 类别</td><td rowspan="2">是否 发布</td><td rowspan="2">变动原因</td></tr><tr><td>码</td><td>码</td><td></td></tr><tr><td>370403</td><td>851543</td><td>医药 生物</td><td>医药商业</td><td>线下药店</td><td>三级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>370404</td><td>851544</td><td>医药 生物</td><td>医药商业</td><td>互联网药店</td><td>三级 行业</td><td>0</td><td>2021新增</td></tr><tr><td>370500</td><td>801153</td><td>医药 生物</td><td>医疗器械</td><td></td><td>二级 行业</td><td></td><td>2021保留</td></tr><tr><td>370502</td><td>851532</td><td>医药 生物</td><td>医疗器械</td><td>医疗设备</td><td>三级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>370503</td><td>851533</td><td>医药 生物</td><td>医疗器械</td><td>医疗耗材</td><td>三级 行业</td><td></td><td>2021新增</td></tr><tr><td>370504</td><td>851534</td><td>医药 生物</td><td>医疗器械</td><td>体外诊断</td><td>三级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>370600</td><td>801156</td><td>医药 生物</td><td>医疗服务</td><td></td><td>二级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>370602</td><td>851562</td><td>医药 生物</td><td>医疗服务</td><td>诊断服务</td><td>三级 行业</td><td>0</td><td>2021新增</td></tr></table></body></html>  

<html><body><table><tr><td>行业代</td><td>指数代</td><td>一级</td><td rowspan="2">二级行业</td><td rowspan="2">三级行业</td><td rowspan="2">指数 类别</td><td rowspan="2">是否 发布</td><td rowspan="2">变动原因</td></tr><tr><td>码</td><td>码</td><td>行业</td></tr><tr><td>370603</td><td>851563</td><td>医药 生物</td><td>医疗服务</td><td>医疗研发外包</td><td>三级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>370604</td><td>851564</td><td>医药 生物</td><td>医疗服务</td><td>医院</td><td>三级 行业</td><td></td><td>2021新增</td></tr><tr><td>370605</td><td>851565</td><td>医药 生物</td><td>医疗服务</td><td>其他医疗服务</td><td>三级 行业</td><td>0</td><td>2021新增</td></tr><tr><td>410000</td><td>801160</td><td>公用 事业</td><td></td><td></td><td>一级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>410100</td><td>801161</td><td>公用 事业</td><td>电力</td><td></td><td>二级 行业</td><td></td><td>2021保留</td></tr><tr><td>410101</td><td>851611</td><td>公用 事业</td><td>电力</td><td>火力发电</td><td>三级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>410102</td><td>851612</td><td>公用 事业</td><td>电力</td><td>水力发电</td><td>三级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>410104</td><td>851614</td><td>公用 事业</td><td>电力</td><td>热力服务</td><td>三级 行业</td><td></td><td>2021保留</td></tr></table></body></html>  

<html><body><table><tr><td>行业代</td><td>指数代</td><td>一级 行业</td><td rowspan="2">二级行业</td><td rowspan="2">三级行业</td><td>指数 类别</td><td rowspan="2">是否 发布</td><td rowspan="2">变动原因</td></tr><tr><td>码</td><td>码</td><td></td></tr><tr><td>410106</td><td>851616</td><td>公用 事业</td><td>电力</td><td>光伏发电</td><td>三级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>410107</td><td>851617</td><td>公用 事业</td><td>电力</td><td>风力发电</td><td>三级 行业</td><td></td><td>2021新增</td></tr><tr><td>410108</td><td>851618</td><td>公用 事业</td><td>电力</td><td>核力发电</td><td>三级 行业</td><td>0</td><td>2021新增</td></tr><tr><td>410109</td><td>851619</td><td>公用 事业</td><td>电力</td><td>其他能源发电</td><td>三级 行业</td><td>0</td><td>2021新增</td></tr><tr><td>410110</td><td>851610</td><td>公用 事业</td><td>电力</td><td>电能综合服务</td><td>三级 行业</td><td></td><td>2021新增</td></tr><tr><td>410300</td><td>801163</td><td>公用 事业</td><td>燃气II</td><td></td><td>二级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>410301</td><td>851631</td><td>公用 事业</td><td>燃气II</td><td>燃气III</td><td>三级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>420000</td><td>801170</td><td>交通 运输</td><td></td><td></td><td>一级 行业</td><td></td><td>2021保留</td></tr></table></body></html>  

<html><body><table><tr><td>行业代</td><td>指数代</td><td>一级 行业</td><td rowspan="2">二级行业</td><td rowspan="2">三级行业</td><td rowspan="2">指数 类别</td><td rowspan="2">是否 发布</td><td rowspan="2">变动原因</td></tr><tr><td>码</td><td>码</td><td></td></tr><tr><td>420800</td><td>801178</td><td>交通 运输</td><td>物流</td><td></td><td>二级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>420802</td><td>851782</td><td>交通 运输</td><td>物流</td><td>原材料供应链服务</td><td>三级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>420803</td><td>851783</td><td>交通 运输</td><td>物流</td><td>中间产品及消费品 供应链服务</td><td>三级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>420804</td><td>851784</td><td>交通 运输</td><td>物流</td><td>快递</td><td>三级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>420805</td><td>851785</td><td>交通 运输</td><td>物流</td><td>跨境物流</td><td>三级 行业</td><td></td><td>2021新增</td></tr><tr><td>420806</td><td>851786</td><td>交通 运输</td><td>物流</td><td>仓储物流</td><td>三级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>420807</td><td>851787</td><td>交通 运输</td><td>物流</td><td>公路货运</td><td>三级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>420900</td><td>801179</td><td>交通 运输</td><td>铁路公路</td><td></td><td>二级 行业</td><td>1</td><td>2021新增</td></tr></table></body></html>  

<html><body><table><tr><td>行业代</td><td>指数代</td><td>一级</td><td>二级行业</td><td>三级行业</td><td>指数</td><td>是否</td><td>变动原因</td></tr><tr><td>码</td><td>码</td><td>行业 交通</td><td></td><td></td><td>类别 三级</td><td>发布</td><td>2021替换</td></tr><tr><td>420901</td><td>851731</td><td>运输</td><td>铁路公路</td><td>高速公路</td><td>行业</td><td>1</td><td>420201</td></tr><tr><td>420902</td><td>851721</td><td>交通 运输</td><td>铁路公路</td><td>公交</td><td>三级 行业</td><td></td><td>2021替换 420301</td></tr><tr><td>420903</td><td>851771</td><td>交通 运输</td><td>铁路公路</td><td>铁路运输</td><td>三级 行业</td><td>1</td><td>2021替换 420701</td></tr><tr><td>421000</td><td>801991</td><td>交通 运输</td><td>航空机场</td><td></td><td>二级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>421001</td><td>851741</td><td>交通 运输</td><td>航空机场</td><td>航空运输</td><td>三级 行业</td><td></td><td>2021替换 420401</td></tr><tr><td>421002</td><td>851751</td><td>交通 运输</td><td>航空机场</td><td>机场</td><td>三级 行业</td><td>0</td><td>2021替换 420501</td></tr><tr><td>421100</td><td>801992</td><td>交通 运输</td><td>航运港口</td><td></td><td>二级 行业</td><td>1</td><td>2021新增</td></tr><tr><td></td><td></td><td>交通</td><td></td><td></td><td>三级</td><td></td><td>2021替换</td></tr><tr><td>421101</td><td>851761</td><td>运输</td><td>航运港口</td><td>航运</td><td>行业</td><td></td><td>420601</td></tr></table></body></html>  

<html><body><table><tr><td>行业代</td><td>指数代</td><td>一级 行业</td><td rowspan="2">二级行业</td><td rowspan="2">三级行业</td><td rowspan="2">指数 类别</td><td rowspan="2">是否 发布</td><td rowspan="2">变动原因</td></tr><tr><td>码</td><td>码</td><td></td></tr><tr><td>421102</td><td>851711</td><td>交通 运输</td><td>航运港口</td><td>港口</td><td>三级 行业</td><td>1</td><td>2021替换 420101</td></tr><tr><td>430000</td><td>801180</td><td>房地 产</td><td></td><td></td><td>一级 行业</td><td></td><td>2021保留</td></tr><tr><td>430100</td><td>801181</td><td>房地 产</td><td>房地产开 发</td><td></td><td>二级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>430101</td><td>851811</td><td>房地 产</td><td>房地产开 发</td><td>住宅开发</td><td>三级 行业</td><td>1</td><td>2021改名</td></tr><tr><td>430102</td><td>851812</td><td>房地 产</td><td>房地产开 发</td><td>商业地产</td><td>三级 行业</td><td></td><td>2021新增</td></tr><tr><td>430103</td><td>851813</td><td>房地 产</td><td>房地产开 发</td><td>产业地产</td><td>三级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>430300</td><td>801183</td><td>房地 产</td><td>房地产服 务</td><td></td><td>二级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>430301</td><td>851831</td><td>房地 产</td><td>房地产服 务</td><td>物业管理</td><td>三级 行业</td><td></td><td>2021新增</td></tr></table></body></html>  

<html><body><table><tr><td>行业代</td><td>指数代</td><td>一级 行业</td><td>二级行业</td><td>三级行业</td><td>指数 类别</td><td>是否 发布</td><td>变动原因</td></tr><tr><td>码 430302</td><td>码 851832</td><td>房地 产</td><td>房地产服 务</td><td>房产租赁经纪</td><td>三级 行业</td><td>0</td><td>2021新增</td></tr><tr><td>430303</td><td>851833</td><td>房地 产</td><td>房地产服 务</td><td>房地产综合服务</td><td>三级 行业</td><td>0</td><td>2021新增</td></tr><tr><td>450000</td><td>801200</td><td>商贸 零售</td><td></td><td></td><td>一级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>450200</td><td>801202</td><td>商贸 零售</td><td>贸易ⅡI</td><td></td><td>二级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>450201</td><td>852021</td><td>商贸</td><td>贸易ⅡI</td><td>贸易川</td><td>三级</td><td></td><td>2021保留</td></tr><tr><td>450300</td><td>801203</td><td>零售 商贸</td><td>一般零售</td><td></td><td>行业 二级</td><td>1</td><td>2021保留</td></tr><tr><td>450301</td><td>852031</td><td>零售 商贸</td><td>一般零售</td><td>百货</td><td>行业 三级</td><td>1</td><td>2021保留</td></tr><tr><td>450302</td><td>852032</td><td>零售 商贸 零售</td><td>一般零售</td><td>超市</td><td>行业 三级 行业</td><td></td><td>2021保留</td></tr></table></body></html>  

<html><body><table><tr><td>行业代</td><td>指数代</td><td>一级 行业</td><td rowspan="2">二级行业</td><td rowspan="2">三级行业</td><td rowspan="2">指数 类别</td><td rowspan="2">是否 发布</td><td rowspan="2">变动原因</td></tr><tr><td>码</td><td>码</td></tr><tr><td>450303</td><td>852033</td><td>商贸 零售</td><td>一般零售</td><td>多业态零售</td><td>三级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>450304</td><td>852034</td><td>商贸 零售</td><td>一般零售</td><td>商业物业经营</td><td>三级 行业</td><td></td><td>2021新增</td></tr><tr><td>450400</td><td>801204</td><td>商贸 零售</td><td>专业连锁</td><td></td><td>二级 行业</td><td>1</td><td>2021改名</td></tr><tr><td>450401</td><td>852041</td><td>商贸 零售</td><td>专业连锁</td><td>专业连锁川</td><td>三级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>450600</td><td>801206</td><td>商贸 零售</td><td>互联网电 商</td><td></td><td>二级 行业</td><td></td><td>2021新增</td></tr><tr><td>450601</td><td>852061</td><td>商贸 零售</td><td>互联网电 商</td><td>综合电商</td><td>三级 行业</td><td>0</td><td>2021新增</td></tr><tr><td>450602</td><td>852062</td><td>商贸 零售</td><td>互联网电 商</td><td>跨境电商</td><td>三级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>450603</td><td>852063</td><td>商贸 零售</td><td>互联网电 商</td><td>电商服务</td><td>三级 行业</td><td></td><td>2021新增</td></tr></table></body></html>  

<html><body><table><tr><td>行业代</td><td>指数代</td><td>一级 行业</td><td rowspan="2">二级行业</td><td rowspan="2">三级行业</td><td rowspan="2">指数 类别</td><td rowspan="2">是否 发布</td><td rowspan="2">变动原因</td></tr><tr><td>码</td><td>码</td><td></td></tr><tr><td rowspan="2">450700</td><td rowspan="2">801207</td><td>商贸</td><td rowspan="2">旅游零售</td><td rowspan="2"></td><td rowspan="2">二级 行业</td><td rowspan="2">0</td><td rowspan="2">2021新增</td></tr><tr><td>零售</td></tr><tr><td>450701</td><td>852071</td><td>商贸 零售</td><td>旅游零售</td><td>旅游零售I川</td><td>三级 行业</td><td>0</td><td>2021新增</td></tr><tr><td>460000</td><td>801210</td><td>社会 服务</td><td></td><td></td><td>一级 行业</td><td>1</td><td>2021改名</td></tr><tr><td>460600</td><td>801216</td><td>社会 服务</td><td>体育II</td><td></td><td>二级 行业</td><td>0</td><td>2021新增</td></tr><tr><td>460601</td><td>852161</td><td>社会 服务</td><td>体育II</td><td>体育I川I</td><td>三级 行业</td><td>0</td><td>2021新增</td></tr><tr><td>460700</td><td>801217</td><td>社会</td><td>本地生活</td><td></td><td>二级</td><td>0</td><td>2021新增</td></tr><tr><td>460701</td><td>852171</td><td>服务 社会</td><td>服务I 本地生活</td><td>本地生活服务川</td><td>行业 三级</td><td>0</td><td>2021新增</td></tr><tr><td></td><td></td><td>服务 社会</td><td>服务I</td><td></td><td>行业 二级</td><td></td><td></td></tr><tr><td>460800</td><td>801218</td><td>服务</td><td>专业服务</td><td></td><td>行业</td><td></td><td>2021新增</td></tr></table></body></html>  

<html><body><table><tr><td>行业代</td><td>指数代</td><td>一级 行业</td><td>二级行业</td><td>三级行业</td><td>指数 类别</td><td>是否 发布</td><td>变动原因</td></tr><tr><td>码 460801</td><td>码 852181</td><td>社会</td><td>专业服务</td><td>人力资源服务</td><td>三级</td><td>0</td><td>2021新增</td></tr><tr><td>460802</td><td>852182</td><td>服务 社会</td><td>专业服务</td><td>检测服务</td><td>行业 三级</td><td></td><td>2021新增</td></tr><tr><td>460803</td><td>852183</td><td>服务 社会 服务</td><td>专业服务</td><td>会展服务</td><td>行业 三级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>460804</td><td>852184</td><td>社会 服务</td><td>专业服务</td><td>其他专业服务</td><td>三级 行业</td><td>0</td><td>2021新增</td></tr><tr><td>460900</td><td>801219</td><td>社会 服务</td><td>酒店餐饮</td><td></td><td>二级 行业</td><td></td><td>2021新增</td></tr><tr><td>460901</td><td>852121</td><td>社会</td><td>酒店餐饮</td><td>酒店</td><td>三级</td><td>1</td><td>2021替换</td></tr><tr><td>460902</td><td>852141</td><td>服务 社会</td><td>酒店餐饮</td><td>餐饮</td><td>行业 三级</td><td>0</td><td>460201 2021替换</td></tr><tr><td></td><td></td><td>服务 社会</td><td>旅游及景</td><td></td><td>行业 二级</td><td></td><td>460401</td></tr><tr><td>461000</td><td>801993</td><td>服务</td><td>区</td><td></td><td>行业</td><td></td><td>2021新增</td></tr></table></body></html>  

<html><body><table><tr><td>行业代</td><td>指数代</td><td>一级 行业</td><td>二级行业</td><td>三级行业</td><td>指数 类别</td><td>是否 发布</td><td>变动原因</td></tr><tr><td>码 461001</td><td>码 859931</td><td>社会</td><td>旅游及景</td><td>博彩</td><td>三级</td><td>0</td><td>2021新增</td></tr><tr><td>461002</td><td>852111</td><td>服务 社会</td><td>区 旅游及景</td><td>人工景区</td><td>行业 三级</td><td></td><td>2021替换</td></tr><tr><td>461003</td><td>852112</td><td>服务 社会</td><td>区 旅游及景</td><td>自然景区</td><td>行业 三级</td><td></td><td>460101 2021替换</td></tr><tr><td>461004</td><td>852131</td><td>服务 社会</td><td>区 旅游及景</td><td></td><td>行业 三级</td><td></td><td>460102 2021替换</td></tr><tr><td></td><td></td><td>服务 社会</td><td>区</td><td>旅游综合</td><td>行业 二级</td><td>1</td><td>460301</td></tr><tr><td>461100</td><td>801994</td><td>服务</td><td>教育</td><td></td><td>行业</td><td></td><td>2021新增</td></tr><tr><td>461101</td><td>859851</td><td>社会 服务</td><td>教育</td><td>学历教育</td><td>三级 行业</td><td>0</td><td>2021新增</td></tr><tr><td>461102</td><td>859852</td><td>社会 服务</td><td>教育</td><td>培训教育</td><td>三级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>461103</td><td>859853</td><td>社会 服务</td><td>教育</td><td>教育运营及其他</td><td>三级 行业</td><td>0</td><td>2021新增</td></tr></table></body></html>  

<html><body><table><tr><td>行业代</td><td>指数代</td><td>一级</td><td rowspan="2">二级行业</td><td rowspan="2">三级行业</td><td rowspan="2">指数 类别</td><td rowspan="2">是否 发布</td><td rowspan="2">变动原因</td></tr><tr><td>码</td><td>码</td><td>行业</td></tr><tr><td>480000</td><td>801780</td><td>银行</td><td></td><td></td><td>一级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>480200</td><td>801782</td><td>银行</td><td>国有大型 银行II</td><td></td><td>二级 行业</td><td></td><td>2021新增</td></tr><tr><td>480201</td><td>857821</td><td>银行</td><td>国有大型 银行II</td><td>国有大型银行川</td><td>三级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>480300</td><td>801783</td><td>银行</td><td>股份制银 行II</td><td></td><td>二级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>480301</td><td>857831</td><td>银行</td><td>股份制银 行I</td><td>股份制银行I川</td><td>三级 行业</td><td></td><td>2021新增</td></tr><tr><td>480400</td><td>801784</td><td>银行</td><td>城商行II</td><td></td><td>二级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>480401</td><td>857841</td><td>银行</td><td>城商行II</td><td>城商行III</td><td>三级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>480500</td><td>801785</td><td>银行</td><td>农商行II</td><td></td><td>二级 行业</td><td></td><td>2021新增</td></tr></table></body></html>  

<html><body><table><tr><td>行业代</td><td>指数代</td><td>一级 行业</td><td rowspan="2">二级行业</td><td rowspan="2">三级行业</td><td rowspan="2">指数 类别</td><td rowspan="2">是否 发布</td><td rowspan="2">变动原因</td></tr><tr><td>码</td><td>码</td><td></td></tr><tr><td>480501</td><td>857851</td><td>银行</td><td>农商行II</td><td>农商行III</td><td>三级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>480600</td><td>801786</td><td>银行</td><td>其他银行</td><td></td><td>二级 行业</td><td>0</td><td>2021新增</td></tr><tr><td>480601</td><td>857861</td><td>银行</td><td>其他银行</td><td>其他银行I</td><td>三级 行业</td><td>0</td><td>2021新增</td></tr><tr><td>490000</td><td>801790</td><td>非银 金融</td><td></td><td></td><td>一级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>490100</td><td>801193</td><td>非银 金融</td><td>证券II</td><td></td><td>二级 行业</td><td></td><td>2021保留</td></tr><tr><td>490101</td><td>851931</td><td>非银 金融</td><td>证券II</td><td>证券I</td><td>三级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>490200</td><td>801194</td><td>非银 金融</td><td>保险II</td><td></td><td>二级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>490201</td><td>851941</td><td>非银 金融</td><td>保险II</td><td>保险III</td><td>三级 行业</td><td></td><td>2021保留</td></tr></table></body></html>  

<html><body><table><tr><td>行业代</td><td>指数代</td><td>一级 行业</td><td>二级行业</td><td>三级行业</td><td>指数 类别</td><td>是否 发布</td><td>变动原因</td></tr><tr><td>码 490300</td><td>码 801191</td><td>非银 金融</td><td>多元金融</td><td></td><td>二级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>490302</td><td>851922</td><td>非银 金融</td><td>多元金融</td><td>金融控股</td><td>三级 行业</td><td></td><td>2021新增</td></tr><tr><td>490303</td><td>851923</td><td>非银 金融</td><td>多元金融</td><td>期货</td><td>三级 行业</td><td>0</td><td>2021新增</td></tr><tr><td>490304</td><td>851924</td><td>非银 金融</td><td>多元金融</td><td>信托</td><td>三级 行业</td><td>0</td><td>2021新增</td></tr><tr><td>490305</td><td>851925</td><td>非银 金融</td><td>多元金融</td><td>租赁</td><td>三级 行业</td><td>0</td><td>2021新增</td></tr><tr><td>490306</td><td>851926</td><td>非银 金融</td><td>多元金融</td><td>金融信息服务</td><td>三级 行业</td><td>0</td><td>2021新增</td></tr><tr><td>490307</td><td>851927</td><td>非银 金融</td><td>多元金融</td><td>资产管理</td><td>三级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>490308</td><td>851928</td><td>非银 金融</td><td>多元金融</td><td>其他多元金融</td><td>三级 行业</td><td>0</td><td>2021新增</td></tr></table></body></html>  

<html><body><table><tr><td>行业代</td><td>指数代</td><td>一级</td><td rowspan="2">二级行业</td><td rowspan="2">三级行业</td><td rowspan="2">指数 类别</td><td rowspan="2">是否 发布</td><td rowspan="2">变动原因</td></tr><tr><td>码</td><td>码</td><td>行业</td></tr><tr><td>510000</td><td>801230</td><td>综合</td><td></td><td></td><td>一级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>510100</td><td>801231</td><td>综合</td><td>综合II</td><td></td><td>二级 行业</td><td></td><td>2021保留</td></tr><tr><td>510101</td><td>852311</td><td>综合</td><td>综合II</td><td>综合III</td><td>三级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>610000</td><td>801710</td><td>建筑 材料</td><td></td><td></td><td>一级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>610100</td><td>801711</td><td>建筑 材料</td><td>水泥</td><td></td><td>二级 行业</td><td></td><td>2021改名</td></tr><tr><td>610101</td><td>857111</td><td>建筑 材料</td><td>水泥</td><td>水泥制造</td><td>三级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>610102</td><td>857112</td><td>建筑 材料</td><td>水泥</td><td>水泥制品</td><td>三级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>610200</td><td>801712</td><td>建筑 材料</td><td>玻璃玻纤</td><td></td><td>二级 行业</td><td></td><td>2021改名</td></tr></table></body></html>  

<html><body><table><tr><td>行业代</td><td>指数代</td><td>一级</td><td rowspan="2">二级行业</td><td rowspan="2">三级行业</td><td rowspan="2">指数 类别</td><td rowspan="2">是否 发布</td><td rowspan="2">变动原因</td></tr><tr><td>码</td><td>码</td><td>行业</td></tr><tr><td>610201</td><td>857121</td><td>建筑 材料</td><td>玻璃玻纤</td><td>玻璃制造</td><td>三级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>610202</td><td>857122</td><td>建筑 材料</td><td>玻璃玻纤</td><td>玻纤制造</td><td>三级 行业</td><td></td><td>2021新增</td></tr><tr><td>610300</td><td>801713</td><td>建筑 材料</td><td>装修建材</td><td></td><td>二级 行业</td><td>1</td><td>2021改名</td></tr><tr><td>610301</td><td>850615</td><td>建筑 材料</td><td>装修建材</td><td>耐火材料</td><td>三级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>610302</td><td>850616</td><td>建筑 材料</td><td>装修建材</td><td>管材</td><td>三级 行业</td><td></td><td>2021保留</td></tr><tr><td>610303</td><td>850614</td><td>建筑 材料</td><td>装修建材</td><td>其他建材</td><td>三级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>610304</td><td>850617</td><td>建筑 材料</td><td>装修建材</td><td>防水材料</td><td>三级 行业</td><td>0</td><td>2021新增</td></tr><tr><td>610305</td><td>850618</td><td>建筑 材料</td><td>装修建材</td><td>涂料</td><td>三级 行业</td><td>0</td><td>2021新增</td></tr></table></body></html>  

<html><body><table><tr><td>行业代</td><td>指数代</td><td>一级 行业</td><td rowspan="2">二级行业</td><td rowspan="2">三级行业</td><td rowspan="2">指数 类别</td><td rowspan="2">是否 发布</td><td rowspan="2">变动原因</td></tr><tr><td>码</td><td>码</td></tr><tr><td rowspan="2">620000</td><td rowspan="2">801720</td><td>建筑</td><td rowspan="2"></td><td rowspan="2"></td><td rowspan="2">一级</td><td rowspan="2">1</td><td rowspan="2">2021保留</td></tr><tr><td></td></tr><tr><td rowspan="3">620100</td><td rowspan="3">801721</td><td>装饰 建筑</td><td rowspan="3">房屋建设</td><td rowspan="3"></td><td>行业 二级</td><td rowspan="3"></td><td rowspan="3">2021保留</td></tr><tr><td>装饰</td><td>行业</td></tr><tr><td></td><td></td></tr><tr><td rowspan="2">620101</td><td rowspan="2">850623</td><td>建筑 装饰</td><td rowspan="2">房屋建设</td><td rowspan="2">房屋建设I川</td><td>三级 行业</td><td rowspan="2">1</td><td rowspan="2">2021保留</td></tr><tr><td>建筑 装修装饰</td><td>二级</td></tr><tr><td>620200</td><td>801722</td><td>装饰</td><td></td><td></td><td>行业</td><td>1</td><td>2021保留</td></tr><tr><td>620201</td><td>857221</td><td>建筑 装饰</td><td>装修装饰</td><td>装修装饰川I</td><td>三级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>620300</td><td>801723</td><td>建筑 装饰</td><td>基础建设</td><td></td><td>二级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>620306</td><td>857236</td><td>建筑 装饰</td><td>基础建设</td><td>基建市政工程</td><td>三级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>620307</td><td>857251</td><td>建筑</td><td>基础建设</td><td></td><td>三级</td><td></td><td>2021替换</td></tr><tr><td></td><td></td><td>装饰</td><td></td><td>园林工程</td><td>行业</td><td></td><td>620501</td></tr></table></body></html>  

<html><body><table><tr><td>行业代</td><td>指数代</td><td>一级 行业</td><td>二级行业</td><td>三级行业</td><td>指数 类别</td><td>是否 发布</td><td>变动原因</td></tr><tr><td>码 620400</td><td>码 801724</td><td>建筑</td><td>专业工程</td><td></td><td>二级</td><td>1</td><td>2021保留</td></tr><tr><td>620401</td><td>857241</td><td>装饰 建筑</td><td>专业工程</td><td>钢结构</td><td>行业 三级</td><td></td><td>2021保留</td></tr><tr><td>620402</td><td>857242</td><td>装饰 建筑</td><td>专业工程</td><td>化学工程</td><td>行业 三级</td><td>1</td><td>2021保留</td></tr><tr><td>620403</td><td>857243</td><td>装饰 建筑</td><td>专业工程</td><td>国际工程</td><td>行业 三级</td><td>1</td><td>2021改名</td></tr><tr><td>620404</td><td>857244</td><td>装饰 建筑</td><td>专业工程</td><td>其他专业工程</td><td>行业 三级</td><td></td><td>2021保留</td></tr><tr><td></td><td></td><td>装饰 建筑</td><td>工程咨询</td><td></td><td>行业 二级</td><td></td><td></td></tr><tr><td>620600</td><td>801726</td><td>装饰</td><td>服务ⅡI</td><td></td><td>行业</td><td></td><td>2021新增</td></tr><tr><td>620601</td><td>857261</td><td>建筑 装饰</td><td>工程咨询 服务ⅡI</td><td>工程咨询服务川</td><td>三级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>630000</td><td>801730</td><td>电力 设备</td><td></td><td></td><td>一级 行业</td><td>1</td><td>2021改名</td></tr></table></body></html>  

<html><body><table><tr><td>行业代</td><td>指数代</td><td>一级 行业</td><td rowspan="2">二级行业</td><td rowspan="2">三级行业</td><td rowspan="2">指数 类别</td><td rowspan="2">是否 发布</td><td rowspan="2">变动原因</td></tr><tr><td>码</td><td>码</td></tr><tr><td>630100</td><td>801731</td><td>电力 设备</td><td>电机II</td><td></td><td>二级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>630101</td><td>850741</td><td>电力 设备</td><td>电机II</td><td>电机III</td><td>三级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>630300</td><td>801733</td><td>电力 设备</td><td>其他电源 设备II</td><td></td><td>二级 行业</td><td>1</td><td>2021改名</td></tr><tr><td>630301</td><td>857331</td><td>电力 设备</td><td>其他电源 设备Il</td><td>综合电力设备商</td><td>三级 行业</td><td>0</td><td>2021保留</td></tr><tr><td>630304</td><td>857334</td><td>电力 设备</td><td>其他电源 设备Il</td><td>火电设备</td><td>三级 行业</td><td></td><td>2021保留</td></tr><tr><td>630306</td><td>857336</td><td>电力 设备</td><td>其他电源 设备II</td><td>其他电源设备川</td><td>三级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>630500</td><td>801735</td><td>电力 设备</td><td>光伏设备</td><td></td><td>二级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>630501</td><td>857351</td><td>电力 设备</td><td>光伏设备</td><td>硅料硅片</td><td>三级 行业</td><td>0</td><td>2021新增</td></tr></table></body></html>  

<html><body><table><tr><td>行业代</td><td>指数代</td><td>一级 行业</td><td>二级行业</td><td>三级行业</td><td>指数 类别</td><td>是否 发布</td><td>变动原因</td></tr><tr><td>码 630502</td><td>码 857352</td><td>电力</td><td>光伏设备</td><td>光伏电池组件</td><td>三级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>630503</td><td>857353</td><td>设备 电力 设备</td><td>光伏设备</td><td>逆变器</td><td>三级 行业</td><td>0</td><td>2021新增</td></tr><tr><td>630504</td><td>857354</td><td>电力 设备</td><td>光伏设备</td><td>光伏辅材</td><td>三级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>630505</td><td>857355</td><td>电力 设备</td><td>光伏设备</td><td>光伏加工设备</td><td>三级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>630600</td><td>801736</td><td>电力 设备</td><td>风电设备</td><td></td><td>二级 行业</td><td></td><td>2021新增</td></tr><tr><td>630601</td><td>857361</td><td>电力 设备</td><td>风电设备</td><td>风电整机</td><td>三级</td><td>0</td><td>2021新增</td></tr><tr><td>630602</td><td>857362</td><td>电力</td><td>风电设备</td><td>风电零部件</td><td>行业 三级</td><td>1</td><td>2021新增</td></tr><tr><td>630700</td><td>801737</td><td>设备 电力 设备</td><td>电池</td><td></td><td>行业 二级 行业</td><td></td><td>2021新增</td></tr></table></body></html>  

<html><body><table><tr><td>行业代</td><td>指数代</td><td>一级 行业</td><td rowspan="2">二级行业</td><td rowspan="2">三级行业</td><td rowspan="2">指数 类别</td><td rowspan="2">是否 发布</td><td rowspan="2">变动原因</td></tr><tr><td>码</td><td>码</td><td></td></tr><tr><td>630701</td><td>857371</td><td>电力 设备</td><td>电池</td><td>锂电池</td><td>三级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>630702</td><td>857372</td><td>电力 设备</td><td>电池</td><td>电池化学品</td><td>三级 行业</td><td></td><td>2021新增</td></tr><tr><td>630703</td><td>857373</td><td>电力 设备</td><td>电池</td><td>锂电专用设备</td><td>三级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>630704</td><td>857374</td><td>电力 设备</td><td>电池</td><td>燃料电池</td><td>三级 行业</td><td>0</td><td>2021新增</td></tr><tr><td>630705</td><td>857375</td><td>电力 设备</td><td>电池</td><td>蓄电池及其他电池</td><td>三级 行业</td><td></td><td>2021新增</td></tr><tr><td>630800</td><td>801738</td><td>电力 设备</td><td>电网设备</td><td></td><td>二级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>630801</td><td>857381</td><td>电力 设备</td><td>电网设备</td><td>输变电设备</td><td>三级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>630802</td><td>857382</td><td>电力 设备</td><td>电网设备</td><td>配电设备</td><td>三级 行业</td><td></td><td>2021新增</td></tr></table></body></html>  

<html><body><table><tr><td>行业代</td><td>指数代</td><td>一级 行业</td><td rowspan="2">二级行业</td><td rowspan="2">三级行业</td><td rowspan="2">指数 类别</td><td rowspan="2">是否 发布</td><td rowspan="2">变动原因</td></tr><tr><td>码</td><td>码</td></tr><tr><td>630803</td><td>857321</td><td>电力 设备</td><td>电网设备</td><td>电网自动化设备</td><td>三级 行业</td><td>1</td><td>2021替换 630201</td></tr><tr><td>630804</td><td>857323</td><td>电力 设备</td><td>电网设备</td><td>电工仪器仪表</td><td>三级 行业</td><td></td><td>2021替换 630203</td></tr><tr><td>630805</td><td>857344</td><td>电力 设备</td><td>电网设备</td><td>线缆部件及其他</td><td>三级 行业</td><td>1</td><td>2021替换 630204</td></tr><tr><td>640000</td><td>801890</td><td>机械 设备</td><td></td><td></td><td>一级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>640100</td><td>801072</td><td>机械 设备</td><td>通用设备</td><td></td><td>二级 行业</td><td></td><td>2021改名</td></tr><tr><td>640101</td><td>850711</td><td>机械 设备</td><td>通用设备</td><td>机床工具</td><td>三级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>640103</td><td>850713</td><td>机械 设备</td><td>通用设备</td><td>磨具磨料</td><td>三级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>640105</td><td>850715</td><td>机械 设备</td><td>通用设备</td><td>制冷空调设备</td><td>三级 行业</td><td></td><td>2021保留</td></tr></table></body></html>  

<html><body><table><tr><td>行业代</td><td>指数代</td><td>一级 行业</td><td rowspan="2">二级行业</td><td rowspan="2">三级行业</td><td rowspan="2">指数 类别</td><td rowspan="2">是否 发布</td><td rowspan="2">变动原因</td></tr><tr><td>码</td><td>码</td></tr><tr><td>640106</td><td>850716</td><td>机械 设备</td><td>通用设备</td><td>其他通用设备</td><td>三级 行业</td><td>1</td><td>2021改名</td></tr><tr><td>640107</td><td>850731</td><td>机械 设备</td><td>通用设备</td><td>仪器仪表</td><td>三级 行业</td><td></td><td>2021替换 640301</td></tr><tr><td>640108</td><td>850751</td><td>机械 设备</td><td>通用设备</td><td>金属制品</td><td>三级 行业</td><td>1</td><td>2021替换 640401</td></tr><tr><td>640200</td><td>801074</td><td>机械 设备</td><td>专用设备</td><td></td><td>二级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>640203</td><td>850725</td><td>机械 设备</td><td>专用设备</td><td>能源及重型设备</td><td>三级 行业</td><td>1</td><td>2021改名</td></tr><tr><td>640204</td><td>850728</td><td>机械 设备</td><td>专用设备</td><td>楼宇设备</td><td>三级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>640206</td><td>850721</td><td>机械 设备</td><td>专用设备</td><td>纺织服装设备</td><td>三级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>640207</td><td>850723</td><td>机械 设备</td><td>专用设备</td><td>农用机械</td><td>三级 行业</td><td>0</td><td>2021保留</td></tr></table></body></html>  

<html><body><table><tr><td>行业代</td><td>指数代</td><td>一级 行业</td><td rowspan="2">二级行业</td><td rowspan="2">三级行业</td><td rowspan="2">指数 类别</td><td rowspan="2">是否 发布</td><td rowspan="2">变动原因</td></tr><tr><td>码</td><td>码</td></tr><tr><td>640208</td><td>850726</td><td>机械 设备</td><td>专用设备</td><td>印刷包装机械</td><td>三级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>640209</td><td>850727</td><td>机械 设备</td><td>专用设备</td><td>其他专用设备</td><td>三级 行业</td><td></td><td>2021改名</td></tr><tr><td>640500</td><td>801076</td><td>机械 设备</td><td>轨交设备</td><td></td><td>二级 行业</td><td>1</td><td>2021改名</td></tr><tr><td>640501</td><td>850936</td><td>机械 设备</td><td>轨交设备</td><td>轨交设备川</td><td>三级 行业</td><td>1</td><td>2021改名</td></tr><tr><td>640600</td><td>801077</td><td>机械 设备</td><td>工程机械</td><td></td><td>二级 行业</td><td></td><td>2021新增</td></tr><tr><td>640601</td><td>850771</td><td>机械 设备</td><td>工程机械</td><td>工程机械整机</td><td>三级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>640602</td><td>850772</td><td>机械 设备</td><td>工程机械</td><td>工程机械器件</td><td>三级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>640700</td><td>801078</td><td>机械 设备</td><td>自动化设 备</td><td></td><td>二级 行业</td><td></td><td>2021新增</td></tr></table></body></html>  

<html><body><table><tr><td>行业代</td><td>指数代</td><td>一级 行业</td><td>二级行业</td><td>三级行业</td><td>指数 类别</td><td>是否 发布</td><td>变动原因</td></tr><tr><td>码 640701</td><td>码 850781</td><td>机械</td><td>自动化设</td><td>机器人</td><td>三级</td><td>1</td><td>2021新增</td></tr><tr><td>640702</td><td>850782</td><td>设备 机械</td><td>备 自动化设</td><td>工控设备</td><td>行业 三级</td><td></td><td>2021新增</td></tr><tr><td>640703</td><td>850783</td><td>设备 机械</td><td>备 自动化设</td><td>激光设备</td><td>行业 三级</td><td>1</td><td>2021新增</td></tr><tr><td>640704</td><td>850784</td><td>设备 机械</td><td>备 自动化设</td><td>其他自动化设备</td><td>行业 三级</td><td>1</td><td></td></tr><tr><td></td><td></td><td>设备 国防</td><td>备</td><td></td><td>行业 一级</td><td></td><td>2021新增</td></tr><tr><td>650000</td><td>801740</td><td>军工</td><td></td><td></td><td>行业</td><td></td><td>2021保留</td></tr><tr><td>650100</td><td>801741</td><td>国防 军工</td><td>航天装备</td><td></td><td>二级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>650101</td><td>857411</td><td>国防 军工</td><td>航天装备</td><td>航天装备川</td><td>三级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>650200</td><td>801742</td><td>国防 军工</td><td>航空装备</td><td></td><td>二级 行业</td><td></td><td>2021保留</td></tr></table></body></html>  

<html><body><table><tr><td>行业代</td><td>指数代</td><td>一级 行业</td><td rowspan="2">二级行业</td><td rowspan="2">三级行业</td><td rowspan="2">指数 类别</td><td rowspan="2">是否 发布</td><td rowspan="2">变动原因</td></tr><tr><td>码</td><td>码</td></tr><tr><td>650201</td><td>857421</td><td>国防 军工</td><td>航空装备</td><td>航空装备川</td><td>三级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>650300</td><td>801743</td><td>国防 军工</td><td>地面兵装</td><td></td><td>二级 行业</td><td></td><td>2021保留</td></tr><tr><td>650301</td><td>857431</td><td>国防 军工</td><td>地面兵装</td><td>地面兵装川</td><td>三级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>650400</td><td>801744</td><td>国防 军工</td><td>航海装备</td><td></td><td>二级 行业</td><td>1</td><td>2021改名</td></tr><tr><td>650401</td><td>850935</td><td>国防 军工</td><td>航海装备</td><td>航海装备川</td><td>三级 行业</td><td></td><td>2021改名</td></tr><tr><td>650500</td><td>801745</td><td>国防</td><td>军工电子</td><td></td><td>二级</td><td>1</td><td>2021新增</td></tr><tr><td>650501</td><td>857451</td><td>军工 国防</td><td>军工电子</td><td>军工电子川</td><td>行业 三级</td><td>1</td><td></td></tr><tr><td></td><td></td><td>军工 计算</td><td></td><td></td><td>行业 一级</td><td></td><td>2021新增</td></tr><tr><td>710000</td><td>801750</td><td>机</td><td></td><td></td><td>行业</td><td></td><td>2021保留</td></tr></table></body></html>  

<html><body><table><tr><td>行业代</td><td>指数代</td><td>一级</td><td rowspan="2">二级行业</td><td rowspan="2">三级行业</td><td rowspan="2">指数 类别</td><td rowspan="2">是否 发布</td><td rowspan="2">变动原因</td></tr><tr><td>码</td><td>码</td><td>行业</td></tr><tr><td>710100</td><td>801101</td><td>计算 机</td><td>计算机设 备</td><td></td><td>二级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>710102</td><td>850702</td><td>计算 机</td><td>计算机设 备</td><td>安防设备</td><td>三级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>710103</td><td>850703</td><td>计算 机</td><td>计算机设 备</td><td>其他计算机设备</td><td>三级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>710300</td><td>801103</td><td>计算 机</td><td>IT服务II</td><td></td><td>二级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>710301</td><td>852226</td><td>计算 机</td><td>IT服务II</td><td>IT服务III</td><td>三级 行业</td><td></td><td>2021替换 710202</td></tr><tr><td>710400</td><td>801104</td><td>计算 机</td><td>软件开发</td><td></td><td>二级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>710401</td><td>851041</td><td>计算 机</td><td>软件开发</td><td>垂直应用软件</td><td>三级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>710402</td><td>851042</td><td>计算 机</td><td>软件开发</td><td>横向通用软件</td><td>三级 行业</td><td></td><td>2021新增</td></tr></table></body></html>  

<html><body><table><tr><td>行业代</td><td>指数代</td><td>一级</td><td rowspan="2">二级行业</td><td rowspan="2">三级行业</td><td rowspan="2">指数 类别</td><td rowspan="2">是否 发布</td><td rowspan="2">变动原因</td></tr><tr><td>码</td><td>码</td><td>行业</td></tr><tr><td>720000</td><td>801760</td><td>传媒</td><td></td><td></td><td>一级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>720400</td><td>801764</td><td>传媒</td><td>游戏II</td><td></td><td>二级 行业</td><td></td><td>2021新增</td></tr><tr><td>720401</td><td>857641</td><td>传媒</td><td>游戏II</td><td>游戏III</td><td>三级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>720500</td><td>801765</td><td>传媒</td><td>广告营销</td><td></td><td>二级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>720501</td><td>857651</td><td>传媒</td><td>广告营销</td><td>营销代理</td><td>三级 行业</td><td></td><td>2021新增</td></tr><tr><td>720502</td><td>857652</td><td>传媒</td><td>广告营销</td><td>广告媒体</td><td>三级 行业</td><td>0</td><td>2021新增</td></tr><tr><td>720600</td><td>801766</td><td>传媒</td><td>影视院线</td><td></td><td>二级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>720601</td><td>857661</td><td>传媒</td><td>影视院线</td><td>影视动漫制作</td><td>三级 行业</td><td></td><td>2021新增</td></tr></table></body></html>  

<html><body><table><tr><td>行业代</td><td>指数代</td><td>一级</td><td rowspan="2">二级行业</td><td rowspan="2">三级行业</td><td rowspan="2">指数 类别</td><td rowspan="2">是否 发布</td><td rowspan="2">变动原因</td></tr><tr><td>码</td><td>码</td><td>行业</td></tr><tr><td>720602</td><td>857662</td><td>传媒</td><td>影视院线</td><td>院线</td><td>三级 行业</td><td>0</td><td>2021新增</td></tr><tr><td>720700</td><td>801767</td><td>传媒</td><td>数字媒体</td><td></td><td>二级 行业</td><td>7</td><td>2021新增</td></tr><tr><td>720701</td><td>857671</td><td>传媒</td><td>数字媒体</td><td>视频媒体</td><td>三级 行业</td><td>0</td><td>2021新增</td></tr><tr><td>720702</td><td>857672</td><td>传媒</td><td>数字媒体</td><td>音频媒体</td><td>三级 行业</td><td>0</td><td>2021新增</td></tr><tr><td>720703</td><td>857673</td><td>传媒</td><td>数字媒体</td><td>图片媒体</td><td>三级 行业</td><td>0</td><td>2021新增</td></tr><tr><td>720704</td><td>857674</td><td>传媒</td><td>数字媒体</td><td>门户网站</td><td>三级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>720705</td><td>857675</td><td>传媒</td><td>数字媒体</td><td>文字媒体</td><td>三级 行业</td><td>0</td><td>2021新增</td></tr><tr><td>720706</td><td>857676</td><td>传媒</td><td>数字媒体</td><td>其他数字媒体</td><td>三级 行业</td><td>0</td><td>2021新增</td></tr></table></body></html>  

<html><body><table><tr><td>行业代</td><td>指数代</td><td>一级</td><td rowspan="2">二级行业</td><td rowspan="2">三级行业</td><td rowspan="2">指数 类别</td><td rowspan="2">是否 发布</td><td rowspan="2">变动原因</td></tr><tr><td>码</td><td>码</td><td>行业</td></tr><tr><td>720800</td><td>801768</td><td>传媒</td><td>社交II</td><td></td><td>二级 行业</td><td>0</td><td>2021新增</td></tr><tr><td>720801</td><td>857681</td><td>传媒</td><td>社交II</td><td>社交III</td><td>三级 行业</td><td>0</td><td>2021新增</td></tr><tr><td>720900</td><td>801769</td><td>传媒</td><td>出版</td><td></td><td>二级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>720901</td><td>857691</td><td>传媒</td><td>出版</td><td>教育出版</td><td>三级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>720902</td><td>857692</td><td>传媒</td><td>出版</td><td>大众出版</td><td>三级 行业</td><td></td><td>2021新增</td></tr><tr><td>720903</td><td>857693</td><td>传媒</td><td>出版</td><td>其他出版</td><td>三级 行业</td><td>0</td><td>2021新增</td></tr><tr><td>721000</td><td>801995</td><td>传媒</td><td>电视广播</td><td></td><td>二级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>721001</td><td>859951</td><td>传媒</td><td>电视广播</td><td>电视广播川</td><td>三级 行业</td><td></td><td>2021新增</td></tr></table></body></html>  

<html><body><table><tr><td>行业代</td><td>指数代</td><td>一级</td><td rowspan="2">二级行业</td><td rowspan="2">三级行业</td><td rowspan="2">指数 类别</td><td rowspan="2">是否 发布</td><td rowspan="2">变动原因</td></tr><tr><td>码</td><td>码</td><td>行业</td></tr><tr><td>730000</td><td>801770</td><td>通信</td><td></td><td></td><td>一级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>730100</td><td>801223</td><td>通信</td><td>通信服务</td><td></td><td>二级 行业</td><td></td><td>2021改名</td></tr><tr><td>730102</td><td>852212</td><td>通信</td><td>通信服务</td><td>电信运营商</td><td>三级 行业</td><td>0</td><td>2021新增</td></tr><tr><td>730103</td><td>852213</td><td>通信</td><td>通信服务</td><td>通信工程及服务</td><td>三级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>730104</td><td>852214</td><td>通信</td><td>通信服务</td><td>通信应用增值服务</td><td>三级 行业</td><td></td><td>2021新增</td></tr><tr><td>730200</td><td>801102</td><td>通信</td><td>通信设备</td><td></td><td>二级 行业</td><td>1</td><td>2021保留</td></tr><tr><td>730204</td><td>851024</td><td>通信</td><td>通信设备</td><td>通信网络设备及器 件</td><td>三级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>730205</td><td>851025</td><td>通信</td><td>通信设备</td><td>通信线缆及配套</td><td>三级 行业</td><td></td><td>2021新增</td></tr></table></body></html>  

<html><body><table><tr><td>行业代</td><td>指数代</td><td>一级</td><td rowspan="2">二级行业</td><td rowspan="2">三级行业</td><td rowspan="2">指数 类别</td><td rowspan="2">是否 发布</td><td rowspan="2">变动原因</td></tr><tr><td>码</td><td>码</td><td>行业</td></tr><tr><td>730206</td><td>851026</td><td>通信</td><td>通信设备</td><td>通信终端及配件</td><td>三级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>730207</td><td>851027</td><td>通信</td><td>通信设备</td><td>其他通信设备</td><td>三级 行业</td><td></td><td>2021新增</td></tr><tr><td>740000</td><td>801950</td><td>煤炭</td><td></td><td></td><td>一级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>740100</td><td>801951</td><td>煤炭</td><td>煤炭开采</td><td></td><td>二级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>740101</td><td>859511</td><td>煤炭</td><td>煤炭开采</td><td>动力煤</td><td>三级 行业</td><td></td><td>2021新增</td></tr><tr><td>740102</td><td>859512</td><td>煤炭</td><td>煤炭开采</td><td>焦煤</td><td>三级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>740200</td><td>801952</td><td>煤炭</td><td>焦炭II</td><td></td><td>二级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>740201</td><td>859521</td><td>煤炭</td><td>焦炭II</td><td>焦炭III</td><td>三级 行业</td><td></td><td>2021新增</td></tr></table></body></html>  

<html><body><table><tr><td>行业代</td><td>指数代</td><td>一级 行业</td><td rowspan="2">二级行业</td><td rowspan="2">三级行业</td><td rowspan="2">指数 类别</td><td rowspan="2">是否 发布</td><td rowspan="2">变动原因</td></tr><tr><td>码</td><td>码</td><td></td></tr><tr><td>750000</td><td>801960</td><td>石油 石化</td><td></td><td></td><td>一级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>750100</td><td>801961</td><td>石油 石化</td><td>油气开采</td><td></td><td>二级 行业</td><td>0</td><td>2021新增</td></tr><tr><td>750101</td><td>859611</td><td>石油 石化</td><td>油气开采</td><td>油气开采川</td><td>三级 行业</td><td>0</td><td>2021新增</td></tr><tr><td>750200</td><td>801962</td><td>石油 石化</td><td>油服工程</td><td></td><td>二级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>750201</td><td>859621</td><td>石油 石化</td><td>油服工程</td><td>油田服务</td><td>三级 行业</td><td></td><td>2021新增</td></tr><tr><td>750202</td><td>859622</td><td>石油 石化</td><td>油服工程</td><td>油气及炼化工程</td><td>三级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>750300</td><td>801963</td><td>石油 石化</td><td>炼化及贸 易</td><td></td><td>二级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>750301</td><td>859631</td><td>石油 石化</td><td>炼化及贸 易</td><td>炼油化工</td><td>三级 行业</td><td></td><td>2021新增</td></tr></table></body></html>  

<html><body><table><tr><td>行业代</td><td>指数代</td><td>一级 行业</td><td rowspan="2">二级行业</td><td rowspan="2">三级行业</td><td rowspan="2">指数 类别</td><td rowspan="2">是否 发布</td><td rowspan="2">变动原因</td></tr><tr><td>码</td><td>码</td><td></td></tr><tr><td>750302</td><td>859632</td><td>石油 石化</td><td>炼化及贸 易</td><td>油品石化贸易</td><td>三级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>750303</td><td>859633</td><td>石油 石化</td><td>炼化及贸 易</td><td>其他石化</td><td>三级 行业</td><td></td><td>2021新增</td></tr><tr><td>760000</td><td>801970</td><td>环保</td><td></td><td></td><td>一级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>760100</td><td>801971</td><td>环保</td><td>环境治理</td><td></td><td>二级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>760101</td><td>859711</td><td>环保</td><td>环境治理</td><td>大气治理</td><td>三级 行业</td><td></td><td>2021新增</td></tr><tr><td>760102</td><td>859712</td><td>环保</td><td>环境治理</td><td>水务及水治理</td><td>三级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>760103</td><td>859713</td><td>环保</td><td>环境治理</td><td>固废治理</td><td>三级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>760104</td><td>859714</td><td>环保</td><td>环境治理</td><td>综合环境治理</td><td>三级 行业</td><td></td><td>2021新增</td></tr></table></body></html>  

<html><body><table><tr><td>行业代</td><td>指数代</td><td>一级 行业</td><td rowspan="2">二级行业</td><td rowspan="2">三级行业</td><td rowspan="2">指数 类别</td><td rowspan="2">是否 发布</td><td rowspan="2">变动原因</td></tr><tr><td>码</td><td>码</td><td></td></tr><tr><td>760200</td><td>801972</td><td>环保</td><td>环保设备</td><td></td><td>二级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>760201</td><td>859721</td><td>环保</td><td>环保设备</td><td>环保设备I川</td><td>三级 行业</td><td></td><td>2021新增</td></tr><tr><td>770000</td><td>801980</td><td>美容 护理</td><td></td><td></td><td>一级 行业</td><td></td><td>2021新增</td></tr><tr><td>770100</td><td>801981</td><td>美容 护理</td><td>个护用品</td><td></td><td>二级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>770101</td><td>859811</td><td>美容 护理</td><td>个护用品</td><td>生活用纸</td><td>三级 行业</td><td></td><td>2021新增</td></tr><tr><td>770102</td><td>859812</td><td>美容 护理</td><td>个护用品</td><td>洗护用品</td><td>三级 行业</td><td>0</td><td>2021新增</td></tr><tr><td>770200</td><td>801982</td><td>美容 护理</td><td>化妆品</td><td></td><td>二级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>770201</td><td>859821</td><td>美容 护理</td><td>化妆品</td><td>化妆品制造及其他</td><td>三级 行业</td><td></td><td>2021新增</td></tr></table></body></html>  

<html><body><table><tr><td>行业代</td><td>指数代 码</td><td>一级</td><td>二级行业</td><td>三级行业</td><td>指数 类别</td><td>是否 发布</td><td>变动原因</td></tr><tr><td>码 770202</td><td>859822</td><td>行业 美容 护理</td><td>化妆品</td><td>品牌化妆品</td><td>三级 行业</td><td>1</td><td>2021新增</td></tr><tr><td>770300</td><td>801983</td><td>美容 护理</td><td>医疗美容</td><td></td><td>二级 行业</td><td>0</td><td>2021新增</td></tr><tr><td>770301</td><td>859831</td><td>美容 护理</td><td>医疗美容</td><td>医美耗材</td><td>三级 行业</td><td>0</td><td>2021新增</td></tr><tr><td>770302</td><td>859832</td><td>美容 护理</td><td>医疗美容</td><td>医美服务</td><td>三级 行业</td><td>0</td><td>2021新增</td></tr></table></body></html>  

输入参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>必选</td><td>描述</td></tr><tr><td>index_code</td><td>str</td><td>N</td><td>指数代码</td></tr><tr><td>level</td><td>str</td><td>N</td><td>行业分级（L1/L2/L3）</td></tr><tr><td>parent_code</td><td>str</td><td>N</td><td>父级代码 (一级为0)</td></tr><tr><td>src</td><td>str</td><td>N</td><td>指数来源（SW2014：申万2014年版本，SW2021：申万2021</td></tr></table></body></html>  

# 输出参数  

<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>index_code</td><td>str</td><td>Y</td><td>指数代码</td></tr><tr><td>industry_name</td><td>str</td><td>Y</td><td>行业名称</td></tr><tr><td>parent_code</td><td>str</td><td>Y</td><td>父级代码</td></tr><tr><td>level</td><td>str</td><td>Y</td><td>行业名称</td></tr><tr><td>industry_code</td><td>str</td><td>Y</td><td>行业代码</td></tr><tr><td>is_pub</td><td>str</td><td>Y</td><td>是否发布了指数</td></tr><tr><td>src</td><td>str</td><td>N</td><td>行业分类（SW申万)</td></tr></table></body></html>  

# 接口示例  

#获取申万一级行业列表 df $=$ pro.index_classify(level $=$ 'L1', src $=$ 'SW2021')  

#获取申万二级行业列表 df $=$ pro.index_classify(level $=$ 'L2', src $=$ 'SW2021')  

#获取申万三级级行业列表 df $=$ pro.index_classify(level='L3', src='SW2021')  

# 数据示例  

index_code industry_name level   
0 801020.SI 采掘 L1   
1 801030.SI 化工 L1   
2 801040.SI 钢铁 L1   
3 801050.SI 有色金属 L1   
4 801710.SI 建筑材料 L1   
5 801720.SI 建筑装饰 L1   
6 801730.SI 电气设备 L1   
7 801890.SI 机械设备 L1   
8 801740.SI 国防军工 L1   
9 801880.SI 汽车 L1   
10 801110.SI 家用电器 L1   
11 801130.SI 纺织服装 L1   
12 801140.SI 轻工制造 L1   
13 801200.SI 商业贸易 L1   
14 801010.SI 农林牧渔 L1   
15 801120.SI 食品饮料 L1   
16 801210.SI 休闲服务 L1   
17 801150.SI 医药生物 L1   
18 801160.SI 公用事业 L1   
19 801170.SI 交通运输 L1   
20 801180.SI 房地产 L1   
21 801080.SI 电子 L1   
22 801750.SI 计算机 L1   
23 801760.SI 传媒 L1   
24 801770.SI 通信 L1   
25 801780.SI 银行 L1   
26 801790.SI 非银金融 L1   
27 801230.SI 综合 L1  

# 申万行业成分构成(分级)  

# 接口：index_member_all  

描述：按三级分类提取申万行业成分，可提供某个分类的所有成分，也可按股票代码提取所属分类，参数灵活  

限量：单次最大2000 行，总量不限制  

权限：用户需2000 积分可调取，积分获取方法请参阅积分获取办法  

输入参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>必选</td><td>描述</td></tr><tr><td>l1_code</td><td>str</td><td>N</td><td>一级行业代码</td></tr><tr><td>12_code</td><td>str</td><td>N</td><td>二级行业代码</td></tr><tr><td>I3_code</td><td>str</td><td>N</td><td>三级行业代码</td></tr><tr><td>ts_code</td><td>str</td><td>N</td><td>股票代码</td></tr><tr><td>is_new</td><td>str</td><td>N</td><td>是否最新（默认为"Y是")</td></tr></table></body></html>  

输出参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>l1_code</td><td>str</td><td></td><td>一级行业代码</td></tr><tr><td>I1_name</td><td>str</td><td></td><td>一级行业名称</td></tr><tr><td>12_code</td><td>str</td><td></td><td>二级行业代码</td></tr><tr><td>12_name</td><td>str</td><td></td><td>二级行业名称</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>13_code</td><td>str</td><td></td><td>三级行业代码</td></tr><tr><td>I3_name</td><td>str</td><td>Y</td><td>三级行业名称</td></tr><tr><td>ts_code</td><td>str</td><td>Y</td><td>成分股票代码</td></tr><tr><td>name</td><td>str</td><td>Y</td><td>成分股票名称</td></tr><tr><td>in_date</td><td>str</td><td>Y</td><td>纳入日期</td></tr><tr><td>out_date</td><td>str</td><td>Y</td><td>剔除日期</td></tr><tr><td>is_new</td><td>str</td><td>Y</td><td>是否最新Y是N否</td></tr></table></body></html>  

# 接口示例  

#获取黄金分类的成份股 df $=$ pro.index_member_all(l3_code $=$ '850531.SI')  

#获取000001.SZ 所属行业df $=$ pro.index_member_all(ts_code $=$ '000001.SZ')  

# 数据示例  

l1_code l1_name l2_code l2_name  l3_code l3_name ts_code name in_date0 801050.SI 有色金属 801053.SI 贵金属  850531.SI 黄金 000506.SZ \*ST 中润  20220729  

1 801050.SI 有色金属  801053.SI 贵金属 850531.SI 黄 金 001337.SZ 四川黄金  20230224   
2 801050.SI 有色金属  801053.SI 贵金属 850531.SI 黄 金 600988.SH 赤峰黄金 20040414   
3 801050.SI 有色金属  801053.SI 贵金属 850531.SI 黄 金 600489.SH 中金黄金 20030812   
4 801050.SI 有色金属  801053.SI 贵金属 850531.SI 黄 金 600547.SH 山东黄金 20030826   
5 801050.SI 有色金属  801053.SI 贵金属 850531.SI 黄 金 002155.SZ 湖南黄金 20070815   
6 801050.SI 有色金属 801053.SI 贵金属 850531.SI 黄 金 002237.SZ 恒邦股份 20080428   
7 801050.SI 有色金属 801053.SI 贵金属 850531.SI 黄 金 601069.SH 西部黄金 20150115   
8 801050.SI 有色金属 801053.SI 贵金属 850531.SI 黄 金 000975.SZ 银泰黄金 20190724   
9 801050.SI 有色金属 801053.SI 贵金属 850531.SI 黄 金 300139.SZ 晓程科技 20220729   
10 801050.SI 有色金属 801053.SI 贵金属 850531.SI 黄 金 600687.SH 退市刚泰(退市)  20130701   
11 801050.SI 有色金属  801053.SI 贵金属 850531.SI 黄 金 600807.SH 济南高新  20220729   
12 801050.SI 有色金属  801053.SI 贵金属 850531.SI 黄 金 600311.SH \*ST 荣华(退市)  20140102  

# 市场交易统计  

# 接口：daily_info  

描述：获取交易所股票交易统计，包括各板块明细  

限量：单次最大4000，可循环获取，总量不限制  

权限：用户积600 积分可调取， 频次有限制，积分越高每分钟调取频次越高，5000 积分以上频次相对较高，积分获取方法请参阅积分获取办法  

输入参数  

<html><body><table><tr><td>名称</td><td>类型</td><td>必选</td><td>描述</td></tr><tr><td>trade_date</td><td>str</td><td>N</td><td>交易日期（YYYYMMDD 格式，下同）</td></tr><tr><td>ts_code</td><td>str</td><td>N</td><td>板块代码 (请参阅下方列表)</td></tr><tr><td>exchange</td><td>str</td><td>N</td><td>股票市场(SH上交所 SZ深交所)</td></tr><tr><td>start_date</td><td>str</td><td>N</td><td>开始日期</td></tr><tr><td>end_date</td><td>str</td><td>N</td><td>结束日期</td></tr><tr><td>fields</td><td>str</td><td>N</td><td>指定提取字段</td></tr><tr><td colspan="4"></td></tr><tr><td colspan="2">板块代码（TS_CODE）</td><td>板块名称（TS_NAME）</td><td>数据天</td></tr><tr><td colspan="2">SZ_MARKET</td><td>深圳市场</td><td>2004</td></tr><tr><td colspan="2">SZ_MAIN</td><td>深圳主板</td><td>2008</td></tr><tr><td colspan="2">SZ_A</td><td>深圳A股</td><td>2008</td></tr><tr><td colspan="2">SZ_B</td><td>深圳B股</td><td>2008</td></tr><tr><td colspan="2">SZ_GEM</td><td>创业板</td><td>2009</td></tr><tr><td colspan="2">SZ_SME</td><td>中小企业板</td><td>2004</td></tr></table></body></html>  

<html><body><table><tr><td>板块代码（TS_CODE）</td><td>板块名称（TS_NAME）</td><td>数据天</td></tr><tr><td>SZ_FUND</td><td>深圳基金市场</td><td>2008</td></tr><tr><td>SZ_FUND_ETF</td><td>深圳基金 ETF</td><td>2008</td></tr><tr><td>SZ_FUND_LOF</td><td>深圳基金LOF</td><td>2008</td></tr><tr><td>SZ_FUND_CEF</td><td>深圳封闭基金</td><td>2008</td></tr><tr><td>SZ_FUND_SF</td><td>深圳分级基金</td><td>2008</td></tr><tr><td>SZ_BOND</td><td>深圳债券</td><td>2008</td></tr><tr><td>SZ_BOND_CN</td><td>深圳债券现券</td><td>2008</td></tr><tr><td>SZ_BOND_REP</td><td>深圳债券回购</td><td>2008</td></tr><tr><td>SZ_BOND_ABS</td><td>深圳债券 ABS</td><td>2008</td></tr><tr><td>SZ_BOND_GOV</td><td>深圳国债</td><td>2008</td></tr><tr><td>SZ_BOND_ENT</td><td>深圳企业债</td><td>2008</td></tr><tr><td>SZ_BOND_COR</td><td>深圳公司债</td><td>2008</td></tr><tr><td>SZ_BOND_CB</td><td>深圳可转债</td><td>2008</td></tr><tr><td>SZ_WR</td><td>深圳权证</td><td>2008</td></tr><tr><td></td><td></td><td></td></tr><tr><td>SH_MARKET</td><td>上海市场</td><td>2019</td></tr></table></body></html>  

<html><body><table><tr><td>板块代码（TS_CODE）</td><td>板块名称（TS_NAME)</td><td>数据天</td></tr><tr><td>SH_A</td><td>上海A股</td><td>19916</td></tr><tr><td>SH_B</td><td>上海B股</td><td>1992</td></tr><tr><td>SH_STAR</td><td>科创板</td><td>2019</td></tr><tr><td>SH_REP</td><td>股票回购</td><td>2019</td></tr><tr><td>SH_FUND</td><td>上海基金市场</td><td>1990</td></tr><tr><td>SH_FUND_ETF</td><td>上海基金 ETF</td><td>1990</td></tr><tr><td>SH_FUND_LOF</td><td>上海基金LOF</td><td>1990</td></tr><tr><td>SH_FUND_REP</td><td>上海基金回购</td><td>1990</td></tr><tr><td>SH_FUND_CEF</td><td>上海封闭式基金</td><td>1990</td></tr><tr><td>SH_FUND_METF</td><td>上海交易型货币基金</td><td>1990</td></tr></table></body></html>  

输出参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>trade_date</td><td>str</td><td></td><td>交易日期</td></tr><tr><td>ts_code</td><td>str</td><td>Y</td><td>市场代码</td></tr><tr><td>ts_name</td><td>str</td><td>V</td><td>市场名称</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>com_count</td><td>int</td><td>Y</td><td>挂牌数</td></tr><tr><td>total_share</td><td>float</td><td>Y</td><td>总股本 (亿股)</td></tr><tr><td>float_share</td><td>float</td><td>Y</td><td>流通股本 （亿股)</td></tr><tr><td>total_mv</td><td>float</td><td>Y</td><td>总市值 (亿元)</td></tr><tr><td>float_mv</td><td>float</td><td>Y</td><td>流通市值 (亿元)</td></tr><tr><td>amount</td><td>float</td><td>Y</td><td>交易金额 (亿元)</td></tr><tr><td>vol</td><td>float</td><td>Y</td><td>成交量 (亿股)</td></tr><tr><td>trans_count</td><td>int</td><td>Y</td><td>成交笔数 （万笔)</td></tr><tr><td>pe</td><td>float</td><td>Y</td><td>平均市盈率</td></tr><tr><td>tr</td><td>float</td><td>Y</td><td>换手率（%），注：深交所暂无此列</td></tr><tr><td>exchange</td><td>str</td><td>Y</td><td>交易所(SH上交所 SZ深交所)</td></tr></table></body></html>  

# 接口示例  

#获取深圳市场20200320 各板块交易数据 df $=$ pro.daily_info(trade_date $=$ '20200320', exchange $=$ 'SZ')  

#获取深圳和上海市场20200320 各板块交易指定字段的数据 df $=$ pro.daily_info(trade_date $=$ '20200320', exchange $=$ 'SZ,SH', fi elds $=$ 'trade_date,ts_name,pe')  

# 数据示例  

trade_date ts_code ts_name com_count  total_share  float _share  \  

0 20200320 SZ_GME 创业板 802 4124.04 31  
59.24  
1 20200320 SZ_MAIN 深市主板 470 8177.40 7  
176.03  
2 20200320 SZ_MARKET 深圳市场 2220 21657.12 17  
674.90  
3 20200320 SZ_SME 中小企业板 948 9355.67  
7339.62  

total_mv float_mv amount vol trans_count pe tr exchange0 66494.71 44955.24 1475.76 99.65 830.0 50.37 NaN SZ1 70732.59 62551.44 961.92 102.30 554.0 16.12 NaN SZ2 236813.99 184009.16 4363.01 NaN NaN 25.46 2.18 SZ3 99586.67 76502.47 1925.32 179.21 1208.0 27.74 NaN SZ  

# 深圳市场每日交易概况  

描述：获取深圳市场每日交易概况  

限量：单次最大2000，可循环获取，总量不限制  

权限：用户积2000 积分可调取， 频次有限制，积分越高每分钟调取频次越高，5000 积分以上频次相对较高，积分获取方法请参阅积分获取办法  

输入参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>必选</td><td>描述</td></tr><tr><td>trade_date</td><td>str</td><td>N</td><td>交易日期（YYYYMMDD 格式，下同）</td></tr><tr><td>ts_code</td><td>str</td><td>N</td><td>板块代码</td></tr><tr><td>start_date</td><td>str</td><td>N</td><td>开始日期</td></tr><tr><td>end_date</td><td>str</td><td>N</td><td>结束日期</td></tr></table></body></html>  

ts_code 主要包括：  


<html><body><table><tr><td>板块代码（TS_CODE)</td><td>板块说明</td><td>数据</td></tr><tr><td>股票</td><td>深圳市场股票总和</td><td>2008</td></tr><tr><td>主板A股</td><td>深圳主板A股情况</td><td>2008</td></tr><tr><td>主板B股</td><td>深圳主板B股情况</td><td>2008</td></tr><tr><td>创业板A股</td><td>深圳创业板情况</td><td>2008</td></tr><tr><td>基金</td><td>深圳市场基金总和</td><td>2008</td></tr></table></body></html>  

<html><body><table><tr><td>板块代码（TS_CODE)</td><td>板块说明</td><td>数据</td></tr><tr><td>ETF</td><td>深圳ETF交易情况</td><td>2008</td></tr><tr><td>LOF</td><td>深圳LOF交易情况</td><td>2008</td></tr><tr><td>封闭式基金</td><td>深圳封闭式基金交易情况</td><td>2008</td></tr><tr><td>基础设施基金</td><td>深圳RETIS 基金交易情况</td><td>2021</td></tr><tr><td>债券</td><td>深圳债券市场总和</td><td>2008</td></tr><tr><td>债券现券</td><td>深圳现券交易情况</td><td>2008</td></tr><tr><td>债券回购</td><td>深圳债券回购交易情况</td><td>2008</td></tr><tr><td>ABS</td><td>深圳ABS交易情况</td><td>2008</td></tr><tr><td>期权</td><td>深圳期权总和</td><td>2008</td></tr></table></body></html>  

输出参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>trade_date</td><td>str</td><td></td><td></td></tr><tr><td>ts_code</td><td>str</td><td></td><td>市场类型</td></tr><tr><td>count</td><td>int</td><td></td><td>股票个娄</td></tr><tr><td>amount</td><td>float</td><td></td><td>成交金客</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>vol</td><td>None</td><td>Y</td><td>成交量</td></tr><tr><td>total_share</td><td>float</td><td>Y</td><td>总股本</td></tr><tr><td>total_mv</td><td>float</td><td>Y</td><td>总市值</td></tr><tr><td>float_share</td><td>float</td><td>Y</td><td>流通股票</td></tr><tr><td>float_mv</td><td>float</td><td></td><td>流通市</td></tr></table></body></html>  

# 接口示例  

#获取深圳市场20200320 交易数据 df $=$ pro.sz_daily_info(trade_date $=$ '20200320')  

#获取深圳市场交易情况 df $=$ pro.sz_daily_info(trade_date $=$ '20200320', ts_code $=$ '股票')  

# 数据示例  

trade_date ts_code count amount vol total_share total_mv floa t_share float_mv 0 20200320 ABS 541 504804930.72 4843368 50 04918501.00 472061975980.53 5004918501.00 47206197598 0.53 1 20200320 ETF 86 10960679423.49 8003777630 992 10471704.00 153213629317.87 99210471704.00 15321362931 7.87  

2 20200320 LOF 249 1202089548.18 2029753496 421   
42809618.00 37448346544.52 42142809618.00 3744834654   
4.52   
3 20200320 中小板 948 192532630530.61  17921759322 9   
35567938002.00 9958667914529.80 733962624249.00 765024730   
7737.14   
4 20200320 主板A 股 460 96090513214.35  10211776104   
805063702685.00 7028091416467.25 705056618283.00 62106755   
51047.30   
5 20200320 主板B 股 46 102202260.47 18980673   
12676603056.00 45168496735.09 12546456576.00 4446931   
4083.06   
6 20200320 债券 6558 170830629708.59 1386734301   
None None None No   
ne   
7 20200320 债券回购 12 97006833500.00 970873520   
None None None  

None  

8 20200320 债券现券 6005 73318991277.87 411017413   
342674191457.00 34325230393533.29 17044369724.00 17541900   
29091.49   
9 20200320 分级基金 208 1162654854.49 1242992337   
42039852135.00 39427148230.75 42039852135.00 3942714   
8230.75   
10 20200320 创业板A 股 802  147576399405.00 9965011014   
412404300212.00 6649471689968.69 315924775647.00 4495524   
754972.39   
11 20200320 基金 544 13326523128.60  11276535453 18   
3401248132.00 230833320937.40 183401248132.00 230833320   
937.40  

12 20200320 封闭式基金 1 1099302.43 11990 8114675.00 744196844.25 8114675.00 744196 844.25  

13 20200320 期权 128 388976963.00 447009 None None None Non  

14 20200320 股票 2256  436301745410.43  38117527113  21   
65712543955.00 23681399517700.83  1767490474755.00  1840091692   
7839.89  

# 同花顺板块指数行情  

接口：ths_daily  

描述：获取同花顺板块指数行情。注：数据版权归属同花顺，如做商业用途，请主动联系同花顺，如需帮助请联系微信：waditu_a限量：单次最大3000 行数据（5000 积分），可根据指数代码、日期参数循环提取。  

输入参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>必选</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td>N</td><td>指数代码</td></tr><tr><td>trade_date</td><td>str</td><td>N</td><td>交易日期（YYYYMMDD格式，下同）</td></tr><tr><td>start_date</td><td>str</td><td>N</td><td>开始日期</td></tr><tr><td>end_date</td><td>str</td><td>N</td><td>结束日期</td></tr></table></body></html>  

# 输出参数  

<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td>Y</td><td>TS指数代码</td></tr><tr><td>trade_date</td><td>str</td><td>Y</td><td>交易日</td></tr><tr><td>close</td><td>float Y</td><td></td><td>收盘点位</td></tr><tr><td>open</td><td>float Y</td><td></td><td>开盘点位</td></tr><tr><td>high</td><td>float Y</td><td></td><td>最高点位</td></tr><tr><td>low</td><td>float Y</td><td></td><td>最低点位</td></tr><tr><td>pre_close</td><td>float Y</td><td></td><td>昨日收盘点</td></tr><tr><td>avg_price</td><td>float V</td><td></td><td>平均价</td></tr><tr><td>change</td><td>float Y</td><td></td><td>涨跌点位</td></tr><tr><td>pct_change</td><td>float Y</td><td></td><td>涨跌幅</td></tr><tr><td>vol</td><td>float Y</td><td></td><td>成交量</td></tr><tr><td>turnover_rate</td><td>float Y</td><td></td><td>换手率</td></tr><tr><td>total_mv</td><td>float N</td><td></td><td>总市值</td></tr><tr><td>float_mv</td><td>float N</td><td></td><td>流通市值</td></tr></table></body></html>  

# 接口示例  

pro $=$ ts.pro_api()  

df $=$ pro.ths_daily(ts_code $=$ '865001.TI', start_date $=$ '20200101', end_date $=$ '20210101', fields $=$ 'ts_code,trade_date,open,close,hig h,low,pct_change')  

# 数据样例  

ts_code trade_date close open high low pct_change vol  

0 865001.TI 20201231  1664.7530 1660.7060  1671.2290 164   
9.4200 0.5646 13224.260000   
1 865001.TI 20201230  1655.4070 1644.5950  1664.2290 163   
8.1100 0.3073 10815.800000   
2 865001.TI 20201229  1650.3360 1686.1620  1686.1620 163   
9.0530 -1.6263 11763.170000   
3 865001.TI 20201228 1677.6190 1682.5670 1689.8980 166   
7.2110 0.6698 11813.210000   
4 865001.TI 20201224  1666.4570 1663.3270  1668.8490 164   
8.7920 0.6533 6571.630000   
229 865001.TI 20200108  1315.8190 1313.4520 1323.2140 131   
2.7090 0.2567 33180.860000   
230 865001.TI 20200107  1312.4500 1319.8580 1323.1850 131   
1.2390 -0.6790 20959.510000   
231 865001.TI 20200106  1321.4230 1322.8090 1328.0270 131   
4.8890 -0.5953 21283.400000   
232 865001.TI 20200103  1329.3370 1309.6150 1330.6640 130   
9.2810 0.6505 28610.530000   
233  865001.TI 20200102  1320.7460 1342.6220  1343.1260 130   
8.6630 -1.1273 26149.740000  

# 中信行业指数行情  

接口：ci_daily  

描述：获取中信行业指数日线行情  

限量：单次最大4000 条，可循环提取  

积分：5000 积分可调取，可通过指数代码和日期参数循环获取所有数据  

输入参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>必选</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td>N</td><td>行业代码</td></tr><tr><td>trade_date</td><td>str</td><td>N</td><td>交易日期（YYYYMMDD 格式，下同)</td></tr><tr><td>start_date</td><td>str</td><td>N</td><td>开始日期</td></tr><tr><td>end_date</td><td>str</td><td>N</td><td>结束日期</td></tr></table></body></html>  

输出参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td></td><td>指数代码</td></tr><tr><td>trade_date</td><td>str</td><td></td><td>交易日期</td></tr><tr><td>open</td><td>float</td><td></td><td>开盘点位</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>low</td><td>float</td><td>Y</td><td>最低点位</td></tr><tr><td>high</td><td>float</td><td>Y</td><td>最高点位</td></tr><tr><td>close</td><td>float</td><td>Y</td><td>收盘点位</td></tr><tr><td>pre_close</td><td>float</td><td>Y</td><td>昨日收盘点位</td></tr><tr><td>change</td><td>float</td><td>Y</td><td>涨跌点位</td></tr><tr><td>pct_change</td><td>float</td><td>Y</td><td>涨跌幅</td></tr><tr><td>vol</td><td>float</td><td>Y</td><td>成交量 (万股)</td></tr><tr><td>amount</td><td>float</td><td>Y</td><td>成交额 (万元)</td></tr></table></body></html>  

# 接口示例  

pro $=$ ts.pro_api('your token')  

df $=$ pro.ci_daily(trade_date $=$ '20230705', fields $=$ 'ts_code,trade_ date,open,low,high,close')  

# 数据示例  

ts_code trade_date open low high close 0 CI005001.CI 20230705 2757.5662 2736.8198  2764.1863 27 54.2617  

1 CI005002.CI 20230705  3006.7166  3000.1382  3039.3916 30   
29.7837   
2 CI005003.CI 20230705 6443.6250 6431.1250 6597.5933 65   
88.1401   
3 CI005004.CI 20230705 2675.3940 2672.7278  2693.6438 26   
76.9941   
4 CI005005.CI 20230705  1575.1489  1571.6997  1597.4792 15   
93.6205   
435  CI005920.CI 20230705 6585.6924  6521.1846  6599.1216 65   
29.9458   
436  CI005921.CI 20230705 2759.9133 2753.9324  2781.3979 27   
57.9863   
437  CI005922.CI 20230705 5690.3843 5645.3955 5690.4165 56   
52.8184   
438  CI005923.CI 20230705 5855.1333 5808.8325  5855.1470 58   
16.7471   
439  CI005924.CI 20230705  5782.8662  5737.0601  5782.8984  57   
44.5962  

[440 rows x 6 columns]  

# 申万行业日线行情  

# 接口：sw_daily  

描述：获取申万行业日线行情（默认是申万2021 版行情）  

限量：单次最大4000 行数据，可通过指数代码和日期参数循环提取，  

5000 积分可调取  

<html><body><table><tr><td>名称</td><td>类型</td><td>必选</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td>N</td><td>行业代码</td></tr><tr><td>trade_date</td><td>str</td><td>N</td><td>交易日期</td></tr><tr><td>start_date</td><td>str</td><td>N</td><td>开始日期</td></tr><tr><td>end_date</td><td>str</td><td>N</td><td>结束日期</td></tr></table></body></html>  

输出参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td>Y</td><td>指数代码</td></tr><tr><td>trade_date</td><td>str</td><td>Y</td><td>交易日期</td></tr><tr><td>name</td><td>str</td><td>Y</td><td>指数名称</td></tr><tr><td>open</td><td>float</td><td>Y</td><td>开盘点位</td></tr><tr><td>low</td><td>float</td><td></td><td>最低点位</td></tr><tr><td>high</td><td>float</td><td>Y</td><td>最高点位</td></tr><tr><td>close</td><td>float</td><td>Y</td><td>收盘点位</td></tr><tr><td>change</td><td>float</td><td>Y</td><td>涨跌点位</td></tr><tr><td>pct_change</td><td>float</td><td></td><td>涨跌幅</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>vol</td><td>float</td><td>Y</td><td>成交量 (万股)</td></tr><tr><td>amount</td><td>float</td><td>Y</td><td>成交额 (万元)</td></tr><tr><td>pe</td><td>float</td><td>Y</td><td>市盈率</td></tr><tr><td>pb</td><td>float</td><td>Y</td><td>市净率</td></tr><tr><td>float_mv</td><td>float</td><td>Y</td><td>流通市值 (万元)</td></tr><tr><td>total_mv</td><td>float</td><td>Y</td><td>总市值 (万元)</td></tr></table></body></html>  

# 接口示例  

pro $=$ ts.pro_api('your token')  

#获取20230705 当日所有申万行业指数的ts_code,name,open,close,vol, pe,pb 数据   
df $=$ pro.sw_daily(trade_date='20230705', fields $=$ 'ts_code,name,o pen,close,vol,pe,pb')  

# 数据示例  

ts_code name open close vol pe pb 0 801001.SI 申万50 2972.86 2946.53 275984.00 13. 99 1.91 1 801002.SI 申万中小 6963.37 6896.69 1540720.00 2 1.19 2.47  

2 801003.SI 申万Ａ指 3793.91 3769.63 6294567.00 1  
6.56 1.78  
3 801005.SI 申万创业 2841.32 2815.48 1220719.00 3  
5.90 3.72  
4 801010.SI 农林牧渔 2986.75 2946.60 83532.00 2  
8.32 2.66  
434 859811.SI 生活用纸 1438.09 1418.16 2542.00 2  
3.25 2.32  
435 859821.SI 化妆品制造及其他 2674.85 2674.57 2069.00  
40.63  2.33  
436 859822.SI 品牌化妆品 12094.45 11877.03 2809.00 4  
4.55 5.52  
437 859852.SI 培训教育 780.30 770.10 20889.00 10  
6.12 5.73  
438 859951.SI 电视广播Ⅲ 1121.00 1122.06 24413.00 5  
1.46 1.05  

# 国际指数  

接口：index_global，可以通过数据工具调试和查看数据。  

描述：获取国际主要指数日线行情  

限量：单次最大提取4000 行情数据，可循环获取，总量不限制积分：用户积6000 积分可调取，积分越高频次越高，请自行提高积分，具体请参阅积分获取办法  

<html><body><table><tr><td>名称</td><td>类型</td><td>必选</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td>N</td><td>TS指数代码，见下表</td></tr><tr><td>trade_date</td><td>str</td><td>N</td><td>交易日期，YYYYMMDD 格式，下同</td></tr><tr><td>start_date</td><td>str</td><td>N</td><td>开始日期</td></tr><tr><td>end_date</td><td>str</td><td>N</td><td>结束日期</td></tr><tr><td colspan="2"></td><td colspan="2"></td></tr><tr><td colspan="2">TS 指数代码</td><td colspan="2">指数名称</td></tr><tr><td colspan="2">XIN9</td><td colspan="2">富时中国A50指数 (富时A50)</td></tr><tr><td colspan="2">HSI</td><td colspan="2">恒生指数</td></tr><tr><td colspan="2">HKTECH</td><td colspan="2">恒生科技指数</td></tr><tr><td colspan="2">HKAH</td><td colspan="2">恒生AH股H指数</td></tr><tr><td colspan="2">DJI</td><td colspan="2">道琼斯工业指数</td></tr><tr><td colspan="2">SPX</td><td colspan="2">标普 500 指数</td></tr><tr><td colspan="2">IXIC</td><td colspan="2">纳斯达克指数</td></tr><tr><td colspan="2">FTSE</td><td colspan="2">富时100指数</td></tr><tr><td colspan="2">FCHI</td><td colspan="2">法国CAC40指数</td></tr><tr><td colspan="2">GDAXI</td><td colspan="2">德国 DAX 指数</td></tr></table></body></html>  

<html><body><table><tr><td>TS 指数代码</td><td>指数名称</td></tr><tr><td>N225</td><td>日经225指数</td></tr><tr><td>KS11</td><td>韩国综合指数</td></tr><tr><td>AS51</td><td>澳大利亚标普 200指数</td></tr><tr><td>SENSEX</td><td>印度孟买 SENSEX 指数</td></tr><tr><td>IBOVESPA</td><td>巴西IBOVESPA指数</td></tr><tr><td>RTS</td><td>俄罗斯 RTS 指数</td></tr><tr><td>TWII</td><td>台湾加权指数</td></tr><tr><td>CKLSE</td><td>马来西亚指数</td></tr><tr><td>SPTSX</td><td>加拿大S&P/TSX指数</td></tr><tr><td>CSX5P</td><td>STOXX欧洲50指数</td></tr><tr><td>RUT</td><td>罗素2000指数</td></tr></table></body></html>  

输出参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td></td><td>TS指数代码</td></tr><tr><td>trade_date</td><td>str</td><td></td><td>交易日</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>open</td><td>float</td><td>Y</td><td>开盘点位</td></tr><tr><td>close</td><td>float</td><td>Y</td><td>收盘点位</td></tr><tr><td>high</td><td>float</td><td>Y</td><td>最高点位</td></tr><tr><td>low</td><td>float</td><td>Y</td><td>最低点位</td></tr><tr><td>pre_close</td><td>float</td><td>Y</td><td>昨日收盘点</td></tr><tr><td>change</td><td>float</td><td>Y</td><td>涨跌点位</td></tr><tr><td>pct_chg</td><td>float</td><td>Y</td><td>涨跌幅</td></tr><tr><td>swing</td><td>float</td><td>Y</td><td>振幅</td></tr><tr><td>vol</td><td>float</td><td>Y</td><td>成交量 (大部分无此项数据)</td></tr><tr><td>amount</td><td>float</td><td>N</td><td>成交额 (大部分无此项数据)</td></tr></table></body></html>  

# 接口使用  

pro $=$ ts.pro_api()  

#获取富时中国50 指数   
df $=$ pro.index_global(ts_code $=$ 'XIN9', start_date $=$ '20200201', en   
d_date $=$ '20200220')  

# 数据示例  

trade_date open close high low pre_close change  \ 0 20200220 13750.45 14009.40 14023.88  13750.45 13750.45 258.95 20200219 13712.13 13750.45 13815.63 13674.43 13712.13 38.32 2 20200218 13859.23  13712.13 13859.32  13671.89 13859.23 -147.10 3 20200217 13646.93 13859.23 13859.23 13632.23 13646.93 212.30 4 20200214 13547.16  13646.93 13660.84 13518.83 13547.16 99.77 5 20200213 13638.49 13547.16 13696.95 13535.21 13638.49 -91.33 6 20200212 13603.43 13638.49 13639.14 13529.55 13603.43 35.06 20200211 13420.83 13603.43  13661.80 13420.70 13420.83 182.60 8 20200210 13426.71  13420.83  13455.79 13260.81 13426.71 -5.88 9 20200207 13481.92  13426.71  13481.92 13286.61 13481.92 -55.21 10 20200206 13301.97 13481.92 13532.73 13273.11 13301.97 179.95 11 20200205 13187.05 13301.97 13389.27 13145.93 13187.05 114.92 12 20200204 12815.75 13187.05 13195.82 12815.01 12815.75 371.30 13 20200203 13791.36  12815.75  13791.36 12622.61 13791.36 -975.61  

pct_chg ts_code   
0 1.8832 XIN9   
1 0.2795 XIN9   
2 -1.0614 XIN9   
3 1.5557 XIN9   
4 0.7365 XIN9   
5 -0.6696 XIN9   
6 0.2577 XIN9   
7 1.3606 XIN9   
8 -0.0438 XIN9   
9 -0.4095 XIN9   
10 1.3528 XIN9   
11 0.8715 XIN9   
12 2.8972 XIN9   
13 -7.0741 XIN9  

# 指数技术因子(专业版)  

接口：idx_factor_pro  

描述：获取指数每日技术面因子数据，用于跟踪指数当前走势情况，数据由Tushare 社区自产，覆盖全历史；输出参数_bfq 表示不复权描述中说明了因子的默认传参，如需要特殊参数或者更多因子可以联系管理员评估，指数包括大盘指数 申万行业指数 中信指数  

限量：单次最大8000  

积分：5000 积分每分钟可以请求30 次，8000 积分以上每分钟500 次  

输入参数  


<html><body><table><tr><td>名称</td><td>类型</td><td>必选</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td>N</td><td>指数代码(大盘指数 申万指数 中信指数)</td></tr><tr><td>start_date</td><td>str</td><td>N</td><td>开始日期</td></tr><tr><td>end_date</td><td>str</td><td>N</td><td>结束日期</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>必选</td><td>描述</td></tr><tr><td>trade_date</td><td>str</td><td>N</td><td>交易日期</td></tr></table></body></html>  

输出参数  

<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>ts_code</td><td>str</td><td>Y</td><td>指数代码</td></tr><tr><td>trade_date</td><td>str</td><td>Y</td><td>交易日期</td></tr><tr><td>open</td><td>float</td><td>Y</td><td>开盘价</td></tr><tr><td>high</td><td>float</td><td>Y</td><td>最高价</td></tr><tr><td>low</td><td>float</td><td>Y</td><td>最低价</td></tr><tr><td>close</td><td>float</td><td>Y</td><td>收盘价</td></tr><tr><td>pre_close</td><td>float</td><td>Y</td><td>昨收价</td></tr><tr><td>change</td><td>float</td><td>V</td><td>涨跌额</td></tr><tr><td>pct_change</td><td>float</td><td>Y</td><td>涨跌幅 （未复权，如果是复权请用通用行情接口）</td></tr><tr><td>vol</td><td>float</td><td>Y</td><td>成交量（手）</td></tr><tr><td>amount</td><td>float</td><td>Y</td><td>成交额 (千元)</td></tr><tr><td>asi_bfq</td><td>float</td><td>Y</td><td>振动升降指标-OPEN,CLOSE,HIGH,LOW,M1=26,M2=10</td></tr><tr><td>asit_bfq</td><td>float</td><td>Y</td><td>振动升降指标-OPEN,CLOSE,HIGH,LOW,M1=26,M2=10</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>atr_bfq</td><td>float</td><td>Y</td><td>真实波动 N 日平均值-CLOSE,HIGH,LOW,N=20</td></tr><tr><td>bbi_bfq</td><td>float</td><td>Y</td><td>BBI多空指标-CLOSE,M1=3,M2=6,M3=12,M4=20</td></tr><tr><td>bias1_bfq</td><td>float</td><td>Y</td><td>BIAS 乖离率-CLOSE,L1=6,L2=12,L3=24</td></tr><tr><td>bias2_bfq</td><td>float</td><td>Y</td><td>BIAS 乖离率-CLOSE,L1=6,L2=12,L3=24</td></tr><tr><td>bias3_bfq</td><td>float</td><td>Y</td><td>BIAS 乖离率-CLOSE,L1=6,L2=12,L3=24</td></tr><tr><td>boll_lower_bfq</td><td>float</td><td>Y</td><td>BOLL 指标，布林带-CLOSE,N=20,P=2</td></tr><tr><td>boll_mid_bfq</td><td>float</td><td>Y</td><td>BOLL指标，布林带-CLOSE,N=20,P=2</td></tr><tr><td>boll_upper_bfq</td><td>float</td><td>Y</td><td>BOLL 指标，布林带-CLOSE,N=20,P=2</td></tr><tr><td>brar_ar_bfq</td><td>float</td><td>Y</td><td>BRAR 情绪指标-OPEN,CLOSE,HIGH,LOW,M1=26</td></tr><tr><td>brar_br_bfq</td><td>float</td><td>Y</td><td>BRAR 情绪指标-OPEN,CLOSE,HIGH,LOW,M1=26</td></tr><tr><td>cci_bfq</td><td>float</td><td>Y</td><td>顺势指标又叫 CCI指标-CLOSE,HIGH,LOW,N=14</td></tr><tr><td>cr_bfq</td><td>float</td><td>Y</td><td>CR 价格动量指标-CLOSE,HIGH,LOW,N=20</td></tr><tr><td>dfma_dif_bfq</td><td>float</td><td>Y</td><td>平行线差指标-CLOSE,N1=10,N2=50,M=10</td></tr><tr><td>dfma_difma_bfq</td><td>float</td><td>Y</td><td>平行线差指标-CLOSE,N1=10,N2=50,M=10</td></tr><tr><td>dmi_adx_bfq</td><td>float</td><td>Y</td><td>动向指标-CLOSE,HIGH,LOW,M1=14,M2=6</td></tr><tr><td>dmi_adxr_bfq</td><td>float</td><td>Y</td><td>动向指标-CLOSE,HIGH,LOW,M1=14,M2=6</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>dmi_mdi_bfq</td><td>float</td><td>Y</td><td>动向指标-CLOSE,HIGH,LOW,M1=14,M2=6</td></tr><tr><td>dmi_pdi_bfq</td><td>float</td><td>Y</td><td>动向指标-CLOSE,HIGH,LOW,M1=14,M2=6</td></tr><tr><td>downdays</td><td>float</td><td>Y</td><td>连跌天数</td></tr><tr><td>updays</td><td>float</td><td>Y</td><td>连涨天数</td></tr><tr><td>dpo_bfq</td><td>float</td><td>Y</td><td>区间震荡线-CL0SE,M1=20,M2=10,M3=6</td></tr><tr><td>madpo_bfq</td><td>float</td><td>Y</td><td>区间震荡线-CLOSE,M1=20,M2=10,M3=6</td></tr><tr><td>ema_bfq_10</td><td>float</td><td>Y</td><td>指数移动平均-N=10</td></tr><tr><td>ema_bfq_20</td><td>float</td><td>Y</td><td>指数移动平均-N=20</td></tr><tr><td>ema_bfq_250</td><td>float</td><td>Y</td><td>指数移动平均-N=250</td></tr><tr><td>ema_bfq_30</td><td>float</td><td>Y</td><td>指数移动平均-N=30</td></tr><tr><td>ema_bfq_5</td><td>float</td><td>Y</td><td>指数移动平均-N=5</td></tr><tr><td>ema_bfq_60</td><td>float</td><td>Y</td><td>指数移动平均-N=60</td></tr><tr><td>ema_bfq_90</td><td>float</td><td>Y</td><td>指数移动平均-N=90</td></tr><tr><td>emv_bfq</td><td>float</td><td>Y</td><td>简易波动指标-HIGH,LOW,VOL,N=14,M=9</td></tr><tr><td>maemv_bfq</td><td>float</td><td>Y</td><td>简易波动指标-HIGH,LOW,VOL,N=14,M=9</td></tr><tr><td>expma_12_bfq</td><td>float</td><td>V</td><td>EMA 指数平均数指标-CLOSE,N1=12,N2=50</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>expma_50_bfq</td><td>float</td><td>Y</td><td>EMA指数平均数指标-CLOSE,N1=12,N2=50</td></tr><tr><td>kdj_bfq</td><td>float</td><td>Y</td><td>KDJ 指标-CLOSE,HIGH,LOW,N=9,M1=3,M2=3</td></tr><tr><td>kdj_d_bfq</td><td>float</td><td>Y</td><td>KDJ指标-CLOSE,HIGH,LOW,N=9,M1=3,M2=3</td></tr><tr><td>kdj_k_bfq</td><td>float</td><td>Y</td><td>KDJ 指标-CLOSE,HIGH,LOW,N=9,M1=3, M2=3</td></tr><tr><td>ktn_down_bfq</td><td>float</td><td>Y</td><td>肯特纳交易通道,N 选 20日，ATR 选10 日-CLOSE,HIGH,</td></tr><tr><td>ktn_mid_bfq</td><td>float</td><td>Y</td><td>肯特纳交易通道,N 选 20 日，ATR 选10 日-CLOSE,HIGH</td></tr><tr><td>ktn_upper_bfq</td><td>float</td><td>Y</td><td>肯特纳交易通道,N 选 20 日，ATR 选 10 日-CLOSE,HIGH,</td></tr><tr><td>lowdays</td><td>float</td><td>Y</td><td>LOWRANGE(LOW)表示当前最低价是近多少周期内最低价</td></tr><tr><td>topdays</td><td>float</td><td>Y</td><td>TOPRANGE(HIGH)表示当前最高价是近多少周期内最高价</td></tr><tr><td>ma_bfq_10</td><td>float</td><td>Y</td><td>简单移动平均-N=10</td></tr><tr><td>ma_bfq_20</td><td>float</td><td>Y</td><td>简单移动平均-N=20</td></tr><tr><td>ma_bfq_250</td><td>float</td><td>Y</td><td>简单移动平均-N=250</td></tr><tr><td>ma_bfq_30</td><td>float</td><td>Y</td><td>简单移动平均-N=30</td></tr><tr><td>ma_bfq_5</td><td>float</td><td>Y</td><td>简单移动平均-N=5</td></tr><tr><td>ma_bfq_60</td><td>float</td><td>Y</td><td>简单移动平均-N=60</td></tr><tr><td>ma_bfq_90</td><td>float</td><td>Y</td><td>简单移动平均-N=90</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>macd_bfq</td><td>float</td><td>Y</td><td>MACD 指标-CLOSE,SHORT=12,LONG=26,M=9</td></tr><tr><td>macd_dea_bfg</td><td>float</td><td>Y</td><td>MACD 指标-CLOSE,SHORT=12,LONG=26,M=9</td></tr><tr><td>macd_dif_bfq</td><td>float</td><td>Y</td><td>MACD指标-CLOSE,SHORT=12,LONG=26,M=9</td></tr><tr><td>mass_bfq</td><td>float</td><td>Y</td><td>梅斯线-HIGH,LOW,N1=9,N2=25,M=6</td></tr><tr><td>ma_mass_bfq</td><td>float</td><td>Y</td><td>梅斯线-HIGH,LOW,N1=9,N2=25,M=6</td></tr><tr><td>mfi_bfq</td><td>float</td><td>Y</td><td>MFI指标是成交量的 RSI指标-CLOSE,HIGH,LOW,VOL,N</td></tr><tr><td>mtm_bfq</td><td>float</td><td>Y</td><td>动量指标-CLOSE,N=12,M=6</td></tr><tr><td>mtmma_bfq</td><td>float</td><td>Y</td><td>动量指标-CLOSE,N=12,M=6</td></tr><tr><td>obv_bfq</td><td>float</td><td>Y</td><td>能量潮指标-CLOSE,VOL</td></tr><tr><td>psy_bfq</td><td>float</td><td>Y</td><td>投资者对股市涨跌产生心理波动的情绪指标-CLOSE,N=12</td></tr><tr><td>psyma_bfq</td><td>float</td><td>Y</td><td>投资者对股市涨跌产生心理波动的情绪指标-CLOSE,N=12</td></tr><tr><td>roc_bfq</td><td>float</td><td>Y</td><td>变动率指标-CLOSE,N=12,M=6</td></tr><tr><td>maroc_bfq</td><td>float</td><td>Y</td><td>变动率指标-CLOSE,N=12,M=6</td></tr><tr><td>rsi_bfq_12</td><td>float</td><td>Y</td><td>RSI 指标-CLOSE,N=12</td></tr><tr><td>rsi_bfq_24</td><td>float</td><td>Y</td><td>RSI指标-CLOSE,N=24</td></tr><tr><td>rsi_bfq_6</td><td>float</td><td>Y</td><td>RSI 指标-CLOSE,N=6</td></tr></table></body></html>  

<html><body><table><tr><td>名称</td><td>类型</td><td>默认显示</td><td>描述</td></tr><tr><td>taq_down_bfq</td><td>float</td><td>Y</td><td>唐安奇通道(海龟)交易指标-HIGH,LOW,20</td></tr><tr><td>taq_mid_bfq</td><td>float</td><td>Y</td><td>唐安奇通道(海龟)交易指标-HIGH,LOW,20</td></tr><tr><td>taq_up_bfq</td><td>float</td><td>Y</td><td>唐安奇通道(海龟)交易指标-HIGH,LOW,20</td></tr><tr><td>trix_bfq</td><td>float</td><td>Y</td><td>三重指数平滑平均线-CLOSE,M1=12,M2=20</td></tr><tr><td>trma_bfq</td><td>float</td><td>Y</td><td>三重指数平滑平均线-CLOSE,M1=12,M2=20</td></tr><tr><td>vr_bfq</td><td>float</td><td>Y</td><td>VR容量比率-CLOSE,VOL,M1=26</td></tr><tr><td>wr_bfq</td><td>float</td><td>Y</td><td>W&R 威廉指标-CLOSE,HIGH,LOW,N=10,N1=6</td></tr><tr><td>wr1_bfq</td><td>float</td><td>Y</td><td>W&R 威廉指标-CLOSE,HIGH,LOW,N=10,N1=6</td></tr><tr><td>xsii_td1_bfq</td><td>float</td><td>Y</td><td>薛斯通道II-CLOSE,HIGH,LOW,N=102,M=7</td></tr><tr><td>xsi_td2_bfq</td><td>float</td><td>Y</td><td>薛斯通道 II-CLOSE,HIGH,LOW,N=102,M=7</td></tr><tr><td>xsii_td3_bfq</td><td>float</td><td>Y</td><td>薛斯通道II-CLOSE,HIGH,LOW,N=102,M=7</td></tr><tr><td>xsii_td4_bfq</td><td>float</td><td>Y</td><td>薛斯通道II-CLOSE,HIGH,LOW,N=102,M=7</td></tr></table></body></html>  