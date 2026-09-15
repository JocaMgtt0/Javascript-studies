<template>
  <div class="calculator">

    <AppDisplay :value="displayValue" />
    <AppButton label="AC" triple @clicouBotao="clearMemory"/>
    <AppButton label="/" operation @clicouBotao="setOperation"/>
    <AppButton label="7" @clicouBotao="addDig"/>
    <AppButton label="8" @clicouBotao="addDig"/>
    <AppButton label="9" @clicouBotao="addDig"/>
    <AppButton label="*" operation @clicouBotao="setOperation"/>
    <AppButton label="4" @clicouBotao="addDig"/>
    <AppButton label="5" @clicouBotao="addDig"/>
    <AppButton label="6" @clicouBotao="addDig"/>
    <AppButton label="-" operation @clicouBotao="setOperation"/>
    <AppButton label="1" @clicouBotao="addDig"/>
    <AppButton label="2" @clicouBotao="addDig"/>
    <AppButton label="3" @clicouBotao="addDig"/>
    <AppButton label="+" operation @clicouBotao="setOperation"/>
    <AppButton label="0" double @clicouBotao="addDig"/>
    <AppButton label="." @clicouBotao="addDig"/>
    <AppButton label="=" operation @clicouBotao="setOperation"/>
   

  </div>
</template>

<script>
import AppDisplay from '../components/AppDisplay';
import AppButton from '../components/AppButton';



export default {


    data: function(){
      return {
        displayValue: "0",
        clearDisplay: false,
        operation: null,
        values: [0,0],
        current: 0
      }
    },

    components: {AppButton, AppDisplay},
    methods: {
      clearMemory(){
        Object.assign(this.$data, this.$options.data())
      },
      
      setOperation(operation){
        
        if(this.current === 0) {
          this.operation = operation
          this.current = 1
          this.clearDisplay = true
        }else{
          const equals = operation === "="
          const currentOperation = this.operation

          try{
            this.values[0] = eval(
              `${this.values[0]} ${currentOperation} ${this.values[1]}`
            )
          }catch (e){
            this.$emit('onError', e) 
          }

          this.values[1] = 0
          
          this.displayValue = this.values[0]
          this.operation = equals ? null : operation
          this.current = equals ? 0 : 1
          this.clearDisplay = !equals
        }

      },

      addDig(n){
        if(n === "." && this.displayValue.includes(".")){
          return
        }

        const clearDisplay = this.displayValue === "0" 
          || this.clearDisplay
        const currentValue = clearDisplay ? "" : this.displayValue
        const displayValue = currentValue + n
        
        this.displayValue = displayValue
        this.clearDisplay = false
        this.values[this.current] = displayValue
      }
    }
}
</script>

<style>

.calculator{
    height: 320px;
    width: 235px;
    border-radius: 5px;
    overflow: hidden;

    display: grid;
    grid-template-columns: repeat(4, 25%);
    grid-template-rows: 1fr 48px 48px 48px 48px 48px;
}

</style>