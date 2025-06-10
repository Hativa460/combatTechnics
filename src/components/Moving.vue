<template>
    <div id="moving">
        <div v-if="showMenu">
            <div class="title">{{ title }}</div>
            <div class="container">
                <div v-for="(subtitle, index) in subTitles" :key="subtitle" class="subTitle" :id="'topic'+(index)" @click="showTopic">
                    <div class="text">{{ subtitle }}</div>
                </div>
            </div>
            <div id="button" @click="nextPage">וואי זה כבר כמעט הסוף</div>
        </div>
        <div v-else>
            <leaving :contentNum="topicNum" :pageNum="7" v-if="topicNum===0" @close-page="backHome"></leaving>
            <storming v-if="topicNum===1" :contentNum="topicNum" :pageNum="7" @close-page="backHome"></storming>
            <second-test v-if="topicNum===2" :contentNum="topicNum" :pageNum="7" @close-page="backHome"></second-test>
        </div>    
    </div>
</template>

<script>
import json from "../../text.json";
import Leaving from "@/components/Leaving";
import Storming from "@/components/Storming";
import SecondTest from "@/components/SecondTest";

export default {
    name: "moving",
    props:[],
    components: {
        Leaving,
        Storming,
        SecondTest
    },
    data() {
        return {
            pageNum:6,
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
 @font-face {
        font-family: "aduma";
        src: url("../assets/fonts/Aduma Regular.ttf");
    }
    #button{
        background-color: #ffc300;
        color: #001d3d;
        font-family: "aduma";
        position: relative;
        margin: auto;
        margin-top: 20%;
        margin-bottom: 8%;
        width: 56vw;
        text-align: center;
        border: none;
        padding: 3%;
        font-size: 8.5vw;
        font-weight: 550;
        border-radius: 5vw;
        -webkit-box-shadow: rgba(0, 0, 0, 0.25) 0px 54px 55px, rgba(0, 0, 0, 0.12) 0px -12px 30px, rgba(0, 0, 0, 0.12) 0px 4px 6px, rgba(0, 0, 0, 0.17) 0px 12px 13px, rgba(0, 0, 0, 0.09) 0px -3px 5px;
        box-shadow: rgba(0, 0, 0, 0.25) 0px 54px 55px, rgba(0, 0, 0, 0.12) 0px -12px 30px, rgba(0, 0, 0, 0.12) 0px 4px 6px, rgba(0, 0, 0, 0.17) 0px 12px 13px, rgba(0, 0, 0, 0.09) 0px -3px 5px;
    }
    #moving {
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
    .subTitle {
        background: url(../assets/media/טכניקה.png);
        background-repeat: no-repeat;
        background-size: 100% 100%;
        width: 90vw;
        height: 12vh;
        margin-top: 7%;
        margin-right: 0%;
    }
    .text {
        color: #001d3d;
        font-family: "aduma";
        font-size: 9vw;
        text-align: start;
        margin-right: 3%;
        margin-top: 7%;
        /* font-weight: bolder; */
    }
    .container {
        margin-top: 10%;
    }
    
    
</style>