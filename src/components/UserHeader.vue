<template>
  <div class="userHeader">
    <div class="image-icon"></div>
    <div class="name">檸檬小助手</div>
    <div class="xmark" @click="handleClear()">
        <i class="fa-solid fa-trash-can-arrow-up"></i>
    </div>
    <div class="xmark" @click="handleWindow()">
        <i v-if="isOpen" class="fa-solid fa-chevron-down"></i>
        <i v-else class="fa-solid fa-chevron-up"></i>
    </div>
  </div>
</template>

<script>
export default {
    name:'userHeader',
    props:['isOpen'],
    methods:{
        handleWindow(){
            this.$bus.$emit('toggleWindow');
        },
        handleClear(){
            if(confirm('確認清除對話紀錄？'))
                this.$bus.$emit('clearDialogue');
        }
    }
}
</script>

<style scope>
    .userHeader{
        width:100%;
        height: 40px;
        background-color: skyblue;
        border-radius: 10px 10px 0 0;
        color: white;
        display: flex;
        align-items: center;
    }
    .image-icon{
        width:30px;
        height: 30px;
        border-radius: 30px;
        border: 1px solid white;
        margin-left: 5px;
        background-color: white;
        z-index: 1;
        background-image: url(../assets/lemon.svg);
        background-repeat: no-repeat;
        background-position: center;
        background-size: contain;
    }
    .name{
        width:190px;
        margin-left: 8px;
    }
    .xmark{
        width:20px;
        margin-right: 10px;
        height: 20px;
        font-size: 20px;
        line-height: 20px;
        text-align: center;
    }
</style>