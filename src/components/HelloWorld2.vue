<template>
<div>
  <input type="text" v-model="message">
  <button @click="add">增加</button>
  <ul>
    <li v-for="(item,index) in msgs" v-if='all1'>
      <input type="checkbox" v-model="item.check" @change="clickI">
      <span>{{item.msg}}</span>
      <button @click="del(index)">删除</button>
    </li>

    <li v-for="(item,index) in delARR" v-if='del1'>
      <input type="checkbox" v-model="item.check" @change="clickI">
      <span>{{item.msg}}</span>
      <button @click="del(index)">删除</button>
    </li> 

    <li v-for="(item,index) in actarr" v-if='act1'>
      <input type="checkbox" v-model="item.check" @change="clickI">
      <span>{{item.msg}}</span>
      <button @click="del(index)">删除</button>
    </li>
  </ul>
  <span>{{number}}items left</span>
  <br>
  <button @click="all(true)">全选</button>
  <button @click="all(false)">全不选</button>
  <br>
  <button @click = "per">全部</button>
  <button @click = "act">活动</button>
  <button @click = "fin">完成</button>
</div>

</template>
<script>
export default {
data () {
  return {
    unlock:true,
    message:'',
    choice:false,
    // number:0,
    msgs:[
      {
        msg:"123",
        check:true
      },
      {
        msg:"14",
        check:false
      }
    ],
    act1:false,
    del1:false,
    actarr:[],
    delARR:[],
    all1:true,
    d:[],
    a:[]

  }
},
computed: {
  number(){
    let a = 0
    for (let index = 0; index < this.msgs.length; index++) {
        console.log(this.msgs[index].check)
        if(this.msgs[index].check){
          a +=1
        }

      }
  return a
  }
},
methods: {
  fin(){
    for (let index = 0; index < this.msgs.length; index++) {
      if(this.msgs[index].check){
          this.d.push(this.msgs[index])
      }
    }
        this.all1 = false
        this.del1 = true
        this.delARR = this.d
        this.d = []
        this.act1 = false
  },
  act(){
    for (let index = 0; index < this.msgs.length; index++) {
      if(!this.msgs[index].check){
          this.a.push(this.msgs[index])
      }
    }
        this.all1 = false
        this.del1 = false
        this.actarr = this.a
        this.a = []
        this.act1 = true
    
  },
  per(){
        this.all1 = true
        this.del1 = false
        this.act1 = false
  },
  add(){
    this.msgs.push({msg:this.message,check:false})
    this.message = ''

    
    // this.number++
  },
  del(i){
    this.msgs.splice(i,1)
  },
  all(is){
    for (let index = 0; index < this.msgs.length; index++) {
      this.msgs[index].check=is
    }
    if(is){
      // this.number = 0
    }else{
      // this.number = this.msgs.length
    }
    
  },
  clickI(){
      console.log(this.msgs)
      let a =0
      for (let index = 0; index < this.msgs.length; index++) {
        console.log(this.msgs[index].check)
        if(this.msgs[index].check){
          a +=1
        }

      }
      // this.number = this.msgs.length - a
  }
}
}
</script>
