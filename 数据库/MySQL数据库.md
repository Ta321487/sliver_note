## 第一部分：数据库

一、创建数据库

1. 数据库定义语言：DDL

   创建数据库、创建数据表（create/alter/drop)

2. 数据定义语言：DML

   数据库→数据表→列→约束

   创建数据库：```create database 数据库名;```

   如果数据库存在，则不提示错误：```create database if not exists 数据库名;```

二、查看MySQL服务器中所有的数据库：```show databases;```

四个系统级数据库：information_schema、performance_schema、mysql、sys

三、查看数据库的创建信息：```show create database 数据库名 \g;``` \g：纵向显示

四、删除数据库

​	delete：清空数据  |  drop：抛弃、丢弃

```drop database 数据库名;```

练习题：

①添加____________可在创建的数据库已存在时防止程序报错。 **```if not exists**```

②Mysql提供的___________可查看指定数据库的创建信息。```show create database 数据库名;```

③Mysql提供的___________可查看所有数据库。```show databases;```

## 第二部分：数据表

1. 选定数据库：```use 数据库名;```

2. 创建表

   ```SQL
   create table 表名(
   	列名1 数据类型 [约束],
       列名2 数据类型 [约束],
       ...
   )
   ```

3. 查看当前数据库中所有表：```show tables;```

4. 查看表：```show tables [like 匹配模式];```  |匹配模式：%多个字符；_一个字符

练习题：

包含good的表：```show table [like good];```

5. 查看表的创建信息：```show create table 表名;```
6. 查看表的字段信息：```desc 表名;```

## 第三部分：修改表

​	可修改表名、修改表的列名、修改列的数据类型、添加列、删除列

1. 修改表名

   ```sql
   alter table 旧表名
   rename to 新表名
   -- 或
   rename table 旧表名 to 新表名
   ```

例：把goods表名改为mygoods。

```sql
alter table goods
rename to mygoods;
   ```

2. 修改表的列名

```sql
alter table 表名
change 旧列名 新列名 数据类型;
```

例：将goods表中的列descrip改成des

```sql
alter table goods
change descrip des int
```

3. 修改列的数据类型

```sql
alter table 表名
modify 列名 新数据类型
```

4. 新增一列

```sql
alter table 表名
add 列名 数据类型 [first | after 列名]
```

   例：新增数量(num)列，类型为int

```sql
alter table 表名
add num int;
```

例：新增列  num1  int ，放在表的最前面
例：新增列 num2 int，在name后

5. 删除列

```sql
alter table 表名
drop 列名;
```

   ## 第四部分：数据增删改查（1）

1. 插入数据

   ```sql
   insert [into] 表名
   values(值1,值2,...) -- 注意值的个数、顺序、数据类型要和表的定义一致
   ```

2. 为部分列添加数据

   ```sql
   insert into 表(列1,列2...)
   values(值1,值2...)
   ```

3. 一次添加多行

   ```sql
   insert into 表名 values
   (值1,值2...),
   (值1,值2...),
   (值1,值2...),
   (值1,值2...),
   (值1,值2...),
   ...
   ```

4. 插入数据

   ```sql
   select * | 列1,列2...
   from 表名
   where 列 = 值
   ```

例：查询goods表中所有的数据

```sql
select *
from goods
```

例：查询goods表的商品名

```sql
select 商品名
from goods
```

例：查询id是2的商品信息

```sql
select *
from goods
where id = '2'
```

例：查询name是笔记本的商品信息

```sql
select *
from goods
where name = '笔记本'
```

5. 修改数据

   ```sql
   update 表名
   set 列 = 值, 列2 = 值...
   where 条件表达式
   ```

6. 删除数据

   ```sql
   delete from 表名
   where 条件表达式
   ```

例：删除笔记本1的信息

```sql
delete from goods
where name = '笔记本1'
```

## 第五部分：数据类型和约束

一、数据类型

1. 整数与浮点数类型

   1. 整数

      <table border = '1'>
          <tr><td>数据类型</td><td>占用字节</td><td>位数</td></tr>
          <tr><td>tinyint</td><td>1</td><td>-128~127</td></tr>
          <tr><td>smallint</td><td>2</td><td>-32768~32767</td></tr>
          <tr><td>int</td><td>4</td><td></td></tr>
          <tr><td>bigint</td><td>8</td><td></td></tr>
      </table>

      注意：  int（5）：显示位数
      显示宽度与取值 无关：
      若数值的位数小于显示宽度，用空格填充。   23
      若数值的位数大于显示宽度，正常显示，不受影响。

      报错信息：out of range value：超出范围

   2. 浮点数类型

      <table border = '1'>
          <tr><td>数据类型</td><td>占用字节</td><td>位数</td></tr>
          <tr><td>float</td><td>4</td><td>精度为6位或7位</td></tr>
          <tr><td>double</td><td>8</td><td>精度大约15位</td></tr>
      </table>

      decimal(M,D) D表示小数位数，M表示 整数+小数
      decimal(5,2)  小数位：2          整数位数：3
      小数超出范围，四舍五入 并警告。
      整数超出范围，错误，插入失败。

