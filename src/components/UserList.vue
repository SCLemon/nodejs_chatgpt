<template>
    <div class="msgBlock" :class="classObj">
        <div class="showMsg" v-text="this.msgList.content"></div>
    </div>
</template>

<script>
export default {
    name:'UserList',
    props:['msgList'],
    computed:{
        classObj(){
            return this.msgList.role=='user'?'user':'assistant'
        }
    },
}
</script>

<style scope>
    .msgBlock{
        width:93%;
        height: auto;
        display: flex;
        margin-left: 10px;
        margin-right: 10px;
    }
    .showMsg{
        max-width:70%;
        word-wrap: break-word;
        padding: 5px;
        border: 1px solid skyblue;
        border-radius: 10px;
        margin-top: 10px;
    }
    .user{
        justify-content: right;
    }
    .assistant{
        justify-content: left;
    }
</style>