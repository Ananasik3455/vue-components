<template>
    <div class="modal-backdrop" @click="$emit('close')"></div>
    <div class="modal">
        <form class="form-control">
            <div v-if="isAuth">
                <h1>Авторизация</h1>
                <input type="email" placeholder="Введите почту">
                <input type="password" placeholder="Введите пароль">
                <router-link class="auth__button" to="">Войти</router-link>
                <small>
                    Нет аккаунта?<router-link class="reg__button" @click="isAuth = false" to="">Создайте!</router-link>
                </small>
            </div>
            <div v-else>
                <h1>Регистрация</h1>
                <input type="text" placeholder="Введите имя">
                <input type="text" placeholder="Введите фамилию">
                <input type="email" placeholder="Введите почту">
                <input type="password" placeholder="Введите пароль">
                <router-link class="auth__button" to="">Создать</router-link>
                <small>
                    Уже есть аккаунт?<router-link class="reg__button" @click="isAuth = true" to="">Войдите!</router-link>
                </small>
            </div>
        </form>
    </div>
</template>

<script>
    export default {
        data(){
            return {
                isAuth: true,
            }
        },
         emits: ['close']
    }
</script>

<style scoped>
    .modal {
        position: fixed;
        top: 160px;
        min-height: 200px;
        width: 500px;
        padding: 1rem;
        background: #fff;
        z-index: 1000;
        left: 50%;
        border-radius: 10px;
        transform: translateX(-50%);
        box-shadow: 2px 3px 10px rgba(0, 0, 0, 0.2);
        text-align: center;
    }

    .modal-backdrop {
        position: fixed;
        top: 0;
        right: 0;
        left: 0;
        bottom: 0;
        background: rgba(0, 0, 0, .35);
    }

    .form-control {
        position: relative;
        margin-bottom: 0.5rem;
    }

    .form-control input,
    .form-control select{
        margin: 15px auto;
        outline: none;
        border: 2px solid #ccc;
        display: block;
        width: 70%;
        color: #2c3e50;
        padding: 0.5rem 1.5rem;
        border-radius: 3px;
        font-size: 1rem;
        resize: none;
    }

    .form-control small {
        text-align: center;
        margin-top: 2px;
        display: block;
    }

    .form-control input:active,
    .form-control input:focus {
        transition: border 0.22s;
        border: 2px solid #42b983;
    }

    .auth__button {
        display: inline-block;
        padding: 5px 25px;
        text-decoration: none;
        color: #fff;
        font-weight: 800;
        text-transform: uppercase;
        margin: 30px 0px 0px;
        background: #f58422;
        border: 2px solid #f58422;
        border-radius: 10px;
        cursor: pointer;
    }

    .auth__button:hover {
        display: inline-block;
        padding: 5px 25px;
        text-decoration: none;
        color: #F2994A;
        font-weight: 800;
        text-transform: uppercase;
        background: none;
        border: 2px solid #f58422;
        margin: 30px 0px 0px;
        cursor: pointer;
        cursor: pointer;
    }

    .reg__button {
        display: inline-block;
        text-decoration: none;
        color: #4B5CD7;
        font-weight: 400;
    }

    .reg__button:hover {
        display: inline-block;
        text-decoration: none;
        color: #4B5CD7;
        font-weight: 400;
        cursor: pointer;
    }

    .reg__button,
    .reg__button:after,
    .reg__button:before {
        transition: all .5s;
    }

    .reg__button{
        position: relative;
    }
    .reg__button:after{
        position: absolute;
        bottom: 0;
        left: 0;
        right: 0;
        margin: auto;
        width: 0%;
        content: '.';
        color: transparent;
        background: #2E3884;
        height: 1px;
    }
    .reg__button:hover:after {
        width: 100%;
    }
</style>