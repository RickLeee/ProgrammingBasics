# IOC容器

## 底层原理

### 什么是IOC

1. 控制反转，创建对象和调用对象由Spring控制
2. 降低耦合度

### 底层

IOC过程：xml解析+反射+工厂

![image-20210914202111159](C:\Users\RickLee\AppData\Roaming\Typora\typora-user-images\image-20210914202111159.png)

## 接口(BeanFactory)

1. ### IOC容器底层就是对象工厂

2. ### IOC容器两种实现方式：

   1. BeanFactory：Spring内部接口，一般不用
   2. ApplicationContext：BeanFactory子接口，功能更强，**配置文件读取时创建对象**

3. ### ApplicationContext实现类

   ![image-20210914205629316](C:\Users\RickLee\AppData\Roaming\Typora\typora-user-images\image-20210914205629316.png)

## IOC操作Bean管理

### Bean管理

两个操作：

1. Spring创建对象
2. Spring注入属性

### bean管理操作

1. 基于xml配置文件方式实现
2. 基于注释方式

## 基于XML

#### 创建对象

```Java
<!--1 配置对象的创建-->
<bean id="user" class="com.lee.spring5.User"></bean>
```

1. 只用bean标签标签中添加属性实现对象创建
2. 常用属性：
   1. id：唯一标识
   2. class：类全路径(包类路径)
3. 创建对象默认执行无参构造

#### 注入属性

1. DI：依赖注入，即注入属性

   1. set注入

      ```java
      /**
      *1.set方法注入
      */
      public class Book {
          private String bookName;
      	private String bookAuthor;
          public void setBookName(String bookName) {
              this.bookName = bookName;
          }
          public void setBookAuthor(String bookAuthor) {
              this.bookAuthor = bookAuthor;
          }
      }
      // xml配置文件
      <!--    2 set注入属性-->
          <bean id="book" class="com.lee.spring5.Book">
      <!--        用property完成属性注入
                  name:属性名
                  value:注入的值-->
              <property name="bookName" value="Java入土"></property>
              <property name="bookAuthor" value="Lee"></property>
          </bean>
      ```

   2. 有参构造注入 

      ```java
      <!--    3 有参构造注入-->
      <bean id="book" class="com.lee.spring5.Book">
          <constructor-arg name="bookName" value="Java入土"></constructor-arg>
          <constructor-arg name="bookAuthor" value="Lee"></constructor-arg>
      </bean>
      ```

#### p名称空间注入

简化xml配置

1.  添加p名称空间

   ```java
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xmlns:p="http://www.springframework.org/schema/p"
          xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
   ```

2. 属性注入，在bean标签中操作(set注入)

   ```
   <bean id="book" class="com.lee.spring5.Book" p:bookName="Java" p:bookAuthor></bean>
   ```

   

3. 插入空值和特殊变量

   ```java
   <property name="address">
       <null/>
   </property>
   
   <property name="address">
       <value>
       <![CDATA <<南京>> ]>
       </value>
   </property>
   ```

#### 注入属性

##### 外部bean

1. 创建两个类service和dao
2. 在service中调用dao
3. spring配置文件中配置 

```
public class UserService {

//    创建UserDao类型属性，生成set
    private UserDao userDao;

    public void setUserDao(UserDao userDao) {
        this.userDao = userDao;
    }

    public void add(){
        System.out.println("Service add......");
//        原始方式
//        UserDao userDao = new UserDaoImpl();
        userDao.update();


    }
}

<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:p="http://www.springframework.org/schema/p"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
    <!--1 配置对象的创建-->
    <bean id="userService" class="com.lee.spring5.service.UserService">
        <!--注入userDao对象
            name:类中属性名
            ref:创建userDao对象bean标签id
        -->
        <property name="userDao" ref="userDaoImpl"></property>
    </bean>

    <bean id="userDaoImpl" class="com.lee.spring5.dao.UserDaoImpl"></bean>
</beans>
```

##### 内部bean和级联赋值

1. 一对多关系
2. 在实体类之间表示一对多

```
package com.lee.spring5.bean;

public class Dept {
    private String dname;

    public void setDname(String dname) {
        this.dname = dname;
    }
}

package com.lee.spring5.bean;

public class Emp {
    private String ename;
    private String gender;
    private String Dept;

    public void setDept(String dept) {
        Dept = dept;
    }

    public void setEname(String ename) {
        this.ename = ename;
    }

    public void setGender(String gender) {
        this.gender = gender;
    }
}
// 配置spring文件
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:p="http://www.springframework.org/schema/p"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="emp" class="com.lee.spring5.bean.Emp">
        <property name="ename" value="lucy"></property>
        <property name="gender" value="女"></property>

        <property name="dept">
            <bean id="dempt" class="com.lee.spring5.bean.Dept">
                <property name="dname" value="保安"></property>
            </bean>
        </property>

    </bean>
</beans>
```

