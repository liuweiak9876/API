# OpenAPI 介绍  

# #概述  

OpenAPI 量化接口，为您的程序化交易，提供丰富的行情和交易接口，满足每一位开发者的量化投资需求，助力您的宽客梦想。  

牛牛用户可以 点击这里了解更多。  

OpenAPI 由 OpenD 和 Futu API 组成：  

OpenD 是 Futu API 的网关程序，运行于您的本地电脑或云端服务器，负责中转协议请求到富途后台，并将处理后的数据返回。Futu API 是富途为主流的编程语言（Python、Java、C#、C++、JavaScript）封装的 API SDK，以方便您调用，降低策略开发难度。如果您希望使用的语言没有在上述之列，您仍可自行对接裸协议，完成策略开发。  

下面的框架图和时序图，帮助您更好地了解 OpenAPI。  

![](FutuAPI/e27ab567cc523426ca2348f9992efef57b1d320105b735dcb5e54aae14ce20df.jpg)  

![](FutuAPI/14efe6f5c3a4f03efbc0d7fc3fe464e7ae882a90e7db3bd03dff278d87afb8c2.jpg)  

初次接触 OpenAPI，您需要进行如下两步操作：  

第一步，在本地或云端安装并启动一个网关程序 OpenD。  

OpenD 以自定义 TCP 协议的方式对外暴露接口，负责中转协议请求到富途服务器，并将处理后的数据返回，该协议接口与编程语言无关。  

第二步，下载 Futu API，完成 环境搭建，以便快速调用。  

为方便您的使用，富途对主流的编程语言，封装了相应的 API SDK（以下简称Futu API）。  

# #账号  

OpenAPI 涉及 2 类账号，分别是 平台账号 和 综合账户。  

# #平台账号  

平台账号是您在富途的用户 ID（牛牛号），此账号体系适用于富途牛牛  

APP、OpenAPI。 您可以使用平台账号（牛牛号）和登录密码，登录 OpenD并获取行情。  

# #综合账户  

综合账户支持以多种货币在同一个账户内交易不同市场品类（港股、美股、A股通、基金）。您可以通过一个账户进行全市场交易，不需要再管理多个账户。综合账户包括综合账户 - 证券，综合账户 - 期货等业务账户：  

综合账户 - 证券，用于交易全市场的股票、ETFs、期权等证券类产品。综合账户 - 期货，用于交易全市场的期货产品，目前支持香港市场期货、美国市场 CME Group 期货、新加坡市场期货、日本市场期货。  

# #功能  

OpenAPI 的功能主要有两部分：行情和交易。  

# #行情功能  

# #行情数据品类  

支持香港、美国、A 股市场的行情数据，涉及的品类包括股票、指数、期权、期货等，具体支持的品种见下表。  
获取行情数据需要相关权限，如需了解行情权限的获取方式以及限制规则，请 点击这里。  

<html><body><table><tr><td>市场</td><td>品种</td><td>牛牛用户</td></tr><tr><td rowspan="5">香港市场</td><td>股票、ETFs、窝轮、牛熊、界内证</td><td>√</td></tr><tr><td>期权</td><td></td></tr><tr><td>期货</td><td></td></tr><tr><td>指数</td><td></td></tr><tr><td>板块</td><td></td></tr><tr><td rowspan="5">美国市场</td><td>股票、ETFs</td><td></td></tr><tr><td>OTC股票</td><td>X</td></tr><tr><td>期权</td><td></td></tr><tr><td>期货</td><td></td></tr><tr><td>指数</td><td>X</td></tr></table></body></html>  

<html><body><table><tr><td></td><td>板块</td><td></td></tr><tr><td rowspan="3">A股市场</td><td>股票、ETFs</td><td></td></tr><tr><td>指数</td><td></td></tr><tr><td>板块</td><td></td></tr><tr><td rowspan="2">新加坡市场</td><td>股票、ETFs、窝轮、REITs、DLCs</td><td>X</td></tr><tr><td>期货</td><td>X</td></tr><tr><td rowspan="2">日本市场</td><td>股票、ETFs、REITs</td><td>X</td></tr><tr><td>期货</td><td>X</td></tr><tr><td>澳大利亚市场</td><td>股票、ETFs</td><td>X</td></tr><tr><td>环球市场</td><td>外汇</td><td>X</td></tr></table></body></html>  

# #行情数据获取方式  

订阅并接收实时报价、实时 K 线、实时逐笔、实时摆盘等数据推送拉取最新市场快照，历史 K 线等  

# #交易功能  

# #交易能力  

支持香港、美国、A 股、新加坡、日本 5 个市场的交易能力，涉及的品类包括股票、期权、期货等，具体见下表：  

<html><body><table><tr><td rowspan="4">市场</td><td rowspan="4">品 种</td><td rowspan="4">模拟交易</td><td colspan="8">真实交易</td></tr><tr><td>F</td><td>Mo</td><td>Mo</td><td>Mo</td><td>Mo</td><td>Mo</td><td>Mo</td></tr><tr><td>U</td><td>om</td><td>om</td><td>om</td><td>om</td><td></td><td></td></tr><tr><td></td><td></td><td></td><td></td><td></td><td></td><td>om</td><td>om</td></tr></table></body></html>  

<html><body><table><tr><td colspan="2"></td><td></td><td>T</td><td>00</td><td>00</td><td>00</td><td>00</td><td>00</td><td>00</td></tr><tr><td rowspan="3"></td><td rowspan="3"></td><td>U</td><td>US</td><td>SG</td><td>AU</td><td>MY</td><td>CA</td><td></td><td>JP</td></tr><tr><td>H K</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td></tr><tr><td>股 票 ET Fs 窝 轮 香 牛 港 熊 界 内</td><td></td><td></td><td></td><td></td><td></td><td>X</td><td>X</td><td>X</td></tr><tr><td>市 场</td><td>证 期 权</td><td></td><td></td><td>X</td><td>X</td><td>X</td><td>X</td><td></td><td>X</td><td>X</td></tr><tr><td rowspan="2">美 国 市</td><td>期 货</td><td></td><td></td><td>X</td><td>X</td><td>X</td><td></td><td>X</td><td>X</td><td>X</td></tr><tr><td>股 票 ET 场 Fs</td><td></td><td></td><td></td><td></td><td></td><td>X</td><td></td><td>X</td><td>X</td></tr></table></body></html>  

<html><body><table><tr><td></td><td>期 权</td><td></td><td></td><td></td><td></td><td></td><td>X</td><td>X</td><td>X</td></tr><tr><td></td><td>期 货</td><td></td><td></td><td>X</td><td></td><td>X</td><td>X</td><td>X</td><td>X</td></tr><tr><td></td><td>A 股 通 股</td><td></td><td></td><td></td><td></td><td>X</td><td>X</td><td>X</td><td>X</td></tr><tr><td>A 股 市 场</td><td>票 非 A 股 通 股 票</td><td></td><td>X</td><td>X</td><td>X</td><td>X</td><td>X</td><td>X</td><td>X</td></tr><tr><td>新 加 坡 市 场</td><td>股 票 ET Fs 窝 轮 REI Ts DL Cs</td><td>X</td><td>X</td><td>X</td><td>X</td><td>X</td><td>X</td><td>X</td><td>X</td></tr></table></body></html>  

<html><body><table><tr><td></td><td>期 货</td><td></td><td></td><td>X</td><td></td><td>X</td><td>X</td><td>X</td><td>X</td></tr><tr><td>日 本 市 场</td><td>股 票 ET Fs REI Ts</td><td>X</td><td>X</td><td>X</td><td>X</td><td>X</td><td>X</td><td>X</td><td>X</td></tr><tr><td>期 货</td><td></td><td></td><td></td><td>X</td><td>X</td><td>X</td><td>X</td><td>X</td><td>X</td></tr><tr><td>澳 大 利 亚 市 场</td><td>股 票 ET Fs</td><td>X</td><td>X</td><td>X</td><td>X</td><td>X</td><td>X</td><td>X</td><td>X</td></tr></table></body></html>  

# #交易方式  

真实交易和模拟交易使用同一套交易接口。  

# #特点  

1. 全平台多语言：  

OpenD 支持 Windows、MacOS、CentOS、UbuntuFutu API 支持 Python、Java、C#、 $C++$ 、JavaScript 等主流语言  

2. 稳定极速免费：  

稳定的技术架构，直连交易所一触即达下单最快只需 0.0014 s  

通过 OpenAPI 交易无附加收费  

3. 丰富的投资品类：  
支持美国、香港等多个市场的实时行情、实盘交易及模拟交易  
4. 专业的机构服务：定制化的行情交易解决方案  

# 权限和限制  

# #登录限制  

# #开户限制  

首先，您需要先在富途牛牛 APP 上，完成交易业务账户的开通，才能成功登录OpenAPI。  

# #合规确认  

首次登录成功后，您需要完成问卷评估与协议确认，才能继续使用 OpenAPI。  
牛牛用户请 点击这里。  

# #行情数据  

行情数据的限制主要体现在以下几方面：  

行情权限 获取相关行情数据的权限  

接口限频 调用行情接口的频率限制  

订阅额度 同时订阅的实时行情的数量  

历史 K 线额度 —— 每 30 天最多可拉取多少个标的的历史 K 线  

# #行情权限  

通过 OpenAPI 获取行情数据，需要相应的行情权限，OpenAPI 的行情权限跟APP 的行情权限不完全一样，不同的权限等级对应不同的时延、摆盘档数以及接口使用权限。  

部分品种行情，需要购买行情卡后方可获取，具体获取方式见下表。  

<html><body><table><tr><td>市 场</td><td>标的类别</td><td>获取方式</td></tr><tr><td rowspan="5">香 港 市 场</td><td>证券类产品（含 股票、ETFs、窝 轮、牛熊、界内</td><td>*中国内地 IP 客户：免费获取 LV2 行情。 如需获得SF权限，请购买 港股高级全盘 行情</td></tr><tr><td>证） 指数</td><td rowspan="2">*港澳台及海外 IP客户：免费获取BMP行 情。如需获得 LV2 权限，请购买港股 LV2高级行情。如需获得SF 权限，请购 买 港股高级全盘行情</td></tr><tr><td>板块</td></tr><tr><td>期权</td><td>*中国内地IP客户：推广期免费获取LV2 行情 *港澳台及海外 IP客户：免费获取 BMP行</td></tr><tr><td>期货</td><td>情，如需获得LV2 权限，请购买 港股期 权期货 LV2高级行情</td></tr><tr><td>美 国</td><td>证券类产品（含 纽交所、美交 所、纳斯达克上</td><td>*如需获得LV1权限（基本报价），请购 买 Nasdaq Basic *如需获得LV2权限（基本报价+深度摆</td></tr></table></body></html>  

![](FutuAPI/6d7c55312ce1d429843d12c3ea6601403860ce48ccd968db4852c3d892c1b7cb.jpg)  

<html><body><table><tr><td>市 场</td><td>板块</td><td>*港澳台及海外IP客户/机构客户：暂不支 持</td></tr><tr><td>新加坡市场</td><td>期货</td><td>暂不支持获取</td></tr><tr><td>日本市场</td><td>期货</td><td>暂不支持获取</td></tr></table></body></html>  

# 提示  

上述表格，中国内地IP 客户和港澳台及海外IP 客户，以 OpenD 登录的 IP地址作为区分依据。  

# #接口限频  

为保护服务器，防止恶意攻击，所有需要向富途服务器发送请求的接口，都会有频率限制。  

每个接口的限频规则会有不同，具体请参见每个接口页面下面的 接口限制。  

举例：  

快照 接口的限频规则是：每 30 秒内最多请求 60 次快照。您可以每隔 0.5秒请求一次匀速请求，也可以快速请求 60 次后，休息 30 秒，再请求下一轮。如果超出限频规则，接口会返回错误。  

# #订阅额度 & 历史 K 线额度  

订阅额度和历史 K 线额度限制如下：  

![](FutuAPI/b946035be46f6c51364d341cf5fb78d1891b4b43d75ef97dd2b95c9a92841e12.jpg)  

# 1、总资产  

总资产，是指您在富途证券的所有资产，包括：港、美、A 股证券账户和期货账户，按照即时汇率换算成以港元为单位。  

# 2、月交易笔数  

月交易笔数，会综合您在富途证券的证券账户和期货账户，在当前自然月与上一自然月的交易情况，取您上个自然月的成交笔数与当前自然月的成交笔数的较大值进行计算，即：  

max (上个自然月的成交笔数，当前自然月的成交笔数)。  

# 3、月交易额  

月交易额，会综合您在富途证券的证券账户和期货账户，在当前自然月与上一自然月的交易情况，取您上个自然月的成交总金额与当前自然月的成交总金额的较大值进行计算，即：  

max（上个自然月的成交总金额，当前自然月的成交总金额）  

按照即期汇率换算成以港币为单位。其中，期货交易额的计算，需要乘以相应  

的调整系数（默认取 0.1），期货交易额计算公式如下：  

期货交易额 $\mathbf{\Psi}=\pmb{\Sigma}$ （单笔成交数 \* 成交价 \* 合约乘数 \* 汇率 \* 调整系数）  

# 4、订阅额度  

订阅额度，适用于 订阅 接口。每只股票订阅一个类型即占用 1 个订阅额度，取消订阅会释放已占用的额度。 举例：  

假设您的订阅额度是 100。 当您同时订阅了 HK.00700 的实时摆盘、US.AAPL的实时逐笔、SH.600519 的实时报价时，此时订阅额度会占用 3 个，剩余的订阅额度为 97。 这时，如果您取消了 HK.00700 的实时摆盘订阅，您的订阅额度占用将变成 2 个，剩余订阅额度会变成 98。  

# 5、历史 K 线额度  

历史 K 线额度，适用于 获取历史 K 线 接口。最近 30 天内，每请求 1 只股票的历史 K 线，将会占用 1 个历史 K 线额度。最近 30 天内重复请求同一只股票的历史 K 线，不会重复累计。 同时，订阅同一股票的不同周期的K 线只占用1 个额度，不会重复累计。 举例：  

假设您的历史 K 线额度是 100，今天是 2020 年 7 月 5 日。 您在 2020 年6 月 5 日\~2020 年 7 月 5 日之间，共计请求了 60 只股票的历史 K 线，则剩余的历史 K 线额度为 40。  

# 提示  

订阅额度和历史 K 线额度为系统自动分配，不需要手动申请。  

新入金的账户，额度等级会在 2 小时内自动生效。  

在途资产  

![](FutuAPI/d365e5159d9ea14dda7ca4a79c698852e6a0b17393358c45dc8be050cd0a6d6a.jpg)  

不会用于额度计算。  

# #交易功能  

进行指定市场的交易时，需要先确认是否已开通该市场的交易业务账户。  
举例：您只能在美股交易业务账户下进行美股交易，无法在港股交易业务账户下进行美股交易。  

# 费用  

# #行情  

中国内地 IP 个人客户，免费获取港股市场 LV2 行情及 A 股市场 LV1 行情。  

部分品种行情，需要购买行情卡后方可获取。您可以在 行情权限 一节，进入具体的行情卡购买页面查看价格。  

# #交易  

通过 OpenAPI 进行交易，无附加收费，交易费用与通过 APP 交易的费用一致。具体收费方案如下表：  

<html><body><table><tr><td>所属券商</td><td>收费方案</td></tr><tr><td>富途证券(香港)</td><td>收费方案</td></tr><tr><td>moomoo证券(美国)</td><td>收费方案</td></tr></table></body></html>  

<html><body><table><tr><td>所属券商</td><td>收费方案</td></tr><tr><td>证券(新加坡) moomoo</td><td>收费方案</td></tr><tr><td>moomoo 证券(澳大利亚)</td><td>收费方案</td></tr></table></body></html>  

# 可视化 OpenD  

OpenD 提供可视化和命令行两种运行方式，这里介绍操作比较简单的可视化OpenD。  

如果想要了解命令行的方式请参考 命令行 OpenD  

# #可视化 OpenD  

# #第一步 下载  

可视化 OpenD 支持 Windows、MacOS、CentOS、Ubuntu 四种系统（点击完成下载）。  

OpenD - Windows、MacOS 、CenOS 、Ubuntu  

# #第二步 安装运行  

解压文件，找到对应的安装文件可一键安装运行。  
Windows 系统默认安装在 %appdata% 目录下。  

#第三步 配置  

可视化 OpenD 启动配置在图形界面的右侧，如下图所示：  

![](FutuAPI/6461f0131c26c08a9c4af2301d4212b6323f919b8a5c3efe9e6bf40f9ff2b25a.jpg)  

![](FutuAPI/2b76a56311d13d902f1e3ba68acfca297577066719e99a667379b543db35f508.jpg)  

<html><body><table><tr><td>配置项</td><td>说明</td></tr><tr><td></td><td></td></tr><tr><td>API推送频率</td><td>API订阅数据推送频率控制</td></tr><tr><td>Telnet 地址</td><td>远程操作命令监听地址</td></tr><tr><td>Telnet 端口</td><td>远程操作命令监听端口</td></tr><tr><td>加密私钥路径</td><td>API 协议 RSA 加密私钥（PKCS#1）文件绝对路 径</td></tr><tr><td>WebSocket监听地 址</td><td>WebSocket服务监听地址</td></tr><tr><td>WebSocket 端口</td><td>WebSocket服务监听端口</td></tr><tr><td>WebSocket 证书</td><td>WebSocket证书文件路径</td></tr><tr><td>WebSocket私钥</td><td>WebSocket证书私钥文件路径</td></tr><tr><td>WebSocket鉴权密 钥</td><td>密钥密文（32 位 MD5 加密 16 进制)</td></tr></table></body></html>  

# 提示  

可视化 OpenD，是通过启动命令行 OpenD 来提供服务，且通过WebSocket 与命令行 OpenD 交互，所以必定启动 WebSocket 功能。为保证您的证券业务账户安全，如果监听地址不是本地，您必须配置私钥才能使用交易接口。行情接口不受此限制。  

当 WebSocket 监听地址不是本地，需配置 SSL 才可以启动，且证书私钥生成不可设置密码。  

密文是明文经过 32 位 MD5 加密后用 16 进制表示的数据，搜索在线MD5 加密（注意，通过第三方网站计算可能有记录撞库的风险）或下载 MD5 计算工具可计算得到。32 位 MD5 密文如下图红框区域（e10adc3949ba59abbe56e057f20f883e）：  

![](FutuAPI/8c9060f0af9c4c0505d2be9483fbb21787f3f87d9a4bc7b27e818c4a0056e49a.jpg)  

OpenD 默认读取同目录下的 OpenD.xml。在 MacOS 上，由于系统保护机制，OpenD.app 在运行时会被分配一个随机路径，导致无法找到原本的路径。此时有以下方法：  

执行 tar 包下的 fixrun.sho 用命令行参数-cfg_file 指定配置文件路径，见下面说明日志级别默认 info 级别，在系统开发阶段，不建议关闭日志或者将日志修改到 warning，error，fatal 级别，防止出现问题时无法定位。  

# #第四步 登录  

输入账号密码，点击登录。  

首次登录，您需要先完成问卷评估与协议确认，完成后重新登录即可。  
登录成功后，您可以看到自己的账号信息和 行情权限。  

# 编程环境搭建  

注意  

不同的编程语言，编程环境搭建的方法有所不同。  

# #Python 环境  

# #环境要求  

操作系统要求：Windows 7/10 的 32 或 64 位操作系统Mac 10.11 及以上的 64 位操作系统o CentOS 7 及以上的 64 位操作系统Ubuntu 16.04 以上的 64 位操作系统  
Python 版本要求：o Python 3.6 及以上  

# #环境搭建  

# #1. 安装 Python  

为避免因环境问题导致的运行失败，我们推荐 Python 3.8 版本。  

下载地址：Python 下载  

提示  

![](FutuAPI/291e5fde41c809b90a1d0ee84ceff533648955e707b65975478c16a6cde0d4d9.jpg)  

当安装成功后，执行如下命令来查看是否安装成功:  

python -V（Windows） 或 python3 -V（Linux 和 Mac）  

# #2. 安装 PyCharm（可选）  

我们推荐您使用 PyCharm 作为 Python IDE（集成开发环境）。  

# #3. 安装 TA-Lib（可选）  

TA-Lib 用中文可以称作技术分析库，是一种广泛用在程序化交易中，进行金融市场数据的技术分析的函数库。它提供了多种技术分析的函数，方便我们量化投资中编程工作。  

安装方法：在 cmd 中直接使用 pip 安装  

# $\oint$ pip install TA-Lib  

提示  

# 简易程序运行  

#Python 示例  

#第一步：下载安装登录 OpenD  

请参考 这里，完成 OpenD 的下载、安装和登录。  

# #第二步：下载 Python API  

方式一：在 cmd 中直接使用 pip 安装。初次安装：Windows 系统 $\oint$ pip install futu-api，Linux/Mac 系统 $\oint$ pip3 install futu-api。二次升级：Windows 系统 $\oint$ pip install futu-api --upgrade，Linux/Mac 系统 $\oint$ pip3 install futu-api --upgrade。  

方式二：点击下载最新版本的 Python API 安装包。  

# #第三步：创建新项目  

打开 PyCharm，在 Welcome to PyCharm 窗口中，点击 New Project。如果你已经创建了一个项目，可以选择打开该项目。  

![](FutuAPI/bfc13b128a01f77ea9c71d71adbace301ef186d92ef43aed7d5ef0c9f5b7a1aa.jpg)  

# #第四步：创建新文件  

在该项目下，创建新 Python 文件，并把下面的示例代码拷贝到文件里。  
示例代码功能包括查看行情快照、模拟交易下单。  

from futu import \*  

quote_ctx $=$ OpenQuoteContext(host='127.0.0.1', port $=$ 11111) #  
创建行情对象  
print(quote_ctx.get_market_snapshot('HK.00700')) # 获取港股  
HK.00700 的快照数据  
quote_ctx.close() # 关闭对象，防止连接条数用尽  
trd_ctx $=$ OpenSecTradeContext(host $=$ '127.0.0.1', port $=$ 11111) #  
创建交易对象  
print(trd_ctx.place_order(price=500.0, qty=100,  
code $^{1=}$ "HK.00700", trd_side $^{1=}$ TrdSide.BUY,  
trd_env $:=$ TrdEnv.SIMULATE)) # 模拟交易，下单（如果是真实环境交易，  
在此之前需要先解锁交易密码）  

trd_ctx.close() # 关闭对象，防止连接条数用尽  

# #第五步：运行文件  

右键点击运行，可以看到运行成功的返回信息如下：  

2020-11-05 17:09:29,705 [open_context_base.py] _socket_reconnect_and_wait_ready:255: Start connecting: host $=$ 127.0.0.1; port $\equiv$ 11111;  

2020-11-05 17:09:29,705 [open_context_base.py] on_connected:344: Connected : conn_id $=\!1$ ; 2020-11-05 17:09:29,706 [open_context_base.py] _handle_init_connect:445: InitConnect ok: conn_id $=\!1$ ;  info $=$ {'server_version':  218,  'login_user_id':  7157878,  'conn_id': 6730043337026687703, 'conn_key': '3F17CF3EEF912C92', 'conn_iv': 'C119DDDD6314F18A', 'keep_alive_interval': 10, 'is_encrypt': False};  

(0, code update_time  last_price  open_price  high_price after_high_price  after_low_price  after_change_val  after_change_rate  after_amplitude  

0 HK.00700 2020-11-05 16:08:06 625.0 610.0 625.0  

N/A N/A N/A N/A N/A  

[1 rows x 132 columns])  

2020-11-05 17:09:29,739 [open_context_base.py] _socket_reconnect_and_wait_ready:255: Start connecting: host $\because$ 127.0.0.1; port $\because$ 11111;  

2020-11-05 17:09:29,739 [network_manager.py] work:366: Close: conn_id $=\!1$ 2020-11-05 17:09:29,739 [open_context_base.py] on_connected:344: Connected : conn_id $=\!2$ ; 2020-11-05 17:09:29,740 [open_context_base.py] _handle_init_connect:445: InitConnect ok: conn_id $=\!2$ ;  info $=.$ {'server_version':  218,  'login_user_id':  7157878,  'conn_id': 6730043337169705045, 'conn_key': 'A624CF3EEF91703C', 'conn_iv': 'BF1FF3806414617B', 'keep_alive_interval': 10, 'is_encrypt': False};  

(0, code stock_name trd_side order_type order_status ... dealt_avg_price last_err_msg  remark time_in_force fill_outside_rth  

0 HK.00700 腾讯控股 BUY NORMAL SUBMITTING   
0.0 DAY N/A  

[1 rows x 16 columns])  

2020-11-05 17:09:32,843 [network_manager.py] work:366: Close: conn_id $=\!2$ (0, code stock_name trd_side order_type order_status  ... dealt_avg_price last_err_msg  remark time_in_force fill_outside_rth  

0 HK.00700 腾讯控股 BUY ABSOLUTE_LIMIT SUBMITTED   
0.0 DAY N/A  

[1 rows x 16 columns])  

# 交易策略搭建示例  

提示  

以下交易策略不构成投资建议，仅供学习参考。  

# #策略概述  

构建一个双均线策略：  

运用某一标的1 分 K 线，计算出两条不同周期的移动平均线 MA1 和 MA3，跟踪 MA1 和 MA3 的相对大小，由此判断买卖时机。  

当 $\mathsf{M A}1\,>\,=\,\mathsf{M A}3$ 时，判断该标的为强势状态，市场属于多头市场，采取开仓的操作；  

当 $\mathsf{M A}\mathbb{1}\,<\,\mathsf{M A}\mathbb{1}$ 时，判断该标的为弱势状态，市场属于空头市场，采取平仓的操作。  

# #流程图  

![](FutuAPI/2a7974a7a4647c4908d1003ff43de54e1cc211dedf8e8f03257ad6954582fee6.jpg)  

# #代码示例  

Example from futu import $\star$  

############################ 全 局 变 量 设 置  

############################  

FUTUOPEND_ADDRESS $=$ '127.0.0.1'  # OpenD 监听地址 FUTUOPEND_PORT $=$ 11111  # OpenD 监听端口  

TRADING_ENVIRONMENT $=$ TrdEnv.SIMULATE  # 交易环境：真实 / 模拟  
TRADING_MARKET $=$ TrdMarket.HK  # 交易市场权限，用于筛选对应交易市场权限的账户  
TRADING_P $\mathrm{\DeltaVD}={\mathrm{}}^{\prime}123456^{\prime}$ # 交易密码，用于解锁交易  
TRADING_PERIOD $=\mathsf{K L T y}$ pe.K_1M  # 信号 K 线周期  
TRADING_SECURIT $r=\mathrm{^\primeHK}.00700^{\circ}$ # 交易标的  
FAST_MOVING_AVERAGE $=1$ # 均线快线的周期  
SLOW_MOVING_AVERAGE $=3$ # 均线慢线的周期quote_context $=$ OpenQuoteContext(host $\equiv$ FUTUOPEND_ADDRESS,port $\equiv$ FUTUOPEND_PORT)  # 行情对象  
trade_context $=$ OpenSecTradeContext(filter_trdmarket $=$ TRADING_MARKET,host $\equiv$ FUTUOPEND_ADDRESS, port $\because$ FUTUOPEND_PORT,security_firm $=$ SecurityFirm.FUTUSECURITIES)  # 交易对象，根据交易品种修改交易对象类型  

# # 解锁交易  

def unlock_trade():  

if TRADING_ENVIRONMENT $==$ TrdEnv.REAL: ret, data $=$ trade_context.unlock_trade(TRADING_PWD) if ret $\begin{array}{r}{!=\mathsf{R E T}\_\mathrm{OK}\mathrm{:}}\end{array}$ print('解锁交易失败：', data) return False print('解锁交易成功！')   
return True  

# # 获取市场状态  

def is_normal_trading_time(code): ret, data $=$ quote_context.get_market_state([code]) if ret ! $\vDash$ RET_OK: print('获取市场状态失败：', data) return False market_state $=$ data['market_state'][0] 1 MarketState.MORNING 港、A 股早盘 MarketState.AFTERNOON 港、A 股下午盘，美股全天 MarketState.FUTURE_DAY_OPEN 港、新、日期货日市开盘 MarketState.FUTURE_OPEN 美期货开盘 MarketState.FUTURE_BREAK_OVER 美期货休息后开盘 MarketState.NIGHT_OPEN 港、新、日期货夜市开盘  

if market_state $==$ MarketState.MORNING or \ market_state $==$ MarketState.AFTERNOON or \ market_state $==$ MarketState.FUTURE_DAY_OPEN  or \ market_state $==$ MarketState.FUTURE_OPEN  or \ market_state $==$ MarketState.FUTURE_BREAK_OVER  or \ market_state $==$ MarketState.NIGHT_OPEN: return True   
print('现在不是持续交易时段。')   
return False  

# # 获取持仓数量  

def get_holding_position(code):  

holding_position $=0$ ret, data $=$ trade_context.position_list_query(code $:=$ code,  

trd_env $:=$ TRADING_ENVIRONMENT)if ret ! $\vDash$ RET_OK:print('获取持仓数据失败：', data)return Noneelse:for qty in data['qty'].values.tolist():holding_position $+=$ qtyprint(' 【持仓状态】 {} 的持仓数量为：{}'.format(TRADING_SECURITY,  
holding_position))return holding_position  

# # 拉取 K 线，计算均线，判断多空  

def calculate_bull_bear(code, fast_param, slow_param): if fast_param $<=0$ or slow_param $<=0$ : return 0 if fast_param $>$ slow_param: return calculate_bull_bear(code, slow_param, fast_param) ret,  data $=$ quote_context.get_cur_kline(code $=$ code,  num $=$ slow_param  +  1,   
ktype $:=$ TRADING_PERIOD) if ret ! $!=$ RET_OK: print('获取K 线失败：', data) return 0 candlestick_list $=$ data['close'].values.tolist()[::-1] fast_value $=$ None slow_value $=$ None if len(candlestick_list) $>$ fast_param: fast_value $=$ sum(candlestick_list[1: fast_param $+\ 1]$ ) / fast_param   
if len(candlestick_list) $>$ slow_param: slow_value $=$ sum(candlestick_list[1: slow_param $+$ 1]) / slow_param   
if fast_value is None or slow_value is None: return 0   
return 1 if fast_value $>=$ slow_value else -1  

# # 获取一档摆盘的 ask1 和 bid1  

def get_ask_and_bid(code): ret, data $=$ quote_context.get_order_book(code, num $=\!1$ ) if ret ! $!=$ RET_OK: print('获取摆盘数据失败：', data) return None, None return data['Ask'][0][0], data['Bid'][0][0]  

# # 开仓函数  

def open_position(code):  

# 获取摆盘数据ask, bid $=$ get_ask_and_bid(code)  

# 计算下单量open_quantity $=$ calculate_quantity()  

# # 判断购买力是否足够  

if is_valid_quantity(TRADING_SECURITY, open_quantity, ask): # 下单 ret, data $=$ trade_context.place_order(price $=$ ask, qty $:=$ open_quantity, code $=$ code,  

order_type $=$ OrderType.NORMAL,  

trd_env $:=$ TRADING_ENVIRONMENT, remark $\equiv$ 'moving_average_strategy') if ret $!=$ RET_OK: print('开仓失败：', data) else: print('下单数量超出最大可买数量。')  

# # 平仓函数  

def close_position(code, quantity):  

# 获取摆盘数据ask, bid $=$ get_ask_and_bid(code)  

# 检查平仓数量 if quantity $==0$ : print('无效的下单数量。') return False  

# 平仓 ret, data $=$ trade_context.place_order(price $=$ bid, qty $=$ quantity,  code $:=$ code,   
trd_side $=$ TrdSide.SELL, order_type $=$ OrderType.NORMAL, trd_env $:=$ TRADING_ENVIRONMENT,   
remark $\mathrel{\mathop:}$ moving_average_strategy') if ret ! $=$ RET_OK: print('平仓失败：', data) return False return True  

# # 计算下单数量  

def calculate_quantity():price_quantity $=0$ # 使用最小交易量ret, data $=$ quote_context.get_market_snapshot([TRADING_SECURITY])if ret ! $!=$ RET_OK:print('获取快照失败：', data)return price_quantityprice_quantity $=$ data['lot_size'][0]return price_quantity  

# # 判断购买力是否足够  

def is_valid_quantity(code, quantity, price): ret,  data $=$ trade_context.acctradinginfo_query(order_type $=$ OrderType.NORMAL,   
code $=$ code, price $=$ price,  

trd_env $:=$ TRADING_ENVIRONMENT) if ret ! $\vDash$ RET_OK: print('获取最大可买可卖失败：', data) return False max_can_buy $=$ data['max_cash_buy'][0] max_can_sell $=$ data['max_sell_short'][0] if quantity $>0$ : return quantity $<$ max_can_buy elif quantity $<0$ : return abs(quantity) $<$ max_can_sell else: return False  

# # 展示订单回调  

def show_order_status(data): order_status $=$ data['order_status'][0] order_info $=$ dict() order_info['代码'] $=$ data['code'][0] order_info['价格'] $=$ data['price'][0] order_info['方向'] $=$ data['trd_side'][0] order_info['数量'] $=$ data['qty'][0] print('【订单状态】', order_status, order_info)  

############################  填充以 下函 数来 完成 您的 策略 ############################  

# 策略启动时运行一次，用于初始化策略def on_init():  

# 解锁交易（如果是模拟交易则不需要解锁）  
if not unlock_trade():return False  
print('\*\*\*\*\*\*\*\*\*\*\*\* 策略开始运行 \*\*\*\*\*\*\*\*\*\*\*')  
return True  

# 每个 tick 运行一次，可将策略的主要逻辑写在此处  

def on_tick():  

pass  

# # 每次产生一根新的 K 线运行一次，可将策略的主要逻辑写在此处  

# 打印分隔线print('\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*')  

# # 只在常规交易时段交易  

if not is_normal_trading_time(TRADING_SECURITY):return  

# 获取 K 线，计算均线，判断多空  

bull_or_bear $=$ calculate_bull_bear(TRADING_SECURITY,  FAST_MOVING_AVERAGE, SLOW_MOVING_AVERAGE)  

# 获取持仓数量 holding_position $=$ get_holding_position(TRADING_SECURITY)  

# # 下单判断  

if holding_position $==0$ :if bull_or_bear $==1$ :print('【操作信号】 做多信号，建立多单。')open_position(TRADING_SECURITY)else:print('【操作信号】 做空信号，不开空单。')  
elif holding_position $>0$ :if bull_or_bear $==-1$ :print('【操作信号】 做空信号，平掉持仓。')close_position(TRADING_SECURITY, holding_position)else:print('【操作信号】 做多信号，无需加仓。')  

# # 委托成交有变化时运行一次  

def on_fill(data):  

pass  

# # 订单状态有变化时运行一次  

def on_order_status(data): if data['code'][0] $==$ TRADING_SECURITY: show_order_status(data)  

################################  框架实现部分，可忽略不看   
###############################   
class OnTickClass(TickerHandlerBase): def on_recv_rsp(self, rsp_pb): on_tick()  

class OnBarClass(CurKlineHandlerBase):  

last_time $=$ None   
def on_recv_rsp(self, rsp_pb): ret_code, data $=$ super(OnBarClass, self).on_recv_rsp(rsp_pb) if ret_code $==$ RET_OK: cur_time $=$ data['time_key'][0] if cur_time ! $!=$ self.last_time and data['k_type'][0] $==$ TRADING_PERIOD: if self.last_time is not None: on_bar_open() self.last_time $=$ cur_time  

class OnOrderClass(TradeOrderHandlerBase): def on_recv_rsp(self, rsp_pb): ret, data $=$ super(OnOrderClass, self).on_recv_rsp(rsp_pb) if re $\mathrm{t==RET\_OK:}$ on_order_status( data)  

class OnFillClass(TradeDealHandlerBase): def on_recv_rsp(self, rsp_pb): ret, data $=$ super(OnFillClass, self).on_recv_rsp(rsp_pb) if ret $=={\mathsf{R E T}}\_{\mathsf{O K}:}$ on_fill(data)  

# # 主函数  

if __name__ $==$ '__main__':  

# 初始化策略  
if not on_init():print('策略初始化失败，脚本退出！')quote_context.close()trade_context.close()  
else:# 设置回调quote_context.set_handler(OnTickClass())quote_context.set_handler(OnBarClass())trade_context.set_handler(OnOrderClass())trade_context.set_handler(OnFillClass())# 订阅标的合约的 逐笔，K 线和摆盘，以便获取数据quote_context.subscribe(code_list $\equiv$ [TRADING_SECURITY],$\equiv$  

subtype_list [SubType.TICKER, SubType.ORDER_BOOK, TRADING_PERIOD])  

# Output  

\*\*\*\*\*\*\*\*\*\*\*\* 策略开始运行 \*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*  

【持仓状态】 $\mathsf{H K}.00700$ 的持仓数量为：0  
【操作信号】 做多信号，建立多单。  
【订单状态】 SUBMITTING {'代码': 'HK.00700', '价格': 597.5, '方向': 'BUY', '数量': 100.0}  

【订单状态】 SUBMITTED {'代码': 'HK.00700', '价格': 597.5, '方向': 'BUY', '数量': 100.0}【订单状态】 FILLED_ALL {'代码': 'HK.00700', '价格': 597.5, '方向': 'BUY', '数量': 100.0}  

【持仓状态】 HK.00700 的持仓数量为：100.0  
【操作信号】 做空信号，平掉持仓。  
【订单状态】 SUBMITTING {'代码': 'HK.00700', '价格': 596.5, '方向': 'SELL', '数量': 100.0}【订单状态】 SUBMITTED {'代码': 'HK.00700', '价格': 596.5, '方向': 'SELL', '数量': 100.0}【订单状态】 FILLED_ALL {'代码': 'HK.00700', '价格': 596.5, '方向': 'SELL', '数量': 100.0}  

# 概述  

OpenD 是 Futu API 的网关程序，运行于您的本地电脑或云端服务器，负责中转协议请求到富途服务器，并将处理后的数据返回。是运行 FutuAPI 程序必要的前提。  
OpenD 支持 Windows、MacOS、CentOS、Ubuntu 四个平台。  
OpenD 集成了登录功能。运行时，需要使用 平台账号（牛牛号）和 登录密码 进行登录。  
OpenD 登录成功后，会启动 Socket 服务以供 Futu API 连接和通信。  

# #运行方式  

OpenD 目前提供两种安装运行方式，您可选择任一方式：  

可视化 OpenD：提供界面化应用程序，操作便捷，尤其适合入门用户，安装和运行请参考 可视化 OpenD。  
命令行 OpenD：提供命令行执行程序，需自行进行配置，适合对命令行熟悉或长时间在服务器上挂机的用户，安装和运行请参考 命令行OpenD。  

# #运行时操作  

OpenD 在运行过程中，可以查看用户额度、行情权限、链接状态、延迟统计，以及操作关闭 API 连接、重登录、退出登录等运维操作。具体方法可以查看下表：  

<html><body><table><tr><td>方式</td><td>可视化 OpenD</td><td>命令行 OpenD</td></tr><tr><td>直接方 式</td><td>界面查看或操作</td><td>命令行发送 运维命令</td></tr><tr><td>间接方 式</td><td>通过 Telnet 发送 运维命 令</td><td>通过 Telnet 发送 运维命 令</td></tr></table></body></html>  

# 命令行 OpenD  

# #第一步 下载  

命令行 OpenD 支持 Windows、MacOS、CentOS、Ubuntu 四种系统（点击完成下载）。  

OpenD - Windows、MacOS 、CentOS 、Ubuntu  

# #第二步 解压  

解压上一步下载的文件，在文件夹中找到 OpenD 配置文件  
FutuOpenD.xml 和程序打包数据文件 Appdata.dat。o FutuOpenD.xml 用于配置 OpenD 程序启动参数，若不存在则程序无法正常启动。  

o Appdata.dat 是程序需要用到的一些数据量较大的信息，打包数据减少启动下载该数据的耗时，若不存在则程序无法正常启动。  

命令行 OpenD 支持用户自定义文件路径，详见 命令行启动参数。  

# #第三步 参数配置  

打开并编辑配置文件 FutuOpenD.xml，如下图所示。普通使用仅需修改账号和登录密码，其他高阶选项可以根据下表的提示进行修改。  

![](FutuAPI/7c5ee1f299cadfa7626db6d5534c618e8e58807b3d511be799d01fd46b482cbe.jpg)  

# 配置项列表：  

<html><body><table><tr><td>配置项</td><td>说明</td></tr><tr><td>ip</td><td>监听地址</td></tr><tr><td>api_port</td><td>API协议接收端口</td></tr><tr><td>login_account</td><td>登录帐号</td></tr></table></body></html>  

![](FutuAPI/ca86299e33dd6ee66bf298e18c04e8d1b7276853a6e72094c0ef41be22965ef8.jpg)  

![](FutuAPI/0bb765cfdeed2f432cdf4bb38319b1cef474ec79a0ab231f85c1e75ff9a284ca.jpg)  

为保证您的证券业务账户安全，如果监听地址不是本地，您必须配置私钥才能使用交易接口。行情接口不受此限制。  

当 WebSocket 监听地址不是本地，需配置 SSL 才可以启动，且证书私钥生成不可设置密码。  

密文是明文经过 32 位 MD5 加密后用 16 进制表示的数据，搜索在线MD5 加密（注意，通过第三方网站计算可能有记录撞库的风险）或下载 MD5 计算工具可计算得到。32 位 MD5 密文如下图红框区域（e10adc3949ba59abbe56e057f20f883e）：  

![](FutuAPI/3c1d902380776ea683c3ecd576a70f971272c7b83dffd6df3ee3b4202de4cb7e.jpg)  

OpenD 默认读取同目录下的 FutuOpenD.xml。在 MacOS 上，由于系统保护机制，OpenD.app 在运行时会被分配一个随机路径，导致无法找到原本的路径。此时有以下方法：  

执行 tar 包下的 fixrun.sh用命令行参数-cfg_file 指定配置文件路径，见下面说明日志级别默认 info 级别，在系统开发阶段，不建议关闭日志或者将日志修改到 warning，error，fatal 级别，防止出现问题时无法定位。  

# #第四步 命令行启动  

在命令行中切到前面解压文件夹 OpenD 文件所在的目录，使用如下命令启动，即可以 FutuOpenD.xml 配置文件中的参数启动。  

Windows：FutuOpenD   
Linux：./FutuOpenD   
MacOS：./FutuOpenD.app/Contents/MacOS/FutuOpenD  

命令行启动参数  

$\leftarrow$ 概述运维命令 $\rightarrow$  

命令行 OpenD  

# 运维命令  

通过命令行或者 Telnet 发送命令可以对 OpenD 做运维操作。  

命令格式：cmd -param_key1=param_value1 -param_key2=param_value2以 help -cmd=exit 为例，介绍Telnet 的用法：  

1. 在OpenD 启动参数中，配置好 Telnet 地址和 Telnet 端口。  

![](FutuAPI/77c9ddec02190444317c6ae43eee89e1672a32c4a02435e1cca2d856c30942df.jpg)  

![](FutuAPI/a74946a9eb3894693b5d24a87504e9e3cd370f8da28641f18638e42d93fd874a.jpg)  

# 2. 启动 OpenD（会同时启动 Telnet）。  

3. 通过 Telnet，向 OpenD 发送 help -cmd=exit 命令。  

from telnetlib import Telnet  

with Telnet('127.0.0.1', 22222) as tn:  # Telnet 地址为：127.0.0.1，Telnet   
端口为：22222 tn.write(b'help -cmd $=$ exit\r\n') $\Gamma\mathsf{e p l y}~=~\mathsf{b}^{\prime}$ ' while True: msg $=$ tn.read_until(b'\r\n', timeout $=\!\theta\cdot5$ ) reply $\scriptstyle+=$ msg if $\mathsf{m s g\ =}\ \mathsf{b}^{\prime}\ \cdot$ : break print(reply.decode('gb2312')) Copied!  

![](FutuAPI/8f4a9b330bb8b52f692846f69c615da96a30b4f69d58029ce3b567aad00db1ba.jpg)  

# #命令帮助  

# help -cmd=exit  

查看指定命令详细信息，不指定参数则输出命令列表  

参数:cmd: 命令  

# #退出程序  

exit  

退出 OpenD 程序  

# #请求手机验证码  

req_phone_verify_code  

请求手机验证码，当启用设备锁并初次在该设备登录，要求做安全验证。  

频率限制:每60 秒内最多请求1 次  

# #输入手机验证码  

input_phone_verify_code -code=123456输入手机验证码，并继续登录流程。  

参数:code: 手机验证码  
频率限制:每60 秒内最多请求10 次  

# #请求图形验证码  

# req_pic_verify_code  

请求图形验证码，当多次输入错登录密码时，需要输入图形验证码。  

频率限制:每60 秒内最多请求10 次  

# #输入图形验证码  

input_pic_verify_code -code=1234输入图形验证码，并继续登录流程。  

参数:o code: 图形验证码  
频率限制:每60 秒内最多请求10 次  

# #重登录  

# relogin -login_pwd=123456  

当登录密码修改或中途打开设备锁等情况，要求用户重新登录时，可以使用该命令。只能重登当前帐号，不支持切换帐号。 密码参数主要用于登录密码修改的情况，不指定密码则使用启动时登录密码。  

参数:login_pwd: 登录密码明文login_pwd_md5: 登录密码密文（32 位 MD5 加密 16 进制）  
频率限制·  

# #检测与连接点之间的时延  

# ping  

检测与连接点之前的时延  

频率限制:每60 秒内最多请求10 次  

# #展示延迟统计报告  

show_delay_report -detail_report_path=D:/detail.txt - push_count_type=sr2cs  

展示延迟统计报告，包括推送延迟，请求延迟以及下单延迟。每日北京时间6:00 清理数据。  

参数:  

detail_report_path: 文件输出路径（MAC 系统仅支持绝对路径，  
不支持相对路径），可选参数，若不指定则输出到控制台  
Paramters: push_count_type: 推送延迟的类型(sr2ss，ss2cr，  
cr2cs，ss2cs，sr2cs)，默认 sr2cs。sr 指服务器接收时间(目前只有港股支持该时间)ss 指服务器发出时间cr 指 OpenD 接收时间cs 指 OpenD 发出时间  

# #关闭 API 连接  

close_api_conn -conn_id=123456  

关闭某条 API 连接，若不指定则关闭所有  

参数: conn_id: API 连接 ID  

# #展示订阅状态  

show_sub_info -conn_id=123456 -sub_info_path=D:/detail.txt  

展示某条连接的订阅状态，若不指定则展示所有  

参数:  

o conn_id: API 连接 ID  

o sub_info_path: 文件输出路径（MAC 系统仅支持绝对路径，不支持相对路径），可选参数，若不指定则输出到控制台  

# #请求最高行情权限  

# request_highest_quote_right  

当高级行情权限被其他设备（如：桌面端/手机端）占用时，可使用该命令重新请求最高行情权限（届时，其他处于登录状态的设备将无法使用高级行情）。  

频率限制:  

每60 秒内最多请求10 次  

# #升级  

update  

运行该命令，可以一键更新 OpenD  

行情接口总览  


<html><body><table><tr><td colspan="2">模块</td><td>接口名</td><td>功能简介</td></tr><tr><td>实时行情</td><td>订阅</td><td>subscribe unsubscribe</td><td>订阅实时数据，指定 股票代码和订阅的数 据类型即可 取消订阅</td></tr></table></body></html>  

![](FutuAPI/a847047a2ae60a7011a321e7aa6ef262e62ed6aa0d4f5558c2ec3f66b46a6b72.jpg)  

<html><body><table><tr><td rowspan="5"></td><td>get owner plate</td><td>获取单支或多支股票 的所属板块信息列表</td></tr><tr><td>request history kline</td><td>获取 K 线，不需要事 先下载 K 线数据</td></tr><tr><td>get rehab</td><td>获取给定股票的复权 因子</td></tr><tr><td>get option expiration date</td><td>通过标的股票，查询 期权链的所有到期日</td></tr><tr><td>get option chain</td><td>通过标的股查询期权</td></tr><tr><td rowspan="5">相关衍生品</td><td>get warrant</td><td>拉取窝轮和相关衍生 品数据接口</td></tr><tr><td>get referencestock list</td><td>获取证券的关联数据</td></tr><tr><td>get future info</td><td>获取期货合约资料</td></tr><tr><td>get stock filter</td><td>获取条件选股</td></tr><tr><td>get plate stock</td><td>获取特定板块下的股 票列表</td></tr><tr><td rowspan="6">全市场筛选</td><td>get plate list</td><td>获取板块集合下的子 板块列表</td></tr><tr><td>get stock basicinfo</td><td>获取指定市场中特定 类型或特定股票的基</td></tr><tr><td>get ipo list</td><td>本信息 获取指定市场的 ipo 列表</td></tr><tr><td>get global state</td><td>获取全局市场状态</td></tr><tr><td>request trading days</td><td>获取交易日历</td></tr><tr><td>个性化 get history kl quota</td><td>获取已使用过的额 度，即当前周期内已 经下载过多少只股票</td></tr></table></body></html>  

<html><body><table><tr><td rowspan="6"></td><td>Set price reminder</td><td>设置到价提醒</td></tr><tr><td>get price reminder</td><td>获取对某只股票(某个 市场)设置的到价提醒 列表</td></tr><tr><td>get user_security _group</td><td>获取自选股分组列表</td></tr><tr><td>get user security</td><td>获取指定分组的自选 股列表</td></tr><tr><td>modify user security</td><td>修改指定分组的自选 股列表</td></tr><tr><td>PriceReminderHandlerBase</td><td>到价提醒推送</td></tr></table></body></html>  

# 行情对象  

#创建连接  

OpenQuoteContext(host='127.0.0.1', port $=$ 11111,is_encrypt=None)  

介绍创建并初始化行情连接  

参数  

<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>host</td><td>str</td><td>OpenD 监听的 IP 地址</td></tr><tr><td>port</td><td>int</td><td>OpenD 监听的端口</td></tr><tr><td>is_encrypt</td><td>bool</td><td>是否启用加密</td></tr></table></body></html>  

Example  

from import \* $=$ ='127.0.0.1', =11111, $=$ False) () # 结束后记得关闭当条连接，防止连接条数用尽 Copied!  

# #关闭连接  

# close()  

介绍  

关闭行情接口类对象。默认情况下，Futu API 内部创建的线程会阻止进程退出，只有当所有 Context 都 close 后，进程才能正常退出。但通过 set_all_thread_daemon 可以设置所有内部线程为 daemon 线程，这时即使没有调用 Context 的 close，进程也可以正常退出。  

# Example  

from import \* $=$ ='127.0.0.1', =11111) () # 结束后记得关闭当条连接，防止连接条数用尽 Copied!  

# #启动  

start()  

介绍启动异步接收推送数据  

# #停止  

# stop()  

介绍停止异步接收推送数据  

# 订阅反订阅  

#订阅  

subscribe(code_list, subtype_list, is_first_push=True, subscribe_push=True, is_detailed_orderbook $\equiv$ False, extended_time $=$ False)  

# 介绍  

订阅注册需要的实时信息，指定股票和订阅的数据类型即可。香港市场（含正股、窝轮、牛熊、期权、期货）订阅，需要 LV1 及以上的权限，BMP 权限下不支持订阅。  

# 参数  

<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>code_list</td><td>list</td><td>需要订阅的股票代码列表</td></tr><tr><td>subtype_list</td><td>list</td><td>需要订阅的数据类型列表</td></tr></table></body></html>  

<html><body><table><tr><td>参数</td><td>类 型</td><td>说明</td></tr><tr><td>is_first_push</td><td>bool</td><td>订阅成功之后是否立即推送一 次缓存数据</td></tr><tr><td>subscribe_push</td><td>bool</td><td>订阅后是否推送</td></tr><tr><td>is_detailed_orderbook</td><td>bool</td><td>是否订阅详细的摆盘订单明 细</td></tr><tr><td>extended_time</td><td>bool</td><td>是否允许美股盘前盘后数据</td></tr></table></body></html>  

返回  


<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>ret</td><td>RET CODE</td><td>接口调用结果</td></tr><tr><td rowspan="2">errmessage</td><td>NoneType</td><td>当 ret == RET_OK 时，返回 INone</td></tr><tr><td>str</td><td>当 ret！= RET_OK 时，返回错误描 述</td></tr></table></body></html>  

# Example  

import time  

from futu import \*  

# def on_recv_rsp(self, rsp_pb):  

ret_code, data $=$ super(OrderBookTest,self).on_recv_rsp(rsp_pb)  
if ret_code ! $!=$ RET_OK:print("OrderBookTest: error, msg: %s" % data)return RET_ERROR, data  
print("OrderBookTest ", data) # OrderBookTest 自己的处理逻辑  
return RET_OK, data  

quote_ctx $=$ OpenQuoteContext(host $\r=\r^{\prime}$ 127.0.0.1', port $=$ 11111)  

handler $=$ OrderBookTest()  

quote_ctx.set_handler(handler)  # 设置实时摆盘回调quote_ctx.subscribe(['HK.00700'], [SubType.ORDER_BOOK])  # 订阅买卖摆盘类型，OpenD 开始持续收到服务器的推送  

time.sleep(15)  #  设置脚本接收 OpenD 的推送持续时间为15 秒quote_ctx.close()  # 关闭当条连接，OpenD 会在1 分钟后自动取消相应股票相应类型的订阅  

# 获取订阅状态  

# query_subscription(is_all_conn=True)  

介绍获取订阅信息参数返回  

<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>is all conn</td><td>bool</td><td>是否返回所有连接的订阅状态</td></tr></table></body></html>  

<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>ret</td><td>RET CODE</td><td>接口调用结果</td></tr><tr><td rowspan="2">data</td><td>dict</td><td>系 ret RETOK，返回订阅信息数据</td></tr><tr><td>str</td><td>当 ret != R RETOK，返回错误描述</td></tr></table></body></html>  

订阅信息数据字典格式如下：  

'total_used': 4, # 所有连接已使用的订阅额度'own_used': 0, # 当前连接已使用的订阅额度'remain': 496, #  剩余的订阅额度'sub_list': #  每种订阅类型对应的股票列表'订阅的类型': 该订阅类型下所有已订阅股票列表,from futu import $\star$ quote_ctx $=$ OpenQuoteContext(host $=$ '127.0.0.1', port $\equiv$ 11111)  

quote_ctx.subscribe(['HK.00700'], [SubType.QUOTE])   
ret, data $=$ quote_ctx.query_subscription()   
if r $\mathfrak{z l}==\mathsf{R E T\_O K}\mathrm{:}$ print(data)  

print('error:', data) quote_ctx.close() # 结束后记得关闭当条连接，防止连接条数用尽  

# 实时报价回调  

# on_recv_rsp(self, rsp_pb)  

介绍  

实时报价回调，异步处理已订阅股票的实时报价推送。在收到实时报价数据推送后会回调到该函数，您需要在派生类中覆盖on_recv_rsp。  

参数  

<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>rsp_pb</td><td>Qot_U UpdateBasicQot_pb2.Response</td><td>派生类中不需要 直接处理该参数</td></tr></table></body></html>  

返回  


<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>ret</td><td>RET CODE</td><td>接口调用结果</td></tr><tr><td rowspan="2">data</td><td>pd.DataFrame</td><td>当 ret == RETOK，返回报价数据</td></tr><tr><td>str</td><td>当 ret!= RET OK，返回错误描述</td></tr></table></body></html>  

报价数据格式如下：  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>code</td><td>str</td><td>股票代码</td></tr><tr><td>data_date</td><td>str</td><td>日期</td></tr><tr><td>data_time</td><td>str</td><td>当前价更 新时间</td></tr><tr><td>last_price</td><td>float</td><td>最新价格</td></tr><tr><td>open_price</td><td>float</td><td>今日开盘 价</td></tr><tr><td>high_price</td><td>float</td><td>最高价格</td></tr><tr><td>low_price</td><td>float</td><td>最低价格</td></tr><tr><td>prev_close_price</td><td>float</td><td>昨收盘价 格</td></tr><tr><td>volume</td><td>int</td><td>成交数量</td></tr></table></body></html>  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>turnover</td><td>float</td><td>成交金额</td></tr><tr><td>turnover_rate</td><td>float</td><td>换手率</td></tr><tr><td>amplitude</td><td>int</td><td>振幅</td></tr><tr><td>suspension</td><td>bool</td><td>是否停 牌</td></tr><tr><td>listing_date</td><td>str</td><td>上市日 期</td></tr><tr><td>price_spread</td><td>float</td><td>当前向上 的价差</td></tr><tr><td>dark_status</td><td>DarkStatus</td><td>暗盘交易 状态</td></tr><tr><td>sec_status</td><td>SecurityStatus</td><td>股票状态</td></tr><tr><td>strike_price</td><td>float</td><td>行权价</td></tr><tr><td>contract_size</td><td>float</td><td>每份合约 数</td></tr><tr><td>open_interest</td><td>int</td><td>未平仓合 约数</td></tr><tr><td>implied_volatility</td><td>float</td><td>隐含波动 率</td></tr></table></body></html>  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>premium</td><td>float</td><td>溢价</td></tr><tr><td>delta</td><td>float</td><td>希腊值 Delta</td></tr><tr><td>gamma</td><td>float</td><td>希腊值 Gamma</td></tr><tr><td>vega</td><td>float</td><td>希腊值 Vega</td></tr><tr><td>theta</td><td>float</td><td>希腊值 Theta</td></tr><tr><td>rho</td><td>float</td><td>希腊值 Rho</td></tr><tr><td>index_option_type</td><td>IndexOptionType</td><td>指数期权 类型</td></tr><tr><td>net_open_interest</td><td>int</td><td>净未平仓 合约数</td></tr><tr><td>expiry_date_distance</td><td>int</td><td>距离到期 日天数</td></tr><tr><td>contract_nominal_value</td><td>float</td><td>合约名义 金额</td></tr><tr><td>owner_lot_multiplier</td><td>float</td><td>相等正股 手数</td></tr></table></body></html>  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>option_area_type</td><td>OptionAreaType</td><td>期权类型 （按行权 时间)</td></tr><tr><td>contract_multiplier</td><td>float</td><td>合约乘数</td></tr><tr><td>pre_price</td><td>float</td><td>盘前价格</td></tr><tr><td>pre_high_price</td><td>float</td><td>盘前最高 价</td></tr><tr><td>pre_low_price</td><td>float</td><td>盘前最低 价</td></tr><tr><td>pre_volume</td><td>int</td><td>盘前成交 量</td></tr><tr><td>pre_turnover</td><td>float</td><td>盘前成交 额</td></tr><tr><td>pre_change_val</td><td>float</td><td>盘前涨跌 额</td></tr><tr><td>pre_change_rate</td><td>float</td><td>盘前涨跌 幅</td></tr><tr><td>pre_amplitude</td><td>float</td><td>盘前振 幅</td></tr><tr><td>after_price</td><td>float</td><td>盘后价格</td></tr><tr><td>after_high_price</td><td>float</td><td>盘后最高 价</td></tr><tr><td>after_low_price</td><td>float</td><td>盘后最低 价</td></tr></table></body></html>  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>after_volume</td><td>int</td><td>盘后成交 量</td></tr><tr><td>after_turnover</td><td>float</td><td>盘后成交 额</td></tr><tr><td>after_change_val</td><td>float</td><td>盘后涨跌 额</td></tr><tr><td>after_change_rate</td><td>float</td><td>盘后涨跌 幅</td></tr><tr><td>after_amplitude</td><td>float</td><td>盘后振 幅</td></tr><tr><td>last_settle_price</td><td>float</td><td>昨结</td></tr><tr><td>position</td><td>float</td><td>持仓量</td></tr><tr><td>position_change</td><td>float</td><td>日增仓</td></tr></table></body></html>  

# Example  

import time from futu import \*  

def on_recv_rsp(self, rsp_pb): ret_code, data $=$ super(StockQuoteTest,self).on_recv_rsp(rsp_pb) if ret_code ! $!=$ RET_OK: print("StockQuoteTest: error, msg: %s" % data) return RET_ERROR, data print("StockQuoteTest ", data) # StockQuoteTest 自己的处理逻辑 return RET_OK, data  

quote_ctx $=$ OpenQuoteContext(host $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ '127.0.0.1', port $\equiv$ 11111)  
handler $=$ StockQuoteTest()  
quote_ctx.set_handler(handler)  # 设置实时报价回调  
ret, data $=$ quote_ctx.subscribe(['HK.00700'], [SubType.QUOTE])  # 订阅实时报价类型，  
OpenD 开始持续收到服务器的推送  
if re $\begin{array}{r}{\mathbf{\Psi}_{:}==\mathsf{R E T}\_{\mathsf{O K G}}.}\end{array}$ print(data)  

print('error:', data)time.sleep(15)  #  设置脚本接收 OpenD 的推送持续时间为15 秒quote_ctx.close()   # 关闭当条连接，OpenD 会在1 分钟后自动取消相应股票相应类型的订阅  

# 实时摆盘回调  

# on_recv_rsp(self, rsp_pb)  

介绍  

实时摆盘回调，异步处理已订阅股票的实时摆盘推送。 在收到实时摆盘数据推送后会回调到该函数，您需要在派生类中覆盖 on_recv_rsp。  

参数  


<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>rsp_pb</td><td>Qot_UpdateOrderBook_pb2. Response</td><td>派生类中不需 要直接处理该 参数</td></tr></table></body></html>  

返回  

<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>ret</td><td>RET CODE</td><td>接口调用结果</td></tr><tr><td rowspan="2">data</td><td>dict</td><td>当 ret RETOK，返回摆盘数据</td></tr><tr><td>str</td><td>当 ret!= RET OK，返回错误描述</td></tr></table></body></html>  

摆盘数据格式如下：  

<html><body><table><tr><td>字段</td><td>类 型</td><td>说明</td></tr><tr><td>code</td><td>str</td><td>股票代码</td></tr><tr><td>name</td><td>str</td><td>股票名称</td></tr><tr><td>svr_recv_time_bid</td><td>str</td><td>富途服务器从交易所收到买 盘数据的时间</td></tr><tr><td>svr_recv_time_ask</td><td>str</td><td>富途服务器从交易所收到卖 盘数据的时间</td></tr><tr><td>Bid</td><td>list</td><td>每个元祖包含如下信息：委 托价格，委托数量，委托订 单数，委托订单明细</td></tr><tr><td>Ask</td><td>list</td><td>每个元祖包含如下信息：委 托价格，委托数量，委托订 单数，委托订单明细</td></tr></table></body></html>  

其中，Bid 和 Ask 字段的结构如下：  

'Bid':  [  (bid_price1,  bid_volume1,  order_num,  {'orderid1':  order_volume1,  'orderid2':  

order_volume2, …… }), (bid_price2, bid_volume2, order_num,  {'orderid1': order_volume1, 'orderid2': order_volume2, …… }),…]  

'Ask':  [  (ask_price1,  ask_volume1 ，order_num,  {'orderid1':  order_volume1,  'orderid2': order_volume2, …… }), (ask_price2, ask_volume2, order_num, {'orderid1': order_volume1, 'orderid2': order_volume2, …… }),…]  

# Example  

import time from futu import $\star$  

class OrderBookTest(OrderBookHandlerBase):  

def on_recv_rsp(self, rsp_pb): ret_code, data $=$ super(OrderBookTest,self).on_recv_rsp(rsp_pb) if ret_code ! $!=$ RET_OK: print("OrderBookTest: error, msg: %s" % data) return RET_ERROR, data print("OrderBookTest ", data) # OrderBookTest 自己的处理逻辑 return RET_OK, data  

quote_ctx $=$ OpenQuoteContext(host $=$ '127.0.0.1', port $\equiv$ 11111)handler $=$ OrderBookTest()  

quote_ctx.set_handler(handler)  # 设置实时摆盘回调ret, data $=$ quote_ctx.subscribe(['HK.00700'], [SubType.ORDER_BOOK])  # 订阅买卖摆盘类型，OpenD 开始持续收到服务器的推送  

if r $\mathfrak{x}\mathfrak{t}==\mathsf{R E T\_O K}\mathrm{:}$ print(data)  

else:  

print('error:', data)time.sleep(15)  #  设置脚本接收 OpenD 的推送持续时间为15 秒quote_ctx.close()  # 关闭当条连接，OpenD 会在1 分钟后自动取消相应股票相应类型的订阅  

# 实时 K 线回调  

# on_recv_rsp(self, rsp_pb)  

介绍  

实时 K 线回调，异步处理已订阅股票的实时 K 线推送。  

在收到实时 K 线数据推送后会回调到该函数，您需要在派生类中覆盖on_recv_rsp。  

参数  


<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>rsp_pb</td><td>Qot_ _UpdateKL_pb2. Response</td><td>派生类中不需要直接处 理该参数</td></tr></table></body></html>  

返回  

<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>ret</td><td>RET CODE</td><td>接口调用结果</td></tr><tr><td rowspan="2">data</td><td>pd. DataFrame</td><td>当 ret RETOK，返回K线数据数据</td></tr><tr><td>str</td><td>当 ret!= RET_OK，返回错误描述</td></tr></table></body></html>  

K 线数据格式如下：  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>code</td><td>str</td><td>股票代码</td></tr><tr><td>name</td><td>str</td><td>股票名称</td></tr><tr><td>time_key</td><td>str</td><td>时间</td></tr><tr><td>open</td><td>float</td><td>开盘价</td></tr><tr><td>close</td><td>float</td><td>收盘价</td></tr><tr><td>high</td><td>float</td><td>最高价</td></tr><tr><td>1ow</td><td>float</td><td>最低价</td></tr></table></body></html>  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>volume</td><td>int</td><td>成交量</td></tr><tr><td>turnover</td><td>float</td><td>成交额</td></tr><tr><td>pe_ratio</td><td>float</td><td>市盈率</td></tr><tr><td>turnover_rate</td><td>float</td><td>换手率</td></tr><tr><td>last_close</td><td>float</td><td>昨收价</td></tr><tr><td>k_type</td><td>KLType</td><td>K 线类型</td></tr></table></body></html>  

# Example  

import time  
from futu import $\star$   
class CurKlineTest(CurKlineHandlerBase):def on_recv_rsp(self, rsp_pb):ret_code, data $=$ super(CurKlineTest,self).on_recv_rsp(rsp_pb)if ret_code ! $!=$ RET_OK:print("CurKlineTest: error, msg: %s" % data)return RET_ERROR, dataprint("CurKlineTest ", data) # CurKlineTest 自己的处理逻辑return RET_OK, data  
quote_ctx $=$ OpenQuoteContext(host $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ '127.0.0.1', port $\equiv$ 11111)  
handler $=$ CurKlineTest()  
quote_ctx.set_handler(handler)  # 设置实时K 线回调  
ret, data $=$ quote_ctx.subscribe(['HK.00700'], [SubType.K_1M])   # 订阅 K 线数据类型，  
OpenD 开始持续收到服务器的推送  
if re $:==\mathsf{R E T\_O K}:$ print(data)  
else:print('error:', data)  
time.sleep(15)  # 设置脚本接收 OpenD 的推送持续时间为15 秒  
quote_ctx.close()   # 关闭当条连接，OpenD 会在1 分钟后自动取消相应股票相应类型的  
订阅  

# 实时分时回调  

# on_recv_rsp(self, rsp_pb)  

介绍  

实时分时回调，异步处理已订阅股票的实时分时推送。在收到实时分时数据推送后会回调到该函数，您需要在派生类中覆盖  

on_recv_rsp。  

# 参数  

<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>rsp_pb</td><td>Qot_UpdateRT_pb2.Response</td><td>派生类中不需要直接处 理该参数</td></tr></table></body></html>  

返回  


<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>ret</td><td>RET CODE</td><td>接口调用结果</td></tr><tr><td rowspan="2">data</td><td>pd.DataFrame</td><td>当 ret RETOK，返回分时数据 二二</td></tr><tr><td>str</td><td>当 ret!= RET OK，返回错误描述</td></tr></table></body></html>  

分时数据格式如下：  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>code</td><td>str</td><td>股票代码</td></tr><tr><td>name</td><td>str</td><td>股票名称</td></tr><tr><td>time</td><td>str</td><td>时间</td></tr></table></body></html>  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>is_blank</td><td>bool</td><td>数据状态</td></tr><tr><td>opened_mins</td><td>int</td><td>零点到当前多少分钟</td></tr><tr><td>cur_price</td><td>float</td><td>当前价格</td></tr><tr><td>last_close</td><td>float</td><td>昨天收盘的价格</td></tr><tr><td>avg_price</td><td>float</td><td>平均价格</td></tr><tr><td>volume</td><td>float</td><td>成交量</td></tr><tr><td>turnover</td><td>float</td><td>成交金额</td></tr></table></body></html>  

# Example  

import time from futu import $\star$  

class RTDataTest(RTDataHandlerBase):  

def on_recv_rsp(self, rsp_pb):ret_code, data $=$ super(RTDataTest, self).on_recv_rsp(rsp_pb)if ret_code ! $!=$ RET_OK:print("RTDataTest: error, msg: %s" % data)return RET_ERROR, dataprint("RTDataTest ", data) # RTDataTest 自己的处理逻辑return RET_OK, data  

quote_ctx $=$ OpenQuoteContext(host $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ '127.0.0.1', port $\equiv$ 11111)handler $=$ RTDataTest()  

quote_ctx.set_handler(handler)  # 设置实时分时推送回调ret, data $=$ quote_ctx.subscribe(['HK.00700'], [SubType.RT_DATA]) # 订阅分时类型，OpenD开始持续收到服务器的推送  

if r $\mathsf{a t}==\mathsf{R E T\_O K}\mathrm{:}$ print(data)   
else: print('error:', data)  

time.sleep(15)  # 设置脚本接收 OpenD 的推送持续时间为15 秒quote_ctx.close()   # 关闭当条连接，OpenD 会在1 分钟后自动取消相应股票相应类型的订阅  

# 实时逐笔回调  

# on_recv_rsp(self, rsp_pb)  

介绍  

实时逐笔回调，异步处理已订阅股票的实时逐笔推送。在收到实时逐笔数据推送后会回调到该函数，您需要在派生类中覆盖  

on_recv_rsp。  

# 参数  

<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>rsp_pb</td><td>Qot_UpdateTicker_pb2. Response</td><td>派生类中不需要直 接处理该参数</td></tr></table></body></html>  

返回  


<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>ret</td><td>RET CODE</td><td>接口调用结果</td></tr><tr><td rowspan="2">data</td><td>pd. DataFrame</td><td>当 ret 二二 RETOK，返回逐笔数据</td></tr><tr><td>str</td><td>当 ret!=RET OK，返回错误描述</td></tr></table></body></html>  

逐笔数据格式如下：  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>code</td><td>str</td><td>股票代码</td></tr><tr><td>name</td><td>str</td><td>股票名称</td></tr></table></body></html>  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>sequence</td><td>int</td><td>逐笔序号</td></tr><tr><td>time</td><td>str</td><td>成交时间</td></tr><tr><td>price</td><td>float</td><td>成交价格</td></tr><tr><td>volume</td><td>int</td><td>成交数量</td></tr><tr><td>turnover</td><td>float</td><td>成交金额</td></tr><tr><td rowspan="2">ticker_direction</td><td>TickerDirect</td><td>逐笔方向</td></tr><tr><td>TickerType</td><td>逐笔类型</td></tr><tr><td>type push_data_type</td><td>PushDataType</td><td>数据来源</td></tr></table></body></html>  

# Example  

import time from futu import $\star$  

class TickerTest(TickerHandlerBase):def on_recv_rsp(self, rsp_pb):ret_code, data $=$ super(TickerTest,self).on_recv_rsp(rsp_pb)if ret_code ! $!=$ RET_OK:print("TickerTest: error, msg: %s" % data)return RET_ERROR, dataprint("TickerTest ", data) # TickerTest 自己的处理逻辑return RET_OK, data  

quote_ctx $=$ OpenQuoteContext(host $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ '127.0.0.1', port $\equiv$ 11111)handler $=$ TickerTest()  

quote_ctx.set_handler(handler)  # 设置实时逐笔推送回调  
ret, data $=$ quote_ctx.subscribe(['HK.00700'], [SubType.TICKER]) # 订阅逐笔类型，OpenD 开  
始持续收到服务器的推送  
if $\mathsf{r e t=}\mathsf{R E T\_O K}\mathrm{:}$ print(data)  

else:  

print('error:', data)time.sleep(15)  # 设置脚本接收 OpenD 的推送持续时间为15 秒quote_ctx.close()   # 关闭当条连接，OpenD 会在1 分钟后自动取消相应股票相应类型的订阅  

# 实时经纪队列回调  

# on_recv_rsp(self, rsp_pb)  

# 介绍  

实时经纪队列回调，异步处理已订阅股票的实时经纪队列推送。在收到实时经纪队列数据推送后会回调到该函数，您需要在派生类中覆盖 on_recv_rsp。  

# 参数  

<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>rsp_pb</td><td>Qot UpdateBroker_pb2.Response</td><td>派生类中不需要直 接处理该参数</td></tr></table></body></html>  

返回  


<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>ret</td><td>RET CODE</td><td>接口调用结果</td></tr><tr><td rowspan="2">data</td><td>tuple</td><td>当 ret RETOK，返回经纪队列数据 二</td></tr><tr><td>str</td><td>当 ret t！= RETOK，返回错误描述</td></tr></table></body></html>  

经纪队列元组内容如下：  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>stock code</td><td>str</td><td>股票</td></tr><tr><td>bid frame table</td><td>pd. DataFrame</td><td>买盘数据</td></tr></table></body></html>  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>ask frame table</td><td>pd. DataFrame</td><td>卖盘数据</td></tr></table></body></html>  

bid_frame_table 格式如下：  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>code</td><td>str</td><td>股票代码</td></tr><tr><td>name</td><td>str</td><td>股票名称</td></tr><tr><td>bid_broker_id</td><td>int</td><td>经纪买盘 ID</td></tr><tr><td>bid _broker_name</td><td>str</td><td>经纪买盘名称</td></tr><tr><td>bid_broker_pos</td><td>int</td><td>经纪档位</td></tr><tr><td>order_id</td><td>int</td><td>交易所订单ID</td></tr><tr><td>order_volume</td><td>int</td><td>单笔委托数量</td></tr></table></body></html>  

ask_frame_table 格式如下：  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>code</td><td>str</td><td>股票代码</td></tr><tr><td>name</td><td>str</td><td>股票名称</td></tr><tr><td>ask_broker_id</td><td>int</td><td>经纪卖盘 ID</td></tr><tr><td>ask broker name</td><td>str</td><td>经纪卖盘名称</td></tr><tr><td>ask broker_pos</td><td>int</td><td>经纪档位</td></tr></table></body></html>  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>order_id</td><td>int</td><td>交易所订单 ID</td></tr><tr><td>order_volume</td><td>int</td><td>单笔委托数量</td></tr></table></body></html>  

# Example  

import time from futu import $\star$  

class BrokerTest(BrokerHandlerBase): def on_recv_rsp(self, rsp_pb): ret_code, err_or_stock_code, data $=$ super(BrokerTest, self).on_recv_rsp(rsp_pb) if ret_code ! $!=$ RET_OK: print("BrokerTest: error, msg: {}".format(err_or_stock_code)) return RET_ERROR, data print("BrokerTest: stock: {} data: {} ".format(err_or_stock_code, data))  # BrokerTest  

自己的处理逻辑return RET_OK, data  
quote_ctx $=$ OpenQuoteContext(host $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ '127.0.0.1', port $\equiv$ 11111)  

handler $=$ BrokerTest()  

quote_ctx.set_handler(handler)  # 设置实时经纪推送回调  

ret, data $=$ quote_ctx.subscribe(['HK.00700'], [SubType.BROKER]) # 订阅经纪类型，OpenD  
开始持续收到服务器的推送  
if ret $==$ RET_OK:print(data)  

else:  

print('error:', data)time.sleep(15)  # 设置脚本接收 OpenD 的推送持续时间为15 秒quote_ctx.close()   # 关闭当条连接，OpenD 会在1 分钟后自动取消相应股票相应类型的订阅  

# 获取快照  

# get_market_snapshot(code_list)  

介绍获取快照数据  

参数  

<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>code list</td><td>list</td><td>股票代码列表</td></tr></table></body></html>  

返回  

<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>ret</td><td>RET CODE</td><td>接口调用结果</td></tr><tr><td rowspan="2">data</td><td>pd. DataFrame</td><td>当 ret RETOK，返回股票快照数据</td></tr><tr><td>str</td><td>当 ret!= RETOK，返回错误描述</td></tr></table></body></html>  

股票快照数据格式如下：  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>code</td><td>str</td><td>股票代码</td></tr><tr><td>name</td><td>str</td><td>股票名称</td></tr><tr><td>update_time</td><td>str</td><td>当前价更新 时间</td></tr><tr><td>last_price</td><td>float</td><td>最新价格</td></tr><tr><td>open_price</td><td>float</td><td>今日开盘价</td></tr><tr><td>high_price</td><td>float</td><td>最高价格</td></tr></table></body></html>  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>low_price</td><td>float</td><td>最低价格</td></tr><tr><td>prev_close_price</td><td>float</td><td>昨收盘价格</td></tr><tr><td>volume</td><td>int</td><td>成交数量</td></tr><tr><td>turnover</td><td>float</td><td>成交金额</td></tr><tr><td>turnover_rate</td><td>float</td><td>换手率</td></tr><tr><td>suspension</td><td>bool</td><td>是否停牌</td></tr><tr><td>listing_date</td><td>str</td><td>上市日期</td></tr><tr><td>equity_valid</td><td>bool</td><td>是否正股</td></tr><tr><td>issued_shares</td><td>int</td><td>总股本</td></tr><tr><td>total_market_val</td><td>float</td><td>总市值</td></tr><tr><td>net_asset</td><td>int</td><td>资产净值</td></tr><tr><td>net_profit</td><td>int</td><td>净利润</td></tr><tr><td>earning_per_share</td><td>float</td><td>每股盈利</td></tr><tr><td>outstanding_shares</td><td>int</td><td>流通股本</td></tr><tr><td>net_asset_per_share</td><td>float</td><td>每股净资产</td></tr><tr><td>circular_market_val</td><td>float</td><td>流通市值</td></tr></table></body></html>  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td></td><td></td><td></td></tr><tr><td>ey_ratio</td><td>float</td><td>收益率</td></tr><tr><td>pe_ratio</td><td>float</td><td>市盈率</td></tr><tr><td>pb_ratio</td><td>float</td><td>市净率</td></tr><tr><td>pe_ttm_ratio</td><td>float</td><td>市盈率 TTM</td></tr><tr><td>dividend_ttm</td><td>float</td><td>股息TTM, 派息</td></tr><tr><td>dividend_ratio_ttm</td><td>float</td><td>股息率 TTM</td></tr><tr><td>dividend_lfy</td><td>float</td><td>股息LFY, 上一年度派 息</td></tr><tr><td>dividend_lfy_ratio</td><td>float</td><td>股息率 LFY</td></tr><tr><td>stock_owner</td><td>str</td><td>窝轮所属正 股的代码或 期权的标的 股代码</td></tr></table></body></html>  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>wrt_valid</td><td>bool</td><td>是否是窝 轮</td></tr><tr><td>wrt_conversion_ratio</td><td>float</td><td>换股比率</td></tr><tr><td>wrt_type</td><td>WrtType</td><td>窝轮类型</td></tr><tr><td>wrt_strike_price</td><td>float</td><td>行使价格</td></tr><tr><td>wrt_maturity_date</td><td>str</td><td>格式化窝轮 到期时间</td></tr><tr><td>wrt_end_trade</td><td>str</td><td>格式化窝轮 最后交易时 间</td></tr><tr><td>wrt_leverage</td><td>float</td><td>杠杆比率</td></tr><tr><td>wrt_ipop</td><td>float</td><td>价内/价 外</td></tr><tr><td>wrt_break_even_point</td><td>float</td><td>打和点</td></tr><tr><td>wrt_conversion_price</td><td>float</td><td>换股价</td></tr><tr><td>wrt_price_recovery_rat io</td><td>float</td><td>正股距收回 价</td></tr><tr><td>wrt_score</td><td>float</td><td>窝轮综合评 分</td></tr><tr><td>wrt_code</td><td>str</td><td>窝轮对应的 正股（此字 段已废除,</td></tr></table></body></html>  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td></td><td></td><td>修改为 stock_owne r)</td></tr><tr><td>wrt_recovery_price</td><td>float</td><td>窝轮收回价</td></tr><tr><td>wrt_street_vol</td><td>float</td><td>窝轮街货量</td></tr><tr><td>wrt_issue_vol</td><td>float</td><td>窝轮发行量</td></tr><tr><td>wrt_street_ratio</td><td>float</td><td>窝轮街货占 比</td></tr><tr><td>wrt_delta</td><td>float</td><td>窝轮对冲值</td></tr><tr><td>wrt_implied_volatility</td><td>float</td><td>窝轮引伸波 幅</td></tr><tr><td>wrt_premium</td><td>float</td><td>窝轮溢价</td></tr><tr><td>wrt_upper_strike_price</td><td>float</td><td>上限价</td></tr><tr><td>wrt_lower_strike_price</td><td>float</td><td>下限价</td></tr><tr><td>wrt_inline_price_statu S</td><td>PriceType</td><td>界内界外</td></tr><tr><td>wrt_issuer_code</td><td>str</td><td>发行人代码</td></tr><tr><td>option_valid</td><td>bool</td><td>是否是期 权</td></tr></table></body></html>  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>option_type</td><td>OptionType</td><td>期权类型</td></tr><tr><td>strike time</td><td>str</td><td>期权行权 日</td></tr><tr><td>option_strike_price</td><td>float</td><td>行权价</td></tr><tr><td>option_contract_size</td><td>float</td><td>每份合约数</td></tr><tr><td>option_open_interest</td><td>int</td><td>总未平仓合 约数</td></tr><tr><td>option_implied_volatil ity</td><td>float</td><td>隐含波动率</td></tr><tr><td>option_premium</td><td>float</td><td>溢价</td></tr><tr><td>option_delta</td><td>float</td><td>希腊值 Delta</td></tr><tr><td>option_gamma</td><td>float</td><td>希腊值 Gamma</td></tr><tr><td>option_vega</td><td>float</td><td>希腊值 Vega</td></tr><tr><td>option_theta</td><td>float</td><td>希腊值 Theta</td></tr><tr><td>option_rho</td><td>float</td><td>希腊值 Rho</td></tr><tr><td>index_option_type</td><td>IndexOption Type</td><td>指数期权类 型</td></tr><tr><td>option_net_open_intere st</td><td>int</td><td>净未平仓合 约数</td></tr></table></body></html>  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>option_expiry_date_dis tance</td><td>int</td><td>距离到期日 天数</td></tr><tr><td>option_contract_nomina 1_value</td><td>float</td><td>合约名义金 额</td></tr><tr><td>option_owner_lot_multi plier</td><td>float</td><td>相等正股手 数</td></tr><tr><td>option_area_type</td><td>OptionAreaT ype</td><td>期权类型 （按行权时 间）</td></tr><tr><td>option_contract_multip lier</td><td>float</td><td>合约乘数</td></tr><tr><td>plate_valid</td><td>bool</td><td>是否为板块 类型</td></tr><tr><td>plate_raise_count</td><td>int</td><td>板块类型上 涨支数</td></tr><tr><td>plate_fall_count</td><td>int</td><td>板块类型下 跌支数</td></tr><tr><td>plate_equal_count</td><td>int</td><td>板块类型平 盘支数</td></tr><tr><td>index_valid</td><td>bool</td><td>是否有指数 类型</td></tr></table></body></html>  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>index_raise_count</td><td>int</td><td>指数类型上 涨支数</td></tr><tr><td>index_fall_count</td><td>int</td><td>指数类型下 跌支数</td></tr><tr><td>index_equal_count</td><td>int</td><td>指数类型平 盘支数</td></tr><tr><td>lot_size</td><td>int</td><td>每手股数, 股票期权表 示每份合约 的股数 ，期货表示 合约乘数</td></tr><tr><td>price_spread</td><td>float</td><td>当前向上的 摆盘价差</td></tr><tr><td>ask_price</td><td>float</td><td>卖价</td></tr><tr><td>bid_price</td><td>float</td><td>买价</td></tr><tr><td>ask_vol</td><td>float</td><td>卖量</td></tr><tr><td>bid_vol</td><td>float</td><td>买量</td></tr><tr><td>enable_margin</td><td>bool</td><td>是否可融资 （已废 弃)</td></tr><tr><td>mortgage_ratio</td><td>float</td><td>股票抵押率 （已废弃)</td></tr></table></body></html>  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>long_margin_initial_ra tio</td><td>float</td><td>融资初始保 证金率（已 废弃)</td></tr><tr><td>enable_short_sell</td><td>bool</td><td>是否可卖空 （已废 弃)</td></tr><tr><td>short_sell_rate</td><td>float</td><td>卖空参考利 率（已废 弃)</td></tr><tr><td>short_available_volume</td><td>int</td><td>剩余可卖空 数量（已废 弃)</td></tr><tr><td>short_margin_initial_r atio</td><td>float</td><td>卖空（融 券）初始保 证金率（已 废弃)</td></tr><tr><td>sec_status</td><td>SecuritySta tus</td><td>股票状态</td></tr><tr><td>amplitude</td><td>float</td><td>振幅</td></tr><tr><td>avg_price</td><td>float</td><td>平均价</td></tr><tr><td>bid_ask_ratio</td><td>float</td><td>委比</td></tr></table></body></html>  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td></td><td></td><td></td></tr><tr><td>volume_ratio</td><td>float</td><td>量比</td></tr><tr><td>highest52weeks_price</td><td>float</td><td>52 周最高 价</td></tr><tr><td>lowest52weeks_price</td><td>float</td><td>52周最低 价</td></tr><tr><td>highest_history_price</td><td>float</td><td>历史最高价</td></tr><tr><td>lowest_history_price</td><td>float</td><td>历史最低价</td></tr><tr><td>pre_price</td><td>float</td><td>盘前价格</td></tr><tr><td>pre_high_price</td><td>float</td><td>盘前最高价</td></tr><tr><td>pre_low_price</td><td>float</td><td>盘前最低价</td></tr><tr><td>pre_volume</td><td>int</td><td>盘前成交量</td></tr><tr><td>pre_turnover</td><td>float</td><td>盘前成交额</td></tr><tr><td>pre_change_val</td><td>float</td><td>盘前涨跌额</td></tr><tr><td>pre_change_rate</td><td>float</td><td>盘前涨跌 幅</td></tr><tr><td>pre_amplitude</td><td>float</td><td>盘前振幅</td></tr><tr><td>after_price</td><td>float</td><td>盘后价格</td></tr><tr><td>after_high_price</td><td>float</td><td>盘后最高价</td></tr><tr><td>after_low_price</td><td>float</td><td>盘后最低价</td></tr></table></body></html>  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>after_volume</td><td>int</td><td>盘后成交 量</td></tr><tr><td>after_turnover</td><td>float</td><td>盘后成交 额</td></tr><tr><td>after_change_val</td><td>float</td><td>盘后涨跌额</td></tr><tr><td>after_change_rate</td><td>float</td><td>盘后涨跌 幅</td></tr><tr><td>after_amplitude</td><td>float</td><td>盘后振幅</td></tr><tr><td>future_valid</td><td>bool</td><td>是否期货</td></tr><tr><td>future_last_settle_pri ce</td><td>float</td><td>昨结</td></tr><tr><td>future_position</td><td>float</td><td>持仓量</td></tr><tr><td>future_position_change</td><td>float</td><td>日增仓</td></tr><tr><td>future main_contract</td><td>bool</td><td>是否主连合 约</td></tr><tr><td>future last_trade_time</td><td>str</td><td>最后交易时 间</td></tr><tr><td>trust_valid</td><td>bool</td><td>是否基金</td></tr><tr><td>trust_dividend_yield</td><td>float</td><td>股息率</td></tr></table></body></html>  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td></td><td></td><td></td></tr><tr><td>trust_aum</td><td>float</td><td>资产规模</td></tr><tr><td>trust_outstanding_unit S</td><td>int</td><td>总发行量</td></tr><tr><td>trust_netAssetValue</td><td>float</td><td>单位净值</td></tr><tr><td>trust_premium</td><td>float</td><td>溢价</td></tr><tr><td>trust_assetClass</td><td>AssetClass</td><td>资产类别</td></tr></table></body></html>  

# Example  

from futu import $\star$ quote_ctx $=$ OpenQuoteContext(host $\mathrel{\mathop:}$ '127.0.0.1', port $\equiv$ 11111)  

ret, data $=$ quote_ctx.get_market_snapshot(['SH.600000', 'HK.00700'])   
if r $\mathsf{a t}==\mathsf{R E T\_O K}\mathrm{:}$ print(data) print(data['code'][0]) # 取第一条的股票代码 print(data['code'].values.tolist())   # 转为 list   
else: print('error:', data)   
quote_ctx.close() # 结束后记得关闭当条连接，防止连接条数用尽  

# 接口限制  

每 30 秒内最多请求 60 次快照。  

每次请求，接口参数 股票代码列表 支持传入的标的数量上限是 400个。  

港股 BMP 权限下，单次请求的香港证券（含窝轮、牛熊、界内证）快照数量上限是 20 个。  

港股期权期货 BMP 权限下，单次请求的香港期货和期权的快照数量上 限是 20 个。  

# 获取实时报价  

# get_stock_quote(code_list)  

介绍  

获取已订阅股票的实时报价，必须要先订阅。  

参数  

<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>code list</td><td>list</td><td>股票代码列表</td></tr></table></body></html>  

返回  

<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>ret</td><td>RET CODE</td><td>接口调用结果</td></tr><tr><td rowspan="2">data</td><td>pd. DataFrame</td><td>当 ret RET_OK，返回报价数据</td></tr><tr><td>str</td><td>当 ret!= RET OK，返回错误描述</td></tr></table></body></html>  

报价数据格式如下：  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>code</td><td>str</td><td>股票代码</td></tr><tr><td>name</td><td>str</td><td>股票名称</td></tr><tr><td>data_date</td><td>str</td><td>日期</td></tr><tr><td>data_time</td><td>str</td><td>当前价更 新时间</td></tr><tr><td>last_price</td><td>float</td><td>最新价格</td></tr><tr><td>open_price</td><td>float</td><td>今日开盘 价</td></tr><tr><td>high_price</td><td>float</td><td>最高价格</td></tr><tr><td>low_price</td><td>float</td><td>最低价格</td></tr><tr><td>prev_close_price</td><td>float</td><td>昨收盘价 格</td></tr><tr><td>volume</td><td>int</td><td>成交数量</td></tr><tr><td>turnover</td><td>float</td><td>成交金额</td></tr><tr><td>turnover_rate</td><td>float</td><td>换手率</td></tr><tr><td>amplitude</td><td>int</td><td>振幅</td></tr><tr><td>suspension</td><td>bool</td><td>是否停 牌</td></tr><tr><td>listing_date</td><td>str</td><td>上市日 期</td></tr></table></body></html>  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td></td><td></td><td></td></tr><tr><td>price_spread</td><td>float</td><td>当前向上 的价差</td></tr><tr><td>dark_status</td><td>DarkStatus</td><td>暗盘交易 状态</td></tr><tr><td>sec_status</td><td>SecurityStatus</td><td>股票状态</td></tr><tr><td>strike_price</td><td>float</td><td>行权价</td></tr><tr><td>contract_size</td><td>float</td><td>每份合约 数</td></tr><tr><td>open_interest</td><td>int</td><td>未平仓合 约数</td></tr><tr><td>implied_volatility</td><td>float</td><td>隐含波动 率</td></tr><tr><td>premium</td><td>float</td><td>溢价</td></tr><tr><td>delta</td><td>float</td><td>希腊值 Delta</td></tr><tr><td>gamma</td><td>float</td><td>希腊值 Gamma</td></tr><tr><td>vega</td><td>float</td><td>希腊值 Vega</td></tr><tr><td>theta</td><td>float</td><td>希腊值 Theta</td></tr></table></body></html>  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>rho</td><td>float</td><td>希腊值 Rho</td></tr><tr><td>index_option_type</td><td>IndexOptionType</td><td>指数期权 类型</td></tr><tr><td>net_open_interest</td><td>int</td><td>净未平仓 合约数</td></tr><tr><td>expiry_date_distance</td><td>int</td><td>距离到期 日天数</td></tr><tr><td>contract_nominal_value</td><td>float</td><td>合约名义 金额</td></tr><tr><td>owner_lot_multiplier</td><td>float</td><td>相等正股 手数</td></tr><tr><td>option_area_type</td><td>OptionAreaType</td><td>期权类型 （按行权 时间)</td></tr><tr><td>contract_multiplier</td><td>float</td><td>合约乘数</td></tr><tr><td>pre_price</td><td>float</td><td>盘前价格</td></tr><tr><td>pre_high_price</td><td>float</td><td>盘前最高 价</td></tr><tr><td>pre_low_price</td><td>float</td><td>盘前最低 价</td></tr><tr><td>pre_volume</td><td>int</td><td>盘前成交 量</td></tr></table></body></html>  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>pre_turnover</td><td>float</td><td>盘前成交 额</td></tr><tr><td>pre_change_val</td><td>float</td><td>盘前涨跌 额</td></tr><tr><td>pre_change_rate</td><td>float</td><td>盘前涨跌 幅</td></tr><tr><td>pre_amplitude</td><td>float</td><td>盘前振 幅</td></tr><tr><td>after_price</td><td>float</td><td>盘后价格</td></tr><tr><td>after_high_price</td><td>float</td><td>盘后最高 价</td></tr><tr><td>after_low_price</td><td>float</td><td>盘后最低 价</td></tr><tr><td>after_volume</td><td>int</td><td>盘后成交 量</td></tr><tr><td>after_turnover</td><td>float</td><td>盘后成交 额</td></tr><tr><td>after_change_val</td><td>float</td><td>盘后涨跌 额</td></tr><tr><td>after_change_rate</td><td>float</td><td>盘后涨跌 幅</td></tr></table></body></html>  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>after_amplitude</td><td>float</td><td>盘后振 幅</td></tr><tr><td>last_settle_price</td><td>float</td><td>昨结</td></tr><tr><td>position</td><td>float</td><td>持仓量</td></tr><tr><td>position_change</td><td>float</td><td>日增仓</td></tr></table></body></html>  

# Example  

from futu import $\star$ quote_ctx $=$ OpenQuoteContext(host $\underline{{\underline{{\mathbf{\delta\pi}}}}}$ '127.0.0.1', port $\equiv$ 11111)  

ret_sub, err_message $=$ quote_ctx.subscribe(['HK.00700'], [SubType.QUOTE], subscribe_push $=$ False)  

# 先订阅 K 线类型。订阅成功后 OpenD 将持续收到服务器的推送，False 代表暂时不需要推送给脚本  

if ret_sub $=={\mathsf{R E T}}\_{\mathsf{O K}:}$ # 订阅成功 ret, data $=$ quote_ctx.get_stock_quote(['HK.00700'])  # 获取订阅股票报价的实时数据 if ret $==$ RET_OK: print(data) print(data['code'][0])   # 取第一条的股票代码 print(data['code'].values.tolist())   # 转为 list else: print('error:', data)  

else:  

print('subscription failed', err_message)  

quote_ctx.close()  # 关闭当条连接，OpenD 会在1 分钟后自动取消相应股票相应类型的订阅  

# 提示  

此接口提供了一次性获取实时数据的功能，如需持续获取推送数据，请参考 实时报价回调 接口  

获取实时数据 和 实时数据回调 的差别，请参考 如何通过订阅接口获取实时行情？  

# 获取实时摆盘  

# get_order_book(code, num $1=18$ )  

介绍  

获取已订阅股票的实时摆盘，必须要先订阅。  

参数  

<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>code</td><td>str</td><td>股票代码</td></tr><tr><td>name</td><td>str</td><td>股票名称</td></tr><tr><td>num</td><td>int</td><td>请求摆盘档数</td></tr></table></body></html>  

返回  

<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>ret</td><td>RET CODE</td><td>接口调用结果</td></tr><tr><td rowspan="2">data</td><td>dict</td><td>当 ret RET_OK，返回摆盘数据</td></tr><tr><td>str</td><td>当 ret!= RET_OK，返回错误描述</td></tr></table></body></html>  

摆盘数据格式如下：  

<html><body><table><tr><td>字段</td><td>类 型</td><td>说明</td></tr><tr><td>code</td><td>str</td><td>股票代码</td></tr><tr><td>name</td><td>str</td><td>股票名称</td></tr><tr><td>svr_recv_time_bid</td><td>str</td><td>富途服务器从交易所收到买 盘数据的时间</td></tr><tr><td>svr_recv_time ask</td><td>str</td><td>富途服务器从交易所收到卖 盘数据的时间</td></tr><tr><td>Bid</td><td>list</td><td>每个元祖包含如下信息：委 托价格，委托数量，委托订 单数，委托订单明细</td></tr><tr><td>Ask</td><td>list</td><td>每个元祖包含如下信息：委 托价格，委托数量，委托订 单数，委托订单明细</td></tr></table></body></html>  

'Bid': [ (bid_price1, bid_volume1, order_num, {'orderid1': order_volume1, 'orderid2': order_volume2, …… }), (bid_price2, bid_volume2, order_num, {'orderid1': order_volume1, 'orderid2': order_volume2, …… }),…]  

'Ask': [ (ask_price1, ask_volume1，order_num, {'orderid1': order_volume1, 'orderid2': order_volume2, …… }), (ask_price2, ask_volume2, order_num, {'orderid1': order_volume1, 'orderid2': order_volume2, …… }),…]  

# Example  

from futu import \*  

quote_ctx $=$ OpenQuoteContext(host $\r=\r^{\prime}$ 127.0.0.1', port $=$ 11111)  

ret_sub $=$ quote_ctx.subscribe(['HK.00700'], [SubType.ORDER_BOOK], subscribe_push $=$ False)[0]  

# 先订阅买卖摆盘类型。订阅成功后 OpenD 将持续收到服务器的推送，False代表暂时不需要推送给脚本  

if ret_sub $==$ RET_OK:  # 订阅成功  

ret, data $=$ quote_ctx.get_order_book('HK.00700', num $=3$ )  # 获取一次 3档实时摆盘数据  

if ret $==$ RET_OK: print(data) else:  

print('error:', data)  

else:  

print('subscription failed')  

quote_ctx.close()  # 关闭当条连接，OpenD 会在 1 分钟后自动取消相应股票相应类型的订阅  

# 接口限制  

富途服务器从交易所收到数据的时间字段，仅支持A 股正股、港股正股、ETFs、窝轮、牛熊，且仅开盘时间才有此数据。  

富途服务器从交易所收到数据的时间字段，部分情况下接收时间可能为零，例如：服务器重启或第一次推送的缓存数据。  

# 获取实时 K 线  

get_cur_kline(code, num, ktype=KLType.K_DAY,autype=AuType.QFQ)  

介绍  

获取已订阅股票的实时 K 线数据，必须要先订阅。  

参数返回  

<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>code</td><td>str</td><td>股票代码</td></tr></table></body></html>  

<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>name</td><td>str</td><td>股票名称</td></tr><tr><td>num</td><td>int</td><td>K线数据个数</td></tr><tr><td>ktype</td><td>KLType</td><td>K 线类型</td></tr><tr><td>autype</td><td>AuType</td><td>复权类型</td></tr></table></body></html>  

<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>ret</td><td>RET CODE</td><td>接口调用结果</td></tr><tr><td rowspan="2">data</td><td>pd. DataFrame</td><td>当 ret 二二 RETOK，返回K线数据数据</td></tr><tr><td>str</td><td>当 ret!= RET_OK，返回错误描述</td></tr></table></body></html>  

K 线数据格式如下：  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>code</td><td>str</td><td>股票代码</td></tr><tr><td>name</td><td>str</td><td>股票名称</td></tr><tr><td>time_key</td><td>str</td><td>时间</td></tr><tr><td>open</td><td>float</td><td>开盘价</td></tr><tr><td>close</td><td>float</td><td>收盘价</td></tr><tr><td>high</td><td>float</td><td>最高价</td></tr><tr><td>1ow</td><td>float</td><td>最低价</td></tr></table></body></html>  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>volume</td><td>int</td><td>成交量</td></tr><tr><td>turnover</td><td>float</td><td>成交额</td></tr><tr><td>pe_ratio</td><td>float</td><td>市盈率</td></tr><tr><td>turnover_rate</td><td>float</td><td>换手率</td></tr><tr><td>last_close</td><td>float</td><td>昨收价</td></tr></table></body></html>

Example  

from futu import \*  

quote_ctx $=$ OpenQuoteContext(host $="$ 127.0.0.1', port $=$ 11111)  

ret_sub, err_message $=$ quote_ctx.subscribe(['HK.00700'], [SubType.K_DAY], subscribe_push $=$ False)  

# 先订阅 K 线类型。订阅成功后 OpenD 将持续收到服务器的推送，False 代表暂时不需要推送给脚本  

if ret_sub $==$ RET_OK:  # 订阅成功 ret, data $=$ quote_ctx.get_cur_kline('HK.00700', 2, KLType.K_DAY,  

AuType.QFQ)  # 获取港股00700 最近2 个 K 线数据  

if ret $==$ RET_OK:  

print(data)  

print(data['turnover_rate'][0]) # 取第一条的换手率print(data['turnover_rate'].values.tolist())   # 转为 list  

else:  

print('error:', data)  

else:  

print('subscription failed', err_message)  

quote_ctx.close()  # 关闭当条连接，OpenD 会在1 分钟后自动取消相应股票相应类型的订阅  

from futu import \*quote_ctx $=$ OpenQuoteContext(host $=$ '127.0.0.1', port $=$ 11111)  

ret_sub, err_message $=$ quote_ctx.subscribe(['HK.00700'], [SubType.K_DAY],  
subscribe_push $=$ False)  
# 先订阅 K 线类型。订阅成功后 OpenD 将持续收到服务器的推送，False 代表暂时不需要  
推送给脚本  
if ret_sub $\L=\textsf{R E T}\_0\ K$ :  # 订阅成功ret, data $=$ quote_ctx.get_cur_kline('HK.00700', 2, KLType.K_DAY,  
AuType.QFQ)  # 获取港股00700 最近2 个 K 线数据if ret $==$ RET_OK:print(data)print(data['turnover_rate'][0])   # 取第一条的换手率print(data['turnover_rate'].values.tolist())   # 转为 listelse:print('error:', data)  

print('subscription failed', err_message)  

quote_ctx.close()  # 关闭当条连接，OpenD 会在1 分钟后自动取消相应股票相应类型的订阅  

# 接口限制  

此接口为获取实时 K 线接口，最多能获取最近的 1000 根。如需获取历史 K 线，请参考 获取历史 K 线  

市盈率和换手率字段，只有日 K 及以上周期的正股才有数据  

期权，仅提供日K, 1 分K，5 分K，15 分K，60 分K。  

# 获取实时分时  

# get_rt_data(code)  

介绍获取已订阅股票的实时分时数据，必须要先订阅。  

# 参数  

<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>code</td><td>str</td><td>股票</td></tr></table></body></html>  

返回  

<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>ret</td><td>RET CODE</td><td>接口调用结果</td></tr><tr><td rowspan="2">data</td><td>pd. DataFrame</td><td>当 ret RETOK，返回分时数据 二二</td></tr><tr><td>str</td><td>当 ret t！=RETOK，返回错误描述</td></tr></table></body></html>  

分时数据格式如下：  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>code</td><td>str</td><td>股票代码</td></tr><tr><td>name</td><td>str</td><td>股票名称</td></tr><tr><td>time</td><td>str</td><td>时间</td></tr><tr><td>is_blank</td><td>bool</td><td>数据状态</td></tr><tr><td>opened_mins</td><td>int</td><td>零点到当前多少分钟</td></tr><tr><td>cur_price</td><td>float</td><td>当前价格</td></tr><tr><td>last_close</td><td>float</td><td>昨天收盘的价格</td></tr><tr><td>avg_price</td><td>float</td><td>平均价格</td></tr><tr><td>volume</td><td>float</td><td>成交量</td></tr><tr><td>turnover</td><td>float</td><td>成交金额</td></tr></table></body></html>  

# Example  

• from futu import \*  
• quote_ctx $=$ OpenQuoteContext(host $=$ '127.0.0.1', port $=$ 11111)ret_sub, err_message $=$ quote_ctx.subscribe(['HK.00700'],[SubType.RT_DATA], subscribe_push $=$ False)# 先订阅分时数据类型。订阅成功后 OpenD 将持续收到服务器的推送，False 代表暂时不需要推送给脚本if ret_sub $\L=\textsf{R E T}\_0\ K$ :   # 订阅成功  
• ret, data $=$ quote_ctx.get_rt_data('HK.00700')   # 获取一次分时数据  
• if ret $==$ RET_OK:  
• print(data)else:  
• print('error:', data)  
• else:print('subscription failed', err_message)  

quote_ctx.close()   # 关闭当条连接，OpenD 会在1 分钟后自动取消相应股票相应类型的订阅  

# 获取实时逐笔  

# get_rt_ticker(code, num=500)  

介绍  

获取已订阅股票的实时逐笔数据，必须要先订阅。  

参数  

<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>code</td><td>str</td><td>股票代码</td></tr><tr><td>num</td><td>int</td><td>最近逐笔个数</td></tr></table></body></html>  

返回  

<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>ret</td><td>RET CODE</td><td>接口调用结果</td></tr><tr><td rowspan="2">data</td><td>pd.DataFrame</td><td>当 ret 二二 ：RETOK，返回逐笔数据</td></tr><tr><td>str</td><td>当 ret!= RET OK，返回错误描述</td></tr></table></body></html>  

逐笔数据格式如下：  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>code</td><td>str</td><td>股票代码</td></tr><tr><td>name</td><td>str</td><td>股票名称</td></tr><tr><td>sequence</td><td>int</td><td>逐笔序号</td></tr><tr><td>time</td><td>str</td><td>成交时间</td></tr></table></body></html>  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td></td><td></td><td></td></tr><tr><td>price</td><td>float</td><td>成交价格</td></tr><tr><td>volume</td><td>int</td><td>成交数量</td></tr><tr><td>turnover</td><td>float</td><td>成交金额</td></tr><tr><td>ticker_direction</td><td>TickerDirect</td><td>逐笔方向</td></tr><tr><td>type</td><td>TickerType</td><td>逐笔类型</td></tr></table></body></html>  

# Example  

• from futu import \*quote_ctx $=$ OpenQuoteContext(host $=$ '127.0.0.1', port $=$ 11111)  

ret_sub, err_message $=$ quote_ctx.subscribe(['HK.00700'],[SubType.TICKER], subscribe_push $=$ False)  
•  # 先订阅逐笔类型。订阅成功后 OpenD 将持续收到服务器的推送，False 代表暂时不需要推送给脚本  
• if ret_sub $==$ RET_OK:  # 订阅成功ret, data $=$ quote_ctx.get_rt_ticker('HK.00700', 2)  # 获取港股00700 最近2 个逐笔if ret $==$ RET_OK:print(data)print(data['turnover'][0])   # 取第一条的成交金额print(data['turnover'].values.tolist())   # 转为 listelse:  
• print('error:', data)  
• else:print('subscription failed', err_message)quote_ctx.close()  # 关闭当条连接，OpenD 会在1 分钟后自动取消相应股票相应类型的订阅  

最多能获取最近 1000 个逐笔数据，更多历史逐笔数据暂未提供港股期权期货在 LV1 权限下，不支持获取逐笔  

# 获取实时经纪队列  

# get_broker_queue(code)  

介绍  

获取已订阅股票的实时经纪队列数据，必须要先订阅。  

# 参数  

<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>code</td><td>str</td><td>股票代码</td></tr></table></body></html>  

返回  

<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>ret</td><td>RET CODE</td><td>接口调用结果</td></tr><tr><td rowspan="2">bid_frame_table</td><td>pd. DataFrame</td><td>当 ret == RET_OK, bid_frame_table 返回买盘 经纪队列数据</td></tr><tr><td>str</td><td>当 ret != RET_OK, bid_frame_table 返回错误 描述</td></tr><tr><td>ask_frame_table</td><td>pd. DataFrame</td><td>当 ret == RET_OK, ask_frame_table返回卖盘 经纪队列数据</td></tr></table></body></html>  

买盘经纪队列格式如下：  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>code</td><td>str</td><td>股票代码</td></tr><tr><td>name</td><td>str</td><td>股票名称</td></tr><tr><td>bid_broker_id</td><td>int</td><td>经纪买盘 ID</td></tr><tr><td>bid_broker_name</td><td>str</td><td>经纪买盘名称</td></tr><tr><td>bid_broker_pos</td><td>int</td><td>经纪档位</td></tr><tr><td>order_id</td><td>int</td><td>交易所订单ID</td></tr><tr><td>order_volume</td><td>int</td><td>单笔委托数量</td></tr></table></body></html>  

卖盘经纪队列格式如下：  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>code</td><td>str</td><td>股票代码</td></tr><tr><td>name</td><td>str</td><td>股票名称</td></tr><tr><td>ask_broker_id</td><td>int</td><td>经纪卖盘 ID</td></tr><tr><td>ask broker name</td><td>str</td><td>经纪卖盘名称</td></tr><tr><td>ask broker_pos</td><td>int</td><td>经纪档位</td></tr><tr><td>order_id</td><td>int</td><td>交易所订单 ID</td></tr></table></body></html>  

![](FutuAPI/483c78f507357000c2e79373f2b869ef17f1dba114fb152c03b8f0cb413dea73.jpg)  

# Example  

• from futu import \*  
• quote_ctx $=$ OpenQuoteContext(host $=$ '127.0.0.1', port $=$ 11111)ret_sub, err_message $=$ quote_ctx.subscribe(['HK.00700'],[SubType.BROKER], subscribe_push $=$ False)# 先订阅经纪队列类型。订阅成功后 OpenD 将持续收到服务器的推送，False 代表暂时不需要推送给脚本  
• if ret_sub $\L=\textsf{R E T}\_0\ K$ :   # 订阅成功  
• ret, bid_frame_table, ask_frame_table $=$ quote_ctx.get_broker_queue('HK.00700')   # 获取一次经纪队列数据if ret $==$ RET_OK:  
• print(bid_frame_table)else:  
• print('error:', bid_frame_table)  
• else:  
• print('subscription failed')quote_ctx.close()   # 关闭当条连接，OpenD 会在1 分钟后自动取消相应股票相应类型的订阅  

# 获取标的市场状态  

get_market_state(code_list)  

介绍  

获取指定标的的市场状态  

参数  

<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>code_list</td><td>list</td><td>需要查询市场状态的股票代码列表</td></tr></table></body></html>  

返回  

<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>ret</td><td>RET CODE</td><td>接口调用结果</td></tr><tr><td rowspan="2">data</td><td>pd. DataFrame</td><td>当 ret RETOK，返回市场状态数据</td></tr><tr><td>str</td><td>当 ret!= RET_OK，返回错误描述</td></tr></table></body></html>  

市场状态数据  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>code</td><td>str</td><td>股票代码</td></tr><tr><td>stock name</td><td>str</td><td>股票名称</td></tr><tr><td>marketstate</td><td>MarketState</td><td>市场状态</td></tr></table></body></html>  

# Example  

• from futu import \*quote_ctx $=$ OpenQuoteContext(host $=$ '127.0.0.1', port $=$ 11111)  

• ret, data $=$ quote_ctx.get_market_state(['SZ.000001', 'HK.00700']) if ret $==$ RET_OK:  

print(data)  

else:  

print('error:', data)  

quote_ctx.close() # 结束后记得关闭当条连接，防止连接条数用尽  

接口限制  

每 30 秒内最多请求 10 次获取标的市场状态接口。  

每次请求的股票代码个数上限为 400 个。  

# 获取资金流向  

get_capital_flow(stock_code, period_type $=$ PeriodType.INTRADAY, start=None, end $=$ None)  

介绍获取个股资金流向  

参数  

<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>stock_code</td><td>str</td><td>股票代码</td></tr><tr><td>period_type</td><td>PeriodType</td><td>周期类型</td></tr><tr><td>start</td><td>str</td><td>开始时间</td></tr><tr><td>end</td><td>str</td><td>结束时间</td></tr></table></body></html>  

start 和 end 的组合如下  

<html><body><table><tr><td>start 类 型</td><td>end 类 型</td><td>说明</td></tr><tr><td>str</td><td>str</td><td>start 和 end 分别为指定的日 期</td></tr><tr><td>None</td><td>str</td><td>start为 end 往前 365 天</td></tr><tr><td>str</td><td>None</td><td>end 为start 往后365 天</td></tr></table></body></html>  

<html><body><table><tr><td>start 类 型</td><td>end 类 型</td><td>说明</td></tr><tr><td>None</td><td>None</td><td>end 为 」当前日期， start 往前 365 天</td></tr></table></body></html>  

返回  


<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>ret</td><td>RET CODE</td><td>接口调用结果</td></tr><tr><td rowspan="2">data</td><td>pd. DataFrame</td><td>当 ret RETOK，返回资金流向数据</td></tr><tr><td>str</td><td>当 ret!= RET OK，返回错误描述</td></tr></table></body></html>  

资金流向数据格式如下：  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>in_flow</td><td>float</td><td>整体净流入</td></tr><tr><td>main_in_flow</td><td>float</td><td>主力大单净流入</td></tr><tr><td>super_in_flow</td><td>float</td><td>特大单净流入</td></tr><tr><td>big_in_flow</td><td>float</td><td>大单净流入</td></tr><tr><td>mid_in_flow</td><td>float</td><td>中单净流入</td></tr><tr><td>sml_in_flow</td><td>float</td><td>小单净流入</td></tr><tr><td>capital_flow_item_time</td><td>str</td><td>开始时间</td></tr><tr><td>last_valid_time</td><td>str</td><td>数据最后有效时间</td></tr></table></body></html>  

Example  

from futu import \*  

quote_ctx $=$ OpenQuoteContext(host $=$ '127.0.0.1', port $=$ 11111)  

ret, data $=$ quote_ctx.get_capital_flow("HK.00700", period_type $=$ PeriodType.INTRADAY)  

if ret $==$ RET_OK:  

print(data)  

print(data['in_flow'][0]) # 取第一条的净流入的资金额度  

print('error:', data)  

quote_ctx.close() # 结束后记得关闭当条连接，防止连接条数用尽  

# 获取资金分布  

# get_capital_distribution(stock_code)  

介绍  

获取资金分布  

参数  

<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>stock K_code</td><td>str</td><td>股票代码</td></tr></table></body></html>  

返回  

<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>ret</td><td>RET CODE</td><td>接口调用结果</td></tr><tr><td rowspan="2">data</td><td>pd.DataFrame</td><td>当 ret RETOK，返回股票资金分布 二二 数据</td></tr><tr><td>str</td><td>当 白 ret！= RET OK，返回错误描述</td></tr></table></body></html>  

资金分布数据格式如下：  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>capital_in_super</td><td>float</td><td>流入资金额度，特大单</td></tr><tr><td>capital_in_big</td><td>float</td><td>流入资金额度，大单</td></tr><tr><td>capital_in_mid</td><td>float</td><td>流入资金额度，中单</td></tr><tr><td>capital_in_small</td><td>float</td><td>流入资金额度，小单</td></tr><tr><td>capital_out_super</td><td>float</td><td>流出资金额度，特大单</td></tr><tr><td>capital_out_big</td><td>float</td><td>流出资金额度，大单</td></tr><tr><td>capital_out_mid</td><td>float</td><td>流出资金额度，中单</td></tr><tr><td>capital_out_small</td><td>float</td><td>流出资金额度，小单</td></tr><tr><td>update_time</td><td>str</td><td>更新时间字符串</td></tr></table></body></html>  

# Example  

• from futu import \*   
• quote_ctx $=$ OpenQuoteContext(host $=$ '127.0.0.1', port $=$ 11111)   
•   
• ret, data $=$ quote_ctx.get_capital_distribution("HK.00700")   
• if ret $==$ RET_OK:   
• print(data)   
• print(data['capital_in_big'][0])    # 取第一条的流入资金额度，大单   
• print(data['capital_in_big'].values.tolist())   # 转为 list   
• else:   
• print('error:', data) quote_ctx.close() # 结束后记得关闭当条连接，防止连接条数用尽  

# 接口限制  

每 30 秒内最多请求 30 次获取资金分布接口。  

仅支持正股、窝轮和基金。  

更多资金分布介绍，请参考 这里。  

返回数据只包括盘中数据，不包含盘前盘后数据。  

# 获取股票所属板块  

# get_owner_plate(code_list)  

介绍  

获取单支或多支股票的所属板块信息列表  

参数  

<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>code list</td><td>list</td><td>股票代码列表</td></tr></table></body></html>  

返回  

<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>ret</td><td>RET CODE</td><td>接口调用结果</td></tr><tr><td rowspan="2">data</td><td>pd. DataFrame</td><td>当 ret 二二 RETOK，返回所属板块数据</td></tr><tr><td>str</td><td>当 ret!= RET_OK，返回错误描述</td></tr></table></body></html>  

所属板块数据格式如下：  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>code</td><td>str</td><td>证券代码</td></tr><tr><td>name</td><td>str</td><td>股票名称</td></tr><tr><td>plate_code</td><td>str</td><td>板块代码</td></tr><tr><td>plate_name</td><td>str</td><td>板块名字</td></tr></table></body></html>  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>plate_type</td><td>Plate</td><td>板块类型</td></tr></table></body></html>  

# Example  

• from futu import \* quote_ctx $=$ OpenQuoteContext(host $=$ '127.0.0.1', port $=$ 11111)   
·   
•   
• code_list $=$ ['HK.00001']   
• ret, data $=$ quote_ctx.get_owner_plate(code_list)   
• if ret $==$ RET_OK:   
• print(data)   
• print(data['code'][0])    # 取第一条的股票代码   
• print(data['plate_code'].values.tolist())   # 板块代码转为 list   
• else:   
• print('error:', data) quote_ctx.close() # 结束后记得关闭当条连接，防止连接条数用尽  

# 接口限制  

每 30 秒内最多请求 10 次获取股票所属板块接口每次请求的股票列表中，股票个数上限为 200 个仅支持正股和指数  

# 获取历史 K 线  

request_history_kline(code, start=None, end $=$ None, ktype $=$ KLType.K_DAY, autype=AuType.QFQ, fields $=$ [KL_FIELD.ALL], max_count=1000, page_req_key=None, extended_time=False)  

介绍  

获取历史 K 线  

# 参数  

<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>code</td><td>str</td><td>股票代码</td></tr><tr><td>start</td><td>str</td><td>开始时间</td></tr><tr><td>end</td><td>str</td><td>结束时间</td></tr><tr><td>ktype</td><td>KLType</td><td>K 线类型</td></tr><tr><td>autype</td><td>AuType</td><td>复权类型</td></tr><tr><td>fields</td><td>KLFields</td><td>需返回的字段列表</td></tr><tr><td>max_count</td><td>int</td><td>本次请求最大返回的 K 线根数</td></tr><tr><td>page_req_key</td><td>bytes</td><td>分页请求</td></tr><tr><td>extended_time</td><td>bool</td><td>是否允许美股盘前盘后数据</td></tr></table></body></html>  

start 和 end 的组合如下  

<html><body><table><tr><td>Start 类 型</td><td>End 类 型</td><td>说明</td></tr><tr><td>str</td><td>str</td><td>start 和 end 分别为指定的日 期</td></tr></table></body></html>  

<html><body><table><tr><td>Start 类 型</td><td>End 类 型</td><td>说明</td></tr><tr><td>None</td><td>str</td><td>start 为 end 往前 365 天</td></tr><tr><td>str</td><td>None</td><td>end 为 start 往后 365 天</td></tr><tr><td>None</td><td>None</td><td>end 为当前日期，start 往前 365天</td></tr></table></body></html>  

返回  

<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>ret</td><td>RET CODE</td><td>接口调用结果</td></tr><tr><td rowspan="2">data</td><td>pd. DataFrame</td><td>当 ret == RET_OK，返回历史 K 线数据</td></tr><tr><td>str</td><td>当 ret!= RET_OK，返回错误 描述</td></tr><tr><td>page_req_key</td><td>bytes</td><td>下一页请求的 key</td></tr></table></body></html>  

历史 K 线数据格式如下:  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>code</td><td>str</td><td>股票代码</td></tr><tr><td>name</td><td>str</td><td>股票名称</td></tr><tr><td>time_key</td><td>str</td><td>K 线时间</td></tr><tr><td>open</td><td>float</td><td>开盘价</td></tr><tr><td>close</td><td>float</td><td>收盘价</td></tr><tr><td>high</td><td>float</td><td>最高价</td></tr></table></body></html>  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>1ow</td><td>float</td><td>最低价</td></tr><tr><td>pe_ratio</td><td>float</td><td>市盈率</td></tr><tr><td>turnover_rate</td><td>float</td><td>换手率</td></tr><tr><td>volume</td><td>int</td><td>成交量</td></tr><tr><td>turnover</td><td>float</td><td>成交额</td></tr><tr><td>change_rate</td><td>float</td><td>涨跌幅</td></tr><tr><td>last_close</td><td>float</td><td>昨收价</td></tr></table></body></html>  

# Example  

from futu import \*   
quote_ctx $=$ OpenQuoteContext(host='127.0.0.1', port $=$ 11111)   
ret, data, page_req_key $=$   
quote_ctx.request_history_kline('HK.00700', start $=$ '2019-09-   
11', $e n d{=}\cdot2619\substack{-}69\,{-}18\,^{\prime}$ , max_count ${}^{=5}$ )  # 每页5 个，请求第一页   
if ret $==$ RET_OK: print(data) print(data['code'][0])    # 取第一条的股票代码 print(data['close'].values.tolist())   # 第一页收盘价转为   
list   
else: print('error:', data)   
while page_req_key ! $=$ None:  # 请求后面的所有结果 print('\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*') ret, data, page_req_key $=$   
quote_ctx.request_history_kline('HK.00700', start $=$ '2019-09-   
11', $e n d{=}\cdot2619\substack{-}69\,{-}18\,^{\prime}$ , max_count ${}^{=5}$ , page_req_key $=$ page_req_key)   
# 请求翻页后的数据 if ret $==$ RET_OK: print(data) else: print('error:', data)   
print('All pages are finished!')  

quote_ctx.close() # 结束后记得关闭当条连接，防止连接条数用尽  

# 接口限制  

•  分 K 提供最近 8 年数据，日 K 及以上提供最近 10 年的数据。我们会根据您账户的资产和交易的情况，下发历史 K 线额度。因此，30 天内您只能获取有限只股票的历史 K 线数据。具体规则参见 订阅额度 & 历史 K 线额度。您当日消耗的历史 K 线额度，会在 30 天后自动释放。每 30 秒内最多请求 60 次历史 K 线接口。注意：如果您是分页获取数据，此限频规则仅适用于每只股票的首页，后续页请求不受限频规则的限制。换手率，仅提供日 K 及以上级别。期权，仅提供日K, 1 分K，5 分K，15 分K，60 分K。美股 盘前和盘后 K 线，仅支持 60 分钟及以下级别。由于美股盘前和盘后时段为非常规交易时段，此时段的 K 线数据可能不足 2 年。美股的 成交额，仅提供 2015-10-12 之后的数据。  

# 获取复权因子  

# get_rehab(code)  

介绍  
获取股票的复权因子  
参数  

<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>code</td><td>str</td><td>股票代码</td></tr></table></body></html>  

返回  


<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>ret</td><td>RET CODE</td><td>接口调用结果</td></tr><tr><td rowspan="2">data</td><td>pd.DataFrame</td><td>当 ret RETOK，返回复权数据</td></tr><tr><td>str</td><td>当 ret!= RET OK，返回错误描述</td></tr></table></body></html>  

复权数据格式如下：  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>ex_div_date</td><td>str</td><td>除权除息日</td></tr><tr><td>split_base</td><td>float</td><td>拆股分子</td></tr><tr><td>split_ert</td><td>float</td><td>拆股分母</td></tr><tr><td>join_base</td><td>float</td><td>合股分子</td></tr><tr><td>join_ert</td><td>float</td><td>合股分母</td></tr><tr><td>split_ratio</td><td>float</td><td>拆合股比例</td></tr><tr><td>per_cash_div</td><td>float</td><td>每股派现</td></tr><tr><td>bonus_base</td><td>float</td><td>送股分子</td></tr></table></body></html>  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>bonus_ert</td><td>float</td><td>送股分母</td></tr><tr><td>per_share_div_ratio</td><td>float</td><td>送股比例</td></tr><tr><td>transfer_base</td><td>float</td><td>转增股分子</td></tr><tr><td>transfer_ert</td><td>float</td><td>转增股分母</td></tr><tr><td>per_share_trans_ratio</td><td>float</td><td>转增股比例</td></tr><tr><td>allot_base</td><td>float</td><td>配股分子</td></tr><tr><td>allot_ert</td><td>float</td><td>配股分母</td></tr><tr><td>allotment_ratio</td><td>float</td><td>配股比例</td></tr><tr><td>allotment_price</td><td>float</td><td>配股价</td></tr><tr><td>add_base</td><td>float</td><td>增发股分子</td></tr><tr><td>add_ert</td><td>float</td><td>增发股分母</td></tr><tr><td>stk_spo_ratio</td><td>float</td><td>增发比例</td></tr><tr><td>stk_spo_price</td><td>float</td><td>增发价格</td></tr><tr><td>forward_adj_factorA</td><td>float</td><td>前复权因子 A</td></tr></table></body></html>  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>forward adj factorB</td><td>float</td><td>前复权因子B</td></tr><tr><td>backward adj_factorA</td><td>float</td><td>后复权因子A</td></tr><tr><td>backward_adj_factorB</td><td>float</td><td>后复权因子B</td></tr></table></body></html>  

前复权价格 $=$ 不复权价格 $\times$ 前复权因子 $\textsf{A+}$ 前复权因子 B后复权价格 $=$ 不复权价格 $\times$ 后复权因子 $\textsf{A+}$ 后复权因子 B  

# Example  

from futu import \*quote_ctx $=$ OpenQuoteContext(host $=$ '127.0.0.1', port $=$ 11111)  

ret, data $=$ quote_ctx.get_rehab("HK.00700")   
if ret $==$ RET_OK: print(data) print(data['ex_div_date'][0])    # 取第一条的除权除息日 print(data['ex_div_date'].values.tolist())   # 转为 list   
else: print('error:', data)   
quote_ctx.close() # 结束后记得关闭当条连接，防止连接条数用尽  

# 接口限制  

每 30 秒内最多请求 60 次获取复权因子接口。  

# 筛选窝轮  

get_warrant(stock_owner='', req=None)  

介绍  

筛选窝轮（仅用于筛选香港市场的窝轮、牛熊证、界内证）  

# 参数  

<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>stockowner</td><td>str</td><td>所属正股的股票代码</td></tr><tr><td>req</td><td>WarrantRequest</td><td>筛选参数组合</td></tr></table></body></html>  

WarrantRequest 类型字段说明如下：  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>begin</td><td>int</td><td>数据起始 点</td></tr><tr><td>num</td><td>int</td><td>请求数据 个数</td></tr><tr><td>sort_field</td><td>SortField</td><td>根据哪个 字段排序</td></tr><tr><td>ascend</td><td>bool</td><td>排序方 向</td></tr><tr><td>type_list</td><td>list</td><td>窝轮类型 过滤列 表</td></tr><tr><td>issuer_list</td><td>list</td><td>发行人过 滤列表</td></tr></table></body></html>  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>maturity_time_min</td><td>str</td><td>到期日过 滤范围的 开始时间</td></tr><tr><td>maturity_time_max</td><td>str</td><td>到期日过 滤范围的 结束时间</td></tr><tr><td>ipo_period</td><td>IpoPeriod</td><td>上市时段</td></tr><tr><td>price_type</td><td>PriceType</td><td>价内/价 外</td></tr><tr><td>status</td><td>WarrantStatus</td><td>窝轮状态</td></tr><tr><td>cur_price_min</td><td>float</td><td>最新价的 过滤下 限</td></tr><tr><td>cur_price_max</td><td>float</td><td>最新价的 过滤上 限</td></tr><tr><td>strike_price_min</td><td>float</td><td>行使价的 过滤下 限</td></tr><tr><td>strike_price_max</td><td>float</td><td>行使价的 过滤上 限</td></tr></table></body></html>  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>street_min</td><td>float</td><td>街货占比 的过滤下 限</td></tr><tr><td>street_max</td><td>float</td><td>街货占比 的过滤上 限</td></tr><tr><td>conversion_min</td><td>float</td><td>换股比率 的过滤下 限</td></tr><tr><td>conversion_max</td><td>float</td><td>换股比率 的过滤上 限</td></tr><tr><td>vol_min</td><td>int</td><td>成交量的 过滤下 限</td></tr><tr><td>vol_max</td><td>int</td><td>成交量的 过滤上 限</td></tr><tr><td>premium_min</td><td>float</td><td>溢价的过 滤下限</td></tr></table></body></html>  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>premium_max</td><td>float</td><td>溢价的过 滤上限</td></tr><tr><td>leverage_ratio_min</td><td>float</td><td>杠杆比率 的过滤下 限</td></tr><tr><td>leverage_ratio_max</td><td>float</td><td>杠杆比率 的过滤上 限</td></tr><tr><td>delta_min</td><td>float</td><td>对冲值的 过滤下 限</td></tr><tr><td>delta_max</td><td>float</td><td>对冲值的 过滤上 限</td></tr><tr><td>implied_min</td><td>float</td><td>引伸波幅 的过滤下 限</td></tr><tr><td>implied_max</td><td>float</td><td>引伸波幅 的过滤上 限</td></tr></table></body></html>  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>recovery_price_min</td><td>float</td><td>收回价的 过滤下 限</td></tr><tr><td>recovery_price_max</td><td>float</td><td>收回价的 过滤上 限</td></tr><tr><td>price_recovery_ratio_min</td><td>float</td><td>正股距收 回价的过 滤下限</td></tr><tr><td>price_recovery_ratio_max</td><td>float</td><td>正股距收 回价的过 滤上限</td></tr></table></body></html>  

返回  

<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>ret</td><td>RET CODE</td><td>接口调用结果</td></tr><tr><td rowspan="2">data</td><td>tuple</td><td>当 ret RETOK，返回窝轮数据</td></tr><tr><td>str</td><td>当 ret != RETOK，返回错误描述</td></tr></table></body></html>  

窝轮数据组成如下：  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>data list warrant</td><td>pd. DataFrame</td><td>筛选后的窝轮数据</td></tr></table></body></html>  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>last_page</td><td>bool</td><td>是否是最后一页</td></tr><tr><td>all_count</td><td>int</td><td>筛选结果中的窝轮 总数量</td></tr></table></body></html>  

warrant_data_list 返回的 pd dataframe 数据格式：  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>stock</td><td>str</td><td>窝轮代 码</td></tr><tr><td>stock_owner</td><td>str</td><td>所属正 股</td></tr><tr><td>type</td><td>WrtType</td><td>窝轮类 型</td></tr><tr><td>issuer</td><td>Issuer</td><td>发行人</td></tr><tr><td>maturity_time</td><td>str</td><td>到期 日</td></tr><tr><td>list_time</td><td>str</td><td>上市时 间</td></tr><tr><td>last_trade_time</td><td>str</td><td>最后交 易日</td></tr><tr><td>recovery_price</td><td>float</td><td>收回 价</td></tr></table></body></html>  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td></td><td></td><td></td></tr><tr><td>conversion_ratio</td><td>float</td><td>换股比 率</td></tr><tr><td>lot_size</td><td>int</td><td>每手数 量</td></tr><tr><td>strike_price</td><td>float</td><td>行使价</td></tr><tr><td>last_close_price</td><td>float</td><td>昨收价</td></tr><tr><td>name</td><td>str</td><td>名称</td></tr><tr><td>cur_price</td><td>float</td><td>当前价</td></tr><tr><td>price_change_val</td><td>float</td><td>涨跌额</td></tr><tr><td>status</td><td>WarrantStatus</td><td>窝轮状 态</td></tr><tr><td>bid_price</td><td>float</td><td>买入价</td></tr><tr><td>ask_price</td><td>float</td><td>卖出价</td></tr><tr><td>bid_vol</td><td>int</td><td>买量</td></tr><tr><td>ask_vol</td><td>int</td><td>卖量</td></tr><tr><td>volume</td><td>int</td><td>成交量</td></tr><tr><td>turnover</td><td>float</td><td>成交额</td></tr><tr><td>score</td><td>float</td><td>综合评 分</td></tr><tr><td>premium</td><td>float</td><td>溢价</td></tr><tr><td>break_even_point</td><td>float</td><td>打和点</td></tr></table></body></html>  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>leverage</td><td>float</td><td>杠杆比 率</td></tr><tr><td>ipop</td><td>float</td><td>价内/ 价外</td></tr><tr><td>price_recovery_ratio</td><td>float</td><td>正股距 收回 价</td></tr><tr><td>conversion_price</td><td>float</td><td>换股价</td></tr><tr><td>street_rate</td><td>float</td><td>街货占 比</td></tr><tr><td>street_vol</td><td>int</td><td>街货量</td></tr><tr><td>amplitude</td><td>float</td><td>振幅</td></tr><tr><td>issue_size</td><td>int</td><td>发行量</td></tr><tr><td>high_price</td><td>float</td><td>最高价</td></tr><tr><td>low_price</td><td>float</td><td>最低价</td></tr><tr><td>implied_volatility</td><td>float</td><td>引伸波 幅</td></tr><tr><td>delta</td><td>float</td><td>对冲 值</td></tr></table></body></html>  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td></td><td></td><td></td></tr><tr><td>effective_leverage</td><td>float</td><td>有效杠 杆</td></tr><tr><td>upper_strike_price</td><td>float</td><td>上限 价</td></tr><tr><td>lower_strike_price</td><td>float</td><td>下限 价</td></tr><tr><td>inline_price_status</td><td>PriceType</td><td>界内界 外</td></tr></table></body></html>  

# Example  

• from futu import \*quote_ctx $=$ OpenQuoteContext(host $=$ '127.0.0.1', port $=$ 11111)  

· req $=$ WarrantRequest()   
• req.sort_field $=$ SortField.TURNOVER   
• req.type_list $=$ WrtType.CALL req.cur_price_min $=~\theta.1$   
• req.cur_price_max $=\ \theta\cdot2$   
· ret, ${\sf1s}\ =$ quote_ctx.get_warrant("HK.00700", req) if ret $\L=\textsf{R E T}\_0\ K$ :  # 先判断接口返回是否正常，再取数据 warrant_data_list, last_page, all_count $=$ ls print(len(warrant_data_list), all_count, warrant_data_list)   
• print(warrant_data_list['stock'][0])    # 取第一条的窝轮代码   
• print(warrant_data_list['stock'].values.tolist())   # 转为 list else: print('error: ', ls)  

req $=$ WarrantRequest()  

req.sort_field $=$ SortField.TURNOVER req.issuer_list $=$ ['UB','CS','BI'] ret, ${\sf1s}\ =$ quote_ctx.get_warrant(Market.HK, req)  

if ret $\L=\textsf{R E T}\_0\ K$ :  

print('error: ', ls)  

quote_ctx.close()  # 所有接口结尾加上这条 close，防止连接条数用尽  

# 接口限制  

港股 BMP 权限不支持调用此接口  

每 30 秒内最多请求 60 次筛选窝轮接口  

每次请求的数据个数上限为 200 个  

# 获取历史 K 线额度使用明细  

get_history_kl_quota(get_detail=False)  

介绍  

获取历史 K 线额度使用明细  

参数  

<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>get_detail</td><td>bool</td><td>是否返回拉取历史 K线的详细纪录</td></tr></table></body></html>  

# 返回  

<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>ret</td><td>RET CODE</td><td>接口调用结果</td></tr><tr><td rowspan="2">data</td><td>tuple</td><td>当 ret RETOK，返回历史K线额度数据</td></tr><tr><td>str</td><td>当 ret!= RETOK，返回错误描述</td></tr></table></body></html>  

历史 K 线额度数据格式如下：  


<html><body><table><tr><td>字段</td><td>类 型</td><td>说明</td></tr><tr><td>used_quota</td><td>int</td><td>已用额度</td></tr><tr><td>remain_quota</td><td>int</td><td>剩余额度</td></tr><tr><td>detail list</td><td>list</td><td>拉取历史 K 线的详细纪录，含股 票代码和拉取时间</td></tr></table></body></html>  

detail_list 数据列格式如下  

<html><body><table><tr><td>字段</td><td>类 型</td><td>说明</td></tr><tr><td>code</td><td>str</td><td>股票代码</td></tr><tr><td>name</td><td>str</td><td>股票名称</td></tr><tr><td>request_time</td><td>str</td><td>最后一次拉取的时间字符 串</td></tr></table></body></html>  

Example  

from futu import \*quote_ctx $=$ OpenQuoteContext(host='127.0.0.1', port $=$ 11111)  

ret, data $=$ quote_ctx.get_history_kl_quota(get_detail=True)  #  
设置 true 代表需要返回详细的拉取历史 K 线的记录  
if ret $==$ RET_OK:print(data)  

else:  

print('error:', data) quote_ctx.close() # 结束后记得关闭当条连接，防止连接条数用尽  

# 接口限制  

我们会根据您账户的资产和交易的情况，下发历史 K 线额度。因此，30 天内您只能获取有限只股票的历史 K 线数据。具体规则参见 订阅额度 & 历史 K 线额度。您当日消耗的历史 K 线额度，会在 30 天后自动释放  

# 设置到价提醒  

set_price_reminder(code, op, key=None, reminder_type=None, reminder_freq=None, value=None, note=None)  

介绍新增、删除、修改、启用、禁用指定股票的到价提醒  

参数  

<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>code</td><td>str</td><td>股票代码</td></tr></table></body></html>  

<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>op</td><td>SetPriceReminderOp</td><td>操作类型</td></tr><tr><td>key</td><td>int</td><td>标识，新增和删除全部 的情况不需要填</td></tr><tr><td>reminder_type</td><td>PriceReminderType</td><td>到价提醒的类型，删 除、启用、禁用的情况 下会忽略该入参</td></tr><tr><td>reminder_freq</td><td>PriceReminderFreq</td><td>到价提醒的频率，删 除、启用、禁用的情况 下会忽略该入参</td></tr><tr><td>value</td><td>float</td><td>提醒值，删除、启用、 禁用的情况下会忽略该 入参</td></tr><tr><td>note</td><td>str</td><td>用户设置的备注，仅支 持 20个以内的中文字 符，删除、启用、禁用 的情况下会忽略该入参</td></tr></table></body></html>  

返回  


<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>ret</td><td>RET _CODE</td><td>接口调用结果</td></tr><tr><td rowspan="2">key</td><td>int</td><td>当 ret == RET_OK 时，返回操作的到价提醒 key</td></tr><tr><td>str</td><td>当 ret!= RET_OK，返回错误描述</td></tr></table></body></html>  

Example  

class PriceReminderTest(PriceReminderHandlerBase):  

def on_recv_rsp(self, rsp_pb): ret_code, content $=$  

uper(PriceReminderTest,self).on_recv_rsp(rsp_pb) if ret_code ! $=$ RET_OK: print("PriceReminderTest: error, msg: %s" % content) return RET_ERROR, content print("PriceReminderTest ", content) #  

PriceReminderTest 自己的处理逻辑return RET_OK, content  

quote_ctx $=$ OpenQuoteContext(host='127.0.0.1', port $=$ 11111)   
handler $=$ PriceReminderTest()   
quote_ctx.set_handler(handler)   
ret, data $=$ quote_ctx.get_market_snapshot(['HK.HSImain'])   
if ret $==$ RET_OK: bid_price $=$ data['bid_price'][0]  # 获取实时买一价 ask_price $=$ data['ask_price'][0]  # 获取实时卖一价 # 设置当卖一价低于（ask_price-1）时提醒 ret_ask, ask_data $=$   
quote_ctx.set_price_reminder(code $=$ 'HK.HSImain',   
op=SetPriceReminderOp.ADD, key $\equiv$ None,   
reminder_type $=$ PriceReminderType.ASK_PRICE_DOWN,   
reminder_freq $=$ PriceReminderFreq.ALWAYS, value $=$ (ask_price-1),   
note $^{1=}$ '123')  

if ret_ask $==$ RET_OK:print('卖一价低于（ask_price-1）时提醒设置成功：',  

else: print('error:', ask_data)   
# 设置当买一价高于（bid_price+1）时提醒   
ret_bid, bid_data $=$   
quote_ctx.set_price_reminder(code $=$ 'HK.HSImain',   
op=SetPriceReminderOp.ADD, key $'=$ None,   
reminder_type $=$ PriceReminderType.BID_PRICE_UP,   
reminder_freq $=$ PriceReminderFreq.ALWAYS, value $=$ (bid_price+1),   
note $^{1=}$ '456')  

if ret_bid $==$ RET_OK: print('买一价高于（bid_price $^{+1}$ ）时提醒设置成功：', bid_data) else: print('error:', bid_data)  

time.sleep(15) quote_ctx.close()  

# 提示  

API 中成交量设置统一以股为单位。但是牛牛客户端中，A 股是以手为单位展示  

到价提醒类型，存在最小精度，如下：  

TURNOVER_UP：成交额最小精度为 10 元（人民币元，港元，美元）。传入的数值会自动向下取整到最小精度的整数倍。如果设置  

【00700 成交额102 元提醒】，设置后会得到【00700 成交额100 元提醒】；如果设置【00700 成交额 8 元提醒】，设置后会得到【00700成交额 0 元提醒】。  

VOLUME_UP：A 股成交量最小精度为 1000 股，其他市场股票成交量最小精度为 10 股。传入的数值会自动向下取整到最小精度的整数倍。  

BID_VOL_UP、ASK_VOL_UP：A 股的买一卖一量最小精度为 100 股。  
传入的数值会自动向下取整到最小精度的整数倍。  

其余到价提醒类型精度支持到小数点后 3 位  

# 接口限制  

每 30 秒内最多请求 60 次设置到价提醒接口  

每只股票每种类型可设置的提醒上限是 10 个  

# 获取自选股列表  

get_user_security(group_name)  

介绍  

获取指定分组的自选股列表  

# 参数  

<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>group. name</td><td>str</td><td>需要查询的自选股分组名称</td></tr></table></body></html>  

返回  

<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>ret</td><td>RET CODE</td><td>接口调用结果</td></tr><tr><td rowspan="2">data</td><td>pd.DataFrame</td><td>当 ret RET_OK，返回自选股数据</td></tr><tr><td>str</td><td>当 ret ！二 RETOK，返回错误描述</td></tr></table></body></html>  

自选股数据格式如下：  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>code</td><td>str</td><td>股票代码</td></tr><tr><td>name</td><td>str</td><td>名字</td></tr><tr><td>lot_size</td><td>int</td><td>每手股数，期权表 示每份合约股数, 期货表示合约乘数</td></tr><tr><td>stock_type</td><td>SecurityType</td><td>股票类型</td></tr><tr><td>stock_child_type</td><td>WrtType</td><td>窝轮子类型</td></tr><tr><td>stock_owner</td><td>str</td><td>窝轮所属正股的代 码，或期权标的股 的代码</td></tr><tr><td>option_type</td><td>OptionType</td><td>期权类型</td></tr><tr><td>strike_time</td><td>str</td><td>期权行权日</td></tr></table></body></html>  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td></td><td></td><td></td></tr><tr><td>strike_price</td><td>float</td><td>期权行权价</td></tr><tr><td>suspension</td><td>bool</td><td>期权是否停牌</td></tr><tr><td>listing_date</td><td>str</td><td>上市时间</td></tr><tr><td>stock_id</td><td>int</td><td>股票ID</td></tr><tr><td>delisting</td><td>bool</td><td>是否退市</td></tr><tr><td>main_contract</td><td>bool</td><td>是否主连合约</td></tr><tr><td>last_trade_time</td><td>str</td><td>最后交易时间</td></tr></table></body></html>  

# Example  

from futu import \*quote_ctx $=$ OpenQuoteContext(host $=$ '127.0.0.1', port $=$ 11111)  

ret, data $=$ quote_ctx.get_user_security("A")  
if ret $==$ RET_OK:print(data)if data.shape[0] > 0:  # 如果自选股列表不为空print(data['code'][0])    # 取第一条的股票代码print(data['code'].values.tolist())   # 转为 list  
else:  

print('error:', data) quote_ctx.close() # 结束后记得关闭当条连接，防止连接条数用尽  

# 获取自选股分组  

# get_user_security_group(group_type $=$ UserSecurityGroupType.ALL)  

介绍获取自选股分组列表  

参数返回  

<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>type group</td><td>UserSecurityGroupT ype</td><td>分组类型</td></tr></table></body></html>  

<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>ret</td><td>RET CODE</td><td>接口调用结果</td></tr><tr><td rowspan="2">data</td><td>pd. DataFrame</td><td>当 ret 二二 RETOK，返回自选股分组数 一据</td></tr><tr><td>str</td><td>当 ret!= RET OK，返回错误描述</td></tr></table></body></html>  

自选股分组数据格式如下：  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>group_name</td><td>str</td><td>分组名</td></tr><tr><td>group_type</td><td>UserSecurityGroupType</td><td>分组类型</td></tr></table></body></html>  

Example  

from futu import \*quote_ctx $=$ OpenQuoteContext(host $=$ '127.0.0.1', port $=$ 11111)  

ret, data $=$ quote_ctx.get_user_security_group(group_type =   
UserSecurityGroupType.ALL)   
if ret $==$ RET_OK: print(data)   
else: print('error:', data)   
quote_ctx.close() # 结束后记得关闭当条连接，防止连接条数用尽  

# 修改自选股列表  

modify_user_security(group_name, op, code_list)  

介绍  

修改指定分组的自选股列表（系统分组不支持修改）  

# 参数  

<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>group_name</td><td>str</td><td>需要修改的自选股分组 名称</td></tr><tr><td>op</td><td>ModifyUserSecurityOp</td><td>操作类型</td></tr><tr><td>code_list</td><td>list</td><td>股票列表</td></tr></table></body></html>  

返回  

<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>ret</td><td>RET CODE</td><td>接口调用结果</td></tr><tr><td rowspan="2">msg</td><td rowspan="2">str</td><td>当 ret RET_OK，返回 success</td></tr><tr><td>当 ret != RET OK, msg 返回错误描述</td></tr></table></body></html>  

Example  

quote_ctx $=$ OpenQuoteContext(host $=$ '127.0.0.1', port $=$ 11111)  

ret, data $=$ quote_ctx.modify_user_security("A",   
ModifyUserSecurityOp.ADD, ['HK.00700'])   
if ret $==$ RET_OK: print(data) # 返回 success   
else: print('error:', data)   
quote_ctx.close() # 结束后记得关闭当条连接，防止连接条数用尽  

# 到价提醒回调  

# on_recv_rsp(self, rsp_pb)  

介绍  

到价提醒通知回调，异步处理已设置到价提醒的通知推送。在收到实时到价提醒通知推送后会回调到该函数，您需要在派生类中覆盖 on_recv_rsp。  

参数  


<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>rsp_pb</td><td>Qot_UpdatePriceReminder_pb2. Response</td><td>派生类中 不需要直 接处理该 参数</td></tr></table></body></html>  

返回  
到价提醒  


<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>ret</td><td>RET CODE</td><td>接口调用结果</td></tr><tr><td rowspan="2">data</td><td>dict</td><td>当 ret RETOK，返回到价提醒</td></tr><tr><td>str</td><td>当 ret!= RET OK，返回错误描述</td></tr></table></body></html>  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>code</td><td>str</td><td>股票代 码</td></tr><tr><td>name</td><td>str</td><td>股票名 称</td></tr><tr><td>price</td><td>float</td><td>当前价 格</td></tr><tr><td>change_rate</td><td>str</td><td>当前涨 跌幅</td></tr><tr><td>market_status</td><td>PriceReminderMarketStatus</td><td>触发的 时间段</td></tr><tr><td>content</td><td>str</td><td>到价提 醒文字 内容</td></tr><tr><td>note</td><td>str</td><td>备注</td></tr><tr><td>key</td><td>int</td><td>到价提 醒标识</td></tr><tr><td>reminder_type</td><td>PriceReminderType</td><td>到价提 醒的类 型</td></tr><tr><td>set_value</td><td>float</td><td>用户设 置的提 醒值</td></tr><tr><td>cur_value</td><td>float</td><td>提醒触 发时的 值</td></tr></table></body></html>  

Example from futu import \*  

class PriceReminderTest(PriceReminderHandlerBase):def on_recv_rsp(self, rsp_pb):ret_code, content $=$   
super(PriceReminderTest,self).on_recv_rsp(rsp_pb)if ret_code ! $=$ RET_OK:print("PriceReminderTest: error, msg: %s" % content)return RET_ERROR, contentprint("PriceReminderTest ", content) #  
PriceReminderTest 自己的处理逻辑return RET_OK, content  
quote_ctx $=$ OpenQuoteContext(host='127.0.0.1', port $=$ 11111)  
handler $=$ PriceReminderTest()  
quote_ctx.set_handler(handler)  # 设置到价提醒通知回调  
time.sleep(15)  # 设置脚本接收 OpenD 的推送持续时间为15 秒  
quote_ctx.close()   # 关闭当条连接，OpenD 会在1 分钟后自动取消相应  
股票相应类型的订阅  

# 行情定义  

#累积过滤属性  

StockField  

未知  

# CHANGE_RATE  

涨跌幅  

# AMPLITUDE  

振幅  

![](FutuAPI/f8192983a7231a0c79c2edca313aa47fb281ef0a3e3faf0a580bf773f95a9e04.jpg)  

VOLUME日均成交量  

TURNOVER日均成交额  

# TURNOVER_RATE  

换手率  

# #资产类别  

AssetClass  

UNKNOW未知  

STOCK股票  

BOND 债券  

COMMODITY  

商品  

CURRENCY_MARKET货币市场  

FUTURE 期货  

SWAP掉期（互换）  

#暗盘状态  

DarkStatus  

NONE   
无暗盘交易   
TRADING   
暗盘交易中   
END   
暗盘交易结束  

# #财务过滤属性 StockField  

NONE未知  

NET_PROFIT 净利润  

![](FutuAPI/71c6f75c471a9d200aa5d336d2fa59c44fbe748fe11fb21ab0aa1ec543f548cb.jpg)  

NET_PROFIX_GROWTH  

净利润增长率  

SUM_OF_BUSINESS  

营业收入  

SUM_OF_BUSINESS_GROWTH  

营收同比增长率  

NET_PROFIT_RATE  

净利率  

![](FutuAPI/0e74c807d6e2c1bb51c4ed9095af16a994ffac019ba16035b7c42a6a55e93308.jpg)  

GROSS_PROFIT_RATE  

毛利率  

DEBT_ASSET_RATE  

资产负债率  

![](FutuAPI/363092700ae466ba9da336f07bdb59752d14f95f44a2cf6e1d33ebb098f82af9.jpg)  

RETURN_ON_EQUITY_RATE  

净资产收益率  

![](FutuAPI/6747d392400173a69e512e88e64f000b42a36d27e55e440962a23313a90e67cf.jpg)  

ROIC  

投入资本回报率  

![](FutuAPI/28cd4f3cac183ae274418ed3b4f0436c1f1e0c57dfaadb51f041344ccf248766.jpg)  

ROA_TTM  

资产回报率 TTM  

![](FutuAPI/9665ae751390833cf2be90f57dbf7ff69039946a95672f402984b3b18fd270f2.jpg)  

EBIT_TTM  

息税前利润 TTM  

![](FutuAPI/37c21f5693163451b936402fb570b1f7d0e1d76bfe78b158eea4629c3b6260dd.jpg)  

EBITDA  

税息折旧及摊销前利润  

# OPERATING_MARGIN_TTM  

营业利润率 TTM  

![](FutuAPI/93942770540877afcab1369522e9d2b459a65a3fcdd110f511a0d1a60d9f37bb.jpg)  

# EBIT_MARGIN  

EBIT 利润率  

![](FutuAPI/01a1c8a8ca270b071a9f9a403708eab24fcff98c2a0d18f436e5e0c0c0961f45.jpg)  

EBITDA_MARGIN  

EBITDA 利润率  

FINANCIAL_COST_RATE  

财务成本率  

![](FutuAPI/a56f13d7812613b422f3aca122daa42ffdf91f0f2fa1c99d522955a1f8bfee70.jpg)  

OPERATING_PROFIT_TTM  

营业利润 TTM  

![](FutuAPI/a62b497be60e6529bad929c77453f1780311b275367778278161a13faff65e66.jpg)  

SHAREHOLDER_NET_PROFIT_TTM  

归属于母公司的净利润  

NET_PROFIT_CASH_COVER_TTM  

盈利中的现金收入比例  

CURRENT_RATIO  

流动比率  

QUICK_RATIO  

速动比率  

CURRENT_ASSET_RATIO  

流动资产率  

CURRENT_DEBT_RATIO  

流动负债率  

![](FutuAPI/084da98a4d1e6fd175b671814ae17beb935a8de87361caeb4dd900098d3d119c.jpg)  

EQUITY_MULTIPLIER  

权益乘数  

![](FutuAPI/47fc7194efda217b93c7bd2794965ab60b261cd87f03e42049572059f6019128.jpg)  

PROPERTY_RATIO  

产权比率  

CASH_AND_CASH_EQUIVALENTS  

现金和现金等价物  

TOTAL_ASSET_TURNOVER  

总资产周转率  

FIXED_ASSET_TURNOVER  

固定资产周转率  

INVENTORY_TURNOVER  

存货周转率  

OPERATING_CASH_FLOW_TTM  

经营活动现金流 TTM  

![](FutuAPI/a3a669525a2bf62e8b0755c923f214e561e2af006eb8c051b63c43aef8b3e233.jpg)  

ACCOUNTS_RECEIVABLE  

应收账款净额  

![](FutuAPI/a7383c7ad769a05d2d4de86cac54f2a159f1ff1f8d9a51fc3f79b05d86b5a5b4.jpg)  

EBIT_GROWTH_RATE  

EBIT 同比增长率  

OPERATING_PROFIT_GROWTH_RATE  

营业利润同比增长率  

![](FutuAPI/397d85c710f5728d2cc840f0108ecb6c0ce3868bb35e983bc1c0e59fe36816e3.jpg)  

TOTAL_ASSETS_GROWTH_RATE  

总资产同比增长率  

![](FutuAPI/0d857709aa351a96d3213dffcb5a9a3c19d8454320286a02a96269d72863ae2a.jpg)  

PROFIT_TO_SHAREHOLDERS_GROWTH_RATE  

归母净利润同比增长率  

PROFIT_BEFORE_TAX_GROWTH_RATE  

总利润同比增长率  

EPS_GROWTH_RATE  

EPS 同比增长率  

ROE_GROWTH_RATE  

ROE 同比增长率  

ROIC_GROWTH_RATE  

ROIC 同比增长率  

![](FutuAPI/fcb0a641ec765cfb1e11ddcc3d6a63c67aed466ef71a30fcdd4c2bf885f96519.jpg)  

NOCF_GROWTH_RATE  

经营现金流同比增长率  

![](FutuAPI/8337b061217ceb8d68733e532b9c64bfbe6d2542eb2442e3cf473752792388c6.jpg)  

NOCF_PER_SHARE_GROWTH_RATE  

每股经营现金流同比增长率  

![](FutuAPI/8c866f86649e9e9c76a97f370db3246ea14296411b33b7fcc5e85b48eb1913e8.jpg)  

OPERATING_REVENUE_CASH_COVER  

经营现金收入比  

OPERATING_PROFIT_TO_TOTAL_PROFIT  

营业利润占比  

# BASIC_EPS  

基本每股收益  

DILUTED_EPS  

稀释每股收益  

![](FutuAPI/bf83bc9ed873013194e1a91aa91df464b1409752fce38f408f652bff91d9dcd9.jpg)  

# NOCF_PER_SHARE  

每股经营现金净流量  

i  

# #财务过滤属性周期  

# FinancialQuarter  

NONE未知  

ANNUAL 年报  

FIRST_QUARTER 一季报  

INTERIM 中报  

THIRD_QUARTER 三季报  

最近季报  

# #自定义技术指标属性  

StockField  

NONE   
未知   
PRICE   
最新价格   
MA  

简单均线  

5 日简单均线（不建议使用）  

10 日简单均线（不建议使用）  

# MA20  

20 日简单均线（不建议使用）  

# MA30  

30 日简单均线（不建议使用）  

# MA60  

60 日简单均线（不建议使用）  

# MA120  

120 日简单均线（不建议使用）  

# MA250  

250 日简单均线（不建议使用）  

RSI  

RSI  

![](FutuAPI/b36f84d7d369717bb4152e88ff7c16d64c07b9cc3c9b7e829964a62ad1e5cf84.jpg)  

# EMA  

指数移动均线  

# EMA5  

5 日指数移动均线（不建议使用）  

# EMA10  

10 日指数移动均线（不建议使用）  

# EMA20  

20 日指数移动均线（不建议使用）  

# EMA30  

30 日指数移动均线（不建议使用）  

# EMA60  

60 日指数移动均线（不建议使用）  

# EMA120  

120 日指数移动均线（不建议使用）  

# EMA250  

250 日指数移动均线（不建议使用）  

# KDJ_K  

KDJ 指标的 K 值  

![](FutuAPI/80150f10d204a20e335664fe09866006e30e1f42356a73feb26c33b55fbb3da6.jpg)  

KDJ_D  

KDJ 指标的 D 值  

![](FutuAPI/31275e06d19134fd135df2ca5a7aeb6fe75ceb964681599b6e00e97c8c25c23c.jpg)  

KDJ_J  

KDJ 指标的 J 值  

MACD_DIFF  

MACD 指标的 DIFF 值  

![](FutuAPI/f902e3eea515018b0bc5dbbdad3088ab1a8f35b1d854c64c6a0063b111982a2a.jpg)  

# MACD_DEA  

MACD 指标的 DEA 值  

![](FutuAPI/9ebc02054646f0f2b288468c95d047a44f1fa1aa8b34ead4180accc89ee2e328.jpg)  

MACD  

MACD  

![](FutuAPI/2375a6d28e6c405dadc4a470c296a948d771911872eb2af2def0ac3a29573746.jpg)  

BOLL_UPPER  

BOLL 指标的 UPPER 值  

![](FutuAPI/ede5a757b8c2250e8d46201cef03289ed45d848901478140dd629125ec06bdd4.jpg)  

BOLL_MIDDLER  

BOLL 指标的 MIDDLER 值  

![](FutuAPI/3f58a2daef90cf6164b10a95fd69ed0b6b4bbeed1ef5df9581fa4a9854ac9c87.jpg)  

# BOLL_LOWER  

BOLL 指标的 LOWER 值  

![](FutuAPI/5c64068d9f4761f0a72369381cbfb755154efea91bc3899e98689940930af82f.jpg)  

# VALUE  

自定义数值（stock_field1 不支持此字段）  

# #相对位置  

RelativePosition  

# NONE  

未知  

大于，stock_field1 位于stock_field2 的上方  

# LESS  

小于，stock_field1 位于stock_field2 的下方  

# CROSS_UP  

升穿，stock_field1 从下往上穿stock_field2  

# CROSS_DOWN  

跌穿，stock_field1 从上往下穿stock_field2  

# #形态技术指标属性  

# PatternField  

# NONE  

未知  

# MA_ALIGNMENT_LONG  

MA 多头排列（连续两天MA5>MA10>MA20>MA30>MA60，且当日收盘价大于前一天收盘价）  

# MA_ALIGNMENT_SHORT  

MA 空头排列（连续两天MA5<MA10<MA20<MA30<MA60，且当日收盘价小于前一天收盘价）  

# EMA_ALIGNMENT_LONG  

EMA 多头排列（连续两天EMA5>EMA10>EMA20>EMA30>EMA60，且当日收盘价大于前一天收盘价）  

# EMA_ALIGNMENT_SHORT  

EMA 空头排列（连续两天EMA5<EMA10<EMA20<EMA30<EMA60，且当日收盘价小于前一天收盘价）  

# RSI_GOLD_CROSS_LOW  

RSI 低位金叉（50 以下，短线RSI 上穿长线RSI（前一日短线RSI 小于长线RSI，当日短线RSI 大于长线RSI））  

# RSI_DEATH_CROSS_HIGH  

RSI 高位死叉（50 以上，短线RSI 下穿长线RSI（前一日短线RSI 大于长线RSI，当日短线RSI 小于长线RSI））  

# RSI_TOP_DIVERGENCE  

RSI 顶背离（相邻的两个K 线波峰，后面的波峰对应的CLOSE>前面的波峰对应的CLOSE，后面波峰的RSI12 值<前面波峰的RSI12 值）  

# RSI_ BOTTOM_DIVERGENCE  

RSI 底背离（相邻的两个K 线波谷，后面的波谷对应的CLOSE<前面的波谷对应的CLOSE，后面波谷的RSI12 值>前面波谷的RSI12 值）  

# KDJ_GOLD_CROSS_LOW  

KDJ 低位金叉（D 值小于或等于30，且前一日K 值小于D 值，当日K 值 大于D 值）  

# KDJ_DEATH_CROSS_HIGH  

KDJ 高位死叉（D 值大于或等于70，且前一日K 值大于D 值，当日K 值小于D 值）  

# KDJ_TOP_DIVERGENCE  

KDJ 顶背离（相邻的两个K 线波峰，后面的波峰对应的CLOSE>前面的波峰对应的CLOSE，后面波峰的J 值<前面波峰的J 值）  

# KDJ_BOTTOM_DIVERGENCE  

KDJ 底背离（相邻的两个K 线波谷，后面的波谷对应的CLOSE<前面的波谷对应的CLOSE，后面波谷的J 值>前面波谷的J 值）  

MACD_GOLD_CROSS_LOW  

MACD 低位金叉（DIFF 上穿DEA（前一日DIFF 小于DEA，当日DIFF 大于DEA））  

# MACD_DEATH_CROSS_HIGH  

MACD 高位死叉（DIFF 下穿DEA（前一日DIFF 大于DEA，当日DIFF 小于DEA））  

# MACD_TOP_DIVERGENCE  

MACD 顶背离（相邻的两个K 线波峰，后面的波峰对应的CLOSE>前面的波峰对应的CLOSE，后面波峰的macd 值<前面波峰的macd 值）  

# MACD_BOTTOM_DIVERGENCE  

MACD 底背离（相邻的两个K 线波谷，后面的波谷对应的CLOSE<前面的波谷对应的CLOSE，后面波谷的macd 值>前面波谷的macd 值）  

# BOLL_BREAK_UPPER  

BOLL 突破上轨（前一日股价低于上轨值，当日股价大于上轨值）  

# BOLL_BREAK_LOWER  

BOLL 突破下轨（前一日股价高于下轨值，当日股价小于下轨值）  

# BOLL_CROSS_MIDDLE_UP  

BOLL 向上破中轨（前一日股价低于中轨值，当日股价大于中轨值）  

# BOLL_CROSS_MIDDLE_DOWN  

BOLL 向下破中轨（前一日股价大于中轨值，当日股价小于中轨值）  

#自选股分组类型 UserSecurityGroupType  

NONE  
未知  
CUSTOM  
自定义分组  
SYSTEM  
系统分组  
ALL  
全部分组  

# #指数期权类别  

IndexOptionType  

NONE  
未知  
NORMAL  
普通的指数期权  
SMALL  
小型指数期权  

#上市时段 IpoPeriod  

NONE未知  

TODAY 今日上市  

TOMORROW 明日上市  

NEXTWEEK 未来一周上市  

LASTWEEK 过去一周上市  

LASTMONTH 过去一月上市  

# #窝轮发行商  

# Issuer  

UNKNOW未知  

SG法兴  

BP法巴  

CS瑞信  

# CT  

花旗  

EA东亚  

GS高盛  

HS 汇丰  

JP摩通  

MB 麦银  

SC 渣打  

UB 瑞银  

BI 中银  

DB德银  

DC大和  

ML美林  

NM  

野村  

RB荷合  

RS苏皇  

BC 巴克莱  

HT海通  

VT瑞通  

KC比联  

MS摩利  

GJ国君  

XZ星展  

HU华泰  

KS韩投  

CI  

信证  

# #K 线字段  

# KL_FIELD  

ALL所有  

DATE_TIME时间  

HIGH最高价  

OPEN 开盘价  

LOW 最低价  

CLOSE 收盘价  

LAST_CLOSE 昨收价  

TRADE_VOL成交量  

TRADE_VAL 成交额  

TURNOVER_RATE换手率  

PE_RATIO 市盈率  

CHANGE_RATE 涨跌幅  

# #K 线类型 KLType  

NONE未知  

K_1M1 分 K  

K_DAY日 K  

K_WEE 周 K  

月 Ki  

K_YEAR年 K  

![](FutuAPI/35b77a352e7ae1038a9cc191246716fc176d618a81ed465c7b11c5e972bb6cc5.jpg)  

K_5M5 分 K  

K_15M15 分 K  

K_30M30 分 K  

K_60M60 分 K  

K_3M3 分 K  

季 K  

#周期类型  

INTRADAY实时  

DAY日  

# WEEK 周  

MONTH月  

#到价提醒市场状态 PriceReminderMarketStatus  

UNKNOW  
未知  
OPEN  
盘中  
USPRE  
美股盘前  

USAFTER 美股盘后 #自选股操作 ModifyUserSecurityOp  

NONE未知  

ADD 新增  

DEL 删除自选  

MOVE_OUT 移出分组  

# #期权类型（按行权时间）  

OptionAreaType  

NONE  
未知  
AMERICAN  
美式  
EUROPEAN  
欧式  
BERMUDA  
百慕大  

# #期权价内/外  

# OptionCondType  

ALL所有  

WITHIN价内  

OUTSIDE 价外  

# #期权类型 （按方向）OptionType  

ALL所有  

CALL 看涨期权  

PUT 看跌期权  

# #板块集合类型  

# Plate  

ALL所有板块  

INDUSTRY 行业板块  

REGION地域板块  

CONCEPT 概念板块  

OTHER其他板块  

# #到价提醒频率  

PriceReminderFreq  

NONE  
未知  
ALWAYS  
持续提醒  
ONCE_A_DAY  
每日一次  
ONCE  
仅提醒一次  

# #到价提醒类型  

PriceReminderType  

NONE未知  

PRICE_UP价格涨到  

PRICE_DOWN价格跌到  

# CHANGE_RATE_UP  

日涨幅超  

# CHANGE_RATE_DOWN  

日跌幅超  

# FIVE_MIN_CHANGE_RATE_UP  

5 分钟涨幅超  

FIVE_MIN_CHANGE_RATE_DOWN  

5 分钟跌幅超  

VOLUME_UP  

成交量超过  

TURNOVER_UP  

成交额超过  

# TURNOVER_RATE_UP  

换手率超过  

![](FutuAPI/875e213389a831a0dad6ab74c901ee68ad61003a7fb2a1145bfd83f36e62316a.jpg)  

BID_PRICE_UP买一价高于  

ASK_PRICE_DOWN卖一价低于  

BID_VOL_UP买一量高于  

ASK_VOL_UP卖一量高于  

THREE_MIN_CHANGE_RATE_UP  

3 分钟涨幅超  

THREE_MIN_CHANGE_RATE_DOWN  

3 分钟跌幅超  

#窝轮价内/外  

PriceType  

UNKNOW未知  

OUTSIDE  

价外，界内证表示界外  

WITH_IN价内，界内证表示界内  

# #逐笔推送类型  

# PushDataType  

# UNKNOW  

未知  

实时推送的数据  

# BYDISCONN  

与富途服务器连接断开期间，拉取补充的数据  

![](FutuAPI/e30605147bddb6c1ce511d7bfa0b569a6459222a7b206e7be0ec7d4935ffd4d4.jpg)  

CACHE非实时非连接断开补充数据  

# #行情市场  

# Market  

未知市场  

HK香港市场  

US  

美国市场  

SH沪股市场  

SZ深股市场  

SG新加坡市场  

JP日本市场  

AU澳大利亚市场  

CA加拿大市场  

MY马来西亚市场  

FX外汇市场  

# #市场状态  

# MarketState  

各市场状态的对应时段：点击这里了解更多  

NONE 无交易  

AUCTION  

盘前竞价  

WAITING_OPEN 等待开盘  

MORNING 早盘  

REST 午间休市  

AFTERNOON午盘 / 美股持续交易时段  

CLOSED 收盘  

PRE_MARKET_BEGIN美股盘前交易时段  

PRE_MARKET_END 美股盘前交易结束  

AFTER_HOURS_BEGIN美股盘后交易时段  

AFTER_HOURS_END 美股盘后结束  

NIGHT_OPEN夜市交易时段  

NIGHT_END 夜市收盘  

NIGHT美指期权夜市交易时段  

TRADE_AT_LAST美指期权盘尾交易时段  

FUTURE_DAY_OPEN日市交易时段  

FUTURE_DAY_BREAK 日市休市  

FUTURE_DAY_CLOSE 日市收盘  

FUTURE_DAY_WAIT_OPEN 期货待开盘  

HK_CAS 港股盘后竞价  

FUTURE_NIGHT_WAIT夜市等待开盘（已废弃）  

FUTURE_AFTERNOON期货下午开盘（已废弃）  

FUTURE_SWITCH_DATE 美期待开盘  

FUTURE_OPEN美期交易时段  

FUTURE_BREAK美期中盘休息  

FUTURE_BREAK_OVER美期休息后交易时段  

FUTURE_CLOSE 美期收盘  

# STIB_AFTER_HOURS_WAIT  

科创板的盘后撮合时段（已废弃）  

STIB_AFTER_HOURS_BEGIN科创板的盘后交易开始（已废弃）  

# STIB_AFTER_HOURS_END  

科创板的盘后交易结束（已废弃）  

# #行情权限  

# QotRight  

# UNKNOW  

未知  

BMP（此权限不支持订阅）  

# LEVEL1  

Level1  

# LEVEL2  

Level2  

SF  

港股 SF 高级全盘行情  

NO无权限  

# #关联数据类型  

SecurityReferenceType  

UNKNOW未知  

WARRANT 正股相关的窝轮  

FUTURE 期货主连的相关合约 #K 线复权类型 AuType  

NONE  
不复权QFQ  
前复权HFQ  
后复权  

#股票状态 SecurityStatus  

NONE未知  

NORMAL 正常状态  

LISTING 待上市  

PURCHASING申购中  

SUBSCRIBING认购中  

BEFORE_DRAK_TRADE_OPENING暗盘开盘前  

DRAK_TRADING暗盘交易中  

DRAK_TRADE_END 暗盘已收盘  

TO_BE_OPEN 待开盘  

SUSPENDED停牌  

CALLED 已收回  

EXPIRED_LAST_TRADING_DATE已过最后交易日  

EXPIRED已过期  

DELISTED 已退市  

CHANGE_TO_TEMPORARY_CODE公司行动中，交易关闭，转至临时代码交易  

TEMPORARY_CODE_TRADE_END 临时买卖结束，交易关闭  

CHANGED_PLATE_TRADE_END 已转板，旧代码交易关闭  

CHANGED_CODE_TRADE_END 已换代码，旧代码交易关闭  

RECOVERABLE_CIRCUIT_BREAKER  

可恢复性熔断  

UN_RECOVERABLE_CIRCUIT_BREAKER  

不可恢复性熔断  

AFTER_COMBINATION盘后撮合  

AFTER_TRANSATION 盘后交易  

# #股票类型  

# SecurityType  

NONE  

未知  

BOND 债券  

BWRT 一揽子权证  

STOCK正股  

ETF信托,基金  

WARRANT 窝轮  

IDX指数  

PLATE 板块  

DRVT 期权  

PLATESET板块集  

FUTURE 期货  

#设置到价提醒操作类型 SetPriceReminderOp  

NONE未知  

ADD 新增  

DEL 删除  

ENABLE启用  

DISABLE禁用  

MODIFY 修改  

DEL_ALL删除全部（删除指定股票下的所有到价提醒）  

# #排序方向  

# SortDir  

NONE 不排序  

ASCEND 升序  

DESCEND 降序  

# #排序字段  

# SortField  

NONE未知  

CODE代码  

CUR_PRICE 最新价  

PRICE_CHANGE_VAL 涨跌额  

CHANGE_RATE 涨跌幅 %  

STATUS 状态  

BID_PRICE 买入价  

ASK_PRICE 卖出价  

BID_VOL买量  

ASK_VOL卖量  

# VOLUME  

成交量  

TURNOVER 成交额  

AMPLITUDE振幅 $\%$  

SCORE综合评分  

PREMIUM 溢价 %  

EFFECTIVE_LEVERAGE 有效杠杆  

# DELTA  

对冲值  

![](FutuAPI/a973fd2e59a12377b576cde22dc0c8d50f7690792324865c739ec0f2b3ff505a.jpg)  

IMPLIED_VOLATILITY  

引伸波幅  

![](FutuAPI/285007bb2aac9a2d131829b6c21aebf0b0f39a7537ed068a8c7d42b5a3bc3feb.jpg)  

TYPE类型  

STRIKE_PRICE  

行权价  

BREAK_EVEN_POINT打和点  

MATURITY_TIME到期日  

LIST_TIME上市日期  

LAST_TRADE_TIME最后交易日  

LEVERAGE 杠杆比率  

IN_OUT_MONEY 价内/价外 %  

# RECOVERY_PRICE  

收回价  

![](FutuAPI/16c20d5b06b60fe5188627eebfedc0927d0ac485b8a13e8066f8b98c7c8d6334.jpg)  

CHANGE_PRICE 换股价  

CHANGE 换股比率  

STREET_RATE街货比 $\%$  

STREET_VOL街货量  

WARRANT_NAME窝轮名称  

ISSUER发行人  

LOT_SIZE每手  

ISSUE_SIZE发行量  

# UPPER_STRIKE_PRICE  

上限价  

![](FutuAPI/aaaf76822d0ec0de64020cb01a82916f84547dc35265f6eef588c62a65257b56.jpg)  

LOWER_STRIKE_PRICE  

下限价  

![](FutuAPI/73af40d1b013a1a16daaca94f05222d27b07eea8348345598de7e648f0d86fe2.jpg)  

INLINE_PRICE_STATUS  

界内界外  

PRE_CUR_PRICE  

盘前最新价  

AFTER_CUR_PRICE 盘后最新价  

PRE_PRICE_CHANGE_VAL 盘前涨跌额  

AFTER_PRICE_CHANGE_VAL 盘后涨跌额  

PRE_CHANGE_RATE盘前涨跌幅 $\%$  

AFTER_CHANGE_RATE 盘后涨跌幅 $\%$  

PRE_AMPLITUDE盘前振幅 $\%$  

AFTER_AMPLITUDE盘后振幅 $\%$  

PRE_TURNOVER 盘前成交额  

AFTER_TURNOVER 盘后成交额  

LAST_SETTLE_PRICE 昨结  

POSITION持仓量  

POSITION_CHANGE日增仓  

# #简单过滤属性  

# StockField  

# NONE  

未知  

STOCK_CODE股票代码，不能填区间上下限值。  

STOCK_NAME股票名称，不能填区间上下限值。  

# CUR_PRICE  

最新价  

![](FutuAPI/e3b629dc65b74668c6e42da4cc42df2beee3e020469541b0d27e0318ccba8dcd.jpg)  

CP：现价  

CUR_PRICE_TO_LOWEST52_WEEKS_RATIO  

CP：现价  

WL52：52 周最低  

对应 PC 端“离 52 周低点百分比”  

HIGH_PRICE_TO_HIGHEST52_WEEKS_RATIO  

(TH - WH52) / WH52TH：今日最高  

WH52：52 周最高  

LOW_PRICE_TO_LOWEST52_WEEKS_RATIO  

(TL - WL52) / WL52  

TL：今日最低  

WL52：52 周最低  

VOLUME_RATIO  

# BID_ASK_RATIO  

委比  

![](FutuAPI/eb5dd93cb999b0a9f448783d684200cdbf22f3f83472a26d71675d5491f5c416.jpg)  

# LOT_PRICE  

每手价格  

![](FutuAPI/1069241054d89391bf51383fb22e828f9fb962b0710c523a2e6b9490de975ca0.jpg)  

# MARKET_VAL  

市值  

![](FutuAPI/c863109438e193f69b2efdd58a9987c95f1c39a91f502899603d1364cc1c39ed.jpg)  

# PE_ANNUAL  

市盈率(静态)  

![](FutuAPI/b0a25bab39a18e50f733ed8b0b02c591d518421de65a75db08f506ed70939a7f.jpg)  

# PE_TTM  

市盈率 TTM  

![](FutuAPI/8ac494927a01a927a94f24c9a7df42636d28dbb458f227a89390836608935d48.jpg)  

PB_RATE  

市净率  

![](FutuAPI/7b27cd4e9862f09b3844cf210d814965d22c0c964c1ac62e3922cf11415e0472.jpg)  

CHANGE_RATE_5MIN  

五分钟价格涨跌幅  

CHANGE_RATE_BEGIN_YEAR  

年初至今价格涨跌幅  

![](FutuAPI/88aec6f84345e11e2fdae1f37ac01d4276f45d186c61af9937fed7d9fe00a578.jpg)  

# PS_TTM  

市销率 TTM  

![](FutuAPI/c6bab128a87fbdc6652b31997467abb3e6d04c142fdeddecd580953ebf796e8e.jpg)  

PCF_TTM  

市现率 TTM  

![](FutuAPI/81543eeaa3d25d684dd4dd1057ca14dc801084f2726eaa413de0c25470e12e3b.jpg)  

TOTAL_SHARE  

总股数  

![](FutuAPI/07a53c823d60c7730659530ea5b19d73e258b5d055448c51efe114b5a859657c.jpg)  

FLOAT_SHARE  

流通股数  

![](FutuAPI/dce58f7fdde2b983bf413f8ff983c2f57265726bf1726a0a78b3f3581d70da6a.jpg)  

FLOAT_MARKET_VAL 流通市值  

# #订阅类型  

# SubType  

NONE未知  

QUOTE 基础报价  

ORDER_BOOK 摆盘  

TICKER 逐笔  

RT_DATA分时  

K_DAY日 K  

K_5M  

5 分 K  

K_15M15 分 K  

K_30M30 分 K  

K_60M60 分 K  

K_1M1 分 K  

K_WEEK 周 K  

K_MON月 K  

BROKER 经纪队列  

K_QURATER季 K  

K_YEAR年 K  

K_3M3 分 K  

# #逐笔成交方向  

TickerDirect  

NONE未知  

BUY 外盘  

SELL 内盘  

NEUTRA 中性盘  

# #逐笔成交类型  

TickerType  

UNKNOWN未知  

AUTO_MATCH 自动对盘  

LATE 开市前成交盘  

NON_AUTO_MATCH 非自动对盘  

INTER_AUTO_MATCH 同一证券商自动对盘  

INTER_NON_AUTO_MATCH 同一证券商非自动对盘  

ODD_LOT 碎股交易  

AUCTION 竞价交易  

BULK 批量交易  

CRASH现金交易  

CROSS_MARKET 跨市场交易  

BULK_SOLD批量卖出  

FREE_ON_BOARD 离价交易  

# RULE127_OR155  

第 127 条交易（纽交所规则）或第 155 条交易  

DELAY 延迟交易  

MARKET_CENTER_CLOSE_PRICE中央收市价  

# NEXT_DAY  

隔日交易  

# MARKET_CENTER_OPENING  

中央开盘价交易  

# PRIOR_REFERENCE_PRICE  

前参考价  

# MARKET_CENTER_OPEN_PRICE  

中央开盘价  

# SELLER  

卖方  

T  

T 类交易（盘前和盘后交易）  

# EXTENDED_TRADING_HOURS  

延长交易时段  

# CONTINGENT  

合单交易  

AVERAGE_PRICE  

平均价成交  

OTC_SOLD场外售出  

ODD_LOT_CROSS_MARKET 碎股跨市场交易  

DERIVATIVELY_PRICED衍生工具定价  

REOPENINGP_RICED 再开盘定价  

收盘定价  

COMPREHENSIVE_DELAY_PRICE  

综合延迟价格  

OVERSEAS交易的一方不是香港交易所的成员，属于场外交易  

# #交易日查询市场  

# TradeDateMarket  

# NONE  

未知  

香港市场  

US美国市场  

![](FutuAPI/fef6d565d20b0b69d66e66ea4fde3b53c4abbc2afb705583179284a6352e1e20.jpg)  

CNA 股市场  

NT深（沪）股通  

ST港股通（深、沪）  

JP_FUTURE日本期货  

SG_FUTURE新加坡期货  

# #交易日类型  

# TradeDateType  

WHOLE 全天交易  

MORNING上午交易，下午休市  

AFTERNOON下午交易，上午休市  

# #窝轮状态  

# WarrantStatus  

NONE未知  

NORMAL 正常状态  

SUSPEND停牌  

STOP_TRADE 终止交易  

PENDING_LISTING 等待上市  

# #窝轮类型  

# WrtType  

NONE未知  

CALL 认购窝轮  

PUT 认沽窝轮  

BULL 牛证  

BEAR 熊证  

INLINE界内证  

# #所属交易所  

# ExchType  

NONE未知  

HK_MAINBOARD港交所·主板  

HK_GEMBOARD 港交所·创业板  

HK_HKEX港交所  

US_NYSE纽交所  

US_NASDAQ纳斯达克  

US_PINKOTC 市场  

US_AMEX  

美交所  

US_OPTION美国  

US_NYMEX NYMEX  

US_COMEX COMEX  

US_CBOT CBOT  

US_CME CME  

US_CBOE CBOE  

CN_SH上交所  

CN_SZ深交所  

CN_STIB科创板  

# SG_SGX  

新交所  

# JP_OSE  

大阪交易所  

# #证券标识  

交易接口总览  


<html><body><table><tr><td>模块</td><td>接口名</td><td>功能简介</td></tr><tr><td rowspan="2">账户</td><td>Get Account List</td><td>获取交易业务账户列 表</td></tr><tr><td>Unlock Trading</td><td>解锁交易</td></tr><tr><td rowspan="4">资产持 仓</td><td>Get Account Financial Information</td><td>获取账户资金数据</td></tr><tr><td>Get Maximum Tradable Quantity</td><td>查询账户最大可买卖 数量</td></tr><tr><td>Get Positions List</td><td>获取持仓列表</td></tr><tr><td>Get Margin Trading Data</td><td>获取融资融券数据</td></tr><tr><td rowspan="6">订单</td><td>Place Order</td><td>下单</td></tr><tr><td>Modify or Cancel Order</td><td>改单撤单</td></tr><tr><td>Get Order list</td><td>查询未完成订单</td></tr><tr><td>Get Order Fees</td><td>查询订单费用</td></tr><tr><td>Get Historical Order List</td><td>查询历史订单</td></tr><tr><td>Order Callback</td><td>订单回调</td></tr></table></body></html>  

<html><body><table><tr><td></td><td>Trade Data Callback</td><td>订阅交易推送</td></tr><tr><td rowspan="3">成交</td><td>Get Today' s Executed Trades</td><td>查询当日成交</td></tr><tr><td>Get Historical Executed Trades</td><td>查询历史成交</td></tr><tr><td>Trade Execution Callback</td><td>成交回调</td></tr></table></body></html>  

# 交易对象  

# #创建连接  

OpenSecTradeContext(filter_trdmarket $=$ TrdMarket.HK, host $=$ '127.0.0.1', port=11111, is_encrypt $=$ None, security_firm $\lvert=$ SecurityFirm.FUTUSECURITIES)  

OpenFutureTradeContext(host $=$ '127.0.0.1', port $=$ 11111, is_encrypt $=$ None, security_firm $\lvert=$ SecurityFirm.FUTUSECURITIES)  

介绍根据交易品类，选择账户，并创建对应的交易对象。  

<html><body><table><tr><td>实例</td><td>账户</td></tr><tr><td>OpenSecTradeContext</td><td>证券账户</td></tr><tr><td>OpenFutureTradeContext</td><td>期货账户</td></tr></table></body></html>  

参数  

<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>filter_trdmarket</td><td>TrdMarket</td><td>筛选对应交易市场权限的 账户</td></tr><tr><td>host</td><td>str</td><td>OpenD 监听的 IP 地址</td></tr><tr><td>port</td><td>int</td><td>OpenD监听的IP 端口</td></tr><tr><td>is_encrypt</td><td>bool</td><td>是否启用加密</td></tr><tr><td>security_firm</td><td>SecurityFirm</td><td>所属券商</td></tr></table></body></html>  

# Example  

from futu import \*   
trd_ctx $=$ OpenSecTradeContext(filter_trdmarket $=$ TrdMarket.HK,   
host $=$ '127.0.0.1', port $=$ 11111, is_encrypt $=$ None,   
security_firm $=$ SecurityFirm.FUTUSECURITIES)   
trd_ctx.close() # 结束后记得关闭当条连接，防止连接条数用尽  

# 关闭连接  

# close()  

介绍  

关闭交易对象。默认情况下，Futu API 内部创建的线程会阻止进程退出，只有当所有 Context 都 close 后，进程才能正常退出。但通过 set_all_thread_daemon 可以设置所有内部线程为 daemon 线程，这时即使没有调用 Context 的 close，进程也可以正常退出。  

# Example  

from futu import \*   
trd_ctx $=$ OpenSecTradeContext(filter_trdmarket=TrdMarket.HK,   
host $=$ '127.0.0.1', port $=$ 11111)   
trd_ctx.close()  # 结束后记得关闭当条连接，防止连接条数用尽  

# 获取交易业务账户列表  

# get_acc_list()  

# 介绍  

获取交易业务账户列表。  
要调用其他交易接口前，请先获取此列表，确认要操作的交易业务账户无误。  

# 参数  

返回  

<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>ret</td><td>RET CODE</td><td>接口调用结果</td></tr><tr><td rowspan="2">data</td><td>pd. DataFrame</td><td>当 ret == RETOK时，返回交易业务账 户列表</td></tr><tr><td>str</td><td>当 ret!= RET OK 时，返回错误描述</td></tr></table></body></html>  

交易业务账户列表格式如下：  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>acc_id</td><td>int</td><td>交易业务账户</td></tr><tr><td>trd_env</td><td>TrdEnv</td><td>交易环境</td></tr><tr><td>acc_type</td><td>TrdAccType</td><td>账户类型</td></tr><tr><td>uni_card_num</td><td>str</td><td>综合账户卡号，同移 动端内的展示</td></tr></table></body></html>  

![](FutuAPI/f855ff2dcc61ba6850df47b5478ac5c8938ad2318983d918b02e868a5aba7b0c.jpg)  

# 说明  

当开通了港/美股期权模拟交易后，此函数在获取港/美交易账号列表时，会返回2 个模拟交易账号。其中第1 个为原先的账号，第2 个是期权模拟交易账号。  

Example  

from futu import \*   
trd_ctx $=$ OpenSecTradeContext(filter_trdmarket $=$ TrdMarket.HK,   
host $=$ '127.0.0.1', port $=$ 11111,   
security_firm $=$ SecurityFirm.FUTUSECURITIES)   
ret, data $=$ trd_ctx.get_acc_list()   
if ret $==$ RET_OK: print(data) print(data['acc_id'][0])  # 取第一个账号 print(data['acc_id'].values.tolist())  # 转为 list   
else: print('get_acc_list error: ', data)   
trd_ctx.close()  

# 解锁交易  

unlock_trade(password=None, password_md5=None, is_unlock=True)  

介绍解锁或锁定交易  

参数返回  

<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>password</td><td>str</td><td>交易密码</td></tr><tr><td>password_md5</td><td>str</td><td>交易密码的32 位 MD5加密（全小写)</td></tr><tr><td>is_unlock</td><td>bool</td><td>解锁或锁定</td></tr></table></body></html>  

<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>ret</td><td>RET CODE</td><td>接口调用结果</td></tr><tr><td rowspan="2">msg</td><td>NoneType</td><td>当 ret RETOK时，返回 None</td></tr><tr><td>str</td><td>当 ret！= RET_OK 时，返回错误描述</td></tr></table></body></html>  

Example  

from futu import \* pwd_unloc $\mathrm{~\textit~{~k~}~}=\mathrm{~\textit~{~}~}^{\prime}\boldsymbol{1}23$ 456'  

trd_ctx $=$ OpenSecTradeContext(filter_trdmarket=TrdMarket.HK,  
host $=$ '127.0.0.1', port $=$ 11111,  
security_firm $=$ SecurityFirm.FUTUSECURITIES)  
ret, data $=$ trd_ctx.unlock_trade(pwd_unlock)  
if ret $==$ RET_OK:print('unlock success!')  
else:print('unlock_trade failed: ', data)  
trd_ctx.close()真实账户调用 下单 或 改单撤单 接口，需要先解锁交易；模拟账户无需解锁。  
解锁或锁定交易针是对 OpenD 的操作，只要有一个连接解锁，其他连接都可以调用交易接口。  
强烈建议，通过外网连接 OpenD 进行实盘交易的客户，使用加密通道，参见 启用协议加密。  
OpenAPI 不支持富途令牌，如果开通了富途令牌，则会解锁失败，需要关闭令牌功能后再使用 OpenAPI 解锁。  

# 接口限制  

每 30 秒内最多请求 10 次解锁交易接口  

# 查询账户资金  

accinfo_query(trd_env=TrdEnv.REAL, acc_id $=0$ , acc_index $=0$ , refresh_cache=False, currency=Currency.HKD)  

介绍  
查询交易业务账户的资产净值、证券市值、现金、购买力等资金数据。参数  

<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>trd_env</td><td>TrdEnv</td><td>交易环境</td></tr><tr><td>acc_id</td><td>int</td><td>交易业务账户ID</td></tr><tr><td>acc_index</td><td>int</td><td>交易业务账户列表中的账户序号</td></tr><tr><td>refresh_cache</td><td>bool</td><td>是否刷新缓存</td></tr><tr><td>currency</td><td>Currency</td><td>计价货币</td></tr></table></body></html>  

返回  

<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>ret</td><td>RET CODE</td><td>接口调用结果</td></tr><tr><td rowspan="2">data</td><td>pd.DataFrame</td><td>当 ret 二二 ：RETOK时，返回资金数据</td></tr><tr><td>str</td><td>当 ret!= RET_OK 时，返回错误描述</td></tr></table></body></html>  

资金数据格式如下：  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>power</td><td>float</td><td>最大购买 力</td></tr><tr><td>max_power_short</td><td>float</td><td>卖空购买 力</td></tr></table></body></html>  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td></td><td></td><td></td></tr><tr><td>net_cash_power</td><td>float</td><td>现金购买 力</td></tr><tr><td>total_assets</td><td>float</td><td>总资产净 值</td></tr><tr><td>securities_assets</td><td>float</td><td>证券资产 净值</td></tr><tr><td>funds_assets</td><td>float</td><td>基金资产 净值</td></tr><tr><td>bonds_assets</td><td>float</td><td>债券资产 净值</td></tr><tr><td>cash</td><td>float</td><td>现金</td></tr><tr><td>market_val</td><td>float</td><td>证券市 值</td></tr><tr><td>long_mv</td><td>float</td><td>多头市值</td></tr><tr><td>short_mv</td><td>float</td><td>空头市值</td></tr><tr><td>pending_asset</td><td>float</td><td>在途资产</td></tr></table></body></html>  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>interest_charged_amount</td><td>float</td><td>计息金额</td></tr><tr><td>frozen_cash</td><td>float</td><td>冻结资金</td></tr><tr><td>avl_withdrawal_cash</td><td>float</td><td>现金可 提</td></tr><tr><td>max_withdrawal</td><td>float</td><td>最大可 提</td></tr><tr><td>currency</td><td>Currency</td><td>计价货 币</td></tr><tr><td>available_funds</td><td>float</td><td>可用资 金</td></tr><tr><td>unrealized_pl</td><td>float</td><td>未实现盈 亏</td></tr><tr><td>realized_pl</td><td>float</td><td>已实现盈 亏</td></tr><tr><td>risk_level</td><td>CltRiskLevel</td><td>风控状 态</td></tr><tr><td>risk_status</td><td>CltRiskStatus</td><td>风险状 态</td></tr></table></body></html>  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td></td><td></td><td></td></tr><tr><td>initial_margin</td><td>float</td><td>初始保证 金</td></tr><tr><td>margin_call_margin</td><td>float</td><td>Margin Call 保证 金</td></tr><tr><td>maintenance_margin</td><td>float</td><td>维持保证 金</td></tr><tr><td>hk_cash</td><td>float</td><td>港元现 金</td></tr><tr><td>hk_avl_withdrawal_cash</td><td>float</td><td>港元可 提</td></tr><tr><td>hkd_net_cash_power</td><td>float</td><td>港元现金 购买力</td></tr><tr><td>hkd_assets</td><td>float</td><td>港股资产 净值</td></tr><tr><td>us_cash</td><td>float</td><td>美元现 金</td></tr><tr><td>us_avl_withdrawal_cash</td><td>float</td><td>美元可 提</td></tr></table></body></html>  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>usd_net_cash_power</td><td>float</td><td>美元现金 购买力</td></tr><tr><td>usd_assets</td><td>float</td><td>美股资产 净值</td></tr><tr><td>cn_cash</td><td>float</td><td>人民币现 金</td></tr><tr><td>cn_avl_withdrawal_cash</td><td>float</td><td>人民币可 提</td></tr><tr><td>cnh_net_cash_power</td><td>float</td><td>人民币现 金购买 力</td></tr><tr><td>cnh_assets</td><td>float</td><td>A股资产 净值</td></tr><tr><td>jp_cash</td><td>float</td><td>日元现 金</td></tr><tr><td>jp_avl_withdrawal_cash</td><td>float</td><td>日元可 提</td></tr></table></body></html>  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>jpy_net_cash_power</td><td>float</td><td>日元现金 购买力</td></tr><tr><td>jpy_assets</td><td>float</td><td>日股资产 净值</td></tr><tr><td>sg_cash</td><td>float</td><td>新元现 金</td></tr><tr><td>sg_avl_withdrawal_cash</td><td>float</td><td>新元可 提</td></tr><tr><td>sgd_net_cash_power</td><td>float</td><td>新元现金 购买力</td></tr><tr><td>sgd_assets</td><td>float</td><td>新股资产 净值</td></tr><tr><td>au_cash</td><td>float</td><td>澳元现 金</td></tr><tr><td>au_avl_withdrawal_cash</td><td>float</td><td>澳元可 提</td></tr></table></body></html>  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>aud_net_cash_power</td><td>float</td><td>澳元现金 购买力</td></tr><tr><td>aud_assets</td><td>float</td><td>澳股资产 净值</td></tr><tr><td>is_pdt</td><td>bool</td><td>是否为 PDT账 户</td></tr><tr><td>pdt_seq</td><td>string</td><td>剩余日内 交易次 数</td></tr><tr><td>beginning_dtbp</td><td>float</td><td>初始日内 交易购买 力</td></tr><tr><td>remaining_dtbp</td><td>float</td><td>剩余日内 交易购买 力</td></tr><tr><td>dt_call_amount</td><td>float</td><td>日内交易 待缴金 额</td></tr></table></body></html>  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>dt_status</td><td>DtStatus</td><td>日内交易 限制情 况</td></tr></table></body></html>  

Example  

from futu import \*   
trd_ctx $=$ OpenSecTradeContext(filter_trdmarket $=$ TrdMarket.HK,   
host $=^{\prime}$ '127.0.0.1', port $=$ 11111,   
security_firm $=$ SecurityFirm.FUTUSECURITIES)   
ret, data $=$ trd_ctx.accinfo_query()   
if ret $==$ RET_OK: print(data) print(data['power'][0])  # 取第一行的购买力 print(data['power'].values.tolist())  # 转为 list   
else: print('accinfo_query error: ', data)   
trd_ctx.close()  # 关闭当条连接  

# 接口限制  

每 30 秒内最多请求 10 次查询账户资金接口调用此接口，只有在刷新缓存时，才受到限频限制  

# 查询最大可买可卖  

acctradinginfo_query(order_type, code, price, order_id $=$ None, adjust_limit=0, trd_env=TrdEnv.REAL, acc_id=0, acc_index $=0$ )  

介绍  

查询指定交易业务账户下的最大可买卖数量，亦可查询指定交易业务账户下指定订单的最大可改成的数量。  

现金账户请求期权不适用。  

参数返回  

<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>order_type</td><td>OrderType</td><td>订单类型</td></tr><tr><td>code</td><td>str</td><td>证券代码</td></tr><tr><td>price</td><td>float</td><td>报价</td></tr><tr><td>order_id</td><td>str</td><td>订单号</td></tr><tr><td>adjust_limit</td><td>float</td><td>价格微调幅度</td></tr><tr><td>trd_env</td><td>TrdEnv</td><td>交易环境</td></tr><tr><td>acc_id</td><td>int</td><td>交易业务账户ID</td></tr><tr><td>acc_index</td><td>int</td><td>交易业务账户列表中的账户序号</td></tr></table></body></html>  

<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>ret</td><td>RET CODE</td><td>接口调用结果</td></tr><tr><td rowspan="2">data</td><td>pd. DataFrame</td><td>当 ret RETOK时，返回账号列表</td></tr><tr><td>str</td><td>当 ret!= RET_OK 时，返回错误描述</td></tr></table></body></html>  

账号列表格式如下：  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>max_cash_buy</td><td>float</td><td>现金可买</td></tr><tr><td>max_cash_and_margin_buy</td><td>float</td><td>最大可买</td></tr><tr><td>max_position_sell</td><td>float</td><td>持仓可卖</td></tr><tr><td>max_sell_short</td><td>float</td><td>可卖空</td></tr><tr><td>max_buy_back</td><td>float</td><td>平仓需买入</td></tr><tr><td>long_required_im</td><td>float</td><td>买 1 张合约所带来 的初始保证金变 动</td></tr><tr><td>short_required_im</td><td>float</td><td>卖 1 张合约所带来 的初始保证金变 动</td></tr></table></body></html>  

Example  

from futu import \*   
trd_ctx $=$ OpenSecTradeContext(filter_trdmarket $=$ TrdMarket.HK,   
host $=$ '127.0.0.1', port $=$ 11111,   
security_firm $=$ SecurityFirm.FUTUSECURITIES)   
ret, data $=$   
trd_ctx.acctradinginfo_query(order_type $=$ OrderType.NORMAL,   
$c o d e=\prime\,{\mathsf{H K}}\,.\,\theta\theta7\theta\theta\,^{\prime}$ , price $\mathrel{=}496$ )   
if ret $==$ RET_OK: print(data) print(data['max_cash_and_margin_buy'][0])  # 最大融资可买数量   
else: print('acctradinginfo_query error: ', data)   
trd_ctx.close()  # 关闭当条连接  

# 接口限制  

每 30 秒内最多请求 10 次查询最大可买可卖接口  

# 提示  

现金业务账户不支持交易衍生品，因此不支持通过现金业务账户查询期权的最大可买可卖。  

# 查询持仓  

position_list_query(code='', position_market=TrdMarket.NONE, pl_ratio_min=None, pl_ratio_max=None, trd_env $\because$ TrdEnv.REAL, acc_id=0, acc_index=0, refresh_cache=False)  

介绍查询交易业务账户的持仓列表  

参数返回  

<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>code</td><td>str</td><td>代码过滤</td></tr><tr><td>position_market</td><td>TrdMarket</td><td>持仓所属市场过滤</td></tr></table></body></html>  

<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td></td><td></td><td></td></tr><tr><td>pl_ratio_min</td><td>float</td><td>当前盈亏比例下限过滤，仅返 回高于此比例的持仓</td></tr><tr><td>pl_ratio_max</td><td>float</td><td>当前盈亏比例上限过滤，低于 此比例的会返回</td></tr><tr><td>trd_env</td><td>TrdEnv</td><td>交易环境</td></tr><tr><td>acc_id</td><td>int</td><td>交易业务账户ID</td></tr><tr><td>acc_index</td><td>int</td><td>交易业务账户列表中的账户序 号</td></tr><tr><td>refresh_cache</td><td>bool</td><td>是否刷新缓存</td></tr></table></body></html>  

持仓列表  


<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>ret</td><td>RET CODE</td><td>接口调用结果</td></tr><tr><td rowspan="2">data</td><td>pd.DataFrame</td><td>当 ret RETOK时，返回持仓列表</td></tr><tr><td>str</td><td>当 ret!= RET OK 时，返回错误描述</td></tr></table></body></html>  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>position_side</td><td>PositionSide</td><td>持仓方向</td></tr><tr><td>code</td><td>str</td><td>股票代码</td></tr><tr><td>stock_name</td><td>str</td><td>股票名称</td></tr><tr><td>position_market</td><td>TrdMarket</td><td>持仓所属市场</td></tr><tr><td>qty</td><td>float</td><td>持有数量</td></tr><tr><td>can_sell_qty</td><td>float</td><td>可用数量</td></tr><tr><td>currency</td><td>Currency</td><td>交易货币</td></tr><tr><td>nominal_price</td><td>float</td><td>市价</td></tr><tr><td>cost_price</td><td>float</td><td>摊薄成本价（证券 账户），平均开仓 价 (期货账户)</td></tr><tr><td>cost_price_valid</td><td>bool</td><td>成本价是否有效</td></tr><tr><td>market_val</td><td>float</td><td>市值</td></tr><tr><td>pl_ratio</td><td>float</td><td>盈亏比例</td></tr><tr><td>pl_ratio_valid</td><td>bool</td><td>盈亏比例是否有 效</td></tr></table></body></html>  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>pl_val</td><td>float</td><td>盈亏金额</td></tr><tr><td>pl_val_valid</td><td>bool</td><td>盈亏金额是否有 效</td></tr><tr><td>today_pl_val</td><td>float</td><td>今日盈亏金额</td></tr><tr><td>today_trd_val</td><td>float</td><td>今日交易金额</td></tr><tr><td>today_buy_qty</td><td>float</td><td>今日买入总量</td></tr><tr><td>today_buy_val</td><td>float</td><td>今日买入总额</td></tr><tr><td>today_sell_qty</td><td>float</td><td>今日卖出总量</td></tr><tr><td>today_sell_val</td><td>float</td><td>今日卖出总额</td></tr><tr><td>unrealized_pl</td><td>float</td><td>未实现盈亏</td></tr><tr><td>realized_pl</td><td>float</td><td>已实现盈亏</td></tr></table></body></html>  

Example  

from futu import \*   
trd_ctx $=$ OpenSecTradeContext(filter_trdmarket $=$ TrdMarket.HK,   
host $=$ '127.0.0.1', port $=$ 11111,   
security_firm $=$ SecurityFirm.FUTUSECURITIES)   
ret, data $=$ trd_ctx.position_list_query()  

print(data)if data.shape[0] > 0:  # 如果持仓列表不为空print(data['stock_name'][0])  # 获取持仓第一个股票名称print(data['stock_name'].values.tolist())  # 转为 listelse:print('position_list_query error: ', data)  

trd_ctx.close()  # 关闭当条连接  

# 接口限制  

每 30 秒内最多请求 10 次查询持仓接口调用此接口，只有在刷新缓存时，才受到限频限制  

# 下单  

place_order(price, qty, code, trd_side,   
order_type=OrderType.NORMAL, adjust_limit $=0$ ,   
trd_env=TrdEnv.REAL, acc_id $=0$ , acc_index $=0$ , remark $\equiv$ None,   
time_in_force=TimeInForce.DAY, fill_outside_rth $|\!=$ False,   
aux_price=None, trail_type $=$ None, trail_value $=$ None,   
trail_spread=None)  

介绍下单提示  

Python API 是同步的，但网络收发是异步的。当 place_order 对应的应答数据包与 响应成交推送回调 或 响应订单推送回调 间隔很短时，就可能出现 place_order 的数据包先返回，但回调函数先被调用的情况。例如：可能先调用了 响应订单推送回调，然后 place_order 这个接口才返回。  

参数  


<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>price</td><td>float</td><td>订单价格</td></tr><tr><td>qty</td><td>float</td><td>订单数量</td></tr><tr><td>code</td><td>str</td><td>标的代码</td></tr><tr><td>trd_side</td><td>TrdSide</td><td>交易方向</td></tr><tr><td>order_type</td><td>OrderType</td><td>订单类型</td></tr><tr><td>adjust_limit</td><td>float</td><td>价格微调幅度</td></tr><tr><td>trd_env</td><td>TrdEnv</td><td>交易环境</td></tr><tr><td>acc_id</td><td>int</td><td>交易业务账户ID</td></tr><tr><td>acc_index</td><td>int</td><td>交易业务账户列表中的账户 序号</td></tr><tr><td>remark</td><td>str</td><td>备注</td></tr></table></body></html>  

<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>time_in_force</td><td>TimeInForce</td><td>有效期限</td></tr><tr><td>fill_outside_rth</td><td>bool</td><td>是否允许盘前盘后</td></tr><tr><td>aux_price</td><td>float</td><td>触发价格</td></tr><tr><td>trail_type</td><td>TrailType</td><td>跟踪类型</td></tr><tr><td>trail_value</td><td>float</td><td>跟踪金额/百分比</td></tr><tr><td>trail_spread</td><td>float</td><td>指定价差</td></tr></table></body></html>  

返回  

<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>ret</td><td>RET CODE</td><td>接口调用结果</td></tr><tr><td rowspan="2">data</td><td>pd. DataFrame</td><td>当 ret RETOK时，返回订单列表</td></tr><tr><td>str</td><td>当 ret！= RET_OK 时，返回错误描述</td></tr></table></body></html>  

订单列表格式如下：  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>trd side</td><td>TrdSide</td><td>交易方向</td></tr></table></body></html>  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>order_type</td><td>OrderType</td><td>订单类型</td></tr><tr><td>order_status</td><td>OrderStatus</td><td>订单状态</td></tr><tr><td>order_id</td><td>str</td><td>订单号</td></tr><tr><td>code</td><td>str</td><td>股票代码</td></tr><tr><td>stock_name</td><td>str</td><td>股票名称</td></tr><tr><td>qty</td><td>float</td><td>订单数量</td></tr><tr><td>price</td><td>float</td><td>订单价格</td></tr><tr><td>create_time</td><td>str</td><td>创建时间</td></tr><tr><td>updated_time</td><td>str</td><td>最后更新时间</td></tr><tr><td>dealt_qty</td><td>float</td><td>成交数量</td></tr><tr><td>dealt_avg_price</td><td>float</td><td>成交均价</td></tr><tr><td>last_err_msg</td><td>str</td><td>最后的错误描述</td></tr><tr><td>remark</td><td>str</td><td>下单时备注的标识</td></tr></table></body></html>  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>time_in_force</td><td>Time InForce</td><td>有效期限</td></tr><tr><td>fill_outside_rth</td><td>bool</td><td>是否允许盘前盘后 （用于港股盘前竞价 与美股盘前盘后)</td></tr><tr><td>aux_price</td><td>float</td><td>触发价格</td></tr><tr><td>trail_type</td><td>TrailType</td><td>跟踪类型</td></tr><tr><td>trail_value</td><td>float</td><td>跟踪金额/百分比</td></tr><tr><td>trail_spread</td><td>float</td><td>指定价差</td></tr></table></body></html>  

# Example  

from futu import \*   
pwd_unlock $=$ '123456'   
trd_ctx $=$ OpenSecTradeContext(filter_trdmarket $=$ TrdMarket.HK,   
host $=$ '127.0.0.1', port=11111,   
security_firm $=$ SecurityFirm.FUTUSECURITIES)   
ret, data $=$ trd_ctx.unlock_trade(pwd_unlock)  # 若使用真实账户下   
单，需先对账户进行解锁。此处示例为模拟账户下单，也可省略解锁。   
if ret $==$ RET_OK: ret, data = trd_ctx.place_order(price=510.0, qty=100,   
${\mathsf{c o d e}}{=}^{\"}{\mathsf{H K}}\,.\,{\mathsf{0}}{\mathsf{6}}{7}{\mathsf{6}}{\mathsf{0}}^{\"}$ , trd_side $=$ TrdSide.BUY,   
trd_env $:=$ TrdEnv.SIMULATE) if ret $==$ RET_OK: print(data) print(data['order_id'][0])  # 获取下单的订单号 print(data['order_id'].values.tolist())  # 转为 list else: print('place_order error: ', data)   
else: print('unlock_trade failed: ', data)   
trd_ctx.close()  

每 30 秒内最多请求 15 次下单接口，且连续两次请求的间隔不可小于0.02 秒。真实账户调用下单接口前，需要先进行 解锁；模拟账户无需解锁。  

# 提示  

各订单类型对应的必传参数：点击这里 了解更多  

对于 可做空标的，暂不支持锁仓功能，故无法同时持有相同产品的多头头寸和空头头寸。  
如果希望对 可做空标的 进行 平仓 操作，需要自行判断持仓头寸的方向，然后提交一笔反向的相同数量的订单完成平仓操作。  
如果希望对 可做空标的 进行 反手 操作，需要两步：1. 先判断持仓头寸的方向，并提交一笔反向的相同数量的订单完成平仓操作；2. 提交一笔反向的订单，完成反向订单的提交。  
举例：A 当前持有 1 手 HK.HSI2012 期货合约的多单，如果希望反手，必须先 卖出 1 手 HK.HSI2012 完成平仓，再卖出 1 手  
HK.HSI2012 完成空单的建立。  

# 改单撤单  

modify_order(modify_order_op, order_id, qty, price, adjust_limit=0, trd_env=TrdEnv.REAL, acc_id=0, acc_index $=0$ , aux_price=None, trail_type=None, trail_value $=$ None, trail_spread $=$ None)  

介绍  

修改订单的价格和数量、撤单、操作订单的失效和生效、删除订单等。如果是 OpenHKCCTradeContext，将不支持改单。可撤单。删除订单是OpenD 本地操作。  

参数  


<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>modify_order_op</td><td>ModifyOrderOp</td><td>改单操作类型</td></tr><tr><td>order_id</td><td>str</td><td>订单号</td></tr><tr><td>qty</td><td>float</td><td>订单改单后的数量</td></tr><tr><td>price</td><td>float</td><td>订单改单后的价格</td></tr><tr><td>adjust_limit</td><td>float</td><td>价格微调幅度</td></tr><tr><td>trd_env</td><td>TrdEnv</td><td>交易环境</td></tr><tr><td>acc_id</td><td>int</td><td>交易业务账户ID</td></tr><tr><td>acc_index</td><td>int</td><td>交易业务账户列表中的账 户序号</td></tr><tr><td>aux_price</td><td>float</td><td>触发价格</td></tr><tr><td>trail_type</td><td>TrailType</td><td>跟踪类型</td></tr></table></body></html>  

<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>trail_value</td><td>float</td><td>跟踪金额/百分比</td></tr><tr><td>trail spread</td><td>float</td><td>指定价差</td></tr></table></body></html>  

返回  

<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>ret</td><td>RET CODE</td><td>接口调用结果</td></tr><tr><td rowspan="2">data</td><td>pd.DataFrame</td><td>当 ret RETOK时，返回改单信息</td></tr><tr><td>str</td><td>当 ret!= RET_OK 时，返回错误描述</td></tr></table></body></html>  

改单信息格式如下：  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>trd env</td><td>TrdEnv</td><td>交易环境</td></tr><tr><td>order_id</td><td>str</td><td>订单号</td></tr></table></body></html>  

# Example  

from futu import \*   
pwd_unlock $=$ '123456'   
trd_ctx $=$ OpenSecTradeContext(filter_trdmarket=TrdMarket.HK, host $=$ '127.0.0.1', port $=$ 11111,   
security_firm $=$ SecurityFirm.FUTUSECURITIES)   
ret, data $=$ trd_ctx.unlock_trade(pwd_unlock)  # 若使用真实账户改 单/撤单，需先对账户进行解锁。此处示例为模拟账户撤单，也可省略解锁。 if ret $==$ RET_OK:   
order_id $=$ "8851102695472794941"   
ret, data $=$ trd_ctx.modify_order(ModifyOrderOp.CANCEL, order_id, 0, 0)  

if ret $==$ RET_OK: print(data) print(data['order_id'][0])  # 获取改单的订单号 print(data['order_id'].values.tolist())  # 转为 list else:  

print('unlock_trade failed: ', data) trd_ctx.close()  

cancel_all_order(trd_env=TrdEnv.REAL, acc_id=0, acc_index $=0$ , trdmarket=TrdMarket.NONE)  

介绍  

撤消全部订单。模拟交易以及 A 股通账户暂不支持全部撤单。  

参数返回  

<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>trd_env</td><td>TrdEnv</td><td>交易环境</td></tr><tr><td>acc_id</td><td>int</td><td>交易业务账户ID</td></tr><tr><td>acc_index</td><td>int</td><td>交易业务账户列表中的账户序号</td></tr><tr><td>trdmarket</td><td>TrdMarket</td><td>指定交易市场</td></tr></table></body></html>  

![](FutuAPI/ded3c96ad051f3c02c9eb72b0eb07dbd9badc1f80643e583718a5ac0d2705e33.jpg)  

<html><body><table><tr><td>ret</td><td>str</td><td>接口调用结果。ret RET OK 二二 代表接口调用正 常，ret ！= RETOK 代表接口调用失败</td></tr><tr><td rowspan="2">data</td><td rowspan="2">str</td><td>当 ret 二二 RETOK，返回" success</td></tr><tr><td>当 ret !=RETOK，返回错误描述</td></tr></table></body></html>  

全部撤单信息格式如下：  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>trd env</td><td>TrdEnv</td><td>交易环境</td></tr><tr><td>order_id</td><td>str</td><td>订单号</td></tr></table></body></html>  

# Example  

from futu import \*  
pwd_unlock $=$ '123456'  
trd_ctx $=$ OpenSecTradeContext(filter_trdmarket=TrdMarket.HK,host $=$ '127.0.0.1', port $=$ 11111,  
security_firm $=$ SecurityFirm.FUTUSECURITIES)  
ret, data $=$ trd_ctx.unlock_trade(pwd_unlock)  # 若使用真实账户改单/撤单，需先对账户进行解锁。此处示例为模拟账户全部撤单，也可省略解锁。  

if ret $==$ RET_OK: ret, data $=$ trd_ctx.cancel_all_order() if ret $==$ RET_OK: print(data) else: print('cancel_all_order error: ', data)  

else: print('unlock_trade failed: ', data)   
trd_ctx.close()  

接口限制  

•  每 30 秒内最多请求 20 次改单撤单接口，且连续两次请求的间隔不可小于 0.04 秒。  

真实账户调用改单撤单接口前，需要先进行 解锁；模拟账户无需解锁。  

提示  

若执行 修改订单 操作，各类订单类型对应的必传参数，可 点击这里 了解更多。  

如果希望执行 改单操作 去 修改订单数量，此接口入参的订单数(N-n) 股，如果您希望撤掉其中的 x 股，modify_order_op 应选择NORMAL，qty 应传 (N-  

![](FutuAPI/f4dcce2ae4718699d200861efd6ae6dfed7303f1358b0a15196a2718ca06ef2d.jpg)  

如果希望执行 撤单操作，此接口入参的 modify_order_op 应该选择CANCEL。  

举例： 一笔订单数量是 N 股，已部分成交 n 股。如果希望将未成交的 (N-n) 股全部撤掉，modify_order_op 应选择 CANCEL，此时 qty和 price 的入参会被忽略。  

# 查询未完成订单  

order_list_query(order_id="", order_market=TrdMarket.NONE, status_filter_list=[], code='', start='', end='',  

# trd_env=TrdEnv.REAL, acc_id=0, acc_index $=0$ , refresh_cache=False)  

介绍  

查询指定交易业务账户的未完成订单列表  

参数  

<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>order_id</td><td>str</td><td>订单号过滤</td></tr><tr><td>order_market</td><td>TrdMarket</td><td>订单标的所属市场过滤</td></tr><tr><td>status_filter_list</td><td>list</td><td>订单状态过滤</td></tr><tr><td>code</td><td>str</td><td>代码过滤</td></tr><tr><td>start</td><td>str</td><td>开始时间</td></tr><tr><td>end</td><td>str</td><td>结束时间</td></tr><tr><td>trd_env</td><td>TrdEny</td><td>交易环境</td></tr><tr><td>acc_id</td><td>int</td><td>交易业务账户ID</td></tr><tr><td>acc_index</td><td>int</td><td>交易业务账户列表中的账户 序号</td></tr></table></body></html>  

![](FutuAPI/d20b2bb482d7c9cd3726ffed28050d77fc86292372af6f043e9d7f2a865c2f1e.jpg)  

返回  

<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>ret</td><td>RET CODE</td><td>接口调用结果</td></tr><tr><td rowspan="2">data</td><td>pd. DataFrame</td><td>当 ret RETOK时，返回订单列表</td></tr><tr><td>str</td><td>当 ret!= RET_OK 时，返回错误描述</td></tr></table></body></html>  

订单列表格式如下：  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>trd_side</td><td>TrdSide</td><td>交易方向</td></tr><tr><td>order_type</td><td>OrderType</td><td>订单类型</td></tr><tr><td>order_status</td><td>OrderStatus</td><td>订单状态</td></tr><tr><td>order_id</td><td>str</td><td>订单号</td></tr><tr><td>code</td><td>str</td><td>股票代码</td></tr><tr><td>stock_name</td><td>str</td><td>股票名称</td></tr><tr><td>order_market</td><td>TrdMarket</td><td>订单标的所属市场</td></tr><tr><td>qty</td><td>float</td><td>订单数量</td></tr><tr><td>price</td><td>float</td><td>订单价格</td></tr></table></body></html>  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td></td><td></td><td></td></tr><tr><td>currency</td><td>Currency</td><td>交易货币</td></tr><tr><td>create_time</td><td>str</td><td>创建时间</td></tr><tr><td>updated_time</td><td>str</td><td>最后更新时间</td></tr><tr><td>dealt_qty</td><td>float</td><td>成交数量</td></tr><tr><td>dealt_avg_price</td><td>float</td><td>成交均价</td></tr><tr><td>last_err_msg</td><td>str</td><td>最后的错误描述</td></tr><tr><td>remark</td><td>str</td><td>下单时备注的标识</td></tr><tr><td>time_in_force</td><td>TimeInForce</td><td>有效期限</td></tr><tr><td>fill_outside_rth</td><td>bool</td><td>是否允许盘前盘后 （用于港股盘前竞价 与美股盘前盘后)</td></tr><tr><td>aux_price</td><td>float</td><td>触发价格</td></tr><tr><td>trail_type</td><td>TrailType</td><td>跟踪类型</td></tr><tr><td>trail_value</td><td>float</td><td>跟踪金额/百分比</td></tr></table></body></html>  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>trail spread</td><td>float</td><td>指定价差</td></tr></table></body></html>  

# Example  

from futu import \*  
trd_ctx $=$ OpenSecTradeContext(filter_trdmarket $=$ TrdMarket.HK,  
host $=$ '127.0.0.1', port $=$ 11111,  
security_firm $=$ SecurityFirm.FUTUSECURITIES)  
ret, data $=$ trd_ctx.order_list_query()  
if ret $==$ RET_OK:print(data)if data.shape[0] > 0:  # 如果订单列表不为空print(data['order_id'][0])  # 获取未完成订单的第一个订单号print(data['order_id'].values.tolist())  # 转为 list  
else:print('order_list_query error: ', data)  
trd_ctx.close()  

# 接口限制  

每 30 秒内最多请求 10 次查询未完成订单接口  

调用此接口，只有在刷新缓存时，才受到限频限制  

# 提示  

未完成订单，按照时间的“顺序”进行排列，即：先提交的订单在前，后提交的订单在后  

# 查询历史订单  

history_order_list_query(status_filter_list=[], code='', order_market=TrdMarket.NONE, start='', end=' trd_env=TrdEnv.REAL, acc_id=0, acc_index $=0$ )  

介绍  

查询指定交易业务账户的历史订单列表  

参数  

<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>status_filter_list</td><td>list</td><td>订单状态过滤</td></tr><tr><td>code</td><td>str</td><td>代码过滤</td></tr><tr><td>order_market</td><td>TrdMarket</td><td>订单标的所属市场过滤</td></tr><tr><td>start</td><td>str</td><td>开始时间</td></tr><tr><td>end</td><td>str</td><td>结束时间</td></tr><tr><td>trd_env</td><td>TrdEnv</td><td>交易环境</td></tr><tr><td>acc_id</td><td>int</td><td>交易业务账户ID</td></tr><tr><td>acc_index</td><td>int</td><td>交易业务账户列表中的账户 序号</td></tr></table></body></html>  

start 和 end 的组合如下  

<html><body><table><tr><td>Start 类 型</td><td>End 类 型</td><td>说明</td></tr><tr><td>str</td><td>str</td><td>start 和end 分别为指定的日 期</td></tr><tr><td>None</td><td>str</td><td>start 为 end 往前 90 天</td></tr><tr><td>str</td><td>None</td><td>end为 start 往后 90 天</td></tr><tr><td>None</td><td>None</td><td>start 为往前 90 天，end 当前 日期</td></tr></table></body></html>  

返回  


<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>ret</td><td>RET CODE</td><td>接口调用结果</td></tr><tr><td rowspan="2">data</td><td>pd. DataFrame</td><td>当 ret RETOK时，返回订单列表</td></tr><tr><td>str</td><td>当 ret!= RET_OK 时，返回错误描述</td></tr></table></body></html>  

订单列表格式如下：  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>trd_side</td><td>TrdSide</td><td>交易方向</td></tr><tr><td>order_type</td><td>OrderType</td><td>订单类型</td></tr><tr><td>order_status</td><td>OrderStatus</td><td>订单状态</td></tr><tr><td>order_id</td><td>str</td><td>订单号</td></tr><tr><td>code</td><td>str</td><td>股票代码</td></tr><tr><td>stock_name</td><td>str</td><td>股票名称</td></tr><tr><td>order_market</td><td>TrdMarket</td><td>订单标的所属市场</td></tr><tr><td>qty</td><td>float</td><td>订单数量</td></tr></table></body></html>  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td></td><td></td><td></td></tr><tr><td>price</td><td>float</td><td>订单价格</td></tr><tr><td>currency</td><td>Currency</td><td>交易货币</td></tr><tr><td>create_time</td><td>str</td><td>创建时间</td></tr><tr><td>updated_time</td><td>str</td><td>最后更新时间</td></tr><tr><td>dealt_qty</td><td>float</td><td>成交数量</td></tr><tr><td>dealt_avg_price</td><td>float</td><td>成交均价</td></tr><tr><td>last_err_msg</td><td>str</td><td>最后的错误描述</td></tr><tr><td>remark</td><td>str</td><td>下单时备注的标识</td></tr><tr><td>time_in_force</td><td>TimeInForce</td><td>有效期限</td></tr><tr><td>fill_outside_rth</td><td>bool</td><td>是否允许盘前盘后 （用于港股盘前竞价 与美股盘前盘后)</td></tr><tr><td>aux_price</td><td>float</td><td>触发价格</td></tr></table></body></html>  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>trail_type</td><td>TrailType</td><td>跟踪类型</td></tr><tr><td>trail value</td><td>float</td><td>跟踪金额/百分比</td></tr><tr><td>trail s spread</td><td>float</td><td>指定价差</td></tr></table></body></html>  

# Example  

from futu import \*  
trd_ctx $=$ OpenSecTradeContext(filter_trdmarket $=$ TrdMarket.HK,  
host $=$ '127.0.0.1', port $=$ 11111,  
security_firm $=$ SecurityFirm.FUTUSECURITIES)  
ret, data $=$ trd_ctx.history_order_list_query()  
if ret $==$ RET_OK:print(data)if data.shape[0] > 0:  # 如果订单列表不为空print(data['order_id'][0])  # 获取持仓第一个订单号print(data['order_id'].values.tolist())  # 转为 list  
else:print('history_order_list_query error: ', data)  
trd_ctx.close()  

接口限制  

每 30 秒内最多请求 10 次查询历史订单接口  

提示  

历史订单，按照时间的“倒序”进行排列，即：后提交的订单在前，先提交的订单在后  

# 响应订单推送回调  

on_recv_rsp(self, rsp_pb)  

# 介绍  

响应订单推送，异步处理 OpenD 推送过来的订单状态信息。  

在收到 OpenD 推送过来的订单状态信息后会回调到该函数，您需要在派生类中覆盖 on_recv_rsp。  

# 参数  

<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>rsp_pb</td><td>Trd_UpdateOrder_pb2. Response</td><td>派生类中不需要直 接处理该参数</td></tr></table></body></html>  

返回  


<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>ret</td><td>RET CODE</td><td>接口调用结果</td></tr><tr><td rowspan="2">data</td><td>pd. DataFrame</td><td>当 ret RETOK时，返回订单列表</td></tr><tr><td>str</td><td>当 ret!= RET OK 时，返回错误描述</td></tr></table></body></html>  

订单列表格式如下：  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>trd_side</td><td>TrdSide</td><td>交易方向</td></tr><tr><td>order_type</td><td>OrderType</td><td>订单类型</td></tr><tr><td>order_status</td><td>OrderStatus</td><td>订单状态</td></tr><tr><td>order_id</td><td>str</td><td>订单号</td></tr><tr><td>code</td><td>str</td><td>股票代码</td></tr><tr><td>stock_name</td><td>str</td><td>股票名称</td></tr></table></body></html>  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>qty</td><td>float</td><td>订单数量</td></tr><tr><td>price</td><td>float</td><td>订单价格</td></tr><tr><td>currency</td><td>Currency</td><td>交易货币</td></tr><tr><td>create_time</td><td>str</td><td>创建时间</td></tr><tr><td>updated_time</td><td>str</td><td>最后更新时间</td></tr><tr><td>dealt_qty</td><td>float</td><td>成交数量</td></tr><tr><td>dealt_avg_price</td><td>float</td><td>成交均价</td></tr><tr><td>last_err_msg</td><td>str</td><td>最后的错误描述</td></tr><tr><td>remark</td><td>str</td><td>下单时备注的标识</td></tr><tr><td>time_in_force</td><td>Time InForce</td><td>有效期限 是否允许盘前盘后</td></tr><tr><td>fill_outside_rth</td><td>bool</td><td>(仅用于美股)</td></tr><tr><td>aux_price</td><td>float</td><td>触发价格</td></tr></table></body></html>  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>trail 1 type</td><td>TrailType</td><td>跟踪类型</td></tr><tr><td>trail_value</td><td>float</td><td>跟踪金额/百分比</td></tr><tr><td>trail s spread</td><td>float</td><td>指定价差</td></tr></table></body></html>  

# Example  

from futu import \*   
from time import sleep   
class TradeOrderTest(TradeOrderHandlerBase): """ order update push""" def on_recv_rsp(self, rsp_pb): ret, content $=$ super(TradeOrderTest,   
self).on_recv_rsp(rsp_pb) if ret $==$ RET_OK: print("\* TradeOrderTest   
content $=\{\}\setminus\ensuremath{\boldsymbol{\mathsf{n}}}^{\prime\prime}$ .format(content)) return ret, content   
trd_ctx $=$ OpenSecTradeContext(filter_trdmarket $=$ TrdMarket.HK,   
host $=$ '127.0.0.1', port $=$ 11111,   
security_firm $=$ SecurityFirm.FUTUSECURITIES)   
trd_ctx.set_handler(TradeOrderTest())   
print(trd_ctx.place_order(price $=$ 518.0, $9t y=160$ ,   
code $=$ "HK.00700", trd_side $=$ TrdSide.SELL))  

sleep(15) trd_ctx.close()  

# 查询订单费用  

order_fee_query(order_id_list=[], acc_id=0, acc_index $=0$ , trd_env=TrdEnv.REAL)  

介绍  

查询指定订单的收费明细（最低版本要求：8.2.4218）  

# 参数  

<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>order_id_list</td><td>list</td><td>订单号列表</td></tr><tr><td>trd_env</td><td>TrdEnv</td><td>交易环境</td></tr><tr><td>acc_id</td><td>int</td><td>交易业务账户ID</td></tr><tr><td>acc_index</td><td>int</td><td>交易业务账户列表中的账户序号</td></tr></table></body></html>  

返回  

<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>ret</td><td>RET CODE</td><td>接口调用结果</td></tr><tr><td rowspan="2">data</td><td>pd. DataFrame</td><td>当表 ret: 二二 ：RETOK时，返回订单费用列</td></tr><tr><td>str</td><td>当 ret!= RET_OK 时，返回错误描述</td></tr></table></body></html>  

订单列表格式如下：  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>order_id</td><td>str</td><td>订单号</td></tr><tr><td>fee_amount</td><td>float</td><td>总费用</td></tr><tr><td>fee_details</td><td>list</td><td>收费明细</td></tr></table></body></html>  

![](FutuAPI/0ca4e557bf99157a5dc661da7e678665bcc5bb0369fd63a8c0ef8f9d90fbc44c.jpg)  

Example  

from futu import \*   
trd_ctx $=$ OpenSecTradeContext(filter_trdmarket $=$ TrdMarket.US,   
host $=$ '127.0.0.1', port $=$ 11111,   
security_firm $=$ SecurityFirm.FUTUSECURITIES)   
ret1, data1 $=$   
trd_ctx.history_order_list_query(status_filter_list $=$ [OrderStat   
us.FILLED_ALL])   
if ret1 $==$ RET_OK: if data1.shape[0] > 0:  # 如果订单列表不为空 ret2, data2 $=$   
trd_ctx.order_fee_query(data1['order_id'].values.tolist())  #   
将订单 id 转为 list，查询订单费用 if ret2 $==$ RET_OK: print(data2) print(data2['fee_details'][0])  # 打印第一笔订单的收费   
明细 else: print('order_fee_query error: ', data2)   
else: print('order_list_query error: ', data1)   
trd_ctx.close()  

接口限制  

每 30 秒内最多请求 10 次查询订单费用接口。  

仅支持查询 2018-01-01 之后的订单。  

# 订阅交易推送  

Python 不需要订阅交易推送  

# 查询当日成交  

deal_list_query(code="", deal_market= TrdMarket.NONE, trd_env=TrdEnv.REAL, acc_id=0, acc_index $=0$ , refresh_cache=False)  

介绍  

查询指定交易业务账户的当日成交列表。  
该接口只支持实盘交易，不支持模拟交易。  

参数  

<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>code</td><td>str</td><td>代码过滤</td></tr><tr><td>deal_market</td><td>TrdMarket</td><td>成交标的所属市场过滤</td></tr><tr><td>trd_env</td><td>TrdEnv</td><td>交易环境</td></tr><tr><td>acc_id</td><td>int</td><td>交易业务账户ID</td></tr></table></body></html>  

<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>acc_index</td><td>int</td><td>交易业务账户列表中的账户序 号</td></tr><tr><td>refresh cache</td><td>bool</td><td>是否刷新缓存</td></tr></table></body></html>  

返回  

<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>ret</td><td>RET CODE</td><td>接口调用结果</td></tr><tr><td rowspan="2">data</td><td>pd.DataFrame</td><td>当表 ret 二二 ：RETOK时，返回交易成交列</td></tr><tr><td>str</td><td>当 ret！= RET OK 时，返回错误描述</td></tr></table></body></html>  

交易成交列表格式如下：  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>trd_side</td><td>TrdSide</td><td>交易方向</td></tr><tr><td>deal_id</td><td>str</td><td>成交号</td></tr><tr><td>order_id</td><td>str</td><td>订单号</td></tr><tr><td>code</td><td>str</td><td>股票代码</td></tr><tr><td>stock_name</td><td>str</td><td>股票名称</td></tr><tr><td>deal_market</td><td>TrdMarket</td><td>成交标的所属市场</td></tr><tr><td>qty</td><td>float</td><td>成交数量</td></tr></table></body></html>  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>price</td><td>float</td><td>成交价格</td></tr><tr><td>create_time</td><td>str</td><td>创建时间</td></tr><tr><td>counter_broker_id</td><td>int</td><td>对手经纪号</td></tr><tr><td>counter_broker_name</td><td>str</td><td>对手经纪名称</td></tr><tr><td>status</td><td>DealStatus</td><td>成交状态</td></tr></table></body></html>  

# Example  

from futu import \*  
trd_ctx $=$ OpenSecTradeContext(filter_trdmarket $=$ TrdMarket.HK,  
host $=$ '127.0.0.1', port $=$ 11111,  
security_firm $=$ SecurityFirm.FUTUSECURITIES)  
ret, data $=$ trd_ctx.deal_list_query()  
if ret $==$ RET_OK:print(data)if data.shape[0] > 0:  # 如果成交列表不为空print(data['order_id'][0])  # 获取当日成交的第一个订单号print(data['order_id'].values.tolist())  # 转为 list  
else:print('deal_list_query error: ', data)  
trd_ctx.close()  

# 接口限制  

每 30 秒内最多请求 10 次查询当日成交接口  

调用此接口，只有在刷新缓存时，才受到限频限制  

# 提示  

当日成交，按照时间的“顺序”进行排列，即：先成交的记录在前，后成交的记录在后  

# 查询历史成交  

history_deal_list_query(code='', deal_market $=$ TrdMarket.NONE, start='', end='', trd_env=TrdEnv.REAL, acc_id=0, acc_index $=0$ )  

# 介绍  

查询指定交易业务账户的历史成交列表。  
该接口只支持实盘交易，不支持模拟交易。  

参数  

<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>code</td><td>str</td><td>代码过滤</td></tr><tr><td>deal_market</td><td>TrdMarket</td><td>成交标的所属市场过滤</td></tr><tr><td>start</td><td>str</td><td>开始时间</td></tr><tr><td>end</td><td>str</td><td>结束时间</td></tr><tr><td>trd_env</td><td>TrdEnv</td><td>交易环境</td></tr></table></body></html>  

<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>acc_id</td><td>int</td><td>交易业务账户ID</td></tr><tr><td>acc_index</td><td>int</td><td>交易业务账户列表中的账户序号</td></tr></table></body></html>  

o start 和 end 的组合如下  

<html><body><table><tr><td>Start 类 型</td><td>End 类 型</td><td>说明</td></tr><tr><td>str</td><td>str</td><td>start 和end 分别为指定的日 期</td></tr><tr><td>None</td><td>str</td><td>start 为 end 往前 90 天</td></tr><tr><td>str</td><td>None</td><td>end 为 start 往后 90 天</td></tr><tr><td>None</td><td>None</td><td>start 为往前 90 天，end 当前 日期</td></tr></table></body></html>  

返回  


<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>ret</td><td>RET CODE</td><td>接口调用结果</td></tr><tr><td rowspan="2">data</td><td>pd. DataFrame</td><td>当 ret == RET_OK 时，返回交易成交列 表</td></tr><tr><td>str</td><td>当 ret!= RET OK时，返回错误描述</td></tr></table></body></html>  

交易成交列表格式如下：  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>trd_side</td><td>TrdSide</td><td>交易方向</td></tr><tr><td>deal_id</td><td>str</td><td>成交号</td></tr><tr><td>order_id</td><td>str</td><td>订单号</td></tr><tr><td>code</td><td>str</td><td>股票代码</td></tr><tr><td>stock_name</td><td>str</td><td>股票名称</td></tr><tr><td>deal_market</td><td>TrdMarket</td><td>成交标的所属市场</td></tr><tr><td>qty</td><td>float</td><td>成交数量</td></tr><tr><td>price</td><td>float</td><td>成交价格</td></tr><tr><td>create_time</td><td>str</td><td>创建时间</td></tr><tr><td>counter_broker_id</td><td>int</td><td>对手经纪号</td></tr><tr><td>counter_broker_name</td><td>str</td><td>对手经纪名称</td></tr><tr><td>status</td><td>DealStatus</td><td>成交状态</td></tr></table></body></html>  

# Example  

from futu import \*   
trd_ctx $=$ OpenSecTradeContext(filter_trdmarket $=$ TrdMarket.HK,   
host $=$ '127.0.0.1', port $=$ 11111,   
security_firm $=$ SecurityFirm.FUTUSECURITIES)   
ret, data $=$ trd_ctx.history_deal_list_query()   
if ret $==$ RET_OK: print(data) if data.shape[0] > 0:  # 如果成交列表不为空 print(data['deal_id'][0])  # 获取历史成交的第一个成交号 print(data['deal_id'].values.tolist())  # 转为 list   
else: print('history_deal_list_query error: ', data)   
trd_ctx.close()  

# 接口限制  

每 30 秒内最多请求 10 次查询历史成交接口  

# 提示  

历史成交，按照时间的“倒序”进行排列，即：后成交的记录在前，先成交的记录在后  

# 响应成交推送回调  

# on_recv_rsp(self, rsp_pb)  

介绍  

响应成交推送，异步处理 OpenD 推送过来的成交状态信息。  

在收到 OpenD 推送过来的成交状态信息后会回调到该函数，您需要在派生类中覆盖 on_recv_rsp。  
该接口只支持实盘交易，不支持模拟交易。  

参数  

<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>rsp_pb</td><td>Trd_UpdateOrderFill_pb2.Response</td><td>派生类中不需 要直接处理该 参数</td></tr></table></body></html>  

返回  


<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>ret</td><td>RET CODE</td><td>接口调用结果</td></tr><tr><td rowspan="2">data</td><td>pd. DataFrame</td><td>当 ret 二二 ：RETOK时，返回交易成交列 表</td></tr><tr><td>str</td><td>当 ret!= RET OK 时，返回错误描述</td></tr></table></body></html>  

交易成交列表格式如下：  

<html><body><table><tr><td>字段</td><td>类型</td><td>说明</td></tr><tr><td>trd_side</td><td>TrdSide</td><td>交易方向</td></tr><tr><td>deal_id</td><td>str</td><td>成交号</td></tr><tr><td>order_id</td><td>str</td><td>订单号</td></tr><tr><td>code</td><td>str</td><td>股票代码</td></tr><tr><td>stock_name</td><td>str</td><td>股票名称</td></tr><tr><td>qty</td><td>float</td><td>成交数量</td></tr><tr><td>price</td><td>float</td><td>成交价格</td></tr><tr><td>create_time</td><td>str</td><td>创建时间</td></tr><tr><td>counter_broker_id</td><td>int</td><td>对手经纪号</td></tr></table></body></html>  

![](FutuAPI/98394af2a8b17bad2b15d00a5216902fe69d26c53176b336d74c2ff321a9b1b9.jpg)  

# Example  

from futu import \*   
from time import sleep   
class TradeDealTest(TradeDealHandlerBase): """ order update push""" def on_recv_rsp(self, rsp_pb): ret, content $=$ super(TradeDealTest,   
self).on_recv_rsp(rsp_pb) if ret $==$ RET_OK: print("TradeDealTest content={}".format(content)) return ret, content   
trd_ctx $=$ OpenSecTradeContext(filter_trdmarket $=$ TrdMarket.HK,   
host $=$ '127.0.0.1', port $=$ 11111,   
security_firm $=$ SecurityFirm.FUTUSECURITIES)   
trd_ctx.set_handler(TradeDealTest())   
print(trd_ctx.place_order(price $^{1=}$ 595.0, qty $=\mathtt{1}6\theta$ ,   
code $^{1=}$ "HK.00700", trd_side $=$ TrdSide.BUY))  

sleep(15) trd_ctx.close()  

# 交易定义  

# #账户风控状态  

CltRiskLevel  

NONE未知  

SAFE安全  

WARNING 预警  

# DANGER  

危险  

# ABSOLUTE_SAFE  

绝对安全  

# OPT_DANGER  

危险  

![](FutuAPI/0e792b0f3f3f722381b5084601810c9721f209d768f25b8ac6c70362b7012150.jpg)  

# 提示  

查询期货账户的风险状态，建议使用 risk_status 字段， 返回结果详见 CltRiskStatus  

# #货币类型  

# Currency  

# NONE  

未知货币  

HKD  

港元  

USD美元  

CNH离岸人民币  

JPY日元  

SGD新元  

AUD澳元  

CAD加拿大元  

MYR马来西亚林吉特  

# #跟踪类型  

# TrailType  

NONE未知  

RATIO比例  

# AMOUNT  

金额  

# #修改订单操作  

# ModifyOrderOp  

NONE未知操作  

NORMAL 修改订单  

CANCEL 撤单  

使失效  

# ENABLE  

使生效  

![](FutuAPI/89b12c1bc8c7916a0e6c21a3bed5b527e31fc8d7af54389e1703654540e24584.jpg)  

删除  

![](FutuAPI/eecd4ad89f2555e64894ff85250129b066296cf267f5c9ac819699f475006b14.jpg)  

# #成交状态  

# DealStatus  

OK正常  

CANCELLED 成交被取消  

CHANGED 成交被更改  

# #订单状态  

# OrderStatus  

NONE 未知状态  

提交中  

SUBMITTED 已提交，等待成交  

![](FutuAPI/0a1ca27a243fb864f195ee5b0332554d95f8f6cf328c526946d173a13a28774d.jpg)  

部分成交  

![](FutuAPI/847743260811c06265001e1a8dc5cfbab5bda348cde0bfb0676e7635ea8848cb.jpg)  

FILLED_ALL  

全部已成交  

CANCELLED_PART部分成交，剩余部分已撤单  

CANCELLED_ALL 全部已撤单，无成交  

FAILED下单失败，服务拒绝  

# DISABLED  

已失效  

![](FutuAPI/c926cd55c8c88cd240fbca0d8af83b6fab975fd8ab138212be1237995dc7984a.jpg)  

# DELETED  

已删除，无成交的订单才能删除  

![](FutuAPI/5c6df760c98659c017b0b3fd0b6bc538afb5ce2a8b68bca83f1bd92b9bb75697.jpg)  

# #订单类型  

# 提示  

实盘交易中，各个品类支持的订单类型  

模拟交易中，仅支持限价单(NORMAL)和市价单(MARKET)。  

# OrderType  

NONE未知类型  

NORMAL 限价单  

MARKET 市价单  

# ABSOLUTE_LIMIT  

绝对限价订单  

![](FutuAPI/a2ca44c8c44e3af9c860f19d6d250a67910140903023ff34507edcbcfab38ef7.jpg)  

# AUCTION  

竞价市价单  

![](FutuAPI/775d8dcd6143e7b861d9d8ce22302c3532be90008ee3bae807a7e0893768dd85.jpg)  

# AUCTION_LIMIT  

竞价限价单  

![](FutuAPI/c97525462cf9a1fac670254c864384f2d04cd710073f6f804349eb6a22a1f001.jpg)  

SPECIAL_LIMIT  

特别限价单  

![](FutuAPI/2457ed4062e475effd56d44bf5894c829bd596642c7c24866802a2a263eb9f85.jpg)  

SPECIAL_LIMIT_ALL特别限价且要求全部成交订单  

![](FutuAPI/43949d74b982838662039c344fd536434d58bcc1010e53449fcc1315946318a2.jpg)  

STOP 止损市价单  

STOP_LIMIT 止损限价单  

MARKET_IF_TOUCHED触及市价单（止盈）  

LIMIT_IF_TOUCHED触及限价单（止盈）  

TRAILING_STOP 跟踪止损市价单  

# TRAILING_STOP_LIMIT  

跟踪止损限价单  

# TWAP_LIMIT  

时间加权限价算法单（港股和美股）  

i  

# TWAP  

时间加权市价算法单（仅美股）  

![](FutuAPI/e61c2c59933307aecad492bd0c253ed930f996a11d830205e0b514cea57937eb.jpg)  

VWAP_LIMIT  

成交量加权限价算法单（港股和美股）  

![](FutuAPI/d8bf6129091663ed79873085e7fedb7fd19197a8958f3ce6e56f12202964f2c1.jpg)  

VWAP  

成交量加权市价算法单（仅美股）  

![](FutuAPI/08b293d4ae9700e3113c462722deebf3a69c0f0265f6bff792d1327bdec06815.jpg)  

# #持仓方向  

PositionSide  

未知方向  

多仓  

![](FutuAPI/417c85a0873a45ceb5d16f1adfdb347579a6dde9355842649dbb0bc30f1fca56.jpg)  

SHORT  

空仓  

# #账户类型  

# TrdAccType  

NONE未知类型  

CASH 现金账户  

MARGIN 保证金账户  

# #交易环境  

TrdEnv  

SIMULATE模拟环境  

REAL真实环境  

# #交易市场  

TrdMarket  

NONE未知市场  

HK香港市场  

US美国市场  

CN  

A 股市场  

![](FutuAPI/afc4ec3fa71905837ff9a9940d00d2feb5beb0bc1bcf590ef60a30b46cb24617.jpg)  

HKCC  

香港 A 股通市场  

![](FutuAPI/d174f3ff0e13d3ec86b1b90658fc87a332bdf540bd1741d48b97c84f859f6a61.jpg)  

FUTURES  

期货市场  

FUTURES_SIMULATE_US  

美国期货模拟市场  

![](FutuAPI/5f35eb481001903ecae0e3614389ca0d43ddc2e83d37b8eeb8dedf10e971dd75.jpg)  

FUTURES_SIMULATE_HK  

香港期货模拟市场  

![](FutuAPI/4534828471be36c0fcc4cd698b68a9022928e34cbdb194325c089e0a21d9893b.jpg)  

FUTURES_SIMULATE_SG  

新加坡期货模拟市场  

![](FutuAPI/386a7d0e9c058bac083b2e18bb232fafd73adf9fc884083519093f8afb918ea9.jpg)  

FUTURES_SIMULATE_JP  

日本期货模拟市场  

![](FutuAPI/620075eff8f4ad24d7f3a01654da881bb15649309f8016650db133b8ed97e8fd.jpg)  

HKFUND  

香港基金市场  

![](FutuAPI/3184e8771acf4a48c33678c4592bcea8d624942c5e076091649040e0af0da3a0.jpg)  

USFUND  

美国基金市场  

![](FutuAPI/146ee53b7bf4af1356831a576a2c82d7dfc3a509444000eda9883d9491b55d4e.jpg)  

SG  

新加坡市场  

![](FutuAPI/6e15f401c7d2bb8e450ecdcc0e4ec67cdf4c68d165473f8fa1d83bbcc701b881.jpg)  

JP  

日本市场  

![](FutuAPI/a03b3d9fcb4dff116885103eea2a712547ca0a03b79b3c48bcb22621f4ad33d7.jpg)  

AU  

澳大利亚市场  

![](FutuAPI/cec69cd0d928581d22cb2ba5a8dd71c2b0af531cd468c9691bbd8bfff4f9e9f9.jpg)  

MY马来西亚市场  

CA加拿大市场  

![](FutuAPI/381511c47900526d9daad29aadd574c74326300df0c17b0de658b6339cd7f216.jpg)  

# #账户状态  

AccStatus  

ACTIVE 生效账户  

DISABLED 失效账户  

# #交易证券市场  

# #交易方向  

TrdSide  

NONE未知方向  

BUY买入  

SELL  

卖出  

![](FutuAPI/412066235071fd7c4538cddd528b6d52498680963f5bc4bf329821177510cab9.jpg)  

提示  

下单 接口的交易方向 ，建议仅使用 买入 和 卖出 两个方向作为入参。  

卖空 和 买回 仅用于 查询今日订单 ，查询历史订单 ，响应订单推送回调 ，查询当日成交 ，查询历史成交 ，响应成交推送回调 接口的返回字段展示。  

# #订单有效期  

TimeInForce  

DAY  
当日有效  
GTC  
撤单前有效  

# #账户所属券商  

SecurityFirm  

NONE  

未知  

FUTUSECURITIES富途证券（香港）  

FUTUINCmoomoo 证券(美国)  

FUTUSGmoomoo 证券(新加坡)  

FUTUAUmoomoo 证券(澳大利亚)  

# #模拟交易账户类型  

# SimAccType  

NONE未知  

STOCK股票模拟账户  

OPTION 期权模拟账户  

FUTURES 期货模拟账户  

# #风险状态  

# CltRiskStatus  

NONE  

未知  

LEVEL1非常安全  

LEVEL2安全  

LEVEL3较安全  

LEVEL4 较低风险  

LEVEL5 中等风险  

LEVEL6 偏高风险  

LEVEL7 预警  

LEVEL8 危险  

LEVEL9 危险  

#日内交易限制情况 DtStatus  

NONE未知  

# Unlimited  

无限次  

# EM_Call  

EM-Call  

# DT_Call  

DT-Call  

# #交易品类  

# 基础功能  

#设置接口信息  

# set_client_info(client_id, client_ver)  

介绍设置调用接口信息, 非必调接口参数client_id: client 的标识o client_ver: client 的版本号  

Example  

from futu import \*   
SysConfig.set_client_info("MyFutuAPI", 0)   
quote_ctx $=$ OpenQuoteContext(host $=$ '127.0.0.1', port $=$ 11111)   
quote_ctx.close()  

# 设置协议格式  

# set_proto_fmt(proto_fmt)  

介绍  

设置通讯协议 body 格式, 目前支持 Protobuf|Json 两种格式，默认ProtoBuf, 非必调接口  

参数proto_fmt: 协议格式，参见ProtoFMT  

from futu import \*  
SysConfig.set_proto_fmt(ProtoFMT.Protobuf)  
quote_ctx $=$ OpenQuoteContext(host $=$ '127.0.0.1', port $=$ 11111)  
quote_ctx.close()  

# 设置回调  

# set_handler(handler)  

介绍设置异步回调处理对象  

参数handler: 回调处理对象  

<html><body><table><tr><td>类</td><td>说明</td></tr><tr><td>SysNotifyHandlerBase</td><td>OpenD 通知处理基类</td></tr><tr><td>StockQuoteHandlerBase</td><td>报价处理基类</td></tr><tr><td>OrderBookHandlerBase</td><td>摆盘处理基类</td></tr><tr><td>CurKlineHandlerBase</td><td>实时 K 线处理基类</td></tr><tr><td>TickerHandlerBase</td><td>逐笔处理基类</td></tr><tr><td>RTDataHandlerBase</td><td>分时数据处理基类</td></tr><tr><td>BrokerHandlerBase</td><td>经济队列处理基类</td></tr><tr><td>PriceReminderHandlerBase</td><td>到价提醒处理基类</td></tr><tr><td>TradeOrderHandlerBase</td><td>订单处理基类</td></tr><tr><td>TradeDealHandlerBase</td><td>成交处理基类</td></tr></table></body></html>  

# Example  

import time from futu import \*  

class OrderBookTest(OrderBookHandlerBase):  

def on_recv_rsp(self, rsp_str): ret_code, data $=$  

super(OrderBookTest,self).on_recv_rsp(rsp_str)if ret_code ! $=$ RET_OK:print("OrderBookTest: error, msg: %s" % data)return RET_ERROR, dataprint("OrderBookTest ", data) # OrderBookTest 自己的处理  
逻辑  

return RET_OK, dataquote_ctx $=$ OpenQuoteContext(host='127.0.0.1', port $=$ 11111)handler $=$ OrderBookTest()quote_ctx.set_handler(handler)  # 设置实时摆盘回调quote_ctx.subscribe(['HK.00700'], [SubType.ORDER_BOOK])  # 订阅买卖摆盘类型，OpenD 开始持续收到服务器的推送time.sleep(15)  #  设置脚本接收 OpenD 的推送持续时间为15 秒  

quote_ctx.close()  # 关闭当条连接，OpenD 会在1 分钟后自动取消相应股票相应类型的订阅  

# 获取连接 ID  

# get_sync_conn_id()  

介绍 获取连接 ID，连接初始化成功后才会有值 返回 conn_id: 连接 ID  

Example  

from futu import \*   
quote_ctx $=$ OpenQuoteContext(host='127.0.0.1', port $=$ 11111) quote_ctx.get_sync_conn_id()   
quote_ctx.close() # 结束后记得关闭当条连接，防止连接条数用尽  

# 事件通知回调  

# SysNotifyHandlerBase  

介绍通知 OpenD 一些重要消息，类似连接断开等  

协议 ID  

1003  

返回  

<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>ret</td><td>RET CODE</td><td>接口调用结果</td></tr><tr><td rowspan="2">data</td><td>tuple</td><td>当 ret RETOK时，返回 事件通知数据</td></tr><tr><td>str</td><td>当 ret!= RET OK，返回错误描述</td></tr></table></body></html>  

事件通知数据 的格式如下：  


<html><body><table><tr><td>参数</td><td>类型</td><td>说明</td></tr><tr><td>notify_t ype</td><td>SysNotifyType</td><td>通知类型</td></tr><tr><td rowspan="3">sub_type</td><td>ProgramStatus Type</td><td>子类型。当 notify_type =二 SysNotifyType. PROGRAM STATUS 时，sub_type 返 回程序状态类型</td></tr><tr><td>GtwEventType</td><td>子类型。当 notify_type == SysNotifyType. GTW_EVEN T 时，sub_type 返回 OpenD事件通知类型</td></tr><tr><td>0</td><td>当 notify_type != SysNotifyType. PROGRAM_ STATUS 且 notify_type != SysNotifyType. GTW_EVEN T时，sub_type 返回0</td></tr><tr><td>msg</td><td>dict</td><td>事件信息。当 notify_type == SysNotifyType. CONN_STA TUS 时，msg 返回连接 状态事件信息字典 事件信息。当 notify_type ==</td></tr></table></body></html>  

![](FutuAPI/fa2b67ba39678eeb2feac8a2d3afed349f97775bb6f968431768e599c18f3fac.jpg)  

# 连接状态事件信息 字典结构如下（连接状态类型为  

import time from futu import \*  

class SysNotifyTest(SysNotifyHandlerBase): def on_recv_rsp(self, rsp_str): ret_code, data $=$ super(SysNotifyTest,   
self).on_recv_rsp(rsp_str) notify_type, sub_type, msg $=$ data if ret_code ! $=$ RET_OK: logger.debug("SysNotifyTest: error, msg:   
{}".format(msg)) return RET_ERROR, data if notify_type $==$ SysNotifyType.GTW_EVENT:  # OpenD 事件   
通知 print("GTW_EVENT, type: {} msg: {}".format(sub_type,   
msg)) elif notify_type $==$ SysNotifyType.PROGRAM_STATUS:  # 程   
序状态变化通知 print("PROGRAM_STATUS, type: {} msg:   
{}".format(sub_type, msg)) elif notify_type $==$ SysNotifyType.CONN_STATUS:  ## 连接   
状态变化通知 print("CONN_STATUS, qot:   
{}".format(msg['qot_logined'])) print("CONN_STATUS, trd:   
{}".format(msg['trd_logined'])) elif notify_type $==$ SysNotifyType.QOT_RIGHT:  # 行情权限   
变化通知 print("QOT_RIGHT, hk:   
{}".format(msg['hk_qot_right']))  

{}".format(msg['hk_option_qot_right'])) print("QOT_RIGHT, hk_future:  

{}".format(msg['hk_future_qot_right'])) print("QOT_RIGHT, us:  

{}".format(msg['us_qot_right'])) print("QOT_RIGHT, us_option:  

{}".format(msg['us_option_qot_right'])) print("QOT_RIGHT, cn:  

{}".format(msg['cn_qot_right'])) print("QOT_RIGHT, us_index:  

{}".format(msg['us_index_qot_right'])) print("QOT_RIGHT, us_otc:  

{}".format(msg['us_otc_qot_right'])) print("QOT_RIGHT, sg_future:  

{}".format(msg['sg_future_qot_right'])) print("QOT_RIGHT, jp_future:  

{}".format(msg['jp_future_qot_right'])) print("QOT_RIGHT, us_future_cme:  

{}".format(msg['us_future_qot_right_cme'])) print("QOT_RIGHT, us_future_cbot:  

{}".format(msg['us_future_qot_right_cbot'])) print("QOT_RIGHT, us_future_nymex:  

{}".format(msg['us_future_qot_right_nymex'])) print("QOT_RIGHT, us_future_comex:  

{}".format(msg['us_future_qot_right_comex'])) print("QOT_RIGHT, us_future_cboe:  

{}".format(msg['us_future_qot_right_cboe'])) return RET_OK, data  

quote_ctx $=$ OpenQuoteContext(host='127.0.0.1', port $=$ 11111)handler $=$ SysNotifyTest()  

quote_ctx.set_handler(handler)  # 设置回调time.sleep(15)  # 设置脚本接收 OpenD 的推送持续时间为15 秒quote_ctx.close()  # 结束后记得关闭当条连接，防止连接条数用尽\`  

# 通用定义  

# #接口调用结果  

# RET_CODE  

RET_OK 成功  

RET_ERROR 失败  

# #协议格式  

ProtoFMT  

Protobuf  
Google Protobuf 格式  
Json  
Json 格式  

#包加密算法#程序状态类型  

ProgramStatusType  

NONE  
未知  
LOADED  
已完成必要模块加载  

LOGING登录中  

NEED_PIC_VERIFY_CODE需要图形验证码  

NEED_PHONE_VERIFY_CODE需要手机验证码  

LOGIN_FAILED 登录失败  

FORCE_UPDATE客户端版本过低  

NESSARY_DATA_PREPARING正在拉取必要信息  

NESSARY_DATA_MISSING缺少必要信息  

UN_AGREE_DISCLAIMER未同意免责声明  

READY 正常可用状态  

FORCE_LOGOUTOpenD 登录后被强制退出登录#网关事件通知类型GtwEventType  

LocalCfgLoadFailed本地配置文件加载失败  

APISvrRunFailed 网关监听服务运行失败  

ForceUpdate 强制升级网关  

LoginFailed 登录富途服务器失败  

UnAgreeDisclaimer未同意免责声明，无法运行  

LOGIN_FAILED 登录失败  

NetCfgMissing缺少网络连接配置  

KickedOut登录被踢下线  

LoginPwdChanged 登录密码变更  

BanLogin牛牛后台不允许该账号登录  

NeedPicVerifyCode登录需要输入图形验证码  

NeedPhoneVerifyCode登录需要输入手机验证码  

AppDataNotExist程序打包数据丢失  

NessaryDataMissing必要的数据没同步成功TradePwdChanged交易密码变更通知EnableDeviceLock需启用设备锁  

# #系统通知类型  

GTW_EVENT  
网关事件  
PROGRAM_STATUS  
程序状态变化  
CONN_STATUS  
与后台服务的连接状态变化  
QOT_RIGHT  
行情权限变化  

# #包唯一标识  

# PacketID  

message PacketID   
{ required uint64 connID $=$ 1; //当前 TCP 连接的连接 ID，一   
条连接的唯一标识，InitConnect 协议会返回 required uint32 serialNo $=$ 2; //自增序列号   
}  

# 程序状态  

message ProgramStatus  
{required ProgramStatusType type $=$ 1; //当前状态optional string strExtDesc $=$ 2; // 额外描述  
}  

# OpenD 相关  

#Q1：OpenD 因未完成“问卷评估及协议确认”自动退出  

A: 您需要进行相关问卷评估及协议确认，才可以使用 OpenD，请先 前往完成。  

# #Q2：OpenD 因”程序自带数据不存在“退出  

A: 一般因权限问题导致自带数据拷贝失败，可以尝试将程序目录下 $A p p d a t a.d a t$ 解压后的文件拷贝到程序数据目录下。  

windows 程序数据目录:%appdata%/com.futunn.FutuOpenD/F3CNN非 windows 程序数据目录:\~/.com.futunn.FutuOpenD/F3CNN  

# #Q3：OpenD 服务启动失败  

A: 请检查：  

1. 是否有其他程序占用所配置的端口；  

2. 是否已经有配置了相同端口的 OpenD 在运行。  

# #Q4：如何验证手机验证码？  

A: 在 OpenD 界面上或远程到 Telnet 端口，输入命令  

input_phone_verify_code -code=123456。  

提示  

123456 是收到的手机验证码  

-code $=$ 123456 前有空格  

# #Q5：是否支持其他编程语言？  

A: OpenD 有对外提供基于 socket 的协议，目前我们提供并维护 Python，  

$C++$ ，Java，C# 和 JavaScript 接口，下载入口。  

如果上述语言仍不能满足您的需求，您可以自行对接 Protobuf 协议。  

# #Q6：在同一设备多次验证设备锁  

A: 设备标识随机生成并存放于  

windows: %appdata%/com.futunn.FutuOpenD/F3CNN/Device.dat 文件中。 非windows: \~/.com.futunn.FutuOpenD/F3CNN/Device.dat  

提示  

1. 如果文件被删除或损坏，OpenD 会重新生成新设备标识，然后验证设备锁。  
2. 另外镜像拷贝部署的用户需要注意，如果多台机器的 Device.dat 内容相同，也会导致这些机器多次验证设备锁。删除 Device.dat 文件即可解决。  

# #Q7：OpenD 是否有提供 Docker 镜像？  

A: 目前没有提供。  

# #Q8：一个账号可以登录多个 OpenD 吗？  

A: 一个账号可以在多台机器上登录 OpenD 或者其他客户终端，最多允许 10个 OpenD 终端同时登录。同时有“行情互踢”的限制，只能有一个 OpenD 获得最高权限行情。例如：两个终端登录同一个账号，只能有一个港股 LV2 行情，另一个是港股 BMP 行情。  

# #Q9：如何控制 OpenD 和其他客户端（桌面端和移动端）的行情权限？  

A: 应交易所的规定，多个终端同时在线会有“行情互踢”的限制，只能有一个终端获得最高权限行情。OpenD 命令行版本的启动参数中，内置了 auto_hold_quote_right 参数，用于灵活配置行情权限。当该参数选项开启时，OpenD 在行情权限被抢后，会自动抢回。如果 10 秒内再次被抢，则其他终端获得最高行情权限（OpenD 不会再抢）。  

# #Q10：如何优先保证 OpenD 行情权限？  

1. 将 OpenD 启动参数 auto_hold_quote_right 配置为 1；  

2. 保证不要在移动端或桌面端富途牛牛上在 10 秒内连续两次抢最高权限（登录算一次，点击“重启行情”算第二次）。  

![](FutuAPI/fc9810a94e4fe4b45a8e30586ebb61290d277329f2b122465697b2387feb6a01.jpg)  

# #Q11：如何优先保证移动端（或桌面端）的行情权限？  

A: OpenD 启动参数 auto_hold_quote_right 设置为 0，移动端或桌面端富途牛牛在 OpenD 之后登录即可。  

# #Q12：使用可视化 OpenD 记住密码登录，长时间挂机后提示连接断开，需要重新登录？  

A: 使用可视化 OpenD，如果选择记住密码登录，用的是记录在本地的令牌。由于令牌有时间限制，当令牌过期后，如果出现网络波动或富途后台发布，就可能导致与后台断开连接后无法自动连接上的情况。因此，可视化 OpenD 如果希望长时间挂机，建议手动输入密码登录，由 OpenD 自动处理该情况。  

# #Q13：遇到产品缺陷，如何请富途的研发工程师排查日志？  

# A:  

1. 与客服沟通问题表现，详述：发生错误的时间、OpenD 版本号、 API版本号、脚本语言名、接口名或协议号、含详细入参和返回的短代码或截图。  
2. 客服确认是产品缺陷后，如需进一步日志排查，研发工程师会主动联系。  
3. 部分问题须提供 OpenD 日志，方便定位确认问题。交易类问题需要info 日志级别，行情类问题需要 debug 日志级别。日志级别 log_level可以在 $_{0p e n D.x m l}$ 中 配置 ，配置后需要重启 OpenD 方能生效，待问题复现后，将该段日志打包发给富途研发工程师。  

# 提示  

日志路径如下：  

windows：%appdata%/com.futunn.FutuOpenD/Log  

非 windows：\~/.com.futunn.FutuOpenD/Log  

# #Q14：脚本连接不上 OpenD  

A: 请先尝试检查：  

1. 脚本连接的端口与 OpenD 配置的端口是否一致。  
2. 由于 OpenD 连接上限为 128，是否有无用连接未关闭。  

3. 检查监听地址是否正确，如果脚本和 OpenD 不在同一机器，OpenD监听地址需要设置成 0.0.0.0 。  

# #Q15：连接上一段时间后断开  

A: 如果是自己对接协议，检查下是否有定时发送心跳维持连接。  

# #Q16：Linux 下通过 multiprocessing 模块以多进程方式运行 Python 脚本，连不上 OpenD？  

A: Linux/Mac 环境下以默认方式创建进程后，父进程中 py-futu-api 内部创建的线程将会在子进程中消失，导致程序内部状态错误。  

可以用 spawn 方式来启动进程：  

import multiprocessing as mp mp.set_start_method('spawn') $\textsf{p}=$ mp.Process(target $=$ func)  

Copied!  

![](FutuAPI/c4b7f147e173ecca4429132bc3865f39a642a481d85ebf2034a8bc47a2396c32.jpg)  

2. 分别打开两个命令行 OpenD 文件夹配置好两份 OpenD.xml 文件。第一份配置文件参数：api_port $=$ 11111，login_account $=$ 登录账号1，login_pwd $=$ 登录密码1  

第二份配置文件参数：api_port $=$ 11112，login_account $=$ 登录账号2，login_pwd $=$ 登录密码2  

![](FutuAPI/34352292b1db7b345dc2debd537089c1b7f161f583bc40f55c20a66fc697849b.jpg)  

3. 配置完成后，分别打开两个 OpenD 程序运行。  

Futu_OpenD_7.2.3407_Windows  

![](FutuAPI/f020fa3b27f0806a6d94035b86f13d5e73e472e60ad0988625da2bbdc83f897c.jpg)  

4. 调用接口时，注意接口的参数port（OpenD 监听端口）与 OpenD.xml文件中的参数api_port 为对应关系例如：  

from futu import \*  

# 向账号1 登录的 OpenD 进行请求  
quote_ctx $=$ OpenQuoteContext(host $=$ '127.0.0.1', port $=$ 11111,is_encrypt $=$ False)  
quote_ctx.close() # 结束后记得关闭当条连接，防止连接条数用尽# 向账号2 登录的 OpenD 进行请求  
quote_ctx $=$ OpenQuoteContext(host $\because$ '127.0.0.1', port $=$ 11112,is_encrypt $=$ False)  
quote_ctx.close() # 结束后记得关闭当条连接，防止连接条数用尽  

# Copied!  

#Q18：行情权限被其他客户端踢掉，如何通过脚本执行抢权限的运维命令？  

A：  

1. 在OpenD 启动参数中，配置好 Telnet 地址和 Telnet 端  

口。  

![](FutuAPI/698e9c61d64ed771c1730540e0d60b0040cd7d17f21e08fca5cc89f2de1dd7cb.jpg)  

![](FutuAPI/9f405b5d78dc2efce65ff514e58c1661a32a77a3ed9f719134bddff25de1b917.jpg)  

2. 启动 OpenD（会同时启动 Telnet）。  

3. 当发现行情权限被抢之后，您可以参考如下代码示例，通过 Telnet，向  

OpenD 发送 request_highest_quote_right 命令。  

from telnetlib import Telnet  

with Telnet('127.0.0.1', 22222) as tn:  # Telnet 地址为：127.0.0.1，Telnet 端口为：22222  

tn.write(b'request_highest_quote_right\r\n')   
$\mathsf{r e p l y\ =\ b^{\prime}\ a l y}\ =\ \mathsf{b^{\prime}}\ ^{\prime}$   
while True: msg $=$ tn.read_until(b'\r\n', timeout=0.5) reply $\scriptstyle+=$ msg if $:\mathtt{m s g\ ==}\ \mathtt{b}^{\prime}\ :$ : break   
print(reply.decode('gb2312'))  

Copied!  

# #Q19：OpenD 自动升级失败  

A： 通过update 命令执行 OpenD 自动更新失败，可能的原因：  

•  文件被其他进程占用：可以尝试关闭其他 OpenD 进程，或者重启系统后，再次执行 update 如果以上仍无法解决，可以通过官网自行下载更新。  

# #Q20：ubuntu22 无法启动可视化 OpenD？  

A： 在有些Linux 发行版（例如Ubuntu 22.04）运行可视化OpenD 时，可能会提示：dlopen(): error loading libfuse.so.2。 这是因为这些系统没有默认安装libfuse。通常可以手动安装来解决，例如对于Ubuntu22.04，可以在命令行运行：  

sudo apt update sudo apt install -y libfuse2  

Copied!  

安装成功后就可以正常运行可视化OpenD 了。详细信息请参考：https://docs.appimage.org/user-guide/troubleshooting/fuse.html。  

# 行情相关  

# #Q1：订阅失败  

A: 订阅接口返回错误，有以下两类常见情况：  

订阅额度不足：  

订阅额度规则参见 订阅额度 & 历史 K 线额度  

订阅权限不足：  

支持订阅的行情权限见下表  

<html><body><table><tr><td>市场</td><td>品种</td><td>支持订阅的行情权限</td></tr><tr><td rowspan="3">香港市场</td><td>股票</td><td>LV2, SF</td></tr><tr><td>期权</td><td>LV1,LV2</td></tr><tr><td>期货</td><td>LV1,LV2</td></tr><tr><td rowspan="3">美国市场</td><td>股票</td><td>LV1,LV2</td></tr><tr><td>期权</td><td>LV1</td></tr><tr><td>期货</td><td>LV2</td></tr><tr><td>A股市场</td><td>股票</td><td>LV1</td></tr></table></body></html>  

获取行情权限的方式参见 行情权限  

注意：若账号拥有上述权限，但仍订阅失败，可能存在被其他终端 踢掉行情权限 的情况。  

# #Q2：反订阅失败  

A: 订阅至少一分钟后才能反订阅。  

# #Q3：反订阅成功但没释放额度  

A: 所有连接都对该行情反订阅，才会释放额度。  

举例：A 连接和 B 连接都在订阅 HK.00700 的摆盘，当 A 连接反订阅后，由于 B 连接仍在调用腾讯的摆盘数据，因此 OpenD 的额度不会释放，直至所有连接都反订阅 HK.00700 的摆盘。  

# #Q4：订阅不足一分钟关闭脚本连接，会释放额度吗？  

A: 不会。连接关闭后，订阅时长不足一分钟的标的类型，会在达到一分钟后才自动反订阅，并释放相应的订阅额度。  

# #Q5：请求限频的具体限制逻辑是怎样？  

A: 30 秒内最多 n 次，是指第 1 次和第 $\mathsf{n}+\mathsf{\tau}^{\mathsf{\tau}}$ 次请求间隔需要大于 30 秒。  

# #Q6：自选股添加不上是什么原因？  

A: 请先检查是否有超出上限，或者删除一部分自选。  

# #Q7：为什么 OpenAPI 端的美股报价和牛牛显示端的全美综合报价有不同？  

A: 由于美股交易分散在很多家交易所，富途有提供两种美股基本报价行情，一种是 Nasdaq Basic（Nasdaq 交易所的报价），另一种是全美综合报价（全美  

13 家交易所的报价）。而 OpenAPI 的美股正股行情目前仅支持通过行情卡购买的方式获取 Nasdaq Basic，不支持全美综合报价。因此，如果您同时购买了显示端的全美综合报价行情卡，和仅用于 OpenAPI 的 Nasdaq Basic 行情卡，确实有可能出现牛牛显示端和 OpenAPI 端的报价差异。  

# #Q8：OpenAPI 行情卡在哪里购买？  

A:  

港股市场  

港股 LV2 高级行情（仅港澳台及海外 IP）港股期权期货 LV2 高级行情（仅港澳台及海外 IP）港股 LV2 + 期权期货 LV2 行情（仅港澳台及海外 IP）港股高级全盘行情（SF 行情）  

美股市场  

Nasdaq Basic   
Nasdaq Basic+TotalView (Non-Pro)   
Nasdaq Basic+TotalView (Pro)   
期权 OPRA 实时行情  

# #Q9：为什么有时候，获取实时数据的 get 接口响应比较慢？  

A: 因为获取实时数据的 get 接口需要先订阅，并依赖后台给 OpenD 的推送。如果用户刚订阅就立刻用 get 接口请求，OpenD 有可能尚未收到后台推送。为了防止这种情况的发生，get 接口内置了等待逻辑，3 秒内收到推送会  

立刻返回给脚本，超过 3 秒仍未收到后台推送，才会给脚本返回空数据。  

涉及的 get 接口包括：get_rt_ticker、get_rt_data、get_cur_kline、get_order_book、get_broker_queue、get_stock_quote。因此，当发现获取实时数据的 get 接口响应比较慢时，可以先检查一下是否是无成交数据的原因。  

# #Q10：购买 OpenAPI 美股 Nasdaq Basic 行情卡后，可以获取哪些数据？  

A: Nasdaq Basic 行情卡购买激活后，可以获取的品类涵盖 Nasdaq、NYSE、NYSE MKT 交易所上市证券（包括美股正股和 ETF，不包括美股期货和美股期权）。  

支持的数据接口包括：快照，历史 K 线，实时逐笔订阅，实时一档摆盘订阅，实时 K 线订阅，实时报价订阅，实时分时订阅，到价提醒。  

# #Q11：各个行情品类的摆盘支持多少档？  

A:   


<html><body><table><tr><td>行情品类</td><td>BMP</td><td>LV1</td><td>LV2</td><td>SF</td></tr><tr><td>港股（含正股、窝轮、 牛熊、界内证)</td><td>0</td><td></td><td>10</td><td>全盘+千 笔明细</td></tr><tr><td>港股期权期货</td><td>0</td><td>1</td><td>10</td><td></td></tr><tr><td>美股（含 ETF)</td><td></td><td>1</td><td>40笔明细（档 数不固定)</td><td></td></tr><tr><td>美股期权</td><td></td><td>1</td><td></td><td></td></tr><tr><td>美股期货</td><td></td><td></td><td>40笔明细（档 数不固定)</td><td></td></tr></table></body></html>  

<html><body><table><tr><td>行情品类</td><td>BMP</td><td>LV1</td><td>LV2</td><td>SF</td></tr><tr><td>A股</td><td></td><td>5</td><td></td><td></td></tr></table></body></html>

#Q12：为什么我购买激活了行情卡之后，OpenD仍然没有行情权限？  

# A:  

1. 由于 OpenAPI 的行情权限跟 APP 的行情权限不完全一样，部分行情卡仅适用于 APP 端。请先确认您所购买的行情卡是否是 OpenD 适用的。我们已将 OpenAPI 适用的 所有 行情卡列在《权限与限制》一节，请点击 这里 查看。  

2. 行情卡购买激活成功后，是立即生效的。请 重新启动 OpenD 后，再次查看权限状态。  

# #Q13：如何通过订阅接口获取实时行情？  

# 第一步：订阅  

将标的的代码和数据类型传入 订阅接口，完成订阅。  

订阅接口支持了实时报价、实时摆盘、实时逐笔、实时分时、实时 K 线、实时经纪队列数据的获取。订阅成功后，OpenD 会持续收到富途服务器的实时数据推送。  

注意：订阅额度会根据您的总资产、交易笔数和交易量，来进行分配，具体规则参见 订阅额度 & 历史 K 线额度。所以，如果您的订阅额度不足，可以先  

检查一下是否有无用的订阅在占用额度，及时 反订阅 即可释放已占用的订阅额度。  

# 第二步：取数据  

如何将订阅推送的数据从 OpenD 取回脚本呢？我们提供了如下两种方式：  

# 方式 1：实时数据回调  

设置相应的回调函数，来异步处理 OpenD 收到的数据推送。  

设置好回调函数后，OpenD 会将收到的实时数据，立即推给脚本的回调函数进行处理。  

如果所订阅的标的比较活跃，此时的推送数据可能数据量较大且频率较高。如果您希望适当降低 OpenD 给脚本的推送频率，建议在 OpenD 启动参数 中配置 API 推送频率（qot_push_frequency）。  

方式 1 涉及的接口包括：实时报价回调、实时摆盘回调、实时 K 线回调、实时分时回调、实时逐笔回调、实时经纪队列回调。  

# 方式 2：获取实时数据  

通过获取实时数据接口，可以将 OpenD 收到的最新的数据，取回脚本。这种方式更加灵活，脚本不需要处理海量的推送。只要 OpenD 在持续接收富途服务器的推送，脚本可以随用随取，不用不取。  

由于是从 OpenD 接收的推送数据中取，所以这类接口没有频率限制。  

方式 2 涉及的接口包括：获取实时报价、获取实时摆盘、获取实时 K 线、获取实时分时、获取实时逐笔、获取实时经纪队列。  

# #Q14：各个市场状态对应什么时间段？  

<html><body><table><tr><td>市场</td><td>品类</td><td>市场状态</td><td>时间段 （当地时 间)</td></tr><tr><td rowspan="9">香港市 场</td><td rowspan="5">证券类 产品 （含股 票、 ETFs、 窝轮、 牛熊、 界内</td><td>*NONE：无交易</td><td>CST 08:55 - 09:00</td></tr><tr><td>*ACTION：盘前竞价</td><td>CST 09:00 - 09:20</td></tr><tr><td>*WAITING_OPEN：等待开盘</td><td>CST 09:20 - 09:30</td></tr><tr><td>* MORNING：早盘</td><td>CST 09:30 - 12:00</td></tr><tr><td>* REST：午间休市</td><td>CST 12:00 - 13:00</td></tr><tr><td>* AFTERNOON：午盘 证）</td><td>CST 13:00 - 16:00</td></tr><tr><td>*HK_CAS：港股盘后竞价（港股市 场增加 CAS 机制对应的市场状 态)</td><td>CST 16:00 - 16:08</td></tr><tr><td>*CLOSED：收盘</td><td>CST 16:08 - 08:55 (T+1)</td></tr><tr><td>*NONE：期权待开盘</td><td>CST 08:55 - 09:30</td></tr><tr><td rowspan="3">期权、 期货 （仅日 市)</td><td>* MORNING：早盘</td><td>CST 09:30 - 12:00</td></tr><tr><td>* REST：午间休市</td><td>CST 12:00 - 13:00</td></tr><tr><td>*AFTERNOON：午盘</td><td>CST 13:00 - 16:00</td></tr></table></body></html>  

<html><body><table><tr><td rowspan="5">期货 （日夜 市)</td><td rowspan="5"></td><td>* CLOSED：收盘</td><td>CST 16:00 - 08:55 (T+1)</td></tr><tr><td>* FUTURE_DAY_WAIT_FOR_OPEN:期 货待开盘</td><td rowspan="5">不同品种 交易时间 不同</td></tr><tr><td>*NIGHTOPEN：夜市交易时段</td></tr><tr><td>*NIGHT_END：夜市收盘 * FUTURE_DAY_WAIT_FOR_OPEN: 期</td></tr><tr><td>货待开盘</td></tr><tr><td>段 *PRE_MARKET_BEGIN：美股盘前交</td><td>*FUTURE_DAY_OPEN：日市交易时</td></tr><tr><td rowspan="8">美国市 场</td><td rowspan="4">证券类 产品 （含股 票、 ETFs)</td><td>* FUTURE DAY_CLOSE：日市收盘</td><td>EST 04:00 - 09:30</td></tr><tr><td>易时段 *AFTERNOON：美股持续交易时段</td><td>EST 09:30</td></tr><tr><td>*AFTER_HOURS_BEGIN：美股盘后</td><td>- 16:00 EST 16:00</td></tr><tr><td>交易时段 *AFTERHOURSEND：美股收盘</td><td>- 20:00 EST 20:00 04:00</td></tr><tr><td rowspan="5">期权</td><td></td><td>(T+1)</td></tr><tr><td>*NONE：期权待开盘</td><td rowspan="4">不同品种 交易时间 不同</td></tr><tr><td>* REST：美指期权午间休市</td></tr><tr><td>*AFTERNOON：美股持续交易时段 *TRADE_AT_LAST：美指期权盘尾</td></tr><tr><td>交易时段 *NIGHT：美指期权夜市交易时段</td></tr><tr><td rowspan="2"></td><td></td><td></td></tr><tr><td>*CLOSED：收盘</td><td></td></tr></table></body></html>  

<html><body><table><tr><td rowspan="5"></td><td rowspan="5">期货</td><td>*FUTURESWITCHDATE：美期待开</td><td rowspan="5">不同品种 交易时间 不同</td></tr><tr><td>*FUTURE_OPEN：美期交易时段</td></tr><tr><td>*FUTURE_BREAK：美期中盘休息</td></tr><tr><td>*FUTRUEBREAKOVER：美期休息 后交易时段</td></tr><tr><td>*FUTURE_CLOSE：美期收盘</td></tr><tr><td rowspan="9">A股市 场</td><td rowspan="5">证券类 产品 （含股 票、 ETFs)</td><td>*NONE：无交易</td><td>CST 08:55 - 09:15</td></tr><tr><td>*Auction：盘前竞价</td><td>CST 09:15 - 09:25</td></tr><tr><td>*WAITING_OPEN：等待开盘</td><td>CST 09:25 - 09:30</td></tr><tr><td>*MORNING：早盘</td><td>CST 09:30 - 11:30</td></tr><tr><td>* REST：午间休市</td><td>CST 11:30 - 13:00</td></tr><tr><td rowspan="2"></td><td>* AFTERNOON：午盘</td><td>CST 13:00 - 15:00</td></tr><tr><td>*CLOSED：收盘</td><td>CST 15:00 - 08:55 (T+1)</td></tr><tr><td rowspan="4">新加坡 市场</td><td rowspan="4">期货</td><td>* FUTURE DAY WAIT FOR OPEN:期 货待开盘</td><td rowspan="4">不同品种 交易时间</td></tr><tr><td>* NIGHTOPEN：夜市交易时段</td></tr><tr><td>*NIGHT_END：夜市收盘</td><td>不同</td></tr><tr><td>*FUTURE_DAY_OPEN：日市交易时 段</td><td></td></tr></table></body></html>  

<html><body><table><tr><td></td><td></td><td>*FUTURE_DAY_CLOSE：日市收盘</td><td></td></tr><tr><td rowspan="5">日本市 场</td><td rowspan="5">期货 段</td><td>* FUTURE DAY WAIT FOR OPEN:期 货待开盘</td><td>JST 16:25 （T-1）- 16:30（T- 1)</td></tr><tr><td>*NIGHT_OPEN：夜市交易时段</td><td>JST 16:30 (T-1) 05:30</td></tr><tr><td>*NIGHTEND：夜市收盘</td><td>JST 05:30 - 08:45</td></tr><tr><td>*FUTURE_DAY_OPEN：日市交易时</td><td>JST 08:45 - 15:15</td></tr><tr><td>*FUTURE_DAY_CLOSE：日市收盘</td><td>JST 15:15 - 16:25</td></tr></table></body></html>  

\* CST, EST, JST 分别表示中国时间，美东时间，日本时间  

# #Q15：接口参数股票代码的格式  

使用不同编程语言的用户，需要的股票代码的格式不同：  

Python 用户  
股票代码 code 格式：行情市场.代码。  
例如：腾讯控股，参数 code 传入'HK.00700'。  
非 Python 用户  
股票结构参见 Security。  
例如：腾讯控股，参数 market 传入 QotMarket_HK_Security，参数 code 传入'00700'。  

查询方式：  

通过 APP 查看代码和行情市场：行情 $>$ 自选 $>$ 全部。  

行情市场定义，请参考 这里。  

![](FutuAPI/831ecba9aae1810a56eb24b0161e63c380fd2ca583885ae971f4b41a7a808286.jpg)  

![](FutuAPI/09732c7e3298be417c38a4bfda0e68faafd42ba4c4e9b9c8676b3cd2cf46277a.jpg)  

# #Q16：复权因子相关  

# #概述  

所谓 复权 就是对股价和成交量进行权息修复，按照股票的实际涨跌绘制股价走势图，并把成交量调整为相同的股本口径。  

公司行动（如：拆股、合股、送股、转增股、配股、增发股、分红）均可能对股价产生影响，而复权计算可对量价进行调整，剔除公司行动的影响，保持股价走势的连续性。  

# #名词解释  

公司行动：上市公司进行一些股权、股票等影响公司股价和股东持仓变化的行为。  
前复权：保持现有的股价不变，以当前的股价为基准，对以前的股价进行复权计算。  
后复权：保持先前的股价不变，以过去的股价为基准，对以后的股价进行复权计算。  
复权因子：即权息修复比例，用于计算复权后的价格及持仓数量。除权除息日：即股权登记日下一个交易日。在股票的除权除息日，证券交易所都要计算出股票的除权除息价，以作为股民在除权除息日开盘的参考。其意义是股票股利分配给股东的日期。  

# #复权方法  

主流的复权计算方法分为两种：事件法和连乘法；而 OpenAPI 针对不同市场使用不同的计算方法。  

事件复权法：通过还原除权除息的各类事件进行复权；存在两个复权因子（复权因子 A 和 复权因子 B），复权因子 B 主要调整现金分红对股价的影响，而复权因子 A 调整其他公司行动对股价的影响。  

连乘复权法：通过复权因子连乘的方式进行复权，只保留 复权因子 A（或将 复权因子 B 置为0），复权因子 A 为 除权除息日前收盘价/该日经权息调整后的前收盘价。  

# 提示  

OpenAPI 对美股前复权使用连乘法，即将 复权因子 B 置为0。  

OpenAPI 对除美股以外的标的（A 股、港股、新加坡股票等）及美股后复权使用事件法。  

# #计算公式  

# #单次复权  

前复权：  

前复权价格 $=$ 不复权价格 $\times$ 前复权因子 A + 前复权因子 B  

后复权：  

后复权价格 $=$ 不复权价格 $\times$ 后复权因子 A $^+$ 后复权因子 B  

# #多次复权  

前复权：按照时间顺序，筛选出大于计算日期的复权因子，优先使用时间较早的复权因子进行复权计算。以两次复权为例：  

$P r i c e_{n}^{a d j u s t e d}=(P r i c e_{n}*F a c t o r A_{n+1}^{a d j u s t e d}+F a c t o r B_{n+1}^{a d j u s t e d})*F a c t o r A_{n+2}^{a d j u s t e d}+F a c t o r B_{n+2}^{a d j u s t e d}$ $P r i c e_{n}^{a d j u s t e d}$ ：被计算当天的前复权价格$P r i c e_{n}$ ：当天的不复权价格Factoraitede后一天的复权因子 $\mathsf{A}$ Factor $.B_{n+1}^{a d j u s t e d}$ ：后一天的前复权因子 BFactorAajuted：后两天的前复权因子 $\mathsf{A}$ $F a c t o r B_{n+2}^{a d j u s t e d}$ ： 后两天的前复权因子 B  

后复权：按照时间倒序，筛选出小于等于计算日期的复权因子，优先使用时间较晚的复权因子进行复权计算。以两次复权为例：  

$P r i c e_{n}^{c u m u l a t i v e}=(P r i c e_{n}*F a c t o r A_{n}^{c u m u l a t i v e}+F a c t o r B_{n}^{b a c k w a r d})*F a c t o r A_{n-1}^{c u m u l a t i v e}+F a c t o r B_{n-1}^{c u m u l a t i v e}$ $P r i c e_{n}^{c u m u l a t i v e}$ ：被计算当天的后复权价格$P r i c e_{n}$ ：当天的不复权价格FactorAgumulatiue：当天的后复权因子 AFactor $B_{n}^{c u m u l a t i v e}$ ：当天的后复权因子 BFactorAcumulatiue：前一天的后复权因子AFactorBeumulatine 前一天的后复权因子B  

# #单次前复权示例  

以牧原股份为例：  

筛选复权因子如下：  

<html><body><table><tr><td>除权除息 日</td><td>股票代码</td><td>方案说明</td><td>前复权因 子A</td><td>前复权因 子B</td></tr><tr><td>2021/06/03</td><td>SZ.002714</td><td>10转4.0股派 14.61元（含 税)</td><td>0.71429</td><td>-1.04357</td></tr></table></body></html>  

不复权数据如下：  


<html><body><table><tr><td>日期</td><td>股票代码</td><td>不复权收盘价</td></tr><tr><td>2021/06/02</td><td>SZ.002714</td><td>93.11</td></tr><tr><td>2021/06/03</td><td>SZ.002714</td><td>66.25</td></tr></table></body></html>  

前复权数据如下：  

<html><body><table><tr><td>日期</td><td>股票代码</td><td>前复权收盘价</td></tr><tr><td>2021/06/02</td><td>SZ.002714</td><td>65.4639719</td></tr><tr><td>2021/06/03</td><td>SZ.002714</td><td>66.25</td></tr></table></body></html>  

前复权数据计算方法：  

牧原股份在 2021/06/03 进行拆股及现金分红行动（10 转4.0 股派14.61 元），根据前复权计算公式对 2021/06/02 的收盘价进行调整计算，则：前复权价格（65.4639719） $=$ 不复权价格（93.11） $\times$ 前复权因子 A（0.71429） $^+$ 前复权因子 B（-1.04357）  

![](FutuAPI/0a90d0813f1cfeee0f8a7910beaf860370d4c7b67075bdca798fb9c2bb4b5d8d.jpg)  

# #多次后复权示例  

接上一个例子，计算牧原股份在 2021/06/02 的后复权价格：  

筛选复权因子如下：  

<html><body><table><tr><td>除权除息 日</td><td>股票代码</td><td>方案说明</td><td>后复权 因子 A</td><td>后复权因 子B</td></tr><tr><td>2014/07/04</td><td>SZ.002714</td><td>10派2.34元 （含税）</td><td>1</td><td>0.234</td></tr><tr><td>2015-06-10</td><td>SZ.002714</td><td>10转10.0股派 0.61元（含税)</td><td>2</td><td>0.061</td></tr><tr><td>2016-07-08</td><td>SZ.002714</td><td>10转10.0股派 3.53元（含税）</td><td>2</td><td>0.353</td></tr><tr><td>2017-07-11</td><td>SZ.002714</td><td>10 转8.0股派 6.9元（含税)</td><td>1.8</td><td>0.69</td></tr><tr><td>2018-07-03</td><td>SZ.002714</td><td>10派6.91元 （含税）</td><td>1</td><td>0.691</td></tr><tr><td>2019-07-04</td><td>SZ.002714</td><td>10派0.5元（含 税）</td><td>1</td><td>0.05</td></tr><tr><td>2020-06-04</td><td>SZ.002714</td><td>10转7.0股派 5.5元（含税)</td><td>1.7</td><td>0.55</td></tr></table></body></html>  

不复权数据如下：  

<html><body><table><tr><td>日期</td><td>股票代码</td><td>不复权收盘价</td></tr><tr><td>2021/06/02</td><td>SZ.002714</td><td>93.11</td></tr></table></body></html>  

后复权数据如下：  

<html><body><table><tr><td>日期</td><td>股票代码</td><td>后复权收盘价</td></tr><tr><td>2021/06/02</td><td>SZ.002714</td><td>1150.5114</td></tr></table></body></html>  

后复权数据计算方法：  

为了计算牧原股份在 2021/06/02 的后复权价格，需要将早于  

2021/06/02 的复权事件进行一一复权，得到最后的后复权价格，具体计算如下：  

![](FutuAPI/c882b28e873ce7cf14c56c487430b744f23c1bd406b1f58d8a82fe33add72c97.jpg)  

# 交易相关  

# #Q1：模拟交易相关  

# #概述  

模拟交易是在真实的市场环境中，用虚拟资金做交易，不会对您的真实账户的资产造成影响。  

# #交易时间  

模拟交易仅支持在常规交易时段交易，不支持在非交易时段、美股盘前盘后时段、A 股港股盘前盘后竞价时段交易。详情可点击 模拟交易规则。  

# #支持品类  

OpenAPI 支持模拟交易的品类请参考 这里。  

# #解锁  

与真实交易不同，模拟交易无需对账户进行解锁，即可下单或改单撤单。  

# #订单  

1. 订单类型：限价单和市价单。  
2. 改单操作类型：模拟交易不支持使生效、使失效、删除，仅支持修改订单、 撤单。  
3. 成交：模拟交易不支持成交相关操作，包括 查询今日成交、查询历史成交、响应成交推送回调。  
4. 有效期限：模拟交易有效期限仅支持当日有效。  
5. 卖空：期权和期货支持卖空。股票仅美股支持卖空。  

# #操作平台  

1. 移动端：我的 — 模拟交易  

![](FutuAPI/de18adf5db307e0c5bc7ad10848deb73fb16fad04831480abbca42866528cdf4.jpg)  

2. 桌面端：左侧模拟 tab  

![](FutuAPI/3ded65320670c3fcfe12af9c66df9aee91dea6530a391f820b36f7448a7a6c73.jpg)  

3. 网页端：模拟交易界面  

4. OpenAPI：在调用接口时，设置参数交易环境为模拟环境即可。详见 如何使用 OpenAPI 进行模拟交易。  

提示  

以上四种方式只是操作平台不同，四种方式操作的模拟账户是共通的。  

# #如何使用 OpenAPI 进行模拟交易？  

# #创建连接  

先根据交易品种 创建相应的连接 。当交易品种是股票或期权时，请使用 OpenSecTradeContext。当交易品种是期货时，请使用 OpenFutureTradeContext。  

# #获取交易业务账户列表  

使用 获取交易业务账户列表 查看交易账户（包括模拟账户、真实账户）。以Python 为例：返回字段交易环境 trd_env 为 SIMULATE，表示模拟账户。  

# Example：Stocks and Options  

from futu import \*  

trd_ctx $=$ OpenSecTradeContext(filter_trdmarket $=$ TrdMarket.HK, hos $=^{1}127.0.0.1\prime,$ port $\leftrightharpoons$ 11111, security_firm $=$ SecurityFirm.FUTUSECURITIES) #trd_ctx $=$ OpenFutureTradeContext(host $\r=1$ 127.0.0.1', port $=$ 11111, is_encrypt $=$ None, security_firm $=$ SecurityFirm.FUTUSECURITIES)  

ret, data $=$ trd_ctx.get_acc_list()  

if ret $==$ RET_OK:  

print(data)  

print(data['acc_id'][0])  # get the first account id print(data['acc_id'].values.tolist())  # convert to list format  

else:  

print('get_acc_list error: ', data)  

trd_ctx.close()  

使用 下单接口 时，设置交易环境为模拟环境即可。以 Python 为例：trd_env  

$=$ TrdEnv.SIMULATE。  

# Example  

• from futu import \* trd_ctx $=$ OpenHKTradeContext(host $=$ '127.0.0.1', port $=$ 11111, security_firm $\lvert=$ SecurityFirm.FUTUSECURITIES) ret, data $=$ trd_ctx.place_order(pric $a\!=\!51\theta.\theta$ , qty $=\tt{1}66$ , code $=$ "HK.00700", trd_side $=$ TrdSide.BUY, trd_env $\because$ TrdEnv.SIMULATE) if ret $==$ RET_OK:   
• print(data)   
• else:   
• print('place_order error: ', data) trd_ctx.close()  

# 撤单改单  

使用 撤单接口 时，设置交易环境为模拟环境即可。以 Python 为  

例：  

# trd_env $=$ TrdEnv.SIMULATE。  

from futu import \*   
trd_ctx $=$ OpenHKTradeContext(host $=$ '127.0.0.1', port $=$ 11111,   
security_firm $\lvert=$ SecurityFirm.FUTUSECURITIES)   
order_id $=$ "4642000476506964749"   
ret, data $=$ trd_ctx.modify_order(ModifyOrderOp.CANCEL, order_id, 0, 0,   
trd_env $=$ TrdEnv.SIMULATE)   
if ret $==$ RET_OK: print(data)   
else: print('modify_order error: ', data)   
trd_ctx.close()  

# 查询历史订单  

使用 查询历史订单接口 时，设置交易环境为模拟环境即可。以 Python 为例：trd_env $=$ TrdEnv.SIMULATE。  

Example • from futu import \* trd_ctx $=$ OpenHKTradeContext(host $=$ '127.0.0.1', port $=$ 11111, security_firm $\lvert=$ SecurityFirm.FUTUSECURITIES) ret, data $=$ trd_ctx.history_order_list_query(trd_env $=$ TrdEnv.SIMULATE) if ret $==$ RET_OK: print(data) else: print('history_order_list_query error: ', data) trd_ctx.close()  

# Q5：各市场支持的订单操作  

A:  

港股支持改单、撤单、生效、失效、删除  
美股仅支持改单和撤单  
A 股通仅支持撤单  
期货支持改单、撤单、删除  

# #Q6：OpenD 启动参数future_trade_api_time_zone 如何使用？  

A：由于期货账户支持交易的品种分布在全球多个交易所，交易所的所属时区各有不同，因此期货交易 API 的时间显示就成为了一个问题。  

OpenD 启动参数中新增了 future_trade_api_time_zone 这一参数，供全球不同地区的期货交易者灵活指定时区。默认时区为 UTC+8，如果您更习惯美东时间，只需将此参数配置为 UTC-5 即可。  

提示  

此参数仅会对期货交易接口类对象生效。港股交易、美股交易、A 股通交易接口类对象的时区，仍然按照交易所所在的时区进行显示。  

此参数会影响的接口包括：响应订单推送回调，响应成交推送回调，查询今日订单，查询历史订单，查询当日成交，查询历史成交，下单。  

# #Q7：通过 OpenAPI 下的订单，能在 APP 上面看到吗？  

A：可以看到。  

通过 OpenAPI 成功发出下单指令后，您可以在 APP 的 交易 页面，查看今日订单、订单状态、成交情况等等，也可以在 消息—订单消息 中收到成交提醒的通知。  

# #Q8：哪些品类支持在非交易时段下单？  

A：所有的订单，都需要在开盘期间才能够成交。  

OpenAPI 仅对一部分品类，支持了 非交易时段下单 的功能（APP 上支持更多品类的非交易时段下单功能）。具体请参考下表：  

<html><body><table><tr><td rowspan="2">市 场</td><td rowspan="2">标的类型</td><td rowspan="2">模 拟 交 易</td><td colspan="4">真实交易</td></tr><tr><td>Futu HK</td><td>Moomoo US</td><td>Moomoo SG</td><td>Moomoo AU</td></tr><tr><td rowspan="3">香 港 市 场</td><td>证券类产品 （含股票、 ETFs、窝 轮、牛熊、</td><td></td><td></td><td></td><td></td><td>X</td></tr><tr><td>界内证) 期权</td><td></td><td>X</td><td>X</td><td>X</td><td>X</td></tr><tr><td>期货</td><td>X</td><td>X</td><td>X</td><td>X</td><td>X</td></tr></table></body></html>  

<html><body><table><tr><td rowspan="4">美 国 市 场</td><td>证券类产品 （含股票、 ETFs)</td><td></td><td>X</td><td>X</td><td>X</td><td>X</td></tr><tr><td>期权</td><td></td><td>X</td><td>X</td><td>X</td><td>X</td></tr><tr><td>期货</td><td>X</td><td>X</td><td>X</td><td>X</td><td>X</td></tr><tr><td>A 股通股票</td><td></td><td>X</td><td>X</td><td>X</td><td>X</td></tr><tr><td>A 股 市 场 新</td><td>非A 股通 股票</td><td></td><td>X</td><td>X</td><td>X</td><td>X</td></tr><tr><td>加 坡 市 场</td><td>期货</td><td>X</td><td>X</td><td>X</td><td>X</td><td>X</td></tr><tr><td>日 本 市 场</td><td>期货</td><td>X</td><td>X</td><td>X</td><td>X</td><td>X</td></tr></table></body></html>  

提示  

✓：支持非交易时段下单  

X：暂不支持非交易时段下单（或暂不支持交易）  

# #Q9：对于下单接口，各订单类型对应的必传参数  

A:   


<html><body><table><tr><td rowspan="7">参断 数</td><td rowspan="7"></td><td rowspan="3"></td><td rowspan="3"></td><td rowspan="3"></td><td rowspan="3"></td><td rowspan="3"></td><td colspan="3"></td><td></td><td></td><td></td><td></td><td></td></tr><tr><td></td><td></td><td></td><td></td><td>触及市价单</td><td>触及限价单</td><td>跟踪止损市价单</td><td>跟踪止损限价单</td></tr><tr><td></td><td></td><td>特别限价单</td><td>特别限价且要求</td><td>止损市价单</td><td>止损限价单</td><td></td><td></td><td></td><td></td></tr><tr><td>限价单</td><td>市价单</td><td></td><td>竞价市价单</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td></tr><tr><td></td><td></td><td>竞价限价单</td><td></td><td>绝对限价单</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td></tr><tr><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td>(</td><td>(</td><td></td><td></td></tr><tr><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td>止</td><td>止</td><td></td><td></td></tr></table></body></html>  

<html><body><table><tr><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td>全 部 成 交 订 单</td><td></td><td></td><td>盈</td><td>盈</td><td></td><td></td></tr><tr><td>pric e</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td></tr><tr><td>qty</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td></tr><tr><td>cod e</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td></tr><tr><td>trd_ side</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td></tr><tr><td>ord er_t ype</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td></tr><tr><td>trd_ env</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td></tr><tr><td>aux !ud' ce</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td></tr><tr><td>trail _typ e</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td></tr><tr><td>trail _val ue</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td></tr><tr><td>trail Ids- ead</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td></tr></table></body></html>  

单类型，仍需对 price 传参，price 可以传入任意值。  

# #Q10：对于改单接口，修改订单时，各订单类型对应的必传参数  

A:   


<html><body><table><tr><td rowspan="2">参数</td><td rowspan="2">限 价 单</td><td rowspan="2">市 价 单</td><td rowspan="2">竞 价 限 价 单</td><td rowspan="2">竞 价 市 价 单</td><td rowspan="2">绝 对 限 价 单</td><td rowspan="2">特 别 限 价 单</td><td rowspan="2">特 别 限 价 且 要 求 全 部 成 交 订 单</td><td rowspan="2">止 损 市 价 单</td><td rowspan="2">止 损 限 价 单</td><td rowspan="2"></td><td rowspan="2">触 及 限 价 单 ( 止 盈</td><td rowspan="2">跟 踪 止 损 市 价 单</td><td rowspan="2">跟 踪 止 损 限 价 单</td></tr><tr><td>触 及 市 价 单 （ 止 盈</td></tr><tr><td>modi fy_or der_o p</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td></tr><tr><td>order _id</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td></tr><tr><td>price</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td></tr><tr><td>qty</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td></tr><tr><td>trd_e nv</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td></tr><tr><td>aux_ price</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td></tr></table></body></html>  

<html><body><table><tr><td>trail_t ype</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td></tr><tr><td>trail_ value</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td></tr><tr><td>trail. sprea d</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td></tr></table></body></html>  

Python 用户 注意，modify_order 并未对 price 设置默认值，对于上述五类订单类型，仍需对 price 传参，price 可以传入任意值。  

#Q11：交易接口返回“当前证券业务账户尚未同意免责协议”？  

A：点击下方链接完成协议确认，重启 OpenD 即可正常使用交易功能。  

<html><body><table><tr><td>所属券商</td><td>协议确认</td></tr><tr><td>FUTU HK</td><td>点击这里</td></tr><tr><td>Moomoo US</td><td>点击这里</td></tr><tr><td>Moomoo SG</td><td>点击这里</td></tr><tr><td>MoomooAU</td><td>点击这里</td></tr></table></body></html>  

# #Q12：典型日内交易者 （PDT）相关  

# #概述  

客户使用moomoo 证券(美国) 账户进行日内交易时，会受到美国 FINRA 的监管限制（此为美国券商受到的监管要求，与交易股票的所属市场无关。其他国家或地区的券商  

![](FutuAPI/eace56be28bedf07a6543889207f4cd5dbe0e3ac7dc5224f9d180a17e70cb6c5.jpg)  

的交易账户则不受此限制）。若用户在任意连续的5 个交易日内，进行日内交易 3 次以上，则会被标记为典型日内交易者（PDT）。  
更多详情，点击这里  

#进行日内交易的流程图  

![](FutuAPI/1f138b7a2b0bd818adece6c6791fef232bb08f5e9478f0ce369517d0a08d074d.jpg)  

# #我愿意被标记为 PDT，且不希望程式交易被打断，如何关闭“防止被标记为 PDT”？  

# A：  

当您在连续的 5 个交易日内，进行第 4 次日内交易时，为了防止您被无意识地标记为 PDT，服务器会对此交易进行拦截。若您主动想被标记为 PDT，并且不希望服务器拦截，可以采取以下措施：  

在 命令行 OpenD 中配置参数，将启动参数 pdt_protection 的值修改为  

0，以关闭“防止被标记为日内交易者”的功能。  

<!-- FUTU US 专用参数 -->  
<!-- Specific parameters for FUTu Us  
<!-- 是否开启防止被标记为日内交易者的功能，0：否，1：是<！--开启功能后，我们会在您将要被标记 PDT 时阻止您的下单， 但不确保您一定不被标记。若您被标记 PDT，当您的账户权益小于\$25000时，您将无法开仓。--><!-- Whether to turn on the Pattern Day Trade Protection, O: No, l: Yes --><!-- When this ameter is set as l, we will prevent you from placing orders which might mark you as a Pattern Day Trader(PDT). The Protection c<pdt_protection/pdt protection>  

注意：若您被标记 PDT，当您的账户权益小于 $\mathbb{S}25000$ 时，您将无法开仓。  

# #如何关闭 DTCall 预警提醒？  

# A：  

您被标记为 PDT 后，需要留意账户的日内交易购买力（DTBP），日内交易超出 DTBP 时将收到日内交易保证金追缴（DTCall）。服务器会在您即将开仓下单超出剩余日内交易购买力前，阻止您的下单。若您仍然希望进行下单，并且不希望服务器拦截，可以采取以下措施：  
在 命令行 OpenD 中配置参数，将启动参数 dtcall_confirmation 的值修改为 0，以关闭“日内交易保证金追缴预警”的功能。<!--是否开启日内交易保证金追缴预警的功能，0：否，1：是-->  
<!--并启功能后，我们会在您即将开仓下单超出剩余日内交易购买力前阻止您的下单。提醒您当前开仓订单的市值大于您的剩余日内交易购买力，若您在今日平仓当前标的，<!-- Whether to turn on the Day-Trading Call Warning, O: No, 1: Yes --)  
eventmlehmtdydaadiy注意：若您开仓订单的市值大于您的剩余日内交易购买力，并且在今日平仓当前标的，您将会收到日内交易保证金追缴通知（Day-Trading Call），只能通过存入资金才能解除。  

# #如何查看 DTBP 的值？  

A：  

通过 查询账户资金 接口，可以获取日内交易相关的返回值，如：剩余日内交易次数、初始日内交易购买力、剩余日内交易购买力等。  

# #Q13：如何跟踪订单成交状态  

A: 下单后，可使用以下接口跟踪订单成交状态：  

<html><body><table><tr><td>交易环境</td><td>接口</td></tr><tr><td>真实交易</td><td>响应订单推送回调，响应成交推送回调</td></tr><tr><td>模拟交易</td><td>响应订单推送回调</td></tr></table></body></html>  

注意：对于非 python 语言用户，在使用上述两个接口之前，需要先进行 订阅交易推送  

# #响应订单推送回调 的特点：  

反馈 整个订单 的信息变动。当以下 8 个字段发生变化时，会触发订单推送：  

订单状态，订单价格，订单数量，成交数量，触发价格，跟踪类型，跟踪金额/百分比，指定价差  

因此，当您进行下单、改单，撤单、使生效、使失效操作，或者订单在市场中发生了高级订单被触发、有成交变动的情况，都会触发订单推送。您只需要调用 响应成交推送回调，即可监听这些信息。  

# #响应成交推送回调 的特点：  

只反馈 单笔成交 的信息。当以下 1 个字段发生变化时，会触发订单推送：  

成交状态  

举例：假设一笔限价单订单 900 股，分成了 3 次才完全成交，每次成交分别是：200、300、400 股。  

![](FutuAPI/97fcfaa8af4b4b4ae0840e777be84878dc5aa7ba49748a345c5ce8d2cc8f7d8b.jpg)  

# #Q14：下单接口返回“订单价格不在价位上”？  

A:对于不同市场的标的，交易所有着不同的最小变动单位要求。如果提交的订单价格不符合要求，订单将会被拒绝。各市场价位规则如下：  

# #价位规则  

# #香港市场  

以港交所官方说明为准，点击 这里。  

# #A 股市场  

股票价位：0.01。  

# #美国市场  

股票价位：  

<html><body><table><tr><td>合约价格</td><td>价位</td></tr><tr><td>$1L 以下</td><td>$0.0001</td></tr><tr><td>$1L 以上</td><td>$0.01</td></tr></table></body></html>  

期权价位：  

<html><body><table><tr><td>合约价格</td><td>价位</td></tr><tr><td>$0.10 0 - $3.00</td><td>$0.01 或者$0.05</td></tr><tr><td>$3.00 以上</td><td>$0.05 或者$0.10</td></tr></table></body></html>  

期货价位：不同合约价位规则不同。可以通过 获取期货合约资料 接口的返回字  

# 段 最小变动的单位 查看。  

# #怎么避免订单价格不在价位上？  

方法一：通过 获取实时摆盘 接口，获取合法的交易价格。交易所摆盘上的价位一定是合法的价位。  

方法二：通过 下单 接口的参数 价格微调幅度，将传入价格自动调整到合法的交易价格上。  

例如：假设腾讯控股当前市价为 359.600，根据价位规则，对应的最小变动价位为 0.200。  

假设您的下单传入订单价格为 359.678，价格微调幅度为 0.0015，代表接受 OpenD 对传入价格自动向上调整到最近的合法价位，且不能超过$0.15\%$ 。此情景下，向上最近的合法价格为 359.800，价格实际需要调整的幅度为 $0.034\%$ ，符合价格微调幅度的要求，因此最终提交的订单价格为 359.800。  

若价格微调幅度设置数值小于实际需要调整的幅度，OpenD 自动调整价位失败，订单仍会返回报错“订单价格不在价位上”。  

# #Q15：我的购买力足够，为什么下市价单会返回“购买力不足”？  

A：  

# #为什么市价单会提示购买力不足  

出于风控考量，系统给了市价单较高的购买力系数。在所有订单参数都相同的情况下，选择市价单会比限价单占用更多的购买力。  

而且对于不同的品种，和不同的市场情况，风控系统会对市价单的购买力系数做动态调整。所以在下市价单时，若您通过最大购买力去计算最大可买数量，计算的结果很可能是不准确的。  

# #如何计算正确的可买数量  

不建议自己计算，您可以通过 查询最大可买可卖 接口获取正确的可买数量。  

# #如何尽可能买更多  

您可以用价格为对价的限价单，替代市价单进行交易。其中，对价：买1 价（下卖单时）或 卖1 价（下买单时）  

# 其他  

# #Q1：如何编译 $\mathsf{C}\!+\!+\!\;\mathsf{A}\!\mathsf{P}\!\mid\!\?$  

A: futu api $C++\ S D K$ 支持Windows/MacOS/Linux，每个系统提供了以下编译环境生成的库文件：  

<html><body><table><tr><td>操作系统</td><td>编译工具</td></tr><tr><td>Windows</td><td>Visual Studio 2013</td></tr></table></body></html>  

<html><body><table><tr><td>操作系统</td><td>编译工具</td></tr><tr><td>Centos 7</td><td>g++ 4.8.5</td></tr><tr><td>Ubuntu 16.04</td><td>g++ 5.4.0</td></tr><tr><td>MacOS</td><td>XCode 11</td></tr></table></body></html>  

如果编译器版本不同，或依赖的protobuf 版本不同，则可能需要自己使用源码重新编译FTAPI 和protobuf，源码位置见下图目录：  

FTAPI 目录结构：  

存放各个系统默认编译环境编译出的依赖库  

+---FTAPI FTAPI 源码+---protobuf-all-3.5.1.tar.gz protobuf 源码Copied!  

![](FutuAPI/e44465c7f48dad22e0bd064c2415c35de9a7728b6d3d9dae7baff865e030b205.jpg)  

# #编译步骤：  

1. 重新编译protobuf：生成libprotobuf 静态库  

2. 从协议proto 文件中生成 $C++$ 文件  

3. 重新编译FTAPI: 源码在Src/FTAPI，生成libFTAPI 静态库#步骤1： 重新编译protobuf：  

Windows：  

打开VS 命令行工具，cd 到protobuf/cmake 目录  
执行：cmake -G "Visual Studio 12 2019" -  
DCMAKE_INSTALL_PREFIX $=$ install -  
Dprotobuf_BUILD_TESTS=OFF  这样会生成Visual Studio 2019 的  
项目文件，其它版本Visual Studio 请修改-G 参数  
打开生成的Visual Studio 项目文件，平台工具集设置为  
v120_xp，编译即可  

Linux（参考protobuf/src/README）  

执行 ./autogen.sh  
执行 CXXFLAGS="-std $=$ gnu++11" ./configure --disable-shared  
执行 make  
将生成的libprotobuf.a 放入Bin/Linux 目录  

MacOS（参考protobuf/src/README）  

使用brew 安装这些依赖库：autoconf automake libtool执行./configure ${\mathsf{C}}{\mathsf{C}}{=}$ clang CXX $=$ "clang++ -std $=$ gnu++11 -stdlib $=$ libc++" --disable-shared  

# #步骤2: 重新生成proto 代码  

上面编译Protobuf 后会同时生成可执行文件protoc。用protoc 将Include/Proto 下面的.proto 文件生成对应的.h 和.cc 文件。例如命令以  

下命令会从Common.proto 生成对应的Common.pb.h 和Common.pb.cc  

protoc -I="FTAPI 路径/Include/Proto" --cpp_out $\c=1$ "." FTAPI 路径 /Include/Proto/Common.proto  

将生成的.h 和.cc 文件放到Include/Proto 下面  

# #步骤3: 重新编译FTAPI  

Windows：新建Visual Studio $C++$ 静态库工程，将Src/FTAPI 和Include下的源码加入工程中，平台工具集设置为v120_xp，然后编译  

Mac：新建XCode $C++$ 静态库工程，将Src/FTAPI 和Include 下的源码加入工程中，然后编译  

Linux：使用CMake 编译FTAPI 静态库，在FTAPI 路径/Src 目录下执  
行：cmake -DTARGET_OS $=$ Linux  

# #Q2：有没有更完整的策略样例可以参考？  

A:  

Python 策略样例在 /futu/examples/ 文件夹下。您可以通过执行如下命令，找到 Python API 的安装路径：  

import futu print(futu.__file__)  

Copied!  

C# 策略样例在 /FTAPI4NET/Sample/ 文件夹下Java 策略样例在 /FTAPI4J/sample/ 文件夹下$C++$ 策略样例在 /FTAPI4CPP/Sample/ 文件夹下JavaScript 策略样例在 /FTAPI4JS/sample/ 文件夹下  

# #Q3：使用 python API 导入异常  

A：  

场景一：已经在 Python 环境中安装了 futu 模块，仍然提示 No modulenamed 'futu'？  

很可能是因为当前 IDE 所使用的 interpreter 并不是你装过 futu 模块的interpreter。也就是说，您的电脑可能装了两个以上的 Python 环境。 您可以操作如下两步：  

1. 在 Python 中运行如下代码，得到当前 interpreter 的路径：  

import sys print(sys.executable)  

Copied!  

2. 在命令行中，执行 $\oint$ D:\software\anaconda3\python.exe -m pipinstall futu-api（其中前半部分的文件路径来自第 1 步打印的路径）。 这样就可以在当前的 interpreter 中也安装一份 futu 模块。  

# #Q4： import 成功了，仍然调用不了相关接口？  

A：通常遇到这种情况，需要确认一下：成功导入的 futu，是不是真正的 FutuAPI 模块。以下几种场景也可能 import 成功。  

场景一：存在与“futu”重名的文件  

1. 当前文件名是 futu.py  
2. 当前文件所在目录下存在另一个名为 futu.py 的文件  
3. 当前文件所在目录下存在名为 /futu 的文件夹  

因此，我们强烈建议您，在给文件 / 文件夹 / 工程起名的时候，不要起名叫“futu”。重名一时爽，查 bug 两行泪。  

场景二：误装了一个名为“futu”的第三方库  

Futu API 的正确名称为futu-api，而非“futu”。  

如果您安装过名为“futu”的第三方库，请将其卸载，并 下载 futu-api。  

以 PyCharm 为例：查看第三方库的安装情况。  

![](FutuAPI/0153b36ecf984a57c568b7181eac6d99f8db8c81ef14c388fdffb1783a1d2b6b.jpg)  

![](FutuAPI/db7f95ea92bfc46248526e4b1262ed5a14dd4aba918f1842950ab55afa2e4709.jpg)  

# #Q5：协议加密相关  

A：  

您可以使用非对称加密算法 RSA，对策略程序（Futu API）与 OpenD 之间的请求和返回内容进行加密，以保证通信安全。  

如果您的策略程序（Futu API）与 FutuOpenD 在同一台电脑上，则通常无需加密。  

# #协议加密流程  

您可以尝试通过以下步骤解决此问题：  

1. 通过第三方 web 平台自动生成密钥文件。  

o  具体方法：在 baidu 或 google 上搜索“RSA 在线生成”，密钥格式设置为 PKCS#1，密钥长度设置为 1024 bit，不需要设置私钥密码，点击生成密钥对。  

![](FutuAPI/7a9fe9b1f364fcc7b45e55628d10eed1072975d74bb6d64e9ffbfc723025f618.jpg)  

2. 将生成的 RSA 加密私钥 复制粘贴至 txt 记事本，并保存至 OpenD 所在电脑的指定路径。  

3. 在 OpenD 所在的电脑中，指定 RSA 加密私钥 的路径。  

o 方式一：在 可视化 OpenD 启动界面右侧的“加密私钥”一栏，指  

定上一步骤中放置 RSA 加密私钥 的路径。如下图所示：  

![](FutuAPI/75dc01e0bc3cf183cb90fdb7156d4cd5a57662d63aa30c1c9b1f42561a1eea50.jpg)  

o  方式二：在 命令行 OpenD 启动文件 OpenD.xml 中，找到参数  

rsa_private_key，将其配置为第 2 步中 RSA 加密私钥 的路  

# 径。如下图所示：  

![](FutuAPI/730f142b95c2251dcf1c38a5fdb043a14cdb13b9f526858b95a2268aabb96230.jpg)  

4. 将第 2 步中 txt 文件另存至策略程序（Futu API）所在电脑的指定路径， 并在策略程序中将此路径 设置为私钥路径。  

5. 在策略程序（Futu API）中启用协议加密。 启用协议加密的方式有两种，其中方式二的优先级更高。  

o 方式一：对单条的连接加密（通用）。在对 行情对象 或 交易对象 创建连接时，通过 是否启用加密 参数设置加密。  
o 方式二：对所有的连接加密（仅 Python）。通过enable_proto_encrypt 接口设置加密，详见 这里。  

# 提示  

在 OpenD 或策略程序（Futu API）中指定 RSA 加密私钥 路径时，需指定至 txt 文件本身。  

RSA 加密公钥无需保存，可通过私钥计算得到。  

# #Q6：为什么我获取的 DataFrame 数据，只能展示一部分 ？  

A：打印 pandas.DataFrame 数据的时候，如果行列数过多，pandas 默认会将数据折叠，导致看起来显示不全。  
因此，并不是接口返回数据真的不全。您只需要在 Python 脚本前面加上如下代码即可解决。  

import pandas as pd pd.options.display.max_rows $=$ 5000 pd.options.display.max_columns $=$ 5000 pd.options.display.width $=1600$  

Copied!  

#Q7：Mac 机器使用 $\mathbf{\check{C}++}$ 语言的 API，遇到 “无法打开 libFTAPIChannel.dylib” 的问题  

A：在对应库目录中执行以下命令即可解决:\$ xattr -r -dcom.apple.quarantine libFTAPIChannel.dylib。  

#Q8：Python 用户，为什么在 OpenD 配置文件中设置了日志级别为 no 后，log 文件夹下仍然持续产生超大容量的日志文件？  

A：OpenD 配置文件中的日志级别参数，只用来控制 OpenD 产生的日志。而Python API 默认也会产生日志，如果您不希望希望 Python API 产生日志，可以在 Python 脚本加上如下语句：  

logger.file_level $=$ logging.FATAL  # 用于关闭 Python API 日志 logger.console_level $=$ logging.FATAL  # 用于关闭 Python 运行时的控制台日志 Copied!  

#Q9：对于 5.4 及以上的版本，Java API 的库名和配置方式的变更  

A: \* 如果您是 Java API 5.3 及以下版本的用户，在更新版本时，请注意以下变更：  

# 配置流程的变更：  

1. 通过 富途牛牛官网下载 Futu API。  

2. 解压下载好的 FTAPI 文件，/FTAPI4J 是 Java API 的目录，将目录结构中的 /lib/futu-api-.x.y.z.jar 添加到您的工程设置中。创建futu-api 工程请参考 这里。  

目录结构的变更：  

1. Futu API 的 Java 版本，库名由之前的 ftapi4j.jar 变更为 futu-api-x.y.z.jar，其中 “x.y.z” 表示版本号。  

2. 第三方库的引用中，去掉了 /lib/jna.jar 和 /lib/jna-platform.jar 依赖，增加了 /lib/bcprov-jdk15on-1.68.jar 和 /lib/bcpkix-jdk15on-1.68.jar 依赖。  

+---ftapi4j futu-api 源码，如果所用 JDK 版本不兼容可以用这  
里的工程重新编译出 futu-api.jar  
+---lib 存放公共库文件  
| futu-api-x.y.z.jar Futu API 的 Java 版本  
| bcprov-jdk15on-1.68.jar 第三方库，用于加解密  
| bcpkix-jdk15on-1.68.jar 第三方库，用于加解密  
| protobuf-java-3.5.1.jar 第三方库，用于解析 protobuf 数据  
+---sample 示例工程  
+---resources maven 工程默认生成的目录  

Copied!  

如果您第一次接触 Futu API，我们提供了更便捷的通过 maven 仓库配置 Java API 的方式。配置流程请参考 这里。  

# #Q10：Python 用户，使用 pyinstaller 打包脚本时报错：找不到 Common_pb2 模块  

A：你可以尝试通过以下步骤解决此问题：  

1. 假设你需要对 main.py 进行打包。使用命令行语句，运行代码：pyinstaller main.py，不要加参数 “- F”（path 为 main.py 的所在路径）  

Copied!  

打包成功后，main.py 所在目录下的 /dist 中，会生成 /main 文件夹，  

main.exe 就在这个文件夹中。  

![](FutuAPI/8c4c8c2c783e0662eb901f39785d3be4dee61cef7033d275d3c0b3c76848cd42.jpg)  

2. 运行以下代码，找到 futu-api 的安装目录。  

import futu print(futu.__file__)  

Copied!  

# 运行结果:  

C:\Users\ceciliali\Anaconda3\lib\site-packages\futu\__init__.py  

Copied!  

![](FutuAPI/a2c458c38745cea337a7c20ed8dc9f160b3116e0598a5f32bbbece5b0323d121.jpg)  

3. 打开上图文件夹中的 /common/pb，将所有文件全部复制到 /main 中。  

4. 在 /main 中创建文件夹，命名为 futu，将上图文件夹中  

的 VERSION.txt 文件复制到 /main/futu 中。  

![](FutuAPI/c7f48eb2d8e0fd0c0e543d3d91d178702b9170fbf2d0b005000f42d413238875.jpg)  
5. 再次尝试运行 main.exe  

# #Q11：接口调用结果正常，但其返回表现不符合预期？  

# A:  

接口调用结果正常，表示富途已经成功收到并响应了您的请求，但接口返回表现可能与您的预期不符。  

例如：若您在非交易时段调用 订阅 接口，虽然您的请求可以被成功响应，并且接口调用结果正常，但在非交易时段下，交易所无行情数据变动，所以您将暂时无法收到行情数据推送，直至市场重新回到交易时段。  

接口调用结果可以通过返回字段（定义参见：接口调用结果）查看，返  
回字段为 0 代表接口调用正常，非 0 代表接口调用失败。  
对于 Python 用户，下面两种写法等价：  
if ret_code $==$ RET_OK:Copied!1  
if ret_code $\mathbf{\mu}=\mathbf{\mu}\circ\mathbf{\Sigma}$ :Copied!  

# #Q12：WebSocket 相关  

A：  

# #概述  

OpenAPI 中，WebSocket 主要用于以下两方面：  

可视化 OpenD 中，UI 界面跟底层的命令行 OpenD 的通信使用WebSocket 方式。  

JavaScript API 跟 OpenD 之间的通信使用 WebSocket 方式。  

![](FutuAPI/e2314be2408ba4c5a83538bc1433832bd90640357643ccd38631da055cb04507.jpg)  

当 WebSocket 启动时，命令行 OpenD 会与 FTWebSocket 中转服务 建立 Socket 连接（TCP），这一连接会用到默认的 监听地址 和 API协议监听端口。同时，JavaScript API 会与 FTWebSocket 中转服务 建立 WebSocket连接（HTTP），这一连接会用到 WebSocket 监听地址 和 WebSocket  
端口。  

# #使用  

为保证账户安全，当 WebSocket 监听来自非本地请求时，我们强烈建议您启用 SSL 并配置 WebSocket 鉴权密钥。  

SSL 通过在配置 WebSocket 证书 以及 WebSocket 私钥 来启用。  

命令行 OpenD 可通过配置 OpenD.xml 或配置命令行参数来设置文件路径。  
可视化 OpenD 点击【更多选项】下拉菜单，可以看到设置项。  

![](FutuAPI/a890760f7b34ec6a8c46bf67d8c91e9418d0ee958fc0d21418d02547ff45acbb.jpg)  

# 提示  

如果证书是自签的，则需要在调用 JavaScript 接口所在机器上安装该证书，或者设置不验证证书。  

# #生成自签证书  

自签证书生成详细资料不便在此文档展开，请自行查阅。在此提供较简单可用的生成步骤：  

1. 安装 openssl。  

2. 修改 openssl.cnf，在 alt_names 节点下加上 OpenD 所在机器 IP 地址或域名。例如： $\vert\mathsf{P}.2=$ xxx.xxx.xxx.xxx, DNS.2 $=$ www.xxx.com  
3. 生成私钥以及证书（PEM）。  

证书生成参数参考如下：  

openssl req -x509 -newkey rsa:2048 -out futu.cer -outform PEM -keyout futu.key -days 10000 -verbose -config openssl.cnf -  

nodes -sha256 -subj "/CN=Futu CA" -reqexts v3_req -extensions v3_req  

# 提示  

openssl.cnf 需要放到系统路径下，或在生成参数中指定绝对路径。  

注意生成私钥需要指定不设置密码（-nodes）  

附上本地自签证书以及生成证书的配置文件供测试：  

openssl.cnf futu.cer futu.key  

# #Q13：OpenAPI 的行情和交易服务分别部署在哪里？  

A：  

行情：  


<html><body><table><tr><td>平台账号</td><td>行情服务器所在地</td></tr><tr><td>牛牛号</td><td>腾讯云广州和香港</td></tr><tr><td>号 moomoo</td><td>腾讯云美国弗吉尼亚和新加坡</td></tr></table></body></html>  

交易：  

<html><body><table><tr><td>所属券商</td><td>交易服务器所在地</td></tr><tr><td>富途证券(香港)</td><td>香港</td></tr></table></body></html>  

<html><body><table><tr><td>所属券商</td><td>交易服务器所在地</td></tr><tr><td>moomoo证券(美国)</td><td>腾讯云美国弗吉尼亚</td></tr><tr><td>moomoo证券(新加坡)</td><td>腾讯云新加坡</td></tr><tr><td>moomoo 证券(澳大利亚)</td><td>AWS 澳大利亚悉尼</td></tr></table></body></html>  

# #Q14：关于综合账户升级的过渡指引  

# #1. 综合账户升级  

综合账户支持以多种货币在同一个账户内交易不同市场品类。从单币种账户升级到综合账户，是在您原来的牛牛号下，进行账户迁移。主要包括：  

创建新的综合账户  
将您原来单币种业务账户里的资产，转移到综合账户里  
关闭原来的单币种账户  

# #2. OpenD 版本升级  

我们会在 9 月14 日、15 日 集中为 OpenAPI 客户的账户做升级，请提前检查OpenD 和 API 版本号：  

# 7.01 及以下版本  

OpenD 因版本过旧，将于 9/14 停止服务。届时，已登录的账户会被强制退出登录。我们建议您在 9/14 之前升级 OpenD 和 API 至最新版本，且不要在 9/14\~9/15 期间跨周末运行策略。  

# $7.02\sim8.2\$ 版本  

OpenD 版本较旧，无法获取综合账户。我们建议您在 9/14 之前升  

级 OpenD 和 API 至最新版本，且不要在 9/14\~9/15 期间跨周末运行策略。  

8.3 及以上版本  

可以正常使用，我们建议您不要在 9/14\~9/15 期间跨周末运行策略。  

综合账户升级时，您的资产会转移到新的综合账户，如果策略指定旧的账户，可能会运行异常。同时，在实盘交易之前，建议您进行必要的检查与测试，确保一切设置正常。  

# #3. 账户升级后，OpenAPI 有哪些表现？  

Python API 将不再支持使用 OpenHKTradeContext,  
OpenUSTradeContext, OpenHKCCTradeContext, OpenCNTradeContext创建交易对象，请参考 创建交易对象连接 改用  
OpenSecTradeContext。  
非Python API 用户，在使用 Trd_GetAccList 接口时，需要将  
needGeneralSecAccount 参数设为 true，才能获取到综合账户的相关信息。  
账户新增 账户状态: 在使用 获取交易业务账户列表 时，返回结果新增了账户状态 。综合账户标记为 ACTIVE 生效账户，被停用的单币种账户标记为 DISABLED 失效账户。  

下单、改单撤单、查询最大可买可卖 等交易接口表现o  支持使用 ACTIVE 生效账户所对应的 acc_id 或acc_index 进行购买力查询与交易。不支持使用 DISABLED 失效账户所对应的 acc_id 或acc_index 进行购买力查询与交易，若使用，将会出现报错信息。Python API 用户：在接口入参中，请指定 acc_id 为升级后的综合账户。  

非Python API 用户：在 TrdHeader 中，请指定accID 为升级后的综合账户。  