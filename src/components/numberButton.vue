<template>
    <div @click="addNumber()" class="button">{{ number }}</div>
</template>
<script>
import { useCalcStore } from '@/stores/calc.ts'
export default {
    props: ['number'],
    methods: {
        addNumber() {

            if (this.number.toString() === 'CE') {
                useCalcStore().resetLast()
                return
            }
            if (this.number.toString() === 'C') {
                useCalcStore().resetAll()
                return
            }

            if (['-', '+', '/','x'].includes(this.number.toString())) {
                useCalcStore().savePrevFigure()
                useCalcStore().setOperation(this.number.toString())
                useCalcStore().resetLast()
                return
            }
            if (this.number.toString() === 'radice') {
                return
            }
            if (this.number.toString() === '%') {
                return
            }
            if (this.number.toString() === '=') {

                useCalcStore().printStoreValues()
                useCalcStore().getResult()
                return
            }
            useCalcStore().addDigit(this.number.toString())

            console.log(useCalcStore().figureShown);
        }
    },
}
</script>
<style>
.button {
    background-color: green;
    width: 50px;
    height: 50px;
    margin-right: 10px;
    margin-bottom: 10px;
    display: flex;
    justify-content: center;
    align-items: center;

}
</style>