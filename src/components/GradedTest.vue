<template>
    <div id="graded-test">
        <div id="main-title">{{ mainTitle }}</div>
        <div id="sub-title">{{ title }}</div>
        <select-multiple-grade :questionNum="1" @points-updated="selectMultiple"></select-multiple-grade>
        <match-table-grade :questionNum="2" @points-updated="matchTable"></match-table-grade>
        <multiple-choice-grade :questionNum="1" @points-updated="multipleChoice"></multiple-choice-grade>
        <sortable-list-grade :questionNum="3"@points-updated="sortableList"></sortable-list-grade>
        <draw-lines-grade :questionNum="1" @points-updated="drawLines"></draw-lines-grade>
        <true-false-grade :questionNum="1" @points-updated="trueOrfalse"></true-false-grade>
        <multiple-choice-grade :questionNum="2" @points-updated="multipleChoice2"></multiple-choice-grade>
        <div id="button" @click="nextPage">הגש</div>
    </div>
</template>

<script>
import SortableListGrade from "@/components/SortableListGrade";
import MatchTableGrade from "@/components/MatchTableGrade";
import DrawLinesGrade from "@/components/DrawLinesGrade";
import MultipleChoiceGrade from "@/components/MultipleChoiceGrade";
import SelectMultipleGrade from "@/components/SelectMultipleGrade";
import TrueFalseGrade from "@/components/TrueFalseGrade";
import json from "../../text.json";
export default {
    name: "graded-test",
    props: ["pageNum", "contentNum"],
    components: {
        SortableListGrade,
        MatchTableGrade,
        DrawLinesGrade,
        MultipleChoiceGrade,
        SelectMultipleGrade,
        TrueFalseGrade
    },
    data() {
        return {
            selectMultiplePoints: 0,
            matchTablePoints: 0,
            multipleChoicePoints: 0,
            sortableListPoints: 0,
            drawLinesPoints: 0,
            trueOrfalsePoints: 0,
            finalGrade: 0,
            multipleChoicePoints2: 0
        }
    },
    methods: {
        nextPage() {
            this.finalGrade = this.selectMultiplePoints +  this.matchTablePoints +  this.multipleChoicePoints +  this.sortableListPoints
            + this.drawLinesPoints + this.trueOrfalsePoints + this.multipleChoicePoints2;
            this.$emit('next-page', this.finalGrade);
            console.log(this.finalGrade);
        },
        selectMultiple(points){
            this.selectMultiplePoints=points;
        },
        matchTable(points){
            this.matchTablePoints = points;
        },
        multipleChoice(points){
            this.multipleChoicePoints = points;
        },
        sortableList(points) {
            this.sortableListPoints = points;
        },
        drawLines(points){
            this.drawLinesPoints = points;
        },
        trueOrfalse(points){
            this.trueOrfalsePoints = points;
        },
        multipleChoice2(points){
            this.multipleChoicePoints2 = points;
        }

    },
    computed: {
        title() { 
            return json.finalGradeTest[0].title;
        },
        mainTitle() {
            return json.finalGradeTest[0].mainTitle;
        }
        
    }
}
</script>

<style scoped>
    #graded-test {
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

    /* button {
        outline: none;
        cursor: pointer;
        border: none;
        padding: 0.9rem 2rem;
        margin: 0;
        margin-bottom: 30%;
        font-family: "aduma";
        font-size: 7vw;
        position: relative;
        display: inline-block;
        font-weight: bold;
        border-radius: 4vh;
        overflow: hidden;
        background: #001d3d;
        color: #001d3d;
        box-shadow: rgba(0, 0, 0, 0.35) 0px 5vw 15vw;
    }

    button span {
        font-family: "aduma";
        position: relative;
        z-index: 10;
        transition: color 0.4s;
    }

    button:hover span {
        color: #ffc300;
    }

    button::before,
    button::after {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        z-index: 0;
    }

    button::before {
        content: "";
        background: #ffc300;
        width: 120%;
        left: -10%;
        transform: skew(30deg);
        transition: transform 0.4s cubic-bezier(0.3, 1, 0.8, 1);
    }

    button:hover::before {
        transform: translate3d(100%, 0, 0);
    } */
    #button {
        background-color: #ffc300;
        color: #001d3d;
        font-family: "aduma";
        position: relative;
        margin: auto;
        margin-bottom: 8%;
        margin-top: 6%;
        width: 25vw;
        text-align: center;
        border: none;
        padding: 2%;
        font-size: 7.5vw;
        font-weight: bold;
        border-radius: 2vw;
        box-shadow: rgba(0, 0, 0, 0.25) 0px 54px 55px, rgba(0, 0, 0, 0.12) 0px -12px 30px, rgba(0, 0, 0, 0.12) 0px 4px 6px, rgba(0, 0, 0, 0.17) 0px 12px 13px, rgba(0, 0, 0, 0.09) 0px -3px 5px;;
    }


</style>
