# MyBatis



# 1 简介

基于Java的持久层框架，使用XML或注解，避免了JDBC代码和手动设置参数。

数据持久化：内存断电易失，并且内存太贵了。用数据库转到硬盘里

分层：Dao层，Service层，Controller层

# 2 获得

```xml
 <dependency>
            <groupId>org.mybatis</groupId>
            <artifactId>mybatis</artifactId>
            <version>3.5.2</version>
 </dependency>
 <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>8.0.21</version>
 </dependency>
      
```

也能在GitHub上找

此外还要在pom里提前解决资源过滤问题

```xml
 <!-- 解决maven资源过滤问题 -->
    <build>
        <resources>
            <resource>
                <directory>
                    src/main/resources
                </directory>
                <includes>
                    <include>**/*.properties</include>
                    <include>**/*.xml</include>
                </includes>
                <filtering>true</filtering>
            </resource>

            <resource>
                <directory>
                    src/main/java
                </directory>
                <includes>
                    <include>**/*.properties</include>
                    <include>**/*.xml</include>
                </includes>
                <filtering>true</filtering>
            </resource>
        </resources>
    </build>
```



# 3 第一个MyBatis程序

## 3. 1 Maven项目，引入坐标

Ok

## 3.2 编写mybatis的核心配置文件

Mybatis-config.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE configuration PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">

<configuration>
    <environments default="development">
        <environment id="development">
            <transactionManager type="JDBC" />
            <!-- 配置数据库连接信息 -->
            <dataSource type="POOLED">
                <property name="driver" value="com.mysql.cj.jdbc.Driver" />
                <property name="url" value="jdbc:mysql://localhost:3306/mybatis?useSSL=true&amp;useUnicode=true&amp;characterEncoding=UTF-8&amp;serverTimezone=GMT%2B8" />
                <property name="username" value="root" />
                <property name="password" value="root" />
            </dataSource>
        </environment>
    </environments>
  
  <!-- Mapping就是Dao -->
  <!-- 每一个Mapper.xml都需要在核心配置文件注册 -->
    <mappers>
        <!-- 还要解决maven资源过滤问题 -->
        <!-- 该UserMapper.xml没有位于resource文件夹下！ -->
        <!-- 需要手动配置，让其也能被导出到target下 -->
        <mapper resource="com/learn/dao/UserMapper.xml"/>
    </mappers>

</configuration>
```



## 3.3 编写mybatis工具类

```java
public class MybatisUtils {

    private static SqlSessionFactory sqlSessionFactory;

    static {
        String resource = "mybatis-config.xml";
        try {
            // 获取Mybatis的sqlSessionFactory对象
            InputStream inputStream = Resources.getResourceAsStream(resource);
            sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    public static SqlSession getSqlSession() {
        // 使用工厂创建SqlSession实例
        return sqlSessionFactory.openSession();
    }

}
```

## 3.4 编写代码

- 实体类pojo

  ```java
  public class User{
    	// 略
  }
  
  ```

  

- Dao接口

  ```java
  public interface UserDao {
      List<User> getUserList();
  }
  ```

  

- 接口实现

  不用写接口实现，使用UserMapper.xml文档

  ```xml
  <?xml version="1.0" encoding="UTF-8" ?>
  <!DOCTYPE mapper
          PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
          "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
  <!-- 绑定一个对应的Dao(mapper)接口 -->
  <mapper namespace="com.learn.dao.UserDao">
      <!-- 查询,id是方法名 -->
      <!-- 返回类型，哪怕查出来的是个集合，也要选范型的类 -->
      <select id="getUserList" resultType="com.learn.pojo.User">
          select * from mybatis.user
      </select>
  </mapper>
  
  ```

  

## 3.5 Junit测试

```java
public class UserDaoTest {

    @Test
    public void test() {

        // 获取SqlSession
        SqlSession sqlSession = MybatisUtils.getSqlSession();

        // 方式一 getMapper执行SQL
        UserDao userDao = sqlSession.getMapper(UserDao.class);
        List<User> userList = userDao.getUserList();

        for(User user : userList) {
            System.out.println(user);
        }

        // 别忘关闭SqlSession
        sqlSession.close();
    }
}
```

