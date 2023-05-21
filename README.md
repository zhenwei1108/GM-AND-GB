# GM-AND-GB

国密及国标部分文档

各种oid的定义在   GMT 0006-2012 密码应用标识规范 中



## RFC

RFC - 查询地址: https://datatracker.ietf.org/

中文翻译：http://www.rfc2cn.com/index.html

常用的RFC编号, 用到再补充...


| RFC            | 说明          | 备注                |
|:---------------|:------------| :------------------ |
| 2104	| HMAC	| 由 RFC 6151 补充 |
| 2256 | DN        | Ldap-证书主题项说明 |
| 2315 | pkcs7     |                     |
| 2328 | hashtabs  |                     |
| 2328 | hashtabs  |                     |
| 2437 | PKCS1、RSA操作   |                     |
| 2459 | CRL |  |
| 2560 | ocsp      |                     |
| 2986 | pkcs10    |                     |
| 3161 | 时间戳    |                     |
| 3447 | pkcs1填充 |                     |
| 3280 | x509证书  |                     |
| 3686 | AES       |                     |
| 3852,5652,8933 | CMS       | 基于PKCS7 frc2315   |
| 4432 | RSA-Key   |                     |
| 5208 | pkcs8     |                     |
| 5280 | CRL   |                     |
| 6025 | ASN1 | |
| 6238 | TOTP| 一次性口令 |
| 6749           | OAuth 2.0   |  |
| 6962           | CT log 1.0  |  |
| 7292           | pkcs12      |                     |
| 7519           | jwt         |                     |
| 8018           | pkcs5       |                     |
| 8032           | ED DSA      |  |
| 9162           | CT log 2.0  |                     |


## OID

参考:

- GMT-0006《密码应用标识规范》
- [OIDS](http://gmssl.org/docs/oid.html)

| 对象标识符OID           | 对象标识符定义                  | 备注                              |
| :---------------------- | :------------------------------ | :-------------------------------- |
| 对象标识符OID           | 对象标识符定义                  | 备注                              |
| 通用标识符              |                                 |                                   |
| 1.2                     | 国际标准化组织成员标识符        |                                   |
| 1.2.156                 | 中国                            |                                   |
| 1.2.156.197             | 国家密码管理局                  |                                   |
| 1.2.156.10197           | 密码行业标准化技术委员会        |                                   |
| 1.2.156.10197.1         | 密码算法                        |                                   |
| 分组密码算法对象标识符  |                                 |                                   |
| 1.2.156.10197.1.100     | 分组密码算法                    |                                   |
| 1.2.156.10197.1.102     | SM1分组算法                     | 算法保密                          |
| 1.2.156.10197.1.103     | SSF33分组算法                   |                                   |
| 1.2.156.10197.1.104     | SM4分组算法                     |                                   |
| 1.2.156.10197.1.104.1   | SM4-ECB                         |                                   |
| 序列密码算法对象标识符  |                                 |                                   |
| 1.2.156.10197.1.200     | 序列密码算法                    |                                   |
| 1.2.156.10197.1.201     | 祖冲之序列密码算法              | ZUC                               |
| 公钥密码算法对象标识符  |                                 |                                   |
| 1.2.156.10197.1.300     | 公钥密码算法                    |                                   |
| 1.2.156.10197.1.301     | SM2椭圆曲线公钥密码算法         |                                   |
| 1.2.156.10197.1.301.1   | SM2-1数字签名算法               |                                   |
| 1.2.156.10197.1.301.2   | SM2-2密钥交换协议               |                                   |
| 1.2.156.10197.1.301.3   | SM2-3公钥加密算法               |                                   |
| 1.2.156.10197.1.302     | SM9标识密码算法                 |                                   |
| 1.2.156.10197.1.302.1   | SM9-1数字签名算法               |                                   |
| 1.2.156.10197.1.302.2   | SM9-2密钥交换协议               |                                   |
| 1.2.156.10197.1.302.3   | SM9-3密钥封装机制和公钥加密算法 |                                   |
| 杂凑算法对象标识符      |                                 |                                   |
| 1.2.156.10197.1.400     | 杂凑算法                        |                                   |
| 1.2.156.10197.1.401     | SM3杂凑算法                     |                                   |
| 1.2.156.10197.1.401.1   | SM3杂凑算法，无密钥使用         | SM3杂凑可以使用公钥参与，用于签名 |
| 1.2.156.10197.1.401.2   | SM3杂凑算法，有密钥使用         |                                   |
| 1.3.6.1.4.1.22554.1.1   | SHA1                            |                                   |
| 1.3.6.1.4.1.22554.1.2.1 | SHA-2.SHA-256                   |                                   |
| 1.3.6.1.4.1.22554.1.2.2 | SHA-2.SHA-384                   |                                   |
| 1.3.6.1.4.1.22554.1.2.3 | SHA-2.SHA-512                   |                                   |
| 1.3.6.1.4.1.22554.1.2.4 | SHA-2.SHA-224                   |                                   |
| 组合运算算法对象标识符  |                                 | 签名算法标识符                    |
| 1.2.156.10197.1.500     | 组合运算机制                    |                                   |
| 1.2.156.10197.1.501     | 基于SM2算法那和SM3算法的签名    | SM3WithSM2                        |
| 1.2.156.10197.1.504     | 基于RSA算法和SM3算法的签名      | SM3WithRSA                        |
|                         |                                 |                                   |
| PKCS                    |                                 |                                   |
| 1.3.6.1.4.1.22554.1.1.1 | SHA-1.PKCS5                     |                                   |
| 1.3.6.1.4.1.22554.1.1.2 | SHA-1.PKCS12                    |                                   |
