<template>
    <div id="content-handler">
        <div v-for="(subtitle, index) in subtitels" :key="index" class="subtitle">
            <div :id="index" class="subtitleName" @click="showText">{{index+1}}. {{subtitle}}</div>
            <open-text v-if="textVis && index === pressedIndex" :mainNum="contentNum+1" :subNum="index"></open-text>
        </div>
        <div class="button" @click="nextPage">כן הבנתי</div>
    </div>
</template>

<script>
import OpenText from '@/components/OpenText.vue';
import json from "../../text.json";

export default {
    name: "content-handler",
    components: {
        OpenText
    },
    props:["contentNum"],
    data() {
        return {
            pressedIndex: 0,
            textVis: false,
        }
    },
    methods: {
        showText(event) {
            this.pressedIndex = Number(event.target.id);
            if (this.textVis === false) {
                this.textVis = true;
            } else {
                this.textVis = false
            }
        },
        nextPage() {
            this.$emit('next-page');
        }
    },
    computed: {
        subtitels() {
            const subtitleKey = `subtitles${this.contentNum}`;
            return json.chapters[0][subtitleKey];
        }
    }
}


</script>

<style scoped>
    @font-face {
        font-family: "aduma";
        src: url("../assets/fonts/Aduma Regular.ttf");
    }
    #content-handler {
        margin: auto;
        margin-top: 5%;
        height: auto;
        padding-top: 5%;
        padding-bottom: 40%;
        /* height: fit-content; */
        margin-bottom: 10%;
        width: 90vw;
        position: relative;
        background-color: #fce9a9;
        border-radius: 1.5vh;
        box-shadow: rgba(0, 0, 0, 0.35) 0px 5vw 15vw;
        /* position: relative;
        top: 0;
        right: 0; */
    }
    .subtitleName {
        box-shadow: rgba(0, 0, 0, 0.24) 0px 3px 8px;
        background-color: #ffc300;
        margin: auto;
        padding: 3%;
        width: 90%;
        color: #001d3d;
        font-size: 7vw;
        font-weight: bold;
        border-radius: 1vh;
        margin-top: 5%;
        margin-bottom: 2.5%;
    }

    .button {
        margin: auto;
        text-align: center;
        position: absolute;
        right: 50%;
        transform: translateX(50%);
        bottom: 6%;
        color:#ffc300;
        background-color: #001d3d;
        border-radius: 1vh;
        font-size: 8vw;
        font-weight: 600;
        font-family: "aduma";
        padding: 3%;
        width: 40vw;
    }
</style>