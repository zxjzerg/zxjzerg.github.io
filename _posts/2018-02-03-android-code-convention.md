---
layout: post
title:  "Android代码规范"
date:   2018-02-04 11:54:01 +0800
categories: jekyll update
---

## 1. 文件命名
### 1.1 Java类文件
* 遵循大驼峰命名法
* 如果是Android组件的子类如Activity、Fragment、自定义View等，增加组件名作为后缀，例如LoginActivity、UserHomeFragment、ConfirmExitDialog（注：自定义View使用Widget作为后缀，以避免和MVX设计模式中的View命名冲突）

### 1.2 资源文件
* 全小写并用下划线“_”分隔单词
* 布局文件（Layout XML）采用“组件_逻辑名”的格式，例如activity_login、fragment_user_detail、widget_star
* 同一图片的不同状态，参考**图片状态后缀表**加上相应的状态后缀，例如ic_email_normal、ic_email_press
* （可选）图片文件加上类型前缀，“ic”代表图标，“bg”代表背景图片。例如ic_launch、bg_splash

## 2. 变量命名
### 2.1 Java类变量
* 成员变量遵循小驼峰命名法
* 安卓控件类型的变量需要加上控件缩写的前缀，参考**安卓控件缩写表**，例如btnLogin、tvUsername
* 常量（static final）全大写并用下划线“_”分隔单词，例如SERVER_URL

### 2.2 资源文件id
* 资源文件的id命名遵循全小写并用下划线“_”分隔单词
* 资源文件的id命名格式参考**图片状态后缀表**加上前缀，例如

## 3. 编码习惯

### 3.1 Android相关

* 禁用Activity、Service、Application类型的静态变量，可能会导致这些对象在Android系统内存回收时无法被释放造成内存泄露
* 自定义View、Adapter中不允许编写业务逻辑逻辑代码，包括用户事件也需要通过监听器上传给上层业务逻辑单元进行处理

## 4. 参考
### 4.1 安卓控件缩写表

|     控件名      |   缩写   |      控件名       |  缩写   |
| :----------: | :----: | :------------: | :---: |
|    Button    |  btn   |    TextView    |  tv   |
|   EditView   |   et   |    CheckBox    |  cb   |
|  RadioGroup  |  rgrp  |  RadioButton   | rbtn  |
|   ListView   |   lv   |  RecyclerView  |  rv   |
| AlertDialog  | dialog |  PopupWindow   | popup |
| LinearLayout |  llyt  | RelativeLayout | rlyt  |
| FrameLayout  |  flyt  |   GridLayout   | glyt  |
|     View     |   v    |   ViewGroup    |  vg   |

### 4.2 图片状态后缀表

| 图片状态 |    后缀     |           例子           |
| :--: | :-------: | :--------------------: |
|  正常  |  _normal  |  btn_login_normal.png  |
|  点按  | _pressed  | btn_login_pressed.png  |
|  选中  | _selected | btn_login_selected.png |
| 不可用  | _disabled | btn_login_disabled.png |
|  焦点  | _focused  | btn_login_focused.png  |

