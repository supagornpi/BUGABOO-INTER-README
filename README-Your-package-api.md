# Your Package Api

**Api** `member/subscriptions/package `     
**Method:** GET     
**Authorization:** Basic    
**Header:** x-token 

## Guide     

``` 
Title = `Current Package` | `แพ็กเกจปัจจุบัน`       
If `gateway` == `promocode`     
    Title = `Current Package (Redeem Code)` | `แพ็กเกจปัจจุบัน (ใช้รหัสโปรโมท)`     
    
Subscription name     
> การแสดงราคา gateway: `Apple, Google, Huawei` ไม่ต้องแสดงราคา ส่วน gateway อื่นๆให้แสดงราคาปกติ (ราคาแยกตามภาษา)   

If `has_subscription` == `true`     
    If `gateway` == `promocode`     
        subscription name = `subscription.name`     
    else        
        If `gateway` == `Apple` or `Google` or `Huawei`     
            subscription name = `subscription.name` + `/` + `subscription.regular_duration`     
        else        
            subscription name = `subscription.name` + `subscription.price or subscription.price_thb` + `/` + `subscription.regular_duration`        
else        
    subscription name = `-`     
    
example   
`1 Month [Test] / 1 Month` | `1 Month [Test] / 1 เดือน`     
`1 Month [Test] 5.99 USD / 1 Month` | `1 Month [Test] 199 THB / 1 เดือน`        


Billing date Title = `Expire date` | `วันหมดอายุ`
If `enabled_recurring` == `true`
   Billing date Title = `Next billing date` | `รอบบิลถัดไป`
   
Billing date
If `eligible` == `true` && `expiry_date` != `null`
   Billing date = `expiry_date` format `07 February 2022 | 07 กุมภาพันธ์ 2565`
   

   
Button (Old)
If (`eligible` == `true` || `enabled_recurring` == `true`) && !(`gateway` == `promocode`)
    Button = `Cancel membership`  | `ยกเลิกการเป็นสมาชิก`
else
    Button = Mobile -> `RENEW SUBSCRIPTION` | `ต่ออายุสมาชิก` , **Website** -> `Buy package / Renew subscription` | `สมัครแพ็กเกจ / ต่ออายุสมาชิก`

disable button (กดไม่ได้) = (`enabled_recurring` == `false` && `eligible`)

   
Button (new (Updated at 17/05/65))
If (`eligible` == `true` || `enabled_recurring` == `true`) && !(`gateway` == `promocode`)
    Button = `Cancel membership`  | `ยกเลิกการเป็นสมาชิก`
    
    if (status == 9)
        if (`gateway` == `Google`)
            Action = show alert update your payment (Text below)
            Positive button action = open 'https://play.google.com/store/account/subscriptions'
            Negative button action = open plan
        else if (`gateway` == `Apple`)
            Action = show alert update your payment (Text below)
            Positive button action = open 'https://apps.apple.com/account/subscriptions'
            Negative button action = open plan
    else
        'ทำตามเงื่อนไขเดิม'
            
    
else
    Button = Mobile -> `RENEW SUBSCRIPTION` | `ต่ออายุสมาชิก` , **Website** -> `Buy package / Renew subscription` | `สมัครแพ็กเกจ / ต่ออายุสมาชิก`

disable button (กดไม่ได้) = (`enabled_recurring` == `false` && `eligible`)


Alert Update your payment
Title EN: 'Update your payment information to continue watching'
Title TH: 'อัปเดตข้อมูลการชำระเงินเพื่อรับชมต่อ'
Positive Button EN: 'Update a payment method'
Positive Button TH: 'อัปเดตการชำระเงิน'
Negative Button EN: 'Change package'
Negative Button TH: 'เปลี่ยนแพ็กเกจ'


```

> **Password:** `123456789`


**Case 1 มี Promotion code** `supagorn.pi+2201@gmail.com `

**Case 2 มี Member subscription** `supagorn.pi+2202@gmail.com `

