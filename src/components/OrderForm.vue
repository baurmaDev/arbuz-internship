<template>
    <form>
        <table>
            <tr>
                <td v-for="item of items" :key="item.id" @click="select(item)" v-bind:class="{selected: item.selected}">
                    <img v-if="item.status !== 'ripped'" :src="item.img"/>
                </td>  
            </tr>
            <tr class="water"></tr>
            <tr>
                <td v-for="item of items2" :key="item.id" @click="select(item)" v-bind:class="{selected: item.selected}">
                    <img v-if="item.status !== 'ripped'" :src="item.img"/>
                </td>
            </tr>
        </table>
    </form>
</template>
<script>
    export default {
        name: 'OrderForm',
        data() {
            return {
                total: 0,
                count: 0,
                
                items: [
                    {id:1,img: "/img/ripe.cdcc8d3d.png", status: 'ripe', selected: false, weight: this.weight()},
                    {id:2,img: '/img/ripe.cdcc8d3d.png', status: 'ripe', selected: false, weight: this.weight()},
                    {id:3,img: '/img/unripe.3a866efc.png', status: 'unripe', selected: false, weight: this.weight()},
                ],
                items2: [
                    {id:1,img: "/img/ripe.cdcc8d3d.png", status: 'ripped', selected: false, weight: this.weight()},
                    {id:2,img: '/img/ripe.cdcc8d3d.png', status: 'ripe', selected: false, weight: this.weight()},
                    {id:3,img: '/img/unripe.3a866efc.png', status: 'unripe', selected: false, weight: this.weight()},
                ]
            }
        },
        methods: {
            weight() {
                return Math.floor((Math.random() * 15) + 8);
            },
            select(item) {
                if(item.status != "ripped"){
                    
                    item.selected = item.selected ? false : true;
                    if(item.selected){
                        this.total += item.weight;
                        this.count++;
                    }else{
                        this.total -= item.weight;
                        this.count--;
                    }  
                    console.log(this.total, this.count);
                }
                              

            }
        }
    }
</script> 
<style scoped>
    table {
        margin: 0 auto;
        width: 20%;
        height: 6rem;
        background-color: green;
    }
    table, th, td {
        border:1px solid black;
    }
    .water {
        background-color: blue;
        height: 30px;
    }
    td {
        background-color: brown;
    }
    td:hover {
        background-color: orange;
    }
    img {
        width: 100%;
    }
    .selected {
        background-color: rgb(94, 245, 7);
    }
</style>