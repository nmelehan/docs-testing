<template>
    <span><i v-bind:class="getClass()"></i></span>
</template>

<script>
export default {
    name: "star",
    data: function () {
        return {
            hover: false,
            active: false,
        };
    },
    props: ["weight", "enabled", "currentrating"],
    methods: {
        getClass: function () {
            var baseClass = "icon-star";

            return baseClass;
        },
    },
};
</script>

<style scoped>
p {
    font-size: 2em;
    text-align: center;
}
</style>
