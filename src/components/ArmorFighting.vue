<template>
    <div id="armor-fighting">
        <div class="title">{{ title }}</div>
        <img id="image" :src="imageSrc" alt="לחימת השריון" class="animate__animated animate__rotateIn">
        <button @click="nextPage">כןכן הלאה</button>
    </div>
</template>

<script>
import json from "../../text.json";
export default {
    name: "armor-fighting",
    props:[],
    data() {
        return {
            pageNum : 2,
            imageSrc: require('../assets/media/לחימת השריון.png')
            // imageSrc: require(json.info[this.pageNum].src),
            // title: json.info[this.pageNum].title
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
        // imageSrc(src) {
        //     return require(json.info[this.pageNum].src);
        // }
    }
}
</script>

<style scoped>
    @font-face {
        font-family: "aduma";
        src: url("../assets/fonts/Aduma Regular.ttf");
    }
    #armor-fighting {
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
        justify-content: center;
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
        overflow: hidden;
    }
    #image {
        max-width: 96%;
        margin-left: 2%;
        margin-right: 2%;
        margin-bottom: 30%;
        height: 38vh;
    }
    button {
        border: none;
        color: #001d3d;
        background-image: linear-gradient(30deg, #f7bd01, #fcdb6c);
        border-radius: 4vh;
        margin-bottom: 30%;
        text-align: center;
        background-size: 100% auto;
        font-family: "aduma";
        font-size: 8vw;
        font-weight: bold;
        padding: 0.6em 1.5em;
        -webkit-animation: pulse512 2s infinite;
        animation: pulse512 2s infinite;
    }
    @-webkit-keyframes pulse512 {
        0% {
            box-shadow: 0 0 0 0 #fcda6c94;
        }

        70% {
            box-shadow: 0 0 0 5vh rgb(218 103 68 / 0%);
        }

        100% {
            box-shadow: 0 0 0 0 rgb(218 103 68 / 0%);
        }
    }

    @keyframes pulse512 {
    0% {
        box-shadow: 0 0 0 0 #fcda6c94;
    }

    70% {
        box-shadow: 0 0 0 5vh rgb(218 103 68 / 0%);
    }

    100% {
        box-shadow: 0 0 0 0 rgb(218 103 68 / 0%);
    }


}

</style>