<template>
    <i
        v-bind:class="getClass()"
        v-on:mouseover="mouseoverHandler"
        v-on:mouseleave="mouseleaveHandler"
        v-on:click="clickHandler"
    ></i>
</template>

<script>
export default {
    name: "Star",
    data: function () {
        return {
            hover: false,
        };
    },
    props: ["weight", "enabled", "currentRating"],
    methods: {
        getClass: function () {
            var baseClass = "icon-star";

            // Adds the hover class if you're hovering over the component or you are hovering over a star with greater weight
            if (this.hover || this.currentRating >= this.weight) {
                baseClass += " hover";
            }
            return baseClass;
        },
        mouseoverHandler: function () {
            // Makes sure stars are not lighting up after vote is cast
            if (this.enabled) {
                // Emits the lightup event with the weight as a parameter
                this.$emit("lightUp", this.weight);
                // Enables hover class
                this.hover = true;
            }
        },
        mouseleaveHandler: function () {
            // Makes sure stars are not lighting up after vote is cast
            if (this.enabled) {
                // Emits the lightDown event
                this.$emit("lightDown", this.weight);
                // Removes hover class
                this.hover = false;
            }
        },
        clickHandler: function () {
            // Makes sure you only vote if you haven't voted yet
            if (this.enabled) {
                // Emits the rate event with the weight as parameter
                this.$emit("rate", this.weight);
            } else {
                alert("Already voted");
            }
        },
    },
};
</script>

<style scoped>
i.icon-star {
    font-size: 20px;
    color: #e3e3e3;
    margin-bottom: 0.5em;
}
i.icon-star.hover {
    color: yellow;
}
</style>
