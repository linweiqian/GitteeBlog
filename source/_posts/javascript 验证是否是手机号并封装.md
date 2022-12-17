---
title: javascript 验证是否是手机号并封装
tags: 
- javascript
categories:
- javascript
---
```bash
//验证是否是手机号
function isPhoneNumber(str){
    var myreg = /^[1][3,4,5,6,7,8,9][0-9]{9}$/;
    if (!myreg.test(str)) {
        return false;
    } else {
        return true;
    }
}
```

