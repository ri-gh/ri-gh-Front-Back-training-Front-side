<template>
  <div class="background" :style="{backgroundColor:this.bgColor, color: this.fColor}">
  <div :style="{backgroundColor:this.bgColor, color: this.fColor}" class="darknight">
    <DarkLight @dark-mode="changeDark"></DarkLight><br>
    <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
    <!-- <InputUser></InputUser> -->
    <CreateUserAccount></CreateUserAccount>
  </div>
</div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import DarkLight from './components/DarkLight.vue'
// import InputUser from './components/InputUser.vue'
import CreateUserAccount from './components/CreateUserAccount.vue'

export default {
  name: 'App',
  data(){
    return{
      bgColor: '',
      fColor: '',
      dark: false

    }
  },
  methods:{
    changeDark(data){
      if(data)
      {this.bgColor='black',
      this.fColor='#56c080'}
      else
      {this.bgColor='white',
      this.fColor='black'}

    }
  },

  components: {
    HelloWorld,
    DarkLight,
    // InputUser,
    CreateUserAccount
  }
}

</script>

<style>
.background {
  height: 100vh;
  width: 100vw;
  background-color:white;}
#app {
  text-align: center;
}
</style>
