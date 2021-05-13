<template>
  <div id="app">
    <h4 class="bg-primary text-white text-center p-2">
      <!-- element with data binding - text interpolation binding-->
      Task List of the user {{name}}
    </h4>
    <div class="container-fluid p-4">
      <div class="row" v-if="filteredTasks.length === 0">
        <div class="col text-center">
          <b>You have nothing to do. Splendid!</b>
        </div>
      </div>
      <template v-else>
        <div class="row">
          <div class="col font-weight-bold">Task</div>
          <div class="col-2 font-weight-bold">Accomplished?</div>
        </div>
        <div class="row" v-for="t in filteredTasks" v-bind:key="t.action">
          <div class="col">{{t.action}}</div>
          <div class="col-2 text-center">
            <input type="checkbox" v-model="t.done" class="form-check-input" />
          </div>
        </div>
      </template>
      <div class="row py-2">
        <div class="col">
          <input v-model="newItemText" class="form-control" />
        </div>
        <div class="col-2">
          <button class="btn btn-primary" v-on:click="addNewTodo">Add new task</button>
        </div>
      </div>
      <div class="row bg-secondary py-2 mt-2 text-white">
        <div class="col text-center">
          <input type="checkbox" v-model="hideCompleted" class="form-check-input" />
          <label class="form-check-label font-weight-bold">
            Hide completed tasks
          </label>
        </div>
        <div class="col text-center">
          <button class="btn btn-sm btn-warning" v-on:click="deleteCompleted">
            Delete completed tasks
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
    data() {
      return {
        name: "Linux Kyrios",
        //Array with tasks
        tasks: [{action: "Check out the arrival of Macs with the new M2 processors", done: false},
                {action: "Start looking for a new car", done: false},
                {action: "Buy the biggest delicious Buenos Nachos Pizza", done: true},
                {action: "Remove ex number from my telephone", done: false}],
        hideCompleted: true,
        newItemText: "",
      }
    },
  //Function data to hide or show completed tasks
  computed: {
    filteredTasks() {
      return this.hideCompleted ? this.tasks.filter(t => !t.done) : this.tasks
    }
  },
  //Function for adding new tasks to array tasks and for using local storage to save state
  methods: {
    addNewTodo() {
      this.tasks.push({
        action: this.newItemText,
        done: false
      });
      this.storeData();
      this.newItemText = "";
    },
    //Function for storing data
    storeData() {
      localStorage.setItem("todos", JSON.stringify(this.tasks));
    },
    //Function for removing completed tasks
    deleteCompleted() {
      this.tasks = this.tasks.filter(t => !t.done);
      this.storeData();
    }
  },

  //Function for uploading data from local storage
  created() {
    let data = localStorage.getItem("todos");
    if (data != null) {
      this.tasks = JSON.parse(data);
    }
  }
}
</script>

