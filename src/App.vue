<!-- eslint-disable vue/valid-template-root -->
<template lang="">
  <!-- <RouterView /> -->
  <div class="wrap">
    <div id="names" class="container" v-if="state">
      <div class="logo"><h1>Who can get Arisan!</h1></div>
      <div class="input-container">
        <input type="text" v-model.trim="inputName" />
        <button @click="addNameToList">Add</button>
      </div>
      <div class="error-table" v-if="showError">
        {{ error }}
      </div>
      <div>
        <ul class="listname">
          <li v-for="(name, index) in names" :key="name" @click="removeName(index)">{{ name }}</li>
        </ul>
      </div>
      <div>
        <button class="check-winner" v-if="names.length > 1" @click="checkWinner">
          Check Winner
        </button>
      </div>
    </div>

    <div id="names" class="container" v-if="!state">
      <div class="logo"><h1>Selamat!</h1></div>
      <div>
        <h2>The winner is {{ winner }}</h2>
      </div>
      <div>
        <button class="back" @click="state = !state">Back</button>
      </div>
    </div>
  </div>
</template>
<script>
// import { RouterView } from 'vue-router'

export default {
  data() {
    return {
      state: true,
      inputName: '',
      names: [],
      error: '',
      showError: false,
      winner: ''
    }
  },
  methods: {
    addNameToList() {
      const userName = this.inputName
      if (this.validate(userName)) {
        this.names.push(userName)
        this.inputName = ''
        this.showError = false
        console.log(this.names)
      } else {
        this.showError = true
      }
    },
    removeName(index) {
      this.names.splice(index, 1)
    },
    validate(value) {
      if (value === '') {
        this.error = 'Name is required'
        return false
      }

      if (this.names.includes(value)) {
        this.error = 'Name already exists'
        return false
      }

      return true
    },
    checkWinner() {
      this.state = !this.state
      const randomIndex = Math.floor(Math.random() * this.names.length)
      const winner = this.names[randomIndex]
      this.winner = winner
    }
  },
  components: {
    // RouterView,
  }
}
</script>
<style>
* {
  font-family: 'Poppins', sans-serif;
}

.wrap {
  display: block;
  height: 90vh;
  display: flex;
  justify-content: center;
  align-items: center;
}

.container {
  padding: 40px 60px;
  align-items: center;
  display: flex;
  flex-direction: column;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
  overflow-wrap: break-word;
}

.logo h1 {
  font-size: 32px;
  font-family: 'Poppins', sans-serif;
  color: slateblue;
}

.input-container {
  display: flex;
  flex-direction: row;
}

.input-container input {
  padding: 10px 20px;
  width: 100%;
}

.input-container button {
  padding: 10px 20px;
  background-color: darkslateblue;
  color: white;
  border: none;
  cursor: pointer;
}

.error-table {
  color: red;
  margin-top: 10px;
  font-weight: bold;
}

.listname {
  list-style-type: none;
  padding: 0;
  display: flex;
  flex-direction: row;
  justify-content: start;
  align-items: center;
  gap: 20px;
}

.listname li {
  padding: 10px 20px;
  background-color: darkslateblue;
  border-radius: 0.3rem;
  color: white;
  cursor: pointer;
}

.check-winner {
  padding: 10px 20px;
  background-color: white;
  color: darkslateblue;
  border: 1px solid darkslateblue;
  font-weight: bold;
  cursor: pointer;
}

.back {
  padding: 10px 20px;
  background-color: darkslateblue;
  color: white;
  border: none;
  cursor: pointer;
}
</style>
