<template>
    <section>
        <div class="container">
            <div class="row">
                <BaseCard class="col-12 col-sm-6 col-lg-3 mb-3" v-for="film in Shared.films" :key="film.id" :arr="Shared.films"/>
                <BaseCard class="col-12 col-sm-6 col-lg-3 mb-3" v-for="tvSerie in Shared.tvSeries" :key="tvSerie.id" :arr="Shared.tvSeries"/>
            </div>
        </div>
    </section>
</template>

<script>
    import BaseCard from '../commons/BaseCard.vue';
    import Shared from "../../shared/Shared";

    export default {
        components: {
            BaseCard
        },
        name: 'BaseSection',
        data() {
            return {
                Shared
            }
        },
    }
</script>

<style lang="scss" scoped>

</style>