<template >
  <div :class="{ 'dark-theme_color': isDark }">
    <!-- <div> -->
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
      <li v-for="person in persons" :key="person.id"
        :style="{ backgroundColor: person.backColor, fontSize: person.size }">
        Name - {{ person.name }}. Age - {{ person.age }}
      </li>
    </ul>
    <p>qwe</p>
    <!-- task2.2 -->
    <hr>
    <button @click="isVisible = !isVisible">Перемкнути</button>
    <Transition name="bounce">
      <p v-if="isVisible" style="margin-top: 20px; text-align: center;">
        трохи пружний текст
      </p>
    </Transition>
    <!-- task2.3 -->
    <hr>
    <button @click="toggleTheme">Переключить тему</button>
    <!-- task3.1 -->
    <hr>
    <label for="rows">Кількість рядків:</label>
    <input v-model="rowValue" type="number" min="1" />
    <br />
    <label for="columns">Кількість стовпців:</label>
    <input v-model="columnValue" type="number" min="1" />
    <br />
    <button @click="createTable()">Додати</button>
    <table border="1">
      <tr v-for="(row, rowIndex) in arrTable" :key="rowIndex">
        <td v-for="(column, columnIndex) in row" :key="columnIndex">{{ column }}</td>
      </tr>
    </table>
    <!-- task3.2, task3.3 -->
    <hr>
    <list-component></list-component>
    <!-- task3.4 -->
    <hr>
    <ul v-for="(person, index) in persons" :key="index">
      <li v-if="person.age > 21">Ім'я -{{person.name}}. Вік - {{person.age}}</li>
    </ul>
    <hr>
  </div>
</template>

<script>
import getDateComponent from './components/getDateComponent.vue'
import listComponent from './components/listComponent.vue'

export default {
  name: 'App',
  components: {
    'get-date-component': getDateComponent,
    'list-component' : listComponent,

  },
  data() {
    return {
      isLogged: false,
      nameValue: '',
      ageValue: '',
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
      isVisible: true,
      isDark: false,
      rowValue: '',
      columnValue: '',
      arrTable: [],
    }
  },
  methods: {
    toggleTheme() {
      document.body.classList.toggle('dark-theme');
      this.isDark = !this.isDark
    },
    setForm(event) {
      event.preventDefault();
      if (this.nameValue.trim() == '' || this.ageValue.trim() == '' || isNaN(+this.ageValue)) {
        console.log('Перевірте дані введені в форму')
        return
      }
      this.persons.push({
        name: this.nameValue.trim(),
        age: this.ageValue.trim(),
        backColor: this.colors[Math.round(Math.random() * (this.colors.length - 1))],
        size: (Math.ceil(Math.random() * 12) + 12) + 'px',
      })
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
    addStyle() {
      for (let person of this.persons) {
        person.backColor = this.colors[Math.round(Math.random() * (this.colors.length - 1))];
        person.size = (Math.ceil(Math.random() * 12) + 12) + 'px';
      }
    },
    createTable() {
      this.arrTable = [];
      let num = 0;
      for (let i = 0; i < this.rowValue; i++) {
        let arrColumn = [];
        for (let j = 0; j < this.columnValue; j++) {
          arrColumn.push(++num)
        }
        this.arrTable.push(arrColumn);
      }
    },
  },
  mounted() {
    this.addStyle();
  },
  watch: {
    isDark() {
      this.isDark
    }
  }
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

.bounce-enter-active {
  animation: bounce-in 0.5s;
}

.bounce-leave-active {
  animation: bounce-in 0.5s reverse;
}

@keyframes bounce-in {
  0% {
    transform: scale(0);
  }

  50% {
    transform: scale(1.25);
  }

  100% {
    transform: scale(1);
  }
}

:root {
  --background-color: #ffffff;
}

.dark-theme {
  --background-color: #333333;
}

body {
  background-color: var(--background-color);
}

.dark-theme_color {
  color: #fff;
}
</style>
