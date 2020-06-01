# breadcrumnav

## 面包屑导航组件

用法：

```
npm install breadcrumnav --save
```

在main.js中导入：

```js
import breadCrumNav from 'breadcrumnav/lib/breadcrumnav.common.js'
import 'breadcrumnav/lib/breadcrumnav.css'
Vue.use(breadCrumNav)
```

路由配置：

```js
const routes = [{
  path: '/home1',
  name: 'home1',
  meta: {
    breadID: '0'
  },
  component(resolve) {
    require.ensure(['./pages/home/home1.vue'], () => {
      resolve(require('./pages/home/home1.vue'));
    });
  }
},{
        path: '/home2',
        name: 'home2',
        meta: {
          breadID: '0-0'
        },
        component(resolve) {
          require.ensure(['./pages/home/home2.vue'], () => {
            resolve(require('./pages/home/home2.vue'));
          });
        }
},{
            path: '/home3',
            name: 'home3',
            meta: {
              breadID: '0-0-0'
            },
            component(resolve) {
              require.ensure(['./pages/home/home3.vue'], () => {
                resolve(require('./pages/home/home3.vue'));
              });
           }
 }]


```

在组件中使用：

```vue
<bread :breadNavList="breadNavList" @changeRoute="changeBread"/>
<script>

  export default {
    data(){
          return {
            breadNavList: [
              {
                id:"0",
                name:'1-第一级',
                url:'/home1',
                menu:[
                  {
                    id:'0-0',
                    name:'1-第二级',
                    url:'/home1/home2',
                    menu:[
                      {
                        id:'0-0-0',
                        name:'1-第三级',
                        url:'/home1/home2/home3',
                      }
                    ]
                  }
                ]
              }
            ]
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

注意：`changeBread(item)`item为当前点击的项。

菜单配置：

```js
let breadNavList = [{
    id:"0",
    name:'1-第一级',
    url:'/home1',
    menu:[{
       id:'0-0',
       name:'1-第二级',
       url:'/home2',
        menu:[{
             id:'0-0-0',
             name:'1-第三级',
             url:'/home3',
         }]
    }]
}]
```

```
  breadID:'0' // 代表第一级第一个
  breadID:'0-0' // 代表第一级第一个 - 第二级第一个
  breadID:'0-1' // 代表第一级第一个 - 第二级第二个
```

