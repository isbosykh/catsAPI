<template>
    <div>
        <Filters/>
        <Elements/>
    </div>
</template>

<script>
    import Elements from "../components/Elements";
    import Filters from "../components/Filters";

    export default {
        name: "Main",
        components: {
            Elements,
            Filters
        }
    };
</script>

<style lang="scss" scoped>
    div {
        max-width: 800px;
        margin: 0 auto;
    }
</style>