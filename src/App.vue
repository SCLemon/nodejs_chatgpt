<template>
  <div class="main">
    <UserHeader :isOpen="isOpen"></UserHeader>
    <div v-show="isOpen">
      <Conversation></Conversation>
      <Search></Search>
    </div>
  </div>
</template>

<script>
import Search from './components/Search.vue'
import Conversation from './components/Conversation.vue'
import UserHeader from './components/UserHeader.vue'
export default {
  name: 'App',
  components: {
    Search,Conversation,UserHeader
  },
  data(){
    return{
      isOpen:true
    }
  },
  methods:{
    toggleWindow(){
      this.isOpen=!this.isOpen;
    }
  },
  mounted(){
    this.$bus.$on('toggleWindow',this.toggleWindow);
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.main{
  width:300px;
  border: 1px solid rgb(184, 184, 184);
  border-radius: 10px 10px 0 0;
}
</style>
