<template>
  <div id="app">
    <h4 class="bg-primary text-white text-center p-2">
      <!-- element with data binding - text interpolation binding-->
      Task List of the user {{name}}
    </h4>
    <div class="container-fluid p-4">
      <div class="row">
        <div class="col font-weight-bold">Task</div>
        <div class="col-2 font-weight-bold">Accomplished?</div>
      </div>
      <div class="row" v-for="t in tasks" v-bind:key="t.action">
        <div class="col">{{t.action}}</div>
        <div class="col-2">
          <input type="checkbox" v-model="t.done" class="form-check-input" />
          {{t.done}}
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
      }
    }
}
</script>

