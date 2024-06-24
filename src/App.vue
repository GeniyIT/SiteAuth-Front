<template>
    <HeaderComponent/>
    <RouterView></RouterView>
    <FooterComponent/>
</template>

<script setup>
import HeaderComponent from "@/components/HeaderComponent.vue";
import FooterComponent from "@/components/FooterComponent.vue";
import {provide, ref} from "vue";
import axios from "axios";

const users = ref([])

    axios.get('http://localhost:3000/users')
        .then(data => {
            users.value = data.data
        })

provide('users', users)
</script>

<style>
*{
    font-family: Heebo, sans-serif;
    padding: 0;
    margin: 0;
}
</style>
