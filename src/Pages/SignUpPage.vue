<template>
    <div class="sign-up-page">
        <div class="sign-up-page-container">
            <article class="sign-up-page__text">
                <h1 class="sign-up-page__title">SignUp</h1>
                <p v-if="errorMessage" class="sign-up-page__error-message">{{ errorMessage }}</p>
            </article>
            <form class="sign-up-page__form" @submit.prevent="handleSubmit">
                <div class="form__container">
                    <p class="form__title">Username</p>
                    <input class="form__input" type="text" v-model="username" name="username"/>
                </div>
                <div class="form__container">
                    <p class="form__title">Password</p>
                    <input class="form__input" type="password" v-model="password" name="password"/>
                </div>
                <div class="form__container">
                    <p class="form__title">Email</p>
                    <input class="form__input" type="email" v-model="email" name="email"/>
                </div>
                <div class="form__container">
                    <p class="form__title">Name</p>
                    <input class="form__input" type="text" v-model="name" name="name"/>
                </div>
                <div class="form__container">
                    <p class="form__title">LastName</p>
                    <input class="form__input" type="text" v-model="lastName" name="lastName"/>
                </div>
                <div class="form__container">
                    <p class="form__title">Age</p>
                    <input class="form__input" type="number" v-model="age" name="Age"/>
                </div>
                <label class="form__title" for="gender">Gender</label>
                <select class="form__input_select" id="gender" v-model="gender" name="gender">
                    <option value="Male">Male</option>
                    <option value="Female">Female</option>
                </select>
                <button class="form__button" type="submit">Submit</button>
            </form>
        </div>
    </div>
</template>

<script setup>
import axios from "axios";
import {ref} from "vue";
import router from "@/router/index.js";

const username = ref('')
const password =ref('')
const email = ref('')
const name = ref('')
const lastName = ref('')
const age = ref('')
const gender = ref('')
const errorMessage = ref('')

const handleSubmit = () => {
    axios.post("http://localhost:3000/register", {
        username: username.value,
        password: password.value,
        email: email.value,
        name: name.value,
        lastName: lastName.value,
        age: age.value,
        gender: gender.value
    })
        .then(data => {
            console.log(data.data.message)
            router.push('/Login')
        })
        .catch((error) => {
            errorMessage.value = error.response.data.message
            console.log(error.response.data.message)
        })
}
</script>

<style scoped>
.sign-up-page{
    display: flex;
    justify-content: center;
    padding-top: 145px;
    padding-bottom: 92px;
}
.sign-up-page-container{
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 26px;
    width: 335px;
    border-radius: 10px;
    box-shadow: 0 3px 9px 0 #00000030;
    padding-bottom: 43px;
}
.sign-up-page__text{
    display: flex;
    justify-content: space-between;
    align-items: center;
    width: 100%;
    padding-top: 16px;
}
.sign-up-page__title{
    font-size: 16px;
    padding-left: 16px;
}
.sign-up-page__error-message{
    color: red;
    font-weight: 500;
    padding-right: 13px;
}
.sign-up-page__form{
    display: flex;
    flex-direction: column;
    gap: 13px;
}
.form__container{
    display: flex;
    flex-direction: column;
    gap: 7px;
}

.form__title{
    font-size: 14px;
    color: #00000099;
}
.form__input{
    width: 136px;
    height: 29px;
    border: none;
    border-radius: 10px;
    background-color: white;
    box-shadow: 0 3px 9px 0 #00000030;
    outline: none;
    padding-left: 16px;
}
.form__input_select{
    width: 152px;
    height: 29px;
    border: none;
    border-radius: 10px;
    background-color: white;
    box-shadow: 0 3px 9px 0 #00000030;
    outline: none;
    padding-left: 16px;
}
.form__button{
    border: none;
    background-color: white;
    margin-top: 7px;
    color: #00000099;
    font-size: 14px;
}
</style>