<template>
  <div class="calc container">
    <div class="display">{{ current || 0 }}</div>
    <div @click="clear"  class="button">C</div>
    <div @click="sign" class="button">+/-</div>
    <div @click="percent" class="button">%</div>
    <div @click="divide" class="button opr">/</div>
    <div @click="append('7')" class="button">7</div>
    <div @click="append('8')" class="button">8</div>
    <div @click="append('9')" class="button">9</div>
    <div @click="times" class="button opr">x</div>
    <div @click="append('4')" class="button">4</div>
    <div @click="append('5')" class="button">5</div>
    <div @click="append('6')" class="button">6</div>
    <div @click="minus" class="button opr">-</div>
    <div @click="append('1')" class="button">1</div>
    <div @click="append('2')" class="button">2</div>
    <div @click="append('3')" class="button">3</div>
    <div @click="add" class="button opr">+</div>
    <div @click="append('0')" class="button zero">0</div>
    <div @click="dot" class="button">.</div>
    <div @click="equal" class="button opr">=</div>
  </div>
  <div class="alert alert-danger" role="alert">
    <strong>{{error}}</strong>
  </div>
  
</template>

<script>
export default {
  name: 'HelloWorld',
  data(){
    return{
      previous : null,
      current :'',
      operator:null,
      operatorClicked: false,
      error:''
    }
  },
  methods:{
    setPrevious(){
      this.previous = this.current
      this.operatorClicked =true
    },
    clear(){
      this.current = ''
    },
    sign(){
      this.current = this.current.charAt(0) === '-' ? 
        this.current.slice(1) : `-${this.current}`
    },
    percent(){
      this.current = `${ parseFloat(this.current) / 100}`
    },
    append(num){
      if(this.operatorClicked){
        this.current=''
        this.operatorClicked = false
      }
       this.current = `${this.current}${num}`
    },
    //dot method
    dot(){
      if(this.current.indexOf('.') === -1 ){
        this.append('.')
      }
    },
    //add method
    add(){
      this.operator = (a,b) => a+b
      this.setPrevious()
    },
    //minus method
    minus(){
      this.operator = (a,b) => a-b
      this.setPrevious()

    },
    //times method
    times(){
      this.operator = (a,b) => a*b
      this.setPrevious()

    },
    //divide method
    divide(){
      this.operator = (a,b) => a/b
      this.setPrevious()
    },
    //equal method
    equal(){
      if(this.previous!=='0'){
        this.current = `${this.operator(parseFloat(this.current),parseFloat(this.previous))}` 
        }
        else{
          this.error = 'Divided By Zero ERROR'
        }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.calc{
  font-size: 2rem ;
  display:grid;
  grid-template-columns: repeat(4,1fr);
  grid-auto-rows: minmax(50px,auto);
}
.display{
  grid-column: 1 / 5;
  background:#333;
  color: white;
}
.zero{
  grid-column:1 / 3;
  text-align: center;
}
.button{
  background: #eee;
  border:1px solid black ;
}
.opr{
  background: orange;
  color: white;
}
</style>
