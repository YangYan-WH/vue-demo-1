<template>
  <div class="cell" v-on:click="onClickSelf">
    <template v-if="a">{{text}}</template>
    <template v-else></template>
  </div>
</template>

<script>
export default {
  props: {
    n: 0,
    ifContinue:Boolean
  },
  data() {
    return {
      a: false,
      b: "X",
      c: "〇",
      text: "",
    };
  },
  methods: {
    onClickSelf() {
      if (this.text || this.ifContinue === false) {
        return;
      }
      this.a = true;
      this.text = this.n % 2 === 0 ? this.b : this.c;
      this.$emit("click", this.text);
    }
  }
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
.cell {
  width: 100px;
  height: 100px;
  line-height: 100px;
  font-size: 50px;
  border: 1px solid #a2a9b6;
  text-align: center;
}
</style>
   