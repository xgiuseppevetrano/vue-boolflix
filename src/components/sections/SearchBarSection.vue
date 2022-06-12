<template>
    <div class="search-bar">
        <form @submit.prevent="submitForm()">
            <input class="search-bar__input" type="text" placeholder="Cerca un film o una serie tv" v-model="search" required>
            <button class="search-bar__button" type="submit"><i class="fa-solid fa-magnifying-glass"></i></button>
        </form>
        <span class="search-bar__icon"><i class="fa-solid fa-bell"></i></span>
        <div class="search-bar__profile">
            <img class="search-bar__profile-img" src="https://occ-0-728-778.1.nflxso.net/dnm/api/v6/K6hjPJd6cR6FpVELC5Pd6ovHRSk/AAAABblk273QcrCjR5jPR9T6L9taELQ9mbaVRrNiR2HzjkJRGuz7kz-ZQAPz4hEXsNe2xFZP7FZtdetaa8xsfjD1apzCdT9BqtE.png?r=3e2" alt="">
            <span class="search-bar__profile-menu"><i class="fa-solid fa-caret-down"></i></span>
        </div>
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
        display: flex;
        align-items: center;

        &__input {
            margin-right: 1.5625rem;
            padding: .3125rem .9375rem;
            border-radius: .9375rem;
            border: none;
            text-align: center;
        }

        &__button {
            border: none;
            background-color: transparent;
            font-size: 1.25rem;
            color: var(--primary-color-text);
            vertical-align: middle;
        }

        &__button:hover &__input {
            display: inline-block;
        }

        &__icon {
            margin: 0 1.5625rem;
            font-size: 1.25rem;
            color: var(--primary-color-text);
        }

        &__profile-img {
            height: 2.1875rem;
            aspect-ratio: 1;
            border-radius: .25rem;
            vertical-align: middle;
        }

        &__profile-menu {
            color: var(--primary-color-text);
            margin-left: .625rem;
        }
    }
</style>