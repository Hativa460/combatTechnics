<template>
    <div id="multiple-choice">
      <div class="question-container">
        <div class="question-text">{{ title }}</div>
        <div class="answers">
          <div
            v-for="(answer, index) in answers"
            :key="index"
            :id="index"
            class="answer"
            @click="selectAns"
            :class="{ selected: selectedAns === index }"
            :style="answerStyle(index)"
          >
            {{ answer }}
          </div>
        </div>
        <div class="btn" @click="checkAns">{{ btnText }}</div>
      </div>
    </div>
  </template>
  
  <script>
  import json from "../../text.json";
  export default {
    name: "multiple-choice",
    props: ["questionNum"],
    data() {
      return {
        btnText: "בדוק אותי",
        selectedAns: -1,
        isClicked: false,
      };
    },
    computed: {
      title() {
        return json.multipleChoice[this.questionNum].title;
      },
      answers() {
        return json.multipleChoice[this.questionNum].answers;
      },
      correctAns() {
        return json.multipleChoice[this.questionNum].correctAns;
      },
    },
    methods: {
      selectAns(event) {
        if (!this.isClicked) {
          this.selectedAns = Number(event.currentTarget.id);
        }
      },
      checkAns() {
        if (!this.isClicked) {
          this.isClicked = true;
          if (this.selectedAns === this.correctAns) {
            this.btnText = "נדיר";
          } else if (this.selectedAns !== -1) {
            this.btnText = "לא בדיוק...";
          }
        } else {
          this.isClicked = false;
          this.btnText = "בדוק אותי";
          this.selectedAns = -1;
        }
      },
      answerStyle(index) {
        if (this.isClicked && index === this.selectedAns) {
          if (index === this.correctAns) {
            return { backgroundColor: 'rgb(179, 241, 160)' };
          } else {
            return { backgroundColor: 'rgb(247, 83, 83)' };
          }
        } else if (this.selectedAns === index && !this.isClicked) {
          return { boxShadow: '#001d3d94 0px 0px 1.5vh' };
        }
        return { backgroundColor: '#fce9a9' };
      },
    },
  };
  </script>
  
  <style scoped>
  #multiple-choice {
    margin: 0;
    height: fit-content;
    margin-bottom: 10%;
    width: 100vw;
    position: relative;
    top: 0;
    right: 0;
    display: flex;
    flex-direction: column;
    flex-wrap: nowrap;
    align-items: center;
  }
  
  .question-container {
    display: flex;
    height: fit-content;
    flex-direction: column;
    flex-wrap: nowrap;
    justify-content: center;
    overflow: hidden;
    margin: auto;
  }
  
  .question-text {
    padding: 2vh;
    padding-bottom: 20vh; /* Reduced bottom padding */
    border-radius: 1vh;
    background: #fce9a9;
    color: #001d3d;
    width: 90vw;
    margin-top: 7%;
    font-size: 8vw;
    font-family: "aduma";
    text-align: center; /* Center the question text */
  }
  .question{
    margin-bottom: 15%;
  }
  
.answers {
 display: -webkit-box;
 display: -ms-flexbox;
 width: 84vw;
 display: flex;
 -webkit-box-orient: vertical;
 -webkit-box-direction: normal;
 -ms-flex-direction: column;
 flex-direction: column;
 -ms-flex-wrap: nowrap;
 flex-wrap: nowrap;
 -webkit-box-pack: center;
 -ms-flex-pack: center;
 justify-content: center;
 overflow-x: hidden;
 margin: auto;
 margin-top: -38%;
 background: #ffc300;
 border-radius: 1vh;
 padding: 2%;
 -webkit-box-shadow: rgba(0, 0, 0, 0.35) 0px 5px 15px;
 box-shadow: rgba(0, 0, 0, 0.35) 0px 5px 15px;
 }


 .answer {
 background-color: #fce9a9;
 color: #001d3d;
 font-size: 5vw;
 font-weight: 600;
 padding: 2%;
 border-radius: 0.5vh;
 margin: 1.5%;
 }
  
  .btn {
    min-width: 35vw;
    display: inline-block;
    font-family: "aduma";
    text-align: center;
    font-size: 8vw;
    font-weight: 580;
    padding: 2%;
    margin-top: 5%;
    margin-bottom: 5%;
    width: fit-content;
    appearance: none;
    background-color: #ffc300;
    color: #001d3d;
    border-radius: 1.5vh;
    border: none;
    cursor: pointer;
    transition: transform ease-in 0.1s, box-shadow ease-in 0.25s;
    box-shadow: 0 2px 25px #fce9a984;
  }
  
  .selected {
    /* box-shadow: #001d3d94 0px 0px 1.5vh; */ /* Removed default selected style */
  }
  </style>