<template>
    <div id="unconsecutive">
        <img @click="backToPage" id="arrow" src="../assets/media/back-arrow.svg" alt="back">
        <div class="title">{{ title }}</div>
        <div class="text">
            <div class="line" v-for="(line, index) in text" :key='index' >{{ line }}</div>
        </div>
        <content-handler :contentNum="7" @next-page="backToPage"></content-handler>
    </div>
</template>

<script>
import json from "../../text.json";
import ContentHandler from "@/components/ContentHandler";
export default {
    name: "unconsecutive",
    props: ["pageNum", "contentNum"],
    components: {
        ContentHandler
    },
    computed: {
        title() {
            return json.info[this.pageNum][this.contentNum].title;
        },
        text() {
            return json.info[this.pageNum][this.contentNum].text;
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
    #unconsecutive {
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
    .title {
        text-align: center;
        width: 90vw;
        margin: auto;
        color: #ffc300;
        margin-top: 30%;
        font-family: "aduma";
        font-size: 12vw;
        font-weight: bold;
    }
    .text {
        margin: auto;
        margin-top: -5%;
        padding: 5%;
        padding-top: 8%;
        width: 80vw;
        border-radius: 3vh;
        border: #ffc300 solid 1.2vw;
        border-top: none;    
        box-shadow: rgb(255, 195, 0, 0.3) 0px 6vh 7vh 1vh, rgba(139, 107, 0, 0.4) 0px 1.5vh 3vh -1.5vh
    }
    .line {
        color: #f6f0e6;
        font-size: 5.5vw;
        margin-top: 8%;
    }
</style>