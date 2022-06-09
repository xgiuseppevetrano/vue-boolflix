<template>
    <section class="tv-series">
        <ul>
            <li class="tv-series__list" v-for="serie in SharedFilms.tvSeries" :key="serie.id">
                {{serie.name}} - 
                {{serie.original_name}} - 
                {{serie.original_language}} - 
                {{serie.vote_average}}
            </li>
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

</style>