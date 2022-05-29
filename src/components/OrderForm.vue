<template>
    <div>
        <OrderAdded v-if="this.success" v-on:clicked="clicked" />
        <table>
            <tr>
                <td  v-for="item of items" :key="item.id"   @click="select(item)" v-bind:class="{selected: item.selected}">
                    <img v-if="item.status !== 'ripped'" :src="item.img" />
                    <span>{{item.status}}</span>
                </td>  
            </tr>
            <tr class="water"></tr>
            <tr>
                <td v-for="item of items2" :key="item.id" @click="select(item)" v-bind:class="{selected: item.selected}">
                    <img v-if="item.status !== 'ripped'" :src="item.img"/>
                    <span>{{item.status}}</span>
                </td>
            </tr>
        </table>
        
        <form v-if="this.total != 0" @submit="checkForm" >
            <h2>Всего: {{this.total}}кг</h2>
            <h3>Кол-во арбузов: {{this.count}}</h3>
            <v-text-field />
            <input placeholder="Введите адрес доставки: "
                type="text" 
                v-model="this.address"
                v-bind:class="input_field"
             />
             <p v-if="this.addressError">{{this.addressError}}</p>
            <input placeholder="Номер телефона: 8XXX-XXX-XXXX "
                type="text" 
                v-model="this.number"
                v-bind:class="input_field"
              />
              <p v-if="this.numberError">{{this.numberError}}</p>
            <input type="datetime-local" v-model="this.date" v-bind:min="this.dateTime" v-bind:max="this.requiredTime" />
            <p v-if="this.dateError">{{this.dateError}}</p>
            <div v-bind:class="{check: true}">
                <input type="checkbox" v-model="this.slice" /><label>Порезать дольками</label>
            </div>
            <button>Заказать</button>
            
        </form>
    </div>

</template>

