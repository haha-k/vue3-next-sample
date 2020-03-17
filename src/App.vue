<template>
  <!-- vue3可以一个template里面有两个根元素 -->
  <div>hello {{title}}</div>
  <div>test</div>
  <div>{{state.haha}}</div>
  <div>{{doubleCount}}</div>
  <button @click="increment">Add {{count}}</button>
  <input type="text" />
  <Button text="hhhh" @foobar="onFoobar"></Button>
</template>

<style lang="css" scoped>
div {
  color: pink;
}
</style>

<script>
//可以推断类型
import {
  defineComponent,
  ref,
  reactive,
  computed,
  onMounted,
  onUnmounted
} from "vue";
import Button from "./components/Button.vue";

//vue3不再用this
export default defineComponent({
  components: {
    Button
  },
  //组件初始化的时候执行
  setup() {
    //为一个值创建引用
    //普通值 string number boolean 数据响应 需要用ref
    const count = ref(1);
    //对象需要数据响应 需要用reactive
    const state = reactive({
      haha: "xxxxx"
    });

    onMounted(() => {
      //mounted 生命周期函数
      console.log("mounted");
    });

    const onFoobar = now => {
      console.log("button foobar");
      console.log(now);
    };

    onUnmounted(() => {
      console.log("unmounted");
    });

    const doubleCount = computed(() => count.value * 2);

    //setup 返回值中的成员可以直接在模板中使用
    const increment = () => {
      count.value++;
      state.haha = "haha";
    };
    return {
      title: "Vue3",
      count,
      state,
      increment,
      doubleCount,
      onFoobar
    };
  }
});
</script>