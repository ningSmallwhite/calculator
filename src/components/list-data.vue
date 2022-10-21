<template>
  <div>————————————————————————————</div>
  <div>msg:{{ msg }}</div>
  <div>msg2:{{ msg2 }}</div>
  <div>————————————————————————————</div>
  <slot name="aaa" />
  <button @click="fn">按钮</button>
</template>
<script>
export default {
  props: ["msg"],
  emits: ["custom-event"],
  setup(props, context) {
    console.log(props, context);
    const fn = () => {
     context.emit("custom-event", 123);   
    };
    return {
      msg2: context.attrs.msg2,
      fn,
    };
  },
};
</script>

