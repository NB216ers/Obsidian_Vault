
---
UID: 20230207141402
alias: []
Type: Write
Category:
tages: [""]
date: 2023-02-07 14:13
---
shell
# CBOSS
[[Pub/write]]
## 收集

### Cboss 一级云测试环境地址
cboss-web : http://10.218.34.85:30339
Cboss-route: http://10.218.34.86:30312

1. CBOSS 调用 CCSWEB 透传的 URL，在哪里n配置的？
select * from cboss. cboss_base_code t where t.code_type = 10017 and t.code_id like '%URL%
select * from cboss. cboss_response_config_hn EXT2 字段
CBOSS_BASE_CODE
CBOSS_RESPONSE_CONFIG
CBOSS_REQUEST_CONFIG


2. 配置脚本提交到了 SVN，一级云 CBOSS 库要执行的？
svn://10.97.85. 11:33 699/CHA/doc/05-上线/20220715/配置脚本/CBOSS 库/CBOSS@CBOSS_RESPONSE_CONFIG@一级云. sql

3. 签退、签到

T 模块的：
测试地址 http://10.248.50.122:1112/Trans/Receiver
生产地址 http://10.87.20.117:1100/Trans/Receiver
查看是否签退成功需要根据两个条件，一个是请求集团返回的结果，另一个是查询表数据，sql 如下：
select * from cboss. home_busi_log_202206 t where t.processtime > sysdate - 2/24/60 and bipcode like 'BIP%' ；  ---签到成功会有数据，签退成功无数据
统一支付的：
统一支付业务记录表：cboss. upss_plat_payed_detail，可以用 create_date 字段判断时间范围

4. 代码提交格式
@gaojian@202206271010@修改测试环境 ARG 格式
以后提交代码不管是 GIT 还是 SVN 都安这个格式来啊！！

5. 远程桌面
测试：117.158.199.2 46:20 120
	账号：zhangqin、liyu7、liming7
	密码：tech-1208


生产：192.168.1.179  liming7/3e4r #E $R


云桌面: wangyatao2/4rfv$RFV
4A: wangyatao2/4rfv$RFV
4A: yaoshaopeng/6yhn^YHN2023
4A: caowenhui/7u8i&U*I  -> 设备登录 -> 数据库 -> 资源名称输入“CBOSS” 可以登北环 (BHKCX)，港区 CBOSS（备库），高新 (GXCBOSS)(主库)，英协 CBOSS 库 (YXKCX)-备库


yaoshaopeng 4A 常用登录 crmlog / OpsysapP #0413


6. 一级云主机密码过期了，重置为 P00ay-0705# 了 2022/7/5

7. crm csf 代码开发流程
master 分支拉分支代码，开发完成合并到测试分支 test-routine。找于俊勇发测试环境。
平常每天 3 次（上午一次、下午两次），上线前期（周五，周一，周二还有紧急发布当天），
按需发布这个是发布人员那边反馈的发布频率

8. 双中心生产账号
cmp: http://10.108.5.68:28880 liming7   密码: liming@123

9. aicache

aicache 控制台-高新 1 http://10.228.148.216:28080 admin admin
aicache 控制台-高新 2 http://10.228.148.217:28080 admin admin
aicache 控制台-航空港 1 http://10.228.105.128:28080 admin admin
aicache 控制台-航空港 2 http://10.228.105.129:28080 admin admin

主机密码：
10.228.105.130 hkg1
10.228.105.131 hkg2
10.228.148.218 gx1
10.228.148.219 gx2

OpsysapP #0413

10. 磐基测试主机密码

10.218.34.85 root Zaq1CDE#
cd /home/dep/cboss_pd

11. ldap
jdbc:oracle:thin:@ldap://10.228.122.1 44:30 60/CBOSS1-CBOSS3-CBOSS2, cn=OracleContext, dc=cn ldap://10.228.122.1 45:30 60/CBOSS1-CBOSS3-CBOSS2, cn=OracleContext, dc=cn


12. panji
CRM 集团磐基-生产环境 https://10.228.109.253:1199 crm-ha-hkg-admin Kem123
CRM 集团磐基-生产环境 http://10.228.149.241:1199 crm-ha-gx-admin Kem12345!

13 et
高新 et 控制台： http://10.228.150.241:27600/et-console/index.html  admin/123456

AISCHEDULE. AI_SCHE_TASK_PARAM
AISCHEDULE. AI_SCHE_TASK_INFO

高新 PDB_GDP 库，AISCHEDULE