2. 日期和时间类型

   1. year：年份。用单引号括起 ```‘2022’```

      可以进行4位字符赋值，表示范围为```‘1901’~’2155’```

      或是2位字符，```‘00’~’99’``` 其中，```‘00’~’69’``` 表示的年份为2000~2069，```‘70’~’99’``` 表示的年份为1970~1999.

      字符```‘0’```表示的年份为2000，而数值```0```表示的年份则为0000

   2. date类型，日期(年月日)

      字符串：```‘YYYY-MM-DD’``` ,中间的连字符```-```可替换为```/```  ```,```  ```.```

      数值型：```YYYYMMDD```

      输入当前系统日期：```current_date```，```now()```

   3. time类型：时间

      字符串：```'HH:MM:SS'```

      数值：``HHMMSS``

      输入当前系统时间：``current_date``，```now()```

   4. datetime：日期+时间

      字符串：```‘YYYY-MM-DD HH:MM:SS’```   例：```’2022-3-2 12:34:23’```

      数值：```YYYYMMDDHHMMSS``` 例：```20220302123423```

      输入当前系统日期和时间：```now()```

   5. timestamp：时间戳（日期+时间）

      1. 比datetime范围小

      2. 使用```current_timestamp```来输入当前系统日期和时间

      3. 使用```on update current_timestamp```能够自动更改成修改时的系统日期和时间

         例：

         ```sql
         create table mytime(
         	t1 timestamp, int
             t2 timestamp default current_timestamp, int
             t3 timestamp default current_timestamp on update current_timestamp
         );
         ```



   复习：
       1. int（4）表示：是表示int的存储空间？不对，12354.不受影响
       2. 要保留2位小数，4位整数使用的数据类型是：decimal(6,2)
       3. 插入：34 ,0，‘0’转换成日期是：2034  0000   2000

3. 字符串类型

   1. char(字节数)：固定长度。例```char(4)```分配四个字节

   2. varchar(字节数)：可变长度，根据实际输入的数据进行分配字节

      例：```name varchar(20)``` 插入数据```‘李明’```，此时分配4个字节

   3. enum：枚举类型，选取其一（作用相当于单选按钮）

   4. set：类型，可以多选（作用相当于复选框）

   5. text：大文本数据类型，用于保存文章

   6. binary，biob：二进制存储（了解即可）

   7. 字符集和校对集

      字符集：utf8

      校对集：utf8_general_ci; 默认不区分大小写

      ​				utf8_bin：区分大小写

   例：让姓名区分大小写，修改name的校对集

   ```sql
   alter table student
   modify name varchar(20) character set utf8 collate utf8_bin
   ```

二、数据完整性约束

1. 实体完整性约束

   1. 主键：唯一标识一行记录，必须有，而且只能有一个

   2. 数据约束：主键值不能为空，不能重复

   3. ```primary key```：只能出现一次

      ```sql
      id int not null primary key -- 定义id为主键
      ```

      列级定义：一个属性做主键

      ```id int primary key,```

      表级定义：

      表后```primary key(属性1,属性2)```

   4. 删除主键

      ```sql
      alter table 表名
      drop primary key
      -- 不嫩同时把not null一并删除掉
      alter table 表名
      modify 列名 数据类型 null;
      ```

   5. 添加主键

      ```sql
      alter table 表名
      add primary key (字段)
      ```

   6. 自动增长：```auto_increment```

      1. 一个表只能有一个，必须是整数。必须是键

         ```sql
         id int unsigned primary key auto_increment
         ```

      2. 插入数据：NULL，0，default。默认都是用自动增长

      3. 输入大值：下次插入会从最大值 +1

      4. 删除记录：自动增长值不会减少或填补孔雀

      5. 清空数据：```truncate table 表名;```自动增长从1开始

         ```delete from 表名;``` 自动增长不受影响

      6. 修改自动增长

         ```alter table 表名 auto_increment = 40```

2. 用户自定义约束

   1. 非空：```not null```

   2. 默认：```default ‘默认值’```

   3. 唯一（键）：```unique```

   4. 添加、删除约束：非空、默认

      ```SQL
      alter table 表名
      modify 列名 数据类型; null没有默认值

      modify 列名 数据类型 not null |default '默认值' |unique;
      ```

   5. 删除唯一约束：index 索引对象

      ```sql
      alter table 表名
      drop index 列名;
      ```

   6. 添加唯一约束

      ```sql
      alter table 表名
      add unique (列名)
      ```

