<template>
  <div class="container" style="max-width: 600px">
    
    <h2 class="text-center mt-5">Todo Task</h2>

    
    <div class="d-flex mt-5">
      <input
        type="text"
        v-model="task"
        placeholder="Enter task"
        class="w-100 form-control"
      />
      <button class="btn" @click="submitTask">
        SUBMIT
      </button>
    </div>

 
    <table class="table table-bordered mt-5">
      <thead>
        <tr>
          <th scope="col" class="text-center2">Task</th>
          <th scope="col"  class="text-center2" style="width: 120px">Status</th>
          <th scope="col" class="text-center2">Delete</th>
          <th scope="col" class="text-center2">Edit</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(task, index) in tasks" :key="index">
          <td>
            <span :class="{ 'line-through': task.status === 'finished' }">
              {{ task.name }}
            </span>
          </td>
          <td>
            <span
              class="pointer noselect"
              @click="changeStatus(index)"
              :class="{
                'text-danger': task.status === 'to-do',
                'text-success': task.status === 'finished',
                'text-warning': task.status === 'in-progress',
              }"
            >
              {{ capitalizeFirstChar(task.status) }}
            </span>
          </td>
          <td >
            <div @click="deleteTask(index)">
              <span class="fa fa-trash pointer"></span>
            </div>
          </td>
          <td >
            <div @click="editTask(index)">
              <p class="fa fa-pen pointer"></p>
            </div>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },

  data() {
    return {
      task: "",
      editedTask: null,
      statuses: ["to-do", "in-progress", "finished"],

      
      tasks: [
        
      ],
    };
  },

  methods: {
    
    capitalizeFirstChar(str) {
      return str.charAt(0).toUpperCase() + str.slice(1);
    },

    
    changeStatus(index) {
      let newIndex = this.statuses.indexOf(this.tasks[index].status);
      if (++newIndex > 2) newIndex = 0;
      this.tasks[index].status = this.statuses[newIndex];
    },

    
    deleteTask(index) {
      this.tasks.splice(index, 1);
    },

    
    editTask(index) {
      this.task = this.tasks[index].name;
      this.editedTask = index;
    },

    
    submitTask() {
      if (this.task.length === 0) return;

      
      if (this.editedTask != null) {
        this.tasks[this.editedTask].name = this.task;
        this.editedTask = null;
      } else {
        
        this.tasks.push({
          name: this.task,
          status: "todo",
        });
      }

      this.task = "";
    },
  },
};
</script>

<style scoped>
.pointer {
  cursor: pointer;
}

.line-through {
  text-decoration: line-through;
}
.text-center2{
  background-color: aqua;
  font-family: 'Times New Roman', Times, serif;
  font-weight: bold;
  padding-left: 10px;
  text-align: center;
  font-size: large;
}
.text-center {
border-style: solid;
font-family: 'Times New Roman', Times, serif;
border-radius: 10px;
}
.w-100 {
  border-radius: 100px;
  background-color: bisque;
  border-color: black;
  
}

.btn{
  border-radius: 100px;
  background-color: greenyellow;
  border-color: black;
}

</style>