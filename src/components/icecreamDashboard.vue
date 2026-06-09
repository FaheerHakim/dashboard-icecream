<script setup>
import { ref} from 'vue'


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

