<template>
    <div id="draw-lines">
      <div id="bg-container" :style="{background: bgColor}">
        <div id="instruction">{{ title }}</div>
        <div id="covered-container" class="covered-container">
          <div class="target-div question-container">
            <div class="container" id="list-container" @click="selectItem">
              <div class="column" id="list1">
                <div class="item" v-for="(item, index) in list1" :key="index">
                  <div class="list-item">{{ item }}</div>
                  <span class="dot" :id="'ans' + (index + 1) + 'a'"></span>
                </div>
              </div>
              <div class="column" id="list2">
                <div class="item" v-for="(item, index) in list2" :key="index">
                  <span class="second-dot" :id="'ans' + (index + 5) + 'b'"></span>
                  <div class="list-item">{{ item }}</div>
                </div>
              </div>
            </div>
          </div>
          <canvas id="canvas" class="overlay-canvas" @load="resizeCanvas"></canvas>
          <div id="checkBtn" @click="checkAns">{{ btnText }}</div>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  import json from "../../text.json";
  export default {
    name: "draw-lines",
    props: ["questionNum"],
    data() {
      return {
        startItem: undefined,
        selectedItems: [],
        bgColor: "#fce9a9",
        btnText: "בדוק אותי",
        linesColors: {} // Object to store the color of each drawn line
      };
    },
    computed: {
      title() {
        return json.drawLines[this.questionNum].title;
      },
      list1() {
        return json.drawLines[this.questionNum].list1;
      },
      list2() {
        return json.drawLines[this.questionNum].list2;
      },
      correctLines() {
        return json.drawLines[this.questionNum].correctLines;
      }
    },
    mounted() {
      this.canvas = document.getElementById('canvas');
      this.ctx = this.canvas.getContext('2d');
      this.resizeCanvas();
    },
    methods: {
      selectItem(event) {
        event.preventDefault();
        if (event.target.tagName === 'SPAN') {
          if (this.startItem === undefined) {
            this.startItem = event.target.id;
            this.deleteLine(event.target.id);
            event.target.classList.add('selected');
            this.drawAllLines();
          } else {
            if (event.target.id.charAt(4) === this.startItem.charAt(4)) {
              if (event.target.id.charAt(3) === this.startItem.charAt(3)) {
                document.getElementById(this.startItem).classList.remove('selected');
                this.startItem = undefined;
                this.drawAllLines();
              } else {
                document.getElementById(this.startItem).classList.remove('selected');
                this.startItem = event.target.id;
                this.deleteLine(event.target.id);
                event.target.classList.add('selected');
                this.drawAllLines();
              }
            } else {
              let selectedTuple = [this.startItem, event.target.id];
              this.deleteLine(event.target.id);
              this.selectedItems.push(selectedTuple);
              document.getElementById(selectedTuple[1]).classList.add('selected');
              this.startItem = undefined;
              this.drawAllLines();
            }
          }
        } else {
          if (this.startItem !== undefined) {
            document.getElementById(this.startItem).classList.remove('selected');
            this.startItem = undefined;
            this.drawAllLines();
          }
        }
      },
      resizeCanvas() {
        const container = document.getElementById('covered-container');
        this.canvas.width = container.offsetWidth;
        this.canvas.height = container.offsetHeight;
        this.drawAllLines(); // Redraw lines after resize
      },
      deleteLine(item) {
        let tempList = [];
        for (let i = 0; i < this.selectedItems.length; i++) {
          if (this.selectedItems[i][0] !== item && this.selectedItems[i][1] !== item) {
            tempList.push(this.selectedItems[i]);
          } else {
            document.getElementById(this.selectedItems[i][0]).classList.remove('selected');
            document.getElementById(this.selectedItems[i][1]).classList.remove('selected');
            // Remove the color information for the deleted line
            const keyToDelete = this.selectedItems[i].sort().join('-');
            delete this.linesColors[keyToDelete];
          }
        }
        this.selectedItems = tempList;
      },
      drawLine(x1, y1, x2, y2, color = '#001d3d') {
        const rect = this.canvas.getBoundingClientRect();
        this.ctx.beginPath();
        this.ctx.moveTo(x1 - rect.left, y1 - rect.top);
        this.ctx.lineTo(x2 - rect.left, y2 - rect.top);
        this.ctx.lineWidth = 5;
        this.ctx.strokeStyle = color;
        this.ctx.stroke();
      },
      drawAllLines() {
        this.ctx.clearRect(0, 0, this.canvas.width, this.canvas.height);
  
        for (let i = 0; i < this.selectedItems.length; i++) {
          const item1 = document.getElementById(this.selectedItems[i][0]);
          const item2 = document.getElementById(this.selectedItems[i][1]);
          if (!item1 || !item2) continue;
          const rect1 = item1.getBoundingClientRect();
          const rect2 = item2.getBoundingClientRect();
          const x1 = rect1.left + rect1.width / 2;
          const y1 = rect1.top + rect1.height / 2;
          const x2 = rect2.left + rect2.width / 2;
          const y2 = rect2.top + rect2.height / 2;
  
          const lineKey = this.selectedItems[i].sort().join('-');
          const lineColor = this.linesColors[lineKey] || '#001d3d'; // Use stored color or default
          this.drawLine(x1, y1, x2, y2, lineColor);
  
          item1.classList.add('selected');
          item2.classList.add('selected');
        }
      },
      checkAns() {
        if (this.btnText === "בדוק אותי") {
          let correctCount = 0;
          const correctMatches = [];
  
          for (let i = 0; i < this.selectedItems.length; i++) {
            const selectedLine = this.selectedItems[i].sort();
            let isCorrect = false;
            for (let j = 0; j < this.correctLines.length; j++) {
              const correctLine = this.correctLines[j].sort();
              if (selectedLine[0] === correctLine[0] && selectedLine[1] === correctLine[1]) {
                isCorrect = true;
                correctCount++;
                correctMatches.push(i);
                break;
              }
            }
            const lineKey = this.selectedItems[i].sort().join('-');
            this.linesColors[lineKey] = isCorrect ? 'rgb(179, 241, 160)' : 'rgb(247, 83, 83)';
          }
  
          this.drawAllLines(); // Redraw lines with updated colors
  
          if (correctCount === this.correctLines.length) {
            this.btnText = "אתה מטורף!";
            // this.bgColor = "rgb(179, 241, 160)";
          } else {
            this.btnText = "הממ לא בדיוק...";
            // this.bgColor = "rgb(247, 83, 83)";
          }
        } else {
          this.bgColor = "#fce9a9";
          this.btnText = "בדוק אותי";
          this.linesColors = {}; // Reset colors
          this.drawAllLines(); // Redraw with default colors
        }
      },
      compareLines(userAns, correctAns) {
        const sortedUserAns = userAns.sort();
        const sortedCorrectAns = correctAns.sort();
        return sortedUserAns[0] === sortedCorrectAns[0] && sortedUserAns[1] === sortedCorrectAns[1];
      }
    }
  };
  </script>
  
  <style scoped>
  @font-face {
    font-family: "aduma";
    src: url("../assets/fonts/Aduma Regular.ttf");
  }
  
  #draw-lines {
    margin: 0;
    margin-top: 10%;
    height: fit-content;
    width: 100vw;
    position: relative;
    top: 0;
    right: 0;
  }
  #bg-container {
    list-style-type: none;
    padding: 1%;
    margin: auto;
    margin-top: 0%;
    background-color: #fce9a9;
    padding-bottom: 3%;
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
  .container {
    display: flex;
    justify-content: space-between;
    width: 100%;
    height: fit-content;
    align-self: center;
  }
  
  .selected {
    background-color: #001d3d;
  }
  
  .column {
    /* width: 20vw; */
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: space-between;
    /* margin-right: 2vw;
    margin-left: 2vw; */
  }
  
  .item {
    display: flex;
    flex-direction: row;
    align-items: center;
  }
  
  .dot {
    border-radius: 50%;
    display: inline-block;
    border: 0.8vw #001d3d solid;
    width: 4.5vw;
    height: 2.5vh;
    /* padding: 4vh; */
    margin-top: 4vh;
    margin-right: 0.5vw;
  }
  
  .second-dot {
    border-radius: 50%;
    display: inline-block;
    border: 0.8vw #001d3d solid;
    width: 4.5vw;
    height: 2.5vh;
    margin-top: 4vh;
    margin-left: 0.5vw;
  }
  
  .list-item {
    background-color: #001d3d;
    /* border: solid #ffc300 0.3vw; */
    border-radius: 2vw;
    margin-top: 12%;
    font-size: 5vw;
    text-align: center;
    width: 30vw;
    list-style-type: none;
    color: #ffc300;
    min-height: 10vh;
    padding-top: 3%;
    white-space: break-spaces;
    padding-bottom: 3%;
    /* font-weight: bolder; */
  
    display: flex;
    align-items: center;
    justify-content: center;
    box-shadow: rgba(0, 0, 0, 0.35) 0 0.5vh 0.5vh;
  }
  
  .covered-container {
    position: relative; /* Necessary for absolute positioning of canvas */
  }
  
  .overlay-canvas {
    position: absolute;
    top: 0;
    left: 0;
    pointer-events: none; /* Allow clicking through the canvas */
  }
  
  #checkBtn {
    margin-top: 6%;
    margin-right: 1%;
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
  </style>