##### 级联赋值

```
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:p="http://www.springframework.org/schema/p"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="emp" class="com.lee.spring5.bean.Emp">
        <property name="ename" value="lucy"></property>
        <property name="gender" value="女"></property>
        <property name="dept" ref="dept"></property>
    </bean>
    <bean id="dept" class="com.lee.spring5.bean.Dept">
        <property name="dname" value="保安"></property>
    </bean>
</beans>


// 第二种 需要get方法
    public Dept getDept() {
        return dept;
    }

    <bean id="emp" class="com.lee.spring5.bean.Emp">
        <property name="ename" value="lucy"></property>
        <property name="gender" value="女"></property>
        <property name="dept" ref="dept"></property>
        <property name="dept.dname" value="技术部"></property>

    </bean>
    <bean id="dept" class="com.lee.spring5.bean.Dept">
        <property name="dname" value="保安"></property>
    </bean>
    
 
```

#### 注入集合

##### 注入数组

```
// 创建对象
package com.lee.spring5.collctionType;

import java.util.List;
import java.util.Map;
import java.util.Set;

public class Stu {
    private String[] courses;
    private List<String> list;
    private Map<String, String> maps;
    private Set<String> sets;

    public void setSets(Set<String> sets) {
        this.sets = sets;
    }

    public void setCourses(String[] courses) {
        this.courses = courses;
    }

    public void setList(List<String> list) {
        this.list = list;
    }

    public void setMaps(Map<String, String> maps) {
        this.maps = maps;
    }
}

//配置文件

	<bean id="stu" class="com.lee.spring5.collctionType.Stu">
        <property name="courses" >
            <array>
                <value>java</value>
                <value>python</value>
            </array>
        </property>

        <property name="list">
            <list>
                <value>22</value>
                <value>33</value>
            </list>
        </property>

        <property name="maps">
            <map>
                <entry key="第一个" value="111"></entry>
                <entry key="第2个" value="222"></entry>
            </map>
        </property>

        <property name="sets">
            <set>
                <value>111</value>
                <value>222</value>
            </set>
        </property>
    </bean>
```

##### 给集合设置对象类型值

```
<bean id="course1" class="com.lee.spring5.collctionType.Course">
        <property name="cname" value="Spring5"></property>
    </bean>

    <bean id="course2" class="com.lee.spring5.collctionType.Course">
        <property name="cname" value="SpringBoot"></property>
</bean>

<bean>
 
<property name="courseList">
<list>
<ref bean="course1"></ref>
<ref bean="course2"></ref>
</list>
</property>

</bean>
```

##### 提取集合注入部分

1. 引入名称空间util

   ```
   <?xml version="1.0" encoding="UTF-8"?>
   <beans xmlns="http://www.springframework.org/schema/beans"
          xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xmlns:p="http://www.springframework.org/schema/p"
          xmlns:util="http://www.springframework.org/schema/util"
          xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
                              http://www.springframework.org/schema/util http://www.springframework.org/schema/util/spring-util.xsd">
   
   </beans>
   ```

2. 直接注入list

   ```
       <util:list id="bookList">
           <value>111</value>
           <value>222</value>
           <value>333</value>
       </util:list>
   
       <bean id="book" class="com.lee.spring5.collctionType.Book">
           <property name="list" ref="bookList"></property>
       </bean>
   ```

### Bean管理(FactoryBean)

1. 两种bean：普通bean，工厂bean
2. 普通bean：配置文件中定义类型即返回类型
3. **工厂bean：定义类型和返回类型不一样**
   1. 创建类，这个类作为工厂bean实现FactoryBean
   2. 实现方法，定义返回bean类型

```
package com.lee.spring5.FacBean;

import com.lee.spring5.collctionType.Course;
import org.springframework.beans.factory.FactoryBean;

public class MyBean implements FactoryBean {
    @Override
    public boolean isSingleton() {
        return FactoryBean.super.isSingleton();
    }

    @Override
    public Course getObject() throws Exception {
        Course course = new Course();
        course.setCname("a");
        return course;
    }

    @Override
    public Class<?> getObjectType() {
        return null;
    }
}
```

