<script setup>
import {ref} from "vue";
import BlockComponent from "@/components/BlockComponent.vue";
import {generateSudoku, isValidSudoku} from "@/functions/sudokuGenerator";

const board = ref(generateSudoku().map((item) => {
  return item.map((el) => {
    return {
      name: el,
      status: false,
      disable: el !== null
    }
  })
}))

// Статус победы
const winStatus = ref(false)

const clearFunction = () => {
  board.value.forEach((item) => {
    item.forEach((el) => {
      el.status = false
    })
  })
}

const setNumber = (x,y, number) => {
  board.value[x][y].name = number
  winStatus.value = isValidSudoku(board.value.map(item => item.map(el => el.name)))
}

const createNewSudoku = () => {
  board.value = generateSudoku().map((item) => {
    return item.map((el) => {
      return {
        name: el,
        status: false,
        disable: el !== null
      }
    })
  })
  winStatus.value = false
}

</script>

<template>
  <button class="sudoku-button" @click="createNewSudoku"> New Sudoku </button>
<div class="sudoku-container">
  <Transition>
    <div v-if="winStatus" class="sudoku-overlay">
      <div class="sudoku-popup">
        <h3> Congratulations!!! You win!</h3>
        <p>You can repeat your success. Just push the button.</p>
        <button class="sudoku-button" @click="createNewSudoku">Push me</button>
      </div>
    </div>
  </Transition>
  <div>
    <div class="board" v-for="(element, index) in board" :key="index" >
      <block-component
          v-for="(item, idx) in element"
          :key="idx"
          :data="item"
          :x="index"
          :y="idx"
          :clearFunction="clearFunction"
          :setNumber="setNumber"
      />
    </div>
  </div>
</div>
</template>

<style lang="scss" scoped>
.board{
  display: flex;
}
.sudoku-container{
  display: flex;
  justify-content: center;
  position: relative;
}
.v-enter-active,
.v-leave-active {
  transition: opacity 0.35s ease;
}
.v-enter-from,
.v-leave-to {
  opacity: 0;
}
.sudoku-overlay{
  position: fixed;
  top: 0;
  right: 0;
  left: 0;
  bottom: 0;
  width: 100%;
  height: 100%;
  background: rgba(0,0,0, .7);
  z-index: 10;
  display: flex;
  justify-content: center;
  align-items: center;
}
.sudoku-popup{
  padding: 16px 20px 12px;
  display: flex;
  flex-direction: column;
  background: white;
}
.sudoku-button{
  outline: none;
  background: #252628;
  padding: 12px 24px;
  border-color: transparent;
  color: white;
  border-radius: 24px;
  margin-bottom: 24px;
  cursor: pointer;
}
</style>