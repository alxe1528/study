## MySQL Server Product

 - mysqld 是服务器进程
 - mysql 是客户端命令行工具

### 1. mysqld服务

    [root@localhost ~]# service mysqld start #启动服务
    [root@localhost ~]# service mysqld stop #关闭服务
    [root@localhost ~]# service mysqld restart #重启服务
    [root@localhost ~]# /etc/rc.d/init.d/mysqld --verbose #查看服务所支持的参数
    Usage: /etc/rc.d/init.d/mysqld {start|stop|status|condrestart|restart}
    [root@localhost ~]# netstat -tnlp #查看服务是否启动成功

**mysql启动服务查找配置的顺序，并不是所有的版本都是一致，使用mysql --verbose --help可以找到当前版本查找的顺序**

1. /etc/my.conf
<pre>
[mysqld]片段中添加以下配置
default_storage_engine=InnoDB
sql_mode=STRICT_ALL_TABLES
</pre>
2. /etc/mysql/my.conf
3. $MYSQL\_HOME/my.conf `$MYSQL_HOME`环境变量设置的目录，如果没有设置，则找mysql数据目录，即`datadir=PATH`
4. --default-extra-file=<PATH/FILE> 启动mysqld服务使用此参数
5. ~/.my.conf 用户家目录下

**插件式存储引擎(表类型，表级别)**

  - MyISAM
  - CSV
  - MEMORY
  - MyISAMMRG
  - InnoDB
    <pre>
    innodb_file_per_table=ON 每张表使用单独的表空间文件
    </pre>
  - Federated
  - Archive
  - Blcakhole

### 2. mysql命令行

    [root@localhost ~]# mysql --verbose --help #显示mysql所支持的参数

**mysql命令的工作模式**

1.  交互式模式
<pre>
    mysql [options] db_name
      --user=user_name, -u user_name 默认为root
      --password[=password], -p[password] 默认为使用空密码登录。可以不输入密码直接进入交互模式下输入密码
      --host=host_name, -h host_name 默认是localhost
        -h localhost --> mysql.sock，基于进程间通信
        -h 127.0.0.1 --> 3306/tcp，基于TCP/IP协议通信
      --protocol={TCP|SOCKET|PIPE|MEMORY} 除了TCP协议，其余都是进程间通信，也就是说mysql和mysqld必须运行在同一台主机上
        SOCKET: Linux/Unix --> mysql.sock
        PIPE,MEMORY: Windows, IPC
      --port=port_num, -P port_num 连接服务器TCP/IP端口
      -e "COMMAND" 在shell命令执行mysql命令，并将结果返回到shell窗口里
        [root@localhost init.d]# mysql -e"show databases"
</pre>
2. 批处理模式

