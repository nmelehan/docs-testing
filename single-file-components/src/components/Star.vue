<template>
    <i
        v-bind:class="getClass()"
        v-on:mouseover="mouseoverHandler"
        v-on:mouseleave="mouseleaveHandler"
        v-on:click="clickHandler"
    ></i>
</template>

<script>
import { eventBus } from "../main";

export default {
    name: "Star",
    data: function () {
        return {
            hover: false,
            active: false,
        };
    },
    props: ["weight", "enabled"],
    methods: {
        getClass: function () {
            var baseClass = "icon-star";
            if (this.active) {
                baseClass += " active";
            }
            if (this.hover) {
                baseClass += " hover";
            }
            return baseClass;
        },
        mouseoverHandler: function () {
            // Makes sure stars are not lighting up after vote is cast
            if (this.enabled) {
                // Emits the lightUp event with the weight as a parameter
                eventBus.$emit("lightUp", this.weight);
            }
        },
        mouseleaveHandler: function () {
            // Makes sure stars are not lighting up after vote is cast
            if (this.enabled) {
                // Emits the lightDown event
                eventBus.$emit("lightDown");
            }
        },
        clickHandler: function () {
            // Makes sure you only vote if you haven't voted yet
            if (this.enabled) {
                // Emits the rate event with the weight as parameter
                eventBus.$emit("rate", this.weight);
            } else {
                alert("Already voted");
            }
        },
    },
    created: function () {
        eventBus.$on("lightUp", (targetWeight) => {
            if (targetWeight >= this.weight) {
                this.hover = true;
            } else {
                this.hover = false;
            }
        });
        eventBus.$on("lightDown", () => {
            this.hover = false;
        });
        eventBus.$on("rate", (targetWeight) => {
            if (targetWeight >= this.weight) {
                this.active = true;
            }
        });
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
i.icon-star.active {
    color: #737373;
}
</style>
