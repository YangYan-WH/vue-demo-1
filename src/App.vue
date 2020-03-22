<template>
  <div>
    <div class="row">
      <Cell v-on:click='onClickCell(0,$event)' v-bind:n="n"/>
      <Cell v-on:click='onClickCell(1,$event)' v-bind:n="n"/>
      <Cell v-on:click='onClickCell(2,$event)' v-bind:n="n"/>
    </div>
    <div class="row">
      <Cell v-on:click='onClickCell(3,$event)' v-bind:n="n"/>
      <Cell v-on:click='onClickCell(4,$event)' v-bind:n="n"/>
      <Cell v-on:click='onClickCell(5,$event)' v-bind:n="n"/>
    </div>
    <div class="row">
      <Cell v-on:click='onClickCell(6,$event)' v-bind:n="n"/>
      <Cell v-on:click='onClickCell(7,$event)' v-bind:n="n"/>
      <Cell v-on:click='onClickCell(8,$event)' v-bind:n="n"/>
    </div>
    <div>
      {{n}} 结果 {{result}}
    </div>
  </div>
</template>

<script>
import Cell from "./Cell";

export default {
  data(){
    return {
      n:0,
      map:[
        [null,null,null],
        [null,null,null],
        [null,null,null]
      ],
      result:false
    }
  },
  components: {
    Cell
  },
  methods:{
    onClickCell(i, text){
      console.log('app')
      console.log(text)
      console.log(i)
      this.map[Math.floor(i / 3)][i%3] = text
      this.n = this.n + 1
      this.tell()
    },
    tell(){
      let map = this.map
      let result = this.result
      console.log(map)
      for(let i = 0;i<2;i++){
        if(map[i][0] && map[i][0] === map[i][1] && map[i][1] === map[i][2]){
          this.result = true
        }
      }

      for(let j = 0;j<2;j++){
        if(map[0][j] && map[0][j] === map[1][j] && map[1][j] === map[2][j]){
          this.result = true
        }
      }

      if(map[0][0] && map[0][0]===map[1][1] && map[1][1] === map[2][2]){
        this.result = true
      }
      if(map[2][0] && map[2][0]=== map[1][1] && map[1][1] === map[0][2]){
        this.result = true
      }

    }
  }
};
</script>

<style>
  .row{
    display: flex;
  }
</style>
