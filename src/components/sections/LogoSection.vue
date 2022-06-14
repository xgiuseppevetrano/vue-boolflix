<template>
  <section>
    <div class="logo">
        <img class="logo__img" src="https://upload.wikimedia.org/wikipedia/commons/7/7a/Logonetflix.png" alt="logo img">
        <BaseNav/>
    </div>
  </section>
</template>

<script>
import BaseNav from '../commons/BaseNav.vue'
export default {
    name: 'LogoSection',
    components: {
        BaseNav
    }
}
</script>

<style lang="scss" scoped>
    @import '../../assets/style/mixins.scss';
    
    .logo {
        @include dflex(flex-start);

        &__img {
            height: 2.5rem;
            vertical-align: middle;
            margin-right: 1.25rem;
        }
    }
</style>