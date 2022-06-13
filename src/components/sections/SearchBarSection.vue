<template>
    <div class="search-bar">
        <form>
            <input v-show="isInputActive" class="search-bar__input" type="text" placeholder="Cerca un film o una serie tv" v-model="search">
            <button class="search-bar__button" @click="submitForm()"><i class="fa-solid fa-magnifying-glass"></i></button>
        </form>
        <div class="search-bar__notification">
            <span class="search-bar__notification-icon"><i class="fa-solid fa-bell"></i></span>
            <span class="search-bar__notification-number">3</span>
        </div>
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
                isInputActive: false
            }
        },
        methods: {
            submitForm() {
                if (this.search === '') {
                    this.isInputActive = !this.isInputActive;
                } else {
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
                }
            },
        }
    }
</script>

<style lang="scss" scoped>
    .search-bar {
        display: flex;
        align-items: center;

        &__input {
            margin-right: 10px;
            padding: .3125rem .9375rem;
            border: none;
            text-align: center;
            background-color: transparent;
            color: var(--primary-color-text);
        }

        &__button {
            border: none;
            background-color: transparent;
            font-size: 1.25rem;
            color: var(--primary-color-text);
            vertical-align: middle;
            cursor: pointer;
        }

        &__button:hover &__input {
            display: inline-block;
        }

        &__notification {
            position: relative;

            &-icon {
                margin: 0 1.5625rem;
                font-size: 1.25rem;
                color: var(--primary-color-text);
                cursor: pointer;
            }

            &-number {
                position: absolute;
                top: 0;
                right: 1.25rem;
                padding: 0 .25rem;
                background-color: #e50914;
                border-radius: 50%;
                color: var(--primary-color-text);
                font-size: .625rem;
                cursor: pointer;
            }
        }

        &__profile {
            
            &-img {
                height: 2.1875rem;
                aspect-ratio: 1;
                border-radius: .25rem;
                vertical-align: middle;
            }
    
            &-menu {
                color: var(--primary-color-text);
                margin-left: .625rem;
                cursor: pointer;
            }
        }
    }
</style>