<script setup>
import { ref, computed } from 'vue';

import eventsData from '@/assets/events.json';
const events = ref(eventsData);

const searchTerm = ref('');

const filteredEvents = computed(() => {
    if (!searchTerm.value) {
        return events.value;
    }
    const lowerCaseSearchTerm = searchTerm.value.toLocaleLowerCase();
    return events.value.filter(event => {
        return event.titre.toLowerCase().includes(lowerCaseSearchTerm);
    });
});

</script>

<template>


    <div>
        <h2>Evénements à venir</h2>

        <div class="filter">
            <label for="eventFilter">Filtrer par titre</label>
            <input type="text" id="eventFilter" v-model="searchTerm" placeholder="Saisissez une partie du texte">
        </div>

        <ul v-if="filteredEvents.length > 0">
            <li v-for="event in filteredEvents" :key="event.id">
                <h3>{{ event.titre }}</h3>
                <p>Date : {{ event.date }}</p>
                <p>{{ event.description }}</p>
            </li>
        </ul>
        <p v-else>Aucun événement à venir pour le moment.</p>
    </div>

</template>

<style scoped>
*{
    border-radius: 10px;
}
h2 {
    background-color: aquamarine;
    color: lightcoral;
}

h3 {

    background-color: lightgreen;
    color: red;
}

p {
    background-color: blue;
    color: antiquewhite;
}
</style>