###  bean的作用域

1. 设置创建的bean实例为**单实例还是多实例**

2. 默认情况下为**单实例**

3. 设置多实例

   1. bean标签中scope属性

   2. 属性值：**singleton、prototype**

      ```
      <bean id="book" class="com.lee.spring5.collctionType.Book" scope="prototype">
          <property name="list" ref="bookList"></property>
      </bean>
      ```

   3. 区别

      1. singleton时，加载配置文件时就会创建单实例对象
      2. prototype在调用getBean时创建对象

### bean的生命周期

1. 通过构造器创建bean实例(无参数构造)
2. 为bean的属性设置值和对其他bean引用(调用set方法)
3. 调用bean的初始化方法(需要进行配置)
4. bean可使用(对象获取到了)
5. 容器关闭时，调用bean的销毁方法(需要配置销毁方法)

```
package com.lee.spring5.bean;

public class Orders {
    private String oname;

    public void setOname(String oname) {
        this.oname = oname;
        System.out.println("第二步，set属性");
    }

    public Orders() {
        System.out.println("第一步，无参构造");
    }

    public void initMethod(){
        System.out.println("第三步，执行初始化方法");
    }

    public void dertoryMethod(){
        System.out.println("第五步，销毁");
    }
}

<bean id="orders" class="com.lee.spring5.bean.Orders" init-method="initMethod" destroy-method="dertoryMethod">
        <property name="oname" value="手机"></property>
</bean>

@Test
public void testOrder(){
    ApplicationContext context =
            new ClassPathXmlApplicationContext("bean3.xml");
    Orders orders = context.getBean("orders", Orders.class);
    System.out.println("第四步，创建bean实例对象");
    System.out.println(orders);
    ((ClassPathXmlApplicationContext) context).close();
}
```

#### 加入bean的后置处理器

1. 通过构造器创建bean实例(无参数构造)
2. 为bean的属性设置值和对其他bean引用(调用set方法)
3. bean实例传递给bean后置处理器
4. 调用bean的初始化方法(需要进行配置)
5. bean实例传递给bean后置处理器
6. bean可使用(对象获取到了)
7. 容器关闭时，调用bean的销毁方法(需要配置销毁方法)

#### 添加后置处理器

```
package com.lee.spring5.bean;

import org.springframework.beans.BeansException;
import org.springframework.beans.factory.config.BeanPostProcessor;

public class MyBeanPost implements BeanPostProcessor {
    @Override
    public Object postProcessBeforeInitialization(Object bean, String beanName) throws BeansException {
        System.out.println("初始化之前");
        return bean;
    }

    @Override
    public Object postProcessAfterInitialization(Object bean, String beanName) throws BeansException {
        System.out.println("初始化之后");
        return bean;
    }
}
```

### xml自动装配

#### 什么是自动装配

根据指定装配规则(属性名称或属性类型)，Spring自动将装配的属性值进行注入

#### 如何自动

```
<bean id="emp" class="com.lee.spring5.Autowire.Emp" autowire="byName">
<!--<property name="dept" ref="dept"></property>-->
</bean>
<bean id="dept" class="com.lee.spring5.Autowire.Dept"></bean>
```

### 外部属性文件

#### 直接配置数据库信息

配置druid连接池

```
<bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource">
    <property name="driverClassName" value="com.mysql.jdbc.Driver"></property>
    <property name="url" value="jdbc:mysql://localhost:3306/userDb"></property>
    <property name="username" value="root"></property>
    <property name="password" value="root"></property>
</bean>
```

#### 引用外部属性文件配置数据库连接池

1. 创建外部属性文件，properties格式文件，写数据库信息

   ```
   prop.driverClass=com.mysql.jdbc.Driver
   prop.url=jdbc:mysql://localhost:3306/userDb
   prop.username=root
   prop.password=root
   ```

2. 把外部properties文件引入spring配置文件

   1. 引入context名称空间

      ```
      xmlns:util="http://www.springframework.org/schema/context"
      xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
                                 http://www.springframework.org/schema/util http://www.springframework.org/schema/util/spring-util.xsd
                                 http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd">
      ```

   2. ```
      <context:property-placeholder location="classpath:jdbc.properties"/>
      <bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource">
          <property name="driverClassName" value="${prop.driverClass}"></property>
          <property name="url" value="${prop.url}"></property>
          <property name="username" value="${prop.username}"></property>
          <property name="password" value="${prop.password}"></property>
      </bean>
      ```