3. 参照完整性约束

   1. 外键：关联两个表的共同属性。是一个表的主键，在另一个表中是外键。

      ​			插入数据：外键值可以为NULL，可以重复

      ​			数据来源：来自主表主键的值域。

      ​			删除数据：主表中删除记录，要考虑从表的外键值，如果外键值存在，则不能删除。先删除从表的外键记录，再删除主表。

      ​			修改数据：主表中修改数据时，要考虑从表的外键值。如果外键值存在，则不能修改。要同时修改，才能保证数据一致

      ​			创建外键：

      ```sql
      [constraint 约束名] -- 约束名：fk_字段
      foreign key(外键字段) reference 主表(主键字段)
      {

      }
      on delete restrict | cascade | set null
      on update restrict | cascade | set null
      -- 说明：
      -- restrict：默认值。拒绝主表删除或修改外键关联的字段。
      -- cascade：级联操作。主表中删除或修改记录时，同时自动删除或修改从表对应的外键值。
      -- set  null：设置空。主表删除或修改主键值的记录，用NULL替换从表中对于的外键值。
      ```

      ​			删除外键（属于修改表的范畴）

      ```sql
      alter table 表名
      drop foreign key 约束名
      -- 同时删除索引
      alter table 表名
      drop key 约束名
      ```

## 第六部分：数据增删改查（2）

一、使用现有的sql语句进行导入操作（MySQL命令行）

“假设该资源在D盘下mysqldm目录下的shop.sql文件，则在命令行输入：

```source d:/mysqldm/shop.sql```

二、单表查询

```sql
select * |列名1 as 别名1,列名2 as 别名2 | distinct 列名| 表达式|函数
from 表名 -- 此处为单表
where 条件表达式
```

1. 查询所有商品信息

   ```sql
   select *
   from sh_goods;
   ```

2. 查询学生表学号、姓名信息

   ```sql
   select sno,sname
   from student;
   ```

3. 查找选课的学号

   ```sql
   select sno
   from sc;
   ```

4. 查找学生原始成绩和提高10%后的成绩

   ```sql
   select grade,grade*1.1
   from sc
   ```

5. 查找学生的出生日期，显示年龄

   ```sql
   select birth, year（now（））-year（birth）
   from student
   ```

三、where子句(有逻辑值，真或假)

1. 比较运算符：``` =，>，<，<=，<=，!=```

​		查找男学生的信息

```sql
select *
from student
where ssex = '男';
```

​		查找及格的学生成绩信息

```sql
select *
from student
where grade > 60
```

2. 确定范围：```between 小 and 大```

   ​					```not between 小 and 大```

   查找成绩70分~80分之间的学生信息

   ```sql
   select *
   from sc
   where grade>=70 and grade<=80
   -- 或
   -- where grade not between 70 and 80
   ```

3. 确定集合  ```in( , ,)```   ```not in() ```

   查找计算机系和数学系的学生信息

   ```sql
   where sdept = '计算机系' and sdept = '数学系' -- 错误，永远为假
   where sdept='计算机系'  or '数学系' -- 错误
   where sdept in('计算机系','数学系') -- 推荐
   where sdept='计算机系'  or sdept='数学系'   
   ```

   查询不是计算机系和数学系的学生信息

   ```sql
   where not （sdept='计算机系' or sdept='数学系'）
   where sdept！='计算机系'  and   sdept！='数学系'
   where sdept  not  in('计算机系','数学系') -- 推荐
   ```

   数学函数：

   ```format（x,y）```:保留数值x的小数位数y，并且四舍五入。
   ```truncate(x,y)```: 不进行四舍五入。
   ```floor（x）```：选取整数部分。
   ```rand（）```：返回随机0~1之间，包含0.  [0,1) .
   随机生成一个整数 1~10 [1,10)：```floor (1+rand()*(10-1))```

   随机生成一个整数 [min,max):  ```floor(min+rand()*(max-min))```

4. 模糊查询：like

   通配符：%：0或多个字符

   ​                _：1个字符

   查询姓刘的学生信息：```sname like ‘刘%’```

   查询以田结尾的学生信息：```sname like ‘%田’```

   查询姓名包含宝的学生信息：```sname like ‘%宝%’```

   查询姓刘，并且两个字的学生信息：```sname like ‘刘_’```

   查询1997年出生的学生信息：```where year(birth)=1997```

   ​                       ```where birth like ‘%1997%’```

   ​                      ```where birth >= ‘1997-1-1’ and birth <=‘1997-12-31’```

   查询1997年12月份出生的学生信息：```where birth like ‘%1997-12%’```

5. 空值查询：```is null```、```is not null```

   ```=null```是错误的写法

四、排序及限制子句

```sql
select
from
where
order by 字段 ASC | DESC  -- ASC：升序；DESC：降序
limit [起始位置.记录数]
   ```

显示学生的选课信息，成绩降序

```sql
select *
from sc
order by grade desc;
```

显示学生选课信息，学号升序，成绩降序

```sql
select *
from sc
order by sno asc grade desc;
```

查询成绩最高的学生信息

```sql
select *
from sc
order by grade desc
limit 1
```

综合应用：分页显示，每页显示4条记录

第一页：```limit 0,4```

第二页：```limit 4,4```

页的起始值：（第N页-1）*记录数

五、分组及聚合函数

```sql
select
from
where
group by
having
order by
limit
```

1. 聚合函数：select后可加，having后可加。但where后不可加

   ```count(*)```：返回行数，从1开始

   ```count(distinct 列)```：返回的是列的非空值的个数

   ```sum(列)```：必须数值类型，返回参数字段的总和

   ```max(列)```：必须数值类型，返回参数字段的最大值

   ```min(列)```：必须数值类型，返回参数字段的最小值

   ```avg(列)```：必须数值类型，返回参数字段的平均值

