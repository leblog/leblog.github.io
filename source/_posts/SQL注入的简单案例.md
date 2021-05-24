---
title: SQL注入的简单案例
top: false
cover: false
toc: true
mathjax: true
date: 2018-10-17 20:40:42
password:
summary:
tags: [SQL,万能密码,SQL注入]
categories: SQL
---


# 什么是SQL注入

SQL注入是现在普通使用的一种攻击手段，就是通过把非法的SQL命令插入到Web表单中或页面请求查询字符串中，最终达到欺骗服务器执行恶意的SQL语句的目的。SQL注入一旦成功，轻则直接绕开服务器验证，直接登录成功，重则将服务器端数据库中的内容一览无余，更有甚者，直接篡改数据库内容等。
### 使用数据库客户端工具查询用户表

该表中有1个用户，账号为admin，明文密码为123456

![](https://note.youdao.com/yws/public/resource/b668ad7e2986aeae14431f59531ace89/xmlnote/6DCFD8AF50F74062B95CE1E4CDDE57C3/2811)


### 访问ERP系统（对密码输入框进行SQL注入）

- 用户名输入：随便输
- 密码输入：' OR '1'='1
![](https://note.youdao.com/yws/public/resource/b668ad7e2986aeae14431f59531ace89/xmlnote/3EA5BB79E7874011B25DFBD7AD9F7D79/2813)

- 发现可以登录进来
![](https://note.youdao.com/yws/public/resource/b668ad7e2986aeae14431f59531ace89/xmlnote/1D3A486CE18442C39F8BF5C05FD28348/2815)

### SQL注入的原理

密码验证的接口根据输入的用户名和密码查询数据表，如果查到用户记录的话，则认证通过。
代码如下:
```
    public boolean auth(String userName,String password) throws Exception{
        Connection conn = null;
        try {
            conn = DBUtil.getConnection();
            Statement state = conn.createStatement();
            //
            String sql = "SELECT * " +
                         "FROM t_user "+
                         "WHERE username='"+userName+"' " +
                         "AND pwd='"+password+"'";
            /*
             * 密码输入:
             * ' OR '1'='1
             * sql注入攻击
             * 
             */
            System.out.println(sql);
            
            ResultSet rs 
                = state.executeQuery(sql);
            //
            if(rs.next()){
                return true;
            }
        } catch (Exception e) {
            e.printStackTrace();
        } finally{
            if(conn != null){
                DBUtil.close(conn);
            }
        }
        return false;
    }

```

实际执行的sql语句如下：

>SELECT * FROM t_user WHERE username='1qwerwterrt' AND pwd='' OR '1'='1';

因为'1'='1'永远成立，导致能够查询到所有的用户，所以登录认证通过。

![](https://note.youdao.com/yws/public/resource/b668ad7e2986aeae14431f59531ace89/xmlnote/CC4DF51160B54463B9B3389E1479D9D5/2817)

### 解决方案

修改UserDAO类（使用shiro框架对输入的密码进行加密，然后再对数据库进行操作），具体步骤如下：

- 修改用户注册的接口
修改后，代码如下：
```
    /**
     * 增加用户信息(注册时用)
     * @param u
     * @throws Exception
     */
    public void save(User u)throws Exception{
        //设置盐巴
        String salt = new SecureRandomNumberGenerator().nextBytes().toString();
        //设置撒多少次盐巴
        int times = 2;
        //生成密文
        String encodedPassword = new SimpleHash("md5",u.getPwd(),salt,times).toString();
        Connection con = null;
        PreparedStatement pst = null;
        try{
            con = DBUtil.getConnection();
            pst = con.prepareStatement("insert into t_user(username,pwd,realname,gender,salt) values (?,?,?,?,?)");
            pst.setString(1,u.getUsername());
            pst.setString(2,encodedPassword);
            pst.setString(3,u.getName());
            pst.setString(4,u.getGender());
            pst.setString(5,salt);
            pst.executeUpdate();
        }catch(Exception e){
            e.printStackTrace();
            throw e;
        }finally{
            DBUtil.close(con);
        }       
    }
```
- 修改登录认证的接口

修改后，代码如下：
```
    /**
     * 登录认证
     * @param userName
     * @param password
     * @return
     * @throws Exception
     */
    public boolean auth(String userName,String password) throws Exception{
        Connection conn = null;
        User user = findByUserName(userName);
        if(user==null){
            return false;
        }
        //得到密文
        String encodePassword = new SimpleHash("md5",password,user.getSalt(),2).toString();
        try {
            conn = DBUtil.getConnection();
            Statement state = conn.createStatement();
            //
            String sql = "SELECT * " +
                         "FROM t_user "+
                         "WHERE username='"+userName+"' " +
                         "AND pwd='"+encodePassword+"'";
            //打印被执行的SQL语句
            System.out.println(sql);
            
            ResultSet rs = state.executeQuery(sql);
            //
            if(rs.next()){
                return true;
            }
        } catch (Exception e) {
            e.printStackTrace();
        } finally{
            if(conn != null){
                DBUtil.close(conn);
            }
        }
        return false;
    }
```

###  重新注册一个管理员账号

- 输入用户名：sys
- 输入密码：123456

![](https://note.youdao.com/yws/public/resource/b668ad7e2986aeae14431f59531ace89/xmlnote/3C2CF8B270C6492CBFE93A9816C06BA2/2819)

- 数据表里面sys用户的密码为密文
![](https://note.youdao.com/yws/public/resource/b668ad7e2986aeae14431f59531ace89/xmlnote/F9FB23BC189547068C8A1DA1DCC95BD3/2821)
### 使用sys账号登录ERP系统（输入正确的密码）

输入密码为：123456
![](https://note.youdao.com/yws/public/resource/b668ad7e2986aeae14431f59531ace89/xmlnote/203D1BF6D8964D4D8B6BCABF8F51CFFC/2823)

### 使用sys账号登录ERP系统（对密码输入框进行SQL注入）

输入密码为：' OR '1'='1
![](https://note.youdao.com/yws/public/resource/b668ad7e2986aeae14431f59531ace89/xmlnote/719FDB661CA24416B059AAD8E8852D5B/2825)
### UserDAO类的完整代码

代码如下：
```
package com.myerp.dao;

import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.Statement;

import org.apache.shiro.crypto.SecureRandomNumberGenerator;
import org.apache.shiro.crypto.hash.SimpleHash;

import com.myerp.model.User;
import com.myerp.utils.DBUtil;

/**
 * 针对用户表t_user的数据访问类
 * @author yangzc
 *
 */
public class UserDAO {
    /**
     * 按照username查询一个实体信息
     * 注册时用于检测用户名是否重复
     * 登录时用于检测用户名密码是否正确
     * @param userName
     * @return
     * @throws Exception
     */
    public User findByUserName(String userName)throws Exception{
        User user = null;
        Connection conn = null;
        PreparedStatement pst = null;
        ResultSet rs = null;
        try{
            conn = DBUtil.getConnection();
            pst = conn.prepareStatement("select * from t_user where username=?");
            pst.setString(1, userName);
            rs = pst.executeQuery();
            while(rs.next()){
                user = new User();
                user.setId(rs.getInt("id"));
                user.setUsername(rs.getString("username"));
                user.setPwd(rs.getString("pwd"));
                user.setName(rs.getString("realname"));
                user.setGender(rs.getString("gender"));     
                user.setSalt(rs.getString("salt"));
            }
        }catch(Exception e){
            e.printStackTrace();
            throw e;
        }finally{
            DBUtil.close(conn);
        }
        return user;
    }
    
    /**
     * 增加用户信息(注册时用)
     * @param u
     * @throws Exception
     */
    public void save(User u)throws Exception{
        //设置盐巴
        String salt = new SecureRandomNumberGenerator().nextBytes().toString();
        //设置撒多少次盐巴
        int times = 2;
        //生成密文
        String encodedPassword = new SimpleHash("md5",u.getPwd(),salt,times).toString();
        Connection con = null;
        PreparedStatement pst = null;
        try{
            con = DBUtil.getConnection();
            pst = con.prepareStatement("insert into t_user(username,pwd,realname,gender,salt) values (?,?,?,?,?)");
            pst.setString(1,u.getUsername());
            pst.setString(2,encodedPassword);
            pst.setString(3,u.getName());
            pst.setString(4,u.getGender());
            pst.setString(5,salt);
            pst.executeUpdate();
        }catch(Exception e){
            e.printStackTrace();
            throw e;
        }finally{
            DBUtil.close(con);
        }       
    }
    
    /**
     * 登录认证
     * @param userName
     * @param password
     * @return
     * @throws Exception
     */
    public boolean auth(String userName,String password) throws Exception{
        Connection conn = null;
        User user = findByUserName(userName);
        if(user==null){
            return false;
        }
        //得到密文
        String encodePassword = new SimpleHash("md5",password,user.getSalt(),2).toString();
        try {
            conn = DBUtil.getConnection();
            Statement state = conn.createStatement();
            //
            String sql = "SELECT * " +
                         "FROM t_user "+
                         "WHERE username='"+userName+"' " +
                         "AND pwd='"+encodePassword+"'";
            //打印被执行的SQL语句
            System.out.println(sql);
            
            ResultSet rs = state.executeQuery(sql);
            //
            if(rs.next()){
                return true;
            }
        } catch (Exception e) {
            e.printStackTrace();
        } finally{
            if(conn != null){
                DBUtil.close(conn);
            }
        }
        return false;
    }
}
```


