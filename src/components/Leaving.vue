<template>
    <div id="leaving">
        <div v-if="clicked === false">
            <img @click="backToPage" id="arrow" src="../assets/media/back-arrow.svg" alt="back">
            <div id="main-title">טכניקות לחימה בתנועה</div>
            <div id="sub-title">{{ title }}</div>
            <div id="text">{{ explenation }}</div>
            <div id="subtitle2">שיטות</div>
            <div class="flex-container" v-for="(topic, index) in topics" :key="index" @click="showTable" :id="'topic'+(index)">
                <div class="topic-text" >{{ topic }}</div>
                <img class="arrow" src="../assets/media/חץ.png" alt="arrow">
            </div>
            <div id="btn-container">
            <button @click="delayBack"> 
                <span>נחזור לנושא המרכזי?</span>
            </button>
        </div>
        </div>
        <div v-if="clicked === true">
            <topic-table :pageNum="pageNum" :contentNum="contentNum" :topicNum="topicNum" @close-page="closePage"></topic-table>
           
        </div>

        <!-- <img id="back-btn" src="../assets/media/חזרה.png" alt="back"> -->
    </div>
</template>

<script>
import json from "../../text.json";
import TopicTable from "@/components/TopicTable";
export default {
    name: "leaving",
    props: ["pageNum", "contentNum"],
    data() {
        return {
            clicked:false,
            topicNum: 0
        }
    },
    components: {
        TopicTable
    },
    computed: {
        title() {
            return json.info[this.pageNum][this.contentNum].title;
        },
        explenation(){
            return json.info[this.pageNum][this.contentNum].explenation;
        },
        topics() {
            return json.info[this.pageNum][this.contentNum].topics;
        }

    },
    methods: {
        showTable(event) {
        let nTopic = Number(event.currentTarget.id.charAt(5));
        this.topicNum = nTopic;
        this.clicked = true;
        console.log('Clicked:', this.clicked, 'Topic Num:', this.topicNum);
    },
    closePage() {
        this.clicked = false;
    },
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
    #arrow {
        position: fixed;
        top: 0%;
        right: 1%;
        z-index: 3;
        max-width: 100%;
        height: 10vh;
        background-color: #001d3d;
    }
    #leaving {
        margin: 0%;
        height: 100%;
        width: 100vw;
        position: absolute;
        top: 0;
        right: 0;
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
    #text {
        /* width: 92%; */
        margin-right: 2%;
        margin-top: 2%;
        margin-bottom: 10%;
        color: #f6f0e6;
        font-size: 6vw;
        white-space: break-spaces;
    }
    #subtitle2 {
        font-family: "aduma";
        margin-top: 12%;
        margin-right: 2%;
        color: #f6f0e6;
        font-weight: bolder;
        font-size: 15vw;
        margin-bottom: 4%;
    }
    .flex-container {
        display: flex;
        flex-wrap: nowrap;
        flex-direction: row;
        background-color: #fce9a9;
        color: #001d3d;
        width: 70vw;
        justify-content: space-between;
        align-items: center;
        margin-bottom: 3%;
        border-bottom-left-radius: 5vh;
        border-top-left-radius: 5vh;
        padding: 2%;
        box-shadow: rgba(0, 0, 0, 0.632) 0px 4vw 8vw 0vh;
    }
    .topic-text {
        font-size: 9vw;
        font-family: "aduma";
    }
    .arrow {
        max-width: 100%;
        height: 6vh;
        margin: 2%;
        position: relative;
        animation: moving 0.7s linear infinite alternate;
        -webkit-animation: moving 0.7s linear infinite alternate;
    }
    #back-btn {
        max-width: 100%;
        height: 10vh;
        margin-top: 4%;
    }
    @keyframes moving {
        from {
            right: 0vw;
        }
        to {
            right: 1vw;
        }
    }
    @-webkit-keyframes moving {
        from {
            right: 0vw;
        }
        to {
            right: 1vw;
        }
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