**mysql命令**
  1. 客户端命令：都不用使用命令结束符
  <pre>
    ?, help 显示帮助信息
    \c, clear 相当于Linux中的Ctrl + c取消执行当前的命令
    \d, delimiter 设置命令结束符
    \g, go 忽视命令结束符，将命令发送到服务器执行
    \G, ego 忽视命令结束符，将命令发送到服务器执行，并将结果以竖排方式显示
    \s, status 显示服务器状态信息
    \., source script_file 执行sql script
    \u, use db_name 切换数据库
    \!, system shell_command 执行系统shell命令
    \W, warnings 打开警告信息
    \w, nowarning 关闭警告信息
  </pre>
  2. 服务端命令：都必须使用命令结束符
  <pre>
    show global variables; 显示所有的配置参数
      动态参数：
        在服务运行时可直接改变的参数，在重启MySQL服务后动态设置的参数值会失效
      静态参数：
        在服务启动前设定好
    show global variables like '%sql_mode%'; 搜索某个配置参数
    show global status; 显示服务器状态
    show local variables;
    show local status;
    show session variables;
    show session status;
    set global|session|local sql_mode='STRICT_ALL_TABLES'; 设置配置参数的值。
      session立即生效
      global改变后的值只有新建立的回话才生效，用户必须有super权限才能修改
    show binary logs; 显示二进制日志
    show master status; 显示当前正在使用的二进制日志
    show processlist; 显示所有的服务器线程信息
    flush logs; 手动滚动二进制日志
    flush privileges; 重新加载授权信息
    show character set; 显示当前支持的字符集
    show collation; 显示当前支持的排序规则集
    show databases; 显示所有的数据库
    show tables; 显示当前数据中所有的表
    show table status; 显示当前数据库中所有表的相关信息
    show table status like'%TABLE_NAME%' [\G]; 在当前数据库中搜索某个表的信息
    show indexes from TABLE_NAME; 显示表中的索引信息
  </pre>
  <pre>
    mysql> help show
    Name: 'SHOW'
    Description:
    SHOW has many forms that provide information about databases, tables,
    columns, or status information about the server. This section describes
    those following:
    
    SHOW CHARACTER SET [like_or_where]
    SHOW COLLATION [like_or_where]
    SHOW [FULL] COLUMNS FROM tbl_name [FROM db_name] [like_or_where]
    SHOW CREATE DATABASE db_name
    SHOW CREATE FUNCTION func_name
    SHOW CREATE PROCEDURE proc_name
    SHOW CREATE TABLE tbl_name #显示create table ddl script
    SHOW DATABASES [like_or_where]
    SHOW ENGINE engine_name {LOGS | STATUS }
    SHOW [STORAGE] ENGINES
    SHOW ERRORS [LIMIT [offset,] row_count]
    SHOW FUNCTION CODE func_name
    SHOW FUNCTION STATUS [like_or_where]
    SHOW GRANTS FOR user
    SHOW INDEX FROM tbl_name [FROM db_name]
    SHOW INNODB STATUS
    SHOW PROCEDURE CODE proc_name
    SHOW PROCEDURE STATUS [like_or_where]
    SHOW [BDB] LOGS
    SHOW MUTEX STATUS
    SHOW OPEN TABLES [FROM db_name] [like_or_where]
    SHOW PRIVILEGES
    SHOW [FULL] PROCESSLIST
    SHOW PROFILE [types] [FOR QUERY n] [OFFSET n] [LIMIT n]
    SHOW PROFILES
    SHOW [GLOBAL | SESSION] STATUS [like_or_where]
    SHOW TABLE STATUS [FROM db_name] [like_or_where]
    SHOW TABLES [FROM db_name] [like_or_where]
    SHOW TRIGGERS [FROM db_name] [like_or_where]
    SHOW [GLOBAL | SESSION] VARIABLES [like_or_where]
    SHOW WARNINGS [LIMIT [offset,] row_count]
    
    like_or_where:
        LIKE 'pattern'
      | WHERE expr
    
    If the syntax for a given SHOW statement includes a LIKE 'pattern'
    part, 'pattern' is a string that can contain the SQL "%" and "_"
    wildcard characters. The pattern is useful for restricting statement
    output to matching values.
  </pre>

**mysqladmin命令，shell命令**
<pre>
mysqladmin [OPTIONS] command[arg] command[arg]....
  create new_db_name 创建数据库
  drop db_name 删除数据库
  password 'PASSWORD' 设置密码
  processlist 显示所有的服务器线程信息
  shutdown 停止mysql服务，会立即停止
  status 显示简要的服务器全局状态信息
    --sleep=2 每隔2秒显示一次
    --count=5 只显示5次
  extended-status 显示扩展的服务器全局状态信息
  variables 显示全局变量值信息
  version 显示mysqld的版本信息
  flush-hosts 清除缓存的host/dns等信息
  flush-logs 手动滚动二进制日志(mysql-bin.000001)
  flush-privileges 重新加载授权信息
  flush-status 重置大部分变量计数器
  flush-tables 关闭当前所有打开的表
  flush-threads 重置线程缓存
  refresh 相当于执行flush-hosts和flush-logs两个命令
</pre>

**查询用户**

    select user,host,password from user;

**修改用户密码**

