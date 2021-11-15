--- 关于 门诊医嘱 表的 医嘱ID, 医嘱编号, 成组医嘱ID， 父医嘱ID
-- 普通医嘱: 数量为正, 医嘱ID等价于医嘱编号, 成组医嘱ID 是该组中一个医嘱ID(一般而言就是最小的那个)
-- 成组医嘱ID退费前后, 不变. 即正负数量的一组医嘱, 医嘱ID, 医嘱编号互不同, 但成组医嘱ID相同
-- 退费后 原医嘱ID, 医嘱编号, 成组医嘱ID 对应退费记录对应的正记录的相应ID
-- 正记录: 医嘱ID == 医嘱编号 == 原医嘱ID
-- 负记录: 医嘱编号 == 原医嘱ID == 正记录(医嘱ID == 医嘱编号 == 原医嘱ID)
-- 负记录: 成组医嘱ID 正负记录同组
辅药的 父医嘱 ID == 主要医嘱ID（编号）



PG的一些坑
1、SUBSTR(性质属性, 12, 1)  性质属性为空时，取不到会返回NULL！性质属性不为空时，取不到居然返回的是空字符串，一定注意，严重坑！
2、update语句里表名不能用别名。
3、select 字段1 into 变量1 要捕获严格错误类型必须加 STRICT，不然返回错误类型不明确，不知道是找不到还是返回多行了。
4、nvl函数不存在，但编译不会报错，可以通过批量查询匹配。
5、编程类必须要$body开头和结尾$body
6、编程类必须声明语言类型，可能是因为pgsql 编程支持多种语言的原因。


门诊医嘱：主辅药，正负记录
	1. 成组医嘱ID 全等
	2. 正记录：
		主药： yizhuid == yizhubh == 成组医嘱ID
			父医嘱 ID 空
		辅药： yizhuid == yizhubh
			父医嘱 ID == 主药医嘱编号
	3. 负记录：
		主辅药都有负记录
		负记录 医嘱ID 不考虑
		医嘱编号 == 对应的（主对主，辅对辅）医嘱ID（编号）

1、院区ID 支持两位 院区 可支持从 1 - ZZ
例如：1、2、3......11、12、13.........99、A1、A2、......AZ、B1

2、应用ID 用六位表示： 1-2 表示系统 ，3-4 表示院区，5-6 表示 应用ID
例如：050102 ：05 表示 药房 01 表示 院区ID 为1 ，02 表示药房编号


gitlab: http://gitlab.df-mic.com（http://192.168.1.206）  gitlab-his.fr-inc.cn

jenkins的地址:  http://192.168.1.213:8020
jenkins的用户名: admin
jenkins的密码: dongfang@123

select *
from all_tab_columns
where Table_Name = 'ZY_BINGRENXX';

$ seata-server.bat -p <port> -m file(store_mode)

http://gitlab-his.fr-inc.cn/operation-dongfang/lc-menzhenjz.git

nacos：http://192.168.1.213:8848/nacos。账号密码都是nacos
如果你要调试代码，本地 nacos/seata 要先启动，然后gy-jichufw 是要最先启动
============================================================================================================================
岱山医共体环境下如果第三方需要访问云HIS的接口，访问地址统一为oapi.his.com，与河南一致。
oapi.his.com要能访问，必须设置dns为192.168.180.27，如果第三方系统环境无法访问192.168.180.27肯定是不通的，
联系医院信息科解决吧。第三方位于前置机的话，就联系信息科在网闸等安全设备上配置映射，然后在系统上添加hosts解析。
http://oapi.his.com/actuator/health  ，这个是第三方访问his接口的测试路径，如果没结果要么dns没设置要么是网络不通。
============================================================================================================================
岱山
    url: jdbc:oracle:thin:@192.168.180.205:1521/orcl
    username: gy_jichufw
    password: daishanhis2021
岱山生产环境数据库只读账号：df_reader
岱山生产环境数据库只读账号密码:  df_reader@daishan2021
jk_waibujk 密码没改还是jk_waibujk2021，这个对应jk_waibujk服务
df_waibujk 密码是df_waibujk2021，这个对应df_waibujk服务

