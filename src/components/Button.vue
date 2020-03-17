<template>
  <button>{{props.text}}</button>
</template>

<style lang="css" scoped>
div {
  color: pink;
}
</style>

<script>
import { defineComponent } from "vue";
import windowSize from "../utils/window-size.js";

export default defineComponent({
  //仍然可以用2的方法
  props: {
    text: String
  },
  setup(props, { emit }) {
    console.log(props);
    const onClick = () => {
      console.log("clicked");
      //vue3无this
      //   this.$emit('foobar');
      emit("foobar", Date.now());
    };

    const { width: windowWidth, height } = windowSize();

    return {
      props
    };
  }
});
</script>