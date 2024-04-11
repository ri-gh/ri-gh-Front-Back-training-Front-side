<template>
    <div>
        <h2>Create user account</h2>
        <form action="submit" @submit.prevent="sendInfos()">
            <label for="uname">Username</label><br>
            <input type="text" id="uname" name="uname" v-model="account.username"><br>
            <label for="email">Email</label><br>
            <input type="text" id="email" name="email" v-model="account.email"><br>
            <label for="password">Mot de passe (8 caractères mininum)</label><br>
            <input type="password" id="password" name="password" minlength="8" required v-model="account.password">
            <i class="far fa-eye" id="togglePassword" style="cursor: pointer;" @click="showPassword"></i><br>
            <label for="cpassword">Confirmer mdp</label><br>
            <input type="password" id="cpassword" name="cpassword" minlength="8" required v-model="account.cPassword">
            <i class="far fa-eye" id="togglePassword" style="cursor: pointer;" @click="showCPassword"></i><br><br>
            <input type="submit" value="Envoyer">
        </form>
    </div>
</template>
<script>
import axios from 'axios'

export default{
    data(){
        return {
            click : false,
            account:{
                username: '',
                email:'',
                password: '',
                cPassword: ''
                    },
                }
            },
    methods:{
        showPassword(){
            this.click = !this.click
            let x = document.getElementById('password')
            if(this.click)
                {x.type = 'text'}
            else
                {x.type = 'password'}
                    },
        showCPassword(){
            this.click = !this.click
            let x = document.getElementById('cpassword')
            if(this.click)
                {x.type = 'text'}
            else
                {x.type = 'password'}
                    },
        sendInfos(){
            try{
                if(this.account.password <= 8)
                    {throw alert('mots de passe trop courts merci de modifier')}

                if(this.account.password === this.account.cPassword)
                        {
                            axios.post('http://localhost:5000/create_account',this.account)
                            .then((response) => {
                                console.log(response)
                                this.account.username = response.data.username
                                this.account.email = response.data.email
                                if(response.status == '200')
                                {alert(`Compte de ${this.account.username} créé`)}
                                    })
                            .catch(error => {alert(error.request.response)})
                        }
                    else
                        {throw alert('Les mots de passe sont différents merci de modifier')}
                }
            catch(error){
                console.log(error)
            }

                }

    }
}
</script>
<style>
</style>