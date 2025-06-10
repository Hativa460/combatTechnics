<template>
    <div id="operational">
        <div v-if="showMenu">
            <div class="title">{{ title }}</div>
            <div class="container">
                <div v-for="(subtitle, index) in subTitles" :key="index" class="topic-container animate__animated animate__slideInRight" :id="'topic'+(index)" @click="showTopic">
                    <div class="topic">{{ subtitle }}</div>
                </div>
            </div>
            <div id="btn" class="animate__animated animate__slideInLeft" @click="nextPage">זהו? כמה עוד?</div>
        </div>
        <div v-else>
            <consecutive v-if="topicNum===0" :contentNum="topicNum" :pageNum="9" @close-page="backHome"></consecutive>
            <unconsecutive v-if="topicNum===1" :contentNum="topicNum" :pageNum="9" @close-page="backHome"></unconsecutive>
            <danger-territory v-if="topicNum===2" :contentNum="topicNum" :pageNum="9" @close-page="backHome"></danger-territory>
            <covering v-if="topicNum===3" :contentNum="topicNum" :pageNum="9" @close-page="backHome"></covering>
            <final-test v-if="topicNum===4" :contentNum="topicNum" :pageNum="9" @close-page="backHome"></final-test>
        </div>
        
    </div>
</template>

<script>
import DangerTerritory from "@/components/DangerTerritory";
import Consecutive from "@/components/Consecutive";
import Unconsecutive from "@/components/Unconsecutive";
import Covering from "@/components/Covering";
import FinalTest from "@/components/FinalTest";

import json from "../../text.json";

export default {
    name: "operational",
    props:[],
    components: {
        DangerTerritory,
        Consecutive,
        Unconsecutive,
        Covering,
        FinalTest
    },
    data() {
        return {
            pageNum: 8,
            showMenu: true,
            topicNum: -1
        }
    },
    methods: {
        showTopic(event) {
            let nTopic = Number(event.currentTarget.id.charAt(5));
            this.topicNum = nTopic;
            this.showMenu= false;
        },
        backHome() {
            this.showMenu = true;
        },
        nextPage() {
            this.$emit('next-page');
            console.log("נמצא בעמוד 7 עובר לעמוד 8")
        }
    },
    computed: {
        title() { 
            return json.info[this.pageNum].title;
        },
        subTitles() {
            return json.info[this.pageNum].subTitles;
        }
    }
}
</script>

<style scoped>
    #operational {
        margin: 0%;
        height: 100%;
        width: 100vw;
        position: absolute;
        top: 0;
        right: 0;
    }
    .title {
        text-align: center;
        width: 100vw;
        margin: auto;
        color: #f6f0e6;
        margin-top: 30%;
        font-family: "aduma";
        font-size: 14vw;
        font-weight: bold;
    }
    .container {
        margin-top: 2%;
    }
    .topic-container {
        display: flex;
        flex-direction: row;
        flex-wrap: nowrap;
        align-items: center;
        justify-content: flex-start;
        color: #001d3d;
    }
    .topic {
        font-family: "aduma";
        font-size: 9vw;
        margin-left: 2%;
        margin-right: 0%;
        font-weight: 580;
        margin-bottom: 5%;
        margin-top: 5%;
        background-color: #ffc300;
        border-top-left-radius: 4vh;
        border-bottom-left-radius: 4vh;
        padding: 2%;
        padding-left: 4vw;
        box-shadow: rgba(0, 0, 0, 0.25) 0px 54px 55px, rgba(0, 0, 0, 0.12) 0px -12px 30px, rgba(0, 0, 0, 0.12) 0px 4px 6px, rgba(0, 0, 0, 0.17) 0px 12px 13px, rgba(0, 0, 0, 0.09) 0px -3px 5px;
    }
    #btn {
        position: absolute;
        left: 0%;
        bottom: 6%;
        padding: 2%;
        font-weight: 580;
        font-size: 9vw;
        background-color: #ffc300;
        color: #001d3d;
        padding-right: 4vw;
        font-family: "aduma";
        border-top-right-radius: 4vh;
        border-bottom-right-radius: 4vh;
        box-shadow: rgba(0, 0, 0, 0.25) 0px 54px 55px, rgba(0, 0, 0, 0.12) 0px -12px 30px, rgba(0, 0, 0, 0.12) 0px 4px 6px, rgba(0, 0, 0, 0.17) 0px 12px 13px, rgba(0, 0, 0, 0.09) 0px -3px 5px;
    }
</style>