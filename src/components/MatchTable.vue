<template>
  <div id="match">
    <div id="table">
      <div id="instruction">{{ title }}</div>
      <table class="inner-table">
        <tr
          v-for="(square, index) in column"
          :key="index"
          :class="index === column.length - 1 ? '' : 'row'"
        >
          <td class="drop-square" :class="{'correct': rowFeedbackClass(index) === 'correct', 'incorrect': rowFeedbackClass(index) === 'incorrect'}">
            <draggable
              class="list-group"
              :list="dropOptions[index]"
              :group="{ name: 'people', put: true, pull: true }"
              @end="updateDropOptions(index)"
            >
              <div v-for="option in dropOptions[index]" class="drag-option" v-if="option !== '[]'">
                {{ option }}
              </div>
            </draggable>
          </td>
          <td class="text-square" :class="{'correct': rowFeedbackClass(index) === 'correct', 'incorrect': rowFeedbackClass(index) === 'incorrect'}">{{ square }}</td>
        </tr>
      </table>
      <div class="drag-options" id="drag-options">
        <draggable :list="dragOptions" :group="{ name: 'people', pull: true, put: true }">
          <div v-for="(option, index) in dragOptions" class="drag-option" :key="index">
            {{ option }}
          </div>
        </draggable>
      </div>
      <div id="checkBtn" @click="checkAns">{{ btnText }}</div>
    </div>
  </div>
</template>

<script>
import json from "../../text.json";
import draggable from 'vuedraggable';

export default {
  name: "match-table",
  props: ["questionNum"],
  components: {
    draggable
  },
  data() {
    return {
      enabled: true,
      dragOptions: json.matching[this.questionNum].dragOptions,
      dropOptions: json.matching[this.questionNum].dropOptions,
      btnText: "בדוק אותי",
      rowCorrect: Array(json.matching[this.questionNum].correctAnswers.length).fill(null) // Initialize feedback for each row
    };
  },
  methods: {
    checkAns() {
      let correctAnswers = json.matching[this.questionNum].correctAnswers;
      let userAnswers = this.dropOptions;

      if (this.btnText === "בדוק אותי") {
        let allCorrect = true;
        for (let i = 0; i < correctAnswers.length; i++) {
          const isRowCorrect = JSON.stringify(userAnswers[i].sort()) === JSON.stringify(correctAnswers[i].sort());
          this.rowCorrect[i] = isRowCorrect;
          if (!isRowCorrect) {
            allCorrect = false;
          }
        }

        if (allCorrect) {
          this.btnText = "אתה מטורף!";
        } else {
          this.btnText = "הממ לא בדיוק...";
        }
      } else {
        this.rowCorrect = Array(correctAnswers.length).fill(null); // Reset feedback
        this.btnText = "בדוק אותי";
      }
    },
    updateDropOptions(index) {
      this.$set(this.dropOptions, index, this.dropOptions[index]);
      this.rowCorrect[index] = null;
    },
    rowFeedbackClass(index) {
      if (this.rowCorrect[index] === true) {
        return 'correct';
      } else if (this.rowCorrect[index] === false) {
        return 'incorrect';
      }
      return '';
    }
  },
  computed: {
    title() {
      return json.matching[this.questionNum].title;
    },
    column() {
      return json.matching[this.questionNum].column;
    }
  }
};
</script>

<style scoped>
@font-face {
  font-family: "aduma";
  src: url("../assets/fonts/Aduma Regular.ttf");
}

#match {
  margin: 0;
  height: fit-content;
  width: 100vw;
  position: relative;
  top: 0;
  right: 0;
}

#table {
  list-style-type: none;
  padding: 1%;
  margin: auto;
  margin-top: 0%;
  background-color: #fce9a9;
  border-radius: 1vh;
  width: 95vw;
}

#instruction {
  color: #001d3d;
  font-size: 8vw;
  margin: 2%;
  font-weight: 560;
  font-family: "aduma";
}

.inner-table {
  border-radius: 2vh;
  margin: auto;
  width: 95%;
  margin-bottom: 2%;
  border-collapse: collapse;
  box-shadow: rgba(0, 0, 0, 0.24) 0px 3px 8px;
}

.row {
  border-bottom: #001d3d solid 0.5vh;
}

.drop-square {
  width: 40%;
  border-left: #001d3d solid 0.5vh;
  background-color: #ffc300;
}

.list-group {
  display: flex;
  flex-wrap: wrap;
}

.text-square {
  height: fit-content;
  white-space: break-spaces;
  color: #001d3d;
  font-size: 5vw;
  padding: 3.5%;
  background-color: #ffc300;
}

.drag-option:active {
  z-index: 1000;
}

.drag-options {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  margin-top: 5%;
  justify-content: space-evenly;
  border: #001d3d 0.4vh dashed;
  border-radius: 5%;
  padding-top: 1%;
  margin-bottom: 2vh;
  min-height: 6vh;
}

.drag-option {
  border-radius: 1vh;
  background-color: #001d3d;
  color: #ffc300;
  padding: 3%;
  font-size: 2.1vh;
  font-weight: bolder;
  margin: 1%;
}

#checkBtn {
  margin: 2%;
  background-color: #001d3d;
  font-family: "aduma";
  color: #ffc300;
  font-size: 8vw;
  border-radius: 1.5vh;
  font-weight: 580;
  width: 35vw;
  text-align: center;
  padding: 2%;
  box-shadow: rgba(0, 0, 0, 0.24) 0px 3px 8px;
}

.correct {
  background-color: rgba(179, 241, 160, 0.704); /* Light green */
}

.incorrect {
  background-color: rgba(247, 83, 83, 0.677); /* Light red */
}
</style>