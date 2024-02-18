<template>
  <div class="footer">
    <input class="searchInput" type="text" v-model="promptText" :placeholder="placeholder">
    <div class="sendBtn" @click="sendGPT()">發送</div>
  </div>
</template>

<script>
import OpenAI from "openai";
const apiKey = 'input your own OpenAI Key';
const openai = new OpenAI({apiKey:apiKey,dangerouslyAllowBrowser: true});
export default {
    name:'Search',
    data(){
        return{
            promptText:'',
            middle:'',
            totalMsg:JSON.parse(localStorage.getItem('dialogue')) || [{role:'assistant',content:'hello! how can I help you?'}],
            placeholder:'請輸入文字'
        }
    },
    methods:{
        sendGPT(){
            if(this.promptText.trim()=='') return alert('輸入不可為空');
            this.placeholder='回答生成中...';
            this.$bus.$emit('recordMsg',{
                role:'user',
                content:this.promptText
            });
            
            this.middle = this.promptText;
            this.promptText='';

            openai.chat.completions.create({
            messages: this.totalMsg,
            model: "gpt-3.5-turbo",
            }).then(res=>{
                this.$bus.$emit('recordMsg',res.choices[0].message);
                this.placeholder='請輸入文字';
            });
        },
        recordTotalMsg(obj){
            this.totalMsg = obj;
        },
    },
    mounted(){
        this.$bus.$on('recordTotalMsg',this.recordTotalMsg);
    },
    watch:{
        totalMsg:{
            deep:true,
            handler(value){
                localStorage.setItem('dialogue',JSON.stringify(value));
                this.$bus.$emit('setWindowScroll');
            }
        }
    }
}
</script>

<style scope>
    ::-webkit-scrollbar{
        display: none;
    }
    ::placeholder{
        font-size: 14px;
    }
    input:focus{
        outline: 0;
    }
    .searchInput{
        height: 30px;
        width:70%;
        border: 0;
        margin-right: 15px;
        margin-left: 7px;
        font-size: 17px;
        padding-left:5px;
        border-bottom: 1px solid skyblue;
    }
    .sendBtn{
        display: inline-block;
        width: 22%;
        height: 30px;
        border: 1px solid skyblue;
        border-radius: 7.5px;
        text-align: center;
        line-height: 30px;
        margin-right: 5px;
    }
    .sendBtn:hover{
        cursor: pointer;
        background-color: skyblue;
        color: white;
    }
    .footer{
        width: 100%;
        display: flex;
        padding-top: 5px;
        padding-bottom: 5px;
        justify-content: space-evenly;
        align-items: center;
    }
</style>