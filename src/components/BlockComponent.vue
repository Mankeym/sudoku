<script setup>
import {defineProps} from "vue";
const props = defineProps({
  data: Object,
  clearFunction: Function,
  setNumber: Function,
  x: String,
  y: String
})

const setStatusTooltip = () => {
  if(props.data.status === true){
    // eslint-disable-next-line vue/no-mutating-props
    props.data.status = false
  } else {
    props.clearFunction();
    // eslint-disable-next-line vue/no-mutating-props
    props.data.status = true
  }


}
</script>

<template>
<div
    :class="{
      'border-right': props.x % 3 === 2 && props.x !== 8 ,
      'border-bottom': props.y % 3 === 2 && props.y !== 8 ,
      'sudoku-block_disabled': props.data.disable
    }"
    class="sudoku-block"
    @click.prevent="setStatusTooltip">
  <p>{{props.data.name}}</p>

  <div :class="{ 'sudoku-block__tooltip_active': props.data.status  }" class="sudoku-block__tooltip">
    <p v-for="(num, idx) in 9" :key="idx" @click="setNumber(x,y,num)"> {{ num }}</p>
  </div>
</div>
</template>

<style lang="scss" scoped>
.sudoku-block{
  position: relative;
  width: 48px;
  padding: 12px;
  cursor: pointer;
  transition: .35s;
  border: 1px solid black;
  &.border-right{
    border-bottom: 3px solid black;
  }
  &.border-bottom{
    border-right: 3px solid black;
  }
  &_disabled{
    pointer-events: none;
    background: rgba(200, 200, 200, 0.3);
  }
  &:hover{
    background: rgba(97, 218, 251, 0.3);
  }
  &__tooltip{
    position: absolute;
    bottom: -90%;
    right: -100%;
    display: flex;
    gap: 8px;
    border-radius: 12px;
    padding: 2px 16px;
    background: white;
    box-shadow: 1px 1px 1px 1px #d6d6d6;
    z-index: 5;
    transition: .35s;
    opacity: 0;
    visibility: hidden;
    p{
      cursor: pointer;
      padding: 4px;
      transition: .35s;
      &:hover{
        background: #61dafb;
      }
    }
    &_active{
      opacity: 1;
      visibility: visible;
    }
  }
}

</style>