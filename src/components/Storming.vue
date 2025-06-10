<template>
    <div id="storming">
        <img @click="backToPage" id="arrow" src="../assets/media/back-arrow.svg" alt="back">
        <div class="title">{{ title }}</div>
        <div class="text">
            <div class="line" v-for="(line, index) in text" :key='index' >{{ line }}</div>
        </div>
        <div class="card">
            <div class="card-title">{{ cardTitle1 }}</div>
            <div class="card-text">{{ text1 }}</div>
        </div>
        <div class="card">
            <div class="card-title">{{ cardTitle2 }}</div>
            <div class="card-text">{{ text2 }}</div>
        </div>
        <div id="btn-container">
            <button @click="delayBack"> 
                <span>סבבה הבנתי מה זה הסתערות</span>
            </button>
        </div>
    </div>
</template>

<script>
import json from "../../text.json";
export default {
    props: ["pageNum", "contentNum"],
    name: "storming",
    data() {
        return {

        }
    },
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
        cardTitle2() {
            return json.info[this.pageNum][this.contentNum].cardTitle2;
        },
        text1() {
            return json.info[this.pageNum][this.contentNum].text1;
        },
        text2() {
            return json.info[this.pageNum][this.contentNum].text2;
        }
    },
    methods: {
        delayBack() {
            setTimeout(() => {
                this.$emit('close-page');
            }, 400);
        },
        backToPage() {
            this.$emit('close-page');
        }
    }
}
</script>

<style scoped>
    @font-face {
        font-family: "aduma";
        src: url("../assets/fonts/Aduma Regular.ttf");
    }
    #storming {
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
    #btn-container {
        text-align: center;
    }
    button {
        outline: none;
        cursor: pointer;
        border: none;
        padding: 0.9rem 2rem;
        margin: 0;
        margin-top: 10%;
        margin-bottom: 5%;
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
    }
</style>
