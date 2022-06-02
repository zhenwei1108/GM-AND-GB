| 原语   | 说明                                                         |
| ------ | ------------------------------------------------------------ |
| (n, e) | RSA Public Key                                               |
| n      | the modulus                                                  |
| e      | the public exponent                                          |
| K      | RSA Private Key , 有两种表示方式 （n, d） 和（p,q dp, dq, qInv） |
| d      | the private exponent                                         |
| p      | the first factor                                             |
| q      | the second factor                                            |
| dP     | the first factor's exponent                                  |
| dQ     | the second factor's exponent                                 |
| qInv   | the CRT coefficient                                          |
|        |                                                              |

(n,e) 公钥

(n,d) 私钥

# 实现方式

1. 找到两个大数 p, q 两个正数互质。（*互质*是公约数只有1的两个整数）
2. n = p * q 
3. 欧拉函数 φ(n) = (p-1) * (q-1)
4. 公钥： 找到e， 1<e<φ(n)， 且e和 φ(n) 互质
5. 私钥： 找到e*d除以φ(n)余1
6. 公钥加密： 原文m， m^e 除以n余c。 c为加密结果。m^e mod n
7. 私钥解密：c^d 除以n余m。 可得到原文m。 c^d mod n
8. 数据签名：m^d除以n余s。s为签名结果。m^d mod n
9. 签名验签：s^e除以n余m。s^d mod n