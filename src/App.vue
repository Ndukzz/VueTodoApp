<template>
<div class="grid md:grid-cols-9 ">
  <div class="col-span-2"></div>
  <div class="col-span-4 m-8 text-center border border-gray-400 rounded-md w-fit p-2 bg-gray-300 shadow-xl ">
    <h2 class="text-center py-2 text-b text-lg border-gray-500 border-b-2 mx-8 px-4">My Vue To-Do app</h2>

    <!-- inputs -->
    <div class="inputs pt-2">
      <input class="border-gray-300 border-b-2 rounded-sm" v-model="task" type="text" placeholder="Enter text">
      <button @click="submitTask" class="btn bg-yellow-300 rounded-sm hover:bg-yellow-400 p-1 hover:shadow-md">SUBMIT</button>
    </div>

    <!-- Task Table -->
    <div class=" mt-4">
      <table class="bg-gray-300 border-collapse border border-slate-500 rounded-md ...">
        <thead>
          <tr class="bg-teal-400">
            <th class="border border-slate-600 px-6 ...">Task</th>
            <th class="border border-slate-600 px-6 ...">Status</th>
            <th class="border border-slate-600 ...">Edit</th>
            <th class="border border-slate-600 ...">#</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(task, index) in  tasks" :key="index">
            <td class="border border-slate-700 px-2 ..." >
              <span> {{ task.name }} </span>
              </td>
            <td class="border border-slate-700 cursor-pointer ..." @click="updateStatus(index)">{{ task.status }}</td>
            <td class="border border-slate-700 ...">
              <div class="text-center" @click="editTask(index)">
                <span class="fa fa-pen px-3 hover:opacity-50 transition ease-in duration-250"></span>
              </div>
            </td>
            <td class="border border-slate-700 ...">
              <div class="text-center" @click="deleteTask(index)">
                <span class="fa fa-trash px-3 hover:opacity-50 transition ease-in duration-250"></span>
              </div>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
  </div>
</template>

<script>
  export default{
    data(){
      return {
        task: '',
        editedTask: null,
        todoStatuses : ["To do", "In progress", "Done"],
        tasks: [
          {
            name: "Go to the supermarket",
            status: "To do"
          },
          {
            name: "Start this project",
            status: "Done"
          },
          {
            name: "Complete the project",
            status: "Done"
          }
        ]
      }
    },
    methods: {
      submitTask(){
        if(this.task.length === 0) return;

        if(this.editedTask === null){
          this.tasks.push({
            name: this.task,
            status: "to-do"
          });
        }else {
          this.tasks[this.editedTask].name = this.task;
          this.editedTask = null;
        }
        this.task = "";
      },

      deleteTask(index){
        this.tasks.splice(index, 1); //the 1 is no of items to remove
      },

      editTask(index){
        this.task = this.tasks[index].name;
        this.editedTask = index;
      },

      updateStatus(index){
        let newIndex = this.todoStatuses.indexOf(this.tasks[index].status);
        if(++newIndex > 2) newIndex = 0;
        this.tasks[index].status = this.todoStatuses[newIndex];
      }
    }
  };
</script>

<style>
.finished{
  text-decoration: line-through;
}

 
</style>