统计选课人数

```sql
select count(distinct sno) from sc
```

统计被选修的课程数

```sql
select count (distinct cno) from sc
```

统计学生的系的个数

```sql
select count(distinct sdept) from student
```

2. 分组

   ```sql
   select -- 后面可插入聚合函数，计算的次数是分组的个数 只能加group by后的列
   from
   where -- 对行进行过滤，先于分组执行
   group by -- 字段1，字段2   with  rollup ；对字段进行分组，分成几组（根据字段值的情况）
   having -- 对分组进行过滤
   order by
   limit
   ```

    聚合函数：```group_concat( 参数)```：返回参数值的连接字符串
                       ``` json_objectagg(参数1，参数2)```：返回单个JSON的对象。
                       ```json_arrayagg(参数)```  返回参数作为JSON数组。

在sh_goods表中统计每种商品的商品号（返回数组），每种商品的商品号（返回json对象）。显示商品分类，及每种商品的商品号。

```sql
select category_id,json_arryagg(id),json_objectagg(id,name)
from sh_goods
group by category_id
having count(distinct id)>2
```

​	where和having的区别：

​	时间：where先执行，having分组后执行

​	过滤：where对行过滤，having对组进行过滤

统计选修超过2门课的学生信息，显示，学号，课程数，选课课程号（返回数组）。

```sql
select sno,count(*) as cn,json_arrayagg(cno)
from sc
group by sno
having cno>2;
```

统计成绩在70分以上的，并且最大值超过80分的学生选课信息，显示，学号，成绩，选课课程号（返回数组）。

```sql
select sno,group_concat(grade),json_arrayagg(cno)
from sc
where grade>70
group by sno
having max(grade)>80
```

```group by 字段1，字段2：```

查询每个系的男女生人数。
第一次分组：对系

```sql
select sdept,group_concat(ssex),count(*)
from student
group by sdept;
   ```

 -第二次分组：基于系组的基础上 对每个系的性别分组

```sql
select sdept,ssex,count(*)
from student
group by sdept,ssex ;
   ```

```group by 字段1，字段2  with rollup；```对分组字段进行汇总。



## 第七部分 多表连接

​	①交叉连接  ②内连接  ③外连接

一、交叉连接：```from A,B|from A cross join B```

结果：列——A列 + B列

​			行——A行数 * B行数 （笛卡尔积的结果）

二、内连接：

```sql
from A as 别名 [inner] join B as 别名2 on 别名1.共有字段 = 别名2.共有字段 join C as 别名3 on 别名3.共有字段 = 其他表.共有字段
```

1. 查询李勇的成绩。显示学号，课程号，成绩（student,sc）

   ```sql
   select s1.sno,s2.cno,s2.grade
   from student as s1 join sc as s2 on s1.sno = s2.sno
   where s1.sname = '李勇'
   ```

2. 查询选修数据库原理的学生姓名（course,student,sc）

   ```sql
   select s1.sname
   from student as s1 join sc as s2 on s1.sno = s2.sno join course as s3 on s3.cno = s2.cno
   where s3.cname = '数据库原理'
   ```

3. 查询Java成绩最高的学生姓名、成绩

   ```sql
   select a.sno,a.sname,c.cname,b.grade
   from student a join sc b on a.sno=b.sno join course c on b.cno = c.cno
   where cname = 'Java'
   order by b.grade desc
   limit 1
   ```

4. 查询平均成绩大于70的信息。显示学号，姓名，平均成绩

   ```sql
   select s1.sno,s1,sname,avg(s2.grade)
   from student as s1 join sc as s2 on s1.sno = s2.sno
   group by s1.sno,s1.sname -- 不影响分组结果，相当于对学号进行分组
   having avg(s2.grade)>70
   ```

自身连接：

5. 查询和李勇一个系的学生的姓名

   ```sql
   select s1.sname
   from student as s1 join student as s2 on s1.sdept = s2.sdept
   where s2.sname = '李勇' and s1.sname!= '李勇'
   ```

6. 查询比李勇年龄大的学生姓名

   ```sql
   select s1.sname
   from student as s1 join student as s2 on s1.birth < s2.birth
   where s2.sname = '李勇'
   ```

三、外连接：左外连接、右外连接

1. 左外连接：```from A left [outer] join B```

   左表A的信息全都显示，B表中没有匹配的信息用NULL填充。

2. 右外连接：```from A right [outer] join B```

   右表B的信息全都显示，A表中没有匹配的信息用NULL填充。

查询没选课的学生信息。显示学号，姓名

```sql
select *
from student s left join sc s1 on s.sno = s1.sno
where s1.cno is null -- 该语句等效于s1.sno is null
```

显示没有被选修的课程信息

```sql
select *
from sc s right join course c on s.cno = c.cno
where s.cno is null
```

在商品分类表找没有被使用的分类id，name