14. cboss-web 模板处理
select t.*, rowid from cboss. cboss_response_config_hn t where t.bipcode = 'BIP1A165' ;
select t.*, rowid from cboss. cboss_home_config t where t.bipcode = 'BIP1A165';
select t.*, rowid from cboss. cboss_home_template t where t.id = 900;

15. 一级云负载均衡地址 
hkg1: 
route  10.228.103.8-10   25000
web  10.228.103.8-10 25001

hkg2:
route  10.228.103.8-10 25100
web 10.228.103.8-10 25101

gx1: 
route  10.228.151.4-6 25000
web 10.228.151.4-6  25001

gx2 
route 10.228.151.4-6 25100
web 10.228.151.4-6 25101

16. 老 cboss 日志查看
10.218.34.4
用户名：was
密码：1qaz! QAZ
cboss-inst1/cboss-inst1-pf1/logs/cboss-inst1-node1-srv/cboss_app. log

10.218.34.8   aicrm 
/home/aicrm/app/other/cboss/log   老 cboss 调过来的日志

10.218.34.5 was  
/home/was/boss_app/boss-app-cen*-pf1/logs/boss-app-cen*-node*-srv  新的 csf 调过去的日志看不到
 
17. 一级云 cboss-rockermq 集群 gx hkg
 航空港：namesrv 端口是 20001，namesrv 运行 IP 范围：10.108.6.182～10.108.6.186，共 5 个实例
 高新：IP 如下，端口还是 20001
10.228.162.182
10.228.162.183
10.228.162.184
10.228.162.185
10.228.162.186
18. 一级云 hkg ailog aim
日志中心（港区、高新）： http://10.228.109.10:27112/    admin    1qaz! QAZ
港区 aim： http://10.228.105.9:29080      admin    aim_12345

19. 测试环境 RocketMQ-Dashboard 安装
docker run -d --name rocketmq-dashboard -e "JAVA_OPTS=-Drocketmq. namesrv. addr=10.218.36.6: 29876; 10.218.36.7: 29876; 10.218.36.8: 29876" -p 80 80:80 80 -t apacherocketmq/rocketmq-dashboard:latest

http://10.218.34.65:33001/



select * from csf. csf_srv_service_param where service_code in ('score_IRemoteCSV_sayHello','score_ICustmerPayMgntCSV_csptBusiBaseInfo','ord_IOrdCenterCSV_mobileKD2SchoolKD');
select * from csf. csf_srv_service_param where service_code in ('invoice_IInvoiceAppRemoteCSV_queryElectInvoiceInfo','score_IRemoteCSV_sayHello')
select * from csf. csf_srv_service_info where center_code in ('score','ord') and service_code= 'score_IRemoteCSV_sayHello';

select * from csf. csf_srv_service_info where center_code in ('score','ord');
select * from csf. csf_registerbycode_info;
select * from csf. csf_client_cluster_mapping where center_code = 'ord';

select * from csf. csf_client_cluster_mapping where center_code = 'cboss'
select * from csf. csf_client_cluster_mapping where center_code = 'score'

20 et
磐基平台
环境高新港区
et http://10.228.150.241:27600/et-console/login.html 
kem 地址 http://10.228.149.241:1199 https://10.228.109.253:1199 
crm 租户名称：crm-ha-gx-admin 密码 Kem12345！ 名称：crm-ha-hkg-admin 密码：Kem123 
crmet 租户名称：crmet-ha-gx-admin 密码 Kem12345！ 名称：crm-ha-hkg-admin crmet-admin 密码：Kem12345！ 
kubectl 控制台 admin 密码 4d5ogEtRvYeFgE# admin 密码 4d5ogEtRvYeFgE# 
crm-habor admin 密码：PaaSPJ#$0918 http://10.228.109.254:1121 admin 密码：PaaSPJ#$0918 
et-habor admin 密码：AbNu99! VIP@23Ts admin 密码：AbNu99! VIP@23Ts 

 -javaagent:/tomcat/ailog/ailog_center_agent. jar -Dailog. enable=kafka -Dailog. center=cbossweb -Dcsf. client. name=cboss_pro -DCENTER=A -DSUBMODULE=APP -DMODULE=CRM -Dfile. encoding=GBK -Dappframe. server. name=cboss-web


21
路由域名：cboss-route. ha. cmcc
WEB 域名：cboss-web. ha. cmcc

港区 1======================
路由负载 ip：10.228.104.2 45:25 000
路由 ingress：10.228.103.8- 10:25 000

