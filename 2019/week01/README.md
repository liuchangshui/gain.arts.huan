# ATRS WEEK01 (0408-0414)
## Algorithm 
### 题目
```
1. Two Sum

Given an array of integers, return indices of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

Example:
	Given nums = [2, 7, 11, 15], target = 9,

	Because nums[0] + nums[1] = 2 + 7 = 9,
	return [0, 1].
```

### 解法 1
```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        int[] result = new int[2];
        for(int i=0; i<nums.length; i++){
            int tempInt = nums[i];
            for(int j=i+1; j<nums.length; j++){
                if(target == (tempInt + nums[j])){
                    result[0] = i;
                    result[1] = j;
                    return result;
                }
            }
        }
        return null;
    }
}
```

### 解法 2
```java
import java.util.HashMap;

class Solution {
    public int[] twoSum(int[] nums, int target) {
        HashMap<Integer,Integer> hashMap = new HashMap<Integer,Integer>();
        for(int i=0; i<nums.length; i++){
            int tempResult = target - nums[i];
            if(hashMap.containsKey(tempResult)){
                return new int[] {hashMap.get(tempResult),i};
            }
            hashMap.put(nums[i],i);
        }
        return new int[] {0,0};
    }
}
```

## Review
### [HTTPS explained with carrier pigeons](https://medium.freecodecamp.org/https-explained-with-carrier-pigeons-7029d2193351)

### 阅读笔记

	这是一篇关于https介绍的文章，文章采用信鸽传递信息来做类比，从而找到解决信息传递安全性的方案。全文划分为七部分：
	1、行文方式介绍（说明文章将采用信鸽做类比，来描述HTTPS的运行原理）
	2、HTTP传输原理与弊端、信息对称加密原理（字母位移举例）
	3、对称加密秘钥传输安全性问题提出（中间人攻击）
	4、非对称加密解决方案提出，解决秘钥传输安全性问题（公钥与私钥联合使用）
	5、公钥与私钥信任问题提出与解决（CA认证）
	6、HTTPS为解决非对称加密性能问题、采用与对称加密联合使用的方式解决数据传输性能问题
	核心内容为对称加密原理、非对称加密原理、以及CA认证存在的意义
	
	对称加密原理
		双方在进行数据传输的过程中，采用同一个秘钥对信息进行加密和解密。加密方式有多种，文中采用字母位移的方式进行举例，比如A向B发送一段信息 "secret message" 加密方式是字母向左位移三位，发送的信息变为“pbzobq jbppxdb”,当B接收到A发送的密文信息，采用同样的规则，将密文信息进行解密，将字母向右移三位，信息变为“secret message”。这种加密方式的好处是加解密快速，对计算能力要求低，缺点是陌生的双方无法建立起来第一次的链接传送秘钥，若是采用HTTP的方式传送秘钥，则有可能泄露秘钥信息，这样就会被第三方截获秘钥，进而造成信息的篡改等风险。
	
	非对称加密原理
		双方在进行数据传输的过程中，采用公钥与私钥的方式进行数据加解密，交互步骤如下
		1、A将自己的公钥发送给B
		2、B拿着A的公钥，对将要发送给A的信息进行加密
		3、A收到由B用A的公钥加密的密文信息，用A自己的私钥对密文信息进行解密。
		4、当B向A发送信息的时候同样遵循如上规则。
		5、补充说明：公钥与私钥的关系可以类比为锁头和钥匙，公钥是可以分发给对方，对方对信息上锁，但是无法打开，只有拥有钥匙的人可以打开，所以私钥是保密信息。
		这种方式解决了对称加密有可能在建立连接的过程中秘钥丢失的问题，但是存在一个缺陷，即，信任问题，双方都没有办法保证对方传过来的公钥是对方的，有可能是黑客替换成黑客自己的，这样同样会有中间人攻击的问题存在，因此进一步提出了CA认证的结局方案
	
	CA认证存在的意义
		CA认证的存在是为了解决互联网上进行数据加密传输的公钥信任问题，可以类比，在村子里有一个德高望重的老者，大家都信任这个老者，村民们在进行交易的时候，都会去问一下老者对方是否可靠，是不是本人，因为老者有村子里面每个人的画像，可以识别出来是不是本人，而且是不是好人，只要经过老者的认可，那么村民就会放心的交易了，同样的道理CA认证的目的就是颁发签名，对在CA认证机构认证的公钥进行签名颁发，当A和B传输信息的时候就会对这个公钥的签名在CA出校验，只有通过校验了，才认为真的是对方的公钥，可以放心的进行交互。
	
	总结
		HTTPS和交互原理和现实世界的交互原理与方式一致的，都可以找到类比，同样的道理，其他计算机实现原理大部分都能在现实世界中找到对应的例子，这样更加便于我们理解。

