<template>
  <div class="playground">
    <h1>playground</h1>
    <button @click="objectHaveMethod.test">objectHaveMethod.test</button>
    <button @click="objectHaveMethod.test1">objectHaveMethod.test1</button>
    <button @click="funcData">funcData</button>
    <!-- 手动绑定 -->
    <button @click="funcData.apply($root)">funcData(manual bind)</button>
    <button @click="funcMethods">funcMethods</button>
    <button @click="arrowFuncData">arrowFuncData</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      that: this,
      text: 1,
      result: "",
      objectHaveMethod: {
        // 作为对象内的属性
        test() {
          console.log(this.f()); // not work
          console.log(this);
        },
        test1: () => {
          console.log(this.f()); // work
          console.log(this);
        }
      },
      funcData() {
        console.log(this.f()); // 传递给子组装件，f也是本组件方法
        console.log(this); // 不会bind本组件上下文，this指向null（若传递给子组件并在`methods`使用，会bind子组件的上下文）
      },
      arrowFuncData: () => {
        console.log(this.f()); // work
        console.log(this);
      }
    };
  },
  methods: {
    funcMethods() {
      console.log(this.f()); // 传递给子组装件，f也是本组件方法
      console.log(this); // 会bind本组件上下文，this指向本组件（传递给子组件或其他bind都不改变this指向本组件）
    },
    f() {
      return this.text;
    }
  }
};
</script>

<style scoped>
.playground {
  display: flex;
  flex-direction: column;
}
</style>
