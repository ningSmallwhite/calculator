<template>
  <div class="home">
    <div>▲</div>
    <div>|</div>
    <div>|</div>
    <div>|</div>
    <div>|</div>
    <div>|</div>  
    <h2>计算器入口点击上面的“Calculate”</h2>
    <p>a:{{ p.a }}</p>
    <p>b:{{ p.b }}</p>
    <p>c:{{p.c}}</p>
    <p>d:{{d}}</p>
    <p>e:{{p.e}}</p>
    <p v-show="p.f">f:{{p.f}}</p>
    <button @click="add">点击</button>
    <button @click="test">添加</button>
    <button @click="delete1">删除</button>
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'  
import { reactive,ref } from '@vue/reactivity';
export default {
  name: 'HomeView',
  // components: {
  //   HelloWorld
  // },
  setup(){
    // let a = ref(1), b=ref(2),c=ref("abc"),
    let d= ref(true);
    const p = reactive({
        a:1,
        b:2,
        c:"abc",
        // d:true
        e:false,
        f:""
      })
    const add = () => {
      p.a++;
      p.b++;
      p.c += "--";
      d.value = !d.value;
      p.e = !p.e
    };
    const test = () =>{
      p.f += "添加的"
    }
    const delete1 = () =>{
      p.f = ""
    }
    return{
      add,p,d,test,delete1
    }
  }
}
</script>