## Tip
### JAVA对象传参,到底是值传参还是引用传参？
本次分享的技巧是关于Java对象传参时到底是值传参还是引用传参，之所以有这个问题是以为前段时间在实现统一认证的时候，涉及到对指定账号下的权限数据放入List数据结构时的不确定性引发的思考，为此我做了一个实验，具体代码如下

```java
import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;
	
public class testListObject {
    public static void main(String[] args) {
        new testListObject().testListObject();
    }
	
    public void testListObject() {
        List<Map> listObject = new ArrayList<Map>(2);
        this.setListObject(listObject);
        System.out.printf("listObject===:"+listObject.get(0).get("name"));
    }
	
    public void setListObject(List<Map> listObject){
	
        Map mapObject = new HashMap();
        mapObject.put("name","zhangsan");
        mapObject.put("sex","male");
        listObject.add(0,mapObject);
        listObject.add(1,mapObject);
        System.out.println("setListObject+listObject===:"+listObject.get(0).get("name"));
    }
}

输出结果：
setListObject+listObject===:zhangsan
listObject===:zhangsan

```
不难看出来，当我new了一个空的list对象，在执行了一次数据初始化后，两次打印的结果是一致的，这说明在java中对象传参是引用传参。
可是这样就完事了吗？我刚才用的对象，还有一种对象没有试验，那就是基本数据类型，为此我从网上查了一遍文章，文章的给出的例子很明确的表明了，对于基本数据类型的传参，java采用的是值传参，

