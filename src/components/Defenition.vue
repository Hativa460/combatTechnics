<template>
    <div id="defenition">
        <div class="title">{{ title }}</div>
        <div class="text">
            <div class="line" v-for="(line, index) in text" :key='index' >{{ line }}</div>
        </div>
        <div id="pyramid">
            <div class="level" v-for="(level, index) in pyramid" :key='index' >
            <!-- <div class="level" v-for="(level, index) in pyramid" :key='index' :style="{width: level.width}"> -->
                <div class="levelTitle">{{ level.title }}</div>
                <div :style="{width: level.width}" class="levelText">{{ level.explenation}}</div>
            </div>
        </div>
        <div id="button" @click="nextPage">כן כן אפשר להמשיך</div>
        <div id="nav-target"></div>
    </div>
</template>

<script>

import json from "../../text.json";
export default {
    name: "defenition",
    props:[],
    data() {
        return {
            pageNum: 0,
            pyramid: json.pyramid,
            steps: [
                {
                    target: '#nav-target',  // We're using document.querySelector() under the hood
                    content: "בכל שלב אתה יכול ללחוץ על תפריט הניווט כדי לעבור לכל נושא שתרצה",
                    params: {
                    placement: 'left'
                    }
                }
            ],
            myOptions: {
                labels: {
                    buttonStop: 'מושלם הבנתי'
                }  
            }
        }
    },
    methods: {
        nextPage() {
            this.$emit('next-page');
        }
    },
    computed: {
        title() { 
            return json.info[this.pageNum].title;
        },
        text() {
            return json.info[this.pageNum].text;
        }
    }
}
</script>

<style scoped>
    @font-face {
        font-family: "aduma";
        src: url("../assets/fonts/Aduma Regular.ttf");
    }
    #defenition {
        margin: 0%;
        height: 100%;
        width: 100vw;
        position: absolute;
        top: 0;
        right: 0;
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
    #pyramid {
        width: 98%;
        margin: auto;
        margin-top: 20%;
        display: flex;
        justify-content: space-around;
        align-items: center;
        flex-direction: column;
        flex-wrap: nowrap;
        margin-bottom: 10%;
        clip-path: polygon(15% 0%, 85% 0%, 100% 100%, 0% 100%);
        /* background-color: aqua; */
    }
    .level {
        display: flex;
        align-items: center;
        flex-direction: column;
        flex-wrap: nowrap;
        background-color: #ffc300;
        position: relative;
        color: #001d3d;
        text-align: center;
        width: 100%;
        margin: 1.5%;
        padding: 2%;
        /* border-radius: 8vh; */
        /* clip-path: polygon(0% 100%, 17.5% 0%, 82.5% 0%, 100% 100%); */
    }

    .levelTitle {
        font-family: "aduma";
        font-weight: 570;
        font-size: 7vw;
    }

    .levelText {
        font-size: 5.5vw;
        /* width: 90vw; */
        margin: 2%;
    }
    #button {
        background-color: #f6e19d;
        color: #001d3d;
        font-family: "aduma";
        position: relative;
        margin: auto;
        margin-bottom: 8%;
        width: 50vw;
        text-align: center;
        border: none;
        padding: 2%;
        font-size: 6vw;
        font-weight: bold;
        border-radius: 2vw;
        box-shadow: rgba(0, 0, 0, 0.25) 0px 54px 55px, rgba(0, 0, 0, 0.12) 0px -12px 30px, rgba(0, 0, 0, 0.12) 0px 4px 6px, rgba(0, 0, 0, 0.17) 0px 12px 13px, rgba(0, 0, 0, 0.09) 0px -3px 5px;;
    }
    #nav-target {
        width: 10vw;
        top: 2%;
        /* z-index: 5; */
        right: 2%;
        margin: 0px;
        position: absolute;
        height: 4vh;
        background-color: rgba(127, 255, 212, 0.416);
    }

    .v-step {
        max-width: 50vw;
    }

</style>