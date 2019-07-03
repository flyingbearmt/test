##数据库：
Complete SELECT query  
SELECT DISTINCT column,   
AGG\_FUNC(column\_or\_expression), …  
FROM mytable  
    JOIN another\_table  
      ON mytable.column = another\_table.column  
    WHERE constraint\_expression  
    GROUP BY column  
    HAVING constraint\_expression  
    ORDER BY column ASC/DESC  
    LIMIT count OFFSET COUNT;
    
1. 事务的四个特性：acid, 原子性（atomic),一致性（consistancy), 独立性（isolation）持久性（duarable）
2. 数据库的基本操作
	- 选择
	- 投影： 会把重复的行删除
	- 并： 重复的还是会删除，（U）要等目，同源（类型相同）
	- 集差： r－s
	- 笛卡尔积： （矩阵相乘），如果在两个关系中有同名的属性，我们还是把它们看作是不同的属性。（r中有B, s中有B，结果是r.B,s.B）
	- 复合运算（可以使用多种）
	- 更名运算 
	
3. 附加操作
	- 集合交
	- 自然连接
	- 除：r／是（包含所有s的r集合
	- 赋值
	
4. super-key －》
	candidate-key －》
	primary-key
	层层深入
	
5. 基本数据类型 
	- char：（n）固定长度
	- varchar（n）：可变长，最大为n
	- int
	- smallint
	- numeric(p,d): 定点数，p位数字，小数点后d位
	- real,double precision
	- float（n）：精度至少为n
	- null
6. 对表的操作
	- CREATE TABLE
	- DROP TABLE ：删除属性
 	- ALTER TABLE： 修改属性

####SQL查询语句

1. 查询
	SELECT FROM WHERE
	默认是不去除重复的，如果想要去除重复，可以使用：
	- select destinct _dept\_name_
	from _instructurr_
	- 可以显式的指明不去除，用all
 	- 可以使用 ＊ 表示所有的属性
 	- where 选出在from 子句中满足特定谓词的
 	- 可以使用 and，or，not，between
 	- from 是笛卡尔积
 	- 为关系和属性重新命名， as:
 		_old\_name_ as _new\_name_
 	- 字符串的运算，like （％：匹配任意子串，_匹配任意一个字符） 
	- 	order by : ordered 顺序显示(desc 表示降序， asc 升序）默认是升序 
	-  聚集函数： avg, min, max, sum, count