岱山 DNS: 192.168.180.27

公司 DNS: 192.168.1.50
河南
业务系统名称  域名地址  用户名  密码
配置中心  http://nacos.his.com/nacos  develop  develop
后端服务api  http://api.his.com  JWTtoken  
主数据管理平台  http://admin.his.com  DBA  123
运维管理平台  http://opm.his.com  DBA  123   845587524959252480
病历夹平台  http://cdr.his.com    
决策支持平台  http://cdss.his.com    
医保管理平台  http://yibao.his.com    
链路追踪平台  http://192.168.0.71:28080/  无  无
CDC平台  http://192.168.0.72:18630/  admin  admin
方软报表  http://192.168.0.77:37799/webroot/decision  admin  zzszfcyy@2021
前端更新ftp地址  192.168.0.78  csharp  csharp@123
河南：
	# url: jdbc:oracle:thin:@192.168.0.30:1521/orcl
    # username: gy_jichufw
    # password: zzszfcyy2021
	nacos： develop/develop
河南测试 jenkins 地址：
http://192.168.1.242:8888/ 用户名/密码
admin/zzszfcyy@2021
河南测试环境地址：192.168.0.90:9000  DBA/123456
河南测试 DB: jdbc:oracle:thin:@192.168.0.90:1521:xe  df_zhushuju/dfhis2020
河南生产环境只读帐号为 df_reader，密码 dfhis2021
==============================================================
岱山:
http://192.168.1.243:8080/
admin
daishan@2021
PCAS: http://192.168.180.183:8090/ClinicalAppointment?id=
===============================================================
VPN:
miaowan 
miaowan@+86-13163249276
linux： root/dell@123123
公司-dev
192.168.1.213:22  cd /opt/logs/dev
公司 DNS: 192.168.1.50
用户名：duping 
密码：duping@18857090975
===============================================================
openvpn/openvpn@123   


ODIN
http://192.168.0.82:8080/
    admin
    szfcyy@2021
http://192.168.1.242:8080/
    admin
    dongfang@123
http://user.odinhealth.co.nz/zh-hans/user
    dongfang2018/dongfang*2019
odin先登录，才能看视频
==============================================================
宝苑：
    url: jdbc:oracle:thin:@192.168.87.9:1521:orcl
    username: gy_jichufw
    password: dfhis2020


==============================================================
plsql 中文乱码问题
NLS_LANG：SIMPLIFIED CHINESE_CHINA.ZHS16GBK
==============================================================

dev:
oracle
driver-class-name: oracle.jdbc.driver.OracleDriver
    url: jdbc:oracle:thin:@192.168.1.200:1521:xe
    username: gy_jichufw
    password: dfhis2020
 jdbc:oracle:thin:@192.168.1.200:1521:orcl
	username: df_zhushuju

============================================================================
交接:
医嘱展开： com.df.cbhis.agg.zhuyuanyz.service.listener.YiZhuZkListener#yiZhuZk
com.df.cbhis.lc.zhuyuan.applicationservice.YiZhuZkService#yiZhuZk
com.df.cbhis.jj.zhuyuan.controller.ZiDongJfController#ziDongJf