**Case 3 Promotion code หมดอายุ แต่มี Member subscription** `supagorn.pi+2203@gmail.com `

**Case 4  Member subscription ถูกยกเลิก** `supagorn.pi+2204@gmail.com `

**Case 5 member subscription หมดอายุแล้ว และมี Promotion code** `supagorn.pi+2205@gmail.com `

**Case 6 member subscription หมดอายุ และ Promotion code หมดอายุ  `(ไม่มี member subscription)`** `supagorn.pi+2206@gmail.com `

## Header
|  | EN | Current Package | Current Package (Redeem Code) | Expire date | Next billing date | RENEW SUBSCRIPTION | Cancel membership |
| ----------- | ----------- | ----------- | ----------- | ----------- | ----------- | ----------- | ----------- |
| Email | TH | แพ็กเกจปัจจุบัน | แพ็กเกจปัจจุบัน (ใช้รหัสโปรโมท)   | วันหมดอายุ | รอบบิลถัดไป | ต่ออายุสมาชิก | ยกเลิกการเป็นสมาชิก |
| `case1: supagorn.pi+2201@gmail.com ` | | |  ✅  | ✅ |  | ✅  |  | 
| `case2: supagorn.pi+2202@gmail.com ` | | ✅ | | | ✅ |  | ✅ |
| `case3: supagorn.pi+2203@gmail.com ` | | ✅ | | | ✅ |  | ✅ |
| `case4: supagorn.pi+2204@gmail.com ` | | ✅ | | ✅ |  |  | ✅ |
| `case5: supagorn.pi+2205@gmail.com ` | | |  ✅  | ✅ |  | ✅  |  | 
| `case6: supagorn.pi+2206@gmail.com ` | | ✅ |    | ✅ |  | ✅  |  | 



### Case 1 มี Promotion code
> **Email:** `supagorn.pi+2201@gmail.com `
response
```json
{
    "expiry_date": "2022-02-07T08:14:34Z",
    "enabled_recurring": false,
    "status": 0,
    "gateway": "promocode",
    "purchase_number": "TESTCODE",
    "has_subscription": true,
    "eligible": true,
    "subscription": {
        "id": 14,
        "name": "1 Month [Test]",
        "price": 5.99,
        "price_thb": 199.0,
        "currency": "USD",
        "regular_duration": "P1M",
        "trial_duration": "P14D"
    }
}
```

##### Display
####
| EN | TH |
| ----------- | ----------- |
| ``` Current Package (Redeem Code) ``` | ``` แพ็กเกจปัจจุบัน (ใช้รหัสโปรโมท) ``` |
| 1 Month [Test] | 1 Month [Test] |
| ``` Expire date  ``` | ``` วันหมดอายุ ``` |
| 07 February 2022 | 07 กุมภาพันธ์ 2565 |
| **Button Website `(Disable)`:** Buy package / Renew subscription   | **Button Website `(Disable)`:** สมัครแพ็กเกจ / ต่ออายุสมาชิก |
| **Button Mobile `(Disable)`:** RENEW SUBSCRIPTION   | **Button Mobile `(Disable)`:** ต่ออายุสมาชิก |

> **การเช็ค:** `Disable` เช็คจาก `enabled_recurring: false` && `has_subscription: true` [^Disable]
> **Current Package (Redeem Code)** เช็คจาก `gateway: promocode`

### Case 2 มี Member subscription
> **Email:**  `supagorn.pi+2202@gmail.com `
response
```json
{
    "expiry_date": "2022-02-01T07:13:39Z",
    "enabled_recurring": true,
    "status": 1,
    "gateway": "Omise",
    "purchase_number": "RPJX16JC-1",
    "has_subscription": true,
    "eligible": true,
    "subscription": {
        "id": 14,
        "name": "1 Month [Test]",
        "price": 5.99,
        "price_thb": 199,
        "currency": "USD",
        "regular_duration": "P1M",
        "trial_duration": "P14D"
    }
}
```

