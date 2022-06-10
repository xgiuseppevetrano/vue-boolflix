<template>
    <main>
        <div class="container">
            <MoviesSection :films="SharedFilms.films" :tvSeries="SharedFilms.tvSeries"/>
        </div>
    </main>
</template>

<script>
    import MoviesSection from "../sections/MoviesSection.vue";
    import SharedFilms from "../../shared/SharedFilms";

    export default {
        name: 'BaseMain',
        data() {
            return {
                SharedFilms
            }
        },
        components: {
            MoviesSection,
        }
    }
</script>

<style lang="scss" scoped>

</style>