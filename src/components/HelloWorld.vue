<template>
  <div>
    <input type="text" v-model="message">
    <button @click="add">添加</button>
    <ul>
      <li :key="index" v-for="(item, index) in datalist">
        <input type="checkbox" v-model="item.check">
        <span>{{item.msg}}</span>
        <button @click="del(item.id)">删除</button>
      </li>
    </ul>
    <button @click="all">all</button>
    <button @click="active">active</button>
    <button @click="finish">finish</button>
  </div>
</template>
<script>
export default { 
  data() {
    return {
      message: "",
      i:0,
      data: [],
      datalist: [],
      status: "all"
    };
  },
  methods: {
    finish() {
      this.status = "finish";
       this.datalist = this.data.filter(function f(item) {
         if(item.check){
           return item
         }
      });
      // this.datalist = this.data.filter(item => {
      //   return item.check;
      // });
    },
    all() {
      this.status = "all";
      this.datalist = this.data;
    },
    active() {
      this.status = "active";
      this.datalist = this.data.filter(item => {
        return !item.check;
      });
    },
    del(j) {
      //this.data.splice(index, 1);
      for (let index = 0; index < this.data.length; index++) {
      if(this.data[index].id == j )
        this.data.splice(index, 1)
        
      }
      this.filet();
    },
    filet() {
      if (this.status == "all") this.all();
      if (this.status == "active") this.active();
      if (this.status == "finish") this.finish();
    
  },
  add() {
    this.data.push({
      msg: this.message,
      check: false,
      id:this.i++
    });
    this.message = ""
    this.filet()
  }
  }
}
</script>