##### Display
####
| EN | TH |
| ----------- | ----------- |
| ``` Current Package ``` | ``` แพ็กเกจปัจจุบัน ``` |
| 1 Month [Test] 5.99 USD / 1 Month [^Price] | 1 Month [Test] 199 THB / 1 เดือน [^Price] |
| ``` Next billing date  ``` | ``` รอบบิลถัดไป ``` |
| 01 February 2022 | 01 กุมภาพันธ์ 256565 |
| **Button:** Cancel membership  | **Button:** ยกเลิกการเป็นสมาชิก |

> **การแสดงราคา** **gateway:** `Apple, Google, Huawei` ไม่ต้องแสดงราคา ส่วน gateway อื่นๆให้แสดงราคาปกติ

> 📝 **Note:** สำหรับ Website จะมี Badge ด้านล่างนี้ต่อท้ายชื่อ Package
**Example**

> **TH:** 1 Month [Test] 199 THB / 1 เดือน ``` หมดอายุในอีก 22 วัน```

> **EN:** 1 Month [Test] 199 THB / 1 Month ``` Remaining 22 days ```

### Case 3 Promotion code หมดอายุ แต่มี Member subscription
> **Email:**  `supagorn.pi+2203@gmail.com `

response
```json
{
    "expiry_date": "2022-02-01T07:13:39Z",
    "enabled_recurring": true,
    "status": 1,
    "gateway": "Omise",
    "purchase_number": "RPJX16JC-2",
    "has_subscription": true,
    "eligible": true,
    "subscription": {
        "id": 14,
        "name": "1 Month [Test]",
        "price": 5.99,
        "price_thb": 199.0,
        "currency": "USD",
        "regular_duration": "P1M",
        "trial_duration": "P14D"
    }
}
```

##### Display
####
| EN | TH |
| ----------- | ----------- |
| ``` Current Package ``` | ``` แพ็กเกจปัจจุบัน ``` |
| 1 Month [Test] 5.99 USD / 1 Month [^Price] | 1 Month [Test] 199 THB / 1 เดือน [^Price] |
| ``` Next billing date  ``` | ``` รอบบิลถัดไป ``` |
| 01 February 2022 | 01 กุมภาพันธ์ 2565 |
| **Button:** Cancel membership  | **Button:** ยกเลิกการเป็นสมาชิก |

> **การแสดงราคา** **gateway:** `Apple, Google, Huawei` ไม่ต้องแสดงราคา ส่วน gateway อื่นๆให้แสดงราคาปกติ

> 📝 **Note:** สำหรับ Website จะมี Badge ด้านล่างนี้ต่อท้ายชื่อ Package
**Example**

> **TH:** 1 Month [Test] 199 THB / 1 เดือน ``` หมดอายุในอีก 22 วัน```

> **EN:** 1 Month [Test] 199 THB / 1 Month ``` Remaining 22 days ```

### Case 4  Member subscription ถูกยกเลิก
> **Email:**  `supagorn.pi+2204@gmail.com `

response
```json
{
    "expiry_date": "2022-02-01T07:13:39Z",
    "enabled_recurring": false,
    "status": 2,
    "gateway": "Omise",
    "purchase_number": "RPJX16JC-3",
    "has_subscription": true,
    "eligible": true,
    "subscription": {
        "id": 14,
        "name": "1 Month [Test]",
        "price": 5.99,
        "price_thb": 199,
        "currency": "USD",
        "regular_duration": "P1M",
        "trial_duration": "P14D"
    }
}
```

