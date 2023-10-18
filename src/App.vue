<template>
  <div>
    <img alt="Vue logo" src="./assets/logo.png">
    <!-- task1.1 -->
    <hr>
    <get-date-component></get-date-component>
    <!-- task1.2 -->
    <hr>
    <form action="">
      <label for="">Ім'я: </label>
      <input v-model="nameValue" type="text">
      <br> <br>
      <label for="">Вік: </label>
      <input v-model="ageValue" type="text">
      <br> <br>
      <button @click="setForm" type="submit">Додати</button>
    </form>
    <!-- task1.3 -->
    <hr>
    <button @click="isLogged ? logout() : login()">click</button>
    <!-- task2.1 -->
    <hr>
    <ul>
      <li v-for="person in persons" :key="person.id" :style="{ backgroundColor: randomColor(), fontSize: randomFontSize() }">
        Name - {{ person.name }}. Age - {{ person.age }}
      </li>
    </ul>
    <p>qwe</p>
    <!-- task2.2 -->
    <hr>

    <!-- task2.3 -->
    <hr>

    <!-- task3.1 -->
    <hr>

    <!-- task3.2 -->
    <hr>

    <!-- task3.3 -->
    <hr>

    <!-- task3.4 -->
    <hr>

    <hr>
  </div>
</template>

<script>
import getDateComponent from './components/getDateComponent.vue'

export default {
  name: 'App',
  components: {
    'get-date-component': getDateComponent,

  },
  data() {
    return {
      isLogged: false,
      nameValue: '',
      ageValue: '',
      wer: '',
      persons: [
        {
          name: 'Alex',
          age: 20,
        },
        {
          name: 'Artem',
          age: 42,
        },
        {
          name: 'Vlad',
          age: 21,
        },
        {
          name: 'Maxim',
          age: 23,
        },
      ],
      colors: ['yellow', 'green', 'red', 'orange', 'pink'],
    }
  },
  methods: {
    setForm(event) {
      event.preventDefault();
      if (this.nameValue.trim() == '' || this.ageValue.trim() == '' || isNaN(+this.ageValue)) {
        console.log('Перевірте дані введені в форму')
        // this.persons.push({
        //   name: this.nameValue.trim(),
        //   age: this.ageValue.trim(),
        // })
        return
      }
      console.log('Данні в формі виконують всі правила')
    },
    login() {
      this.isLogged = true
      console.log("Logged in");
    },
    logout() {
      this.isLogged = false
      console.log("Logged out");
    },
    randomColor() {
      return this.colors[Math.round(Math.random() * (this.colors.length - 1))];
    },
    randomFontSize() {
      return (Math.ceil(Math.random() * 12) + 12) + 'px'
    }
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
