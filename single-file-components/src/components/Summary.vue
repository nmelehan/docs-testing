<template>
    <div class="summaryContainer">
        <ul>
            <li v-for="rating in ratings" v-bind:key="rating.weight">
                {{ rating.weight }}<i class="icon-star"></i>: {{ rating.votes }}
            </li>
        </ul>
    </div>
</template>

<script>
export default {
    name: "sum",
    data: function () {
        return {
            greeting: "Hello",
        };
    },
    props: ["ratings"],
    methods: {},
    created: function () {},
};
</script>

<style scoped></style>
