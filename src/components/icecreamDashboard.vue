<script setup>
import { ref} from 'vue'
const api_url = 'http://localhost:3000/api/v1/icecream'


let orders = reactive({data: []});
let orderId;
let name = ref('');
let email = ref('');
let phone = ref('');
let coneFlavor = ref('');
let iceFlavors = ref('');
let quantity = ref('');
let notes = ref('');

onMounted( () => {
    fetch(api_url) 
    .then((respons) => respons.json())
    .then((data) => {
        orders.data = data.data.icecream;
    })
})

const getOneOrder = (id) => {
    fetch(api_url) 
    .then((response) => respons.json())
    .then((data) => {
        const order = data.data.oneIcecream;
    })
    const order = {
        name: name.value,
        email: email.value,
        phone: phone.value,
        coneFlavor: coneFlavor.value,
        iceFlavors: iceFlavors.value,
        quantity: quantity.value,
        notes: notes.value,
        statuus: status.value,
        timestamps: timestamps.value,

    }

}



</script>

<template>
<div v-for="item in orders.data" :key="item" class="order" >
    <img src="" alt="">
    <h3>{{item.orderId}}</h3>
    <p class="client"> {{ item.name }}</p>
    <p class="status">statuus: <span>{{item.status }} </span></p>
    <button class=" details" @click.prevent="getOneOrder(item._id)">Details</button>
    <button class="delete" @click.prevent="deleteOrder(item._id)">Verwijderen</button>
</div>

<!-- make a pop up card with information of one order -->
    <div id="popup1" class="overlay">
    <div class="popup">
        <h2>{{orderId}}</h2>
        <a class="close" href="#">&times;</a>
        <div class="content">
            <p>Naam: <span>{{name}}</span></p>
            <p>E-mail: <span>{{email}}</span></p>
            <p>Gsm nummer: <span>{{phone}}</span> </p>
            <p>Hoorntje Smaak: <span>{{coneFlavor}}</span></p>
            <p>Ijsje Smaak: <span>{{iceFlavor}}</span></p>
            <p>Aantal: <span> {{quantity}}</span></p>
            <p>Statuus: 
                <select v-model="status">
                    <option disabled value=""></option>
                    <option>Te verwerken</option>
                    <option>Geannuleerd</option>
                    <option>Verzonden</option>
                </select>
            </p>
        </div>
        <button class="details update" @click.prevent="updateOrder( orderId)">Update</button>
    </div>
</div>
</template>

<style scoped>
.order {
   
    box-shadow: 0 0 10px #4E3629;
    padding: 0.5rem;
    margin: 5rem 1rem;
    border-radius: 0.5rem;
    width: 200px;
    height: 300px;
    background: #FAFAFA;
    display: inline-block;
}
/* center order img */
.order img {
    display: block;
    margin-left: auto;
    margin-right: auto;
    width: 100px;
    height: 100px;
    border-radius: 50%;
}

.order h3 {
    text-align: center;
    font-size: 1.5rem;
    margin: 0.5rem 0;
    color: #4E3629;
}

.order p {
    margin: 1rem;  
}
.order .client {
    font-size: 1rem;
    color: rgb(143, 143, 143);
    text-align: center;
    font-weight: 200;

}
.order .status {
    font-weight: 700;
}
.order .status span {
    color: #00A1E4;
}
.order button {
display: inline-block;
margin: 0.5rem 0.75rem;
padding:  0.75rem 1rem;
border: none;
border-radius: 0.25rem;
font-size: 14px;
box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
}
.details {
background: #00A1E4;
color: #FAFAFA;
}
.details:hover {
background: #FFF200;
color: #FAFAFA;
}
.order .delete {
background: #4E3629;
color: #4FA83D;
border: 1px solid #FFF200;
}
.order .delete:hover {
background: #4FA83D;
color: #FAFAFA;
}

.overlay {
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  background: #4E3629;
  transition: opacity 500ms;
  visibility: hidden;
  opacity: 0;
}
.overlay:target {
  visibility: visible;
  opacity: 1;
}

.popup {
  margin: 70px auto;
  padding: 20px;
  background: #FAFAFA;
  border-radius: 5px;
  width: 30%;
  position: relative;
  transition: all 5s ease-in-out;
}

.popup h2 {
  margin-top: 0;
  color: #00A1E4;
  text-align: center;
}
.popup .close {
  position: absolute;
  top: 20px;
  right: 30px;
  transition: all 200ms;
  font-size: 30px;
  font-weight: bold;
  text-decoration: none;
  color: #4E3629;
}
.popup .close:hover {
  color: #4FA83D;
}
.popup .content {
  max-height: 30%;
  overflow: auto;
}
.content p {
    font-size: 1rem;
    margin: 0.5rem 1rem;
    color: #4E3629;
    font-weight: 700;
}
.content p span {
    font-weight: 200;
}
.content p select {
    padding:  0.5rem 0;
    border: 1px solid #4FA83D;
    border-radius: 0.25rem;
    margin: 0.5rem 0;
}

.update {
   border: none;
    border-radius: 0.25rem;
    padding: 0.85rem 1rem;
    position: absolute;
    bottom: 7px;
    right: 0;
    margin: 0.5rem 1rem;

}
</style>

