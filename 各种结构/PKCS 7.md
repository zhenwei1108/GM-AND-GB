## PKCS 7

#### RFC 2315

```ASN.1
ContentInfo ::= SEQUENCE {
     contentType ContentType,
     content
       [0] EXPLICIT ANY DEFINED BY contentType OPTIONAL }
       
ContentType ::= OBJECT IDENTIFIER
--  data, signedData, envelopedData, signedAndEnvelopedData, digestedData, and encryptedData

1. Data ::= OCTET STRING

2. SignedData ::= SEQUENCE {
     version Version,
     digestAlgorithms DigestAlgorithmIdentifiers, (SET)
     contentInfo ContentInfo,  (SEQUENCE)
     certificates [0] IMPLICIT ExtendedCertificatesAndCertificates OPTIONAL,
     crls [1] IMPLICIT CertificateRevocationLists OPTIONAL,
     signerInfos SignerInfos 
     }
     
     
DigestAlgorithmIdentifiers ::=  SET OF DigestAlgorithmIdentifier

SignerInfos ::= SET OF SignerInfo

SignerInfo ::= SEQUENCE {
     version Version,
     issuerAndSerialNumber IssuerAndSerialNumber,
     digestAlgorithm DigestAlgorithmIdentifier,
     authenticatedAttributes [0] IMPLICIT Attributes OPTIONAL,
     digestEncryptionAlgorithm DigestEncryptionAlgorithmIdentifier,
     encryptedDigest EncryptedDigest,
     unauthenticatedAttributes [1] IMPLICIT Attributes OPTIONAL }

EncryptedDigest ::= OCTET STRING


 DigestInfo ::= SEQUENCE {
     digestAlgorithm DigestAlgorithmIdentifier,
     digest Digest }

   Digest ::= OCTET STRING
   
   
   
   
3. EnvelopedData ::= SEQUENCE {
     version Version,
     recipientInfos RecipientInfos, --接收者信息，最少一个
     encryptedContentInfo EncryptedContentInfo }

   RecipientInfos ::= SET OF RecipientInfo

   EncryptedContentInfo ::= SEQUENCE {
     contentType ContentType,
     contentEncryptionAlgorithm ContentEncryptionAlgorithmIdentifier,
     encryptedContent  [0] IMPLICIT EncryptedContent OPTIONAL }

   EncryptedContent ::= OCTET STRING
   
   
RecipientInfo ::= SEQUENCE {
     version Version,
     issuerAndSerialNumber IssuerAndSerialNumber, 
     keyEncryptionAlgorithm KeyEncryptionAlgorithmIdentifier, --算法标识
     encryptedKey EncryptedKey } --公钥加密数据的结果（加密的对称密钥）

   EncryptedKey ::= OCTET STRING
   
   



 4. SignedAndEnvelopedData ::= SEQUENCE {
     version Version,
     recipientInfos RecipientInfos,
     digestAlgorithms DigestAlgorithmIdentifiers,
     encryptedContentInfo EncryptedContentInfo,
     certificates [0] IMPLICIT ExtendedCertificatesAndCertificates OPTIONAL,
     crls [1] IMPLICIT CertificateRevocationLists OPTIONAL,
     signerInfos SignerInfos }
     
     
 5. DigestedData ::= SEQUENCE {
     version Version,
     digestAlgorithm DigestAlgorithmIdentifier,
     contentInfo ContentInfo,
     digest Digest }

   Digest ::= OCTET STRING
 
 
 
 6. EncryptedData ::= SEQUENCE {
     version Version,
     encryptedContentInfo EncryptedContentInfo }


pkcs-7 OBJECT IDENTIFIER ::=
     { iso(1) member-body(2) US(840) rsadsi(113549)
         pkcs(1) 7 }
         
   data OBJECT IDENTIFIER ::= { pkcs-7 1 }
   signedData OBJECT IDENTIFIER ::= { pkcs-7 2 }
   envelopedData OBJECT IDENTIFIER ::= { pkcs-7 3 }
   signedAndEnvelopedData OBJECT IDENTIFIER ::=
      { pkcs-7 4 }
   digestedData OBJECT IDENTIFIER ::= { pkcs-7 5 }
   encryptedData OBJECT IDENTIFIER ::= { pkcs-7 6 }
```

