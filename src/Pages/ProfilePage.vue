<template>
    <div class="profile-page">
        <h1 v-if="isLoading" class="profile-page__loading">Loading...</h1>
        <h1 v-else-if="errorMessage" class="profile-page__error">{{ errorMessage }}</h1>
        <div v-else class="profile-page__content">
            <div class="content-text">
                <h1 class="content-title">My profile</h1>
                <div class="content-data__list">
                    <div class="content-data__item">
                        <p>Username: {{ thisUsers.username }}</p>
                    </div>
                    <div class="content-data__item">
                        <p>Name: {{ thisUsers.name }}</p>
                    </div>
                    <div class="content-data__item">
                        <p>Lastname: {{ thisUsers.lastName }}</p>
                    </div>
                    <div class="content-data__item">
                        <p>Gender: {{ thisUsers.gender }}</p>
                    </div>
                    <div class="content-data__item">
                        <p>Age: {{ thisUsers.age }}</p>
                    </div>
                    <div class="content-data__item">
                        <p>Email: {{ thisUsers.email }}</p>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
import {ref} from "vue";
import axios from "axios";

const thisUsers = ref({})
let errorMessage = ref('')
const isLoading = ref(true)

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
</script>

<style>
.profile-page{
    display: flex;
    justify-content: center;
    padding-top: 51px;
    padding-bottom: 87px;
}

.profile-page__content{
    display: flex;
    gap: 110px;
}
.content-text{
    display: flex;
    flex-direction: column;
    gap: 50px;
}
.content-title{
    font-size: 44px;
}
.content-data__list{
    display: flex;
    flex-direction: column;
    gap: 11px;
}
.content-data__item{
    display: flex;
    align-items: center;
    height: 40px;
    box-shadow: 0 3px 9px 0 #00000030;
    border-radius: 10px;
    width: fit-content;
}
.content-data__item>p{
    font-weight: 700;
    padding-left: 16px;
    padding-right: 20px;
}
.content-image>img{
    width: 243px;
    height: 243px;
}
</style>
