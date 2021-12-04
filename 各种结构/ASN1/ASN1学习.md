# ASN.1

`ASN.1` 的全称是Abstract Syntax Notation One.用来描述通信协议中的数据传输.

`ASN.1` 是由以下组织联合定义的标准:

- ISO(International Organization for Standardization)
- IEC(International Electrotechnical Commission)
- ITU-T(International Telecommunication Union)

# 参考资料

* 参考RFC-5280

* ```JAVA
  org.bouncycastle.asn1.BERTags
  ```

## 数据类型

### 2.3.1. 简单类型

- BOOLEAN(布尔类型)

```
Active ::= BOOLEAN
```

- INTEGER(整数类型)

```
Age ::= INTEGER
```

- ENUMERATED(枚举类型)

```
Color ::={red,blue,yellow}
```

- REAL(实数类型) M × BE

**B只能为2或10**

```
pi REAL ::={``314``,``10``,-``2``}
```

- BIT STRING(位串类型)

**由0或多个比特组成的有序位串。可用二进制或16进制表示**

```
key BIT STRING ::= ``'10010001'``B``key BIT STRING ::= ``'91'``H
```

- OCTET STRING(八位位组串)

**由0或多个8位位组组成的有序串。可用十进制(0-255),二进制或16进制表示**

```
key OCTET STRING ::= ``'145'``key OCTET STRING ::= ``'10010001'``B``key OCTET STRING ::= ``'91'``H
```

- OBJECT IDENTIFIER(对象标识符)



BER按着TLV模式进行编码,TLV即Type,Length,Value.



Tag



| TagName           | TagValue |
| :---------------- | :------- |
| TagName           | TagValue |
| BOOLEAN           | 0x01     |
| INTEGER           | 0x02     |
| BIT STRING        | 0x03     |
| OCTET STRING      | 0x04     |
| NULL              | 0x05     |
| OBJECT IDENTIFIER | 0x06     |
| EXTERNAL          | 0x08     |
| ENUMERATED        | 0x0a     |
| SEQUENCE          | 0x10     |
| SEQUENCE OF       | 0x10     |
| SET               | 0x11     |
| SET_OF            | 0x11     |
| NUMERIC STRING    | 0x12     |
| PRINTABLE STRING  | 0x13     |
| T61 STRING        | 0x14     |
| VIDEOTEX STRING   | 0x15     |
| IA5 STRING        | 0x16     |
| UTC TIME          | 0x17     |
| GENERALIZED TIME  | 0x18     |
| GRAPHIC STRING    | 0x19     |
| VISIBLE STRING    | 0x1a     |
| GENERAL STRING    | 0x1b     |
| UNIVERSAL STRING  | 0x1c     |
| BMP STRING        | 0x1e     |
| UTF8 STRING       | 0x0c     |
| CONSTRUCTED       | 0x20     |
| APPLICATION       | 0x40     |
| TAGGED            | 0x80     |