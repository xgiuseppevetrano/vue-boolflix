<template>
    <div class="card">
        <img class="card__img" :src="urlImage(card.poster_path)" :alt="card.title || card.name">
        <div class="card__overlay">
            <div class="card__info">
                <h4 class="card__title"> {{card.title || card.name}}</h4>
            </div>
            <div class="card__description">
                <p>{{card.overview || 'No description'}}</p>
            </div>
            <div class="card__info-plus">
                <flag :iso="languageIso(card.original_language)"/>
                <span class="card__star" v-html="starsVote(card.vote_average)"></span>
            </div>
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
                return `https://via.placeholder.com/185x260?text=No image`
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
            flex-direction: column;
            position: absolute;
            right: 0;
            left: 0;
            bottom: 0;
            height: 60%;
            background-color: rgba(0, 0, 0, 0.8);
            color: white;
            font-size: .875rem;
            padding: .3125rem;
        }

        &__img {
            height: 100%;
            width: 100%;
        }

        &__info {
            text-align: center;
            padding-bottom: .3125rem;
        }

        &__description {
            flex-grow: 1;
            overflow-y: auto;

            &::-webkit-scrollbar {
                width: .375rem;
            }

            &::-webkit-scrollbar-track {
                border-radius: .625rem;
            }
                
            &::-webkit-scrollbar-thumb {
                background: lightgray; 
                border-radius: .625rem;
            }

            &::-webkit-scrollbar-thumb:hover {
                background: gray; 
            }
        }

        &__info-plus {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding-top: .3125rem;
        }

        &__star {
            color: #fdcc0d;
        }

        &:hover &__overlay {
            display: flex;
        }
    }
</style>