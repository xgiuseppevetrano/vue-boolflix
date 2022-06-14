<template>
  <nav class="nav-bar">
    <ul class="nav-bar__list">
        <li class="nav-bar__item" v-for="(link, index) in links" :key="index">
            <a class="nav-bar__link" @click.prevent="currentLink(index)" :class="{active : link.isActive}" href="#">{{link.text}}</a>
        </li>
    </ul>
    <div class="menu">
        <span class="menu__title">Sfoglia</span>
        <span @click="openMenu()" class="menu__icon"><i class="fa-solid fa-caret-down"></i></span>
        <div v-show="dropdownMenu" class="menu__dropdown">
            <ul class="menu__list">
                <li class="menu__item" v-for="(link, index) in links" :key="index">
                    <a class="menu__link" @click.prevent="currentLink(index)" :class="{active : link.isActive}" href="#">{{link.text}}</a>
                </li>
            </ul>
        </div>
    </div>
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
                dropdownMenu: false,
                links: [
                    {
                        text: 'Home',
                        isActive: true
                    },
                    {
                        text: 'Serie Tv',
                        isActive: false
                    },
                    {
                        text: 'Film',
                        isActive: false
                    },
                    {
                        text: 'Nuovi e popolari',
                        isActive: false
                    },
                    {
                        text: 'La mia lista',
                        isActive: false
                    }
                ]
            }
        },
        methods: {
            openMenu() {
                this.dropdownMenu = !this.dropdownMenu
            },
            currentLink(index) {
                if (index === 0) {
                    this.links.forEach(link => link.isActive = false);
                    this.links[index].isActive = !this.links[index].isActive;
                    axios.get('https://api.themoviedb.org/3/movie/upcoming',
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

                    axios.get('https://api.themoviedb.org/3/tv/on_the_air',
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
                } else if (index === 1) {
                    this.links.forEach(link => link.isActive = false);
                    this.links[index].isActive = !this.links[index].isActive;
                    axios.get('https://api.themoviedb.org/3/tv/top_rated',
                        {
                            params: {
                                api_key: 'a7a419e37d72e1c36a8e9d8a86beb8d5',
                                language: 'it-IT'
                            }
                        }
                    ).then((response) => {
                        Shared.tvSeries = response.data.results;
                        Shared.films = [];
                    }).catch((error) => {
                        console.log(error);
                    })
                } else if (index === 2) {
                    this.links.forEach(link => link.isActive = false);
                    this.links[index].isActive = !this.links[index].isActive;
                    axios.get('https://api.themoviedb.org/3/movie/top_rated',
                        {
                            params: {
                                api_key: 'a7a419e37d72e1c36a8e9d8a86beb8d5',
                                language: 'it-IT'
                            }
                        }
                    ).then((response) => {
                        Shared.films = response.data.results;
                        Shared.tvSeries = [];
                    }).catch((error) => {
                        console.log(error);
                    })
                } else if (index === 3) {
                    this.links.forEach(link => link.isActive = false);
                    this.links[index].isActive = !this.links[index].isActive;
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
                } else if (index === 4) {
                    this.links.forEach(link => link.isActive = false);
                    this.links[index].isActive = !this.links[index].isActive;
                    axios.get('https://api.themoviedb.org/3/tv/on_the_air',
                        {
                            params: {
                                api_key: 'a7a419e37d72e1c36a8e9d8a86beb8d5',
                                language: 'it-IT'
                            }
                        }
                    ).then((response) => {
                        Shared.tvSeries = response.data.results;
                        Shared.films = [];
                    }).catch((error) => {
                        console.log(error);
                    })
                }
            }
        }
    }
</script>

<style lang="scss" scoped>
    @import '../../assets/style/mixins.scss';
    
    .nav-bar {
        &__list {
            @include dflex(flex-start);

            @media screen and (max-width: 48rem) {
                & {
                    display: none;
                }
            }
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

            &.active {
                color: var(--primary-color-text);
                font-weight: 700;
            }
        }
    }

    .menu {
        display: none;
        position: relative;
        color: var(--primary-color-text);

        &__dropdown {
            position: absolute;
            top: 35px;
            right: -2.5rem;
            display: flex;
            flex-direction: column;
            padding: .625rem;
            color: var(--primary-color-text);
            background-color: rgba(var(--bg-color-overlay));
            z-index: 1;
            width: 9.375rem;
            text-align: center;
        }

        &__icon {
            margin-left: .625rem;
            cursor: pointer;
        }

        @media screen and (max-width: 48rem) {
            & {
                display: block;
            }
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

            &.active {
                color: var(--primary-color-text);
                font-weight: 700;
            }
        }
    }
    
</style>