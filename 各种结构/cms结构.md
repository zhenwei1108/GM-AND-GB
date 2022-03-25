# cms

## rfc 3852



基于pkcs7 协议, frc2315

升级版本v1 =  rfc 2630

升级版本v2 = rfc 3369

升级至 = rfc 3852

升级至 = rfc 5652

升级至 = rfc 8933





```ASN.1

ContentInfo ::= SEQUENCE {
     contentType ContentType, -- OBJECT IDENTIFIER
     content [0] EXPLICIT ANY DEFINED BY contentType  -- 如下
     }

-- 第一种
SignedData ::= SEQUENCE {
  version CMSVersion, -- INTEGER  { v0(0), v1(1), v2(2), v3(3), v4(4), v5(5) }
  digestAlgorithms DigestAlgorithmIdentifiers, -- SET OF DigestAlgorithmIdentifier
  encapContentInfo EncapsulatedContentInfo, -- 封装内容  如下
  certificates [0] IMPLICIT CertificateSet OPTIONAL,
  crls [1] IMPLICIT RevocationInfoChoices OPTIONAL, -- SET OF RevocationInfoChoice
  signerInfos SignerInfos -- SET OF SignerInfo
  }


-- 1
      EncapsulatedContentInfo ::= SEQUENCE {
        eContentType ContentType, -- id-contentType OBJECT IDENTIFIER ::= { iso(1) member-body(2)          us(840) rsadsi(113549) pkcs(1) pkcs9(9) 3 }
        eContent [0] EXPLICIT OCTET STRING OPTIONAL 
        }
 
      SignerInfo ::= SEQUENCE {
        version CMSVersion,
        sid SignerIdentifier, -- 如下
        digestAlgorithm DigestAlgorithmIdentifier, -- 
        signedAttrs [0] IMPLICIT SignedAttributes OPTIONAL, -- SET SIZE (1..MAX) OF Attribute
        signatureAlgorithm SignatureAlgorithmIdentifier, --AlgorithmIdentifier
        signature SignatureValue, -- OCTET STRING
        unsignedAttrs [1] IMPLICIT UnsignedAttributes OPTIONAL -- SET SIZE (1..MAX) OF Attribute
        }

-- 2

                  SignerIdentifier ::= CHOICE {
                    issuerAndSerialNumber IssuerAndSerialNumber,
                    subjectKeyIdentifier [0] SubjectKeyIdentifier 
                    }

                    Attribute ::= SEQUENCE {
                      attrType OBJECT IDENTIFIER,
                      attrValues SET OF AttributeValue  -- ANY
                      }


--第二种
EnvelopedData ::= SEQUENCE {
     version CMSVersion,
     originatorInfo [0] IMPLICIT OriginatorInfo OPTIONAL, -- 如下
     recipientInfos RecipientInfos, -- SET SIZE (1..MAX) OF RecipientInfo --如下
     encryptedContentInfo EncryptedContentInfo, --如下
     unprotectedAttrs [1] IMPLICIT UnprotectedAttributes OPTIONAL  -- SET SIZE (1..MAX) OF Attribute --如上
     }

OriginatorInfo ::= SEQUENCE {
     certs [0] IMPLICIT CertificateSet OPTIONAL, -- SET OF CertificateChoices --如下
     crls [1] IMPLICIT RevocationInfoChoices OPTIONAL --SET OF RevocationInfoChoice
     }
     
EncryptedContentInfo ::= SEQUENCE {
     contentType ContentType,
     contentEncryptionAlgorithm ContentEncryptionAlgorithmIdentifier, -- AlgorithmIdentifier
     encryptedContent [0] IMPLICIT EncryptedContent OPTIONAL -- OCTET STRING
     }


RecipientInfo ::= CHOICE {
     ktri KeyTransRecipientInfo,
     kari [1] KeyAgreeRecipientInfo,
     kekri [2] KEKRecipientInfo,
     pwri [3] PasswordRecipientInfo,
     ori [4] OtherRecipientInfo }
--one
        KeyTransRecipientInfo ::= SEQUENCE {
            version CMSVersion, -- always set to 0 or 2
            rid RecipientIdentifier, --如下
            keyEncryptionAlgorithm KeyEncryptionAlgorithmIdentifier, --AlgorithmIdentifier
            encryptedKey EncryptedKey 
        }
        

                RecipientIdentifier ::= CHOICE {
                   issuerAndSerialNumber IssuerAndSerialNumber,
                   subjectKeyIdentifier [0] SubjectKeyIdentifier 
             }
--two
        KeyAgreeRecipientInfo ::= SEQUENCE {
          version CMSVersion, -- always set to 3
          originator [0] EXPLICIT OriginatorIdentifierOrKey, -- 如下
          ukm [1] EXPLICIT UserKeyingMaterial OPTIONAL, --OCTET STRING
          keyEncryptionAlgorithm KeyEncryptionAlgorithmIdentifier, 
          recipientEncryptedKeys RecipientEncryptedKeys -- SEQUENCE OF RecipientEncryptedKey --如下
				}
                OriginatorIdentifierOrKey ::= CHOICE {
                   issuerAndSerialNumber IssuerAndSerialNumber,
                   subjectKeyIdentifier [0] SubjectKeyIdentifier,
                   originatorKey [1] OriginatorPublicKey 
                }
                		
                		OriginatorPublicKey ::= SEQUENCE {
                       algorithm AlgorithmIdentifier,
                       publicKey BIT STRING 
                      }
                      		
                      		RecipientEncryptedKey ::= SEQUENCE {
                             rid KeyAgreeRecipientIdentifier, -- 如下
                             encryptedKey EncryptedKey }
                             
                             KeyAgreeRecipientIdentifier ::= CHOICE {
                                 issuerAndSerialNumber IssuerAndSerialNumber,
                                 rKeyId [0] IMPLICIT RecipientKeyIdentifier --如下
                                 }
                                 
                                  RecipientKeyIdentifier ::= SEQUENCE {
                                     subjectKeyIdentifier SubjectKeyIdentifier, --OCTET STRING
                                     date GeneralizedTime OPTIONAL,
                                     other OtherKeyAttribute OPTIONAL -- 如下
                                     }
                                     
                                     OtherKeyAttribute ::= SEQUENCE {
                                       keyAttrId OBJECT IDENTIFIER,
                                       keyAttr ANY DEFINED BY keyAttrId OPTIONAL 
                                       }

                                     
--three                         
        KEKRecipientInfo ::= SEQUENCE {
          version CMSVersion, -- always set to 4
          kekid KEKIdentifier, --如下
          keyEncryptionAlgorithm KeyEncryptionAlgorithmIdentifier, 
          encryptedKey EncryptedKey 
          }                             

                  KEKIdentifier ::= SEQUENCE {
                     keyIdentifier OCTET STRING,
                     date GeneralizedTime OPTIONAL,
                     other OtherKeyAttribute OPTIONAL 
                     }
--four
        PasswordRecipientInfo ::= SEQUENCE {
						version CMSVersion, -- always set to 0 
						keyDerivationAlgorithm [0]  KeyDerivationAlgorithmIdentifier OPTIONAL,  -- AlgorithmIdentifier
            keyEncryptionAlgorithm KeyEncryptionAlgorithmIdentifier,
            encryptedKey EncryptedKey }
-- five
        OtherRecipientInfo ::= SEQUENCE {
           oriType OBJECT IDENTIFIER,
           oriValue ANY DEFINED BY oriType 
           }
        
        
--第三种
DigestedData ::= SEQUENCE {
     version CMSVersion,
     digestAlgorithm DigestAlgorithmIdentifier,
     encapContentInfo EncapsulatedContentInfo,
     digest Digest --OCTET STRING
     }
-- 第四种
EncryptedData ::= SEQUENCE {
     version CMSVersion,
     encryptedContentInfo EncryptedContentInfo,
     unprotectedAttrs [1] IMPLICIT UnprotectedAttributes OPTIONAL }   
        
-- 第五种
AuthenticatedData ::= SEQUENCE {
     version CMSVersion,
     originatorInfo [0] IMPLICIT OriginatorInfo OPTIONAL,
     recipientInfos RecipientInfos, -- SET SIZE (1..MAX) OF RecipientInfo
     macAlgorithm MessageAuthenticationCodeAlgorithm, -- AlgorithmIdentifier
     digestAlgorithm [1] DigestAlgorithmIdentifier OPTIONAL, -- AlgorithmIdentifier
     encapContentInfo EncapsulatedContentInfo,
     authAttrs [2] IMPLICIT AuthAttributes OPTIONAL, --SET SIZE (1..MAX) OF Attribute
     mac MessageAuthenticationCode, --OCTET STRING
     unauthAttrs [3] IMPLICIT UnauthAttributes OPTIONAL --SET SIZE (1..MAX) OF Attribute
     }



		RevocationInfoChoice ::= CHOICE {
     crl CertificateList,
     other [1] IMPLICIT OtherRevocationInfoFormat 
     }


         OtherRevocationInfoFormat ::= SEQUENCE {
           otherRevInfoFormat OBJECT IDENTIFIER,
           otherRevInfo ANY DEFINED BY otherRevInfoFormat 
           }
           
     CertificateChoices ::= CHOICE {
       certificate Certificate,
       extendedCertificate [0] IMPLICIT ExtendedCertificate,  -- Obsolete
       v1AttrCert [1] IMPLICIT AttributeCertificateV1,        -- Obsolete
       v2AttrCert [2] IMPLICIT AttributeCertificateV2,
       other [3] IMPLICIT OtherCertificateFormat 
       }
       
         OtherCertificateFormat ::= SEQUENCE {
           otherCertFormat OBJECT IDENTIFIER,
           otherCert ANY DEFINED BY otherCertFormat 
           }
         
     IssuerAndSerialNumber ::= SEQUENCE {
       issuer Name,
       serialNumber CertificateSerialNumber 
       }


   AttributeCertificateV1 ::= SEQUENCE {
     acInfo AttributeCertificateInfoV1,
     signatureAlgorithm AlgorithmIdentifier,
     signature BIT STRING 
     }
     
     
     AttributeCertificateInfoV1 ::= SEQUENCE {
     version AttCertVersionV1 DEFAULT v1,
     subject CHOICE {
       baseCertificateID [0] IssuerSerial, -- associated with a Public Key Certificate
       subjectName [1] GeneralNames  -- associated with a name
         },
     issuer GeneralNames,
     signature AlgorithmIdentifier,
     serialNumber CertificateSerialNumber,
     attCertValidityPeriod AttCertValidityPeriod,
     attributes SEQUENCE OF Attribute,
     issuerUniqueID UniqueIdentifier OPTIONAL,
     extensions Extensions OPTIONAL }
```

