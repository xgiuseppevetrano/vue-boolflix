<template>
    <header>
        <div class="container">
            <div class="header">
                <LogoSection/>
                <SearchBarSection/>
            </div>
        </div>
    </header>
</template>

<script>
    import LogoSection from '../sections/LogoSection.vue'
    import SearchBarSection from '../sections/SearchBarSection.vue'

    export default {
        name: 'BaseHeader',
        components: {
            LogoSection,
            SearchBarSection,
        }
    }
</script>

<style lang="scss" scoped>
    @import '../../assets/style/mixins.scss';

    header {
        background-color: var(--primary-color);
        height: var(--header-height);

        .header {
            @include dflex(space-between);
        }
    }
</style>