
<script>
export default{
  data(){
    return {
      current: '',
      firstNum: 0,
      secondNum: 0,
      currentOperator: '',
      operatorClicked: false
    }
  },
  methods:{
    clearAll(){
      this.current = '';
    },
    clear(){
      this.current = this.current.slice(0,-1);
    },  
    sign(){
      if( this.current.charAt( 0 ) == '-' ){
        this.current = this.current.slice(1);
      }
      else if( this.current.charAt(0) == 0 ){
        return ;
      }
      else{
        this.current = "-" + this.current;
      }
    },
    percentage(){
      this.current = ( parseFloat( this.current ) / 100.0 ).toString();
    },
    decimalPoint(){
      //TODO: make sure dot only comes if no other dot operator is present
      if( this.current.includes( '.' ) ){
        return ;
      }
      this.current = this.current + ".";
    },
    operator( op ){
      this.currentOperator = op;
      this.firstNum = parseFloat( this.current );
      this.operatorClicked = true;
    },
    append( number ){
      if( this.current.length >= 8 ){
        return ;
      }
      if( this.operatorClicked ){
        this.current = number;
        this.operatorClicked = false;
      }
      else{
        this.current = this.current + number;
      }
    },
    solve(){
      this.secondNum = parseFloat( this.current );
      this.operatorClicked = false;
      if( this.currentOperator == '+' )
        this.current = ( this.firstNum + this.secondNum ).toString();
      else if( this.currentOperator == '-' )
        this.current = ( this.firstNum - this.secondNum ).toString();
      else if( this.currentOperator == 'x' )
        this.current = ( this.firstNum * this.secondNum ).toString();
      else if( this.currentOperator == '÷' )
        this.current = ( this.firstNum / this.secondNum ).toString();
      else  
        this.current = this.secondNum;
      if( this.current.length >= 8 ){
        this.current = this.current.slice( 0, 8 );
      }
      console.log( this.current );
    }
  }
}
</script>

<template>
  <div class="calculator">
    <div class="display">
      <span class="display_span">
        {{current || 0 }}
      </span> 
    </div>
    <div @click="clearAll" class="button specialButtons">AC</div>
    <div @click="clear" class="button specialButtons">C</div>
    <div @click="percentage" class="button specialButtons">%</div>
    <div @click="operator( '÷' )" class="button op">÷</div>
    <div @click="append( '7' )" class="button">7</div>
    <div @click="append( '8' )" class="button">8</div>
    <div @click="append( '9' )" class="button">9</div>
    <div @click="operator( 'x' )" class="button op">x</div>
    <div @click="append( '4' )" class="button">4</div>
    <div @click="append( '5' )" class="button">5</div>
    <div @click="append( '6' )" class="button">6</div>
    <div @click="operator( '-' )" class="button op">-</div>
    <div @click="append( '1' )" class="button">1</div>
    <div @click="append( '2' )" class="button">2</div>
    <div @click="append( '3' )" class="button">3</div>
    <div @click="operator( '+' )" class="button op">+</div>
    <div @click="append( '0' )" class="button zero">0</div>
    <div @click="decimalPoint" class="button">.</div>
    <div @click="solve" class="button op">=</div>
    <div class="footer">
      <span class="footer_span">
        Calculator
      </span>
    </div>
  </div>
</template>

<style scoped>

.calculator{
  background-color: black;
  width: 400px;
  margin-left: 50px;
  text-align: center;
  font-size: 40px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(90px, auto);
  border-radius: 25px;
  overflow: hidden;
}

.footer{
  grid-column: 1/5;
  background-color: black;
  font-size: 30px;

}
.footer_span{
  position: absolute;
  bottom: 25px;
  right: 10px;
}

.display{
  background-color: black;
  position: relative;
  grid-column: 1/5;
  grid-row: 1/3;
  color: white;
  text-align: right;
  padding-right: 10px;
  font-size: 90px;
}

.display_span{
    position: absolute;
    bottom: 0;
    right: 10px;
}

.zero{
  grid-column: 1/3;
  text-align: left;
  padding-left: 22%;
}

.button{
  border-radius: 100px;
  background-color: #505050;
  color: black;
  /* border: 1px solid #999; */
  font-size: 50px;
  color: white;
  margin: 10px;
}

.specialButtons{
  background-color: #D4D4D2;
  color: black;
}

.op{
  text-align: center;
  background-color: #FF9500;
  color: black;
  line-height: 65px;
}
</style>