<template>
    <div>
        <table>
            <tr>
                <td  v-for="item of items" :key="item.id"   @click="select(item)" v-bind:class="{selected: item.selected}">
                    <img v-if="item.status !== 'ripped'" :src="item.img" />
                    
                </td>  
            </tr>
            <tr class="water"></tr>
            <tr>
                <td v-for="item of items2" :key="item.id" @click="select(item)" v-bind:class="{selected: item.selected}">
                    <img v-if="item.status !== 'ripped'" :src="item.img"/>
                </td>
            </tr>
        </table>
        
        <form v-if="this.total != 0">
            <h2>Всего: {{this.total}}кг</h2>
            <h3>Кол-во арбузов: {{this.count}}</h3>
            <input placeholder="Введите адрес доставки: " type="text"/>
            <input placeholder="Введите свой номер телефона: " type="tel" />
            <input type="datetime-local" v-bind:min="this.dateTime" v-bind:max="this.requiredTime" step=1800 />
            <div>
                <input type="checkbox" /><label>Порезать дольками</label>
            </div>
            <button>Заказать</button>
            
        </form>
    </div>

</template>

<script>
    import { validationMixin } from 'vuelidate';
    import { required} from 'vuelidate/lib/validators'
    export default {
        name: 'OrderForm',
        mixins: [ validationMixin, ],
        data() {
            return {
                form: {
                    name: '',
                    number: ''
                },
                total: 0,
                count: 0,
                dateTime: '',
                requiredTime: '',
                selected: [],
                items: [
                    {id:1,img: "/images/ripe.png", status: 'ripe', selected: false, weight: this.weight()},
                    {id:2,img: "/images/ripe.png", status: 'ripe', selected: false, weight: this.weight()},
                    {id:3,img: "/images/unripe.png", status: 'unripe', selected: false, weight: this.weight()},
                    {id:4,img: "/images/ripe.png", status: 'ripped', selected: false, weight: this.weight()},
                    {id:5,img: "/images/ripe.png", status: 'ripe', selected: false, weight: this.weight()},
                    {id:6,img: "/images/unripe.png", status: 'unripe', selected: false, weight: this.weight()}
                ],
                items2: [
                    {id:7,img: "#", status: 'ripped', selected: false, weight: this.weight()},
                    {id:8,img: "/images/ripe.png", status: 'ripe', selected: false, weight: this.weight()},
                    {id:9,img: "/images/unripe.png", status: 'unripe', selected: false, weight: this.weight()},
                    {id:10,img: "/images/ripe.png", status: 'ripe', selected: false, weight: this.weight()},
                    {id:11,img: "/images/unripe.png", status: 'unripe', selected: false, weight: this.weight()},
                    {id:12,img: "/images/ripe.png", status: 'ripe', selected: false, weight: this.weight()}
                ]
            }
        },
        validations: {
            form: {
                name: {
                    required
                },
                number: {
                    required
                }
            }
        },
        mounted() {
            var currentdate = new Date(); 
            var month = 0;
            var day = 0;
            var hour = 0;
            var minutes = 0;
            const monthConverter = (currentMonth) => {
                if(currentMonth >= 10){
                 return currentMonth;
                }else{
                    month.toString();
                    month = "0" + (currentMonth);
                    return month;
                }
            }
            const dayConverter = (currentDay) => {
                if(currentDay >= 10){
                 return currentDay;
                }else{
                    day.toString();
                    day = "0" + (currentDay);
                    return day;
                }
            }
            const hoursConverter = (currentHour) => {
                if(currentHour >= 10){
                 return currentHour;
                }else{
                    hour.toString();
                    hour = "0" + (currentHour);
                    return hour;
                }
            }
            const minutesConverter = (currentMinutes) => {
                if(currentMinutes >= 10){
                 return currentMinutes;
                }else{
                    minutes.toString();
                    minutes = "0" + (currentMinutes);
                    return minutes;
                }
            }
            this.dateTime = currentdate.getFullYear() + "-"
             + monthConverter(currentdate.getMonth()+1) + "-"
              + dayConverter(currentdate.getDate()) + "T"
               + hoursConverter(currentdate.getHours()) + ":"  
                + minutesConverter(currentdate.getMinutes());
            var myDate = new Date(new Date().getTime()+(9*24*60*60*1000));
            
            this.requiredTime = myDate.getFullYear() + "-"
             + monthConverter(myDate.getMonth()+1) + "-"
              + dayConverter(myDate.getDate()) + "T"
               + hoursConverter(myDate.getHours()) + ":"  
                + minutesConverter(myDate.getMinutes());
            console.log("Date before: ", this.dateTime);
            console.log("Date after: ", this.requiredTime);
        },
        methods: {
            weight() {
                return Math.floor((Math.random() * 15) + 8);
            },
            select(item) {
                if(item.status != "ripped" && item.selected == false && this.count < 3 && !this.selected.includes(item.id)){
                    this.selected.push(item.id);
                    console.log("Object: ", this.selected)
                }
                this.selected.forEach(i => {
                    if(i == item.id){
                        console.log(item.id)
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
                })
                
                // if(item.status != "ripped"){
                //     item.selected = item.selected ? false : true;
                //     if(item.selected){
                //         this.total += item.weight;
                //         this.count++;
                //     }else{
                //         this.total -= item.weight;
                //         this.count--;
                //     }  
                    
                //     console.log(this.total, this.count);
                // }
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
    form {
        display: flex;
        flex-direction: column;
        margin: 0 auto;
        width: 15rem;
    }
</style>