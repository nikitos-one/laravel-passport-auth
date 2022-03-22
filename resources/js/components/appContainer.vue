<template>
    <v-app id="inspire">
        <v-navigation-drawer
            v-model="drawer"
            app
        >
            <v-list dense>
                <v-list-item link>
                    <v-list-item-action>
                        <v-list-item-icon>
                            <v-icon>mdi-home</v-icon>
                        </v-list-item-icon>
                    </v-list-item-action>
                    <v-list-item-content>
                        <v-list-item-title>Home</v-list-item-title>
                    </v-list-item-content>
                </v-list-item>
                <v-list-item link @click="logout">
                    <v-list-item-action>
                        <v-list-item-icon>
                            <v-icon>mdi-power</v-icon>
                        </v-list-item-icon>
                    </v-list-item-action>
                    <v-list-item-content>
                        <v-list-item-title>Logout</v-list-item-title>
                    </v-list-item-content>
                </v-list-item>
            </v-list>
        </v-navigation-drawer>

        <v-app-bar app color="deep-purple accent-4" dark>
            <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>

            <v-toolbar-title>Application</v-toolbar-title>
        </v-app-bar>

        <v-main>
            <!--  -->
        </v-main>
    </v-app>
</template>

<script>
export default {
    data: () => ({ drawer: null }),
    computed: {
       currentUser: {
           get() {
               return this.$store.state.currentUser.user;
           }
       }
    },
    methods: {
        logout() {
            axios.post("/logout")
            .then( response => {
                window.location.href = "/login";
            })
        }
    },
    created() {
        axios.defaults.headers.common["Authorization"] = "Bearer " + localStorage.getItem("laravel-app_token");
        this.$store.dispatch('currentUser/getUser');
    }
}
</script>
