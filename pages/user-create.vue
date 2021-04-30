<template>
    <section>
        <b-field label="Username">
            <b-input v-model="username" minlength="3" validation-message="Username minimal 3 karakter" maxlength="100"></b-input>
        </b-field>

        <b-field label="Password">
            <b-input type="password"
                v-model="password" minlength="7" validation-message="Password minimal 7 karakter" maxlength="100"
                password-reveal>
            </b-input>
        </b-field>
        <b-field label="Name">
            <b-input v-model="name" minlength="3" validation-message="Name minimal 3 karakter" maxlength="100"></b-input>
        </b-field>
        <b-button @click="submit">
            Submit
        </b-button>
        <b-button @click="$router.push('/user-management')">
            Home Page
        </b-button>
    </section>
</template>
<script>
import axios from 'axios';
    export default {
        data() {
            return {
                username: '',
                password: '',
                name: '',
            }
        },
        methods: {
            submit(){
                const payload={
                    username: this.username,
                    password: this.password,
                    name: this.name
                }
                axios.post('http://127.0.0.1:5000/user/', payload)
            }
        }
    }
</script>

