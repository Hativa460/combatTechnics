<template>
    <div id="positions">
        <div class="title">{{ title }}</div>
        <div id="main-container">
            <div class="sub-container" @click="showHandler" id="subj1">
                <img class="img" src="../assets/media/glasses.svg" alt="glasses">
                <div class="img-txt">ניהול הגילוי</div>
            </div>
            <div class="sub-container second-img" @click="showHandler" id="subj2">
                <img class="img" src="../assets/media/fire.svg" alt="fire">
                <div class="img-txt">ניהול האש</div>
            </div>
            <div class="sub-container" @click="showHandler" id="subj3">
                <img class="img" src="../assets/media/test.svg" alt="test">
                <div class="img-txt">תרגול</div>
            </div>
        </div>
        <div id="button" @click="nextPage">יאללה נקסט</div>
        
    </div>
</template>

<script>
import PositionsHandler from "@/components/PositionsHandler";
import json from "../../text.json";

export default {
    name: "positions",
    components: {
        PositionsHandler
    },
    props:[],
    data() {
        return {
            pageNum: 4,
            clicked: false,
            chosenContent: 0
        }
    },
    methods: {
        showHandler(event) {
            let chosenNum = Number(event.currentTarget.id.charAt(4));
            this.chosenContent = chosenNum;
            this.clicked = true;
            this.$emit('show-pos', chosenNum);
        },
        nextPage() {
            this.$emit('next-page');
        }
    },
    computed: {
        title() { 
            return json.info[this.pageNum].title;
        }
    }
}
</script>

<style scoped>
    @font-face {
        font-family: "aduma";
        src: url("../assets/fonts/Aduma Regular.ttf");
    }
    #positions {
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
    #main-container {
        display: flex;
        flex-wrap: nowrap;
        flex-direction: column;
        align-items: flex-start;
        margin-top: 4%;
        justify-content: center;
    }
    .sub-container {
        display: flex;
        flex-wrap: nowrap;
        flex-direction: column;
        align-items: center;
        margin: 0%;
        margin-right: 4%;
    }
    .img {
        max-width: 100%;
        height: 17vh;
        border-radius: 2vh;
        border: #ffc300 solid 0.4vh;
        /* box-shadow: inset rgb(255, 195, 0, 0.3) 0px 0vh 2vh 1vh, rgba(139, 107, 0, 0.4) 0px 1.5vh 3vh -1.5vh */
    }
    .second-img {
        align-self: flex-end;
        margin-left: 4%;
    }
    .img-txt {
        font-size: 7vw;
        color: #ffc300;
        margin-top: 2%;
        font-weight: bold;
    }
    #button {
        margin: auto;
        margin-top: 7%;
        margin-bottom: 2%;
        font-family: "aduma";
        color: #001d3d;
        background-color: #ffc300;
        border-radius: 1.5vh;
        padding: 3%;
        width: 35vw;
        font-size: 9vw;
        text-align: center;
        font-weight: 570;
        box-shadow: rgba(34, 34, 38, 0.2) 0px 7vw 29vw 0px;
        animation: scaling 1.1s linear infinite alternate;
        -webkit-animation: scaling 1.1s linear infinite alternate;
    }
    @keyframes scaling {
        from {
            scale: 1;
        }
        to {
            scale: 1.05;
        }
    }
    @-webkit-keyframes scaling {
        from {
            scale: 1;
        }
        to {
            scale: 1.05;
        }
    }

</style>