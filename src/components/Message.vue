<template>
    <div v-show="msg" id="message-container">
        <p>{{msg}}</p>
    </div>
</template>

<script>    
export default {
    name: 'Message',
    data(){
        return {
            msg : ''
        }
    },
    methods: {
        get(msg){
            this.msg = msg;
            setTimeout(() => { this.msg = ''; }, 3000);
        }
    }
}
</script>

<style scoped>
    #message-container{
        color: #004085;
        background-color: #CCE5FF;
        border: 2px solid #B8BAFF;
        border-radius: 5px;
        padding: 10px;
        max-width: 400px;
        max-width: 400px;
        margin: 30px auto;
    }
</style>