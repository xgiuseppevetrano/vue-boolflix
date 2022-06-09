<template>
    <section class="tv-series">
        <h3 class="tv-series__title">Tv Series</h3>
        <ul>
            <li class="tv-series__list" v-for="serie in SharedFilms.tvSeries" :key="serie.id">{{serie.name}} - {{serie.original_name}} - {{serie.original_language}} - {{serie.vote_average}}</li>
        </ul>
    </section>
</template>

<script>
    import SharedFilms from "../../shared/SharedFilms";

    export default {
        name: 'SeriesTvSection',
        data() {
            return {
                SharedFilms
            }
        },
    }
</script>

<style lang="scss" scoped>
    .tv-series {

        &__title {
            text-transform: uppercase;
            color: lightcoral;
            margin-bottom: .625rem;
        }
        
        &__list {
            color: var(--primary-color-text);
            margin-bottom: .3125rem;
            list-style-type: none;
        }
    }
</style>