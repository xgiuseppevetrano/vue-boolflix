<template>
    <div class="card">
        <img :src="urlImage(arr.poster_path)">
        <span>{{arr.title || arr.name}}</span>
        <span>{{arr.original_title || arr.original_name}}</span>
        <flag :iso="languageIso(arr.original_language)"/>
        <span class="star" v-html="starsVote(arr.vote_average)"></span>
    </div>
</template>

<script>
export default {
    name: 'BaseCard',
    props: {
        arr: Array,
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
        },

    }
}
</script>

<style lang="scss" scoped>
    .star {
        color: #fdcc0d;
    }
</style>