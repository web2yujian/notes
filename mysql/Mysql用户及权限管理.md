# Mysql

## 一、数据控制语言

- ### 用户管理

  - **用户数据所在位置**

    > mysql数据库的user表中

  - **创建用户**

    ```mysql
    create user '用户名'@'允许登录的地址' identified by '密码'
    create user 'xing'@'localhost' identified by 'xing123'
    ```

    > 注意：若授予该用户在所有的地址访问，则@后面为%

  - **删除用户**

    ```mysql
    drop user  '用户名'@'允许登录的地址'
    ```

  - **修改用户密码**

    - 修改自己的密码

      ```mysql
      set password = password('新密码')
      ```

    - 修改他人的密码

      ```mysql
      set password for '用户名'@'允许登录的地址' = password('新密码')
      ```

- ### 权限管理

  - **权限是什么**

    > 就是这些单词： `select`  `upadate`    `delete`   ,.....等

  - **授予权限**

    ```mysql
    grant 权限1.权限2，... on 某库.某下级对象 to '用户名'@'允许登录的地址' [identified by '密码']
    ```

    - 某库.某下级对象有两个特殊含义写法
      1. `  *.*`就是所有库中的所有下级对象
      2. `某库.*`就是该数据库的所有下级对象

    - 授予所有权限

      ```
      grant ALL PRIVILEGES on 某库.某下级对象 to '用户名'@'允许登录的地址' [identified by '密码']
      
      grant ALL PRIVILEGES on db_edu.* to mifeng@'%' identified by '123'
      
      GRANT ALL PRIVILEGES ON *.* TO zhou@"%" IDENTIFIED BY 'zhou';
      FLUSH PRIVILEGES;
      ```

  - **剥夺权限**

    ```mysql
    revoke 权限1.权限2，... on 某库.某下级对象 to '用户名'@'允许登录的地址'
    ```



```
revoke all privileges,grant option from 'ted'@'%';
```

```mysql
grant select,create,delete,update on db_oa.* to 'ted'@'%' with grant option;
```

```
grant select on *.* to 'ted'@'%' with grant option;
```

```
revoke all privileges,grant option from 'ted'@'%';
```

```
grant select,create,delete on db_oa.* to 'ted'@'%' with grant option;
```

revoke drop,alter on db_oa.* to 'ted'@'%' with grant option;