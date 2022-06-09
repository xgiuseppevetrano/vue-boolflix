<template>
    <section class="films">
        <ul>
            <li class="films__list" v-for="film in films" :key="film.id">
                <img :src="urlImage(film.poster_path)" :alt="film.title">
                {{film.title}} - 
                {{film.original_title}} - 
                <flag :iso="languageIso(film.original_language)"/> - 
                {{film.vote_average}}
            </li>
        </ul>
        <ul>
            <li class="tv-series__list" v-for="serie in tvSeries" :key="serie.id">
                <img :src="urlImage(serie.poster_path)" :alt="serie.title">
                {{serie.name}} - 
                {{serie.original_name}} - 
                <flag :iso="languageIso(serie.original_language)"/> - 
                {{serie.vote_average}}
            </li>
        </ul>
    </section>
</template>

<script>

    export default {
        name: 'FilmSection',
        props: {
            films: Array,
            tvSeries: Array
        },
        methods: {
            languageIso(language) {
                return language === 'en' ? 'gb' : language === 'ja' ? 'jp' : language;
            },
            urlImage(url) {
                if (url === null) {
                    return `https://via.placeholder.com/185x260`
                } 
                return `https://image.tmdb.org/t/p/w185/${url}`
            }
        }
    }
</script>

<style lang="scss" scoped>
    .films {
        padding-bottom: 1.25rem;

        &__list {
            margin-top: 1.25rem;
        }
    }
</style>