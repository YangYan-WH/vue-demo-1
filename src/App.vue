<template>
  <div class="wrapper">
    <h4>3 个相连即获胜</h4>
    <div class="board">
      <div class="row">
        <Cell v-on:click="onClickCell(0,$event)" v-bind:n="n" :ifContinue='ifContinue'/>
        <Cell v-on:click="onClickCell(1,$event)" v-bind:n="n" :ifContinue='ifContinue'/>
        <Cell v-on:click="onClickCell(2,$event)" v-bind:n="n" :ifContinue='ifContinue'/>
      </div>
      <div class="row">
        <Cell v-on:click="onClickCell(3,$event)" v-bind:n="n" :ifContinue='ifContinue'/>
        <Cell v-on:click="onClickCell(4,$event)" v-bind:n="n" :ifContinue='ifContinue'/>
        <Cell v-on:click="onClickCell(5,$event)" v-bind:n="n" :ifContinue='ifContinue'/>
      </div>
      <div class="row">
        <Cell v-on:click="onClickCell(6,$event)" v-bind:n="n" :ifContinue='ifContinue'/>
        <Cell v-on:click="onClickCell(7,$event)" v-bind:n="n" :ifContinue='ifContinue'/>
        <Cell v-on:click="onClickCell(8,$event)" v-bind:n="n" :ifContinue='ifContinue'/>
      </div>
      
    </div>
    <div class="result" v-bind:class="{success: !!result}">{{result?`${result} 获得胜利`:'胜负未分'}}</div>
  </div>
</template>

<script>
import Cell from "./Cell";

export default {
  data() {
    return {
      n: 0,
      map: [
        [null, null, null],
        [null, null, null],
        [null, null, null]
      ],
      result: null,
      ifContinue:true
    };
  },
  components: {
    Cell
  },
  methods: {
    onClickCell(i, text) {
      console.log("app");
      console.log(text);
      console.log(i);

      this.map[Math.floor(i / 3)][i % 3] = text;
      this.n = this.n + 1;
      if(this.ifContinue){
        this.tell(text);
      }
    },
    tell(text) {
      let map = this.map;
      let result = this.result;
      for (let i = 0; i < 2; i++) {
        if (map[i][0] && map[i][0] === map[i][1] && map[i][1] === map[i][2]) {
          this.result = text;
          this.ifContinue = false
        }
      }

      for (let j = 0; j < 2; j++) {
        if (map[0][j] && map[0][j] === map[1][j] && map[1][j] === map[2][j]) {
          this.result = text;
          this.ifContinue = false
        }
      }

      if (map[0][0] && map[0][0] === map[1][1] && map[1][1] === map[2][2]) {
        this.result = text;
        this.ifContinue = false
      }
      if (map[2][0] && map[2][0] === map[1][1] && map[1][1] === map[0][2]) {
        this.result = text;
        this.ifContinue = false
      }
    }
  }
};
</script>

<style>
body {
  height: 100vh;
  background-color: #0a70efba;
}
.wrapper {
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  text-align: center;
}
h4{
  color: #f7f9fa;
}
.row {
  display: flex;
  justify-content: center;
  align-items: center;
}
.row > div {
  background-color: #fff;
}
.result {
  font-size: 32px;
  color: #f7f9fa;
}
.success {
  color: #eb4646;
}
</style>
