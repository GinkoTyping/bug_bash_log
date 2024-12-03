## 页面触发的POST请求返回 404
### 详细描述
浏览器里触发的请求路径符合@WebServlet的匹配规则 但无法实际被Servlet匹配
### 解决方法
检查tomcat的版本

## 连接数据库时报错 Datasource.driverClassName 为 null
### 详细描述
- tomcat的conf文件夹中的context.xml 配置了正确的driver name
- 项目内的webcontent/WEB-INF 的web.xml 配置了正确的driver name
  
但是项目运行时依然报错 datasource.driverClassName 为 null
### 解决方法
创建webapp/META-INF/context.xml 再次定义 driver name
```xml
<?xml version="1.0" encoding="UTF-8"?>
<Context>
    <!-- Tomcat User Database Configuration -->
    <Resource auth="Container"
              description="User database that can be updated and saved"
              factory="org.apache.catalina.users.MemoryUserDatabaseFactory"
              name="UserDatabase"
              pathname="conf/tomcat-users.xml"
              type="org.apache.catalina.UserDatabase"/>

    <!-- JDBC DataSource Configuration -->
    <Resource name="jdbc/myData"
              auth="Container"
              type="javax.sql.DataSource"
              maxTotal="100"
              maxIdle="30"
              maxWaitMillis="10000"
              username="root"
              password="123456"
              driverClassName="com.mysql.cj.jdbc.Driver"
              url="jdbc:mysql://localhost:3306/mysq"/>

    <!-- Optionally, you can add other configurations here, such as:
         - <Environment> elements for application-specific environment variables
         - <Loader> elements for class loader configuration
         - <Realm> elements for security configuration
         - <Valve> elements for logging and monitoring
         - <Manager> elements for session management
         - <Listener> elements for application lifecycle events
    -->
</Context>
```