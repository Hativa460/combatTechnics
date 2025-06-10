<template>
    <div id="test">
        <div id="main-title">{{ mainTitle }}</div>
        <div id="sub-title">{{ title }}</div>
        <sortable-list :questionNum="0"></sortable-list>
        <match-table :questionNum="pageNum-5"></match-table>
        <draw-lines :questionNum="pageNum-5"></draw-lines>
    </div>
</template>

<script>
import SortableList from "@/components/SortableList";
import MatchTable from "@/components/MatchTable";
import DrawLines from "@/components/DrawLines";
import json from "../../text.json";
export default {
    name: "test",
    props: ["pageNum", "contentNum"],
    components: {
        SortableList,
        MatchTable,
        DrawLines
    },
    data() {
        return {
            
        }
    },
    methods: {

    },
    computed: {
        title() { 
            return json.info[this.pageNum][this.contentNum-1].title;
        },
        mainTitle() {
            return json.info[this.pageNum][this.contentNum-1].mainTitle;
        }
    }
}
</script>

<style scoped>
    #test {
        margin: 0%;
        height: 100%;
        width: 100vw;
        position: absolute;
        top: 0;
        right: 0;
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