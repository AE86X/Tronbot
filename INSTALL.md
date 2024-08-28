
## 写在前面

* 机器人免费使用，并未开源，基础功能完整，能覆盖现有业务需求，**不接受定制/修改等需求**，如介意，请关闭此页面。
* 部署请仔细查看教程，自己不了解或不懂的，请使用 [Google](https://google.com) 来解决您的问题。




## 如何部署

1. 先下载 `tronbot.tar.gz`，下载完成后，文件夹内仅依赖2个文件，`tronbot` 和`config.yaml` 
2. `tronbot` 为启动文件，无需关注。`config.yaml`  为配置文件，所有配置信息在此文件内填写，请认真阅读下方内容。
3. 有必填字样的必须填写，其他可选填。

		
		# 机器人token，@botfather 申请。（必填）
		TGBotToken: 6182447221:AAGD3BDe6PYxo0EXTYjj65sHDbjfsy9HGOY
		# 管理员UID（必填）
		TGUserID: 520921928
		# 波场APIKEY地址, 去 https://www.trongrid.io/ 申请 (可不填, 防止请求限制, 最好去申请下)
		TRONApiKey: xxxx-xx-xx-xx-xx
		# https://t.me/XXTrxBot 查看ApiKey，用于能量发送（必填）
		XBotApiKey: 9396B64F-14A5-3829-A63D-AX
		# 点击联系客服回复内容（必填）
		Contact: "客服 @BotFather"
		
		# 下方填写托管转租地址，不限制数量，可无限添加，每个-后可以看成一块，复制往后追加即可
		Values:
		  - trx_own: "TXYqcWRnNP1bGsa9tzjsEJiKAYwMRonoMv" #收TRX地址（必填）
		    price: 3.5	#32000能量定价（必填）
		    max: 10	#最高翻倍数，如转入35TRX，发送32W能量（必填）
		    auto_price: 6.5	#笔数单价，（不开通笔数直接删除该字段）
		    auto_values: "10,20,30,50,100,200,300,500"	#笔数下单按钮，可显示XX笔，（不开通笔数可删除该字段）
		    usdt_own: "TXYqcWRnNP1bGsa9tzjsEJiKAYwMRonoMv"  # USDT兑换TRX功能的收U地址（不开通可删除此字段）
		    profit: 0.1	# 按照交易所汇率下浮点位，如：8个点填写0.08，15个点填写0.15。如需固定汇率请直接填写数值，1U换7TRX，直接填写7即可（不建议）
		    trx_from: "TXYqcWRnNP1bGsa9tzjsEJiKAYwMRonwMv"	# 兑换TRX出TRX的地址，该地址请保留足够的TRX，否则发送不成功（不开通可删除此字段）
		    trx_pk: "d66182f1bfe2b6b3a32a231f0cf1e748f1336513150cc9d718383343bab81111"	#兑换TRX出TRX的地址的私钥，不正确则发送不成功（不开通可删除此字段）
		    bot_btn: "按钮一|https://t.me,按钮二|https://t.me/botfather,按钮三|https://google.com,按钮四|https://google.com,按钮四|https://google.com" #机器人回复消息下方挂载的按钮，显示文字和跳转地址请使用 | 竖线符号分开，多个按钮请使用 , 逗号隔开。
		    bot_token: "6182447221:AAGD3BDe6PYxo0EXTYjj65sHDbjfsy9HGOY" #发送群通知的机器人token
		    group_btn: "按钮一|https://t.me,按钮二|https://t.me/botfather,按钮三|https://google.com" #群通知消息下方挂载的按钮，显示文字和跳转地址请使用 | 竖线符号分开，多个按钮请使用 , 英文逗号隔开。
		    group_id: "-4073190212,-4073190212,-4073190212" # 通知到到哪些群/频道，多个请使用, 英文逗号隔开
		    
		  - trx_own: "TTnvWwCA7Mw5U1P66Y4tpB3QaUTwxssSSS" 
		    price: 1.5
		    max: 10
		    auto_price: 3.5
		    auto_values: "10,20,30,50,100,200,300,500"
		    usdt_own: "TTnvWwCA7Mw5U1P66Y4tpB3QaUTwxssSSS"
		    profit: 0.1
		    trx_from: "TTnvWwCA7Mw5U1P66Y4tpB3QaUTwxssSSS"
		    trx_pk: "d66182f1bfe2b6b3a32a231f0cf1e748f1336513150cc9d718383343bab81111"
		    bot_btn: "按钮一|https://t.me,按钮二|https://t.me/botfather,按钮三|https://google.com"
		    bot_token: "6182447221:AAGD3BDe6PYxo0EXTYjj65sHDbjfsy9HGOY"
		    group_btn: "按钮一|https://t.me,按钮二|https://t.me/botfather,按钮三|https://google.com"
		    group_id: "-4073190212,-4073190212,-4073190212"


 ⚠️注意：配置文件内必填项必须填写，其他可直接删除。
 
 
1. 给予`tronbot`可执行权限，命令行输入`chmod +x tronbot`
2. 启动命令 `./tronbot` 
3. 到这一步就算是正式启动了，但是无法后台运行，关掉终端，程序就停了，为了保证程序持续运行，请看第7步。
4. 配置supervisor (不太熟悉下面流程的建议使用宝塔，搜索supervisor管理器，运行目录`/root/tronbot`，执行命令填写`/root/tronbot/tronbot`即可，这里的`/root/tronbot/tronbot`不要照抄，根据你的可执行文件的位置来)
5. 如果你使用宝塔配置成功，就无需往下看了，如果不用宝塔，请看第9步。
6. 为了保证`tronbot`常驻后台运行，我们需要配置`supervisor`来实现进程监听，安装supervisor `apt install supervisor`，安装完成进入 `/etc/supervisor/conf.d/` ，文件夹编辑配置文件， `vi /etc/supervisor/conf.d/tronbot.conf`

可参考以下配置文件，注意更改路径，编辑完记得保存。

	[program:bot]
	process_name=bot
	directory=/root/tronbot
	command=/root/tronbot/tronbot
	autostart=true
	autorestart=true
	user=root
	numprocs=1
	redirect_stderr=true
	startsecs=3


* 接下来输入命令 `supervisorctl update` 不报错即执行成功

* 查看运行状态 `supervisorctl status` 显示 RUNNING 即正在运行


#### 其他注意事项
* `.config.yaml`配置文件修改后务必重启supervisor进程后才会生效，重启命令 `supervisorctl restart bot` 
