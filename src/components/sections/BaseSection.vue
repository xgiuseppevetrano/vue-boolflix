<template>
    <section>
        <div class="container">
            <div class="row">
                <BaseCard class="col" v-for="film in Shared.films" :key="film.id" :card="film"/>
                <BaseCard class="col" v-for="tvSerie in Shared.tvSeries" :key="tvSerie.id" :card="tvSerie"/>
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
    .row {
        display: flex;
        flex-wrap: wrap;

        .col {
            width: calc(100% / 6 - 1.875rem);
            margin: .9375rem;

            @media screen and (max-width: 75rem) {
                & {
                    width: calc(100% / 5 - 1.875rem);
                }
            }

            @media screen and (max-width: 62rem) {
                & {
                    width: calc(100% / 4 - 1.875rem);
                }
            }

            @media screen and (max-width: 48rem) {
                & {
                    width: calc(100% / 3 - 1.875rem);
                }
            }

            @media screen and (max-width: 36rem) {
                & {
                    width: calc(100% / 2 - 1.875rem);
                }
            }

            @media screen and (max-width: 25rem) {
                & {
                    width: calc(100% - 1.875rem);
                }
            }
        }
    }
</style>