<template>
  <div class="col">
    <input type="text" v-model="input">
    <p>{{ input }}</p>
    <button @click="increaseCounter()">{{ counter }}</button>
    <p>{{ goalAchieved }}</p>
    <!-- Enkel bij methods moeten er () achter een functie. omdat goalAchieved in computed staat, moeten er geen haken-->
    <input type="text" v-model="newtask">
    <button @click="addTask()">Taak toevoegen</button>
    <p v-if="hasTasks == false">Alle taken werden uitgevoerd!</p>
    <p v-else>Er zijn nieuwe taken beschikbaar.</p>
    <ol>
      <li v-for="(item, index) in tasks" @click="removeTask(item)" :key="index">{{ item }}</li>
    </ol>
  </div>
</template>

<script>
import JSConfetti from 'js-confetti'
import { computed } from 'vue';

export default {
  computed: {
    hasTasks() {
      if (this.tasks.length == 0) {
        return false
      } else {
        return true
      }
    },
    goalAchieved() {
      if (this.counter >= 10) {
        this.jsConfetti.addConfetti()
        return 'Doel bereikt!'
      }
      else {
        return 'Klik nog meer!'
      }
    }
  },

  data() {
    return {
      counter: 0,
      jsConfetti: new JSConfetti(),
      input: '',
      tasks: [],
      newtask: ''
    }
  },

  methods: {
    increaseCounter() {
      this.counter++
    },
    addTask() {
      this.tasks.push(this.newtask)
      this.newtask = ''
    },
    removeTask(item) {
        const index = this.tasks.indexOf(item);
        this.tasks.splice(index, 1);
    }
  },
}
</script>

<style>
.col {
  display: flex;
  flex-direction: column;
  gap: 1rem;
  width: 25%;
  margin: 0 auto;
  border: 1px solid black;
  padding: 2rem;
}
</style>

























<!--
oplossing
<script>
  import moment from 'moment'

  export default {
    data() {
      return {
        name: '',
        counter: 0
      }
    },

    computed: {
      outputFullNameComputed() {
        console.log('Computed');
        if (this.name === '') {
          return ''
        }
        return `${this.name} ${moment().format('hh:mm:ss')}`
      },
    },

    methods: {
      outputFullName() {
        console.log('Methode');
        if (this.name === '') {
          return ''
        }
        return `${this.name} ${moment().format('hh:mm:ss')}`
      },

      addOne() {
        this.counter += 1
      }
    }
  }
</script>

<template>
  <div class="container">
    <div class="form__field">
      <label for="name">Naam:</label>
      <input type="text" id="name" v-model="name">
    </div>
    <div class="result">
      <h3>Volledige naam met methode</h3>
      <p>{{ outputFullName() }}</p>
    </div>
    <div class="result">
      <h3>Volledige naam met computed property</h3>
      <p>{{ outputFullNameComputed }}</p>
    </div>
    <div class="result">
      <h3>Naam</h3>
      <p>{{ name }}</p>
    </div>
    <div class="result">
      <h3>Teller</h3>
      <p>{{ counter }}</p>
      <button @click="addOne()">Tel 1 bij</button>
    </div>
  </div>
</template>

<style>
.container {
  width: 75%;
  margin: auto;
  padding-bottom: 5rem;
}
.form__field {
  display: flex;
  flex-direction: column;
  margin: 2rem auto;
  padding: 1rem;
  width: 50%;
}

.form__field input {
  width: 100%;
}

.result {
  width: 50%;
  border: 1px solid #0F0F0F;
  border-radius: 5px;
  margin: 2rem auto;
  padding: 1rem;
}
</style> -->
