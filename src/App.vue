<template>
<v-app>
    <!-- Header -->
    <v-app-bar
      color="primary"
      src="mountains.png"
      app
      dark
      hide-on-scroll
      prominent
    >
        <template
          v-slot:img="{ props }"
        >
            <v-img
              v-bind="props"
              gradient="to top right, rgba(19,84,122,.5), rgba(128,208,199,.8)"
            ></v-img>
        </template>

        <v-spacer></v-spacer>

        <!-- Date and Time -->
        <v-container
          class="text-h4 ma-6"
        >
            <v-row>
                {{ date }}
            </v-row>
        </v-container>

    </v-app-bar>

    <v-main>
        <HelloWorld />
    </v-main>
</v-app>
</template>

<script>
import HelloWorld from './components/HelloWorld';
import {
    format
} from 'date-fns'

export default {
    name: 'App',

    components: {
        HelloWorld,
    },

    data() {
        return {
            date: ''
        }
    },
    methods: {
        getDate() {
            this.date = format(new Date(), 'MMMM d, H:mm:ss')
            setTimeout(this.getDate, 1000)
        }
    },
    mounted() {
        this.getDate()
    }
};
</script>
