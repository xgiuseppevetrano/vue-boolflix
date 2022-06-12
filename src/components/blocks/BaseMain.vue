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
        background-color: var(--primary-color);
        height: var(--main-height);
        overflow-y: auto;

        &::-webkit-scrollbar {
            width: .5rem;
        }
        
        &::-webkit-scrollbar-track {
            border-radius: .625rem;
        }
            
        &::-webkit-scrollbar-thumb {
            background: lightgray; 
            border-radius: .625rem;
        }

        &::-webkit-scrollbar-thumb:hover {
            background: gray;
        }

        .main__title {
            text-transform: uppercase;
        }
    }
</style>