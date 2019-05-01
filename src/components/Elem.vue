<template>
    <div class="ElemWrapper">
        <router-link :to="'/item/' + item.id" class="Elem">
            <div :style="{ backgroundImage: 'url('+ item.url +')' }"></div>
        </router-link>
    </div>


</template>

<script>
    export default {
        name: "Elem",
        props: {
            item: Object,
        },
    }
</script>

<style lang="scss" scoped>
    .ElemWrapper {
        width: 33.3333333333%;
        padding: 2em;
        box-sizing: border-box;
    }
    .Elem {
        background: aliceblue;
        position: relative;
        display: block;
        &:before {
            display: block;
            content: '';
            padding-top: 100%;
        }
        div {
            position: absolute;
            top:0; left: 0;right: 0;bottom: 0;
            margin: auto;
            background-position: center;
            background-size: cover;
        }
    }
</style>