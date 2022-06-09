<template>
    <section class="films">
        <ul>
            <li class="films__list" v-for="film in SharedFilms.films" :key="film.id">
                {{film.title}} - 
                {{film.original_title}} - 
                <flag :iso="LanguageIso(film.original_language)"/> - 
                {{film.vote_average}}
            </li>
        </ul>
    </section>
</template>

<script>
    import SharedFilms from "../../shared/SharedFilms";

    export default {
        name: 'FilmSection',
        data() {
            return {
                SharedFilms
            }
        },
        methods: {
            LanguageIso(language) {
                return language === 'en' ? 'gb' : language === 'ja' ? 'jp' : language;
            }
        }

    }
</script>

<style lang="scss" scoped>
    .films {
        padding-bottom: 1.25rem;
    }
</style>