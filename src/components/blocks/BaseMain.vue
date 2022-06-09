<template>
    <main>
        <div class="container">
            <FilmSection/>
            <SeriesTvSection/>
        </div>
    </main>
</template>

<script>
    import FilmSection from "../sections/FilmSection.vue";
    import SeriesTvSection from '../sections/SeriesTvSection.vue'

    export default {
        name: 'BaseMain',
        components: {
            FilmSection,
            SeriesTvSection
        }
    }
</script>

<style lang="scss" scoped>

</style>