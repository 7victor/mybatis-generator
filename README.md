# mybatis-generator
目的：mybatis逆向工程生成po、mapper.java、mapper.xml

前提条件：java环境（JDK、开发工具如eclipse）

项目：



首先导入mybatis.jar、mybatis-generator-core.jar、mysql-connector-java.jar（版本号我没写）

写GeneratorXML.xml

<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE generatorConfiguration
  PUBLIC "-//mybatis.org//DTD MyBatis Generator Configuration 1.0//EN"
  "http://mybatis.org/dtd/mybatis-generator-config_1_0.dtd">
<generatorConfiguration>
	<context id="testTables" targetRuntime="MyBatis3">
		<commentGenerator>
			<!-- 是否去除自动生成的注释 true：是 ： false:否 -->


			<property name="suppressAllComments" value="true" />
		</commentGenerator>
		<!--数据库连接的信息：驱动类、连接地址、用户名、密码 -->
		 <jdbcConnection driverClass="com.mysql.jdbc.Driver" connectionURL="jdbc:mysql://localhost:3306/inventory?characterEncoding=utf8" 
			userId="root" password="root"> </jdbcConnection>
		<!-- <jdbcConnection driverClass="oracle.jdbc.OracleDriver"
			connectionURL="jdbc:oracle:thin:@127.0.0.1:1521:XE" userId="bbs"
			password="123456">
		</jdbcConnection> -->
		<!-- 默认false，把JDBC DECIMAL 和 NUMERIC 类型解析为 Integer，为 true时把JDBC DECIMAL 
			和 NUMERIC 类型解析为java.math.BigDecimal -->
		<javaTypeResolver>
			<!-- 是否使用bigDecimal， false可自动转化以下类型（Long, Integer, Short, etc.） -->
			<property name="forceBigDecimals" value="false" />
		</javaTypeResolver>
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
		<!-- 指定数据库表 -->
		<table tableName="user"></table>
		<table tableName="good"></table>
		<table tableName="good_type"></table>
		<table tableName="orders"></table>
		<table tableName="order_goods"></table>
		<table tableName="stock"></table>
		<table tableName="stock_goods"></table>
		<table tableName="menu"></table>
		<!-- <table tableName="BBSSection"></table>
		<table tableName="BBSTopic"></table>
		<table tableName="BBSReply"></table>
		<table tableName="BBSNews"></table>
		<table tableName="BBSFriend"></table>
		<table tableName="BBSIMPEACH"></table> -->
		<!-- <table schema="" tableName="sys_user"></table> <table schema="" tableName="sys_role"></table> 
			<table schema="" tableName="sys_permission"></table> <table schema="" tableName="sys_user_role"></table> 
			<table schema="" tableName="sys_role_permission"></table> -->
		<!-- 有些表的字段需要指定java类型 <table schema="" tableName=""> <columnOverride column="" 
			javaType="" /> </table> -->
	</context>
</generatorConfiguration>
相关配置在文中注释已经比较清楚了
项目中使用的mysql，如需要更改成oracle或者其他数据库则自己将驱动程序放至lib底下。然后修改上面的设置如： 已在文件中有配置将注释去除即可

JDBC连接设置

jdbcConnection driverClass="com.mysql.jdbc.Driver" connectionURL="jdbc:mysql://localhost:3306/inventory?characterEncoding=utf8" 
		userId="root" password="root"> </jdbcConnection>
各种生成包的路径设置  主要修改targetPackage="位置"
	<javaModelGenerator targetPackage="com.ssm.po"
		targetProject=".\src">
		<!-- enableSubPackages:是否让schema作为包的后缀 -->
		<property name="enableSubPackages" value="false" />
		<!-- 从数据库返回的值被清理前后的空格 -->
		<property name="trimStrings" value="true" />
	</javaModelGenerator>
	<sqlMapGenerator targetPackage="com.ssm.mapper"
		targetProject=".\src">
		<!-- enableSubPackages:是否让schema作为包的后缀 -->
		<property name="enableSubPackages" value="false" />
	</sqlMapGenerator>
	<javaClientGenerator type="XMLMAPPER"
		targetPackage="com.ssm.mapper" targetProject=".\src">
		<!-- enableSubPackages:是否让schema作为包的后缀 -->
		<property name="enableSubPackages" value="false" />
	</javaClientGenerator>
需要生成的表的设置

<table tableName="表名1"></table>
<table tableName="表名2"></table>
<table tableName="表名3"></table>
可以写多个表一同生成
最后写Test.java
public class test {

	public void generator() throws Exception{

		List<String> warnings = new ArrayList<String>();
		boolean overwrite = true;
		File configFile = new File("GeneratorXML.xml"); 
		ConfigurationParser cp = new ConfigurationParser(warnings);
		Configuration config = cp.parseConfiguration(configFile);
		DefaultShellCallback callback = new DefaultShellCallback(overwrite);
		MyBatisGenerator myBatisGenerator = new MyBatisGenerator(config,
				callback, warnings);
		myBatisGenerator.generate(null);

	} 
	public static void main(String[] args) throws Exception {
		try {
			test generatorSqlmap = new test();
			generatorSqlmap.generator();
		} catch (Exception e) {
			e.printStackTrace();
		}
		
	}
}
最后只需要run Test.java即可自动生成。刷新项目（Refresh F5）即可看到新增的mapper和po

是不是很简单呢。

附上Git代码https://github.com/7victor/mybatis-generator小伙伴们可以自行下载
