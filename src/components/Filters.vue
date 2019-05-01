<template>
    <form>
        <div>
            <p>Categories</p>
            <select v-model="Categories">
                <option :value="null">All</option>
                <option v-for="option in CategoriesOptions" :value="option.id">{{ option.name }}</option>
            </select>
        </div>

        <div>
            <p>Image type</p>
            <select v-model="ImageType">
                <option value="jpg,png,gif">All</option>
                <option value="jpg,png">Static</option>
                <option value="gif">Animated</option>
            </select>
        </div>

        <div>
            <p>Breed</p>
            <select v-model="Breed">
                <option :value="null">All</option>
                <option v-for="option in BreedOptions" :value="option.id">{{ option.name }}</option>
            </select>
        </div>
    </form>
</template>

<script>
    import $ from 'jquery'

    export default {
        name: "Filters",
        created: function () {

            const urlCategories = 'https://api.thecatapi.com/v1/categories';
            const urlBreeds = 'https://api.thecatapi.com/v1/breeds';
            const apiK = '6dd98ac3-a5c0-44ce-bb23-1f816ddbb071';

            $.ajax(urlCategories, {
                method: 'GET',
                headers: {
                    'x-api-key': apiK
                }
            })
                .done((response) => {
                    this.CategoriesOptions = response;
                });

            $.ajax(urlBreeds, {
                method: 'GET',
                headers: {
                    'x-api-key': apiK
                }
            })
                .done((response) => {
                    this.BreedOptions = response;
                });
        },
        data: function () {
            let default_ = null;
            return {
                Categories: default_,
                ImageType: 'jpg,png,gif',
                Breed: default_,
                CategoriesOptions: [],
                BreedOptions: [],
            }
        },
        computed: {
            filterOptions: function () {
                return {Categories: this.Categories, ImageType: this.ImageType, Breed: this.Breed};
            }
        },
        watch: {
            filterOptions: function (value) {
                EventBus.$emit('Filters:Options', value);
            }
        }
    };
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
    form {
        display: flex;
        justify-content: space-evenly;
        margin: auto;
        width: 100%;
        padding: 1rem 0;
        height: 57px;
    }
    select {
        border: none;
        border-bottom: 1px solid black;
        outline: none;
        margin: .6rem 0;
    }
</style>
