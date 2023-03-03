# 构建容灾报文
## 创建工厂类 
- START
	- START_FaultContextFactory
- N2N
	- N2N_FaultContextFactory
- SOAP
	- SOAP_FaultContextFactory

## 是否启用异常遮断（默认启用）
select * from cboss.cboss_base_code_hn where code_type = '20000' and code_id='00'
- 如果配置不启用遮断，记录监控日志（Cboss_System_Monitorlog_YYYYMM）并返回。

## Request中RESPONESE_COMMITED已经被提交
记录监控日志，MonitorType = 0

## 协议类型为STAR、N2N、SOAP和 JSONBUSI进行后续容灾处理
- 设置容灾报文构建器
	- STAR_SimulationResponseBuilderFacotry,N2N_SimulationResponseBuilderFacotry,SOAP_SimulationResponseBuilderFacotry,JSONBUSI_SimulationResponseBuilderFacotry
	- 业务逻辑：根据bipcode和actcode从Redis缓存获取遮断报文，并组装成Response，业务逻辑涉及到 一级返回码 和 二级返回码
		
- 设置容灾报文发送器
	- 应答报文是否加密 
		business_encryption表配置RSP_FLAG = 1 ，加密返回
 * 是否不走容灾判断
	 支持该时间段内所有的业务交易均不进入容灾模式处理，直接按照正常模式应答，即使超过日、月最大不走容灾笔数  。不容灾则直接拼装“2998 系统异常“返回
	 记录业务返回日志 HOME_BUSI_LOG
	 记录监控日志 CBOSS_SYSTEM_MONITORLOG。 monitorType=20 异常容灾-不遮断
