<template>
  <div class="home">
    <label for="searc"><b>Github</b> Search</label>
    <div>
      <input type="search" name="" id="searc" v-model="value"><button @click="search()" :disabled='button'>Buscar</button>
    </div>
  </div>
</template>
<style scoped>
  .home{
    width: 100%;
    height: 100vh;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }
</style>
<script>

export default {
  name: 'HomeView',
  data(){
    return {
      value:null,
      url:'https://api.github.com/users/',
      button:false
    }
  },
  methods:{
   async search(){
     this.button = true
      let data = await this.ajaxGet(this.value)
      this.button=false
      if(!data.message){
        localStorage.setItem("user",JSON.stringify(data))
        location.href ='/painel'
      }else console.log(data.message)
    },
   async ajaxGet(user){
     let resul= await fetch(this.url+user)
     return await resul.json()
    }
  }
}
</script>
