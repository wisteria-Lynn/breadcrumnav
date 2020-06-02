<template>
  <div class="bread-wrap">
    <div class="bread-item" v-for="(item,index) in bread" :key="index">
      <span @click="toBreadRouter(item)">{{item.name}}</span><i v-if="index !== bread.length - 1"> > </i></div>
  </div>
</template>

<script>
  export default {
    name: "breadNav",
    props:{
      // 默认菜单
      breadNavList: {
        type:Array,
        default:function(){
          return [
            {
              id:"0",
              name:'1-第一级',
              url:'1-第一级url',
              menu:[
                {
                  id:'0-0',
                  name:'1-第二级',
                  url:'1-第二级url',
                  menu:[
                    {
                      id:'0-0-0',
                      name:'1-第三级',
                      url:'1-第三级url',
                    }
                  ]
                }
              ]
            },
            {
              id:"1",
              name:'2-第一级',
              url:'2-第一级url',
              menu:[
                {
                  id:'1-0',
                  name:'2-第二级',
                  url:'2-第二级url',
                  menu:[
                    {
                      id:'1-0-0',
                      name:'2-第三级',
                      url:'2-第三级url',
                    }
                  ]
                }
              ]
            }
          ]
        }
      }
    },
    data() {
      return {
        bread:[]//面包屑
      }
    },
    watch:{
      '$route':{
        handler(){
          this.bread = []
          if(this.$route && this.$route.meta && this.$route.meta.breadID){
            let arr = this.$route.meta.breadID.split('-')
            this.getBread(arr,this.breadNavList)
          } else {
            console.error('字段`this.$route.meta.breadID`没有设置')
          }
        },
        immediate:true
      }
    },
    methods: {
      getBread(arr,menu){
        if(arr.length > 0){
          this.bread.push(menu[arr[0]])
          menu = menu[arr[0]].menu
          arr.shift()
          if(arr.length > 0){
            return this.getBread(arr,menu)
          }
        }
      },
      toBreadRouter(item){
        this.$emit('changeRoute',item)
      }
    }
  }
</script>

<style scoped>
  .bread-wrap{
    color:#606266;
    font-size:14px;
  }
  .bread-wrap .bread-item{
    display: inline-block;
  }
  .bread-wrap .bread-item span:hover{
    cursor: pointer;
    color:#409EFF;
  }
  .bread-wrap .bread-item:last-child{
    cursor: auto;
    color:#303133;
  }
  .bread-wrap .bread-item:last-child span{
    cursor: auto;
  }
  .bread-wrap .bread-item i{
    font-style: normal;
  }
</style>