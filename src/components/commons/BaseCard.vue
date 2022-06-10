<template>
    <div class="card">
        <img :src="urlImage(card.poster_path)">
        <span>{{card.title || card.name}}</span>
        <span>{{card.original_title || card.original_name}}</span>
        <flag :iso="languageIso(card.original_language)"/>
        <span class="star" v-html="starsVote(card.vote_average)"></span>
    </div>
</template>

<script>
export default {
    name: 'BaseCard',
    props: {
        card: Object,
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
    },
    created() {
        console.log(this.card);
    }
}
</script>

<style lang="scss" scoped>
    .star {
        color: #fdcc0d;
    }
</style>