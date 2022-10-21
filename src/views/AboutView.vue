<template>
  <div class="about">
    <h1>This is an about page</h1>
    <p>{{a}}</p>
    <p>{{b}}</p>
    <p>{{c}}</p>
    <p>{{d}}</p>
    <p>{{obj}}</p>
    <button @click="update">按钮</button>
    
  </div>
  <p>e:{{eee}}</p>
  <List @custom-event="cus" msg="你好" msg2="你好,vue3">
    <template #aaa>我是插槽</template>
  </List>
  
</template>
<script>
// import { defineComponent } from '@vue/composition-api'
import { reactive } from '@vue/reactivity'
import { toRefs } from 'vue'
import List from '../components/list-data.vue'

export default ({
  components: {
    List
  },
  setup() {
    const lists = reactive({
      a:100,
      b:110,
      c:120,
      d:false,
      obj:{
        abc:1
      },
      eee:""
    })
    const update=()=>{
      lists.a++;
      lists.b++;
      lists.c++;
      lists.d = !lists.d;
      lists.obj.abc++;
    };
    const cus = (value) => {
      console.log(value)
      lists.eee += value
    }
    return{
      ...toRefs(lists),//对reactive定义的对象进行包装，包装之后的数据都是响应式的。
      update,
      cus
    }
  },
})
</script>