```sql
select s1.id,s1.name
from  sh_goods_category s1 left join  sh_goods s2 on s1.id = s2.category_id
where s2.category_id is null;
```

 查询没有被评论的商品id，name。sh_goods , sh_goods_comment;

```sql
select s1.id,s1.name,s2.goods_id
from sh_goods as s1 left join sh_goods_comment as s2 on s1.id = s2.goods_id
where  s2.goods_id is  null
```

## 第八部分 子查询

内、外 不相关，子查询先执行，然后在执行外查询）。一个select语句 放在（select，insert，update,delete）中。

1. 标量子查询：子查询返回一行一列（一个值）

查询和李勇一个系的学生信息

步骤①：先查李勇的系：```select sdept from student where sname='李勇'```

步骤②：根据这个系查找该系的学生：

```sql
select * from student
where  sdept  = (
	select sdept
    from student
    where sname='李勇'  --  子查询
   )
and  sname!='李勇'
```

2. 2列子查询：返回多行一列

   ```where 列 in | not in (子查询)```

查询成绩大于80分的学生信息，显示学号，姓名。

步骤①：```select sno from sc where grade>80```

步骤②：查找学号和姓名

```sql
select sno ,sname
from student
where sno in (
	select distinct sno
    from sc
    where grade>80    -- 子查询
              )
-- 等效于使用多表连接：
-- select *
-- from student as s join sc as s1 on s.sno =s1.sno
-- where  grade>80;
```

3. 行子查询：子查询返回多列一行

```where （指定列1，指定列2）=（select 列1，列2  from ...）```

> (a,b) =（x,y）相当 于  a=x  and  b=y

在shop数据库中，sh_goods表中，查找价格最高，评分最低的商品的id，name，price，score。

注意：这种写法是错误的！

```where price = max(price) and score =min(price)```   聚合函数不能写在where后

正确写法：

步骤①：先找最高价格

```select max(price)  from sh_goods;```

步骤②：查找最低评分

```select  min(price) from sh_goods;```

步骤③：结合

```sql
select id,name,price,score
from sh_goods
where price = (
    select max(price)
    from sh_goods
	)
	and score =（
	select min(price)
	from sh_goods
	）
```

上述两个子查询可以改写为：

```where（price，score） = (select max(price),min(score) from sh_goods)```

4. 表级子查询

   ```from (子查询) as 表名 join...```

查询每种商品价格最高的商品id，name，price

步骤①：构造表：显示商品分类号，最高价格

```sql
(select category_id , max(price) as max1
from sh_goods
group by category_id) as a
```

步骤②

```sql
a join sh_goods as s on a.category_id = s.category_id and a.max1 = s.price
```

步骤③：结合

```sql
select s.id, s.name, s.price
from(
    select category_id,max(price) as max1
    from sh_goods
    group by categpry_id) as a join sh_goods as s on a.category_id = s.category_id and a.max1 = s.price
```

​	exist关键字：

查询选课的学生信息（sno,sname） 【用子查询】

1. 多表连接

   ```sql
   select distinct s1.sno,s1.sname
   from student as s1 join sc as s2 on s1.sno = s2.sno
   ```

2. 子查询

   ```sql
   select sno,sname
   from student
   where sno in
   {
   	select distinct sno
   	from sc
   }
   ```

3. exists

   ```sql
   select *
   from student
   where exists
   (
   	select *
       from sc
       where student.sno = sc.sno
   )
   ```

   执行逻辑：从外表的第一条记录开始执行，到内表中判断有没有满足条件的记录。如果有，返回1，外表的这条记录被保留；如果没有，返回0，外表的这条记录不被保留。

查询没有选课的学生信息

```sql
select *
from student
where not exists
(
	select *
    from sc
    where student.sno = sc.sno
)
```

查询没有被选修的课程名

```sql
select *
from course
where not exists
(
	select *
    from sc
    where course.cno = sc.cno
)
```

（带 ```in``` 的子查询可以被```exists```替代

查询成绩大于70的学号和姓名

用包含in的子查询写：

```sql
select sno,sname
from student
where sno in(
	select distinct sno
    from sc
    where grade>70
)
```

用exists写：

```sql
select *
from student
where exists(
	select *
    from sc
    where grade >70
)
```



shop数据库中，在商品表sh_goods中，将id为5的商品名改成电饭煲，价格修改为599，分类号修改为“厨具”的分类号。

分析：用到两个表：商品表(sh_goods)和商品分类表(sh_goods_category)

​			关系：一个商品只属于一个分类，一个分类有多个商品。故关系为多对一

​			外键：1端表的主键放到多端表中充当外键

```sql
update sh_goods
set name = '电饭煲', price = 599
category_id = (
	select id
    from sh_goods_category
    where name = '厨具'
)
where exists(
	select *
    from sh_goods_category
    where name = '厨具' -- 该子查询的目的是判断是否存在“厨具”分类，不存在则返回0
) and id = 5
   ```

修改表语句中的多表连接

```sql
update 表1 join 表2 on 连接条件
set 表1.字段 = 值,表1.字段2 =表2.字段3
where 表名.字段  -- 这是多表连接中条件
   ```

