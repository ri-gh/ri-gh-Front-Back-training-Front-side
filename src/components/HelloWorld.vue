<template>
  <div>
    <h1 class="font-effect-fire">Vue.js Frontend avec Backend Python Fastapi</h1>
    <div v-if="message">
    <h2>{{ message }}</h2>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default{
  data(){
    return{
      message: null
    };
  },
mounted() {
  axios.get('http://localhost:5000/api/message')
  .then(response => {
    this.message = response.data.message
    console.log(this.message)
    })
  .catch(error => {
    console.error(error)
    })

}
}
</script>
