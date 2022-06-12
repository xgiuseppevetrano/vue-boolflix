<template>
    <div class="search-bar">
        <form @submit.prevent="submitForm()">
            <input class="search-bar__input" type="text" placeholder="Search film or tv series" v-model="search" required>
            <button class="search-bar__button" type="submit"><i class="fa-solid fa-magnifying-glass"></i></button>
        </form>
    </div>
</template>

<script>
    import axios from 'axios';
    import Shared from "../../shared/Shared";

    export default {
        name: 'SearchBarSection',
        data() {
            return {
                search: '',
                Shared,
            }
        },
        created() {
            axios.get('https://api.themoviedb.org/3/movie/popular',
                {
                    params: {
                        api_key: 'a7a419e37d72e1c36a8e9d8a86beb8d5',
                        language: 'it-IT'
                    }
                }
            ).then((response) => {
                Shared.films = response.data.results;
            }).catch((error) => {
                console.log(error);
            })

            axios.get('https://api.themoviedb.org/3/tv/popular',
                {
                    params: {
                        api_key: 'a7a419e37d72e1c36a8e9d8a86beb8d5',
                        language: 'it-IT'
                    }
                }
            ).then((response) => {
                Shared.tvSeries = response.data.results;
            }).catch((error) => {
                console.log(error);
            })

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
                    Shared.films = response.data.results;
                    this.search = '';
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
                    Shared.tvSeries = response.data.results;
                    this.search = '';
                }).catch((error) => {
                    console.log(error);
                })
            },
        }
    }
</script>

<style lang="scss" scoped>
    .search-bar {
        &__input {
            margin-right: 3.125rem;
            padding: .3125rem 1.25rem;
            border-radius: .9375rem;
            border: none;
            text-align: center;
        }

        &__button {
            border: none;
            background-color: transparent;
            font-size: 1.5625rem;
            color: var(--primary-color-text);
            vertical-align: middle;

            &:hover {
                color: #ee2721;
            }
        }
    }
</style>