1. 使用mysqladmin命令
<pre>
mysqladmin -u<USER> password <'PASSWORD'> [-p]
mysqladmin -u<USER> -h<HOST_NAME> password <'PASSWORD'> [-p]
  -p 修改用户密码，需要验证旧密码
</pre>
2. 在mysql命令中
<pre>
  1) set password for 'USER'@'HOST_NAME'=password('PASSWORD');
  2) update mysql.user set password=password('PASSWORD') where user='USER' and host='HOST_NAME';
  最后都需要执行flush privileges;
</pre>

**删除用户**

1. 在mysql命令中
<pre>
  1) drop user 'USER'@'HOST_NAME';
  2) delete from mysql.user where user='USER' and host='HOST_NAME';
</pre>

### 3. MySQL Server SQL Modes

- 四类常用的SQL Modes
<pre>
    ANSI 兼容ANSI标准
    TRADITIONAL 兼容传统数据库
    STRICT_TRANS_TABLES 用于支持事务的表上严格限制
    STRICT_ALL_TABLES 用于所有的表上严格限制
</pre>
- 设置sql_mode
<pre>
  1) set global|session|local sql_mode='STRICT_ALL_TABLES'; 重启后会失效
  2) 在/etc/my.cnf中的[mysqld]分段中添加如下配置，要重启MySQL服务后才会生效
  sql_mode=STRICT_ALL_TABLES
</pre>

### 4. MySQL数据类型
1. 数值型
  修饰符：not null, null, default #, unsgined(无符号), auto_increment(必须是主键或者唯一键)
  - 整数
<pre>
    数据类型   有符号取值范围                                     无符号取值范围                  字节大小
    TINYINT   -128~127(2^8/2-1)                                  0~255(2^8-1)                   1byte
    SMALLINT  -32768~32767(2^16/2-1)                             0~65535(2^16-1)                2bytes
    MEDIUMINT -8388608~8388607(2^24/2-1)                         0~16777215(2^24-1)             3bytes
    INT       -2147483648~2147483647(2^32/2-1)                   0~4294967295(2^32-1)           4bytes
    BIGINT    -9223372036854775808~9223372036854775807(2^64/2-1) 0~18446744073709551615(2^64-1) 8bytes
</pre>
  - 布尔型
<pre>
    BIT 取值：0或1
</pre>
  - 浮点数
<pre>
    FLOAT 4bytes
      float(p)
      floag(g,f)
    DOUBLE 8bytes
      double(g,f)
</pre>
  - 十进制
<pre>
    DECIMAL(g,f) g表示整体总共有多少位，f表示小数部分有多少位
    NUMERIC(g,f)
</pre>
2. 字符型
  修饰符：not null, null, default '', character set '', collation ''
  - 不区分字母的大小写，有字符集和排序规则，以文本方式保存数据
<pre>
    char(0~255), varchar(0~65532)
      char在搜索效率上要高于varchar
      varchar在存储空间上比char节省
    tinytext, text, mediumtext, longtext
</pre>
  - 区分字母大小写，没有字符集和排序规则，以二进制方式保存数据
<pre>
    binary(0~255), varbinary(0~65532)
    tinyblob(255bytes), blob(65535=16Kb), mediumblob(16777215=16Mb), longblob(4294967295=4Gb) 
</pre>
  - enum 枚举
<pre>
    数组范围：1~65535个
    example: enum('M','F')
</pre>
  - set 集合
3. 日期
  修饰符：not null, null, default
<pre>
  数据类型   取值范围                                    字节大小
  date      '1000-01-01'~'9999-12-31'                   3bytes
  datetime  '1000-01-01 00:00:01'~'9999-12-31 23:59:59' 8bytes
  time      '-838:59:59'~'838:59:58'                    3bytes
  timestamp '1970-01-01 00:00:00'~'2038-01-18 22:14:07' 4bytes
    修饰符
      with time zone
      without time zone
  year
    year(2) 00~99                                       1byte
    year(4) 1901~2155                                   1byte
</pre>

### 5. MySQL内置函数

```
 select current_date();
 select current_time();
 select database(); 显示当前use的数据库
```

### 6. sql statement大小写问题

