<template>
    <div id="second-test">
        <img @click="backToPage" id="arrow" src="../assets/media/back-arrow.svg" alt="back">
        <div id="main-title">{{ mainTitle }}</div>
        <div id="sub-title">{{ title }}</div>
        <sortable-list :questionNum="1"></sortable-list>
        <multiple-choice :questionNum="0"></multiple-choice>
        <match-table :questionNum="1"></match-table>

        <!-- <advantage-table :questionNum="0"></advantage-table> -->
    </div>
</template>

<script>
import json from "../../text.json";
import SortableList from "@/components/SortableList";
import MultipleChoice from "@/components/MultipleChoice";
import MatchTable from "@/components/MatchTable";

export default {
    name: "second-test",
    props: ["pageNum", "contentNum"],
    components: {
        SortableList,
        MultipleChoice,
        MatchTable
    },
    computed: {
        title() { 
            return json.info[this.pageNum][this.contentNum].title;
        },
        mainTitle() {
            return json.info[this.pageNum][this.contentNum].mainTitle;
        }
    },
    methods: {
        backToPage() {
            this.$emit('close-page');
        }
    }
}
</script>

<style scoped>
    #second-test {
        margin: 0%;
            height: 100%;
            width: 100vw;
            position: absolute;
            top: 0;
            right: 0;
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
    #main-title {
        color: #f6f0e6;
        margin-right: 2%;
        font-family: "aduma";
        font-size: 8vw;
        margin-top: 25%;
    }
    #sub-title {
        color: #f6f0e6;
        margin-right: 2%;
        font-size: 15vw;
        font-family: "aduma";
        font-weight: bold;
        margin-top: 0%;
    }
</style>