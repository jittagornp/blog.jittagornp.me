# Public Key / Private Key คืออะไร  สร้างยังไง แล้วเอาไปใช้ทำอะไรได้บ้าง (ตัวอย่าง Code ภาษา Java)

![](./keys.jpg)

*Image from [https://www.insureon.com/blog/safeguard-building-services-with-lost-key-insurance-coverage](https://www.insureon.com/blog/safeguard-building-services-with-lost-key-insurance-coverage)*

# การเข้ารหัสข้อมูล

ถ้าพูดถึงเรื่องของ `กุญแจ` หรือ `Key` ก็คงจะหนีไม่พ้น เรื่องของ**การเข้ารหัสข้อมูล (Encryption)**   
คือ การที่เราต้องการส่งข้อมูลที่มีอยู่ ไปให้ใครสักคนนึง แล้วต้องการให้ข้อมูลชุดนั้น`เป็นความลับ` 
    
<img src="./secret-file.png" width="200">

เราก็จะเอาข้อมูลที่ต้องการจะส่ง มาทำการ**เข้ารหัส (Encrypt)** ด้วย Key เพื่อไม่ให้ใครอ่านข้อมูลนั้นออก 
*(ยกเว้นคนที่เราต้องการจะส่งข้อมูลไปหาจริง ๆ เท่านั้น ถึงจะอ่านข้อมูลออก)* 

![](./encrypt.png)

จากนั้น   
เราก็จะส่งข้อมูล**ที่ถูกเข้ารหัสแล้ว** ไปหาคนที่เราต้องการส่งไปหา 
  
![](./send-to-internet.png?v=1)

เมื่อปลายทางได้รับข้อมูล   
ก็จะทำการ**ถอดรหัส (Decrypt) กลับ** ด้วย Key เพื่อให้ได้ข้อมูลจริง ๆ ที่ต้นทางส่งมาให้  

![](./receive-data.png)

ก็จะเป็นอันเสร็จสิ้นกระบวนการในการเข้ารหัส/ถอดรหัส และรับ/ส่งข้อมูล 

---

การเข้ารหัส/ถอดรหัส (Encryption) สามารถทำได้หลายวิธี   
แต่ปกติแล้ว จะถูกแบ่งออกเป็นแค่ 2 กลุ่มใหญ่ ๆ คือ

- การเข้ารหัสแบบใช้ Key เดียว (Secret Key) กับ
- การเข้ารหัสแบบใช้ Key คู่ (Keypair) หรือใช้ 2 Keys ช่วยกัน
  
# การเข้ารหัสแบบใช้ Key เดียว (Secret Key)

<img src="./secret-key.png" width="120">

เราจะเรียก การเข้ารหัสแบบนี้ว่า `การเข้ารหัสแบบสมมาตร` หรือ `Symmetric Encryption`   

> คือ ถ้าใช้ Key ไหนเข้ารหัส ก็จะใช้ Key เดิมถอดรหัสออกมา

หน้าตาของ Secret Key จะประมาณนี้ 

```plaintext
password

//หรือ

123456

//หรือ

0863235932516704

//หรือ 

E9lSpLZ0Pbebzq5gj6Ja6w
```

- Secret Key อาจจะใช้วิธีการ Random ขึ้นมา 
- หรือ กำหนดขึ้นมาตายตัวเลย ว่าเป็นแบบนี้ ๆ 
- มีรูปแบบไม่แน่นอน      

### แนะนำ

ถ้าจะให้ดี Secret Key ควรใช้วิธีการ Random ขึ้นมา และเป็นการ Random ที่ได้มาตรฐาน เพื่อให้ Key มีความปลอดภัย ไม่ถูกคาดเดาได้ง่าย 

### กระบวนการทำงาน

ใช้ Key ไหนเข้ารหัส ก็จะใช้ Key เดิมถอดรหัส 

![](./secret-key-flow.png)

### Algorithm ที่นิยมใช้

Algorithm ที่นิยมใช้ในการเข้ารหัสแบบ Key เดียว คือ   
- [AES (Advanced Encryption Standard)](https://www.wikiwand.com/en/Advanced_Encryption_Standard)
  
ไม่ได้มีตัวเดียวน่ะ แค่ยกตัวอย่างที่ใช้กันบ่อย ๆ

### ข้อดี 

- เร็ว (กว่าแบบ Key คู่)
 
### ข้อเสีย

- ไม่เหมาะกับการแชร์ (Share) Key หรือการเอา Secret Key เรา ไปให้คนอื่นใช้ร่วมด้วย เพราะ Key ประเภทนี้ถือเป็นความลับ **ห้ามเปิดเผย** 

วิธีการนี้ **ปัจจุบันก็ยังคงใช้งานกันอยู่ ไม่ใช่ว่าไม่ใช้แล้ว**    

> เพราะหลาย ๆ อย่าง ก็ยังต้องใช้การเข้ารหัสแบบ Key เดียวอยู่   

เช่น 

- การทำ Https ก็ใช้การเข้ารหัสแบบ Key เดียว   
แต่ก็มีใช้แบบ Key คู่ร่วมด้วย ซึ่งจะอธิบายในหัวข้อถัดไป 
  
ถ้าอยากเข้าใจการทำงานของ Https สามารถอ่านจากบทความนี้ได้ครับ 

- [HTTPS คืออะไร ทำงานอย่างไร](/blog/what-is-https/) 
- [อธิบายการทำงานของ HTTPS และเทคโนโลยีที่เกี่ยวข้อง แบบพยายามไม่ให้งง](https://rath.asia/2017/02/https-and-related-technology-explained/)

# การเข้ารหัสแบบใช้ Key คู่ (Keypair) หรือใช้ 2 Keys 

<img src="./keypair.png" width="120">

เราจะเรียก การเข้ารหัสแบบนี้ว่า  `การเข้ารหัสแบบอสมมาตร` หรือ `Asymmetric Encryption`   

> คือ ใช้ Key นึงเข้ารหัส แล้วใช้อีก Key นึงถอดรหัส 

หน้าตาของ Keys จะประมาณนี้ 

Public Key 
```plaintext
-----BEGIN PUBLIC KEY-----
MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAvDzcdSVY5HbgU3hnCW5vG3/kl8QFN
jUxVZJvAOpKh8ym9LaV98gGSlp8N/OjeQT2DsI6FKhJmCWUXn+7XTKPSxr4Xv2If6IWT2i6YV
VHhcdj4roTVQrDhFopj8hdjWOYPMg05u5lulU5Sa7JxPpA0zohYcSnw3JBoSBghfsjaf3oMRe
oQeMfYlbpaHP5/zqe5FSPwqxTXtR/3rpbfeVoNOp8lG4kjF7W5SINpuBEDz69+VCjDupL0Si5
/LGiDzGIA1X8M3j0zV95u/AwjhSD0VmkZBQvAws6G0aATdAgnlI1RK+AdpZf/zr3Q6l9J0SYj
1PFWgZzbagjkOGi3DlZdwIDAQAB
-----END PUBLIC KEY-----
```

Private Key
```plaintext
-----BEGIN PRIVATE KEY-----
MIIEvgIBADANBgkqhkiG9w0BAQEFAASCBKgwggSkAgEAAoIBAQC8PNx1JVjkduBTeGcJbm8bf
+SXxAU2NTFVkm8A6kqHzKb0tpX3yAZKWnw386N5BPYOwjoUqEmYJZRef7tdMo9LGvhe/Yh/oh
ZPaLphVUeFx2PiuhNVCsOEWimPyF2NY5g8yDTm7mW6VTlJrsnE+kDTOiFhxKfDckGhIGCF+yN
p/egxF6hB4x9iVuloc/n/Op7kVI/CrFNe1H/eult95Wg06nyUbiSMXtblIg2m4EQPPr35UKMO
6kvRKLn8saIPMYgDVfwzePTNX3m78DCOFIPRWaRkFC8DCzobRoBN0CCeUjVEr4B2ll//OvdDq
X0nRJiPU8VaBnNtqCOQ4aLcOVl3AgMBAAECggEACZlY7Khg5hWhzt/e8T4ucEqPT6XxVhhUUb
bL7lIERvSKtwPwldgfaf8/QmMsPOmh2pLQ/2itiBKyhDcjSNdhM0VG0SFAqrGLTbVbe8crhIj
scQ1oGvgXjFJEuE5RZvpjMwZKnFQf3+akqzs8kszoLV1TgnbSz0auThcmlO5/mdIAdnc/BxoT
yVcNW+948hgTnh6w9hqr+Gtd7T6CSdksSFpBD3xtAQvdKCq5tDcexapJPDvmzOIg4VLuaXP2x
cVGc4DOQj5pKA77HQrpJ8VqWDV3ecXwkiqAG2r7VdW8T4juPnj2whAxkSFVU8D4vUFyVrnFRh
818QaDKP1dWXstkQKBgQDgEHp+NIlKEStbBgxYXOc+clpAZMnVw+bFYcSDjzGdX/dzaI9zxrN
GO/ZjGko4SqYqp6EFmLsQiJDFHY9lxpFv74ouTEF/69d8tXqxhrqH1emDMraO/Y7gvsXtIhH4
3Zk9NkB/A+bOMj+sBUJZh2RxCgyhKZ4yE3L5FT9nllaCfQKBgQDXESmwYiPWllph4VhlnLtsO
gkWd83Nfi1vEOt2KZKw0uqnmg+tcTCHUCtepGwlchep8/4g2TweXtJ/8wVqkiiUat8gPsv0dk
eNzIwAbpDSVxErNYwE0e2LT7P+Mj+Ze/47qf52G+aY5lgZXrSfFnCAXUisZMPdcmD3qHtK1bO
6AwKBgH46qleZT1Lr00oHYUMSq6/xikjGvzJvl/3Q833OWPw5CVX6LP7jjTHfLBJuyCtoWq6j
G0Lk5VYOKcjyu0tyD5NJFsa4bRodCpwWPVXv+fv2lgQ0uMZbsHeK4kSSsh9K8D6c5r7nusqlY
luN5vA7J2nLaIwOvzGk5VvQDZVVC82dAoGBAIP9X4WFpZMD8XJS12p9NzVjpMIqQp8UChQ44R
lCyGlG+IZl8aszZWIWHJfX9xtAGy/Ns7A7Qj8tWKj33+IY01jLAicLAycEFEP9Pgrh0HWWw82
t7kHjCJNQFhoygn/S7iN139piozJBY94mFlnwbpkJJxnOObrFgKddulUiNEw7AoGBAJgR47tg
u4kRtVT0KWCkjEWGAWDlDpi5zXwGXAz46s1yBE/vYuh3DVA9w3cVX3Y6WNLD0RGozLSsqUU0I
1uyUhqDcHKCmqtcOSrcsVUpVJBhxJuPAJglRSJLVEflxSSZwFWJmQCB/WcPbL3a+xM4av53Tt
9YgGEku37mlGuNwxtA
-----END PRIVATE KEY-----
```

### หมายเหตุ

อันนี้เป็นแค่รูปแบบการจัดเก็บ Keys รูปแบบนึง   
โดยการแปลง Key (Bytes) ไปเป็น Base64
     
จริง ๆ แล้ว ยังมีรูปแบบอื่น ที่อาจจะไม่ได้เก็บ Key เป็นแบบนี้   
แต่เราก็มักจะเห็น Format นี้กันบ่อย ๆ 
  
### Base64 Format    

สังเกตว่า Key จะมี 
```plaintext
-----BEGIN XXXXX KEY-----

//และ 

-----END XXXXX KEY-----
```
ครอบอยู่   
  
เพื่อใช้บอกว่า Key นี้ เป็น Key ประเภทไหน   
  
- ขนาดของ Key จะยาวกว่าแบบ Key เดียว หรือ Secret Key 
- Public Key และ Private Key ได้มาโดยการ**ใช้กระบวนการทางคณิตศาสตร์** ในการสร้าง (Generate) ขึ้นมา Random คู่กันแบบมั่ว ๆ ไม่ได้ 
- ทั้ง 2 Keys มีความสัมพันธ์กัน 
- Key นึงสามารถใช้ตรวจสอบอีก Key นึงได้ ว่า Key นั้นเป็นคู่ Key ของตัวเองรึเปล่า 


### กระบวนการทำงาน

ใช้ Key นึงเข้ารหัส แล้วใช้อีก Key นึงถอดรหัส (คนละ Key กัน)

![](./public-key-flow.png)

### Algorithm ที่นิยมใช้

Algorithm ที่นิยมใช้ในการเข้ารหัสแบบ Key คู่ คือ   
- [RSA (Rivest–Shamir–Adleman)](https://www.wikiwand.com/en/RSA_(cryptosystem))
- [ECC (Elliptic Curve Cryptography)](https://www.wikiwand.com/en/Elliptic-curve_cryptography)

### ข้อดี

- แชร์ Key ได้ โดยการเก็บ Key นึงไว้เก็บตัวเอง แล้วแชร์อีก Key นึงให้กับคนอื่น ๆ

### ข้อเสีย

- ช้ากว่าแบบ Key เดียว 
- ไม่เหมาะกับการนำไปเข้ารหัสกับข้อมูลที่มีขนาดใหญ่ เพราะมันช้า 

### แนะนำ

ปกติการเข้ารหัสข้อมูลแบบ Key คู่ (ถ้าต้องเข้ารหัสกับข้อมูลที่มีขนาดค่อนข้างใหญ่) เค้าจะใช้วิธีการเข้ารหัสข้อมูลด้วย Secret Key ก่อน 
  
แล้วจึงใช้การเข้ารหัสแบบ Key คู่ เข้ารหัส Secret Key อีกที   
พร้อมกับแนบ **Secret Key ที่ถูกเข้ารหัสแล้ว + ข้อมูลที่ถูกเข้ารหัส ด้วย Secret Key** ไปด้วยกัน เพื่อให้ปลายทางนำไปถอดข้อมูลต่อไป
 
### ทำไมต้องใช้ Key คู่

> เพราะบางกระบวนการ ไม่สามารถที่จะใช้การเข้ารหัสแบบ Key เดียวได้

**ทำความเข้าใจตรงนี้กันก่อน**
  
การเข้ารหัสต่าง ๆ เราสามารถที่จะเอามาใช้สำหรับการเข้ารหัส/ถอดรหัส เพื่อให้ข้อมูลชุดนั้นเป็นความลับ (Encryption/Decryption) ในระหว่างการส่งข้อมูล  
   
หรือ
    
เอามาใช้กับ กระบวนการที่เรียกว่า `การทำลายเซ็นต์ดิจิตอล (Digital Signature)` ก็ได้   
  
**เดี๋ยว**

ลายเซ็นต์ดิจิตอล ไม่ใช่แบบนี้น่ะ

<img src="./signature.png?v=1" width="230">

**ไม่ใช่ลายเซ็นต์ตัวหนังสือ**ที่เราเซ็นต์ลงไปบน Tablet ตอนที่เค้าเอาของมาส่งหน้าบ้านเราน่ะ บางคนยังเข้าใจผิดคิดว่าเป็นแบบนี้อยู่ 
  
แต่ลายเซ็นต์ดิจิตอลจริง ๆ เป็นแบบนี้ คือ  

เค้าจะใช้กระบวนการเข้ารหัสมาช่วยในการเซ็นต์ (Sign)  
แล้วก็ใช้กระบวนการถอดรหัสมาช่วยในการตรวจสอบลายเซ็นต์ (Verify)

![](./digital-signature.png?v=1) 

เพื่อใช้สำหรับตรวสอบ และยืนยันว่า ลายเซ็นนั้น เป็นของคนที่เซ็นต์ลงไปจริง ๆ   
และเอกสารที่คน ๆ นั้นเซ็นต์ลงไป ไม่ได้ถูกแก้ไขเปลี่ยนแปลงระหว่างการส่งแต่อย่างใด   
   
> ถ้าเราต้องการส่งเอกสารออนไลน์ (Online) โดยไม่ใช้กระดาษ ให้มีความน่าเชื่อถือ การทำลายเซ็นต์ดิจิตอล สามารถเอามาใช้แก้ปัญหานี้ได้ 

โดยการใช้ความสามารถของการเข้ารหัสแบบ Public Key / Private Key 

**หมายเหตุ**     
  
สามารถอ่านเรื่องลายเซ็นต์ดิจิตอล ได้จากบทความนี้

- [กระบวนการทำลายเซ็นต์ดิจิตอล (Digital Signature Methodology)](/blog/digital-signature-methodology/)

ตัวอย่างเบื้องต้น  
  
ขอยกตัวอย่าง ในลักษณะของการทำ Signature (Digital Signature แบบย่อ)   
คือ การเอา Keys ไปใช้ในการ **Sign / Verify Token** สำหรับระบบ Authentication  
  
---

**ปัญหา**  

ถ้าเราพัฒนาระบบแบบใช้ Key เดียว หรือแบบ Secret Key   
บางครั้ง เราอาจเจอสถานการณ์ที่ต้องมีการ**แชร์ (Share) Key** ให้คนอื่นเกิดขึ้น
       
ซึ่งจริง ๆ แล้ว เราไม่ได้อยากที่จะยก Secret Key เราให้ใคร     
เพราะถ้าเราให้ Secret Key ใครไป มันจะเหมือนกับว่า อีกฝั่งนึง ได้สิทธิ์ของเราไปเต็ม ๆ
  
เพราะเค้ามี Key เรา เค้าจะทำอะไรใน**นามของเรา**ก็ได้   
เพราะ Key นั้นเป็น Key ของระบบเรา

เช่น 
  
มีการเอา Secret Key ไปใช้กับเรื่องของ Authentication  
   
ถ้าเราเอา Secret Key มาใช้สำหรับการ **Sign Token**   
แล้วเรา Share Secret Key เรา ให้ระบบอื่น ๆ เอาไปใช้ด้วย 
(สมมติว่ามีระบบอื่นต้องการ Plug หรือ เชื่อมต่อ (Integrate) เข้ามายังระบบเรา)  
และคนที่พัฒนาระบบนั้น รู้วิธีการ Sign Token ที่เราใช้   

ระบบอื่น ๆ สามารถที่จะ Sign Token ขึ้นมาใช้เองได้   
และสามารถใส่ข้อมูลอะไรลงไปใน Token ก็ได้ 
  
ทำให้ระบบนั้นสามารถที่จะควบคุม หรือ กำหนดบทบาทอะไรต่าง ๆ ของข้อมูล User Login ในระบบเองได้ทั้งหมดเลย 
ทั้ง ๆ ที่ระบบนนั้นไม่ใช่ระบบ Authentication  
  
ซึ่งจริง ๆ แล้ว เหตุการณ์แบบนี้เราไม่ได้ต้องการให้มันเกิดขึ้น 
เราต้องการแค่ว่า ยก Secret Key ให้ระบบนึงไป โดยมีวัตถุประสงค์ว่า ต้องการให้ระบบนั้น เอา Secret Key ไปใช้สำหรับ การ **Verify Token** เท่านั้น

---

**วิธีแก้ไข**

ถ้าเราเปลี่ยนจากการใช้ Secret Key มาใช้แบบ Key คู่ หรือแบบ Keypair
เราสามารถที่จะยก Key ชุดนึง (Public Key) ของเราให้กับระบบอื่น ๆ ได้   
  
เวลา Sign Token เราก็จะใช้ Private Key ในการ Sign **ที่ระบบเรา** (ระบบ Authentication)   
ส่วนระบบอื่น ๆ ก็ใช้ Public Key ในการ Verify Token แทน 
  
ทำให้ไม่ต้องกังวลว่าระบบอื่น ๆ จะสามารถ Sign Token ขึ้นมาใช้เองได้ เพราะเค้าไม่มี Private Key ของระบบเรา   
  
ต่อให้เค้าใช้ Public Key Sign Token ขึ้นมา   
ตอน Verify Token ก็จะ Verify ไม่ผ่าน 

เพราะเราจะใช้ Public Key Verify Token นั้นด้วย     

> เราไม่สามารถใช้ Key เดิม Sign แล้ว Verify ตัวมันเองได้ ต้องใช้อีก Key นึงที่เป็นคู่ของมันเท่านั้น  
  
Public Key อื่น ๆ ที่ไม่ใช่คู่ Key ของมัน ก็ไม่สามารถเอามาใช้ Verify แทนกันได้   
   
นี่จึงเป็นข้อได้เปรียบนึงของการใช้ การเข้ารหัสแบบ Public Key / Priavte Key (Keypair)
  
ตัวอย่างอื่น ๆ ก็มีอีกมากมาย สามารถดูตัวอย่างได้จาก หัวข้อ   

-  **Public Key / Private Key เอาไปใช้ทำอะไรบ้าง** 

ด้านล่าง 

# การเลือกใช้ Encryption

![](./selection.jpg)

*Image from [https://www.brandbuffet.in.th/wp-content/uploads/2018/07/shutterstock-rockthatstock-1.jpg](https://www.brandbuffet.in.th/wp-content/uploads/2018/07/shutterstock-rockthatstock-1.jpg)*

การใช้ Key หรือ Encryption ทั้ง  2 แบบ มีข้อดี/ข้อเสีย แตกต่างกัน ทั้งนี้ 

> จะเลือกใช้ Encryption แบบใด ขึ้นอยู่กับวัตถุประสงค์ และข้อจำกัดต่าง ๆ ที่ทำให้ต้องเลือกใช้ Encryption แบบนั้น

เช่น

ถ้าต้องการ**ความเร็ว**ในการเข้ารหัส (Encryption) / ถอดรหัส (Decryption)  
**และ** Key ที่ใช้อยู่ไม่ได้ต้องการเปิดเผยให้ใคร (เป็นความลับ เข้ารหัสเอง ถอดรหัสเอง)    
ก็ให้เลือกใช้ การเข้ารหัสแบบ Key เดียว หรือ Secret Key หรือ Symmetric Encryption
  
### หมายเหตุ 

ที่เร็ว เพราะโดยปกติ แบบ Key เดียว จะมีขนาดเล็กกว่าแบบ Key คู่ จึงทำให้การเข้ารหัสนั้นสามารถทำได้เร็วกว่า
  
---  

**แต่**ถ้าต้องการเปิดเผย Key ให้คนอื่นใช้ร่วมด้วย (Share Key)     
ก็ให้เลือกใช้ การเข้ารหัส/ถอดรหัส แบบ Key คู่ หรือ Keypair หรือ Asymmetric Encryption คือ 
  
เราจะเปิดเผย Key นึงเป็นสาธารณะ   
ให้ใครก็ได้สามารถเข้าถึง (Access) Key นั้นได้ เราเรียก Key นี้ว่า `Public Key`  
ใครที่อยากจะส่งข้อมูลให้เรา ก็สามารถใช้ Public Key นี้ เอามาเข้ารหัสได้

และเราจะเก็บ Key นึงไว้กับตัวเอง ไม่เปิดเผยให้ใครเห็น เราเรียก Key นี้ว่า `Private Key`  
เมื่ออีกฝ่ายส่งข้อมูลมาถึงเรา เราก็จะใช้ Private Key ของเรา ถอดรหัสข้อมูลออกมา
   
คนอื่นจะไม่สามารถใช้ Key ใด ๆ มาถอดรหัสข้อมูลที่ส่งมาได้  
ต้องใช้ Key ที่ถูกสร้างขึ้นมาคู่กันเสมอ  ถึงจะถอดรหัสออกมาได้   
  
บางครั้ง ก็มีการใช้คุณสมบัติและความสามารถของ Key ทั้ง 2 แบบช่วยกัน เช่น การทำงานของ Https เป็นต้น 

# RSA (Rivest–Shamir–Adleman)

![](./creators-of-RSA.png?v=1)

`RSA` ย่อมาจาก `Rivest–Shamir–Adleman` เป็นหนึ่งในวิธีการ หรือ อัลกอริทึม (Algorithm) ที่นิยมใช้มากที่สุด 
สำหรับการเข้ารหัสแบบ Public Key / Private Key
   
แต่ละภาษาโปรแกรมมิ่ง จะมีการเขียน Code หรือ Implement ตัว RSA ขึ้นมา  
เพื่อให้โปรแกรมเมอร์ สามารถนำ RSA ไปช่วยในการ สร้างรหัส เข้ารหัส/ถอดรหัส แบบ Asymmetric Encryption ได้ 
โดยที่ไม่ต้องเขียน Code ส่วนนี้ขึ้นมาเอง 
  
### หมายเหตุ

**RSA** มาจากอักษรตัวแรกของนามสกุลของ 3 ผู้คิดค้น Algorithm นี้ คือ 
- [Ron **R**ivest](https://www.wikiwand.com/en/Ron_Rivest)
- [Adi **S**hamir](https://www.wikiwand.com/en/Adi_Shamir)
- [Leonard **A**dleman](https://www.wikiwand.com/en/Leonard_Adleman)

# Public Key / Private Key เอาไปใช้ทำอะไรบ้าง

ตัวอย่างของการนำ กระบวนการเข้ารหัสแบบ Public Key / Private Key (Public Key Crytography) ไปใช้ได้แก่ 

- การทำ Digital Certificate เพื่อใช้สำหรับการทำ Https หรือ นำไปใช้กับเรื่อง Digital Signature ลองอ่านจากบทความนี้ดูครับ  [ทำความรู้จักกับ X.509 Certificate พื้นฐานสำหรับการทำ Https และ Security อื่น ๆ](/blog/what-is-x509-certificate/)
- การทำงานของ SSH ที่มีการใช้ Public Key / Private Key ในการทำ Authentication ตัวอย่างจากบทความนี้ [การติดตั้งและใช้งาน SSH บน Ubuntu Server](/blog/ssh-ubuntu-server/)
- การใช้งานกับ JWT (Json Web Token) สำหรับการ Sign และ Verify Token ด้วย RSA Algorithm 
- การใช้งานกับ Blockchain เช่น BitCoin ที่ใช้ Public Key ในการเป็น Bitcoin Address และใช้ Private Key ในการเป็น Owner Key ลองอ่านบทความนี้ดู [Blockchain for Geek ... เบื้องหลังการทำงานฉบับ Technical ตัวอย่างจาก Bitcoin โดย NuuNeoi](https://nuuneoi.com/blog/blog.php?read_id=901)
- การทำ Credentials ใน Firebase ของ Google (JSON File) เพื่อให้เราสามารถเข้าใช้งาน Service ต่าง ๆ ของ Firebase ได้ 
- เรื่องอื่น ๆ ที่มีการใช้ PKI (Public Key Infrastructure) ลองอ่านบทความนี้ดูครับ [โครงสร้างการเข้ารหัสข้อมูลแบบกุญแจสาธารณะ (Public Key Infrastructure)](/blog/public-key-infrastructure/)

จะเห็นว่าเรื่อง Public Key / Private Key แทบจะเป็นพื้นฐานของการทำ Security สำหรับทุก ๆ เรื่อง ในปัจจุบันนี้เลยก็ว่าได้  


# วิธีที่ใช้ในการสร้าง Public Key / Private Key  

<img src="./create-keys.png?v=2" width="350"/>

*Image from [https://news.gearvn.com/wp-content/uploads/2020/02/Build-Vs-Buy-Pt-1-Value-of-Custom-Software.jpg](https://news.gearvn.com/wp-content/uploads/2020/02/Build-Vs-Buy-Pt-1-Value-of-Custom-Software.jpg)*

เราสามารถสร้าง (Generate) Public Key / Private Key ได้หลายวิธี ทั้ง

- การใช้เครื่องมือต่าง ๆ ที่มีอยู่ ช่วยสร้างขึ้นมา เช่น 
    - [OpenSSL](https://wiki.openssl.org/index.php/Command_Line_Utilities) (Command Line Tool)
    - [Java Keytool](/blog/java-keytool/?series=java-security) (Command Line Tool)
    - [SSH Keygen](/blog/ssh-ubuntu-server/) (Command Line Tool)
    - เครื่องมือแบบ GUI ต่าง ๆ เช่น [KeyStore Explorer](https://keystore-explorer.org/)
    - อื่น ๆ
- การเขียนโปรแกรมด้วยภาษาโปรแกรมมิ่ง (Programming) ต่าง ๆ ที่รองรับการเข้ารหัส/ถอดรหัส  
- อื่น ๆ

ในบทความนี้จะยกตัวอย่าง การสร้าง Public Key / Private Key ด้วยภาษา Java ซึ่งเป็นภาษาโปรแกรมมิ่งตัวนึง ที่ได้รับความนิยมอย่างกว้างขวางในปัจจุบันนี้

# Key Format 

ก่อนที่จะเริ่มเขียนโปรแกรม เราจะต้องเข้าใจเรื่องของ Key Format กันก่อน เพราะมันมีผลกับการเลือกใช้ Code  ในการเขียนโปรแกรม ดังนี้

- **Public Key** เป็น Key ที่มี Format เป็น `X.509` 
- **Private Key** เป็น Key ที่มี Format เป็น `PKCS#8`

### X.509 คืออะไร

[X.509](https://www.wikiwand.com/th/X.509) เป็นมาตรฐาน (Standard) ที่ใช้สำหรับโครงสร้างพื้นฐานกุญแจสาธารณะ (PKI : Public Key Infrastructure) 
  
ถ้าเป็นกระบวนการ ที่ใช้การเข้ารหัสแบบที่มี Public Key   
มาตรฐานที่ใช้เป็นตัวกำหนดเรื่องของ Public Key ก็คือมาตรฐาน X.509 

### PKCS คืออะไร 

[PKCS](https://www.wikiwand.com/en/PKCS) ย่อมาจาก **Public Key Cryptography Standards** เป็นกลุ่มของข้อกำหนด และมาตรฐาน (Standard) ต่าง ๆ สำหรับการเข้ารหัสแบบที่ใช้ Public Key   
  
โดย PCKS มีการกำหนดเป็นตัวเลขตั้งแต่ `PKCS#1`, `PKCS#2`, `PKCS#3` ไปจนถึง `PKCS#15` (ในปัจจุบัน) 

- PKCS#1 เป็นมาตรฐานสำหรับ RSA Cryptography Standard
- PKCS#2 ไม่ได้ใช้แล้ว (ถูกยกเลิก)
- PKCS#3 เป็นเรื่องของ Diffie–Hellman Key Agreement Standard 
- PKCS#4 ไม่ใช้แล้ว (ถูกยกเลิก) 
- PKCS#5 เป็นเรื่องของ Password-based Encryption Standard
- และ PKCS อื่น ๆ สามารถอ่านเพิ่มเติมได้จาก [https://www.wikiwand.com/en/PKCS](https://www.wikiwand.com/en/PKCS)

ส่วน `PKCS#8` เป็นเรื่องของมาตรฐาน ข้อกำหนด และรูปแบบต่าง ๆ ของ Private Key (Private-Key Information Syntax Standard) 
  
ถ้าเรามีอะไรที่ต้องยุ่งกับ Private Key ให้ Focus ไปที่ PKCS ตัวนี้   

# ตัวอย่าง Code ภาษา Java 

<img src="./java.jpg" width="300"> 

### การสร้าง Public Key / Private Key แบบ RSA

จะใช้ class `java.security.KeyPairGenerator` เป็นตัวช่วยสร้าง ดังนี้ 

```java
//Generate Keypair
final KeyPairGenerator keyPairGenerator = KeyPairGenerator.getInstance("RSA");

//กำหนดขนาด Key เป็น 2,048 bits
keyPairGenerator.initialize(2048);

final KeyPair keyPair = keyPairGenerator.genKeyPair();

final PublicKey publicKey = keyPair.getPublic();
final PrivateKey privateKey = keyPair.getPrivate();
```

ตอนนี้เราได้ Public Key และ Private Key ที่มีความสัมพันธ์กันขึ้นมาแล้ว   
  
ต่อมาเราจะลอง Print ผลลัพธ์ หรือ Attributes ต่าง ๆ ของ Key ออกมาดู ว่ามีค่าอะไรบ้าง

### Print Key Attributes

```java
System.out.println("publicKey");
System.out.println("publicKey.algorithm => " + publicKey.getAlgorithm());
System.out.println("publicKey.format => " + publicKey.getFormat());
System.out.println("publicKey.encoded.length => " + publicKey.getEncoded().length);

System.out.println("privateKey");
System.out.println("privateKey.algorithm => " + privateKey.getAlgorithm());
System.out.println("privateKey.format => " + privateKey.getFormat());
System.out.println("privateKey.encoded.length => " + privateKey.getEncoded().length);
```

output

```plaintext
publicKey.algorithm => RSA
publicKey.format => X.509
publicKey.encoded.length => 294
//
privateKey.algorithm => RSA
privateKey.format => PKCS#8
privateKey.encoded.length => 1219
```

สังเกตุว่า 

- **Public Key** จะมี Format เป็น `X.509` และ 
- **Private Key** มี Format เป็น `PKCS#8`  

ถัดมา   
  
Key ที่เราสร้างขึ้นมาแต่ละ Key เราสามารถ Get ค่าได้จาก Method `byte[] getEncoded()` ซึ่งจะมีการ Return Key ออกมาเป็น Byte Array (หลาย Byte) 
   
เราสามารถนำ Key นี้ไปใช้ได้เลย เพราะเป็น Key ที่ถูกต้องแล้ว  

### Base64 Format 

แต่ถ้าเราต้องการ Save Key เก็บไว้ และต้องการให้คนอ่านได้ เราจะต้องทำการแปลง Byte Array นั้นไปเป็น Format ที่คนพอจะอ่านรู้เรื่องก่อน นั่นก็คือ Base64 Format ดังนี้

```java
private static String convertToBase64PublicKey(final byte[] bytes) {
    return new StringBuilder()
            .append("-----BEGIN PUBLIC KEY-----")
            .append("\n")
            .append(Base64.getEncoder().encodeToString(bytes))
            .append("\n")
            .append("-----END PUBLIC KEY-----")
            .toString();
}

private static String convertToBase64PrivateKey(final byte[] bytes) {
    return new StringBuilder()
            .append("-----BEGIN PRIVATE KEY-----")
            .append("\n")
            .append(Base64.getEncoder().encodeToString(bytes))
            .append("\n")
            .append("-----END PRIVATE KEY-----")
            .toString();
}
```

สังเกตุว่า เราจะมีการครอบด้วย 

```plaintext
-----BEGIN XXXXX KEY-----

//และ

-----END XXXXX KEY-----
```

ลองดูผลลัพธ์ สมมติมีการเรียกใช้ 2 Method นี้
  
output

```plaintext
-----BEGIN PUBLIC KEY-----
MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAj//uo4lZW6f1qgeKJVSULHI4fd6VZ8HOiUNYpWsh1lLazm5TtMqHjgYbh42L3fdz/pszO8S02EP9xS9aCp11Qy5MFF8mI5GkBra0NN7okNGcNU4zAuyxM8mDyS6amGTZX3ZM0xAe/WneH+YjHHYZ1OfRMev2JKEVvOqU8z4DAqyfQsvfWJrLxNQbtg5jjQCaV/lsYwi3gTZm6DOxeeLCZqy5nWrHkqUPx18utwF2TwKbrKaxAqkxxjGH7EAnwF9PrgC2tFoh0NHI/uHVdmgmHlvHPerQIveOjH/C9QCs+Hgb/Gt6tD2P2X4KVfxiaIToXN0B5F89ngJtVF6zFfVDiwIDAQAB
-----END PUBLIC KEY-----
```

และ

```plaintext
-----BEGIN PRIVATE KEY-----
MIIEvwIBADANBgkqhkiG9w0BAQEFAASCBKkwggSlAgEAAoIBAQCP/+6jiVlbp/WqB4olVJQscjh93pVnwc6JQ1ilayHWUtrOblO0yoeOBhuHjYvd93P+mzM7xLTYQ/3FL1oKnXVDLkwUXyYjkaQGtrQ03uiQ0Zw1TjMC7LEzyYPJLpqYZNlfdkzTEB79ad4f5iMcdhnU59Ex6/YkoRW86pTzPgMCrJ9Cy99YmsvE1Bu2DmONAJpX+WxjCLeBNmboM7F54sJmrLmdaseSpQ/HXy63AXZPApusprECqTHGMYfsQCfAX0+uALa0WiHQ0cj+4dV2aCYeW8c96tAi946Mf8L1AKz4eBv8a3q0PY/ZfgpV/GJohOhc3QHkXz2eAm1UXrMV9UOLAgMBAAECggEBAI5O0IjfkOaqu3ZYUycHShQOoVOLKD3M4471dmKr2FnVshV2JNUznfk2gfhZY1NuXDzPJje38z0THHTFkgeRirRkyZ0MV0Wphd94qejiLhYIgIaRjIokXg8e5FVq8C8Q412bLNsdQHMSMAl4R1S2RlsI6c2bMrsKUtBLR/6HVzRI4xKXLuNccsGA/PiFq/bQa3WzGpbaKhHRzS9VHmbf/qMbq4nkc6LUs49wiCZkWlFstl8Pw4cLIqif6YWf6FrjAX5Q83qTMh5y6RMlyKkuqBxK+zyyh3RL22vAuwWwp/uX/KGmTtFJpNrisHiruvnAGKv3BiPyvGUFw9DciFixmbECgYEA3XG7HTXTlIAfr1dptSRJDijPYYc4GVC/RrMnV/cauoiwszvE26mSksoDp8IxnwCAflNucmGMSx/6WtlxVMNabp9aAcQDcKJj4nWUNoKjggus1IEMxrlx0N0yASgG3Gtcl3dO0d5MhtaolXyfWtxajAHVY9c+bXrdr5xEj6IfzukCgYEApnhxSZ84sgiG6S4NEoDn0u2NYv2ZWT5gCdnB0OJfyTatI8Vee8n8xl+ntjfbvVa5xLs/lBH2OcUkgdjshDOOV5puJT0mwX3HOlf+pOevBddr1p22sA9KYahAa/e4ictPZiQ4q4JgjdxfYMvD+yh3zpMSQ+5xw/fUeMJTgI9K/lMCgYEAn6Pz7tT1GSNctD1iOXJVMF3/UyH2MVni6wcQn/vGSx9rs2qtOmZ/Ak+cXv5CY4wrFebzwoXMbAQ7qe8EIsVKlmFOs+MpT7PiKkn1dW6sjX35NKFsIn9iK96qw+alO5YyhAdAzU9i//oUQuA6yXf91t0jhvyPRsHCu2z+iEWqhLECgYAz29Fu3esLixx8B5yK5x1Q2C/zZo0fAA9rAisep2aviBjny9RjO8lDAwl7+mq50QqN/scPmYja9k8pJCqKBIWTRMiLUUGBhW1K/56UQJiFeVZexULkFd9WDNQEzmbuhid16lK9GyB5EO2ledTTqQepkqdeAinuooXOGLtqkTkLgQKBgQC1wKNu4av+gv8v7qsWVyA0KZCHzviEnOA4O/uovEtUTTgTx6jtjkxKtMlLhCa99amGEq+mGr7ZlqpCvcMJyKD/ybgoPujtOPdJD7kUlfNdf4lfhaUTdlk1f7J4kaapu0PUfF9u/dPm8Zeg826bWgATNdY+DqMNLSOYVrdHnt8kkg==
-----END PRIVATE KEY-----
```

เราสามารถนำ Key นี้ ไป Save เป็น File นามสกุลต่าง ๆ เก็บไว้ได้เลย เช่น `.pem`, `.key`, `.pub` etc.

### การอ่าน Key Base64 Format ขึ้นมาใช้งาน

ทำได้ดังนี้

```java
private static String removeKeyBlock(final String key){
    return key
            .replaceAll("-----BEGIN.*KEY-----", "")
            .replaceAll("-----END.*KEY-----", "")
            .replaceAll("\\s+", "");
}

private static PublicKey convertToPublicKey(final String base64PublicKey) throws NoSuchAlgorithmException, InvalidKeySpecException {
    final String realKey = removeKeyBlock(base64PublicKey);
    final byte[] keyBytes = Base64.getDecoder().decode(realKey);
    final X509EncodedKeySpec spec = new X509EncodedKeySpec(keyBytes);
    final KeyFactory keyFactory = KeyFactory.getInstance("RSA");
    return keyFactory.generatePublic(spec);
}

private static PrivateKey convertToPrivateKey(final String base64PrivateKey) throws NoSuchAlgorithmException, InvalidKeySpecException {
    final String realKey = removeKeyBlock(base64PrivateKey);
    final byte[] keyBytes = Base64.getDecoder().decode(realKey);
    final PKCS8EncodedKeySpec spec = new PKCS8EncodedKeySpec(keyBytes);
    final KeyFactory keyFactory = KeyFactory.getInstance("RSA");
    return keyFactory.generatePrivate(spec);
}
```

สังเกตว่าเราจะทำการ Replace

```plaintext
-----BEGIN XXXXX KEY-----

//และ

-----END XXXXX KEY-----
```

ด้วย Empty String ก่อน 
  
เพราะ Key จริง ๆ อยู่ข้างใน Block นี้  
จากนั้นก็ **Decode Base64** กลับมาเป็น Byte Array แล้วใช้ KeySpec อ่าน Key ขึ้นมา     

**สังเกตุ**

สังเกตว่า KeySpec ที่ใช้กับ Public Key และ Private Key ไม่เหมือนกัน 

- **Public Key** ใช้ `X509EncodedKeySpec` 
- **Private Key** ใช้ `PKCS8EncodedKeySpec` 

เพราะว่าแต่ละ Key มี Key Format ที่ **ไม่เหมือนกัน** ตามที่ได้อธิบายไว้ในหัวข้อที่ผ่านมา  
  
เมื่อเราเรียกใช้งาน Method นี้ ก็จะประมาณนี้ 

```java
final PublicKey aPublicKey = convertToPublicKey(base64PublicKey);
final PrivateKey aPrivateKey = convertToPrivateKey(base64PrivateKey);
```

เราสามารถนำ Public Key / Private Key นี้ไปใช้งานต่อได้เลย  

### Code เต็ม ๆ

```java
package me.jittagornp.learning.keypair;

import java.security.KeyFactory;
import java.security.KeyPair;
import java.security.KeyPairGenerator;
import java.security.NoSuchAlgorithmException;
import java.security.PrivateKey;
import java.security.PublicKey;
import java.security.spec.InvalidKeySpecException;
import java.security.spec.PKCS8EncodedKeySpec;
import java.security.spec.X509EncodedKeySpec;
import java.util.Base64;

/**
 * @author jitta
 */
public class JavaKeyPair {

    public static void main(String[] args) throws NoSuchAlgorithmException, InvalidKeySpecException {

        //Generate Keypair
        final KeyPairGenerator keyPairGenerator = KeyPairGenerator.getInstance("RSA");

        keyPairGenerator.initialize(2048);

        final KeyPair keyPair = keyPairGenerator.genKeyPair();

        final PublicKey publicKey = keyPair.getPublic();
        final PrivateKey privateKey = keyPair.getPrivate();

        final String base64PublicKey = convertToBase64PublicKey(publicKey.getEncoded());
        final String base64PrivateKey = convertToBase64PrivateKey(privateKey.getEncoded());

        System.out.println("Generating Keypair");
        System.out.println("");
        System.out.println("publicKey");
        System.out.println("publicKey.algorithm => " + publicKey.getAlgorithm());
        System.out.println("publicKey.format => " + publicKey.getFormat());
        System.out.println("publicKey.encoded.length => " + publicKey.getEncoded().length);
        System.out.println(base64PublicKey);
        System.out.println("======================================================");

        System.out.println("privateKey");
        System.out.println("privateKey.algorithm => " + privateKey.getAlgorithm());
        System.out.println("privateKey.format => " + privateKey.getFormat());
        System.out.println("privateKey.encoded.length => " + privateKey.getEncoded().length);
        System.out.println(base64PrivateKey);
        System.out.println("======================================================");

        System.out.println("Reading Keypair");
        System.out.println("");

        final PublicKey aPublicKey = convertToPublicKey(base64PublicKey);
        final PrivateKey aPrivateKey = convertToPrivateKey(base64PrivateKey);

        //Do something...
    }

    private static String convertToBase64PublicKey(final byte[] bytes) {
        return new StringBuilder()
                .append("-----BEGIN PUBLIC KEY-----")
                .append("\n")
                .append(Base64.getEncoder().encodeToString(bytes))
                .append("\n")
                .append("-----END PUBLIC KEY-----")
                .toString();
    }

    private static String convertToBase64PrivateKey(final byte[] bytes) {
        return new StringBuilder()
                .append("-----BEGIN PRIVATE KEY-----")
                .append("\n")
                .append(Base64.getEncoder().encodeToString(bytes))
                .append("\n")
                .append("-----END PRIVATE KEY-----")
                .toString();
    }
    
    private static String removeKeyBlock(final String key){
        return key
                .replaceAll("-----BEGIN.*KEY-----", "")
                .replaceAll("-----END.*KEY-----", "")
                .replaceAll("\\s+", "");
    }

    private static PublicKey convertToPublicKey(final String base64PublicKey) throws NoSuchAlgorithmException, InvalidKeySpecException {
        final String realKey = removeKeyBlock(base64PublicKey);
        final byte[] keyBytes = Base64.getDecoder().decode(realKey);
        final X509EncodedKeySpec spec = new X509EncodedKeySpec(keyBytes);
        final KeyFactory keyFactory = KeyFactory.getInstance("RSA");
        return keyFactory.generatePublic(spec);
    }

    private static PrivateKey convertToPrivateKey(final String base64PrivateKey) throws NoSuchAlgorithmException, InvalidKeySpecException {
        final String realKey = removeKeyBlock(base64PrivateKey);
        final byte[] keyBytes = Base64.getDecoder().decode(realKey);
        final PKCS8EncodedKeySpec spec = new PKCS8EncodedKeySpec(keyBytes);
        final KeyFactory keyFactory = KeyFactory.getInstance("RSA");
        return keyFactory.generatePrivate(spec);
    }
}

```

# ทดสอบเข้ารหัส/ถอดรหัส ด้วย Public Key / Private Key

![](./encrypt-decrypt-hello-world.png?v=1)

เมื่อเราได้ Keys มาแล้ว   
ต่อมา เรามาลองเขียน Code เพื่อทดสอบการเข้ารหัส/ถอดรหัส กันดู ดังนี้  
  
เขียน Method สำหรับรับข้อมูลมาทำการเข้ารหัส/ถอดรหัส  
```java
//เข้ารหัส
public static byte[] encrypt(final byte[] data, final PublicKey publicKey) throws NoSuchAlgorithmException, NoSuchPaddingException, InvalidKeyException, IllegalBlockSizeException, BadPaddingException {
    final Cipher cipher = Cipher.getInstance("RSA");
    cipher.init(Cipher.ENCRYPT_MODE, publicKey);
    return cipher.doFinal(data);
}

//ถอดรหัส
public static byte[] decrypt(final byte[] data, final PrivateKey privateKey) throws NoSuchAlgorithmException, NoSuchPaddingException, InvalidKeyException, IllegalBlockSizeException, BadPaddingException {
    final Cipher cipher = Cipher.getInstance("RSA");
    cipher.init(Cipher.DECRYPT_MODE, privateKey);
    return cipher.doFinal(data);
}
```

โดยเราจะใช้ class `javax.crypto.Cipher` ช่วย ทำทั้งเข้ารหัส และถอดรหัส 
  
สังเกตตรง `cipher.init()` จะมีการกำหนด **Mode** ที่ใช้ นั่นคือ

- ถ้าต้องการจะเข้ารหัส ให้ใช้ Mode เป็น `Cipher.ENCRYPT_MODE` 
- แต่ถ้าต้องการจะถอดรหัส ให้ใช้ Mode เป็น `Cipher.DECRYPT_MODE` 

แล้วส่ง Key เข้าไปเป็น Parameter ตัวที่ 2 
  
ทดสอบ    

```java
final String message = "Hello World";
        
final byte[] encryptedBytes = encrypt(message.getBytes(), publicKey); 
final String encrypted = new String(encryptedBytes);
final String encryptedBase64 = Base64.getEncoder().withoutPadding().encodeToString(encryptedBytes);

final byte[] decryptedDecodeBytes = Base64.getDecoder().decode(encryptedBase64);
final byte[] decryptedBytes = decrypt(decryptedDecodeBytes, privateKey);
final String decrypted = new String(decryptedBytes);
```

และ

```java
System.out.println("message => " + message);
System.out.println("");
System.out.println("Encrypt");
System.out.println("encryptedBytes.length => " + encryptedBytes.length);
System.out.println("encryptedBase64 => " + encryptedBase64);
System.out.println("");
System.out.println("Decrypt");
System.out.println("decryptedDecodeBytes.length => " + decryptedDecodeBytes.length);
System.out.println("decryptedBytes.length => " + decryptedBytes.length);
System.out.println("decrypted => " + decrypted);
```

output

```plaintext
message => Hello World

Encrypt
encryptedBytes.length => 256
encrypted => S�p?��ץ�޴�d��qV�3�t�%z�1}��(Z˄�����Fa#��٨�Z@�6[�UU$�5�5�o�Z�bS�<_��G��&FL�	�$?��܂
.#ߞ�:
<�r����>��-(��3�8�K�0�J���)?�O��F�K��J���^��~+��:�
encryptedBase64 => U/5wgQbii+PXpRLK3rT5ZJvzcVacM/x06yV6zTF9/ZsoWsuEjpvY+PkcAw5GYSPu5NmovFoDQL0RDjZb86evVVUkjjWCNeZvolrgtWJTmTxfmJlHhPcmRkwOEcsJsCQ/q+vcgg0ELiPfntg6BRANPBygcsz17+YQPtjeLSi11TPiHTimS9kwzEoMvBsP+5IpkKgDTwuV4UaGS5H7SsXq017D234r1wu4OhOTAANft8Dn8pQd68lpsG70FcRIdx1CanajPjRE5+kRX/2bUwONEQAKgSOelPnrVTmB9rDvse+7w/Ymao9u81Hd8WY1Ul/4mVWZVuuck9rzAwf2a700AA

Decrypt
decryptedDecodeBytes.length => 256
decryptedBytes.length => 11
decrypted => Hello World
```

Message **"Hello World"** ถูกนำไปใช้เข้ารหัสด้วย Public Key ผ่าน Method `encrypt()`   
  
สังเกตว่า ผลลัพธ์ที่ออกมาในตัวแปร `encrypted` หลังจากที่ทำการแปลงเป็น String แล้ว อ่านไม่รู้เรื่องเลย เพราะเป็น Byte ข้อมูลที่ถูกเข้ารหัสแล้ว 
  
เราไม่สามารถนำอักขระ (Character) ในลักษณะของตัวแปร `encrypted` ไปใช้งานตรง ๆ ได้ เนื่องจากอักขระบางตัว ไม่รองรับกับการใช้งานบางอย่าง ยกเว้นว่าเราจะ Save Byte ข้อมูลนี้เก็บไว้เป็น File หรือ Database หรือ อื่น ๆ ที่สามารถเก็บ Byte ข้อมูลนี้ได้   
  
เราจึงต้องทำการแปลงไปเป็น Base64 ก่อน เพื่อให้สามารถนำไปใช้กับงานอื่น ๆ ได้ และเราก็มักจะเห็น Format การเข้ารหัสข้อมูลแบบนี้กันบ่อย ๆ คือ 

> เข้ารหัสแล้ว ก็มักที่จะ Encode เป็น Base64 ต่อ  

จากนั้น ก็ลองนำข้อมูลที่ถูกเข้ารหัสแล้ว มาทำการถอดรหัสด้วย Private Key ผ่าน Method `decrypt()` ดู ก็จะเห็นว่า ได้คำว่า "Hello World" ออกมาเหมือนเดิม 

### Code เต็ม ๆ

```java
package me.jittagornp.learning.keypair;

import java.security.InvalidKeyException;
import java.security.KeyPair;
import java.security.KeyPairGenerator;
import java.security.NoSuchAlgorithmException;
import java.security.PrivateKey;
import java.security.PublicKey;
import java.util.Base64;
import javax.crypto.BadPaddingException;
import javax.crypto.Cipher;
import javax.crypto.IllegalBlockSizeException;
import javax.crypto.NoSuchPaddingException;

/**
 * @author jitta
 */
public class Encyption {
    
    public static void main(String[] args) throws Exception {
        
        //Generate Keypair
        final KeyPairGenerator keyPairGenerator = KeyPairGenerator.getInstance("RSA");

        keyPairGenerator.initialize(2048);

        final KeyPair keyPair = keyPairGenerator.genKeyPair();

        final PublicKey publicKey = keyPair.getPublic();
        final PrivateKey privateKey = keyPair.getPrivate();
        //======================================================================
        
        final String message = "Hello World";
        
        final byte[] encryptedBytes = encrypt(message.getBytes(), publicKey); 
        final String encrypted = new String(encryptedBytes);
        final String encryptedBase64 = Base64.getEncoder().withoutPadding().encodeToString(encryptedBytes);
        
        final byte[] decryptedDecodeBytes = Base64.getDecoder().decode(encryptedBase64);
        final byte[] decryptedBytes = decrypt(decryptedDecodeBytes, privateKey);
        final String decrypted = new String(decryptedBytes);
        
        System.out.println("message => " + message);
        System.out.println("");
        System.out.println("Encrypt");
        System.out.println("encryptedBytes.length => " + encryptedBytes.length);
        System.out.println("encrypted => " + encrypted);
        System.out.println("encryptedBase64 => " + encryptedBase64);
        System.out.println("");
        System.out.println("Decrypt");
        System.out.println("decryptedDecodeBytes.length => " + decryptedDecodeBytes.length);
        System.out.println("decryptedBytes.length => " + decryptedBytes.length);
        System.out.println("decrypted => " + decrypted);
        
    }

    public static byte[] encrypt(final byte[] data, final PublicKey publicKey) throws NoSuchAlgorithmException, NoSuchPaddingException, InvalidKeyException, IllegalBlockSizeException, BadPaddingException {
        final Cipher cipher = Cipher.getInstance("RSA");
        cipher.init(Cipher.ENCRYPT_MODE, publicKey);
        return cipher.doFinal(data);
    }

    public static byte[] decrypt(final byte[] data, final PrivateKey privateKey) throws NoSuchAlgorithmException, NoSuchPaddingException, InvalidKeyException, IllegalBlockSizeException, BadPaddingException {
        final Cipher cipher = Cipher.getInstance("RSA");
        cipher.init(Cipher.DECRYPT_MODE, privateKey);
        return cipher.doFinal(data);
    }
}
```

สมมติว่า เราใช้ Public Key `encrypt` และลองใช้ Public Key `decrypt` ดู  

```java
public static byte[] encrypt(final byte[] data, final PublicKey publicKey) throws NoSuchAlgorithmException, NoSuchPaddingException, InvalidKeyException, IllegalBlockSizeException, BadPaddingException {
    final Cipher cipher = Cipher.getInstance("RSA");
    cipher.init(Cipher.ENCRYPT_MODE, publicKey);
    return cipher.doFinal(data);
}

public static byte[] decrypt(final byte[] data, final PublicKey publicKey) throws NoSuchAlgorithmException, NoSuchPaddingException, InvalidKeyException, IllegalBlockSizeException, BadPaddingException {
    final Cipher cipher = Cipher.getInstance("RSA");
    cipher.init(Cipher.DECRYPT_MODE, publicKey);
    return cipher.doFinal(data);
}
```

ทดสอบ

```java
final String message = "Hello World";
final byte[] encryptedBytes = encrypt(message.getBytes(), publicKey); 
final byte[] decryptedBytes = decrypt(encryptedBytes, publicKey);
```

จะพบว่ามี Error เกิดขึ้น

```plaintext
Exception in thread "main" javax.crypto.BadPaddingException: Decryption error
```

### สรุป 

การเข้ารหัส/ถอดรหัส จริง ๆ แล้ว เราจะเริ่มจาก Key ประเภทไหน ก็ได้ 

- ถ้าใช้ Public Key เข้ารหัส ก็ต้องใช้ Private Key ถอดรหัสออกมา 
- แต้ถ้าใช้ Private Key เข้ารหัส ก็ต้องใช้ Public key ถอดรหัส

class **Cipher** สามารถทำได้ทั้ง 2 แบบ  
  
แต่ การส่งข้อมูลที่เป็นความลับให้กันจริง ๆ เราจะใช้ Public Key ของคนที่เราต้องการจะส่งข้อมูลให้ มาเข้ารหัส 
พอเค้า ได้รับข้อมูล เค้าจะใช้ Private Key เค้าถอดรหัสออกมา
  
คนอื่นจะถอดรหัสนี้ไม่ได้ เพราะเค้าไม่มี Key ที่สัมพันธ์กัน    

# ทดลองใช้ Public Key / Private Key Sign JWT Token 

<img src="./jwt.jpg" width="400">

ถ้าใครยังไม่รู้จัก JWT (Json Web Token) สามารถอ่านได้จาก 

- [ทำความรู้จักกับ JWT (Json Web Token)](/blog/what-is-jwt/)

เดี๋ยวเราจะลองใช้ JWT Dependency จาก Auth0 ช่วยในการ Sign / Verify ดู จากลิงค์นี้ 

- [https://github.com/auth0/java-jwt](https://github.com/auth0/java-jwt)

เขียน Method Sign

```java
public static String sign(final Map<String, Object> claims, final Algorithm algorithm, final int expiresMinutes) {
    final LocalDateTime now = LocalDateTime.now();
    final LocalDateTime expires = now.plusMinutes(expiresMinutes);
    return JWT.create()
            .withIssuedAt(toDate(now))
            .withExpiresAt(toDate(expires))
            .withClaim("user", claims)
            .sign(algorithm);
}
```

Method `sign()` เราจะส่งข้อมูล (Data) ที่ต้องการจะ Sign เข้ามาที่ตัวแปร `claims` และ ส่ง Algorithm + เวลาที่ต้องการให้ Token หมดอายุ เข้ามาเป็น Parameter ตัวที่ 2 และ 3  

เขียน Method Verify 
```java
public static Map<String, Object> verify(final String token, final Algorithm algorithm) {
    return JWT.require(algorithm)
            .build()
            .verify(token)
            .getClaims()
            .get("user")
            .asMap();
}
```

Method `verify()` เราจะส่ง Token ที่ต้องการ Verify เข้าไปผ่านตัวแปร `token` และ ส่ง Algorithm ที่ใช้ในการ Verify เข้าไปเป็น Parameter ตัวที่ 2
  
### ทดสอบ 

```java
final Map<String, Object> claims = new HashMap<>();
claims.put("id", 1L);
claims.put("name", "จิตกร พิทักษ์เมธากุล");
claims.put("authorities", Arrays.asList("MANAGE_USER"));

final String token = sign(claims, Algorithm.RSA256(null, privateKey), 30);
final Map<String, Object> output = verify(token, Algorithm.RSA256(publicKey, null));

System.out.println("claims => " + claims);
System.out.println("token => " + token);
System.out.println("output => " + output);
```

**สังเกต** 
  
- Method `sign()` ตรง Algorithm `RSA` เราใช้แค่ Private Key และ  
- Method `verify()` ตรง Algorithm `RSA` เราใช้แค่ Public Key 


output

```plaintext
claims => {name=จิตกร พิทักษ์เมธากุล, id=1, authorities=[MANAGE_USER]}
token => eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJkYXRhIjp7Im5hbWUiOiLguIjguLTguJXguIHguKMg4Lie4Li04LiX4Lix4LiB4Lip4LmM4LmA4Lih4LiY4Liy4LiB4Li44LilIiwiaWQiOjEsImF1dGhvcml0aWVzIjpbIk1BTkFHRV9VU0VSIl19LCJleHAiOjE1ODM1NjYxNDQsImlhdCI6MTU4MzU2NDM0NH0.R-e4tZJE3PmZXKiSqI5plC2rUrLrUZDI_24ssHtbf18KH7mOSxsIOcvLHsJ-bCyGo3ZcE48N5vTtTOOFxpkfNzWmR_a36Lr-TRXcA2Jf5f5gGYNJeztJYx4ch6OTP9RbCQRCJ3tqCFlvGFqcpRh3E6vdwjp-WfLv-0hECW9AjQKp28UolAIyzhyumlDB78MB-Xf8ryibpMKpQZE5a3JsxAfNTK67T9SrXAfRbEjyA-Iu5lalgU0w1a_lQotwkwq5jH-NWzGPvA6-2SssJfHBhbwYkwZEQo2vMzT_rNCBFQRHshYUOqwbl0KOVcZVouTdEWn1GEA0mlYyvZg0YKG-ow
output => {name=จิตกร พิทักษ์เมธากุล, id=1, authorities=[MANAGE_USER]}
```

เมื่อเอา Token ไป Verify สังเกต ค่าจากตัวแปร `output` จะเห็นว่าเหมือนกับค่าในตัวแปร `claims` เป๊ะเลย 

### Code เต็ม ๆ

```java
package me.jittagornp.learning.keypair;

import com.auth0.jwt.JWT;
import com.auth0.jwt.algorithms.Algorithm;
import java.security.KeyPair;
import java.security.KeyPairGenerator;
import java.security.NoSuchAlgorithmException;
import java.security.interfaces.RSAPrivateKey;
import java.security.interfaces.RSAPublicKey;
import java.time.LocalDateTime;
import java.time.ZoneId;
import java.util.Arrays;
import java.util.Date;
import java.util.HashMap;
import java.util.Map;

/**
 * @author jitta
 */
public class JWTExample {

    public static void main(String[] args) throws NoSuchAlgorithmException {

        //Generate Keypair
        final KeyPairGenerator keyPairGenerator = KeyPairGenerator.getInstance("RSA");

        keyPairGenerator.initialize(2048);

        final KeyPair keyPair = keyPairGenerator.genKeyPair();

        final RSAPublicKey publicKey = (RSAPublicKey) keyPair.getPublic();
        final RSAPrivateKey privateKey = (RSAPrivateKey) keyPair.getPrivate();
        //======================================================================

        final Map<String, Object> claims = new HashMap<>();
        claims.put("id", 1L);
        claims.put("name", "จิตกร พิทักษ์เมธากุล");
        claims.put("authorities", Arrays.asList("MANAGE_USER"));

        final String token = sign(claims, Algorithm.RSA256(null, privateKey), 30);
        final Map<String, Object> output = verify(token, Algorithm.RSA256(publicKey, null));

        System.out.println("claims => " + claims);
        System.out.println("token => " + token);
        System.out.println("output => " + output);
    }

    public static String sign(final Map<String, Object> claims, final Algorithm algorithm, final int expiresMinutes) {
        final LocalDateTime now = LocalDateTime.now();
        final LocalDateTime expires = now.plusMinutes(expiresMinutes);
        return JWT.create()
                .withIssuedAt(toDate(now))
                .withExpiresAt(toDate(expires))
                .withClaim("user", claims)
                .sign(algorithm);
    }

    public static Map<String, Object> verify(final String token, final Algorithm algorithm) {
        return JWT.require(algorithm)
                .build()
                .verify(token)
                .getClaims()
                .get("user")
                .asMap();
    }

    private static Date toDate(final LocalDateTime localDateTime) {
        if (localDateTime == null) {
            return null;
        }
        return Date.from(localDateTime.atZone(ZoneId.systemDefault()).toInstant());
    }
}
```

# ปิดท้าย 

บทความนี้ ไม่ใช่มุมมองทางวิชาการเกี่ยวกับการเข้ารหัส/ถอดรหัส แต่เป็นมุมมองที่เกิดจากการที่เคยนำมาเขียนโปรแกรม หรือเคยสัมผัสมาบ้าง หากผิดพลาด หรือตกหล่นตรงไหน ต้องขออภัยและขอคำชี้แนะจากคนที่รู้ลึกด้วยครับ 

# Reference 

- [https://www.wikiwand.com/en/RSA_(cryptosystem)](https://www.wikiwand.com/en/RSA_(cryptosystem))
- [https://www.wikiwand.com/en/Public-key_cryptography](https://www.wikiwand.com/en/Public-key_cryptography)








  

 
