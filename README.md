# mybatis-generator
mybatis的逆向工程，自动生成mapper和po
生成的一些配置在GeneratorXML.xml中，注释已经很明白
常见的修改地方比如
<!--数据库连接的信息：驱动类、连接地址、用户名、密码 -->
		 <jdbcConnection driverClass="com.mysql.jdbc.Driver" connectionURL="jdbc:mysql://localhost:3306/inventory?characterEncoding=utf8" 
			userId="root" password="root"> </jdbcConnection>
项目中使用的mysql，如需要更改成oracle或者其他数据库则自己将驱动程序放至lib底下。然后修改上面的设置如：
<jdbcConnection driverClass="oracle.jdbc.OracleDriver"
			connectionURL="jdbc:oracle:thin:@127.0.0.1:1521:XE" userId="bbs"
			password="123456">
已在文件中有配置将注释去除即可
<!-- targetProject:生成PO类的位置 -->
		<javaModelGenerator targetPackage="com.ssm.po"
			targetProject=".\src">
			<!-- enableSubPackages:是否让schema作为包的后缀 -->
			<property name="enableSubPackages" value="false" />
			<!-- 从数据库返回的值被清理前后的空格 -->
			<property name="trimStrings" value="true" />
		</javaModelGenerator>
<!-- targetProject:mapper映射文件生成的位置 -->
		<sqlMapGenerator targetPackage="com.ssm.mapper"
			targetProject=".\src">
			<!-- enableSubPackages:是否让schema作为包的后缀 -->
			<property name="enableSubPackages" value="false" />
		</sqlMapGenerator>
<!-- targetPackage：mapper接口生成的位置 -->
		<javaClientGenerator type="XMLMAPPER"
			targetPackage="com.ssm.mapper" targetProject=".\src">
			<!-- enableSubPackages:是否让schema作为包的后缀 -->
			<property name="enableSubPackages" value="false" />
		</javaClientGenerator>
主要修改targetPackage="位置"
<!-- 指定数据库表 -->
		<table tableName="表名1"></table>
    <table tableName="表名2"></table>
    <table tableName="表名3"></table>
可以多表
修改完毕后run test.java
刷新项目则可以自动生成mapper与po
