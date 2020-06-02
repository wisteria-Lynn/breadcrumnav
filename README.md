# breadcrumnav

## 面包屑导航组件

用法：

```
npm install breadcrumnav --save
```

在main.js中导入：

```js
import breadCrumNav from 'breadcrumnav/packages/breadCrumNav/index.js'
import 'breadcrumnav/lib/breadcrumnav.css'
Vue.use(breadCrumNav)
```

路由配置：

```js
const routes = [
  {
    path: '/',
    name: 'home',
    meta: {
      breadID: '1'
    }
  }, {
    path: '/home1',
    name: 'home1',
    meta: {
      breadID: '0'
    }
  },
  {
    path: '/home2',
    name: 'home2',
    meta: {
      breadID: '0-0'
    }
  },
  {
    path: '/home3',
    name: 'home3',
    meta: {
      breadID: '0-0-0'
    }
  }
]
```

菜单配置

```js
let breadNavList = [
        {
          id:"0",
          name:'所有商品',
          url:'/home1',
          menu:[
            {
              id:'0-0',
              name:'女装',
              url:'/home2',
              menu:[
                {
                  id:'0-0-0',
                  name:'连衣裙',
                  url:'/home3',
                }
              ]
            }
          ]
        },
        {
          id:"1",
          name:'主页',
          url:'/'
        }
]
```

可以看到在路由的meta字段中加入了属性breadID，详情解说一下这个属性

breadID表明当前路由在menu菜单中的位置。

```
'0' 当前面包屑有一级，0代表该路由在在菜单栏中的位置breadNavList[0]
'0-0' 代表当前面包屑有两级，breadNavList[0].menu[0]
'0-0-0' 代表当前面包屑有三级，breadNavList[0].menu[0].menu[0]
'0-1-0' 代表当前面包屑有三级，breadNavList[0].menu[1].menu[0]
.....以此类推
```

在组件中使用：

```vue
<template>
  <div id="app">
   <breadNav :breadNavList="breadNavList" @changeRoute="changeBread"/>
  </div>
</template>

<script>

export default {
  name: 'App',
  data(){
    return {
      breadNavList: []
    }
  },
  methods:{
    changeBread(item){
      console.log(item)
      this.$router.push({
        path:item.url
      })
    }
  }
}
</script>
```

changeRoute函数

当点击面包屑时，该函数返回当前路由的url,name,id,及子菜单menu

源码详解可查看文档[实现基于Vue的面包屑导航+链接可跳转组件](https://juejin.im/post/5ed5b5d5f265da76c26e6dd2)

