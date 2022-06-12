<template>
  <nav class="nav-bar">
    <ul class="nav-bar__list">
        <li class="nav-bar__item"><a class="nav-bar__link active" href="#">Home</a></li>
        <li class="nav-bar__item"><a @click="searchTv()" class="nav-bar__link" href="#">Serie TV</a></li>
        <li class="nav-bar__item"><a @click="searchMovie()" class="nav-bar__link" href="#">Film</a></li>
        <li class="nav-bar__item"><a class="nav-bar__link" href="#">Nuovi e popolari</a></li>
        <li class="nav-bar__item"><a class="nav-bar__link" href="#">La mia lista</a></li>
    </ul>
  </nav>
</template>

<script>
    import axios from 'axios';
    import Shared from "../../shared/Shared";

    export default {
        name: 'BaseNav',
        data() {
            return {
                search: '',
                Shared,
            }
        },
        methods: {
            searchTv() {
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
            searchMovie() {
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
            }
        }
    }
</script>

<style lang="scss" scoped>
    .nav-bar {
        &__list {
            display: flex;
            align-items: center;
        }

        &__item {
            list-style-type: none;
            margin: .625rem;
        }

        &__link {
            color: var(--secondary-color-text);
            text-decoration: none;
            font-size: .875rem;

            &:hover {
                color: var(--tertiary-color-text);
            }

            .active & {
                color: var(--primary-color-text);
                font-weight: 700;
            }
        }
    }
</style>