需求:
 1. 消息推送: 新增检查申请单时, 推送数据给第三方接口.
		lc-shenqingdanzx
	门诊: 绿色通道-开立（保存）后; 普通病人-收费后; 
		保存门诊病历: 判断特殊通道病人-可执行标志为 1 发送 pacs
		http://api.his.com/winbff-linchuangmz/menZhenBingLi/saveMenZhenBl
		com.df.cbhis.lc.menzhenjz.controller.BingRenXxController#saveMenZhenBl
		收费：
		com.df.cbhis.lc.shenqingdanzx.jiancha.service.JianChaSqdService#menZhenSf
	住院: his 复核展开后（护士站）
    com.df.cbhis.lc.shenqingdanzx.controller.JianChaSqdController.saveJianChaSqd
	com.df.cbhis.lc.shenqingdanzx.jiancha.service.impl.JianChaSqdServiceImpl#menZhenSf
	住院医嘱复核: 
	http://api.his.com/winbff-linchuangzy/bingRenYz/saveBingRenYzXx?requestID=900f1dee118b4dc9875ed5ae48fc150f
	com.df.cbhis.lc.zhuyuan.controller.BingRenYzController#yiZhuFuHe
    http://192.168.0.115:8888/pacs/JianChaSqd
    post

    http://192.168.0.115:8888/pacs/updateWeiJiZhiZt
    post
 2. 状态更新
	 门诊:
		检查登记; yewulx = 2 修改检查申请单状态
		取消登记; yewulx = 5 修改检查申请单状态
		取消报告; yewulx = 6 修改检查申请单状态
	 住院:
		检查登记; 取消登记; 取消报告;
		状态修改,业务类型同门诊
 3. 检查报告: 门诊, 住院检查报告
 4. 门诊医嘱:
    4.1. request:
            开单时间区间: start-end time, 默认当天
            bingrenid: Nullable
            当前登录的科室: NotNull
        db-table: LC_MENZHENJZ.MZ_YIZHU 表
    4.2. 医嘱执行:
        yizhulx = 91、92的项目执行后， 修改
        table: LC_MENZHENJZ.MZ_YIZHU
            column: zhixingbz,zhixingren,zhixingrenxm,zhixingrq
        table: JJ_GUAHAO.mz_feiyong2
            column: set  zhixingbz = 1
=============================================================================================
宝苑测试：
his-gateway  --> api.df-mic.com
web-zhushujugl  --> admin.df-mic.com
onecenter-service  --> opm.df-mic.com
web-yibaogl  --> yibao.df-mic.com
cdr-web  --> cdr.df-mic.com
cdss-web  --> cdss.df-mic.com
web-main  --> main.df-mic.com
宝苑本地模拟环境oracle地址192.168.1.68  用户名没改过，还是最老的gy_jichufw这种，密码是dfhis2020
宝苑本地模拟环境web相关用户名是DBA，密码abc+123
宝苑本地模拟环境nacos地址nacos.df-mic.com/nacos，用户名nacos，密码nacos
上述所有的域名需要将DNS配置为192.168.1.50才可以解析
或者是在本机hosts文件添加静态解析，各域名对应的ip地址为192.168.1.52


=============================================================================================
by:
	jdbc:oracle:thin:@192.168.87.9:1521:orcl   
	gy_jichufw/dfhis2020

by-dev:
	jdbc:oracle:thin:@192.168.1.68:1521/orcl
	gy_jichufw/dfhis2020
dev: 
	jdbc:oracle:thin:@192.168.1.200:1521:orcl
	df_zhushuju/dfhis2020
	jdbc:postgresql://192.168.1.213:5432/df_his
dlh:
	jdbc:postgresql://192.168.10.23:5000/df_his
	df_zhushuju/dfhis2020
ds:
	jdbc:oracle:thin:@192.168.180.205:1521/orcl
	df_zhushuju/
hn:
	jdbc:oracle:thin:@192.168.0.30:1521/orcl
	df_zhushuju/
hn-dev:
	jdbc:oracle:thin:@192.168.0.90:1521:xe
	df_zhushuju/











