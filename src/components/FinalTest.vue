<template>
    <div id="final-test">
        <img @click="backToPage" id="arrow" src="../assets/media/back-arrow.svg" alt="back">
        <div class="title">{{ title }}</div>
        <select-multiple :questionNum="0"></select-multiple>
        <sortable-list :questionNum="2"></sortable-list>

    </div>
</template>

<script>
import json from "../../text.json";
import SelectMultiple from "@/components/SelectMultiple";
import SortableList from "@/components/SortableList";

export default {
    name: "final-test",
    props: ["pageNum", "contentNum"],
    components: {
        SelectMultiple,
        SortableList
    },
    methods: {
        backToPage() {
            this.$emit('close-page');
        }
    },
    computed: {
        title() {
            return json.info[this.pageNum][this.contentNum].title;
        }
    }
}
</script>

<style scoped>
#final-test {
    margin: 0%;
        height: 100%;
        width: 100vw;
        position: absolute;
        top: 0;
        right: 0;
}
.title {
    color: #f6f0e6;
        margin-right: 2%;
        font-size: 15vw;
        font-family: "aduma";
        font-weight: bold;
        margin-top: 0%;
}
#arrow {
        position: fixed;
        top: 0%;
        right: 1%;
        z-index: 3;
        max-width: 100%;
        height: 10vh;
        background-color: #001d3d;
    }
</style>