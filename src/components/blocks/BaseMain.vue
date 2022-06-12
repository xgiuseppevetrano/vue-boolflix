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
    }
</style>