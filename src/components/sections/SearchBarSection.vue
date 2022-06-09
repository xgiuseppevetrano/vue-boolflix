<template>
    <div class="search-bar">
        <form @submit.prevent="submitForm()">
            <input type="text" placeholder="Search film" v-model="search">
            <button type="submit">Search</button>
        </form>
    </div>
</template>

<script>
    import axios from 'axios';
    import SharedFilms from "../../shared/SharedFilms";

    export default {
        name: 'SearchBarSection',
        data() {
            return {
                search: '',
                SharedFilms
            }
        },
        methods: {
            submitForm() {
                axios.get('https://api.themoviedb.org/3/search/movie',
                    {
                        params: {
                            api_key: 'a7a419e37d72e1c36a8e9d8a86beb8d5',
                            query: this.search,
                            language: 'it-IT'
                        }
                    }
                ).then((response) => {
                    SharedFilms.films = response.data.results;
                }).catch((error) => {
                    console.log(error);
                })

                axios.get('https://api.themoviedb.org/3/search/tv',
                    {
                        params: {
                            api_key: 'a7a419e37d72e1c36a8e9d8a86beb8d5',
                            query: this.search,
                            language: 'it-IT'
                        }
                    }
                ).then((response) => {
                    SharedFilms.tvSeries = response.data.results;
                }).catch((error) => {
                    console.log(error);
                })

            }
        }
    }
</script>

<style lang="scss" scoped>

</style>