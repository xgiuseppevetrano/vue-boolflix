<template>
    <section>
        <ul>
            <h1>Film</h1>
            <li v-for="film in films" :key="film.id">
                <img :src="urlImage(film.poster_path)" :alt="film.title">
                {{film.title}} - 
                {{film.original_title}} - 
                <flag :iso="languageIso(film.original_language)"/> - 
                <span class="star" v-html="starsVote(film.vote_average)"></span>
            </li>
        </ul>
        <ul>
            <h1>Serie tv</h1>
            <li v-for="serie in tvSeries" :key="serie.id">
                <img :src="urlImage(serie.poster_path)" :alt="serie.title">
                {{serie.name}} - 
                {{serie.original_name}} - 
                <flag :iso="languageIso(serie.original_language)"/> - 
                <span class="star" v-html="starsVote(serie.vote_average)"></span>
            </li>
        </ul>
    </section>
</template>

<script>

    export default {
        name: 'MoviesSection',
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
            },
            starsVote(vote) {
                let htmlFullStars = '';
                let htmlEmptyStars = '';
                for (let i = 0; i < Math.ceil(vote / 2); i++) {
                    htmlFullStars += '<i class="fa-solid fa-star"></i>';
                }
                for (let i = 0; i < (5 - Math.ceil(vote / 2)); i++) {
                    htmlEmptyStars += '<i class="fa-regular fa-star"></i>';
                }
                return `${htmlFullStars}${htmlEmptyStars}`;
            }
        }
    }
</script>

<style lang="scss" scoped>
    .star {
        color: #fdcc0d;
    }
</style>