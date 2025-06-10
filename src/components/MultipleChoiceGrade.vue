<template>
    <div id="multiple-choice-grade">
      <div class="question-container">
        <div class="question-text">{{ title }}</div>
        <div class="answers">
          <div
            v-for="(answer, index) in answers"
            :key="index"
            :id="index"
            class="answer"
            @click="selectAns(index)"
            :class="{ selected: selectedAns === index }"
            :style="{ background: bgColor }"
          >
            {{ answer }}
          </div>
        </div>
        </div>
    </div>
  </template>
  
  <script>
  import json from "../../text.json";
  export default {
    name: "multiple-choice-grade",
    props: ["questionNum"],
    data() {
      return {
        btnText: "בדוק אותי", // **כבר לא בשימוש ישיר**
        selectedAns: -1,
        bgColor: '#fce9a9',
        isClicked: false,
        points: 0,
        correctAnswer: json.multipleChoice[this.questionNum].correctAns,
      };
    },
    computed: {
      title() {
        return json.multipleChoice[this.questionNum].title;
      },
      answers() {
        return json.multipleChoice[this.questionNum].answers;
      },
      // correctAns() { // **הוסר - הערך נשמר ב-data**
      //   return json.multipleChoice[this.questionNum].correctAns;
      // }
    },
    methods: {
      selectAns(index) {
        if (!this.isClicked) {
          this.selectedAns = index;
          this.checkAnswerAndEmitPoints(index); // בדוק תשובה ושלח נקודות
          this.isClicked = true; // משתמש לא יכול לשנות תשובה לאחר הבחירה
        } else {
          // אם כבר נבחרה תשובה, אפשר לאפשר ביטול בחירה או התנהגות אחרת
          // לדוגמה:
          // this.isClicked = false;
          // this.selectedAns = -1;
          // this.bgColor = "#fce9a9";
          // this.points = 0;
          // this.$emit('points-updated', this.points);
        }
      },
      checkAnswerAndEmitPoints(selectedAnswer) {
          if (selectedAnswer === this.correctAnswer) {
          this.points = 10; 
        } else {
          this.points = 0;
        }
        this.$emit('points-updated', this.points);
        console.log(this.points+"שאלה שלישית")
      }
    }
  };
  </script>

<style scoped>
    #multiple-choice-grade {
        margin: 0;
        height: fit-content;
        margin-bottom: 10%;
        width: 100vw;
        position: relative;
        top: 0;
        right: 0;
        /* background-color: blueviolet; */
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
        padding-bottom: 20vh;
        border-radius: 1vh;
        background: #fce9a9;
        color: #001d3d;
        width: 90vw;
        margin-top: 7%;
        font-size: 8vw;
        font-family: "aduma";
    }

    .question {
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
        margin-right: 4%;
        margin-top: 5%;
        margin-bottom: 5%;
        width: fit-content;
        -webkit-appearance: none;
        appearance: none;
        /* justify-self: center; */
        background-color: #ffc300;
        color: #001d3d;
        border-radius: 1.5vh;
        border: none;
        cursor: pointer;
        /* justify-self: flex-end; */
        transition: transform ease-in 0.1s, box-shadow ease-in 0.25s;
        box-shadow: 0 2px 25px #fce9a984;
    }
    .selected {
        box-shadow: #001d3d94 0px 0px 1.5vh;
        /* background-color: #001d3d;
        color: #fce9a9; */
    }

</style>