<script>
import OrderAdded from "./OrderAdded.vue";
    
    export default {
    name: "OrderForm",
    data() {
        return {
            success: false,
            address: null,
            number: null,
            date: null,
            slice: false,
            addressError: "",
            numberError: "",
            dateError: "",
            total: 0,
            count: 0,
            dateTime: "",
            requiredTime: "",
            selected: [],
            items: [
                { id: 1, img: "/images/ripe.png", status: "ripe", selected: false, weight: this.weight() },
                { id: 2, img: "/images/ripe.png", status: "ripe", selected: false, weight: this.weight() },
                { id: 3, img: "/images/unripe.png", status: "unripe", selected: false, weight: this.weight() },
                { id: 4, img: "/images/ripe.png", status: "ripped", selected: false, weight: this.weight() },
                { id: 5, img: "/images/ripe.png", status: "ripe", selected: false, weight: this.weight() },
                { id: 6, img: "/images/unripe.png", status: "unripe", selected: false, weight: this.weight() }
            ],
            items2: [
                { id: 7, img: "#", status: "ripped", selected: false, weight: this.weight() },
                { id: 8, img: "/images/ripe.png", status: "ripe", selected: false, weight: this.weight() },
                { id: 9, img: "/images/unripe.png", status: "unripe", selected: false, weight: this.weight() },
                { id: 10, img: "/images/ripe.png", status: "ripe", selected: false, weight: this.weight() },
                { id: 11, img: "/images/unripe.png", status: "unripe", selected: false, weight: this.weight() },
                { id: 12, img: "/images/ripe.png", status: "ripe", selected: false, weight: this.weight() }
            ]
        };
    },
    mounted() {
        var currentdate = new Date();
        var month = 0;
        var day = 0;
        var hour = 0;
        var minutes = 0;
        const monthConverter = (currentMonth) => {
            if (currentMonth >= 10) {
                return currentMonth;
            }
            else {
                month.toString();
                month = "0" + (currentMonth);
                return month;
            }
        };
        const dayConverter = (currentDay) => {
            if (currentDay >= 10) {
                return currentDay;
            }
            else {
                day.toString();
                day = "0" + (currentDay);
                return day;
            }
        };
        const hoursConverter = (currentHour) => {
            if (currentHour >= 10) {
                return currentHour;
            }
            else {
                hour.toString();
                hour = "0" + (currentHour);
                return hour;
            }
        };
        const minutesConverter = (currentMinutes) => {
            if (currentMinutes >= 10) {
                return currentMinutes;
            }
            else {
                minutes.toString();
                minutes = "0" + (currentMinutes);
                return minutes;
            }
        };
        this.dateTime = currentdate.getFullYear() + "-"
            + monthConverter(currentdate.getMonth() + 1) + "-"
            + dayConverter(currentdate.getDate()) + "T"
            + hoursConverter(currentdate.getHours()) + ":"
            + minutesConverter(currentdate.getMinutes());
        var myDate = new Date(new Date().getTime() + (9 * 24 * 60 * 60 * 1000));
        this.requiredTime = myDate.getFullYear() + "-"
            + monthConverter(myDate.getMonth() + 1) + "-"
            + dayConverter(myDate.getDate()) + "T"
            + hoursConverter(myDate.getHours()) + ":"
            + minutesConverter(myDate.getMinutes());
        console.log("Date before: ", this.dateTime);
        console.log("Date after: ", this.requiredTime);
    },
    methods: {
        validatePhoneNumber(input_str) {
            var re = /^\8?(\d{3})\)?[- ]?(\d{3})[- ]?(\d{4})$/;

            return re.test(input_str);
        },
        checkForm: function (e) {
            e.preventDefault();
            var phone = this.validatePhoneNumber(this.number);
            if (this.address && this.number && this.date && phone) {
                
                this.success = true;
                console.log(this.success);
                console.log(this.address, this.date);
                console.log(this.selected, this.total);
            }
            if (!this.address) {
                this.addressError = "Укажите адрес доставки";
            }
            if (!this.number) {
                this.numberError = "Укажите ваш номер телефона";
            }
            if (!this.date) {
                this.dateError = "Укажите дату и время доставки";
            }
            if(!phone){
                this.numberError = "Неверный формат"
            }
        },
        weight() {
            return Math.floor((Math.random() * 15) + 8);
        },
        select(item) {
            if (item.status != "ripped" && item.selected == false && this.count < 3 && !this.selected.includes(item.id)) {
                this.selected.push(item.id);
                console.log("Object: ", this.selected);
            }
            this.selected.forEach(i => {
                if (i == item.id) {
                    console.log(item.id);
                    item.selected = item.selected ? false : true;
                    if (item.selected) {
                        this.total += item.weight;
                        this.count++;
                    }
                    else {
                        this.total -= item.weight;
                        this.count--;
                    }
                    console.log(this.total, this.count);
                }
            });
        },
        clicked(success) {
            console.log("Closed")
            this.success = success;
            console.log("Component needed: ", this.success);
        }
    },
    components: { OrderAdded }
}
</script> 
<style scoped>
    table {
        margin: 0 auto;
        width: 40%;
        height: 6rem;
        background-color: green;
    }
    @media only screen and (max-width: 500px){
        table{
            margin: 0 auto;
            width: 100%;
            height: 6rem;
            background-color: green;
        }
    }
    @media screen and (min-width: 520px) and (max-width: 1000px){
        table{
            margin: 0 auto;
            width: 100%;
            height: 6rem;
            background-color: green;
        }
        form {
            display: flex;
            flex-direction: column;
            margin: 0 auto;
            width: 600px;
        }
        input:not([type='checkbox']) {
        margin: 10px 0;
        width: 500px;
        height: 2rem;
        padding: 5px 0 5px 8px;
        border-radius: 10px;
    }
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
    h2, h3{
        text-align: center;
    }
    form {
        display: flex;
        flex-direction: column;
        margin: 0 auto;
        width: 300px;
        
    }
    input[type="checkbox"] {
        background-color: #fff;
        margin: 0;
        font: inherit;
        color: currentColor;
        width: 1.15em;
        height: 1.15em;
        border: 0.15em solid currentColor;
        border-radius: 0.15em;
        transform: translateY(-0.075em);
    }
    
    .check{
        text-align: center;
        display: flex;
        justify-content: center;
    }
    label{
        margin-left: 5px;
    }
    input:not([type='checkbox']) {
        margin: 10px 0;
        width: 300px;
        height: 2rem;
        padding: 5px 0 5px 8px;
        border-radius: 10px;
    }
    
    button {
        width: 50%;
        margin: 0 auto;
        margin-top: 10px;
        
        align-items: center;
        font-family: inherit;
        font-weight: 500;
        font-size: 16px;
        padding: 0.7em 1.4em 0.7em 1.1em;
        color: white;
        background: #ad5389;
        background: linear-gradient(0deg, rgba(20,167,62,1) 0%, rgba(102,247,113,1) 100%);
        border: none;
        box-shadow: 0 0.7em 1.5em -0.5em #14a73e98;
        letter-spacing: 0.05em;
        border-radius: 20em;
        cursor: pointer;
        user-select: none;
        -webkit-user-select: none;
        touch-action: manipulation;
    }
    p{
        color:red;
        font-size: small;
        margin-top: -8px;
    }
    span{
        visibility: hidden;
    }
    td:hover span{
        visibility: visible;
    }
</style>