```sql
update sh_goods as s1 join sh_goods_category as s2 on s1.category_id = s2.id
set s1.name = '电饭煲',s1.price = 599,s1.category_id = (
	select id
    from sh_goods_category
    where name = '厨具'
)
where s2.name='厨具' and s1.id = 5
   ```

```>=ALL    :  > =  select  MAX()```

```<=ALL   :   <=   select  MIN()```

查询比分类3所有商品价格都高的商品信息

```sql
select *
from sh_goods
where price<(
	select max(price)
    from sh_goods
    where category_id = 3 -- 查找分类3的最低价格
)
```

```>ANY    :   >  min()```

```<ANY   :   <   max()```



insert子查询

1. 表的结构：

   ```create table 新表名 like 旧表名```

2. 数据的复制：

   ```sql
   insert into 表1
   select * from 表2 -- 表2和表1的结构相同
   ```

复制student，新表名studentCopy

```create table studentCopy like student```

集合查询：并（union），交（intersect），查(except)

例：查询计算机系和数学系的学生信息

```sql
where sdept in('计算机系','数学系')
   ```

-- union：自动去重复行 union all：不去重

查询：多表连接（内连接join，外连接left join，right join)

子查询（不相关子查询 标量子查询 = ，列子查询 in，行子查询 and，表子查询）

相关子查询(exists)：执行原理：从外层开始 >all >any union



## 第九部分：视图

一、视图的概念

1. 是从一个或几个基本表中导出的表，虚表，结构和数据都来源于基本表。
2. 视图就是存储了一个select 语句。所有对视图的数据操作都最终转换成对基本表的操作。

二、视图的优点

 	1. 安全性
 	2. 简化用户操作
 	3. 具有逻辑设计独立性

三、创建视图

```sql
create view 视图名(列名1,列名2...)
as
	select
	from
	where
	group by
	having
	order by
	limit
with check option; -- 在视图修改数据，满足where限定条件
```

1. 创建单表视图

   创建视图stu_j，视图显示计算机系的学生学号，姓名，系

   查询计算机系的学号，姓名，系

   ```sql
   create view stu_j
   as
   	select sno,sname,sdept
   	from student
   	where sdept='计算机系'
   ```

```desc 视图名; ```：查询视图的结构

2. 带有表达式或函数列的视图

   创建视图stu_age，显示学号、姓名、年龄

   ```sql
   create view stu_age(学号,姓名,年龄)
   as
   	select sno,sname,year(now()-year(birth))
   	from student
   ```

   （基于stu_age查询，查询年龄大于20岁的学生信息）

   ```sql
   select * from stu_age
   where 年龄 > 20
   -- 优点：简化用户的查询操作，不能提高运行效率
   ```

3. 带有统计的视图

创建视图s_count，显示每个学生的学号、总分、平均分

查询每个学生的学号，总分，平均分

```sql
create view s_count(学号,姓名,平均分)
as
	select sno,sum(grade),avg(grade)
    from sc
    group by sno
   ```

基于视图查询平均分大于70分的学生信息

```sql
select *
from s_count
where 平均分>70   -- 体现了简化用户操作的优点
```

4. 基于多表的视图

   创建视图s_sc，显示学生的选课信息。（学号，姓名，课程号，课程名，成绩）

   ```sql
   create view s_sc(学号,姓名,课程号,课程名,成绩)
   as
   	select a.sno,a.sname,c.cno,c.cname,b.grade
   	from student a join sc b on a.sno=b.sno join course c on b.cno = c.cno;
   ```

   查询王晓伟的Java成绩。

   ```sql
   select 成绩
   from s_sc
   where 姓名 = "王晓伟" and 课程名 = "java"
   ```

   表结构的变化对视图有影响，也对应用程序有影响，可以让应用程序直接操作视图

四、修改、删除视图

1. 修改视图

   ```sql
   alter view 视图名
   as
   	select ......
   ```

2. 删除视图

   ```sql
   drop view 视图名
   ```

五、视图的数据操作

​	增、删、改对数据有改变，查不会发生

增加基本表中不存在的列：可以用函数、表达式

多表连接的视图：不能更新和删除

```with check option```：为了确保视图的一致性，在创建或修改视图时使用该子句

查询计算机系的学号，姓名，系。插入或修改 限定只能是计算机系的。

```sql
alter view stu_j
as
	select sno,sname,sdept
    from student
    where sdept='计算机系'
with check option;
   ```

## 第十部分 DCL

一、创建用户

mysql.user表的相关信息

1. 用户在mysql.user表中 所有用户信息

2. 使用plugin验证插件名称，authentication_string：根据plugin指定的算法对密码加密生成的字符串

3. password_expired：密码是否过期

   password_last_changed：密码最后一次修改时间

   password_lifetime：密码的有效期限

4. 资源限制字段：max_开头

   max_question：每小时用户查询的最多次数

   max_updates：保存每小时允许用户执行更新操作的最多次数

   max_connection：保存每小时允许用户建立连接的最多次数

   默认值为0：没有资源限定