1. SQL关键字和系统函数不区分大小写
2. database, table, view names是否区分大小写取决于文件系统
  - linux上是区分大小写的
  - windows上是不区分大写的
3. 存储过程，存储函数，事件调度器不区分大小写，触发器区分大小写
4. table aliases区分大小写
5. 对于字符串，binary类型的区分大小写；非binary类型的是否区分大小写取决于设置的字符集，一般不区分大小写

## DDL操作
查看语法帮助，如：`help create database`
- **create**, **drop**, **alter**
  - **database**
    - **创建数据库**

     <pre>
    CREATE {DATABASE | SCHEMA} [IF NOT EXISTS] db_name
        [create_specification] ...
    create_specification:
        [DEFAULT] CHARACTER SET [=] charset_name
      | [DEFAULT] COLLATE [=] collation_name
     </pre>

    - **修改数据库**

     <pre>
    ALTER {DATABASE | SCHEMA} [db_name]
        alter_specification ...
    alter_specification:
        [DEFAULT] CHARACTER SET [=] charset_name
      | [DEFAULT] COLLATE [=] collation_name
     </pre>

    - **删除数据库**

     <pre>
    DROP {DATABASE | SCHEMA} [IF EXISTS] db_name
     </pre>

  - **table**
    - **创建表**(TEMPORARY指临时表)

    <pre>
    CREATE [TEMPORARY] TABLE [IF NOT EXISTS] tbl_name
        (create_definition,...)
        [table_option] ...
    Or: 表结构和数据都会复制，表字段的约束会丢失
    CREATE [TEMPORARY] TABLE [IF NOT EXISTS] tbl_name
        [(create_definition,...)]
        [table_option] ...
        select_statement
    Or: 只复制表结构，表字段的约束不会丢失
    CREATE [TEMPORARY] TABLE [IF NOT EXISTS] tbl_name
        { LIKE old_tbl_name | (LIKE old_tbl_name) }

    create_definition:
        col_name column_definition
      | [CONSTRAINT [symbol]] PRIMARY KEY [index_type] (index_col_name,...)
            [index_type]
      | {INDEX|KEY} [index_name] [index_type] (index_col_name,...)
            [index_type]
      | [CONSTRAINT [symbol]] UNIQUE [INDEX|KEY]
            [index_name] [index_type] (index_col_name,...)
            [index_type]
      | {FULLTEXT|SPATIAL} [INDEX|KEY] [index_name] (index_col_name,...)
            [index_type]
      | [CONSTRAINT [symbol]] FOREIGN KEY
            [index_name] (index_col_name,...) reference_definition
      | CHECK (expr)

    column_definition:
        data_type [NOT NULL | NULL] [DEFAULT default_value]
          [AUTO_INCREMENT] [UNIQUE [KEY] | [PRIMARY] KEY]
          [COMMENT 'string'] [reference_definition]

    data_type:
        BIT[(length)]
      | TINYINT[(length)] [UNSIGNED] [ZEROFILL]
      | SMALLINT[(length)] [UNSIGNED] [ZEROFILL]
      | MEDIUMINT[(length)] [UNSIGNED] [ZEROFILL]
      | INT[(length)] [UNSIGNED] [ZEROFILL]
      | INTEGER[(length)] [UNSIGNED] [ZEROFILL]
      | BIGINT[(length)] [UNSIGNED] [ZEROFILL]
      | REAL[(length,decimals)] [UNSIGNED] [ZEROFILL]
      | DOUBLE[(length,decimals)] [UNSIGNED] [ZEROFILL]
      | FLOAT[(length,decimals)] [UNSIGNED] [ZEROFILL]
      | DECIMAL[(length[,decimals])] [UNSIGNED] [ZEROFILL]
      | NUMERIC[(length[,decimals])] [UNSIGNED] [ZEROFILL]
      | DATE
      | TIME
      | TIMESTAMP
      | DATETIME
      | YEAR
      | CHAR[(length)]
          [CHARACTER SET charset_name] [COLLATE collation_name]
      | VARCHAR(length)
          [CHARACTER SET charset_name] [COLLATE collation_name]
      | BINARY[(length)]
      | VARBINARY(length)
      | TINYBLOB
      | BLOB
      | MEDIUMBLOB
      | LONGBLOB
      | TINYTEXT [BINARY]
          [CHARACTER SET charset_name] [COLLATE collation_name]
      | TEXT [BINARY]
          [CHARACTER SET charset_name] [COLLATE collation_name]
      | MEDIUMTEXT [BINARY]
          [CHARACTER SET charset_name] [COLLATE collation_name]
      | LONGTEXT [BINARY]
          [CHARACTER SET charset_name] [COLLATE collation_name]
      | ENUM(value1,value2,value3,...)
          [CHARACTER SET charset_name] [COLLATE collation_name]
      | SET(value1,value2,value3,...)
          [CHARACTER SET charset_name] [COLLATE collation_name]
      | spatial_type

    index_col_name:
        col_name [(length)] [ASC | DESC]

    index_type:
        USING {BTREE | HASH | RTREE}

    reference_definition:
        REFERENCES tbl_name (index_col_name,...)
          [MATCH FULL | MATCH PARTIAL | MATCH SIMPLE]
          [ON DELETE reference_option]
          [ON UPDATE reference_option]

    reference_option:
        RESTRICT | CASCADE | SET NULL | NO ACTION

    table_option:
        {ENGINE|TYPE} [=] engine_name 表存储引擎
      | AUTO_INCREMENT [=] value
      | AVG_ROW_LENGTH [=] value
      | [DEFAULT] CHARACTER SET [=] charset_name
      | CHECKSUM [=] {0 | 1}
      | [DEFAULT] COLLATE [=] collation_name
      | COMMENT [=] 'string'
      | CONNECTION [=] 'connect_string'
      | DATA DIRECTORY [=] 'absolute path to directory'
      | DELAY_KEY_WRITE [=] {0 | 1}
      | INDEX DIRECTORY [=] 'absolute path to directory'
      | INSERT_METHOD [=] { NO | FIRST | LAST }
      | MAX_ROWS [=] value 最多存储多少行
      | MIN_ROWS [=] value
      | PACK_KEYS [=] {0 | 1 | DEFAULT}
      | PASSWORD [=] 'string'
      | ROW_FORMAT [=] {DEFAULT|DYNAMIC|FIXED|COMPRESSED|REDUNDANT|COMPACT}
      | UNION [=] (tbl_name[,tbl_name]...)

    select_statement:
        [IGNORE | REPLACE] [AS] SELECT ...   (Some legal select statement)
    </pre>

    - **修改表结构**

    <pre>
    ALTER [IGNORE] TABLE tbl_name
        alter_specification [, alter_specification] ...

    alter_specification:
        table_option ...
      | ADD [COLUMN] col_name column_definition
            [FIRST | AFTER col_name ]
      | ADD [COLUMN] (col_name column_definition,...)
      | ADD {INDEX|KEY} [index_name]
            [index_type] (index_col_name,...) [index_type]
      | ADD [CONSTRAINT [symbol]] PRIMARY KEY
            [index_type] (index_col_name,...) [index_type]
      | ADD [CONSTRAINT [symbol]]
            UNIQUE [INDEX|KEY] [index_name]
            [index_type] (index_col_name,...) [index_type]
      | ADD [FULLTEXT|SPATIAL] [INDEX|KEY] [index_name]
            (index_col_name,...) [index_type]
      | ADD [CONSTRAINT [symbol]]
            FOREIGN KEY [index_name] (index_col_name,...)
            reference_definition
      | ALTER [COLUMN] col_name {SET DEFAULT literal | DROP DEFAULT}
      | CHANGE [COLUMN] old_col_name new_col_name column_definition
            [FIRST|AFTER col_name]
      | MODIFY [COLUMN] col_name column_definition
            [FIRST | AFTER col_name]
      | DROP [COLUMN] col_name
      | DROP PRIMARY KEY
      | DROP {INDEX|KEY} index_name
      | DROP FOREIGN KEY fk_symbol
      | DISABLE KEYS
      | ENABLE KEYS
      | RENAME [TO] new_tbl_name
      | ORDER BY col_name [, col_name] ...
      | CONVERT TO CHARACTER SET charset_name [COLLATE collation_name]
      | [DEFAULT] CHARACTER SET [=] charset_name [COLLATE [=] collation_name]
      | DISCARD TABLESPACE
      | IMPORT TABLESPACE

    index_col_name:
        col_name [(length)] [ASC | DESC]

    index_type:
        USING {BTREE | HASH | RTREE}
    </pre>

    - **修改表名**

    <pre>
    ALTER TABLE tbl_name RENAME [TO] new_tbl_name
    RENAME TABLE tbl_name TO new_tbl_name
        [, tbl_name2 TO new_tbl_name2] ...
    </pre>

    - **删除表**

    <pre>
    DROP [TEMPORARY] TABLE [IF EXISTS]
      tbl_name [, tbl_name] ...
      [RESTRICT | CASCADE(会级联删除)]
    </pre>
  - **tablespace**
  - **trigger**
  - **view**
    - **创建视图**

    <pre>
    CREATE
        [OR REPLACE]
        [ALGORITHM = {UNDEFINED | MERGE | TEMPTABLE}]
        [DEFINER = { user | CURRENT_USER }]
        [SQL SECURITY { DEFINER | INVOKER }]
        VIEW view_name [(column_list)]
        AS select_statement
        [WITH [CASCADED | LOCAL] CHECK OPTION]

    </pre>

    - **删除视图**

    <pre>
    DROP VIEW [IF EXISTS]
        view_name [, view_name] ...
        [RESTRICT | CASCADE]

    </pre>

  - **envent**
  - **function**
  - **index**
    - 创建索引

    <pre>
    CREATE [UNIQUE|FULLTEXT|SPATIAL] INDEX index_name
        [index_type]
        ON tbl_name (index_col_name,...)
        [index_type]

    index_col_name:
        col_name [(length)] [ASC | DESC]

    index_type:
        USING {BTREE | HASH | RTREE}
    </pre>
  - **logfile group**
  - **procedure**

