<template>
    <header>
        <div class="container">
            <SearchBarSection/>
        </div>
    </header>
</template>

<script>
    import SearchBarSection from '../sections/SearchBarSection.vue'

    export default {
        name: 'BaseHeader',
        components: {
            SearchBarSection,
        }
    }
</script>

<style lang="scss" scoped>
    header {
        height: var(--header-height);
        background-color: var(--primary-color);
        display: flex;
        align-items: center;
    }
</style>