5. 权限字段：_priv结尾

   29个权限：select_priv，insert_priv，update_priv...

创建用户

```sql
create user 账号名@主机
identified by 密码;
```

例：创建一个用户名字为test53，本地登录，密码为123

```sql
create user 'test53'@'localhost'
identified by '123'
-- localhost：本地登录，只允许用户从本地主机连接MySQL服务器
-- % ：用户可以在任何主机连接MySQL服务器
```

一次创建多个用户

```sql
create user
账号名@主机 identified by 密码,
账号名@主机 identified by 密码;
```

创建用户时，设置操作资源范围

例：创建用户test56，本地用户，限制每小时最多可以更新10次

```sql
create user 'test56'@'localhost'
identified by '123' with max_updates_per_hour 10;
```

创建本地用户test57，设定密码每七天更新一次

```sql
create user 'test57'@'localhost'
identified by '123'
password expire interval 7 day;
```

修改密码

```sql
alter user 用户名@主机
identified by '密码'
```

例：修改本地用户test53的密码为er123

```sql
alter user 'test53'@'localhost'
identified by 'er123'
```

二、删除用户

```sql
drop user 用户名@主机;
```

例：删除本地用户test57

```sql
drop user 'test57'@'localhost'
-- 省略主机地址：默认为%
```

三、为用户分配权限

全局权限：grant 权限列表 on \**.\** to 账户名[with grant option]

数据库级权限：grant 权限列表 on 数据库名.\* to账户名[with grant option]

表级权限：grant 权限列表 on 数据库名.表名 to 账户名 [with grant option]

列级权限：grant 权限列表 (字段列表)[,...]on 数据库名.表名 to 账户名[with grant option]

例：为本地用户test53分配xuanke47的查询操作权限

```sql
grant select on xuanke47.*
to 'test54'@'localhost'
```

例：为本地用户test54 分配xuanke47下的学生表的查看操作权限。

```sql
grant select on xuanke47.student
to 'test54'@'localhost'
```

例：为本地用户test55分配xuanke47下的学生表的查看操作权限

```sql
grant select(sno,sname) on xuanke47.student
to 'test54'@'localhost'
```

四、回收用户权限

revoke 权限列表 on\*.\* from 账户名;

例：回收test57的对学生表的查询权限

```sql
revoke select on xuanke47.student
from 'test57'@'localhost'
```

## 第十一部分 事务

一、事务的概念

数据库中的一组操作，它可以由一条或多条SQL语句构成，且每个SQL相互依赖。

只要一条SQL执行失败，则其他语句都不会执行；要么全都不执行，要不全都执行

二、事务的特征（ACID）

1. 原子性

   一个事务必须视为一个不可分割的最小工作单元。只有事务的所有操作都成功，事务才成功；只要有一个操作失败，已经执行成功的SQL语句也必须撤销。数据库退回到事务执行前的状态。

2. 一致性

   无论事务成功还是失败，保持数据的一致性状态。

3. 隔离性

   一个事务在执行，不会受到其他事务的影响。直到事务完成，才能看到事务的结果（并发机制，锁，可串行化）

4. 持久性

   事务一旦提交，对数据库的修改就是永久性的

三、事务的基本操作

​	默认情况：每一条SQL语句都是单独的事务，自动提交。

​	事务是一组SQL语句，显式地开启事务：

```sql
start transaction;
sql1...
commit; | rollback;
-- commit：提交事务 | rollback：回滚事务（回到事务执行之前的状态）
```

例：Alex给Bill转账100

1. 查看Alex和Bill的钱数

2. ```sql
   # 开启事务
   start transaction
   # alex 的账号少100元
   update sh_user set money=money-100 where name = 'Alex';
   # bili 的账号多100元
   update sh_user set money=money+100 where name = 'bili';
   # 提交事务
   commit;
   ```

3. 事务的保存点

   回滚事务：事务内所有的操作都撤销，希望只撤销一部分，可以用保存点实现

   ```savepoint 保存点名;```

   回滚到指定的保存点：

   ```rollback to savepoint 保存点;```

四、事务的隔离级别

1. 读取未提交（read uncommitted）

   最低隔离级别，在该级别下的事务可以读取到其他事务中未提交的数据，这种读取方式也被称为“脏读”

   脏读：就是一个事务读取另外一个事务未提交的数据

   例：把bill 事务设置隔离级别 为 read uncommitted

   ```sql
   set session transaction isolation level read uncommitted
   ```

2. 读取提交（read committed）

   在该隔离级别下，只能读取其他事务已经提交的数据，避免了脏读

   例：把bill 事务设置隔离级别 为 read committed

   ```sql
   set session  transaction isolation level read committed;
   ```

```sql
# 开启事务
# 查看Alex 的金额
select money from sh_user
where name='alex';
```

```sql
#更改alex 减100
update sh_user
set money=money-100
where name='alex';
```

```sql
#查看Alex 的金额
select money from sh_user
where name='alex';
```

3. 可重复读（repeatable read）

   MySQL的默认隔离级别，它能解决脏读和不可重复读。确保同一个事务在并发读取数据时，会看到同样的结果

