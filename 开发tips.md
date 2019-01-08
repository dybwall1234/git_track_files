# 操作系统
glibc gcc
glibc 升级 https://www.cnblogs.com/madsnotes/articles/7264150.html 
rpm -Uvh *.rpm 不要源码安装 错了以下命令改回去
LD_PRELOAD=/lib64/libc-2.15.so ln -s /lib64/libc-2.15.so  lib64/libc.so.6

# Python
virtualenv
优点：
1，non-root包管理
glibc 问题，单机：/opt/compiler/gcc-4.8.2/lib/ld-linux-x86-64.so.2 --library-path /opt/compiler/gcc-4.8.2/lib /root/.jumbo/bin/python
集群 先用docker测试

# Docker
镜像
container 实例 退出即销毁 可以commit到镜像

# Mysql问题
连接池
commit
问题1：Commands out of sync; you can't run this command now
解决 1. cursor.nextset()
    2. cursor.close()再重启
    3. UPDATE DELETE INSERT需要commit
参考：http://blog.csdn.net/lee_zix/article/details/52216126
http://blog.csdn.net/gukesdo/article/details/7026371

本机不能登录问题，安装后mysql_secure_installation
https://stackoverflow.com/questions/1412339/cannot-log-in-with-created-user-in-mysql

## 代码规范
1. 函数返回值必须小于等于3个。3个以上时必须通过class/namedtuple/dict等具名形式进行包装
2. 命名规则
    `ClassName, ExceptionName
    
    GLOBAL_CONSTANT_NAME, CLASS_CONSTANT_NAME,
    
    module_name, package_name, method_name, function_name, global_var_name, instance_var_name, function_parameter_name, local_var_name
    
    _InternalClassName, _INTERNAL_CONSTANT_NAME, _internal_function_name, _protected_member_name, __private_member_name`
3. 圆括号、方括号、花括号内侧都不加空格
4. True/False求值
5. 对容器或文件的只读遍历，应该使用内置的迭代方法，不要使用返回list的方式遍历。
6. 对容器类型，使用in或not in判断元素是否存在。而不是has_key。
7. 捕捉异常时，应当使用as语法，禁止使用逗号语法。

# Java，scala
jdk 百度盘
## maven
install到本地仓库
system本地依赖包
assembly打包with-dependcies

# 习惯
1. 命名
2. 快速测试

# awk sed
`sed 's/^A/\t/g' file` ctrl+V+A
`awk -F'.' '{IGNORECASE=1} $1 == "PoiListPG" {print $2}'`

# 分隔符
hive \001 spark


