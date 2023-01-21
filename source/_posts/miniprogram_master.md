---
title: miniprogram_master
date: 2023-01-20 18:15:50
cover: assets/OIP-C.jfif
tags:
---

# miniprogram_master

## 组别验证码

<img src="https://images-1316609369.cos.ap-guangzhou.myqcloud.com/image-20230118224004953.png" alt="image-20230118224004953" style="zoom: 50%;" />



## 实现接口(学习前端代码)

我自己还要写很多的前端代码

```js
const app = getApp()

const defaultAvatarUrl = 'https://mmbiz.qpic.cn/mmbiz/icTdbqWNOwNRna42FI242Lcia07jQodd2FJGIYQfG0LAJGFxM4FbnQP6yfMxBgJ0F3YRqJCJ1aPAK2dQagdusBZg/0'


Page({

  getPhoneNumber (e) {
    console.log(e.detail.code)
  },

  data: {
// 图片地址
    avatarUrl: "https://lin-yueheng.oss-cn-shanghai.aliyuncs.com/img_for_typora/202301191901415.png",
    username: "",
    password: "",
    mobphone: "",
    check: "",
    wolfList: [{}],
    theme: wx.getSystemInfoSync().theme,
     //是否为密码框
     passwordType:true,
     // 是否显示密码
     show_pass:false,
  },

/*我写的

  //获取app.js中的数据
  getAppData(){
    var arr=getApp();
    this.data=getApp().data;
  },

    //提交表单注册
getData1:function () {
  wx.request({
    // url: 'http://localhost:8080/logins/check',  //测试
    url: 'https://person.hr16.top/logins/check',  //部署
    method:"POST",
    data:{
      name:this.data.username,
      code:this.data.check,
      mobile:this.data.mobphone,
      password:this.data.password
    },
    //调试中
    success: (res)=> {
      console.log(this.data.username)
  },
      fail: (res) => {
        console.log(this.data.username)
  },
  })
},


  //判断用户输入的数据是否配对
  getData2(that){
    wx.request({
      // url: 'http://localhost:8080/logins/goin', //测试
      url: 'https://person.hr16.top/logins/goin',  //部署
      method: "GET",
      success(res){
        that.setData({
        wolfList: res.data
        })
      }
    })
  },

     //点击注册，判断用户输入的名称以及组别验证码是否正确,true->跳转页面
  onRegister: function(){
      this.getData1();
      let u=false;      //用来判断该成员是否为野狼队的
      for (let i = 0; i < this.data.wolfList.length; ++i) {
      if(this.data.username==this.data.wolfList[i].username&&this.data.check==this.data.wolfList[i].code){
        u=true;       
        this.pageRouter.navigateTo({
      // 错误写法："/pages/homePage/homePage"
      url: '../homePage/homePage',
    })
      }
    }
      //false->
      if(!u){
        wx.showModal({
          title: '野狼成员专属',
          content: '请等程序猿优化以后再来登录！',
          success: function (res) {
            if (res.confirm) {//这里是点击了确定以后
              console.log('用户点击确定')
            } else {//这里是点击了取消以后
              console.log('用户点击取消')
            }
          }
        })
  }
    },

    //获取用户输入的名称，并传给data中的username
    username: function(res){
      this.setData({
        username: res.detail.value
      })
    },

    //同上
    password: function(res){
      this.setData({
        password: res.detail.value
      })
    },

    //同上
    mobphone: function(res){
      this.setData({
        mobphone: res.detail.value
      })
    },

    //同上
    check: function(res){
      this.setData({
        check: res.detail.value
      })
    },
    
    到这里
    */

  // onChooseAvatar(e) {
  //   const { avatarUrl } = e.detail 
  //   this.setData({
  //     avatarUrl,
  //   })
  // },
  
  seeTap:function(data){
    // 经常会在接口的sucess函数里边重置data{}数据，但是直接this.setData是不行的；须写成var that=this;
    var that = this; 
    that.setData({
      // 切换图标
      show_pass:!that.data.show_pass,
      // 切换是否密码框
      passwordType:!that.data.passwordType,
    })
  },
  // 获取页面输入为定义的username赋值
  getUserName(username){
    var that = this; 
    that.setData({
      username:that.username.detail.value
    })
  },
  // form 组件可以识别这些自定义组件，并在 submit 事件中返回组件的字段名及其对应字段值
  // e.detail.value.各组件的name属性
  formSubmit(e) {
    this.setData({
      username:e.detail.value.username,
      password:e.detail.value.password,
      mobphone:e.detail.value.mobphone,
      check:e.detail.value.check
    })
    // 检验数据是否传递成功的输出语句
    // console.log(this.data.username);
  },

  onLoad(option) {
    this.getAppData()
       wx.showToast({
         title: '首次登录默认注册',
         icon: 'none',
         duration: 1500//持续的时间
       })

    var that=this;
    // this.getData(that);
    this.getData2(that);
    wx.onThemeChange((result) => {
      this.setData({
        theme: result.theme
      })
    })
  },
})


```