## DML操作
- **insert**

<pre>
INSERT [LOW_PRIORITY | DELAYED | HIGH_PRIORITY] [IGNORE]
    [INTO] tbl_name [(col_name,...)]
    {VALUES | VALUE} ({expr | DEFAULT},...),(...),...
    [ ON DUPLICATE KEY UPDATE
      col_name=expr
        [, col_name=expr] ... ]
  example：如果已经存在则update，不执行insert操作
  insert into user (id,name,age) values (1,'Jerry',18) on duplicate key update id=1,name='Jerry',age=18;

Or:
INSERT [LOW_PRIORITY | DELAYED | HIGH_PRIORITY] [IGNORE]
    [INTO] tbl_name
    SET col_name={expr | DEFAULT}, ...
    [ ON DUPLICATE KEY UPDATE
      col_name=expr
        [, col_name=expr] ... ]

Or:
INSERT [LOW_PRIORITY | HIGH_PRIORITY] [IGNORE]
    [INTO] tbl_name [(col_name,...)]
    SELECT ...
    [ ON DUPLICATE KEY UPDATE
      col_name=expr
        [, col_name=expr] ... ]
</pre>

- **replace**

<pre>
REPLACE [LOW_PRIORITY | DELAYED]
    [INTO] tbl_name [(col_name,...)]
    {VALUES | VALUE} ({expr | DEFAULT},...),(...),...

