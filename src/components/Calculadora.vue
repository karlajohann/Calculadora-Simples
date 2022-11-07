<template>
  <div class="p-3" style="max-width: 400px; margin: 50px auto; background: #234">

    <!--Resultados da Calculadora-->
    <div class="w-full rounded m-1 p-3 text-right lead font-weight-bold text-white bg-vue-dark">
      {{ calculatorShowValue || 0 }}
    </div>
      
    <!--Botões da calculadora-->
    <div class="row no-gutters">
      <div class="col-3" v-for="n in calculatorElements" :key="n">
        <div class="lead text-white text-center m-1 py-3 bg-vue-dark rounded hover-class"
        :class="{'bg-vue-green': ['C','/','*','-','+','%','='].includes(n)}"
        @click="action(n)"
        >
          {{n}}
        </div>
        
      </div>
    </div>

  </div>
</template>

<script>
export default {
  name: 'Calculadora-vue', 
  props: {
    msg: String
  },
  data() {
    return {
      calculatorShowValue:'',     //valor que vai ser mostrado na tela
      calculatorValue: '',        // valor que vai ser calculado
      resultFlag:false,           //um boolean para indicar se o botão '=' ja foi clicado
      calculatorElements: ['C','/','*','-',7,8,9,'+',4,5,6,'%',1,2,3,'=',0,'.'],
      operator: null, 
      previousCalculatorValue: '',
    }
  },
  methods: {
    action(n) {
      /* Adicionar valor */
      if(!isNaN(n) || n=== '.') {
  
        if(this.resultFlag){
          this.calculatorValue = '';
          this.calculatorShowValue='';
          this.resultFlag =false;     // seta para falso de novo até relizar outra operação de =
        }
        this.calculatorValue += n + '';
        this.calculatorShowValue+= n;
      }
      /* Botão C para limpar os valores */
      if( n === 'C') {
        this.calculatorValue = '';
        this.calculatorShowValue='';
      }
      /* Botão de porcentagem */
      if( n === '%') {
        this.calculatorValue = this.calculatorValue / 100 + '';
        this.calculatorShowValue=this.calculatorValue;// depois de fazer o calculo na linha acima o valor pra mostrar na tela recebe o valor real calculado
      }
      /* Botões de comandos soma, subtração, multiplicação e divisão */
      if(['/','*','-','+'].includes(n)) {
        console.log(n);
        this.calculatorShowValue = this.calculatorValue + n; // aqui ele agrupa o numero + o operador pra mostrar na tela
        this.operator = n;
        this.previousCalculatorValue = this.calculatorValue;
        this.calculatorValue = '';
        this.resultFlag=false;
        // deixa false caso queira realizar mais operações continuando com o valor dado depois do '=' da operação
      }
      if( n === '=') {
        this.calculatorValue = eval (
          this.previousCalculatorValue + this.operator + this.calculatorValue
        );
        this.calculatorShowValue = this.calculatorValue;
        this.resultFlag = true;     //seta flag para true para indicar que houve uma operação de =
        this.previousCalculatorValue = '';
        this.operator = null; 
      }
    }
  }
}
</script>


<style scoped>
  .bg-vue-dark {
    background: #31475e;
  }
  .hover-class:hover {
    cursor: pointer;
    background: #3d5875;
  }
  .bg-vue-green {
    background: #3fb984;
  }
</style>