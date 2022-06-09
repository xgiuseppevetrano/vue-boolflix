<template>
    <main>
        <div class="container">
            <FilmSection/>
        </div>
    </main>
</template>

<script>
    import FilmSection from "../sections/FilmSection.vue";

    export default {
        name: 'BaseMain',
        components: {
            FilmSection
        }
    }
</script>

<style lang="scss" scoped>
    main {
        background-color: var(--secondary-color);
    }
</style>