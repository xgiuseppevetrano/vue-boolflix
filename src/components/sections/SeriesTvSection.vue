<template>
    <section class="tv-series">
        <ul>
            <li class="tv-series__list" v-for="serie in SharedFilms.tvSeries" :key="serie.id">
                {{serie.name}} - 
                {{serie.original_name}} - 
                <flag :iso="LanguageIso(serie.original_language)"/> - 
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
                SharedFilms,
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

</style>