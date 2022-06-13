<template>
    <main>
        <div class="container">
            <BaseSection/>
        </div>
    </main>
</template>

<script>
    import BaseSection from "../sections/BaseSection.vue";
    import Shared from "../../shared/Shared";
    import axios from 'axios';

    export default {
        name: 'BaseMain',
        components: {
            BaseSection,
        },
        data() {
            return {
                Shared,
            }
        },
        created() {
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
        },
    }
</script>

<style lang="scss" scoped>
    main {
        background-color: var(--primary-color);
        height: var(--main-height);
        overflow-y: auto;

        &::-webkit-scrollbar {
            width: .5rem;
        }
        
        &::-webkit-scrollbar-track {
            border-radius: .625rem;
        }
            
        &::-webkit-scrollbar-thumb {
            background: var(--bg-color-scrollbar); 
            border-radius: .625rem;
        }

        &::-webkit-scrollbar-thumb:hover {
            background: var(--bg-color-active-scrollbar);
        }

        .main__title {
            text-transform: uppercase;
        }
    }
</style>