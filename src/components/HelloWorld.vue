<template>
  <div>

  <img class="tianqi_img" src="../assets/logo.png" />

  <span style="font-size:20px;position: relative;top:-100px;font-weight: bold;color:green;">天气预告2018</span>
    <span style="font-size:20px;position: relative;top:-50px;font-weight: bold;color:orangered;"><a href="HelloWorld.vue">未来7天气预告</a></span>
    <el-row>

    <el-input  class="input-width" v-model="input" placeholder="请输入内容"></el-input>
      <el-button v-on:click="onSubmit" type="primary" icon="el-icon-search">搜索</el-button>
    </el-row>
    <template>
    <el-table :data="tableData" style="width: 100%;">
      <el-table-column prop="date" label="日期"></el-table-column>
      <el-table-column prop="high" label="温度"></el-table-column>
      <el-table-column prop="low" label="低温"></el-table-column>
      <el-table-column prop="type" label="天气"></el-table-column>

    </el-table>

    </template>
  </div>
</template>
<!--http://wthrcdn.etouch.cn/weather_mini?city=%E5%B9%BF%E5%B7%9E -->
<script>

//import {getRequest} from '../utils/api'
import axios from 'axios'

export default {

  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      input: '广州',
      tableData:[]
    }
  },
    methods:{
        onSubmit() {
            axios.get("http://wthrcdn.etouch.cn/weather_mini",{params:{city:this.input}})
                .then(response=>{
                this.tableData = response.data.data.forecast
            }).catch(function(err){
                console.log(err);
            });
        }
    }


}


</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  div{
    width:600px;margin:0 auto;
  }
  .input-width{width:500px;}
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
