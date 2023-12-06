

## 如何部署

1. 下载最新的二进制文件，目录下有3个文件，`tronbot` 、  `.env.example`  `config.yaml` 
2. 命令行执行 `mv .env.example .env`，修改 `.env.example` 的名字为 `.env`
3. config.yaml 文件不用动。
4. 根据 `.env ` 内的备注，修改相关参数，非必填的可不写。

		# 店铺名称
		SHOP_NAME="TRX自助兑币机"
		# TRC20地址
		add=TXTnkc4giLRKwGKtmPxC2dru3NBD5xxxxx
		# TRC20地址私钥, 可不填，不填USDT兑换TRX无法实现
		PrivateKey=8cd604b6919af1f61cdf5964cd591c78b18c9435300d646105e8488dxxxxx
		# 波场APIKEY地址, 去 https://www.trongrid.io/ 申请 (可不填, 影响不大)
		TRON_APIKEY=xxx
		# 管理员 telegram ID 用于接收账户变动通知
		uid=63332812122
		# 群组ID, 用于向群里发送交易通知  注意群ID都是以 - 开头
		gid=-4073121212
		# TG 机器人Token
		TG_TOKEN=6182447226:AAGD3BDe6PYxo0EXTYjj65sHxxxxxxx
		# 能量租赁时长默认 1个小时 60分钟 不要动
		lockTime=60
		# 兑换TRX利润率默认8%  如果你想赚8个点,就写0.08, 赚10个点,就写0.1
		trxRate=0.08
		# 能量单价  32000能量需要多少TRX, 默认2.0TRX 32000, 自行定价, 目前成本2.0
		energyUnit=2.0
		# TRX兑换/能量租赁欢迎语,底部挂载按钮文字及链接,格式如下, | 必须带
		linkButton=联系客服|https://t.me/自己的TG用户名
		# 调用能量发送的APIKEY  去 https://t.me/XXTrxBot 申请
		DAPI_KEY=XXXX-XXXX-XXXX-XXXX


 ⚠️注意：配置文件里面不认识的不要修改，留空即可

1. 给予`tronbot`可执行权限，命令行输入`chmod +x tronbot`
2. 启动命令 `./tronbot` 
3. 到这一步就算是正式启动了，但是无法后台运行，你关掉终端，程序就停了，为了保证程序持续运行，请看第4步。
4. 配置supervisor (不太熟悉下面流程的建议使用宝塔，搜索supervisor管理器，添加路径/root/tron，可执行文件填写/root/tron/tronbot即可，这里的`/root/tron/tronbot`不要照抄，根据你的可执行文件的位置来)
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
