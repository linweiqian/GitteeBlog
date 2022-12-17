---
title: js解决移动端在iOS和android 监听软键盘弹起、收起
tags: 
- javascript
categories:
- javascript
---

> 1.在ios中软键盘弹起时，仅会引起$(‘body’).scrollTop值改变，但是我们可以通过输入框的获取焦点情况来做判断，但也只能在ios中采用这个方案，因为在android中存在主动收起键盘后，但输入框并没有失焦，而ios中键盘收起后就会失焦；
> 2.在android中软键盘弹起或收起时，会改变window的高度，因此监听window的onresize事件；

<!--more-->
```c

## 一、Android

//获取原窗口的高度
var originalHeight=document.documentElement.clientHeight ||document.body.clientHeight;
window.onresize=function(){
    //键盘弹起与隐藏都会引起窗口的高度发生变化
       var resizeHeight=document.documentElement.clientHeight || document.body.clientHeight;
        if(resizeHeight-0<originalHeight-0){
         //当软键盘弹起，在此处操作
         }else{
         //当软键盘收起，在此处操作
         }
}

## 二、ios

focusin和focusout支持冒泡，对应focus和blur, 使用focusin和focusout的原因是focusin和focusout可以冒泡，focus和blur不会冒泡，这样就可以使用事件代理，处理多个输入框存在的情况。
 document.body.addEventListener('focusin', () => {
            //软键盘弹出的事件处理
            if(isIphone()）{

            }
        })
  document.body.addEventListener('focusout', () => {
       //软键盘收起的事件处理
        if(isIphone()）{

        }
   })
```

