<template>
    <div class="users-page">
        <h1 v-if="isLoading"></h1>
        <h1 v-else-if="errorMessage" class="profile-page__error">{{ errorMessage }}</h1>
        <div v-else class="users-list">
            <div class="users-list__item" v-for="user in users" :key="user.id">
                <h1 class="users-list__name">{{user.name + user.lastName}}</h1>
                <p class="users-list__email">{{user.email}}</p>
            </div>
        </div>
    </div>
</template>

<script setup>
import {inject, ref} from "vue";
import axios from "axios";

const isLoading = ref(true)
let errorMessage = ref('')

axios.post('http://localhost:3000/auth', {
    token: localStorage.getItem('token'),
    refreshToken: localStorage.getItem('refreshToken')
})
    .then(data => {
        if(data.data.token){
            isLoading.value = false
            localStorage.setItem('token', data.data.token)
            thisUsers.value = data.data.user
        } else {
            isLoading.value = false
            thisUsers.value = data.data.user
            console.log(data.data.user)
        }
    })
    .catch((error) => {
        isLoading.value = false
        errorMessage.value = error.response.data.message
    })

const users = inject('users')
</script>

<style>
.users-page{
    display: flex;
    justify-content: center;
    padding-top: 71px;
    padding-bottom: 17px;
}
.users-list{
    display: flex;
    flex-direction: column;
    gap: 18px;
}
.users-list__item{
    display: flex;
    align-items: center;
    justify-content: space-between;
    box-shadow: 0 3px 9px 0 #00000030;
    border-radius: 10px;
    padding-left: 16px;
    padding-right: 20px;
    height: 56px;
    width: 500px;
}
.users-list__name{
    font-size: 16px;
}
.users-list__email{
    font-size: 14px;
    color: #00000099;
}
</style>