##### Display
####
| EN | TH |
| ----------- | ----------- |
| ``` Current Package ``` | ``` แพ็กเกจปัจจุบัน ``` |
| 1 Month [Test] 5.99 USD / 1 Month [^Price] | 1 Month [Test] 199 THB / 1 เดือน [^Price] |
| ``` Expire date  ``` | ``` วันหมดอายุ ``` |
| 01 February 2022 | 01 กุมภาพันธ์ 2565 |
| **Button Website:** `ไม่แสดงปุ่ม (ตามของเดิม)`  | **Button Website:** `ไม่แสดงปุ่ม (ตามของเดิม)` |
| **Button Mobile `(Disable)`:** Cancel membership  | **Button Mobile `(Disable)`:** ยกเลิกการเป็นสมาชิก |

> **การแสดงราคา** **gateway:** `Apple, Google, Huawei` ไม่ต้องแสดงราคา ส่วน gateway อื่นๆให้แสดงราคาปกติ

> **การเช็ค:** `Disable` เช็คจาก `enabled_recurring: false` && `has_subscription: true` [^Disable]

> 📝 **Note:** สำหรับ Website จะมี Badge ด้านล่างนี้ต่อท้ายชื่อ Package
**Example**

> **TH:** 1 Month [Test] 199 THB / 1 เดือน ``` หมดอายุในอีก 22 วัน```

> **EN:** 1 Month [Test] 199 THB / 1 Month ``` Remaining 22 days ```

### Case 5 member subscription หมดอายุแล้ว และมี Promotion code
> **Email:**  `supagorn.pi+2205@gmail.com `

response
```json
{
    "expiry_date": "2022-02-07T12:24:51Z",
    "enabled_recurring": false,
    "status": 0,
    "gateway": "promocode",
    "purchase_number": "TESTCODE",
    "has_subscription": true,
    "eligible": true,
    "subscription": {
        "id": 14,
        "name": "1 Month [Test]",
        "price": 5.99,
        "price_thb": 199.0,
        "currency": "USD",
        "regular_duration": "P1M",
        "trial_duration": "P14D"
    }
}
```

##### Display
####
| EN | TH |
| ----------- | ----------- |
| ``` Current Package (Redeem Code) ``` | ``` แพ็กเกจปัจจุบัน (ใช้รหัสโปรโมท) ``` |
| 1 Month [Test] | 1 Month [Test] |
| ``` Expire date  ``` | ``` วันหมดอายุ ``` |
| 07 February 2022 | 07 กุมภาพันธ์ 2565 |
| **Button Website `(Disable)`:** Buy package / Renew subscription   | **Button Website `(Disable)`:** สมัครแพ็กเกจ / ต่ออายุสมาชิก |
| **Button Mobile `(Disable)`:** RENEW SUBSCRIPTION   | **Button Mobile `(Disable)`:** ต่ออายุสมาชิก |
> **การเช็ค:** `Disable` เช็คจาก `enabled_recurring: false` && `has_subscription: true` [^Disable]
> **Current Package (Redeem Code)** เช็คจาก `gateway: promocode`

### Case 6 member subscription หมดอายุ และ Promotion code หมดอายุ  `(ไม่มี member subscription)`
> **Email:**  `supagorn.pi+2206@gmail.com `

response
```json
{
    "has_subscription": false,
    "eligible": false
}
```
##### Display
####
| EN | TH |
| ----------- | ----------- |
| ``` Current Package ``` | ``` แพ็กเกจปัจจุบัน ``` |
| - | - |
| ``` Expire date  ``` | ``` วันหมดอายุ ``` |
| - | - |
| **Button Website:** Buy package / Renew subscription   | **Button Website:** สมัครแพ็กเกจ / ต่ออายุสมาชิก |
| **Button Mobile:** RENEW SUBSCRIPTION   | **Button Mobile:** ต่ออายุสมาชิก |


## รายละเอียดเพิ่มเติม


[^Price]: การแสดงราคา **gateway:** `Apple, Google, Huawei` ไม่ต้องแสดงราคา ส่วน gateway อื่นๆให้แสดงราคาปกติ
[^Disable]: **การเช็ค:** `Disable` เช็คจาก `enabled_recurring: false` && `has_subscription: true`