WEB 负载 ip：10.228.104.2 45:25 001
WEB ingress：10.228.103.8- 10:25 001

港区 2======================
路由 ip：10.228.103.2 45:25 000
路由 ingress：10.228.103.8- 10:25 100

WEB 负载 ip：10.228.103.2 45:25 001
WEB ingress：10.228.103.8- 10:25 101

高新 1：======================
路由 ip：10.228.150.2 45:25 000
路由 ingress：10.228.151.4-6:25000

WEB 负载 ip：10.228.150.2 45:25 001
WEB ingress：10.228.151.4-6:25001

高新 2：======================
路由 ip：10.228.151.2 45:25 000
路由 ingress：10.228.151.4-6:25100

WEB 负载 ip：10.228.151.2 45:25 001
WEB ingress：10.228.151.4-6:25101

22. nc 探测端口是否启用
nc -v -w 2 -z mq4-cboss-gx. ha. cmcc 20001
23 rocketMQ
hkg: deploy@10.228.109.5
 gx: deploy@10.228.149.5
passwd: Xtfb #0508
cd /data/deploy/middleware/control

23 启动远程桌面 dashboard
PS E:\liyu7> .\jdk1.8.0_31_64\bin\java. exe -jar .\rocketmq-dashboard-1.0.1-SNAPSHOT. jar --rocketmq. config. namesrvAddr='10.228.162.1 82:20 001; 10.228.162.1 83:20 001; 10.228.162.1 84:20 001; 10.228.162.1 85:20 001; 10.228.162.1 86:20 001; 10.228.162.1 87:20 001'
 参考：.\jdk1.8.0_31_64\bin\java. exe -jar .\dashboard\rocketmq-dashboard-1.0.1-SNAPSHOT. jar --rocketmq. config. namesrvAddr='10.228.162.1 82:20 001; 10.228.162.1 83:20 001; 10.228.162.1 84:20 001; 10.228.162.1 85:20 001; 10.228.162.1 86:20 001; 10.228.162.1 87:20 001' --rocketmq. config. dataPath='~/dashboard/data' --debug

24 测试环境 rocketmq 主机
{"ip": "10.218.36.6", "port": 22, "user": "root", "password": "Zaq1CDE#"}, 
{"ip": "10.218.36.7", "port": 22, "user": "root", "password": "Zaq1CDE#"}, 
{"ip": "10.218.36.8", "port": 22, "user": "root", "password": "Zaq1CDE#"}, 

was@10.218.34.17 跳板机访问


25. sftp 账号：
	10.248.38.131 pandao-cluster1 河南 sftp 端口 4002
    	终端 sftp3711 密码用 Sftp_371!%00
    大音客服 sftpcsv3711  密码用 Sftpcsv_371!%

sftp -P 4002 sftp3711@10.248.38.131  -主
sftp -P 4002 sftp3711@10.248.38.150
put cboss_pd/file/DC_M_20221102011000_371.000 /incoming/file_interface/ctrm


-- 上传文件
curl -XPOST -k -H "Content-Type: multipart/form-data" -H "Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9. eyJhdWQiOlsicGFuZGFvIl0sImV4cCI6MTY3MjM5MDc5NSwiaWF0IjoxNjY3MjA2Nzk1LCJpc3MiOiJodHRwczovL3BhbmRhby1hdXRoLXNlcnZlci5jbWl0LmNtY2MvYXV0aCIsInN1YiI6InNwaWZmZTovL3BkLmNtaXQuY21jYy9vcmcvcGQvcGFydHkvYm9zczM3MTAifQ. feRjxGqe7QnmmMyyq3u0F4oHPC4Xj-D6aUtMnsUD3yI" -F file=@/home/dep/cboss_pd/file/DC_M_20221102011000_371.000 -F username=sftp3711 -F path=/incoming/file_interface/ctrm " https://10.248.38.131:4018/api/v0/add"

-- 大于 100M
curl -XPOST -k -H "Content-Type: multipart/form-data" -H "Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9. eyJhdWQiOlsicGFuZGFvIl0sImV4cCI6MTY3MjM5MDc5NSwiaWF0IjoxNjY3MjA2Nzk1LCJpc3MiOiJodHRwczovL3BhbmRhby1hdXRoLXNlcnZlci5jbWl0LmNtY2MvYXV0aCIsInN1YiI6InNwaWZmZTovL3BkLmNtaXQuY21jYy9vcmcvcGQvcGFydHkvYm9zczM3MTAifQ. feRjxGqe7QnmmMyyq3u0F4oHPC4Xj-D6aUtMnsUD3yI" -F file=@/home/dep/DC_M_20221103100000_371.007 -F username=sftp3711 -F path=/incoming/file_interface/ctrm " https://10.248.38.131:4018/api/v0/add"


