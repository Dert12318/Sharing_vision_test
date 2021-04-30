<template>
    <section>
        <b-field label="Username">
            <b-input v-model="username" maxlength="100"></b-input>
        </b-field>

        <b-field label="Password">
            <b-input type="password"
                v-model="password" maxlength="100"
                password-reveal>
            </b-input>
        </b-field>
        <b-field label="Name">
            <b-input v-model="name" maxlength="100"></b-input>
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
                id: null,
                username: null,
                password: null,
                name: null,
            }
        },
        mounted(){
            this.id= this.$route.params.id
            this.getdata()
        },
        methods: {
            submit(){
                const payload={
                    username: this.username,
                    password: this.password,
                    name: this.name
                }
                axios.put(`http://127.0.0.1:5000/user/${this.id}`, payload)
            },
            getdata(){
                axios.get(`http://127.0.0.1:5000/user/${this.id}`).then((res) => {
                    this.username= res.data.username
                    this.password= res.data.password
                    this.name = res.data.name
                });
            }
        }
    }
</script>

