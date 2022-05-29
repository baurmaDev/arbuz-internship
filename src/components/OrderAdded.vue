<template>

    <div v-bind:class="{modal: true}">
        <div v-bind:class="{modalContent: true}">
            <span v-bind:class="{close: true}" v-on:click="$emit('clicked', this.success)">&times;</span>
            <p>Ваш заказ был успешно добавлен, ожидайте нашего звонка!</p>
        </div>
    </div>
    
</template>
<script>
    export default {
        name: "OrderAdded",
        data(){
            return{
                success: false
            }
        },
        // methods: {
        //     close() {
        //         this.su
        //     }
        // }
    }
</script>
<style scoped>
    .modal {
     
    position: fixed; 
    z-index: 1; /* Sit on top */
    left: 0;
    top: 0;
    width: 100%; /* Full width */
    height: 100%; /* Full height */
    overflow: auto; /* Enable scroll if needed */
    background-color: rgb(0,0,0); /* Fallback color */
    background-color: rgba(0,0,0,0.4); 
    }

    /* Modal Content/Box */
    .modalContent {
    background-color: #fefefe;
    margin: 15% auto; /* 15% from the top and centered */
    padding: 20px;
    border: 1px solid #888;
    width: 80%; /* Could be more or less, depending on screen size */
    color:black;
    font-size: medium;
    font-weight: 500;
    font-style: italic;
    }

    /* The Close Button */
    .close {
    color: #aaa;
    float: right;
    font-size: 28px;
    font-weight: bold;
    }

    .close:hover,
    .close:focus {
    color: black;
    text-decoration: none;
    cursor: pointer;
    }
</style>