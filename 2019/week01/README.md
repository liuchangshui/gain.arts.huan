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
### JAVA对象传参
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