df:
  jdbc:
    ykf-jichuyw:
      username: df_yaokufang
      password: dfhis2020
    gy-jichufw:
      username: df_zhushuju
      password: dfhis2020
    gy-bingrenzsy:
      username: df_bingrenzsy
      password: dfhis2020
    gy-mobanku:
      username: df_bingli
      password: dfhis2020
    jj-guahao:
      username: df_jj_menzhen
      password: dfhis2020
    jj-piaojugl:
      username: df_piaojugl
      password: dfhis2020
    jj-zhuyuan:
      username: df_jj_zhuyuan
      password: dfhis2020
    lc-bingliku:
      username: df_bingli
      password: dfhis2020
    lc-menzhenjz:
      username: df_lc_menzhen
      password: dfhis2020
    lc-shenqingdanzx:
      username: df_shenqingdan
      password: dfhis2020
    lc-zhuyuan:
      username: df_lc_zhuyuan
      password: dfhis2020
    yb-yibaogl:
      username: df_yibao
      password: dfhis2020
    oss:
      username: df_oss
      password: dfhis2020
    cdr:
      username: df_cdr
      password: dfhis2020
    ba-binganjk:
      username: df_bajk
      password: bajk
    lc-binglizk:
      username: df_yiliaogl
      password: dfhis2020
    dfmessage-service:
      username: df_message
      password: dfhis2020
    lc-jibingbk:
      username: df_yiliaogl
      password: dfhis2020
    df-biaodan:
      username: df_biaodan
      password: dfhis2020
    df-authorization:
      username: df_authorization
      password: dfhis2020
    onecenter-service:
      username: df_opm
      password: dfhis2020
    # ykf-jichuyw:
    #   username: ykf_jichuyw
    #   password: dfhis2020
    # gy-jichufw:
    #   username: gy_jichufw
    #   password: dfhis2020
    # gy-bingrenzsy:
    #   username: gy_bingrenzsy
    #   password: dfhis2020
    # gy-mobanku:
    #   username: gy_mobanku
    #   password: dfhis2020
    # jj-guahao:
    #   username: jj_guahao
    #   password: dfhis2020
    # jj-piaojugl:
    #   username: jj_piaojugl
    #   password: dfhis2020
    # jj-zhuyuan:
    #   username: jj_zhuyuan
    #   password: dfhis2020
    # lc-bingliku:
    #   username: lc_bingliku
    #   password: dfhis2020
    # lc-menzhenjz:
    #   username: lc_menzhenjz
    #   password: dfhis2020
    # lc-shenqingdanzx:
    #   username: lc_shenqingdanzx
    #   password: dfhis2020
    # lc-zhuyuan:
    #   username: lc_zhuyuan
    #   password: dfhis2020
    # yb-yibaogl:
    #   username: yibao
    #   password: dfhis2020
    # oss:
    #   username: oss
    #   password: dfhis2020
    # cdr:
    #   username: cdr
    #   password: dfhis2020
    # ba-binganjk:
    #   username: bajk
    #   password: bajk
    # lc-binglizk:
    #   username: lc_binglizk
    #   password: dfhis2020
    # dfmessage-service:
    #   username: message_center
    #   password: dfhis2020
    # lc-jibingbk:
    #   username: lc_jibingbk
    #   password: dfhis2020
    # df-biaodan:
    #   username: df_biaodan
    #   password: dfhis2020
    # df-authorization:
    #   username: df_authorization
    #   password: dfhis2020
    # onecenter-service:
    #   username: onecenter_service
    #   password: dfhis2020
	-----------------------------------------------------
	ds
	df:
  jdbc:
    ykf-jichuyw:
      username: df_yaokufang
      password: DaI3an1gt2021
    gy-jichufw:
      username: df_zhushuju
      password: DaI3an1gt2021
    gy-bingrenzsy:
      username: gy_bingrenzsy
      password: dfhis2020
    gy-mobanku:
      username: gy_mobanku
      password: dfhis2020
    jj-guahao:
      username: jj_guahao
      password: dfhis2020
    jj-piaojugl:
      username: jj_piaojugl
      password: dfhis2020
    jj-zhuyuan:
      username: jj_zhuyuan
      password: dfhis2020
    lc-bingliku:
      username: lc_bingliku
      password: dfhis2020
    lc-menzhenjz:
      username: lc_menzhenjz
      password: dfhis2020
    lc-shenqingdanzx:
      username: lc_shenqingdanzx
      password: dfhis2020
    lc-zhuyuan:
      username: lc_zhuyuan
      password: dfhis2020
    yb-yibaogl:
      username: yibao
      password: dfhis2020
    oss:
      username: oss
      password: dfhis2020
    cdr:
      username: cdr
      password: dfhis2020
    ba-binganjk:
      username: bajk
      password: bajk
    lc-binglizk:
      username: lc_binglizk
      password: dfhis2020
    dfmessage-service:
      username: message_center
      password: dfhis2020
    lc-jibingbk:
      username: lc_jibingbk
      password: dfhis2020
    df-biaodan:
      username: df_biaodan
      password: dfhis2020
    df-authorization:
      username: df_authorization
      password: dfhis2020
    onecenter-service:
      username: onecenter_service
      password: dfhis2020
      
    