4. 可串行化：serializable

   每个读的行都加锁。影响数据的并发性。不会使用该级别





# 总复习



## 一、创建数据库及表

1. 基础概念

DB（数据库）、DBMS（数据库管理系统）、DBS（数据库系统）：

数据库是可共享的，冗余度低的数据的集合。

DBMS：数据库管理软件。MySQL，SQL server，Oracle

DBS：数据库系统。软硬件、人员

DBS>DBMS>DB

2. 创建数据库：```create database 数据库名;```

3. 创建表：**如何创建表，列的数据类型会根据实际分配，数据约束**

   例：创建一个用户表。id,name,sex,birth，要求主键自增长，性别为男女，默认男

   ```sql
   create table user(
   id int primary key auto_increment,
   name char(20),
   sex enum('男','女') default '男',
   birth datetime
   )
   ```

   1. 自动增长

      原有数据：1，2，3，4，6，7，90.再次插入数据，为91

   2. 数据类型

      定义整数：int(12)。12表示显示位数，而不是存储空间

      decimal(10,4)：存储的整数位是6，小数位是4

      decimal(23.4536743)：能插入，会出现警告

      年份：0和‘0’不同。0是0000年，‘0’是‘2000’年

      date类型：’1988-3-4’、’1988/3/4’ 数值输入：19880304

   3. 数据约束

      外键约束

      创建选课表SC(id,sno,cname,grade)

      ```sql
      create table SC(
      id int primary key auto_increment,
      sno int ,-- 外键的数据类型和主表一样
      cname varchar(20),
      grade int,
      foreign key(sno) references student(id)
          on delete restrict; -- 默认
          on update restrict; -- 默认
      )
      ```

   删除数据级联操作：cascade

例：

| 学号 | 姓名 |
| ---- | ---- |
| 1    | a    |
| 2    | b    |
| 3    | c    |

| id   | 学号 | 成绩 |
| ---- | ---- | ---- |
| 1    | 1    | 90   |
| 2    | 2    | 80   |

能进行表的操作的是：

主表：学生表。插入允许，删除不允许，修改不允许

从表：成绩表。插入(学号必须是学生表中已有的)

​						   修改(外键值必须参照主表)

​						   删除：没有要求

4. 查看表结构：```DESC 表名;```

   ```DESC table student```：错误

5. 查看表的创建信息：```show create table 表名```

6. 修改表

   新增一列：学生表新增班级名，放到name后

   ```sql
   alter table student
   add cname varchar(20) after name
   ```

7. 删除课程表

   ```drop 课程表;```：错误

   ```drop table 课程表;```：正确（结构和数据都删除）

## 二、数据操作

数据操作：更新，插入，修改，删除

1. 插入数据：student(id,name,sex,birth)

   ```sql
   -- 向学生表插入数据：6号,章鸣,女的学生信息
   insert into student values(6,'章鸣','女'，NULL);
   -- 或者
   --insert into student(id,name,sex) values(6,'章鸣','女')
   ```

2. 修改：修改3号学生birth改成1998年4月8号

   ```sql
   update student
   set birth = '1998-4-8'
   where id = 3
   ```

3. 删除：删除7号的学生记录

   ```sql
   delete from student
   where id = 7;
   ```

4. 清空选课表(sc)中的数据

```sql
delete from sc -- sc表结构存在，数据删除
```

## 三、查询

```sql
select
from
where
group by
having
order by asc | desc
limit
```

多表连接：内连接、外连接、左外连接、右外连接

子查询：where后面的子查询：标量（子查询返回一个值）、列、行子查询

​				from后面的子查询：表

​				exists，all，any

distinct：去重

统计：购买数量超过30的用户个数

| 用户 | 商品 | 数量 |
| ---- | ---- | ---- |
| 1    | 11   | 30   |
| 1    | 13   | 40   |
| 2    | 11   | 20   |
| 2    | 13   | 10   |
| 3    | 13   | 50   |

```sql
select count(distinct 用户)
from order
where 数量>30; -- 结果2
```

count：返回行数

| id   | 用户 | 商品() | 价格 | 是否发货 |
| ---- | ---- | ------ | ---- | -------- |
| 1    | 1    | 11     | 80   | 1        |
| 2    | 2    | 12     | 90   | null     |
| 3    | 2    | 13     | 80   | 0        |
| 4    | 2    | 13     | 40   | 0        |
| 5    | 3    | 12     | 20   | 1        |
| 6    | 3    | 13     | 70   | 0        |
```count(*)```：6

```count(status)```：5

```count(distinct goods_id)```：3  去掉good_id的重复值的行数

例：查询每个用户的购买商品的总价格、平均价格，并进行汇总

显示平均价格大于60元的信息，并对平均价格降序排序，显示前两条记录

```sql
select sum(price),ang(price)
from order
group by user_id
having avg(price)>60
order by avg(price) desc
limit 2
   ```

例：查询每个用户的购买商品的总价格，平均价格。并进行汇总

```sql
select sum(price),avg(price)
from order
   ```
