---
title: vue安卓移动端点击input输入框引起布局混乱
tags: 
- vue
categories:
- vue
---
> 问题描述：Vue开发中，当我们相对于父视图的底部布局子控件时，需要用position:fixed，如果页面内容不是很长，没有超出屏幕范围，那就还好，没有问题；一旦超出屏幕范围，当你点击输入框，弹出键盘时，底部固定定位的子控件就会被顶起来。
> 这个问题在iOS端不会出现，在安卓端会出现，原因是键盘加载方式不一样，这里不作详情解答。

> 
> 解决方案：在键盘弹起时，页面高度变小，底部固定定位上升，所以我们只需要在页面高度变小时，隐藏底部子控件，当键盘消失时再显示底部子控件。

> 解决方法：检测浏览器的resize事件，当高度过小时就可以判定为出现这种情况，这时把定位改成absolute或者直接隐藏掉之类的。

## 第一步： 先在 data 中去 定义 一个记录高度是 属性

<!--more-->
```javascript
data () {
    return {

        docmHeight: '0',  //默认屏幕高度

        showHeight:  '0',  //实时屏幕高度

        hidshow:true  //显示或者隐藏footer,

       isResize:false //默认屏幕高度是否已获取

    };
  },
```

## 第二步： 我们需要将 reisze 事件在 vue mounted 的时候 去挂载一下它的方法


```javascript
mounted() {

    // window.onresize监听页面高度的变化

    window.onresize = ()=>{

        return(()=>{

                     if (!this.isResize) {

                               //默认屏幕高度

                               this.docmHeight: document.documentElement.clientHeight 

                               this.isResize = true

                       }

                        //实时屏幕高度

                       this.showHeight = document.body.clientHeight 

        })()

    }

  },
```

## 第三步：watch监控比较，判断按钮是否该显示出来

```javascript
showHeight:function() {

        if(this.docmHeight > this.showHeight){

            this.hidshow=false

        }else{

            this.hidshow=true

        }

    }
```

## 第四步：在模板中给footer添加v-show

```handlebars
<div class="footer" v-show="hidshow">

移动端点击输入框，弹出键盘，底部被顶起问题

</div>

```

