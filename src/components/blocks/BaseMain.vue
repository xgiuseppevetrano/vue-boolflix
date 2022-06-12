<template>
    <main>
        <div class="container">
            <BaseSection/>
        </div>
    </main>
</template>

<script>
    import BaseSection from "../sections/BaseSection.vue";

    export default {
        name: 'BaseMain',
        components: {
            BaseSection,
        }
    }
</script>

<style lang="scss" scoped>
    main {
        background-color: rgba(var(--primary-color), 0.98);
        min-height: calc(100vh - 6.25rem);

        .main__title {
            text-transform: uppercase;
        }
    }
</style>