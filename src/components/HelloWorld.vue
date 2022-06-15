<template>
  <v-container>
    <v-row class="text-center">
      <v-col class="mb-4">

        <!-- Title -->
        <h1 class="display-2 font-weight-bold ma-4">
          My Todo List
        </h1>

        <!-- Form Input Text Field -->
        <v-text-field class="pa-3" outlined label="Add task" append-icon="mdi-plus-box"></v-text-field>

        <!-- List of tasks -->
        <div v-for="task in tasks" :key="task.id">
          <v-list class="pt-0" flat>
            <v-list-item>
              <template v-slot:default="{ active, }">
                <v-list-item-action>
                  <v-checkbox :input-value="active" color="primary"></v-checkbox>
                </v-list-item-action>

                <v-list-item-content>
                  <v-list-item-title>{{ task.title }}</v-list-item-title>
                </v-list-item-content>
              </template>
            </v-list-item>
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
      tasks: [
        {
          id: 1,
          title: "Sleep",
          done: false
        },
        {
          id: 2,
          title: "Code",
          done: false
        },
        {
          id: 3,
          title: "Repeat",
          done: false
        },]
    }
  },
}
</script>
