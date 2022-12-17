---
title: vue axios常用写法
tags: 
- vue
categories:
- vue
---
```bash
axios({
                    url: '传入的api',
                    //对封装好的对象进行序列化,如果后台没说明可以直接传obj对象就行
                    data: {obj:JSON.stringify(obj)},
                    //定义get请求或者post请求
                    method: "post",
                    //设置参数的表头形式，这是表单形式传递
                    headers: {
                        "Content-Type": 'application/x-www-form-urlencoded'
                    },
                    //对data的参数转化为键值对
                    transformRequest: [function (data) {
                        let ret = '';
                        for (let it in data) {
                            ret += encodeURIComponent(it) + '=' + encodeURIComponent(data[it]) + '&';
                        }
                        return ret
                    }]
                }).then(res=>{
                //后台成功请求200运行到这里
                   console.log(res)
                    }
                })
                    .catch(err=>{
				//后台请求失败运行到这里
                    });
```