Or:
REPLACE [LOW_PRIORITY | DELAYED]
    [INTO] tbl_name
    SET col_name={expr | DEFAULT}, ...

Or:
REPLACE [LOW_PRIORITY | DELAYED]
    [INTO] tbl_name [(col_name,...)]
    SELECT ...
</pre>

- **update**

<pre>
Single-table syntax:
UPDATE [LOW_PRIORITY] [IGNORE] table_reference
    SET col_name1={expr1|DEFAULT} [, col_name2={expr2|DEFAULT}] ...
    [WHERE where_condition]
    [ORDER BY ...]
    [LIMIT row_count]

Multiple-table syntax:
UPDATE [LOW_PRIORITY] [IGNORE] table_references
    SET col_name1={expr1|DEFAULT} [, col_name2={expr2|DEFAULT}] ...
    [WHERE where_condition]
</pre>

- **delete**

<pre>
Single-table syntax:
DELETE [LOW_PRIORITY] [QUICK] [IGNORE] FROM tbl_name
    [WHERE where_condition]
    [ORDER BY ...]
    [LIMIT row_count]

Multiple-table syntax:
DELETE [LOW_PRIORITY] [QUICK] [IGNORE]
    tbl_name[.*] [, tbl_name[.*]] ...
    FROM table_references
    [WHERE where_condition]

