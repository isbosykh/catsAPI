<template>
    <div class="container">
        <!--FIXME: flex is not working correctly without h1px-->
        <div style="height: 1px;"></div>
        <Elem v-for="item in items" :item="item"/>
        <infinite-loading :distance="0" :identifier="filterOptions" @infinite="infiniteHandler">
            <div slot="spinner" class="spinner">
                <h1>Hmm... (·.·)</h1>
            </div>
        </infinite-loading>
    </div>
</template>

<script>
    import InfiniteLoading from 'vue-infinite-loading';
    import Elem from './Elem';
    import $ from 'jquery';

    export default {
        name: "Elements",
        components: {
            Elem,
            InfiniteLoading
        },
        created: function() {
            EventBus.$on('Filters:Options', (payload) => {
                this.filterOptions = payload;
            });
        },
        mounted: function() {
            this.filterOptions = {}
        },
        data: function() {
            return {
                filterOptions: {
                    Breed: null,
                    Categories: null,
                    ImageType: null,
                },
                items: [],
            }
        },
        methods: {
            infiniteHandler($state) {
                const urlSearch = 'https://api.thecatapi.com/v1/images/search';
                const apiK = '6dd98ac3-a5c0-44ce-bb23-1f816ddbb071';

                console.log(1)

                $.ajax(urlSearch, {
                    method: 'GET',
                    headers: {
                        'x-api-key': apiK
                    },
                    data: {
                        limit: 25,
                        breed_id: this.filterOptions.Breed,
                        category_ids: this.filterOptions.Categories,
                        mime_types: this.filterOptions.ImageType,
                    },
                })
                    .done((response) => {
                        this.items = this.items.concat(response);
                        $state.loaded();
                    })
            }
        },
        watch: {
            filterOptions() {
                this.items = []
            }
        }
    }
</script>

<style lang="scss">
    .infinite-loading-container {
        width: 100%;
        height: 1px;
    }
    .spinner {
        font-family: 'Roboto Mono', monospace;
        margin: 2rem auto;
    }
</style>

<style lang="scss" scoped>
    @import url('https://fonts.googleapis.com/css?family=Roboto+Mono');

    .container {
        width: 100%;
        display: flex;
        justify-content: flex-start;
        align-content: flex-start;
        flex-wrap: wrap;
        border-top: 1px solid rgba(0,0,0,.2);
    }
    button {
        position: absolute;
        width: 100px;
        height: 100px;
    }
</style>