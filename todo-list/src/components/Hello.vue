<template>
  <div class="hello">
    <!-- <h1>{{ msg }}</h1>
    <h2>Essential Links</h2>
    <ul>
      <li><a href="https://vuejs.org" target="_blank">Core Docs</a></li>
      <li><a href="https://forum.vuejs.org" target="_blank">Forum</a></li>
      <li><a href="https://gitter.im/vuejs/vue" target="_blank">Gitter Chat</a></li>
      <li><a href="https://twitter.com/vuejs" target="_blank">Twitter</a></li>
      <br>
      <li><a href="http://vuejs-templates.github.io/webpack/" target="_blank">Docs for This Template</a></li>
    </ul>
    <h2>Ecosystem</h2>
    <ul>
      <li><a href="http://router.vuejs.org/" target="_blank">vue-router</a></li>
      <li><a href="http://vuex.vuejs.org/" target="_blank">vuex</a></li>
      <li><a href="http://vue-loader.vuejs.org/" target="_blank">vue-loader</a></li>
      <li><a href="https://github.com/vuejs/awesome-vue" target="_blank">awesome-vue</a></li>
    </ul> -->
    <input type="text" placeholder="请输入类型" v-model="msg" @keyup.enter='submit'><button @click='submit'>提交</button>
    <ul>
      <li v-show="isShow" v-for="(item,index) in todoList" >
        <span v-bind:class="{update:item.isUpdated}">{{item.msg}}</span> 
        <button @click='removeItem(index)'>删除</button>
        <button @click='updateItem(index,item)'>修改</button>
        <!-- <input type="text" v-model="alterMsg"> -->
      </li>
    </ul>
    <button @click="deleteAll" v-show="isAll">delete all</button>
  </div>
</template>

<script>
export default {
  name: 'hello',
  data () {
    return {
      msg: '',
      todoList:[],
      isShow:false,
      isUpdated:false,
      isAll:false
    }
  },
  mounted(){
    this.isAll = this.todoList && this.todoList.length?true:false
  },
  methods:{
    submit:function(){
      this.todoList.push({msg:this.msg,isUpdated:this.isUpdated});
      this.isShow = true;
      this.msg = '';
    }
    ,removeItem:function(i){
      this.todoList.splice(i,1)
    }
    ,updateItem:function(i,item){
      this.todoList[i].isUpdated = !item.isUpdated;
    }
    ,deleteAll:function(){
      this.todoList=[]
    }
  },
  watch:{
    todoList:{
      handler:function(){
        this.isAll = this.todoList && this.todoList.length?true:false;
        deep:true
       }
    }
  },
  computed:{

  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
input{
  width: 200px
}
ul{
  list-style:none
}
input{
  margin-right:10px;
  border: 0;
  box-shadow: 0 0 3px 2px #869523
}
.update{
  text-decoration: line-through;
}
/*h1, h2 {
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
}*/
</style>
