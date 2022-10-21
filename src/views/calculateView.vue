<template>
  <div>
  <div>姓名：<input type="text" v-model="user.name" /></div>
  <div>年龄：<input type="text" v-model="user.age" /></div>
  <p>计算：{{ user.fullUser }}</p>
  <p>计算：<input type="text" v-model="user.fullUser"></p>
  </div>
</template>
<script>
import { reactive  } from "@vue/reactivity";
import { computed } from "@vue/runtime-core";
export default {
  name: "calculateView",
  setup() {
    const user = reactive({
      name: "张三",
      age: 18,
    });
    //计算属性第一种写法
    // const fullUser = computed(() => {
    //   return user.name + "" + user.age;
    // });

    //计算属性第二种写法：只读
    // user.fullUser = computed(() => {
    //   return user.name + "" + user.age;
    // });
    //第三种写法：可读可写
    user.fullUser = computed({
      get(){
        return user.name + "-" + user.age;
      },
      set(value){
        const nameArr = value.split('-')
        user.name = nameArr[0]
        user.age = nameArr[1]
      }
    })
    return {
        //...toRef(user)
        // name: toRef(user, 'name'),
        // age: toRef(user, 'age'),
        //, #
        user, 
    };
  },
};
</script>