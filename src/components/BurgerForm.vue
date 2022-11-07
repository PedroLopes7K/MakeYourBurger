<template>
  
<div>
  <div>

    <form id="burger-form" @submit="createBurger($event)">
    <Message :msg="msg" v-show="msg"/>

   <div class="input-container">
    <label for="name">Name of customer:</label>
    <input type="text" id="name" name="name" v-model="name">
   </div>
   <div class="input-container">
    <label for="bread">Choice the bread:</label>
    <select name="bread" id="bread" v-model="bread">
      <option value="">-----</option>

      <option v-for="bread in breads" :key="bread.id" :value="bread.tipo"> {{ bread.tipo}}</option>
    </select>
   </div>

   <div class="input-container">
    <label for="meat">Choice the meat:</label>
    <select name="meat" id="meat" v-model="meat">
      <option value="">-----</option>
      <option v-for="meat in meats" :key="meat.id" :value="meat.tipo"> {{ meat.tipo}}</option>
    </select>
   </div>

   
   <div id="options-container" class="input-container">
    <label id="options-title" for="meat">Choice options:</label>
    <div class="checkbox-container" v-for="option in optionsData" :key="option.id" >
      <input type="checkbox" name="options" v-model="opitions" :value="option.value" >
      <span>{{option.tipo}}</span>
    </div>
    
   </div>

   
   <div class="input-container">
<input type="submit" class="submit-btn" value="Create Burger">
   </div>
    </form>
  </div>
</div>
</template>

<script>
import Message from './Message.vue'
export default {
  name: "BurgerForm",
  components: {
    Message
  },
  data() {
    return {
      breads: null,
      meats: null,
      optionsData: null,
      name:null,
      bread: null,
      meat: null,
      options: [],
      status: "Send",
      msg: null
    }
  },

  methods: {
    async getIngredients() {
      const req = await fetch('http://localhost:3000/ingredientes')
      const data = await req.json()

      console.log(data)

      this.breads = data.paes
      this.meats = data.carnes
      this.optionsData = data.opcionais

    },
    async createBurger(e) {

      e.preventDefault()

      const data = {
        nome: this.name,
        carne: this.meat,
        pao:   this.bread,
        opcionais: Array.from(this.options) ,
        status: "Solicitado"
      }

      const dataJson = JSON.stringify(data)

      const req = await fetch("http://localhost:3000/burgers", {
        method: "POST",
        headers: {"Content-Type": "application/json"},
        body: dataJson
      })

      const res = await req.json()
      this.msg = "Success!"

      setTimeout(() => {
        this.msg = null
      }, 4000)

      console.log(res)
      this.name = '',
      this.meat = '',
      this.bread = '',
      this.options = []


    }

  },

  mounted() {
    this.getIngredients()
  }
}
</script>

<style scoped>

#burger-form {
  max-width: 400px;
  margin: 0 auto;
}
.input-container {
  display: flex;
  flex-direction: column;
  margin-bottom: 20px;
}

label {
  font-weight: bold;
  margin-bottom: 15px;
  color: #222;
  padding: 5px 10px;
  border-left: 4px solid #FCBA03;
}

input, select {
  padding: 5px, 10px;
width: 300px;
height: 30px;
}

#options-container {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
}
#options-title {
  width: 100%;
}
.checkbox-container {
  display: flex;
  align-items: center;
}
.checkbox-container span {
  margin-left: 6px;
  font-weight: bold;
}

.checkbox-container span,
.checkbox-container input {
  width: auto;
  margin: 4px;
}


.submit-btn {
  background-color: #222;
  color: #FCBA03;
  font-weight: bold;
  height: 50px;
  border: 2px solid #222;
  border-radius: 5px;
  padding: 5px 5px;
  font-size: 16px;
  margin: 0 auto;
  cursor: pointer;
  transition: .5s;
}

.submit-btn:hover {
  background-color: transparent;
  color: #222;
}
</style>