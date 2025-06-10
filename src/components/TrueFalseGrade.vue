<template>
    <div id="true-false-grade" class="questions-container">
        <p id="title">סמן נכון/לא נכון לפי המשפטים המוצגים לפניך:</p>
      <div
        v-for="(questionData, index) in questions"
        :key="index"
        class="question-item"
      >
        <div class="question-text">{{ questionData.question }}</div>
        <div class="answers">
          <div
            class="answer true-button"
            @click="selectAnswer(index, true)"
            :class="{ selected: userAnswers[index] === true, 'clicked': clickedIndex === index && clickedAnswer === true }"
          >
            נכון
          </div>
          <div
            class="answer false-button"
            @click="selectAnswer(index, false)"
            :class="{ selected: userAnswers[index] === false, 'clicked': clickedIndex === index && clickedAnswer === false }"
          >
            לא נכון
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  import json from "../../text.json";
  
  export default {
    name: "true-false-grade",
    data() {
      return {
        questions: json.trueOrFalse ,
        userAnswers: [],
        clickedIndex: null,
        clickedAnswer: null,
        points: 0, 
      };
    },
    methods: {
    selectAnswer(index, answer) {
      console.log("index:"+ index, "answer:"+ answer, "correctAnswer:"+ this.questions[index].correctAnswer, +"previousAnswer:"+ this.userAnswers[index]+ "currentPoints:"+ this.points);
      const wasPreviouslyCorrect = this.userAnswers[index] === this.questions[index].correctAnswer;
      this.$set(this.userAnswers, index, answer);
      this.clickedIndex = index;
      this.clickedAnswer = answer;
      const isCurrentlyCorrect = answer === this.questions[index].correctAnswer;

      if (isCurrentlyCorrect && !wasPreviouslyCorrect) {
        this.points += 4;
      } else if (!isCurrentlyCorrect && wasPreviouslyCorrect) {
        this.points -= 4;
      }

      this.$emit('points-updated', this.points);
      console.log("points after update:", this.points);
    },
    },
  };
  </script>
  
  <style scoped>
  #true-false-grade {
    display: flex;
    flex-direction: column;
    align-items: center;
    width: 85vw;
    background-color: #fce9a9;
    border-radius: 2vh;
    padding: 5%;
    margin: 5% auto 0;
    margin-top: 8%;
    box-shadow: rgba(0, 0, 0, 0.24) 0px 3px 8px;
  }
  
  .question-item {
    width: 100%;
    padding: 3% 0;
  }
  
  .question-item:not(:last-child) {
    border-bottom: 1px solid #ddd;
    margin-bottom: 2vh;
  }
  
  .question-text {
    color: #001d3d;
    font-size: 7vw;
    font-weight: 560;
    font-family: "aduma";
    text-align: center;
    margin-bottom: 3%;
  }

  #title {
    color: #001d3d;
    font-size: 8vw;
    font-weight: 560;
    font-family: "aduma";
    text-align: center;
    margin-bottom: 3%;
  }
  
  .answers {
    display: flex;
    width: 80%;
    justify-content: space-around;
  }
  
  .answer {
    background-color: #001d3d;
    color: #ffc300;
    font-family: "aduma";
    font-size: 6vw;
    border-radius: 1vh;
    font-weight: 580;
    text-align: center;
    padding: 2% 4%;
    cursor: pointer;
    box-shadow: none; /* הסרת צל ברירת מחדל */
    transition: box-shadow 0.3s ease; /* מעבר חלק עבור הצל */
  }
  
  .answer.selected {
    background-color:#ffc300;
    color: #001d3d;
    font-family: "aduma";
    font-size: 6vw;
    border-radius: 1vh;
    font-weight: 580;
    text-align: center;
    padding: 2% 4%;
    cursor: pointer;
    box-shadow: none; /* הסרת צל ברירת מחדל */
    transition: box-shadow 0.3s ease; /* מעבר חלק עבור הצל */

  }
  
  .answer.clicked {
    /* box-shadow: rgba(0, 0, 1, 0.482) 0px 2px 4px 0px; הוספת צל בעת לחיצה */
  }
  
  /* .true-button:hover {
    background-color: #19376d;
  }
  
  .false-button:hover {
    background-color: #19376d;
  } */
  </style>