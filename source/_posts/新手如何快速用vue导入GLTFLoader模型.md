---
title: 新手如何快速用vue导入GLTFLoader模型
tags: 
- threejs
- vue
categories:
- vue
- threejs
---

>Three.js支持包括 .obj、.gltf等类型的模型结构。glTF（GL传输格式）是Khronos的一个开放项目，它为3D资产提供了一种通用的、可扩展的格式，这种格式既高效又与现代web技术高度互操作。

## 一、安装引入Three.js

```
cnpm install three --save // 很好装的最新版本，可正常引入使用
```

###  在需要使用3D模型的页面导入包：

<!--more-->
```
import * as Three from "three"
```
### 在Vue中导入glTF模型需要使用 Three.js 中的 GLTFLoader：

```
import { GLTFLoader } from "three/examples/jsm/loaders/GLTFLoader"
// GLTF加载器(GLTFLoader)，用于载入glTF 2.0资源的加载器。
import { OrbitControls } from "three/examples/jsm/controls/OrbitControls"
// OrbitControls是THREEJS中最常用的一个控制器,可以帮助我们实现以目标为焦点的旋转缩放。
```

## 二、页面DOM元素渲染

### 在Vue中，我们需要使用一个 div 元素来作为3D模型的容器：

```
<div id="container"></div>
```
原理：页面打开之后，Three.js会给 div 元素添加一个 canvas 子元素用来作为3D模型的画布。

## 三、初始化

Three.js中最重要的三大组件:

> 场景——Scene
>
> 相机——Camera
>
> 渲染器——Renderer

### 代码：

```
mounted(){

  this.initScene()

  this.initContainer()

  this.initCamera()

  this.initRenderer()

  this.initControls()

},

methods:{

   initModelContainer() {

   this.model_container = document.getElementById("container");

   this.model_container.style.height = window.innerHeight + "px";

   this.model_container.style.width = window.innerWidth + "px";

   this.height = this.model_container.clientHeight;

   this.width = this.model_container.clientWidth;

  },

  initScene() {

   this.scene = new Three.Scene();

  },

  initCamera() {

    // 照相机

   this.camera = new Three.PerspectiveCamera(70, this.width / this.height, 0.01, 1000);

   this.camera.position.set(-100, 60, 0);

  },

  initRenderer() {

   this.renderer = new Three.WebGLRenderer({ antialias: true, alpha: true });

   this.renderer.setSize(this.width, this.height);

   // 兼容高清屏幕

   this.renderer.setPixelRatio(window.devicePixelRatio);

    // 消除canvas的外边框

   this.renderer.domElement.style.outline = "none";

   this.model_container.appendChild(this.renderer.domElement);

  },

  initControls() {

   this.orbitControls = new OrbitControls(

    this.camera,

    this.renderer.domElement

   );

   // 惯性

   this.orbitControls.enableDamping = true;

   // 动态阻尼系数

   this.orbitControls.dampingFactor = 0.25;

   // 缩放

   this.orbitControls.enableZoom = true;

   // 右键拖拽

   this.orbitControls.enablePan = true;

   // 水平旋转范围

   this.orbitControls.maxAzimuthAngle = Math.PI / 6;

   this.orbitControls.minAzimuthAngle = -Math.PI / 6;

   // 垂直旋转范围

   this.orbitControls.maxPolarAngle = Math.PI / 6;

   this.orbitControls.minPolarAngle = -Math.PI / 6;

  },

}
```

## 四、导入glTF模型

> 将你的 gltf 模型放在 Vue 项目中的 public 文件夹下，注意，只有将 gltf 模型放在静态资源文件夹下才能被访问到。


在钩子函数 mounted 中进行模型加载：

```
mounted(){

  this.loadModel()

},

methods:{

  loadModel(){

    let that = this

    // gltf模型加载器

    let loader = new GLTFLoader()

    return new Promise(function(resolve, reject){

      loader.load(

        // 模型在 /public/static/building/文件夹下

        "static/building/scene.gltf",

        gltf => {

          console.log(gltf)

          gltf.scene.traverse(object => {

            // 修改模型材质

            let material = ...

            object.material = material

          })

          let group = new Three.Group()

          group.add(gltf.scene)

          let box = new Three.Box3()

          box.setFromObject(group)

          let wrapper = new Three.Object3D()

          wrapper.add(group)

          // 根据自己模型的大小设置位置

          wrapper.position.set(100, -300, 120)

          // 将模型加入到场景中 ! important

          that.scene.add(wrapper)

        },

        xhr => {

          // 模型加载期间的回调函数

          console.log(`${(xhr.loaded / xhr.total) * 100% building model loaded`

      );

        },

        error => {

          // 模型加载出错的回调函数

          console.log("error while loading", error);

          reject("load model error", error);

        }

      )

    })

  }

}
```
启动项目，模型导入成功，可以根据自己的需求为模型渲染材质。

## 五、免费下载3D模型的素材网站

[网址一](https://glbxz.com/err/search.php?a=search&keyword=%E5%85%8D%E8%B4%B9&searchtype=titlekeyword&channeltype=0&orderby=&kwtype=0&pagesize=10&typeid=0&TotalResult=63&PageNo=3)

[网址二](https://sketchfab.com/3d-models?date=week&features=downloadable&sort_by=-likeCount)
