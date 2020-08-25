<template>
  <div class="container">
    <div class="puzzle-container">
      <div
        class="puzzle-piece"
        :class="'piece' + n"
        v-for="(n, index) in getShuffledNumbers"
        :key="index"
        @click="movePiece(index)"
      >
        <div>{{ n }}</div>
      </div>
    </div>
    <div class="random-button" @click="randomizedNumbers(number)">
      Randomize
    </div>
  </div>
</template>

<script>
export default {
  name: "Puzzle",
  data() {
    return {
      number: 14,
      schuffledNumbers: []
    };
  },
  computed: {
    getShuffledNumbers() {
      return this.schuffledNumbers;
    }
  },
  methods: {
    // Creates the numbers based on the value you put in
    createNumbersArray(value) {
      var newNumbers = [];
      for (let i = 1; i < value + 1; i++) {
        newNumbers.push(i);
      }
      return newNumbers;
    },
    // Randomizes the numbers from createNumbersARray
    randomizedNumbers(value) {
      const createdNumbers = this.createNumbersArray(value);

      createdNumbers.forEach(i => {
        const r = Math.floor(Math.random() * i);
        const temporary = createdNumbers[i];
        createdNumbers[i] = createdNumbers[r];
        createdNumbers[r] = temporary;
      });
      createdNumbers.push("");
      this.schuffledNumbers = createdNumbers;
    },
    // Moves the pieces
    movePiece(index) {
      // Moves the piece to the left of the empty space
      if (this.schuffledNumbers[index + 1] === "") {
        this.schuffledNumbers.splice(
          index + 1,
          0,
          this.schuffledNumbers.splice(index, 1)[0]
        );
        // Moves the piece to the right of the empty space
      } else if (this.schuffledNumbers[index - 1] === "") {
        this.schuffledNumbers.splice(
          index - 1,
          0,
          this.schuffledNumbers.splice(index, 1)[0]
        );
        // Moves the piece under of the empty space
      } else if (this.schuffledNumbers[index - 5] === "") {
        const newIndex = index - 5;
        const oldIndex = index;
        this.schuffledNumbers.splice(
          newIndex,
          0,
          this.schuffledNumbers.splice(oldIndex, 1)[0]
        );
        this.schuffledNumbers.splice(
          oldIndex,
          0,
          this.schuffledNumbers.splice(newIndex + 1, 1)[0]
        );
        // Moves the piece over of the empty space
      } else if (this.schuffledNumbers[index + 5] === "") {
        const newIndex = index + 5;
        const oldIndex = index;
        this.schuffledNumbers.splice(
          newIndex,
          0,
          this.schuffledNumbers.splice(oldIndex, 1)[0]
        );
        this.schuffledNumbers.splice(
          oldIndex,
          0,
          this.schuffledNumbers.splice(newIndex - 1, 1)[0]
        );
      }
    }
  },
  mounted() {
    this.randomizedNumbers(this.number);
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  background: #000;
  color: #ffffff;
  .puzzle-container {
    display: flex;
    justify-content: flex-start;
    flex-wrap: wrap;
    background: #5a331a;
    border-radius: 1rem;
    border: 3px solid #27160b;
    width: 100%;
    max-width: 26.8rem;
    padding: 1rem;

    .puzzle-piece {
      display: flex;
      justify-content: center;
      align-items: center;
      background: #27160b;
      border-radius: 1.5rem;
      border: 1px solid #000;
      width: 5rem;
      height: 5rem;
      margin: 0.1rem;
      font-size: 30px;
      cursor: pointer;
      &.piece {
        border: 1px solid #5a331a;
        background: transparent;
        color: transparent;
        cursor: default;
      }
    }
  }
  .random-button {
    background: #5a331a;
    border-radius: 1rem;
    border: 3px solid #27160b;
    padding: 1rem 1.5rem;
    margin-top: 1rem;
    font-size: 20px;
    cursor: pointer;
  }
}
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
