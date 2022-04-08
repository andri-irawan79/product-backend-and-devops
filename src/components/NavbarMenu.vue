<template>
        <v-app-bar
            app
            fixed
            color="primary"
            dark
        >
            <v-btn icon @click="setMenu()">
                <v-icon>mdi-menu</v-icon>
            </v-btn>

            <v-toolbar-title class="pl-0 pl-sm-5" style="padding: 0px">
                <h4>News App</h4>
            </v-toolbar-title>
            <v-spacer></v-spacer>
            <div v-if="!searchOn">
                <v-btn icon @click="setSearchOn()" class="mr-3">
                    <v-icon>mdi-magnify</v-icon>
                </v-btn>
            </div>
            <div v-else class="mt-6">
                <v-text-field
                    placeholder="Enter for search..."
                    append-icon="mdi-close"
                    @click:append="setSearchOff" 
                    autofocus
                    rounded
                    light
                    background-color="white"
                    @keyup.enter="searchNews()"
                    v-model="keyWordSearch"
                />
            </div>
        </v-app-bar>
</template>

<script>
export default {
    name: 'NavbarMenu',
    data(){
        return {
            searchOn: false,
            keyWordSearch: ''
        };
    },
    computed: {
        menuValue(){
            return this.$store.state.sidebar;
        },
        newsList(){
            return this.$store.state.articles;
        },
        statusData() {
            return this.$store.state.statusPage;
        },
    },
    methods: {
        setSearchOn(){
            this.searchOn = true;
        },
        setSearchOff(){
            this.searchOn = false;
        },
        setMenu(){
            if (this.menuValue === false) {
                return this.$store.dispatch('changeSidebar', true);
            }
            else {
                return this.$store.dispatch('changeSidebar', false);
            }
        },
        searchNews(){
            if(this.keyWordSearch == '') {
                this.searchOn = false;
            }
            else {
                this.$store.dispatch('fetchByMenu', this.keyWordSearch);
                this.keyWordSearch = '';
                // this.searchOn = false;
                  
            }
        },
    },
}
</script>

<style>

</style>