## 基于注解

### 注解

1. @注解名称(属性名称=属性值...)
2. 使用注解可以作用在类、方法、属性上
3. 简化xml配置

### Spring为Bean管理提供的注解

#### @Component

#### @Service

#### @Controller

#### @Repository

### 基于注释方式实现对象创建

1. 引入依赖-aop

2. 开启组件扫描

   ```
   <!--    <context:component-scan base-package="com.lee.spring5.Dao, com.lee.spring5.Service"></context:component-scan>-->
   <!--    <context:component-scan base-package="com.lee"></context:component-scan>-->
   ```

3. 创建类，在类上面添加对象注解

   ```
   @Component(value="userService")// (value可省略)
   ```








# AOP

面向切面编程

利用AOP可以对业务逻辑的各个部分进行隔离，从而使得业务逻辑各部分之间的[耦合度](https://baike.baidu.com/item/耦合度/2603938)降低，提高程序的可重用性，同时提高了开发的效率。

## 底层原理(使用动态代理)

### 有接口情况，使用jdk的动态代理

![image-20211005102550131](https://raw.githubusercontent.com/RickLeee/ProgrammingBasics/main/img/image-20211005102550131.png)

### 没有接口，使用CGLIB动态代理

![image-20211005103013639](https://raw.githubusercontent.com/RickLeee/ProgrammingBasics/main/img/image-20211005103013639.png)

## 操作术语

### 连接点

类中哪些方法可以被增强的方法

### 切入点

实际被增强的方法

### 通知(增强)

实际增强的逻辑部分

类型：

1. 前置通知
2. 后置通知
3. 环绕通知
4. 异常通知
5. 最终通知

### 切面

动作-把通知应用到切入点的过程

## AOP操作

1. Spring框架一般都是基于AspectJ实现AOP操作

   1.  基于xml配置文件
   2.  **基于注解方式**

2. 在项目中引入AOP相关依赖

   ![image-20211215095415311](https://raw.githubusercontent.com/RickLeee/ProgrammingBasics/main/img/image-20211215095415311.png)

3. 切入点表达式

   1. 作用：知道对哪个类的哪个方法增强

   2. 语法：execution(\[权限修饰符\][返回类型]\[类全路径\]\[方法名称\]([参数列表]))

      如：execution(* com.lee.spring5.dao.BookDao.add(..))

      execution(* com.lee.spring5.dao.BookDao.* (..))

### 注解形式

#### 流程

```
@Component //增强类与被增强类中加入
@Aspect //生成代理对象
@Order(0)	//增强优先级 0最高
```

#### 相同切入点抽取

```java
@Pointcut(value = "execution(* com.lee.spring5.Service.UserService.add(..))")
public void point(){

}
@Before(value = "point()")
public void before(){System.out.pringln("before...")}
```

## JDBCTemplate

### 准备工作

#### 在spring配置文件中配置数据库连接池

```java
<!-- 数据库连接池 -->
<bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource"
      destroy-method="close">
    <property name="url" value="jdbc:mysql:///user_db" />
    <property name="username" value="root" />
    <property name="password" value="root" />
    <property name="driverClassName" value="com.mysql.jdbc.Driver" />
</bean>
```

#### 配置JdbcTemplate对象，注入DataSource

```
<bean id="jdbcTemplate" class="org.springframework.jdbc.core.JdbcTemplate">
    <property name="dataSource" ref="dataSource"></property>
</bean>
```

#### 创建service类，创建dao类，向dao类中注入jdbcTemplate对象

1. 开启组件扫描`<context:component-scan base-package="com.lee"></context:component-scan>`

2. 创建对象并注入dao

   1. Service

      ```
      @Service
      public class BookService {
      	// 注入dao
          @Autowired
          private BookDao bookDao;
      }
      ```

   2. Dao

      ```
      @Repository
      public class BookDaoImp implements BookDao {
      	//注入jdbcTemplate
          @Autowired
          private JdbcTemplate jdbcTemplate;
      }
      ```

### 操作数据库

#### 增删改与查询记录数

```
public class BookDaoImp implements BookDao {
    @Autowired
    private JdbcTemplate jdbcTemplate;

    @Override
    public void add(Book book) {
        String sql = "insert into book values(?,?,?)";
        Object[] args = {book.getUserId(), book.getUsername(), book.getUstatus()};
        int update = jdbcTemplate.update(sql, args);
        System.out.println(update);
    }
    // 查询记录数
    @Override
    public int selectCount(){
        String sql = "select count(*) from book";
        Integer count = jdbcTemplate.queryForObject(sql, Integer.class);
        return count;
    }
}
```

#### 查询返回对象

参数：

1. sql
2. RowMapper接口，返回不同类型数据，完成数据封装
3. sql语句值

```
@Override
public Book findBookInfo(String id) {
    String sql= "select * from book where user_id=?";
    Book book = jdbcTemplate.queryForObject(sql, new BeanPropertyRowMapper<Book>(Book.class), id);
    return book;
}
```

#### 批量操作

```
@Override
public void batchAddBook(List<Object[]> batchArgs) {
    String sql = "insert into book values(?,?,?)";
    int[] ints = jdbcTemplate.batchUpdate(sql, batchArgs);
    System.out.println(ints);
}
```

### 事务

#### 什么是事务

数据库操作最基本单元，逻辑上的一组操作，要么都成功，一个失败则都失败

如 银行转账1

#### 四个特性

1. 原子性A：不可分割，都成功
2. 一致性C：总量不变
3. 隔离性I：不同事务之间没影响
4. 持久性D：提交后表中数据变化

#### 搭建事务操作环境

##### 创建service，注入dao，完成对象创建和注入关系 

```
@Repository
public class UserDaoImp implements UserDao{
	//注入jdbc
    @Autowired
    private JdbcTemplate jdbcTemplate;

}

@Service
public class UserService {
	//注入dao
    @Autowired
    private UserDao userDao;
}
```

##### 基础转账环境

```
@Override
public void addMoney() {
    String sql = "update t_account set money=money-? where username=?";
    int update = jdbcTemplate.update(sql, 100, "lucy");
    System.out.println(update);
}

@Override
public void reduceMoney() {
    String sql = "update t_account set money=money+? where username=?";
    int update = jdbcTemplate.update(sql, 100, "mary");
    System.out.println(update);
}
```

#####  事务解决异常基本流程

```
try{
    //1.开启事务操作
    //2.进行业务操作
    userDao.addMoney();
    userDao.reduceMoney();
    //3.没有异常，提交事务
}catch (Exception e){
    //4.有异常，事务回滚
}
```

#### 注解声明式事务管理

1. spring配置文件中配置事务管理器

   ```
   <bean id="transactionManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">、
       <property name="dataSource" ref="dataSource"></property>
   </bean>
   ```

2. spring配置文件中开启事务注解

   1. 引入名称空间

      ```
      <beans xmlns="http://www.springframework.org/schema/beans"
             xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
             xmlns:p="http://www.springframework.org/schema/p"
             xmlns:context="http://www.springframework.org/schema/context"
             xmlns:aop="http://www.springframework.org/schema/aop"
             xmlns:tx="http://www.springframework.org/schema/tx"
             xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
                                  http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd
                                  http://www.springframework.org/schema/aop http://www.springframework.org/schema/aop/spring-aop.xsd
                                  http://www.springframework.org/schema/tx http://www.springframework.org/schema/tx/spring-tx.xsd">
      ```

   2.  开启事务注解

      `<tx:annotation-driven transaction-manager="transactionManager"></tx:annotation-driven>` 

3. service类方法上添加事务注解

   ```
   @Transactional
   ```

   可以添加到类(所有方法都会加上)或方法上
#### @Transactional中的参数配置

##### propagation:事务传播行为

多事务方法直接进行调用，这个过程事务如何管理![image-20211215213252429](https://raw.githubusercontent.com/RickLeee/ProgrammingBasics/main/img/image-20211216204915872.png)

` @Transactional(propagation = Propagation.REQUIRED)`

##### ioslation:隔离级别 

1. 隔离性：多事务操作之间不会产生影响
2. 不隔离的问题：脏读、不可重复读、幻读
   1. 脏读：一个未提交事务读取到另一个未提交事务的数据
   2. 不可重复读：一个未提交事务读取到另一个未提交事务修改数据
   3. 幻读：一个未提交事务读取到另一个未提交事务添加数据

 ![image-20211216204915872](https://raw.githubusercontent.com/RickLeee/ProgrammingBasics/main/img/image-20211215213252429.png)

` @Transactional(isolation = Isolation.REPEATABLE_READ)`

##### timeout:超时时间

1. 事务超过一定时间不提交就回滚
2. 默认-1

##### readOnly:是否只读

##### rollbackFor:回滚

##### noRollbackFor:不会滚

   
