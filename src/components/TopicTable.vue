<template>
<div id="table">
    <img @click="closePage" id="arrow" src="../assets/media/back-arrow.svg" alt="back">
    <div id="main-title">טכניקות יציאה ממרחב עמדות</div>
    <div id="sub-title">שיטות</div>
    <div class="card">
        <div class="card-title">{{ cardTitle }}</div>
        <div class="card-text">{{ text }}</div>
    </div>
    <content-handler :contentNum="topicNum+3" @next-page="closePage"></content-handler>


</div>
</template>

<script>
import json from "../../text.json";
import ContentHandler from "@/components/ContentHandler";
export default {
    name: "topic-table", 
    props: ["pageNum", "contentNum","topicNum"],
    components: {
        ContentHandler
    },
    computed: {
        text(){
            return json.info[this.pageNum][this.contentNum][`text${this.topicNum}`]
        },
        cardTitle() {
            return json.info[this.pageNum][this.contentNum][`subTitle${this.topicNum}`];
        }
    },
    methods: {
        closePage() {
            this.$emit('close-page');
        }
    }
}
</script>

<style scoped>
    #table {
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
    .card {
        margin: auto;
        width: 84vw;
        border-radius: 1.5vh;
        color: #001d3d;
        background-color: #ffc300;
        margin-top: 10%;
        padding: 3%;
        border: none;
        box-shadow: rgba(0, 0, 0, 0.632) 0px 4vw 8vw 0vh;
    }
    .card-title {
        background-color: #fce9a9;
        padding-right: 1%;
        font-family: "aduma";
        margin: -3%;
        margin-bottom: 4%;
        font-size: 9vw;
        font-weight: 550;
    }

    .card-text {
        font-size: 5.5vw;
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