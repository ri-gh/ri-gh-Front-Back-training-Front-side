<template>
    <div>
        <p v-if="infos.name">Bonjour {{ infos.name }}</p>
         <br>
        <input v-model="infos.name" type="text" placeholder="Input your name"><br>
         <br>
        <input type="text" v-model="infos.job" placeholder="Input your job"><br>
        <br>
        <input type="text" v-model="infos.company_name" placeholder="Your company name"><br>
        <input type="submit" @click.prevent="sendInfos(), condition=!condition" value="Envoyer vos réponses"><br>
        <template v-if="condition">
            <table class="job-details">
                <caption>Tableau détails du candidat</caption>
                <tr>
                    <th>Name</th>
                    <th>Company Name</th>
                    <th>Job</th>
                </tr>
                    <td>{{ infos.name }}</td>
                    <td>{{ infos.company_name }}</td>
                    <td>{{ infos.job }}</td>
            </table>
        </template>
        
    </div>
</template>
<script>
import axios from 'axios'

export default{
    data(){
        return{
            infos: {
                name: '',
                job: '',
                company_name :''
            },
            condition: false
        }
    },
    methods: {
        sendInfos(){
            axios.post('http://localhost:5000/post/infos',this.infos)
            .then((response) => {console.log(response)
            this.name = response.data.name
            this.job = response.data.job
            this.company_name = response.data.company_name
            })
            .catch(error => {console.log(error)})
        }
    },
}
</script>
<style>
table, td {
    border: 1px solid;
    background-color: aquamarine;
    font-family: "Sofia", sans-serif;
}

th {
    border: 1px solid;
    background-color: greenyellow;
    font-family: "Trirong", serif;
}

caption{
    font-family: 'Courier New';
    font-weight: bold;
}
</style>