<template>
<v-container>
    <v-row class="text-center">
        <v-col class="mb-4">

            <!-- Title -->
            <h1 class="display-2 font-weight-bold ma-4">
                My Todo List
            </h1>

            <!-- Form Input Text Field -->
            <v-text-field v-model="taskName" class="pa-3" outlined label="Add task" @click:append="addTask" @keyup.enter="addTask" append-icon="mdi-plus-box" clearable>
            </v-text-field>

            <!-- List of tasks -->
            <div v-for="task in tasks" :key="task.id">
                <v-list class="pt-0" flat>
                    <v-list-item @click="doneTask(task.id)" :class="{ 'blue lighten-5': task.done }">
                        <template v-slot:default>

                            <!-- Checkbox -->
                            <v-list-item-action>
                                <v-checkbox :input-value="task.done"></v-checkbox>
                            </v-list-item-action>

                            <!-- Name of task -->
                            <v-list-item-content>
                                <v-list-item-title :class="{'text-decoration-line-through':task.done}">{{ task.title }}</v-list-item-title>
                            </v-list-item-content>

                            <!-- Button to delete -->
                            <v-list-item-action>
                                <v-btn icon @click.stop="deleteTask(task.id)">
                                    <v-icon color="primary lighten-1">mdi-delete</v-icon>
                                </v-btn>
                            </v-list-item-action>

                        </template>
                    </v-list-item>
                    <v-divider></v-divider>
                </v-list>
            </div>

        </v-col>
    </v-row>
</v-container>
</template>

<script>
export default {
    name: 'HelloWorld',

    data() {
        return {
            taskName: "",
            tasks: []
        }
    },

    methods: {
        addTask() {
            let newTask = {
                id: Date.now(),
                title: this.taskName,
                done: false
            }
            this.tasks.push(newTask);
            this.taskName = "";
        },
        doneTask(id) {
            let task = this.tasks.filter(task => task.id === id)[0]
            task.done = !task.done
        },
        deleteTask(id) {
            this.tasks = this.tasks.filter(task => task.id !== id)
        }
    }
}
</script>
