# Filter 顺序
1. "ApplicationFilterConfig[name=VisitorFilter, filterClass=com.asiainfo.cboss.web.common.filter.VisitorFilter]"
2. {ApplicationFilterConfig@9532} "ApplicationFilterConfig[name=MultipartFilter, filterClass=org.springframework.web.multipart.support.MultipartFilter]"
3. {ApplicationFilterConfig@9584} "ApplicationFilterConfig[name=CommonFilter, filterClass=com.asiainfo.cboss.web.common.filter.CommonFilter]"
4.  {ApplicationFilterConfig@9585} "ApplicationFilterConfig[name=ProtocolFilter, filterClass=com.asiainfo.cboss.web.common.filter.DetectProtocolFilter]" 检测报文下来是哪种协议
	1. 根据请求报文 Content-Type 判断
	2. 根据 url 
5.  {ApplicationFilterConfig@9586} "ApplicationFilterConfig[name=HeartBeatFilter, filterClass=com.asiainfo.cboss.web.common.filter.HeartBeatFilter]" 心跳检测
	1. SOAP 报文  请求方法为 Echo ,返回心跳报文
	2. GET 请求返回心跳检测
6. {ApplicationFilterConfig@9587} "ApplicationFilterConfig[name=DuplicateFilter, filterClass=com.asiainfo.cboss.web.common.filter.DuplicateFilter]" 多重下发交易过滤
	1. 需要连接数据库，高并发下，数据库链接吃紧，默认注释，不开启
7. {ApplicationFilterConfig@9588} "ApplicationFilterConfig[name=AllFaultFilter, filterClass=com.asiainfo.cboss.web.home.system.faultbarrier.allfault.AllFaultFilter]" 全业务容灾
	1. 静态变量 ALL_FAULT_FLAG (默认0)= 1，触发全容灾
	2. 通过 请求 容灾触发器 servelt 
		1. AllFaultTrigger
	3. 通过 Filter触发
		1. AllFaultConfigFilter
8. {ApplicationFilterConfig@9589} "ApplicationFilterConfig[name=KindFaultFilter, filterClass=com.asiainfo.cboss.web.home.system.faultbarrier.kindfault.KindFaultFilter]" 分业务容灾过滤器
	1. fault_barrier_code 表 根据 平台、bipcode、actcode 配置的code_type（配置1 容灾）来判断是否容灾
9.  {ApplicationFilterConfig@9590} "ApplicationFilterConfig[name=AntiDetectionFilter, filterClass=com.asiainfo.cboss.web.tolerance.AntiDetectionFilter]" 反集团探针
	1. 集团通过用户资料查询时填写5位的密码来进行探测,该Filter判断如果密码不是6位就直接返回密码错误2102
10.  {ApplicationFilterConfig@9591} "ApplicationFilterConfig[name=Tomcat WebSocket (JSR356) Filter, filterClass=org.apache.tomcat.websocket.server.WsFilter]"
