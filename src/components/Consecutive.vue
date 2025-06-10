<template>
    <div id="consecutive">
        <img @click="backToPage" id="arrow" src="../assets/media/back-arrow.svg" alt="back">
        <div class="title">{{ title }}</div>
        <div id="info">{{ info }}</div>
        <div id="subtitle">{{ subtitle }}</div>
        <div v-for="(subTitle, index) in subtitles" :key="index" class="big-container">
            <div class="subTitle">{{ subTitle }}</div>
            <div class="container">
                <div class="explenation">{{ txt[index] }}</div>
                <img :src="imgs[index]" alt="pic"  class="pic">
            </div>
        </div>
        <div id="button" @click="backToPage">וואלה קליל</div>
    </div>
</template>

<script>
import json from "../../text.json";
export default {
    name: "consecutive",
    props: ["pageNum", "contentNum"],
    data() {
        return {

        }
    },
    computed: {
        title() {
            return json.info[this.pageNum][this.contentNum].title;
        },
        info() {
            return json.info[this.pageNum][this.contentNum].info;
        },
        subtitle() {
            return json.info[this.pageNum][this.contentNum].subtitle;
        },
        subtitles() {
            return json.info[this.pageNum][this.contentNum].subtitles;
        },
        txt() {
            return json.info[this.pageNum][this.contentNum].txt;
        },
        imgs() {
            return json.info[this.pageNum][this.contentNum].imgs.map(img => require(`@/assets/media/${img}`));
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
    #consecutive {
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
        color: #f6f0e6;
        margin-right: 2%;
        font-size: 15vw;
        font-family: "aduma";
        font-weight: bold;
        margin-top: 25%;
    }
    #info {
        width: 92%;
        margin-right: 2%;
        margin-top: 2%;
        color: #f6f0e6;
        font-size: 6vw;
    }
    #subtitle {
        font-family: "aduma";
        margin-top: 12%;
        margin-right: 2%;
        color: #f6f0e6;
        font-weight: 580;
        font-size: 9.5vw;
    }
    .big-container {
        color: #f6f0e6;
        margin-top: 6%;
    }
    /* .big-container {
        color: #f6f0e6;

        margin-top: 6%;
        width: 98vw;
        border-top-left-radius: 2vh;
        border-bottom-left-radius: 2vh;
        border-left: 1vw solid #ffc300;
        border-top: 1vw solid #ffc300;
        border-bottom: 1vw solid #ffc300;
        padding-top: 1%;
        padding-bottom: 1%;
    } */
    .subTitle {
        font-family: "aduma";
        margin-right: 2%;
        font-weight: 580;
        font-size: 7vw;
    }
    .explenation {
        margin-right: 2%;
        font-weight: 580;
        width: 43vw;
        font-size: 4.5vw;
        margin-left: 2%;
    }
    .container {
        display: flex;
        flex-direction: row;
        flex-wrap: nowrap;
        align-items: start;
        /* justify-content: center; */
    }
    .pic{
        display: block;
        max-height: 100%;
        width: 50vw;
    }
    #button{
        background-color: #ffc300;
        color: #001d3d;
        font-family: "aduma";
        position: relative;
        margin: auto;
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