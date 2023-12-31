<script>
import numberButton from '../components/numberButton.vue'
import { useCalcStore } from '@/stores/calc.ts'

export default {
  components: {
    numberButton
  },
  data() {
    return {
      buttonsList: [['%', '√', 'CE', 'C'], [7, 8, 9, '-'], [4, 5, 6, '/'], [1, 2, 3, 'x'], ['.', 0, '=', '+']],


    }
  },
  computed: {
    result() {
      const res = useCalcStore().figureShown
      if (res.includes('NaN')) {
        useCalcStore().resetAll()
        return ''
      }
      else {return res}
    },
    prevResult(){
      let res = useCalcStore().prevFigureShown + ' ' + useCalcStore().operation + ' ' +  useCalcStore().secondPrevFigureShown
      if (useCalcStore().operation === '%') res = ''// temporary
      return res
    }
  },
}
</script>

<template>
  <div class="calc">
    <div class="title">Calculator</div>
    <div class="prevResult"> {{prevResult}} </div>
    <div class="result">{{ result }}</div>
    <div v-for="line in buttonsList" :key="line" class="line">
      <div v-for="number in line" :key="number">

        <numberButton :number="number"></numberButton>
      </div>
    </div>
  </div>
</template>

<style scoped>
.calc {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  border: 3px green;
  scale: 1.5;
}

.title {
  text-align: center;
}

.result {
  text-align: right;
  width: 230px;
  height: 25px;
  background-color: greenyellow;
  margin-top: 10px;
  margin-bottom: 10px;
}
.prevResult{
  text-align: right;

}
.line {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  width: 200px;
}

.button {
  width: 50px;
}
</style>
