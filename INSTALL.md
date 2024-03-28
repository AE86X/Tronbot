

## 如何部署

1. 下载最新的二进制文件，目录下有3个文件，`tronbot` 、  `.env`  `config.yaml` 
3. config.yaml 文件不用动。
4. 根据 `.env ` 内的备注，修改相关参数，非必填的可不写。

		# 店铺名称
		SHOP_NAME="能量自动兑换"
		
		# TRC20地址，收TRX的地址
		add=TXTnkc4giLRKwGKtmPxC2dru3NBD5xxxxx
		
		
		# 波场APIKEY地址, 去 https://www.trongrid.io/ 申请 (可不填, 防止请求限制, 最好去申请下)
		TRON_APIKEY=cb6fxx
		# 管理员 telegram ID 用于接收账户变动通知
		uid=6028xxx
		# TG 机器人Token
		TG_TOKEN=5962152892:AAGIdZtUxxxxxx
		# 能量租赁时长默认 1个小时 60分钟 不要动
		lockTime=60
		# 兑换TRX利润率默认8%  如果你想赚8个点,就写0.08, 赚10个点,就写0.1
		trxRate=0.08
		# 能量单价  32000能量需要多少TRX, 默认2.5TRX 32000, 自行定价
		energyUnit=2.5
		# 最高翻倍数, 定价2.5 设置20倍，转进去50TRX, 自动回32000*20=640000能量，转进去51及以上，不触发能量发送
		MAX=20
		# TRX兑换/能量租赁/笔数欢迎语,底部挂载按钮文字及链接,格式如下, | 必须带
		linkButton=联系客服|https://t.me/xxxxx
		# 调用能量发送的APIKEY  去 https://t.me/XXTrxBot 申请
		DAPI_KEY=D7698E31xxxx
		
		
		
		# =============如果使用USDT兑换TRX, 请根据下方要求填写, 如不使用该功能, 忽略即可============
		# USDT兑换TRX的收U地址, 可与上方收TRX地址相同
		USDTADD=TXTnkc4giLRKwGKtmPxC2dru3NBD5xxxx
		# USDT兑换上方收U地址收到USDT后, 出TRX的地址(发起转账TRX)和私钥填写下方, 可与收TRX收USDT地址一样(不想麻烦3个地址填写同一个地址即可)
		USDTOWNER=TXTnkc4giLRKwGKtmPxC2dru3NBD5xxxx
		# 发起TRX转账地址的私钥，USDTOWNER地址对应的私钥
		PrivateKey=d66182f1bfe2b6b3a32a231f0cf1e748f1336513150cc9d71838334
		# =============如果使用USDT兑换TRX, 请根据上方要求填写, 如不使用该功能, 忽略即可============
		
		# !!!!!!!!!!!如您想使用USDT兑换功能不想从自己地址发起转账TRX, 可联系客服使用客服地址!!!!!!!!!!!
		
		
		# =============群组内通知，如果您不使用该功能，忽略下方=============
		# 群组ID, 用于向群里发送交易通知  注意群ID都是以 - 开头(可不填)
		gid=
		# 群组内通知，底部两个按钮支持挂载链接
		GroupLeftButton=群组通知下方左侧文字|https://t.me/BotFather
		GroupRightButton=群组通知下方右侧文字|https://t.me/BotFather
		# =============群组内通知，如果您不使用该功能，忽略上方=============
		
		
		# =============笔数模式，如果您不使用该功能，忽略下方=============
		# 笔数模式单笔定价, 如果设置>1即生效, 不使用笔数模式, 留空或把价格改为0
		AutoPrice=0
		# 最小购买多少笔, 该设置X笔数单价,务必大于小时单笔定价X最高翻倍数. 举例:小时单价2.5,最高翻20倍,那笔数的单价乘以最小购买笔数务必大于50,否则入账不能判定是购买笔数还是小时
		AutoMin=0
		# 最大购买笔数, 最高100, 填写小于或等于100即可 如果开启笔数订单, 配置好此参数, 比如你写了50, 那超过50*5.0=250TRX的入账, 不会兑换笔数. 自己地址资金调配务必大于该金额
		AutoMax=0
		# =============笔数模式，如果您不使用该功能，忽略上方=============


 ⚠️注意：配置文件里面不认识的不要修改，留空即可。
 
 ⚠️⚠️📢📢 **记得配置MAX最高翻倍数，入账的TRX超过最高翻倍数，不会发起能量兑换**
 
1. 给予`tronbot`可执行权限，命令行输入`chmod +x tronbot`
2. 启动命令 `./tronbot` 
3. 到这一步就算是正式启动了，但是无法后台运行，你关掉终端，程序就停了，为了保证程序持续运行，请看第4步。
4. 配置supervisor (不太熟悉下面流程的建议使用宝塔，搜索supervisor管理器，运行目录/root/tron，执行命令填写/root/tron/tronbot即可，这里的`/root/tron/tronbot`不要照抄，根据你的可执行文件的位置来)
5. 如果你使用宝塔配置成功，就无需往下看了，如果不用宝塔，请看第6步。
6. 为了保证`tronbot`常驻后台运行，我们需要配置`supervisor`来实现进程监听  (supervisor的安装，可参考[链接](https://learnku.com/laravel/t/3592/using-supervisor-to-manage-laravel-queue-processes))

`vi /etc/supervisor/conf.d/tronbot.conf`

你可以参考以下配置文件，注意更改路径，编辑完记得保存。

	[program:usdt]
	process_name=usdt
	directory=/root/tron
	command=/root/tron/tronbot
	autostart=true
	autorestart=true
	user=root
	numprocs=1
	redirect_stderr=true
	startsecs=3


接下来输入命令 `supervisorctl update` 不报错即执行成功

查看运行状态 `supervisorctl status` 显示 RUNNING 即正在运行


#### 其他注意事项
* 所有`.env`配置文件有了修改后都需要重启supervisor进程 `supervisorctl restart usdt `
