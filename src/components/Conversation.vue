<template>
  <div class="container" ref="container">
      <UserList v-for="(obj,index) in content" :key="index" :msgList="obj" ></UserList>
  </div>
</template>

<script>
import UserList from './UserList.vue';
export default {
  name:'Conversation',
  components:{
    UserList
  },
  data(){
    return{
      content:JSON.parse(localStorage.getItem('dialogue')) || [{role:'assistant',content:'hello! how can I help you?'}]
    }
  },
  methods:{
    recordMsg(obj){
      this.content.push(obj);
      this.$bus.$emit('recordTotalMsg',this.content);
    },
    setWindowScroll(){
      var el = this.$refs.container;
      this.$nextTick(function(){
        el.scrollTop = el.scrollHeight;
      })
    },
    clearDialogue(){
      this.content=[{role:'assistant',content:'hello! how can I help you?'}];
      this.$bus.$emit('recordTotalMsg',this.content);
    }
  },
  mounted(){
    this.$bus.$on('recordMsg',this.recordMsg);
    this.$bus.$on('setWindowScroll',this.setWindowScroll);
    this.$bus.$on('clearDialogue',this.clearDialogue);
  }
}
</script>

<style scope>
    .container{
        width: 100%;
        height: 300px;
        border-bottom: 1px solid rgb(184, 184, 184);
        overflow-y: scroll;
        overflow-x: hidden;
        padding-bottom: 10px;
    }
</style>