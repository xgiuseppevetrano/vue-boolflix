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
        SearchBarSection
    }
}
</script>

<style lang="scss" scoped>

</style>