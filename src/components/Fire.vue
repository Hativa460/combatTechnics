<template>
    <div id="fire">
        <div id="main-title">טכניקות לחימה ממרחב עמדות</div>
        <div id="sub-title">{{ title }}</div>
        <div id="text">{{ explenation }}</div>
        <div class="card">
            <div class="card-title">{{ cardTitle1 }}</div>
            <div class="card-text">{{ text1 }}</div>
        </div>
        <div class="card">
            <div class="card-title">{{ cardTitle2 }}</div>
            <div class="card-text">{{ text2 }}</div>
        </div>
        <div id="subtitle2">שלבי ניהול האש ופעולות המ"מ</div>
        <content-handler :contentNum="2" @next-page="nextPage"></content-handler>
    </div>
</template>

<script>
import ContentHandler from "@/components/ContentHandler";
import json from "../../text.json";
export default {
    name: "fire",
    components:
    {
        ContentHandler
    },
    props: ["pageNum", "contentNum"],
    data() {
        return {
            loopCount: 2
        }
    },
    methods: {
        nextPage() {
            this.$emit('back-to-menu');
        }
    },
    computed: {
        title() { 
            return json.info[this.pageNum][this.contentNum-1].title;
        },
        explenation(){
            return json.info[this.pageNum][this.contentNum-1].explenation;
        },
        cardTitle1() {
            return json.info[this.pageNum][this.contentNum-1].subTitle0;
        },
        cardTitle2() {
            return json.info[this.pageNum][this.contentNum-1].subTitle1;
        },
        text1() {
            return json.info[this.pageNum][this.contentNum-1].text0;
        }, 
        text2() {
            return json.info[this.pageNum][this.contentNum-1].text1;
        }
    }
}

</script>

<style scoped>
    #fire {
        margin: 0%;
        height: 100%;
        width: 100vw;
        position: absolute;
        top: 0;
        right: 0;
    }
    #text {
        width: 92%;
        margin-right: 2%;
        margin-top: 2%;
        margin-bottom: 10%;
        color: #f6f0e6;
        font-size: 6vw;
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
        width: 90vw;
        border-radius: 1.5vh;
        color: #001d3d;
        background-color: #ffc300;
        margin-top: 6%;
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

    #subtitle2 {
        font-family: "aduma";
        margin-top: 12%;
        margin-right: 2%;
        color: #f6f0e6;
        font-weight: bolder;
        font-size: 10vw;
    }

</style>