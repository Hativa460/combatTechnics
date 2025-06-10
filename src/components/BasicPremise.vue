<template>
    <div id="basic-premise">
        <div class="title">{{ title }}</div>
        <div class="text">
            <div class="line" v-for="(line, index) in text" :key='index' >{{ line }}</div>
        </div>
        <button @click="nextPage"> 
            <span>מושלם הבנתי</span>
        </button>
    </div>
</template>

<script>
import json from "../../text.json";

export default {
    name: "basic-premise",
    props:[],
    data() {
        return {
            pageNum : 1
        }

    },
    methods: {
        nextPage() {
            setTimeout(() => {
                this.$emit('next-page');
            }, 400);
            
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

    #basic-premise {
        margin: 0%;
        height: 100%;
        width: 100vw;
        position: absolute;
        top: 0;
        right: 0;
        display: flex;
        flex-wrap: nowrap;
        flex-direction: column;
        align-items: center;
        justify-content: flex-start;
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
        margin-top: -46%;
        padding: 5%;
        padding-top: 15%;
        padding-bottom: 10%;
        width: 80vw;
        border-radius: 3vh;
        border: #ffc300 solid 1.2vw;
        border-top: none;    
        box-shadow: rgb(255, 195, 0, 0.3) 0px 6vh 7vh 1vh, rgba(139, 107, 0, 0.4) 0px 1.5vh 3vh -1.5vh;

    }
    .line {
        color: #f6f0e6;
        font-size: 5.5vw;
        margin-top: 8%;

    }
    button {
        outline: none;
        cursor: pointer;
        border: none;
        padding: 0.9rem 2rem;
        margin: 0;
        margin-bottom: 30%;
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