总结：在java中，基本类型传参是值传参，对象传参是引用传参。<br>
参考文章：[关于Java对象作为参数传递是传值还是传引用的问题](https://blog.csdn.net/xiangwanpeng/article/details/52454479)

## Share
### 基于RBAC原则设计的用户权限管理能力
RBAC全称是基于角色的访问控制，本次的用户权限控制就参考了RBAC对数据模型进行设计，设计这套模型的目的是希望通过数据模型做到基于用户或者角色灵活的进行权限配置，权限的类型包括菜单权限和按钮权限，这篇短文我将采用总分的模式来介绍。
#### 用户权限数据模型涉及到的模型

* 用户基本信息表 ： 用来存放用户基本信息，本次表结构的设计将各类用户的共同数据进行抽象，个性化数据统一放到拓展信息表中。
* 用户拓展信息表 ： 存放各类用户的拓展信息，该表模型采用了纵表的设计模式，方面表的内容可以无限扩展。后期可根据数据量的大小再行决定对用户数据这部分内容进行升级。
* 角色表 ： 存放用户角色信息，考虑到角色后期可以分为多个级别，因此该表的设计理念采用了行政区划表的设计模型，即对于每条数据增加一个父级属性，这样就可以做到无限级联的数据支撑。
* 权限表 ： 存放菜单权限或者数据权限与用户和角色的关系数据。起到灵活控制数据的权限数据的目的。
* 菜单表、按钮表：存放系统菜单数据和按钮数据，这两个实体将通过权限表与角色和用户产生关联。

#### 数据表结构
```sql

----用户基本信息表/*==============================================================*//* Table: USER_INFO                                          *//*==============================================================*/create table USER_INFO(   USER_ID              varchar(25) not null comment '用户ID',   ORGANIZATION_ID      varchar(25) comment '组织ID',   USER_CODE            varchar(25) comment '用户code',   USER_NAME            varchar(50) comment '用户名',   USER_ALIAS_NAME      varchar(50) comment '别名',   USER_TYPE_ENUM       varchar(8) comment '用户类型',   USER_PASSWORD        varchar(255) comment '用户密码',   USER_TEL             varchar(30) comment '用户电话',   USER_EMAIL           varchar(50) comment '用户邮箱',   USER_CLOSE_TIME      datetime comment '用户关闭时间',   LOGIN_TIME           datetime comment '当前登陆时间',   LAST_LOGIN_TIME      datetime comment '上一次登陆时间',   LOGIN_TIMES          int comment '登陆次数',   AUTHENTICATE_STATUS_ENUM varchar(8) comment '认证状态',   USER_STATUS_ENUM     varchar(8) comment '用户状态',   CREATE_TIME          datetime comment '创建时间',   UPDATE_TIME          datetime comment '更新时间',   primary key (USER_ID));alter table USER_INFO comment '用户基本信息表';

----用户拓展信息表
/*==============================================================*//* Table: USER_ADDITIONAL_INFO                               *//*==============================================================*/create table USER_ADDITIONAL_INFO(   ADDITIONAL_ID        varchar(25) not null comment '附加信息ID',   USER_ID              varchar(25) comment '用户ID',   ADDITIONAL_CATEGORY  varchar(50) comment '附加分类',   ADDITIONAL_CATEGORY_NAME varchar(50) comment '附加分类名',   CATEGORY_ITEM        varchar(50) comment '附加分类项',   CATEGORY_ITEM_NAME   varchar(50) comment '附加分类项名',   ITEM_NAME            varchar(50) comment '分类项项目名',   ITEM_VALUE           varchar(255) comment '分类项项目值',   ITEM_SORT            int comment '分类项项目排序',   primary key (ADDITIONAL_ID));alter table USER_ADDITIONAL_INFO comment '用户拓展信息表';

----角色表/*==============================================================*//* Table: ROLE_INFO                                          *//*==============================================================*/create table ROLE_INFO(   ROLE_ID              varchar(25) not null comment '角色ID',   PARENT_ROLE_ID       varchar(25) comment '父角色ID',   ROLE_NAME            varchar(50) comment '角色名称',   ROLE_DESC            varchar(255) comment '角色描述',   IS_DEFAULT_ENUM      varchar(8) comment '是否默认',   ROLE_STATUS_ENUM     varchar(8) comment '角色状态',   CREATE_USER          varchar(25) comment '创建人',   CREATE_TIME          datetime comment '创建时间',   UPDATE_USER          varchar(25) comment '更新人',   UPDATE_TIME          datetime comment '更新时间',   CORP_CODE            varchar(50) comment '租户代码',   CORP_NAME            varchar(50) comment '租户名称',   REMARK               varchar(255),   primary key (ROLE_ID));alter table ROLE_INFO comment '角色表';

----权限表/*==============================================================*//* Table: PERMISSION_INFO                                    *//*==============================================================*/create table PERMISSION_INFO(   PERMISSION_ID        varchar(25) not null comment '权限ID',   PARENT_PERMISSION_ID varchar(25) comment '父权限ID',   PERMISSION_NAME      varchar(50) comment '权限名称',   PERMISSION_DESC      varchar(255) comment '权限描述',   PERMISSION_MASTER    varchar(50) comment '权限属主:如用户权限或者角色权限',   PERMISSION_MASTER_ID varchar(25) comment '权限属主值:如，用户ID或者角色ID',   PERMISSION_ACCESS    varchar(50) comment '权限操纵类型，如：button或者menu',   PERMISSION_ACCESS_ID varchar(25) comment '权限操作类型ID，如，buttonID或者MenuID',   PERMISSION_STATUS_ENUM varchar(8) comment '权限状态',   CORP_CODE            varchar(50) comment '租户代码',   CORP_NAME            varchar(50) comment '租户名称',   REMARK               varchar(255),   primary key (PERMISSION_ID));alter table PERMISSION_INFO comment '权限表';
----菜单表/*==============================================================*//* Table: SYS_MENU_DICT                                      *//*==============================================================*/create table SYS_MENU_DICT(   MENU_ID              varchar(25) not null comment '菜单ID',   MENU_CODE            varchar(50) comment '菜单编码',   MENU_NAME            varchar(50) comment '菜单名称',   MENU_TAG             varchar(255) comment '菜单唯一标识，对应shiro中的标识，用作权限控制',   MENU_TYPE_ENUM       varchar(8) comment '菜单类型',   PARENT_MENU_ID       varchar(25) comment '父菜单ID',   MENU_URL             varchar(255) comment '菜单路径',   MENU_SORT            varchar(4) comment '菜单排序',   IS_DELETE_ENUM       varchar(8) comment '是否删除',   IS_ROOT              varchar(8) comment '是否根节点',   IS_LEAF              varchar(8) comment '是否叶子节点',   MENU_DEPTH           numeric comment '目录深度',   CREATE_USER          varchar(25) comment '创建用户',   CREATE_TIME          datetime comment '创建时间',   UPDATE_USER          varchar(25) comment '更新用户',   UPDATE_TIME          datetime comment '更新时间',   DELETE_USER          varchar(25) comment '删除用户',   DELETE_TIME          datetime comment '删除时间',   CORP_CODE            varchar(50) comment '租户编码',   CORP_NAME            varchar(50) comment '租户名称',   MENU_STATUS_ENUM     varchar(25) comment '菜单状态',   REMARK               varchar(255) comment '备注',   primary key (MENU_ID));alter table SYS_MENU_DICT comment '菜单表';
```
#### 实体关系
![实体模型关系图](https://github.com/liuchangshui/gain.arts.huan/blob/master/Resources/%E7%94%A8%E6%88%B7%E8%A7%92%E8%89%B2%E6%9D%83%E9%99%90%E5%AE%9E%E4%BD%93%E5%85%B3%E7%B3%BB.png)
