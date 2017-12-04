<template>
  <div class="hello">
    <input @keyup.enter= "add" type="text" v-model.trim= 'messge'>
    <ul>
      <li v-for='(varible,index) in msgs' v-show='peace'>
        <input type="checkbox" v-model='varible.check'>
        <span>{{varible.msg}}</span>
        <button @click='del(index)'>删除</button>
      </li>
      <!-- 全部 -->
      <li v-for='(varible,index) in msgsBackPer' v-show='per'>
        <input type="checkbox" v-model='varible.check'>
        <span>{{varible.msg}}</span>
        <button @click='del(index)'>删除</button>
      </li>
      <!-- 活动 -->
      <li v-for='(varible,index) in msgsBackAct' v-show='act'>
        <input type="checkbox" v-model='varible.check'>
        <span>{{varible.msg}}</span>
        <button @click='del(index)'>删除</button>
      </li>
      <!-- 完成 -->
      <li v-for='(varible,index) in msgsBackCom' v-show='com'>
        <input type="checkbox" v-model='varible.check'>
        <span>{{varible.msg}}</span>
        <button @click='del(index)'>删除</button>
      </li>
    </ul>
    <button @click='change'>{{textAll}}</button>
    <br>
    <button @click="perfect">全部</button>
    <button @click="active">活动</button>
    <button @click="complish">完成</button>
    <div>{{number}} items left</div>
  </div>
</template>
<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      messge: '',
      msgs: [],
      msgsBackPer:[],
      msgsBackAct: [],
      msgsBackCom:[],
      number: 0,
      textAll: '全选',
      peace:true,
      show:false,
      per:false,
      act:false,
      com:false,
      open:false,
      unlock:false
    }
  },
   methods: {
    add: function(){
      this.msgs.push({msg:this.messge,check:false})
      this.number++
    },
    del: function(i){
      this.msgs.splice(i,1)
      this.messge = ''
      this.number--
    },
    change: function(){
      if(this.textAll === "全选"){
        for(let i=0,j=this.msgs.length; i<j; i++){
          if(this.msgs[i].check===false){
            this.msgs[i].check =true
          }
        }
        this.textAll = "全不选"
        this.number = 0
      }else if(this.textAll === "全不选"){
        for(let i=0,j=this.msgs.length; i<j; i++){
          if(this.msgs[i].check===true){
            this.msgs[i].check =false
          }
        }
        this.textAll = "全选"
        this.number = this.msgs.length
      }
    },
    perfect:function(){
       this.msgs=[]
       this.show = true
       this.unlock = false
       this.open = false
       console.log(this.msgs.length)
       for(let i=0,j=this.msgs.length; i<j; i++){
          this.msgsBackPer.push(this.msgs[i])
      }
    },
    active:function(){
      this.msgsBackAct=[]
      this.show = false
      this.unlock = false
      this.open = true
      console.log(this.msgs.length)
      for(let i=0,j=this.msgs.length; i<j; i++){
          if(this.msgs[i].check===false){
            this.msgsBackAct.push(this.msgs[i])
        }
      }
    },
    complish:function(){
        this.msgs=[]
        this.show = false
        this.open = false
        this.unlock = true
        console.log(this.msgs.length)
        for(let i=0,j=this.msgs.length; i<j; i++){
          if(this.msgs[i].check===true){
            this.msgsBackCom.push(this.msgs[i])
          }
        }
    }
  }
}
</script>
<style scoped>
</style>
