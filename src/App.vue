<script>

export default {
  name: 'App',
  data() {

    return {

      error: false,
      tasks: [
        {
          text: 'fare la spesa',
          done: true
        },
        {
          text: 'pagare la bolletta',
          done: false
        },
        {
          text: 'prendere appuntamento dal dentista',
          done: true
        },
        {
          text: 'passare in farmacia',
          done: true
        },
        {
          text: 'chiamare il veterinario',
          done: false
        },
        {
          text: 'comprare le scarpe',
          done: true
        },
      ],

    }
  },

  methods: {
    removeTask(index) {
      this.tasks.splice(index, 1);
    },

    addNewTask() {
      const newTask = {
        text: this.newTaskText,
        done: false
      };
      if (this.newTaskText.length > 4) {
        this.error = false;
        this.tasks.unshift(newTask);
        this.newTaskText = '';
      } else {
        this.error ='The task must be at least 4 characters long'
      }

    }
  }
}
</script>



<template>
  <div class="container">
    <div class="card">
      <div class="card-body">
        <h1>To do list</h1>
        <ul class="list-group" v-if="tasks.length > 0">
          <li v-for="(task, index) in tasks">

            <!--Opzione 1 style bindin-->
            <span :style="{ textDecoration: task.done ? 'line-through' : '' }">

              {{ task.text }}
            </span>
            <!--Opzione 2: class binding-->
            <!-- <span v-bind:class="{ 'text-decoration-line-through': task.done }">
            {{ task.text }}
            </span> -->

            <!--Stampa x in pagina-->
            <span v-on:click="removeTask(index)">

              &#10060;

            </span>

          </li>
        </ul>

        <p v-else>
          Compiti eseguiti:
          Complimenti 🎈🎈🎈
        </p>


        <div>
          <input type="text" v-model="newTaskText">
          <button @click="addNewTask">Add Task</button>

        </div>
        <span v-if="error">{{ error }}</span>
      </div>
    </div>
  </div>
</template>

<style scoped>
ul {
  list-style: none;
}
</style>
