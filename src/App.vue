<template>
  <div id="app">
    <h1>{{title.name}}</h1>
    <div>{{user}}</div>
    <button @click="updateUser">修改名称</button>
    <div>当前count：{{computedCount}}</div>
    <button @click="increment">修改count</button>
  </div>
  <HellWorld msg="hello"></HellWorld>
</template>

<script>
import { reactive,ref,onMounted,computed } from 'vue'
import HellWorld from './components/HelloWorld.vue'
export default {
  name: 'App',
  components:{
    HellWorld
  },
  setup(){
    const title = reactive({
      name:'欢迎学习Vue3.0'
    })
    //reactive作用：创建响应式对象，非包装对象，可以认为是模板中的状态。它本身一种Hooks能力，用过React Hook的，实际上就等同于useState();

    const user = ref('rose');
    //ref作用：创建一个包装式对象，含有一个响应式属性value。它和reactive的差别，就是前者没有包装属性value如果需要修改值，可通过value
    
    const updateUser = ()=>{
      user.value = 'jack'
    }
    //事件处理
    
    //新生命周期方法
    onMounted(()=>{
      console.log('init mounted...')
    })

    // 初始化count值
    const count = ref(0);

    const increment = ()=>{
      count.value++
    }

    // 调用计算属性函数Hook
    const computedCount=computed(()=>count.value*2)

    return { title , user, updateUser,count,increment,computedCount }
  }
}
</script>

<style>
#app {
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
