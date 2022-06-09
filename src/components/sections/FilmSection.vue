<template>
    <section class="films">
        <ul>
            <li class="films__list" v-for="film in SharedFilms.films" :key="film.id">{{film.title}} - {{film.original_title}} - {{film.original_language}} - {{film.vote_average}}</li>
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
    }
</script>

<style lang="scss" scoped>
    .films {
        
        &__list {
            color: var(--primary-color-text);
            margin-bottom: .3125rem;
        }
    }
</style>