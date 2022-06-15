<template>
<v-app>
    <!-- Header -->
    <v-app-bar app color="primary" dark prominent hide-on-scroll src="mountains.png">
        <template v-slot:img="{ props }">
            <v-img v-bind="props" gradient="to top right, rgba(19,84,122,.5), rgba(128,208,199,.8)"></v-img>
        </template>

        <v-spacer></v-spacer>

    </v-app-bar>

    <v-main>
        <HelloWorld />
    </v-main>
</v-app>
</template>

<script>
import HelloWorld from './components/HelloWorld';

export default {
    name: 'App',

    components: {
        HelloWorld,
    },

    data: () => ({
        //
    }),
};
</script>
