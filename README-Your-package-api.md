# Your Package Api

**Api** `member/subscriptions/package ` **Method:** GET
**Authorization:** Basic
**Header:** x-token
> **Password:** `123456789`

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