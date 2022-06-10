<template>
    <div class="card">
        <img class="card__img" :src="urlImage(card.poster_path)">
        <div class="card__overlay">
            <p class="card__title"><strong>Titolo:</strong> {{card.title || card.name}}</p>
            <p class="card__original-title"><strong>Titolo originale:</strong> {{card.original_title || card.original_name}}</p>
            <p class="card__description"><strong>Description:</strong> {{card.overview}}</p>
            <p class="card__language"><strong>Lingua:</strong> <flag :iso="languageIso(card.original_language)"/></p>
            <p class="card__stars"><strong>Voto:</strong> <span class="star" v-html="starsVote(card.vote_average)"></span></p>
        </div>
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
        }
    }
}
</script>

<style lang="scss" scoped>
    .card {
        position: relative;
        
        &__overlay {
            display: none;
            position: absolute;
            right: 0;
            left: 0;
            bottom: 0;
            height: 50%;
            background-color: rgba(0, 0, 0, 0.8);
            overflow-y: auto;
            color: white;
            font-size: .875rem;
        }

        &__img {
            height: 100%;
            width: 100%;
        }

        .star {
            color: #fdcc0d;
        }

        &:hover &__overlay {
            transition: 1s ease-in;
            display: block;
        }
    }
</style>