# Project14

## PGP简介

PGP是由Phil Zimmermann于1991年开发的一种加密系统，它用于保护电子邮件和文件的隐私和安全。PGP采用了混合加密的方式，结合了对称加密和非对称加密算法。
发送方使用对称加密算法来加密邮件或文件内容，并使用接收方的公钥（非对称加密）来加密对称密钥，确保只有接收方可以解密数据。

### PGP结构图

![image](https://github.com/1-14/Project14/blob/main/2.png)

### 具体算法

使用SM2和SM4共同实现

## 关键代码

```
def sm2_enc(M, PK, SK):
    sm2_ = sm2.CryptSM2(public_key=PK, private_key=SK)
    return sm2_.encrypt(M)


def sm2_dec(CT, PK, SK):
    sm2_ = sm2.CryptSM2(public_key=PK, private_key=SK)
    return sm2_.decrypt(CT)


def sm4_enc(M, K):
    sm4_ = sm4.CryptSM4()
    sm4_.set_key(K, sm4.SM4_ENCRYPT)
    return sm4_.crypt_ecb(M)


def sm4_dec(CT, K):
    sm4_ = sm4.CryptSM4()
    sm4_.set_key(K, sm4.SM4_DECRYPT)
    return sm4_.crypt_ecb(CT)


def PGP_enc(M, K, PK, SK):
    M_enc = sm4_enc(M, K)
    K_enc = sm2_enc(K, PK, SK)

    return M_enc, K_enc


def PGP_dec(M_enc, K_enc, PK, SK):
    K = sm2_dec(K_enc, PK, SK)
    M = sm4_dec(M_enc, K)

    return M, K
```

使用gmssl库中的SM2和SM4，实现SM2和SM4加密解密，并定义PGP_enc和PGP_dec直接实现整个系统的加密解密。

## 结果展示

![image](https://github.com/1-14/Project14/blob/main/1.png)

**成功解密出密钥和明文**




