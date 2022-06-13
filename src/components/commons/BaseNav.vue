<template>
  <nav class="nav-bar">
    <ul class="nav-bar__list">
        <li v-for="(link, index) in links" :key="index" class="nav-bar__item">
            <a @click.prevent="currentLink(index)" class="nav-bar__link" :class="{active : link.isActive}" href="#">{{link.text}}</a>
        </li>
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