<template>
    <div id="covering">
        <img @click="backToPage" id="arrow" src="../assets/media/back-arrow.svg" alt="back">
        <div class="title">{{ title }}</div>
        <div class="text">
            <div class="line" v-for="(line, index) in text" :key='index' >{{ line }}</div>
        </div>
        <div id="subtitle">{{ subtitle }}</div>
        <div id="explenation">{{ explenation }}</div>
        <div class="card">
            <div class="card-title">{{ cardTitle1 }}</div>
            <div class="card-text">{{ text1 }}</div>
        </div>
        <div class="card">
            <div class="card-title">{{ cardTitle2 }}</div>
            <div class="card-text">{{ text2 }}</div>
        </div>
        <div id="button" @click="backToPage">סיימתיייי</div>
    </div>
</template>

<script>
import json from "../../text.json";
export default {
    name: "covering",
    props: ["pageNum", "contentNum"],
    computed: {
        title() {
            return json.info[this.pageNum][this.contentNum].title;
        },
        text() {
            return json.info[this.pageNum][this.contentNum].text;
        },
        cardTitle1() {
            return json.info[this.pageNum][this.contentNum].cardTitle1;
        },
        text1() {
            return json.info[this.pageNum][this.contentNum].text1;
        },
        cardTitle2() {
            return json.info[this.pageNum][this.contentNum].cardTitle2;
        },
        text2() {
            return json.info[this.pageNum][this.contentNum].text2;
        },
        subtitle() {
            return json.info[this.pageNum][this.contentNum].subtitle;
        },
        explenation() {
            return json.info[this.pageNum][this.contentNum].explenation;
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
    #covering {
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
    #subtitle {
        font-family: "aduma";
        margin-top: 12%;
        margin-right: 2%;
        color: #f6f0e6;
        font-weight: 580;
        font-size: 9.5vw;
    }
    #explenation {
        margin-top: 1%;
        width: 94vw;
        margin-bottom: 6%;
        margin-right: 2%;
        color: #f6f0e6;
        font-weight: 580;
        font-size: 5.5vw;
        white-space: break-spaces;
    }
    .card {
        margin: auto;
        width: 84vw;
        border-radius: 1.2vh;
        color: #001d3d;
        background-color: #ffc300;
        margin-top: 6%;
        padding: 3%;
        border: none;
        white-space: break-spaces;
        box-shadow: rgba(0, 0, 0, 0.632) 0px 4vw 8vw 0vh;
    }
    .card-title {
        background-color: #fce9a9;
        padding-right: 1%;
        font-family: "aduma";
        margin: -3%;
        margin-bottom: 4%;
        font-size: 8vw;
        font-weight: 550;
    }

    .card-text {
        font-size: 5.5vw;
    }
    #button{
        background-color: #ffc300;
        color: #001d3d;
        font-family: "aduma";
        position: relative;
        margin-right: 5%;
        margin-top: 6%;
        margin-bottom: 3%;
        width: 30vw;
        text-align: center;
        border: none;
        padding: 2%;
        font-size: 7.5vw;
        font-weight: 550;
        border-radius: 3vw;
        -webkit-box-shadow: rgba(0, 0, 0, 0.25) 0px 54px 55px, rgba(0, 0, 0, 0.12) 0px -12px 30px, rgba(0, 0, 0, 0.12) 0px 4px 6px, rgba(0, 0, 0, 0.17) 0px 12px 13px, rgba(0, 0, 0, 0.09) 0px -3px 5px;
        box-shadow: rgba(0, 0, 0, 0.25) 0px 54px 55px, rgba(0, 0, 0, 0.12) 0px -12px 30px, rgba(0, 0, 0, 0.12) 0px 4px 6px, rgba(0, 0, 0, 0.17) 0px 12px 13px, rgba(0, 0, 0, 0.09) 0px -3px 5px;
    }
</style>