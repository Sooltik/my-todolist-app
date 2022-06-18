<template>
<v-row
  class="text-center"
>
    <v-col
      class="mb-4"
    >
        <div
          class="home"
        >
            <!-- Title -->
            <h1
              class="display-2 font-weight-bold ma-4"
            >
                My Todo List
            </h1>

            <!-- Form Input Text Field -->
            <v-text-field
              v-model="taskName"
              @click:append="addTask"
              @keyup.enter="addTask"
              class="pa-3"
              append-icon="mdi-plus"
              label="Add Task"
              clearable
              hide-details
              outlined></v-text-field
            >

            <!-- List of Tasks -->
            <v-list
              v-if="tasks.length" 
              class="pt-0"
              flat
            >
                <div
                  v-for="task in tasks"
                  :key="task.id"
                >
                    <v-list-item
                      :class="{ 'blue lighten-5': task.done }"
                      @click="doneTask(task.id)"
                    >
                        <template
                          v-slot:default
                        >

                            <!-- Checkbox -->
                            <v-list-item-action>
                                <v-checkbox
                                  :input-value="task.done"
                                  color="primary"
                                ></v-checkbox>
                            </v-list-item-action>

                            <!-- Name of Task -->
                            <v-list-item-content>
                                <v-list-item-title
                                  :class="{ 'text-decoration-line-through': task.done }"
                                >
                                    {{ task.name }}
                                </v-list-item-title>
                            </v-list-item-content>

                            <!-- Button to Edit -->
                            <v-list-item-action>
                                <v-btn
                                  @click.stop="editTask(task.id)"
                                  icon
                                >
                                    <v-icon
                                      color="primary lighten-1"
                                    >mdi-pencil</v-icon>
                                </v-btn>
                            </v-list-item-action>

                            <!-- Button to Delete -->
                            <v-list-item-action>
                                <v-btn
                                  @click.stop="deleteTask(task.id)"
                                  icon
                                >
                                    <v-icon
                                      color="primary lighten-1"
                                    >mdi-delete</v-icon>
                                </v-btn>
                            </v-list-item-action>

                        </template>
                    </v-list-item>
                    <v-divider></v-divider>
                </div>

            </v-list>

            <!-- No Task Fallback -->
            <div
              v-else
              class="no-tasks"
            >
                <v-icon
                  color="primary"
                  size="100"
                >
                    mdi-check
                </v-icon>
                <div
                  class="text-h5 primary--text"
                >No
                    tasks</div>
            </div>

            <!-- Snackbar -->
            <div>
                <v-snackbar
                v-model="snackbar"
                >
                {{ text }}

                    <template
                      v-slot:action="{ attrs }"
                    >
                        <v-btn
                          v-bind="attrs"
                          :value="true"
                          @click="snackbar = false"
                          color="primary lighten-1"
                          rounded="pill"
                          absolute
                          right
                          text
                        >
                        Close
                        </v-btn>
                    </template>
                </v-snackbar>
            </div>

            <div>
              <v-alert
                :value="alert"
                color="red"
                elevation="8"
                icon="mdi-alert-circle"
                prominent
                type="warning"
                dismissible
                transition="fade-transition"
              >Text field can not be empty</v-alert>
            </div>

        </div>
    </v-col>
</v-row>
</template>

<script>
export default {
    name: 'HelloWorld',

    data() {
        return {
            taskName: "",
            tasks: [],
            snackbar: false,
            text: ``,
            alert : false
        }
    },

    methods: {
        addTask() {
          if(this.taskName === ""){
            this.alert = true
            return false
          }else{
            let newTask = {
                id: Date.now(),
                name: this.taskName,
                done: false
            }
            this.tasks.push(newTask)
            this.taskName = ""
            this.snackbar = true
            this.text = "Task Added"
          }   
        },
        doneTask(id) {
            let task = this.tasks.filter(task => task.id === id)[0]
            task.done = !task.done
            this.snackbar = true
            if(task.done){
                this.text = "Task is Done"
            }else{
                this.text = "Task is not Done yet"
            }
            
        },
        deleteTask(id) {
            this.tasks = this.tasks.filter(task => task.id !== id)
            this.snackbar = true
            this.text = "Task is Deleted"
        },
        editTask(id) {     
            let task = this.tasks.filter(task => task.id === id)[0]
            this.taskName = task.name
            this.tasks = this.tasks.filter(task => task.id !== id)
            this.snackbar = true
            this.text = "Task is being Edited"
        }
    }
}
</script>

<style lang="sass">
.no-tasks
    position: absolute
    left: 50%
    top: 50%
    trasnform: translate(-50%, -50%)
    opacity: 0.5
</style>
