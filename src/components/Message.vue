<template>
    <div v-show="msg" :class="status" id="message-container">
        <p>{{msg}}</p>
    </div>
</template>

<script>    
export default {
    name: 'Message',
    data(){
        return {
            msg : '',
            status: 'info',
        }
    },
    methods: {
        get(msg, status){
            this.status = status === 'danger' || status === 'info' || status === 'success' ? status : 'info'
            this.msg = msg;
            setTimeout(() => { this.msg = ''; }, 3000);
        }
    }
}
</script>

<style scoped>
    .danger{
        color: #FFF;
        border: rgb(163, 45, 45);
        background-color: rgb(255, 75, 75);
    }
    .info{
        color: #004085;
        border: #B8BAFF;
        background-color: #CCE5FF;
    }
    .success{
        color: #FFF;
        border: rgb(76, 199, 76);
        background-color: rgb(100, 255, 100);
    }
    #message-container{
        border-radius: 5px;
        padding: 10px;
        max-width: 400px;
        max-width: 400px;
        margin: 30px auto;
    }
</style>