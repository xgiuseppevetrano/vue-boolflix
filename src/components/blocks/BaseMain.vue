<template>
    <main>
        <div class="container">
            <FilmSection :films="SharedFilms.films" :tvSeries="SharedFilms.tvSeries"/>
        </div>
    </main>
</template>

<script>
    import FilmSection from "../sections/FilmSection.vue";
    import SharedFilms from "../../shared/SharedFilms";

    export default {
        name: 'BaseMain',
        data() {
            return {
                SharedFilms
            }
        },
        components: {
            FilmSection,
        }
    }
</script>

<style lang="scss" scoped>

</style>