学习：

![image-20230118155034334](https://images-1316609369.cos.ap-guangzhou.myqcloud.com/image-20230118155034334.png)



![image-20230115095409824](https://images-1316609369.cos.ap-guangzhou.myqcloud.com/image-20230115095409824.png)



![image-20230115100014492](https://images-1316609369.cos.ap-guangzhou.myqcloud.com/image-20230115100014492.png)



![image-20230115100041161](https://images-1316609369.cos.ap-guangzhou.myqcloud.com/image-20230115100041161.png)



![image-20230115103511046](https://images-1316609369.cos.ap-guangzhou.myqcloud.com/image-20230115103511046.png)



![image-20230115152156925](https://images-1316609369.cos.ap-guangzhou.myqcloud.com/image-20230115152156925.png)



### 常见错误描述

想传JSON数据，定义的domain类中成员变量不能含有下划线例，user_Name，是错误的！！！





模仿：

![image-20230118164512651](https://images-1316609369.cos.ap-guangzhou.myqcloud.com/image-20230118164512651.png)



### POST请求

找了半天才找到一个正确的！

```js
    //提交表单注册
getData1:function () {
  wx.request({
    url: 'https://person.hr16.top/logins/check',
    method:"POST",
    data:{
      name:this.data.username,
      code:this.data.check,
      mobile:this.data.mobphone,
      password:this.data.password
    },
    //调试中
    success: (res)=> {
      console.log(this.data.username)
  },
      fail: (res) => {
        console.log(this.data.username)
  },
  })
},
```







## 数据库设计

初步概要设计

average和teamsrank是一对多的关系

![image-20230119155337840](https://images-1316609369.cos.ap-guangzhou.myqcloud.com/image-20230119155337840.png)

![image-20230119153229260](https://images-1316609369.cos.ap-guangzhou.myqcloud.com/image-20230119153229260.png)



### 约束

![image-20230119161429453](https://images-1316609369.cos.ap-guangzhou.myqcloud.com/image-20230119161429453.png)



### 视图

![image-20230119102951720](https://images-1316609369.cos.ap-guangzhou.myqcloud.com/image-20230119102951720.png)





### @设计说明

#### teamsrank->1.0

由于用户在初次注册的时候，在相应的数据库中并没有相应的数据，因此在导出excel数据到teamsrank表的时候就必须先产生code验证码，队员输入相应的验证码以及相应的队员名称才能够注册登录。



### 前提概要

![image-20230117133751374](https://images-1316609369.cos.ap-guangzhou.myqcloud.com/image-20230117133751374.png)



![image-20230117133933043](https://images-1316609369.cos.ap-guangzhou.myqcloud.com/image-20230117133933043.png)



![image-20230117134056113](https://images-1316609369.cos.ap-guangzhou.myqcloud.com/image-20230117134056113.png)



![image-20230117134522180](https://images-1316609369.cos.ap-guangzhou.myqcloud.com/image-20230117134522180.png)



### 登录

<img src="https://images-1316609369.cos.ap-guangzhou.myqcloud.com/image-20230117104355478.png" alt="image-20230117104355478" style="zoom:25%;" />

![image-20230119225452075](https://images-1316609369.cos.ap-guangzhou.myqcloud.com/202301192254166.png)



### 任务列表

首先先拿到用户的姓名，通过姓名查询到自己的id，再将用户输入的内容insert到属于自己的个人任务中，也就是通过给定的user_id来确定是谁的任务。

<img src="https://images-1316609369.cos.ap-guangzhou.myqcloud.com/image-20230117104545409.png" alt="image-20230117104545409" style="zoom:25%;" />

![image-20230119225452075](https://lin-yueheng.oss-cn-shanghai.aliyuncs.com/img_for_typora/202301192254166.png)





#### 修改任务的信息

![image-20230119203224606](https://lin-yueheng.oss-cn-shanghai.aliyuncs.com/img_for_typora/202301192032696.png)



### 测试数据

<img src="https://images-1316609369.cos.ap-guangzhou.myqcloud.com/image-20230117104737869.png" alt="image-20230117104737869" style="zoom:25%;" />

![image-20230117125449843](https://images-1316609369.cos.ap-guangzhou.myqcloud.com/image-20230117125449843.png)

### 每周排行

<img src="https://images-1316609369.cos.ap-guangzhou.myqcloud.com/image-20230117105001722.png" alt="image-20230117105001722" style="zoom:25%;" />

![image-20230117104630605](https://images-1316609369.cos.ap-guangzhou.myqcloud.com/image-20230117104630605.png)

### ~~我的时长统计~~

<img src="https://images-1316609369.cos.ap-guangzhou.myqcloud.com/image-20230117110007766.png" alt="image-20230117110007766" style="zoom:25%;" />

### ~~我的完成记录~~

<img src="https://images-1316609369.cos.ap-guangzhou.myqcloud.com/image-20230117110216878.png" alt="image-20230117110216878" style="zoom:25%;" />





### 数据表测试

#### teamsrank

```sql
/*
 Navicat Premium Data Transfer

 Source Server         : cuteness
 Source Server Type    : MySQL
 Source Server Version : 50724
 Source Host           : localhost:3306
 Source Schema         : software

 Target Server Type    : MySQL
 Target Server Version : 50724
 File Encoding         : 65001

 Date: 18/01/2023 14:10:22
*/

SET NAMES utf8mb4;
SET FOREIGN_KEY_CHECKS = 0;

-- ----------------------------
-- Table structure for teamsrank
-- ----------------------------
DROP TABLE IF EXISTS `teamsrank`;
CREATE TABLE `teamsrank`  (
  `username` varchar(100) CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL,
  `groupname` varchar(100) CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL,
  `minstime` float(100, 2) NOT NULL,
  `users_id` int(20) NULL DEFAULT NULL,
  `id` int(10) NOT NULL AUTO_INCREMENT,
  PRIMARY KEY (`id`) USING BTREE
) ENGINE = InnoDB AUTO_INCREMENT = 112 CHARACTER SET = utf8 COLLATE = utf8_general_ci ROW_FORMAT = Dynamic;

```

#### users

```sql
/*
 Navicat Premium Data Transfer

 Source Server         : cuteness
 Source Server Type    : MySQL
 Source Server Version : 50724
 Source Host           : localhost:3306
 Source Schema         : software

 Target Server Type    : MySQL
 Target Server Version : 50724
 File Encoding         : 65001

 Date: 18/01/2023 14:06:47
*/

SET NAMES utf8mb4;
SET FOREIGN_KEY_CHECKS = 0;

-- ----------------------------
-- Table structure for users_copy1
-- ----------------------------
DROP TABLE IF EXISTS `users`;
CREATE TABLE `users`  (
  `name` varchar(10) CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL,
  `password` varchar(40) CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL,
  `mobile` bigint(15) NOT NULL,
  `code` varchar(40) CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL,
  `id` int(10) NOT NULL,
  `url` varchar(255) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL,
  PRIMARY KEY (`id`, `mobile`) USING BTREE,
  INDEX `mobile`(`mobile`) USING BTREE
) ENGINE = InnoDB CHARACTER SET = utf8 COLLATE = utf8_general_ci ROW_FORMAT = Dynamic;
```



#### problem

![image-20230118150422537](https://images-1316609369.cos.ap-guangzhou.myqcloud.com/image-20230118150422537.png)



