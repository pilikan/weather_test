<script setup lang="ts">
import { ref } from 'vue';

const emit = defineEmits(['searchCountry'])
const isNotFilled = ref(false);

const country = ref("")

const searchCountry = (): void => {
    if (country.value !== "") {
        isNotFilled.value = true;
        emit('searchCountry', country.value)
    } else {
        isNotFilled.value = true;
    }
}
</script>

<template>
    <div class="form_card">
        <input :placeholder="isNotFilled ? 'Required' : 'Country'" type="text" v-model="country"
            :class="{ 'placeholder-warning': isNotFilled, 'placeholder-default': !isNotFilled }">
        <button class="button" @click="searchCountry">Поиск</button>
    </div>
</template>

<style scoped>
.form_card {
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 10px;
}
</style>