curl -XPOST  -k -H "Content-Type: multipart/form-data" -H "Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9. eyJhdWQiOlsicGFuZGFvIl0sImV4cCI6MTY3MjM5MDc5NSwiaWF0IjoxNjY3MjA2Nzk1LCJpc3MiOiJodHRwczovL3BhbmRhby1hdXRoLXNlcnZlci5jbWl0LmNtY2MvYXV0aCIsInN1YiI6InNwaWZmZTovL3BkLmNtaXQuY21jYy9vcmcvcGQvcGFydHkvYm9zczM3MTAifQ. feRjxGqe7QnmmMyyq3u0F4oHPC4Xj-D6aUtMnsUD3yI"  " https://10.248.38.131:4018/api/v0/get?arg=QmeWVboC9nVwsRJBvtG4ktfEBpwamhAoi8Ge1J9Us5QjL9&username=sftp3711"

--150
curl -XPOST -k -H "Content-Type: multipart/form-data" -H "Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9. eyJhdWQiOlsicGFuZGFvIl0sImV4cCI6MTY3MjM5MDc5NSwiaWF0IjoxNjY3MjA2Nzk1LCJpc3MiOiJodHRwczovL3BhbmRhby1hdXRoLXNlcnZlci5jbWl0LmNtY2MvYXV0aCIsInN1YiI6InNwaWZmZTovL3BkLmNtaXQuY21jYy9vcmcvcGQvcGFydHkvYm9zczM3MTAifQ. feRjxGqe7QnmmMyyq3u0F4oHPC4Xj-D6aUtMnsUD3yI" -F file=@/home/dep/cboss_pd/file/DC_M_20221102011000_371.000 -F username=sftp3711 -F path=/incoming/file_interface/ctrm " https://10.248.38.150:4018/api/v0/add"

curl -XPOST  -k -H "Content-Type: multipart/form-data" -H "Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9. eyJhdWQiOlsicGFuZGFvIl0sImV4cCI6MTY3MjM5MDc5NSwiaWF0IjoxNjY3MjA2Nzk1LCJpc3MiOiJodHRwczovL3BhbmRhby1hdXRoLXNlcnZlci5jbWl0LmNtY2MvYXV0aCIsInN1YiI6InNwaWZmZTovL3BkLmNtaXQuY21jYy9vcmcvcGQvcGFydHkvYm9zczM3MTAifQ. feRjxGqe7QnmmMyyq3u0F4oHPC4Xj-D6aUtMnsUD3yI"  " https://10.248.38.131:4018/api/v0/get?arg=QmVkwjPVdW3saxCajWk1qXDKsN7Y2w9FMmexTyCjXJKPP9&username=sftp3711"



QmeWVboC9nVwsRJBvtG4ktfEBpwamhAoi8Ge1J9Us5QjL9


implementation 'org. apache. httpcomponents. client5:httpclient5: 5.2-alpha1' 33

implementation 'org. apache. httpcomponents. core5:httpcore5: 5.2-alpha1' 34

implementation 'org. apache. httpcomponents, core5: httpcore5-h2: 5.2-alpha1' 35




## Shell
### Cmp deploy shell

```sh
#!/bin/bash

newimage=$1
deploymentname=$2

echo ${newimage}
echo ${deploymentname}
echo "update image..."
./kubectl set image deployment -n cboss-gx-core-node ${deploymentname} container-0=${newimage}
rm -rf app/*

echo "verify image..."
./kubectl describe deployment -n cboss-gx-core-node ${deploymentname} | grep -i image

```

### Cmp 修改密码脚本

```sh
#pwd
#runtime-config/config/prod
find . -type d -regex ".*config-cboss-.*" | awk -F/ '{print $2}' | sort | uniq | xargs -I path sh -c 'find ./path -name *.xml -o -name *.properties' | xargs grep -l 6a9bd079c45db1bbb885db32


find . -type d -regex ".*config-cboss-.*" | awk -F/ '{print $2}' | sort | uniq | xargs -I path sh -c 'find ./path -name csf.xml' | xargs grep -l 80000


```

## Vim
1. vim 换行符替换成 “|“ 操作
   
```ruby
:%s/\n/|/g
```
