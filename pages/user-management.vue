
31-40 / 200
<template>
    <section>
        <b-button @click="$router.push('/user-create')">
            Create User
        </b-button>
        <b-table 
            :data="data" 
            :total="total"
            :per-page="perPage"
            paginated
            backend-pagination
            @page-change="onPageChange" >
            <b-table-column field="id" label="ID" v-slot="props">
                {{ props.row.id }}
            </b-table-column>
            <b-table-column field="username" label="Username" v-slot="props">
                {{ props.row.username }}
            </b-table-column>
            <b-table-column field="password" label="Password" v-slot="props">
                {{ props.row.password }}
            </b-table-column>
            <b-table-column field="name" label="Name" v-slot="props">
                {{ props.row.name }}
            </b-table-column>
            <b-table-column field="action" label="action" v-slot="props">
                <b-button @click="deleteUser(props.row.id)">
                    delete
                </b-button>
                <b-button @click="$router.push(`/user-edit/${props.row.id}`)">
                    edit
                </b-button>
            </b-table-column>
            </b-table>
    </section>
</template>

<script>  
    import axios from 'axios';
    export default {
        data() {
            return {
                total: 100,
                current: 1,
                perPage: 5,
                data:[]
            }
        },
        mounted(){
            this.getTabel()
        },
        methods: {
                onPageChange(page){
                    this.current = page
                    this.getTabel()
                },
                getTabel() {
                const tabel = [];
                axios.get(`http://127.0.0.1:5000/user/${this.perPage}/${this.current-1}`)
                .then((res) => {
                        this.data = res.data;
                });
                },
                deleteUser(id){
                    axios.delete(`http://127.0.0.1:5000/user/${id}`)
                .then(() => {
                        this.getTabel()
                });
                }
            }
    }
</script>