Or:
DELETE [LOW_PRIORITY] [QUICK] [IGNORE]
    FROM tbl_name[.*] [, tbl_name[.*]] ...
    USING table_references
    [WHERE where_condition]
</pre>

- **truncate** [TABLE] tbl_name 清空表，对于auto_increment字段会重新记数

- **select**

<pre>
SELECT
    [ALL | DISTINCT | DISTINCTROW ]
      [HIGH_PRIORITY]
      [STRAIGHT_JOIN]
      [SQL_SMALL_RESULT] [SQL_BIG_RESULT] [SQL_BUFFER_RESULT]
      [SQL_CACHE | SQL_NO_CACHE] [SQL_CALC_FOUND_ROWS]
    select_expr [, select_expr ...]
    [FROM table_references
    [WHERE where_condition]
    [GROUP BY {col_name | expr | position}
      [ASC | DESC], ... [WITH ROLLUP]]
    [HAVING where_condition]u
    [ORDER BY {col_name | expr | position}
      [ASC | DESC], ...]
    [LIMIT {[offset,] row_count | row_count OFFSET offset}]
    [PROCEDURE procedure_name(argument_list)]
    [INTO OUTFILE 'file_name' export_options
      | INTO DUMPFILE 'file_name'
      | INTO var_name [, var_name]]
    [FOR UPDATE | LOCK IN SHARE MODE]]
</pre>

- **join**

<pre>
MySQL supports the following JOIN syntaxes for the table_references
part of SELECT statements and multiple-table DELETE and UPDATE
statements:

table_references:
    table_reference [, table_reference] ...

table_reference:
    table_factor
  | join_table

table_factor:
    tbl_name [[AS] alias] [index_hint)]
  | table_subquery [AS] alias
  | ( table_references )
  | { OJ table_reference LEFT OUTER JOIN table_reference
        ON conditional_expr }

join_table:
    table_reference [INNER | CROSS] JOIN table_factor [join_condition]
  | table_reference STRAIGHT_JOIN table_factor
  | table_reference STRAIGHT_JOIN table_factor ON conditional_expr
  | table_reference {LEFT|RIGHT} [OUTER] JOIN table_reference join_condition
  | table_reference NATURAL [{LEFT|RIGHT} [OUTER]] JOIN table_factor

join_condition:
    ON conditional_expr
  | USING (column_list)

index_hint:
    USE {INDEX|KEY} [FOR JOIN] (index_list)
  | IGNORE {INDEX|KEY} [FOR JOIN] (index_list)
  | FORCE {INDEX|KEY} [FOR JOIN] (index_list)

index_list:
    index_name [, index_name] ...
</pre>


## 服务器缓存

查看sql执行分析计划

    explain SELECT_SQL; 

- 服务器是否启动缓存功能：server variables
  - 查询缓存：show global variables like 'query_cache%';

   <pre>
    query_cache_size 用于缓存的内存空间大小，以字节为单位，必须是1024的倍数
    query_cache_min_res_unit 分配缓存块的最小值
    query_cache_limit 存储缓存内容的最大结果
    query_cache_wlock_invalidate 是否缓存其它联结已经锁定的表
   </pre>

- 缓存工作统计数据查看：status variables

  <pre>
   show global status like '%qcache%';
  </pre>