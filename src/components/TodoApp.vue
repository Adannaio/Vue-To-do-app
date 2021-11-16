<template>
    <div class="container">
        <h2 text-center mt-5>My Vue to-do app</h2>

        <!-- Input -->
        <div class="d-flex">
            <input v-model="task" type="text"  class="form-control" placeholder="Add todo">
            <button @click="submitTask"  class="btn btn-warning rounded-0">Submit</button>
        </div>

        <!-- Tasks Table -->
        <table class="table table-bordered mt-5">
            <thead>
                <tr>
                <th scope="col">Task</th>
                <th scope="col">Status</th>
                <th scope="col" class="text-center">#</th>
                <th scope="col" class="text-center">#</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="(task, index) in tasks" :key="index">
                    <th>{{task.task}}</th>
                    <td style="width : 120px">
                        <span class="pointer" @click="changeStatus(index)">{{task.status}}</span>
                    </td>
                    <td>
                        <div class="text-center" @click="editTask(index)">
                            <span class="fa fa-pen"></span>
                        </div>
                    </td>
                    <td>
                        <div class="text-center" @click="deleteTask(index)">
                            <span class="fa fa-trash"></span>
                        </div>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
</template>


<script>
    export default {
        data() {
            return {
                task: "",
                editedTask: null,
                availableStatuses: ["to-do", "in-progress", "finished"],
                tasks: [
                    {
                        task: "Read my Vue book",
                        status: "to-do"
                    }
                ]
            }
        },

        methods: {
            submitTask(){
                if(this.task.length === 0) return;

                if(this.editedTask === null){
                      this.tasks.push({
                        task: this.task,
                        status: 'to-do'
                    })  
                    this.task = " "
                } else {
                    this.tasks[this.editedTask].task = this.task;
                    this.editedTask = null;
                    this.task = " "
                }
            },

            deleteTask(index){
                this.tasks.splice(index,1)
            },

            editTask(index){
                this.task = this.tasks[index].task;
                this.editedTask = index;
            },

            changeStatus(index){
                let newIndex = this.availableStatuses.indexOf(this.tasks[index].status);
                if(++newIndex > 2) newIndex = 0;
                this.tasks[index].status = this.availableStatuses[newIndex];
            }
        }
    };
</script>

<style scoped>
.pointer{
    cursor:pointer;
}
</style>
